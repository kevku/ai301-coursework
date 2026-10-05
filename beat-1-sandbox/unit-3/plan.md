# Plan: Webhook notifications when a review is ready (#35)

  

**Issue:** [#35](https://github.com/codepath/pathreview-ai301-fa26-s1/issues/35), "Implement a webhook system that notifies users when their review is ready" (est. 8–12h)

**Repro comment:** [my unit 2 reproduction](https://github.com/codepath/pathreview-ai301-fa26-s1/issues/35#issuecomment-5863874875)

**Branch base:** `kevku/pathreview-ai301-fa26-s1` at `f89c06f` on `main`

  

## 1. Diagnosis

  

Reviews over multiple repositories are expected to take 30–90 seconds. Today the only way a client can learn that a review has finished is by polling `GET /reviews/{id}/status`. My repro comment states the problem this way:

  

> The issue wants to implement a webhook because for longer reviews, we can reduce the amount requests made to the server. The current model makes a request every 3 seconds to the server.

  

The polling comes from the frontend hook `frontend/src/hooks/useReviewStatus.ts`. On the server side, `process_review` runs as an in-process FastAPI background task and only updates the review's status in the database. There is no webhook, callback, notification, queue, pub/sub, websocket, SSE, or outbound `POST` anywhere in the codebase. The only outbound HTTP is `httpx.get` / `httpx.head` to GitHub in `agent/tools/github_tool.py`, and there is no table or column for storing callbacks. My repro confirms this from the route side:

  

> There is no pre-existing `webhook` as part of the route and from the evidence, the behavior of it shows polling rather than the effects of a webhook.

  

The goal is to let a client register a callback URL once and receive a `POST` with the review payload when processing finishes, so it no longer has to poll.

  

## 2. Reproduction evidence (from my unit 2 repro comment)

  

**Environment:** macOS Tahoe v26.4.1, Docker 29.5.2, Python 3.14.4, `kevku/pathreview-ai301-fa26-s1` at `f89c06f` on `main` with a clean working tree.

  

The real pipeline returns hardcoded data and finishes in milliseconds, so I simulated a long review. As I wrote in the repro:

  

> in the function `_run_rag_retrieval_generation` in `core/services/review_service.py` has hardcoded data which is why I chose to simulate the processing time of 30-90 seconds.

  

Steps, as posted:

  

1. Added `debug_review_delay_seconds: int = 0` inside the `Settings` of `core/config.py`.

2. Added `import asyncio` and `from core.config import settings` at the top of `core/services/review_service.py`.

3. Added, right before the `return` of `_run_rag_retrieval_generation`:

```python

if settings.debug_review_delay_seconds:

await asyncio.sleep(settings.debug_review_delay_seconds)

```

4. Ran `docker compose up -d`, `make setup`, `make run`.

5. Went to `http://localhost:5173` and logged in as `user1@example.com` / `password1`.

6. Clicked **Start a New Review**, opened the browser's Network tab, and filtered on `status`.

7. Entered `octodad` as the GitHub username and uploaded an empty `test.txt`.

  

The evidence I relied on (Network tab screenshots of the full waterfall, a `processing` response, and the final `complete` response):

  

> In my example I used 45 seconds as a test case and we can see around ~15 requests that has `status: processing` from the waterfall and the final being `status: complete`.

  

> These images show that while a review is ocuring, the client is continuously requesting from the server for the status of the review.

  

So a 45-second review costs about 15 status requests, one every 3 seconds, and nothing notifies the client when the review finishes.

  

**Note on the debug delay:** this change is a local reproduction aid only. It stays uncommitted and **out of the repo and the PR**; I will stash or revert it before committing. It is listed as out of scope in section 7.

  

## 3. Design decisions

  

### 3.1 Registration model: per-user webhook resource

Clients register webhooks through a new `/webhooks` resource owned by the user. This matches the issue wording ("register a callback URL") and the suggested `api/routes/webhooks.py`. A user can register **several webhooks** (up to 10). Each one fires for every review on any of the user's profiles. At delivery time the owner is found from the review's profile (`profile.user_id`), which `process_review` already loads. All list/get/delete operations enforce ownership: another user's webhook returns 404, the same way `get_review` handles reviews.

  

A per-review `callback_url` on `POST /reviews` is **not** included. It could be added later on top of the same delivery service.

  

### 3.2 Events

Two event types:

- `review.completed`: status became `complete`.

- `review.failed`: status became `failed` (profile not found, safety check failed, or an unexpected exception).

  

Without `review.failed`, a client that has stopped polling would wait forever on a failed review. Each webhook stores the list of events it subscribes to, defaulting to both.

  

Three code paths in `process_review` (`core/services/review_service.py`) set `failed`:

  

| Path | Line (approx.) | Webhook behavior |

|---|---|---|

| Profile not found | 119 | **No delivery.** `profile` is `None`, so there is no owner to notify. Logged as `webhook_dispatch_skipped` with `reason="no_owner"`. |

| Safety check failed | 155 | `review.failed` sent |

| Catch-all `except` | 193 | `review.failed` sent |

  

All three go through one helper, `_mark_failed(db, review, message)`. It sets the status, sets `error_message`, commits, then dispatches. This way no failure path can skip the notification.

  

**`error_message` is never set today.** Nothing in `api/` or `core/` writes to the column, so every `review.failed` payload would carry `null`. The helper fixes this with a **safe, generic message** per path. Raw exception text is never stored or sent; it goes to the structlog error log only.

- Profile not found: `"Profile not found."`

- Safety check failed: `"Review did not pass safety checks."`

- Unexpected error: `"An internal error occurred while processing the review."`

  

### 3.3 Payload

An event envelope wrapping the existing `ReviewResponse`, so clients get the same shape they already get from `GET /reviews/{id}`:

  

```json

{

"id": "evt_<uuid>",

"type": "review.completed",

"created_at": "2026-10-04T18:30:00Z",

"data": {

"id": "...", "profile_id": "...", "status": "complete",

"sections": [ ... ], "overall_score": 0.82,

"error_message": null, "created_at": "...", "updated_at": "..."

}

}

```

  

Headers sent with each delivery:

- `Content-Type: application/json`

- `User-Agent: PathReview-Webhooks/1.0`

- `X-PathReview-Event`: event type

- `X-PathReview-Delivery`: event id (lets receivers deduplicate retries)

- `X-PathReview-Timestamp`: Unix seconds

- `X-PathReview-Signature`: `sha256=<hex HMAC>` (see 3.5)

  

### 3.4 Delivery

- **Trigger point:** in `process_review()` (`core/services/review_service.py`), after each commit that sets a terminal status: the success commit (around line 172) sends `review.completed`, and the `_mark_failed` helper (see 3.2) sends `review.failed` for the safety-check and `except` paths. Both call `dispatch_review_event(review_id, event_type)`.

- **Isolation:** the dispatch call is wrapped so that **no delivery error can change the review's status or raise out of `process_review`**. Delivery happens only after the status commit, never before.

- **Own session:** `dispatch_review_event` opens its own session via `AsyncSessionLocal()` rather than reusing the request-scoped session passed to the background task. It reloads the review there, so the payload reflects committed state.

- **Lookup:** Review → Profile → User, then the user's active webhooks subscribed to the event. If no owner can be found (the profile-not-found path, or a profile deleted mid-review), dispatch logs `webhook_dispatch_skipped` and returns.

- **HTTP:** `httpx.AsyncClient` with a 5s timeout and `follow_redirects=False`. Deliveries to multiple webhooks run concurrently with `asyncio.gather`.

- **Retries:** `tenacity`, up to 3 attempts with exponential backoff (1s, 2s), retrying only on network errors, timeouts, 5xx, and 429. Other 4xx responses are not retried. Worst case the background work is bounded to roughly 20 seconds per webhook.

- **Record of attempts:** structlog, following existing conventions: `webhook_delivery_succeeded`, `webhook_delivery_retrying`, `webhook_delivery_failed`, with `webhook_id`, `review_id`, `event_type`, `attempt`, `status_code`. There is no deliveries table.

- **Last delivery status:** after all deliveries finish, dispatch writes `last_delivery_status` (`"succeeded"` or `"failed"`) and `last_delivery_at` on each webhook it called, in its own session. These show in `GET /webhooks`, so users can see whether their endpoint is working. A failure to write these columns is logged and ignored.

- **Tradeoffs of log-only delivery, stated openly:**

- No delivery history beyond the last status, and no way to resend a missed notification. A client that misses one can still fall back to `GET /reviews/{id}`.

- Delivery and its retries run in-process through FastAPI `BackgroundTasks` (no queue), like review processing itself. A server restart drops any pending delivery or retry.

- A durable queue (Redis), a deliveries table, and a redelivery endpoint are out of scope.

  

### 3.5 Security

- **SSRF protection:**

- At registration: require `https` (and `http` only when the dev setting below is on), reject URLs with credentials, and reject hosts that resolve to private, loopback, link-local (including `169.254.169.254`), reserved, multicast, or unspecified addresses (checked with the `ipaddress` module).

- At delivery: resolve and check the host again, to guard against DNS rebinding. Redirects are not followed.

- Checking only at registration is not enough: a hostname that passes then could later resolve to an internal address. So the delivery-time check resolves the hostname and validates every resulting IP before connecting.

- A `webhook_allow_private_urls: bool = Field(default=False)` setting in `core/config.py` (same style as the other settings) allows `http://localhost` receivers for local development, tests, and the demo. It is off by default and applies at both check points.

- **Signing:** each webhook gets a secret from `secrets.token_urlsafe(32)`, returned **only once** in the `POST /webhooks` response. The signature is HMAC-SHA256 over `"{timestamp}.{raw_body}"`, so receivers can verify authenticity and reject replays. The secret must be stored retrievably (HMAC needs the raw value), so it is never included in list/get responses or logs.

- **Ownership:** every webhook endpoint filters by `user_id = current_user.id`. A webhook belonging to another user returns **404**, consistent with how `get_review` handles reviews you don't own.

- **Abuse limit:** at most 10 webhooks per user (409 Conflict when exceeded).

  

## 4. API

  

All endpoints require the existing Bearer JWT (`get_current_user`).

  

| Method | Path | Body / result |

|---|---|---|

| `POST` | `/webhooks` | `{url, events?, description?}` → **201** `WebhookCreatedResponse` (includes `secret`, shown once) |

| `GET` | `/webhooks` | → **200** list of `WebhookResponse` (no secret) |

| `GET` | `/webhooks/{id}` | → **200** `WebhookResponse`, or 404 |

| `DELETE` | `/webhooks/{id}` | → **204**, or 404 |

  

Validation errors (bad scheme, blocked address, unknown event type) return **422**. Routes follow the existing pattern: thin wrappers with try/except, re-raise `HTTPException`, map anything else to 500.

  

## 5. Data model

  

New `webhooks` table (Alembic migration **003_add_webhooks**):

  

| Column | Type | Notes |

|---|---|---|

| `id` | UUID str, PK | same style as other models |

| `user_id` | FK → `users.id` | `ON DELETE CASCADE`, indexed |

| `url` | `String(2048)` | |

| `secret` | `String` | never returned after creation |

| `events` | JSON | list of event types |

| `description` | `String`, nullable | |

| `is_active` | `Boolean` | default true |

| `last_delivery_status` | `String`, nullable | `succeeded` / `failed`; null until first delivery |

| `last_delivery_at` | timestamp, nullable | |

| `created_at`, `updated_at` | timestamps | |

  

`User` gets a `webhooks` relationship. No schema changes to the `reviews` table (the existing `error_message` column starts being populated; see 3.2).

  

## 6. Files to change

  

**New**

- `core/models/webhook.py`: `Webhook` model (export from `core/models/__init__.py`).

- `api/schemas/webhook.py`: `WebhookCreate`, `WebhookResponse`, `WebhookCreatedResponse`, `WebhookEvent`, `WebhookEventPayload`.

- `core/services/webhook_service.py`: module-level async functions, matching existing services: `create_webhook`, `list_webhooks`, `get_webhook`, `delete_webhook`, `validate_callback_url`, `sign_payload`, `deliver`, `dispatch_review_event`.

- `api/routes/webhooks.py`: the four endpoints above.

- `alembic/versions/003_add_webhooks.py`.

- `tests/unit/test_webhook_service.py`, `tests/unit/test_webhook_routes.py`.

  

**Modified**

- `api/main.py`: register the webhooks router.

- `core/config.py`: `webhook_timeout_seconds: float = Field(default=5.0)`, `webhook_max_attempts: int = Field(default=3)`, `webhook_allow_private_urls: bool = Field(default=False)`. All have safe defaults, so no `.env` changes are required to run normally.

- `core/services/review_service.py`: add the `_mark_failed` helper used by all three failure paths (lines ~119, ~155, ~193), set a generic `error_message` on each, and call `dispatch_review_event` after the success commit and inside `_mark_failed`.

- `core/models/user.py`: `webhooks` relationship.

  

## 7. Out of scope

- Frontend changes (the frontend keeps polling; it could switch later).

- Wiring the real LLM (`ReviewGenerator`) into the pipeline.

- A durable delivery queue (Redis/worker), a `webhook_deliveries` table, and redelivery endpoints.

- Per-review `callback_url`, webhook update (`PATCH`), and secret rotation.

- The `DEBUG_REVIEW_DELAY_SECONDS` reproduction change (stays local, never committed).

- `progress_pct` always being 0.

- Unrelated bugs, to be filed as separate issues:

- `_run_ingestion_pipeline` passes `raw_data=` to `IngestedSource`, which has no such column.

- `api/routes/health.py` reads `settings.redis_host` / `redis_port`, which don't exist, so the Redis check always reports unhealthy.

  

## 8. Unit tests

  

Unit tests follow existing conventions (`@pytest.mark.unit`, `@pytest.mark.asyncio`, `AsyncMock` sessions, `patch("core.services.<module>.<Name>")`). `pytest-httpserver` acts as the callback receiver. Because it listens on localhost, **delivery tests patch `webhook_allow_private_urls` to `True`**.

  

**URL validation (setting `False`, the default)**

- Accepts a public `https` URL.

- Rejects `ftp://`, URLs with credentials, `127.0.0.1`, `localhost`, `10.0.0.1`, `192.168.1.1`, `169.254.169.254`, and `[::1]`.

- Rejects the pytest-httpserver URL at registration **and** at delivery (no `POST` reaches the receiver).

- Delivery-time check: a hostname that passed registration but now resolves to a private IP (resolver patched) is blocked.

- With the setting `True`, `http://localhost` is accepted.

  

**Failure paths**

- Safety check failed: `review.failed` sent, `error_message` is the generic safety message.

- Unexpected exception: `review.failed` sent, `error_message` is the generic internal-error message, and the raw exception text does not appear in the payload.

- Profile not found: review is `failed` with `"Profile not found."`, no delivery attempted, `webhook_dispatch_skipped` logged.

  

**Signing**

- Signature matches an independently computed HMAC; changing the body or timestamp changes it.

  

**Delivery**

- Completed review: the receiver gets one `POST` with the correct envelope, `data` matching `ReviewResponse`, and all headers.

- Failed review: `review.failed` is sent with `error_message` populated.

- Webhook subscribed only to `review.completed` receives nothing on failure.

- Receiver returns 500 twice, then 200: three attempts, success logged.

- Receiver returns 400: one attempt, no retry.

- Receiver times out: retries, then gives up and logs `webhook_delivery_failed`.

- Redirect response is not followed.

- A user with two webhooks: both receive the event.

- After a successful delivery, `last_delivery_status` is `succeeded` and `last_delivery_at` is set; after exhausted retries, it is `failed`.

  

**Isolation**

- With `dispatch_review_event` patched to raise, `process_review` still leaves the review `complete` and does not raise.

- Dispatch opens its own `AsyncSessionLocal` session.

  

**Routes and ownership**

- Create returns 201 with the secret; list and get never include it.

- User2 gets 404 for user1's webhook on get and delete.

- 11th webhook returns 409; invalid URL returns 422; unauthenticated returns 401.

  

**CI checks:** `make lint`, `make format`, `make typecheck`, `make test-unit` all pass. The migration upgrades and downgrades cleanly on a fresh `make reset-db`.

  

## 9. Test plan: unit 2 repro re-run, with expected results after the fix

  

**Setup.** Apply the same local debug-delay change from section 2 (steps 1–3), then set in `.env`:

```

DEBUG_REVIEW_DELAY_SECONDS=45

WEBHOOK_ALLOW_PRIVATE_URLS=true

```

`WEBHOOK_ALLOW_PRIVATE_URLS` is needed only because the test receiver runs on localhost, which the SSRF check blocks by default. Start a small local receiver on port 9000 that logs incoming `POST` bodies and headers (kept out of the repo).

  

**Re-run of the unit 2 steps:**

1. `docker compose up -d`, `make setup` (applies migration 003), `make run`.

2. Register a webhook first. The frontend has no webhook UI, so use Swagger (`http://localhost:8000/docs`): log in as `user1@example.com` / `password1`, call `POST /webhooks` with `{"url": "http://localhost:9000/hook"}`, and save the returned secret. **Expected:** 201, and the secret appears only in this response.

3. Go to `http://localhost:5173`, log in as user1, click **Start a New Review**, and open the Network tab filtered on `status`.

4. Enter `octodad` as the GitHub username and upload an empty `test.txt`.

  

**Expected after the fix:**

- About 45 seconds after the review starts, the receiver gets **one** `POST` with `X-PathReview-Event: review.completed`, a signature that verifies with the saved secret, and the full review (sections, score, `status: complete`) in `data`.

- The Network tab looks **the same as in unit 2** (about 15 `processing` responses, then `complete`). This is expected: the browser frontend can't receive webhooks, and changing it is out of scope (see section 11).

- To show the polling-free path, repeat the review using only Swagger (`POST /reviews` with the profile id) and don't call `/status`. The receiver still gets the `POST` after about 45 seconds, with zero status requests.

  

**Additional checks:**

- Force a failure (for example, have the safety check fail) and confirm the receiver gets `review.failed` with a generic `error_message`, not raw exception text.

- Log in as `user2@example.com` and confirm `GET /webhooks/{user1's id}` returns 404.

- The unit tests in section 8 pass, along with `make lint`, `make format`, `make typecheck`, and `make test-unit`.

  

## 10. Risks and unknowns

  

**Risks**

- **In-process delivery** is lost on restart. This is documented, and the same limitation already applies to review processing.

- **Retries extend background task lifetime** by up to about 20 seconds per webhook. This is bounded by the timeout and attempt settings.

- **Plaintext secret storage** is required for HMAC. It is mitigated by never returning or logging the secret after creation.

- **DNS-based SSRF checks** cannot fully close the gap between resolution and connection. The check at delivery time plus no redirects covers the common cases.

  

**Unknowns**

- **Does this meet the issue's goal for the browser?** My repro framed the problem as reducing the frontend's polling. Webhooks are server-to-server: a browser can't host a callback URL, so the frontend will keep polling after this change. The benefit is for API clients that register a webhook. Reducing the browser's polling would need something like SSE or websockets, which I will raise with the maintainers rather than build here.

- **Is `review.failed` and setting `error_message` welcome?** The issue only mentions completion. I will ask in the plan comment.

- **Real-world timing.** The pipeline is stubbed, so delivery has only been exercised against a simulated 45-second delay, not a real LLM run.

- **The background task reuses the request-scoped db session.** Webhook dispatch avoids this by opening its own session, but I have not verified whether the existing pattern causes problems under load. Not fixing it here.

  

## Deviations

The design held: same endpoints, events, signing, and SSRF approach. These implementation details changed:

- **Dispatch uses two short database sessions** instead of one, so a connection isn't held open through up to ~20s of retries.
- **Added `await db.rollback()`** before marking a review failed in the catch-all `except`; otherwise a database error leaves the session unusable and `review.failed` is never sent.
- **Stricter URL check:** also rejects any address that isn't `is_global`, which catches CGNAT (`100.64.0.0/10`).
- **3xx responses are permanent failures** (not retried), where the plan only said redirects aren't followed.
- **Timeout test uses a mocked client** raising `httpx.ReadTimeout`, since a slow pytest-httpserver handler leaked into the next test.
- **Ownership is tested at the route and the service** (compiled SQL filters on `webhooks.user_id`), since unit tests have no real database.
- **`user_id` is typed `UUID | str`** rather than extending the mypy arg-type override.
- **Test typing fix:** annotated the fake store in `test_webhook_routes.py` to pass mypy and ruff.
- **Setup:** migration 003 is applied with `make migrate`, not `make setup` as section 9 said.