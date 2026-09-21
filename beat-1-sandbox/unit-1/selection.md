# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**:
[Link to Issue](https://github.com/codepath/pathreview-ai301-fa26-s1/issues/35)

**Verdict output**
Issue #35: Implement webhook system for review notifications

┌────────────────────┬───────┬───────────────────────────────────────────────────────────────────────────────────────┐
│       Check        │ Grade │                                       Evidence                                        │
├────────────────────┼───────┼───────────────────────────────────────────────────────────────────────────────────────┤
│ Maintainer         │ pass  │ Aburke225 committed Sept 16, 2026 (within 60 days)                                    │
│ activity           │       │                                                                                       │
├────────────────────┼───────┼───────────────────────────────────────────────────────────────────────────────────────┤
│ Issue is unclaimed │ pass  │ No assignee, no comments indicating claimed work                                      │
├────────────────────┼───────┼───────────────────────────────────────────────────────────────────────────────────────┤
│ No active PR for   │ pass  │ 0 open PRs in repo                                                                    │
│ the issue          │       │                                                                                       │
├────────────────────┼───────┼───────────────────────────────────────────────────────────────────────────────────────┤
│ Locations are      │       │ Specifies exact endpoint behavior (POST with review payload on completion), suggests  │
│ identifiable       │ pass  │ implementation files (api/routes/webhooks.py, core/services/webhook_service.py), and  │
│                    │       │ describes trigger (long-running reviews completing)                                   │
├────────────────────┼───────┼───────────────────────────────────────────────────────────────────────────────────────┤
│ Scope is bounded   │ pass  │ Implement webhook system for one event type (review completion); estimated 8–12       │
│ to one deliverable │       │ hours; single deliverable                                                             │
├────────────────────┼───────┼───────────────────────────────────────────────────────────────────────────────────────┤
│ AI contribution    │ pass  │ No prohibition in CONTRIBUTING.md                                                     │
│ allowed            │       │                                                                                       │
└────────────────────┴───────┴───────────────────────────────────────────────────────────────────────────────────────┘

Verdict: ✅ ACCEPT

**The verdict must record `accept` for this issue.** 
```
{
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/35",
    "checks": [
      {
        "name": "Maintainer activity",
        "grade": "pass",
        "evidence": "Aburke225 committed on Sept 16, 2026 (4 days ago, within 60 days)"
      },
      {
        "name": "Issue is unclaimed",
        "grade": "pass",
        "evidence": "No assignee; no comments indicating anyone is working on this"
      },
      {
        "name": "No active PR for the issue",
        "grade": "pass",
        "evidence": "Repository has 0 open pull requests"
      },
      {
        "name": "Locations are identifiable",
        "grade": "pass",
        "evidence": "Specifies endpoint behavior, trigger condition (review completion), suggested implementation files, and POST payload content"
      },
      {
        "name": "Scope is bounded to one deliverable",
        "grade": "pass",
        "evidence": "Single webhook system for one event type (review completion); 8–12 hour estimate; clear deliverable"
      },
      {
        "name": "AI contribution allowed",
        "grade": "pass",
        "evidence": "CONTRIBUTING.md contains no prohibition on AI-assisted contributions"
      }
    ],
    "verdict": "accept"
  }
```

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

15/20 → 17/20 → 17/20 → 17/20 → 18/20

**Issue analysis**

One issue that failed against my rubric and did not match the gold label was `issue-19`. In the gold rubric it accepts the issue because `{"id": "issue-19", "source": "zxcalc/zxlive#517", "category": "clear-accept", "calibration": false, "verdict": "accept", "note": "maintainer-diagnosed performance bug with named causes, unclaimed"}`. My result after a full run provided a `issue-19  accept  reject   NO     failed: Scope is bounded to one deliverable`. Prior to the full run, my rubric agreed with the gold label shown here: 
```python3 run_eval.py --rubric ../skill/rubric.md --only issue-15,issue-19 
grading 2 bundle(s) with rubric.md, model sonnet, 5 worker(s)...
  issue-15: reject
  issue-19: accept

item      gold    verdict  agree  note
issue-15  reject  reject   yes    
issue-19  accept  accept   yes  
```
While both runs utilizes the same prompt, different sessions have interpretted the pass condition differently:
"The issue describes a single fixed deliverable or lists multiple fixes related to the same issue, not an open-ended or codebase-wide initiative with no defined endpoint (e.g. "wherever it makes sense," "anyone can work on this"); the issue should not require a judgement call made by the maintainer or the community. This focuses on abstract concepts like design, looks, and overall structure of the program.; and does not have multiple closed/abandoned linked PRs that failed to resolve it. Multiple valid technical approaches to a goal that is not itself in dispute."
Due to the wording of "lists multiple fixes" and "Multiple valid technical approaches", this leaves room for the model to side towards one or the other. In the isolated run, that session may have recognized that the list it provided all related to a performance bug and is accepted. In the other end, the session that was part of the entire run may have only focused on "single fixed deliverable" too literally and believes that the list the issue provided is fixing multiple parts of the project which would be considered as a reject.

**Check rationale**
`|Maintainer activity|The last 5 default-branch commit dates and authors in the repo-facts block; maintainer comments/reviews/merges in the issue or PR history|At least one of the following within the past 60 days: a commit or PR merge to the default branch (merging implies maintainer/write access), or a comment/review from an account tagged OWNER, MEMBER, or COLLABORATOR|required|`
Originally I had the pass condition as "At least one maintainer has made a commit, merged a PR, or commented/reviewed an issue or PR within the past 60 days". The commits did not show that the author was actually working on the issue. I was not explicit enough to say that an action like merge pull request is the role of a maintainer so the llm marked as unclear and failed it. This is why I had to add the actions that are related to a maintainer. I thought that default branch merge was evident enough that the user would be a maintainer since in `issue-06` there was no explicit tags that were provided.

**Trade-offs**

For `Scope is bounded to one deliverable`, I needed to add `lists multiple fixes related to the same issue` and `not an open-ended or codebase-wide initiative with no defined endpoint (e.g. "wherever it makes sense," "anyone can work on this"); the issue should not require a judgement call made by the maintainer or the community. This focuses on abstract concepts like design, looks, and overall structure of the program.;` as the pass condition because for multiple fixes related to same issue was trying to address `issue-01` and `issue-04` because they listed multiple items that needed to be fixed as part of the issue. Then I needed the requirement of the scope to be specific enough that there can be a technical implementation since `issue-05`, `issue-15` and `issue-20` applied to the entire codebase or required additional input/decision making. With the balance of the wording, I can see the case of `issue-19` where it was both accepted and not accepted in the two cases from the full run and isolated:
```python3 run_eval.py --rubric ../skill/rubric.md --only issue-15,issue-19 
grading 2 bundle(s) with rubric.md, model sonnet, 5 worker(s)...
  issue-15: reject
  issue-19: accept

item      gold    verdict  agree  note
issue-15  reject  reject   yes    
issue-19  accept  accept   yes  
```
If I were to be more specific of the scope, it may fail issues like 1 and 4 where multiple parts are part of the same issue. If the wording is too loose, then it would pass the issues where there is more ambiguity in the issue like 5, 15, and 20.

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

1. I enjoy working with APIs and the files are written in Python. Previously I worked on something similar in AI-201 with implementing a RateLimitingHeader (which is also an issue in this project) where I was able to finish in the assigned time.
2. The vedict from my rubric was all `Maintainer activity`, `Issue is unclaimed`, `No active PR for the issue`, `Locations are identifiable`, `Scope is bounded to one deliverable`, and `AI contribution allowed` Passed from the judge. The rubric did not weigh in the fact that I have already worked on an issue similar to this and how it was in the same tier as the issue from AI-201.
3. Given that I've worked on a similar issue, I wanted to give myself enough time to double check the work and ensuring that I thoroughly investigate the root problem. I believe that it would not be too hard to the point where I can't finishe addressing the issue with the allotted time.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
