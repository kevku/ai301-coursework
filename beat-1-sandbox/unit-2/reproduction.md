# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username**

kevku

---

## Posted upstream

**Claim comment**

[Link to Claim](https://github.com/codepath/pathreview-ai301-fa26-s1/issues/35#issuecomment-5862246642)

I'd like to investigate #35. I'll provide a reproduction of the long running reviews that will take around 30-90 seconds. Following the reproduction, I'll look into providing an implementation of the webhook endpoint.

**Reproduction comment**

[Link Reproduction](https://github.com/codepath/pathreview-ai301-fa26-s1/issues/35#issuecomment-5863874875)

# Issue
The issue wants to implement a webhook because for longer reviews, we can reduce the amount requests made to the server. The current model makes a request every 3 seconds to the server.

## Environment
- OS: macOS Tahoe v26.4.1
- Docker version 29.5.2, build 79eb04c7d8
- Python 3.14.4
- Repository: `kevku/pathreview-ai301-fa26-s1` (`f89c06f`) on `main`, with a clean working tree.

## Steps to Reproduce
1. Added `debug_review_delay_seconds: int = 0` inside the `Settings` of `core/config.py`.
2. Added `import asyncio` and `from core.config import settings` at the top of `core/services/review_service.py`.
3. Added the following lines right before the `return` of function definition `_run_rag_retrieval_generation` in `core/services/review_service.py`.
``` 
if settings.debug_review_delay_seconds:
  await asyncio.sleep(settings.debug_review_delay_seconds)
```
4. Run the following commands in Pathfinder directory
  - `docker compose up -d`
  - `make setup`
  - `make run`
5. Went to `http://localhost:5173` and logged in with 
  - User: `user1@example.com`
  - Password: `password1`
6. Clicked on `Start a New Review`, inspected elements and went to the `Network` tab with the filter of `status`.
7. Entered `octodad` as the Github Username and provided an empty file called `test.txt`

## Evidence
### Full Network
<img width="1510" height="783" alt="Image" src="https://github.com/user-attachments/assets/7ad736f5-e535-45bf-b4df-dbdd07355a74" />

### Processing Status
<img width="732" height="581" alt="Image" src="https://github.com/user-attachments/assets/8c71bd93-5471-4818-9001-75a536763f90" />

### Complete Status
<img width="732" height="590" alt="Image" src="https://github.com/user-attachments/assets/213e2aaa-7c5b-491c-ae90-3c9abe264338" />

These images show that while a review is ocuring, the client is continuously requesting from the server for the status of the review.

## Behavior

- Expected: Webhook is not implemented yet as an endpoint
- Actual: There is no pre-existing `webhook` as part of the route and from the evidence, the behavior of it shows polling rather than the effects of a webhook.

## Conclusion and Comments
The current system of making reviews is constantly polling the server which can make unesessary requests to the server when a webhook can solve that issue. I manually simulated the delay of the review process as the LLM was not connected from `.env`:
```
# LLM provider
# Options: "mock" (default, no API key needed), "openai"
LLM_PROVIDER=mock
OPENAI_API_KEY=sk-your-key-here
```
Additionally, in the function `_run_rag_retrieval_generation` in `core/services/review_service.py` has hardcoded data which is why I chose to simulate the processing time of 30-90 seconds. In my example I used 45 seconds as a test case and we can see around ~15 requests that has `status: processing` from the waterfall and the final being `status: complete`.  
AI was used to help investigate deeper into webhook, structure of the program, and to investigate whether it was possible to trigger an LLM running on live data.


## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

17/20 → 17/20 → 20/20 

**Package analysis**

For pkg-19, my rubric began with four required checks that graded only the reproduction: environment, steps, expected vs actual, and files and commands. The gold label was reject, and in the second run the rubric graded it accept possibly due to the rubric not as strict. The newer run of reject comes from the claim comment, which asks maintainers to "assign it to me," promises a fix "within 2 days guaranteed," and asks them to keep the issue "reserved," while naming no concrete next step. My rubric read the item as an accept because it never evaluated the claim comment at all; a strong report attached to a bad comment looked like a clean pass. The fix is a claim-comment check that requires a concrete, issue-specific next step and fails on assign-or-reserve requests, delivery guarantees, or generic enthusiasm, while leaving a plain "I'd like to work on this" alone.

**Check rationale**

[Quote one check from the `rubric.md` you uploaded to `tools/repro-check/`, exactly as it reads now.
Then say why it reads that way — what you revised to get there, or what you rejected in
favour of it.]
`|Expected vs Actual|Provides the report of the expected issue and a report of the result the user actually got when reproducing|The actual result should match the expected issue. If it differs, the check still passes only if the report explicitly states the mismatch (e.g. "could not reproduce"), gives the observed output, and Environment Check, Steps of Reproduction, and Files & Commands all pass. A different result that is not acknowledged as different fails.|required|` is taken straight from the rubric. Originally I required the check as expected vs actual to be exactly the same or else it fails. I forgot about the cases where results can either differ a little bit or could not reproduce as some issues' results can differ from extremely niche cases. This is why I can consider it as a pass if my other condition passes of OS, steps, and exaxt files/commands. This was why I had to add the entire if condition.

**Trade-offs**

Back to `|Expected vs Actual|Provides the report of the expected issue and a report of the result the user actually got when reproducing|The actual result should match the expected issue. If it differs, the check still passes only if the report explicitly states the mismatch (e.g. "could not reproduce"), gives the observed output, and Environment Check, Steps of Reproduction, and Files & Commands all pass. A different result that is not acknowledged as different fails.|required|`, I think it will fail when a certain version or OS does not affect the main problem of the issue, but they mismatch and produce a slightly different result. An example would be the problem in a certain issue can be the same for different operating systems, but since they're different operating systems a differen type of error message can output.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
