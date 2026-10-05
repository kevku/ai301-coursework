# Rubric: is this plan ready to post and build from?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here (via your procedure.md). It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the plan's scope statement, the test plan read against
     the repro evidence's steps, the plan comment read against the
     thread highlights, the repo-facts block) or a location from your
     references/evidence-guide.md. "The plan" is not a source; "the
     plan's stated cause read against what the repro evidence shows"
     is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (is
     this one bounded change? could a stranger start executing it?),
     never the write-up's shape (how many sections it has, how long it
     is, whether it uses headings). Structure-shaped checks are what
     make graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad plans posted. The lecture named the
failure families: the diagnosis ignores or contradicts the reproduced
evidence, the change is unbounded (scope creep), the plan targets the
symptom while the evidence points at the cause, a stranger could not
start executing it, the test plan proves nothing observable, the
unknowns are dressed up as certainty, and the comment ignores what the
thread or the repo's stated conventions ask. A rubric that ignores a
family will fail eval packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Summary | Plan's opening description | Briefly states the issue being worked on, and the description matches what the issue actually reports. | preferred |
| Root Cause | Diagnosis section | Names a cause supported by the issue description, reproduction steps, comments, or other provided evidence. Does not ignore or contradict the reproduced evidence. | required |
| Fix Targets Cause | Proposed fix | The fix removes the identified cause. Fails if it only hides the symptom (e.g. swallowing the error, special-casing the reproduction input, adding a retry or suppression) when the evidence points at a deeper cause. | required |
| Scope Files | Files mentioned | Every listed file relates to the issue through the description, reproduction, or comments. If no files are listed, the plan still names the module, function, or area to change; otherwise fail. | required |
| Scope Features | Features mentioned | Every listed feature relates to the issue through the description or comments. If none are listed and the issue doesn't need any, grade pass. | required |
| Bounded Change | Planned changes | Changes are limited to what the issue needs. Fails if the plan adds unrelated refactors, renames, dependency upgrades, or extra features, unless the evidence justifies them. | required |
| Planned Changes | Proposal of changes | Describes concrete changes (what changes, where, and how) that map directly to the identified cause. | required |
| Actionability | Whole plan | A contributor unfamiliar with the codebase could start from the plan alone. It says where to look and what to do, not just a goal like "fix the bug". | required |
| Test Plan | Reproduction and verification | Reproduces the reported issue or its triggering conditions, then verifies the change fixes it. Each test states an observable expected result (a specific output, behavior, or assertion). Covers each distinguishing condition when the issue has several. | required |
| Honest Uncertainty | Diagnosis and fix wording | Where the cause or fix isn't confirmed by the evidence, the plan says so (e.g. "likely", "to be verified by X"). Fails if a guess is stated as established fact. | required |
| Conventions | Thread and repo guidance | Does not contradict maintainer comments, contributing guidelines, or stated conventions (e.g. "don't change the public API", "assign first", required test style). If none exist in the provided material, grade pass. | required |
| AI policy compliance | The contribution-policy line in the package's Repo facts section, plus the candidate's claim comment and repro report | Fail if the policy prohibits AI-assisted contributions. If the policy requires AI usage to be disclosed for issues or comments, the claim comment or repro report must contain an explicit statement about AI use (the tool and extent, or an explicit "no AI used"); the absence of any such statement fails, regardless of whether AI use is suspected. If the policy has no disclosure requirement for issues or comments, pass. | required |



## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->
Accept if every required check passes and if any is unclear, then it's considered as a fail. Prefered does not change whether it is accepted or rejected.
