# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

kevku

**Plan comment**

[Link to Comment](https://github.com/codepath/pathreview-ai301-fa26-s1/issues/35#issuecomment-5987055189)


Following up on my repro comment: with a simulated 45-second review, the client made ~15 GET /reviews/{id}/status requests (one every 3s) before seeing complete. Nothing on the server notifies a client when a review finishes. process_review only updates the status in the database, and there is no outbound POST anywhere in the codebase.

Approach: add per-user webhooks. A client registers a callback URL once, and when a review reaches complete or failed, PathReview sends a signed POST with the event type and the same review payload as GET /reviews/{id}.

In scope:

POST/GET/DELETE /webhooks in a new api/routes/webhooks.py. Each user can register several webhooks and can only see or delete their own (404 otherwise).
A new core/services/webhook_service.py that validates callback URLs (blocking localhost, private, and cloud-metadata addresses), signs each payload with an HMAC of a per-webhook secret shown once at creation, and delivers with a timeout and up to 3 retries.
A new Webhook model, schemas, and Alembic migration 003_add_webhooks.
In core/services/review_service.py, notify after the review's final status is saved. A delivery failure can never change the review's status. The three failure paths go through one helper that also sets a generic error_message, which is currently never set.
Out of scope: frontend changes, wiring the real LLM, a durable delivery queue or delivery history, and the two unrelated bugs I noticed (ingestion's raw_data column and the Redis health check), which I'll file separately. My debug-delay change stays local.

Testing:

Unit tests with pytest-httpserver as the receiver, covering URL validation, signatures, retries, ownership, and each failure path.
Re-running my repro steps with a webhook registered: the receiver should get one review.completed POST about 45s in. Creating a review through the API alone should need zero status requests.
Questions for maintainers:

A browser can't receive webhooks, so the frontend will keep polling after this change; the benefit is for API clients. Is that the intended scope, or would you like a follow-up issue for SSE or websockets to reduce the frontend's polling?
Is it OK to also send review.failed and set a generic error_message on failures, or should this PR only cover completion?

---

## Your branch

**Branch**

`feat/35-webhook-notifications`

**Evidence**

## Before (main, `f89c06f`): polling only

Same steps as my [Unit 2 repro](https://github.com/codepath/pathreview-ai301-fa26-s1/issues/35#issuecomment-5863874875), with `DEBUG_REVIEW_DELAY_SECONDS=45` to simulate a long review (local only, not in this PR):

```
docker compose up -d
make setup
make run
```

1. Logged in at `http://localhost:5173` as `user1@example.com`.
2. Clicked **Start a New Review**, opened DevTools → Network filtered on `status`.
3. Entered `octodad` and uploaded an empty `test.txt`.

Result: about 15 `GET /reviews/{id}/status` requests, one every 3s, returning `processing` until the final response:

```json
{"review_id": "0693e698-c35c-4215-abf1-7dc60660a4d5", "status": "complete", "progress_pct": 0}
```

There was no webhook endpoint and no outbound notification. The only way to learn the review finished was to keep polling. (Screenshots: see the Unit 2 comment.)

## After (`feat/35-webhook-notifications`): webhook delivered

Setup, with `DEBUG_REVIEW_DELAY_SECONDS=45` and `WEBHOOK_ALLOW_PRIVATE_URLS=true` in `.env` (so a localhost receiver is allowed):

```
docker compose up -d
make reset-db
make migrate
make run
```

Registered a webhook in Swagger (`POST /webhooks`, logged in as user1):

```
curl -X POST 'http://localhost:8000/webhooks' \
  -H 'Authorization: Bearer <token>' \
  -H 'Content-Type: application/json' \
  -d '{"url": "http://localhost:9000/hook"}'
```

The response was 201 with the one-time secret (not shown here). Started a local receiver, which prints each POST and verifies its signature:

```
python receiver.py <secret>
```

**Run 1: same steps as Unit 2 (frontend).** Started the review from the UI for `octodad` / `test.txt`. The frontend polled `/status` as before, and about 45s later the receiver printed:

```
Received at:    21:18:16
Event:          review.completed
Delivery id:    evt_97431a7f-ef86-451d-a7d7-9d9b5fe2e5aa
Review id:      a18babac-f58d-4d4b-8291-8d5b86199b2a
Signature ok:   True
Body:
{
  "id": "evt_97431a7f-ef86-451d-a7d7-9d9b5fe2e5aa",
  "type": "review.completed",
  "created_at": "2026-10-05T04:18:16.894142Z",
  "data": {
    "id": "a18babac-f58d-4d4b-8291-8d5b86199b2a",
    "profile_id": "59f9325e-5139-415c-8dbe-737442b62d8d",
    "status": "complete",
    "sections": [ ...3 sections... ],
    "overall_score": 0.81,
    "error_message": null,
    "created_at": "2026-10-05T11:17:31.860118Z",
    "updated_at": "2026-10-05T11:18:16.875008Z"
  }
}
```

The review id matches the one in the Network tab's `status` response, and `created_at` to `updated_at` is 45s, matching the delay. The frontend still polls, since a browser can't receive webhooks (out of scope).

**Run 2: API only (Swagger), no polling.**

```
curl -X POST 'http://localhost:8000/reviews' \
  -H 'Authorization: Bearer <token>' \
  -H 'Content-Type: application/json' \
  -d '{"profile_id": "59f9325e-5139-415c-8dbe-737442b62d8d"}'
```

Response: `200`, `"id": "b97adaad-f917-44cb-9976-5ef44b8997ed"`, `"status": "pending"`. I made no further requests. The Network tab filtered on `status` showed **0 / 1 requests**. About 45s later the receiver printed:

```
Received at:    21:26:40
Event:          review.completed
Delivery id:    evt_d0bae2d9-902b-4a54-9e92-f9ca3e3bed0e
Review id:      b97adaad-f917-44cb-9976-5ef44b8997ed
Signature ok:   True
```

(The body has the same structure as Run 1.)

So the client made one request, never polled, and was still notified with a verified signature when the review finished.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

19/20 → 20/20 

**Package analysis**

In `pkg-20` my first rubric accepted it. The gold label said it should be held, with this reason: "excellent bounded plan that follows the thread's direction, but the comment contains no AI-use disclosure and ghostty's stated policy requires disclosing all AI usage; every package here is treated as AI-assisted work."

The plan really is strong, which is why my first rubric accepted it. The diagnosis matches the issue and the repro contro. The generation-counter fix follows the direction mitchellh gave in the thread and targets the cause instead of hiding the crash. The scope excludes the approach the thread rejected, and the risk section is honest about the unmeasured per-print cost. Every check I had passed.

My rubric missed the contribution policy. The repo facts for `pkg-20` say all AI usage must be disclosed, with the tool and the extent of the assistance. Neither the plan comment nor the repro report says anything about AI. I had no check that read that line, so a flawless plan sailed through. Adding the "AI policy compliance" check fixed it: the check now looks at the policy line and at the claim comment and repro report, finds no statement, and fails the package. That matches the gold label.

**Check rationale**

| AI policy compliance | The contribution-policy line in the package's Repo facts section, plus the candidate's claim comment and repro report | Fail if the policy prohibits AI-assisted contributions. If the policy requires AI usage to be disclosed for issues or comments, the claim comment or repro report must contain an explicit statement about AI use (the tool and extent, or an explicit "no AI used"); the absence of any such statement fails, regardless of whether AI use is suspected. If the policy has no disclosure requirement for issues or comments, pass. | required |

It reads this way because of `pkg-20`. The check began as something I forgot, and the wording came from fixing that miss. I rejected a version where the check tries to guess whether the author used AI. The gold label treats every package as AI-assisted, and a guess would be unreliable. A missing statement is a checkable fact. It also gives honest non-AI contributors a way to pass, so the check doesn't punish them. I kept this so the check only fires when the repo's own policy demands disclosure. A repo without such a rule, like PathReview, isn't penalized for staying silent.

**Trade-offs**

The AI policy compliance check changes the result for `pkg-20`: my first rubric accepted it, and with this check it is rejected, matching the gold label. The cost is that a plan can now fail on disclosure alone, however strong it is. `pkg-20` had a well-bounded plan that followed the maintainer's direction, and it still fails because neither the claim comment nor the repro report says anything about AI.

The check also has a case it will miss. It only looks for an explicit statement, so a vague or untrue one ("some AI help") passes, because I can't verify from the text whether the disclosure is honest or complete. I accepted that because a missing statement can be checked, while judging honesty can't. I also kept the check narrow: it fires only when the repo's policy line requires disclosure, so a package whose repo has no such rule is not affected.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.
