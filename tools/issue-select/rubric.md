# Rubric: is this a good first issue?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
|Maintainer activity|The last 5 default-branch commit dates and authors in the repo-facts block; maintainer comments/reviews/merges in the issue or PR history|At least one of the following within the past 60 days: a commit or PR merge to the default branch (merging implies maintainer/write access), or a comment/review from an account tagged OWNER, MEMBER, or COLLABORATOR|required|
|Issue is unclaimed|The issue's assignee field, labels, and the full comment thread on the issue.|The issue has no assignee and the issue body/comments do not indicate that someone has already committed to working on it|required|
|No active PR for the issue|The repository's open pull requests, including PR title, body, linked issues, and recent comments; see references/evidence-guide.md for the prescribed PR evidence|There is no open PR that addresses the issue or clearly claims to implement the same requested change|required|
|Locations are identifiable|Issue body, linked code references, comments|The issue body and/or comment thread describe a specific, reproducible symptom, behavior, or requested feature (including trigger conditions, affected command/flag/UI area, or expected vs. actual behavior) precise enough that a contributor could locate the relevant code through normal searching — without requiring an explicit file list, and regardless of whether the exact implementation approach is already decided.|required|
|Scope is bounded to one deliverable|Issue body, comment thread, and linked PR list (including closed/abandoned PRs)|The issue describes a single fixed deliverable or lists multiple fixes related to the same issue, not an open-ended or codebase-wide initiative with no defined endpoint (e.g. "wherever it makes sense," "anyone can work on this"); the issue should not require a judgement call made by the maintainer or the community. This focuses on abstract concepts like design, looks, and overall structure of the program.; and does not have multiple closed/abandoned linked PRs that failed to resolve it. Multiple valid technical approaches to a goal that is not itself in dispute.|required|
|AI contribution allowed|The repository's CONTRIBUTING.md, README.md, and CODE_OF_CONDUCT.md (or equivalent contribution policy documentation)|None of the repository's contribution policy documentation explicitly prohibits AI-generated or AI-assisted contributions|required|

## Verdict rule

Accept if every required check (Maintainer activity, Issue is unclaimed, No active PR for the issue, Locations are identifiable, Scope is bounded to one deliverable) passes. A required check graded unclear counts as a fail on that check. Preferred checks never change the accept/reject verdict; they only rank among already-accepted issues.
