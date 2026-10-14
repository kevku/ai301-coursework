# Rubric: is this pull request ready to submit?

<!--
THIS IS THE PART YOU WRITE (fourth week running; this is the rubric's
final form in the sandbox). Your frame in SKILL.md executes whatever
checks you define here, via your procedure.md. It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the diff read against the plan's scope, the test
     evidence read against the plan's test plan, the description read
     against the diff, the repo-facts block's template asks) or a
     location from your references/evidence-guide.md. "The PR" is not
     a source; "the diff's changed files read against the plan's
     stated boundary" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself
     (does the diff fall inside the plan plus its deviation notes? is
     the claimed evidence observable?), never the write-up's shape
     (how long the description is, how many commits there are).
     Structure-shaped checks are what make graders disagree with
     themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (submit) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. State the `unclear`
   treatment explicitly: the frame here is YOUR SKILL.md, so a rubric
   that stays silent is only covered if your frame's grading
   discipline says what happens (the contract's own default is that
   an unverifiable claim fails).

Cover what actually gets bad PRs submitted. The failure families the
lecture named ARE the harness's scoring categories, same names as the
eval README: silent drift (the diff silently does more or less than
the posted plan, or the description claims fidelity the diff
contradicts), not tested (the evidence proves nothing observable, or
the repo's own checks were never run), unreviewable (debris or
unrelated hunks bury the change), and standards wall (the repo's
stated template and disclosure asks are ignored). Your evidence
guide's four headings map onto these one to one (plan fidelity =
silent drift, test evidence = not tested, diff quality =
unreviewable, standards and comms = standards wall), and the category
floor is scored on exactly these names plus clear accept. A rubric
that ignores a category will fail the eval packages built around
that category. And remember the honest-outcome
rule, fourth week running: a PR that honestly discloses a shortfall
can be ready; a rubric that equates "less than everything" with
"hold" fails the set.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
|No unplanned changes|The diff's changed files and hunks, read against the plan-context block's scope pair (in-scope statement, boundary, named files or areas) and any deviation notes in the plan, commits, or description|Every changed file and hunk falls inside the plan's stated boundary, or is covered by a deviation note that names the change and gives a reason. A hunk outside the boundary with no note anywhere in the package is a fail, even if the change is correct or useful.|required|
|Planned work delivered or disclosed|The plan's scope pair and list of promised changes, read against the diff's file list and the description|Every change the plan promised appears in the diff, or the package states that it was dropped, deferred, or only partly done, with a reason. A promised change that is missing from the diff with no note is a fail. A shortfall that is honestly disclosed passes.|required|
|Description matches the diff|Each claim in the PR description and title about what changed, what was fixed, and what was left alone, read against the diff's hunks|Every claimed change has a hunk in the diff that delivers it, and no substantive hunk goes unmentioned. A claim the diff does not contain, or a claim that overstates what a hunk does, is a fail. This is graded here and not again under the standards check.|required|
|Behavior evidence is observable|The test-evidence section, read against the plan's test plan and the reproduction steps|The evidence reruns the plan's test plan or reproduction steps on the built change, names a specific observable behavior, and shows the before and the expected-after. "Tests pass," "works for me," or a test plan that was never run is a fail. If the package honestly states that the behavior could not be verified and says why, it passes.|required|
|Repo's own checks shown|The repo-facts block's stated checks (test suite, linter, build, CI), read against the check outcomes shown in the test-evidence section or description|The outcome of each check the repo requires is visible as passing, or a failing check is named with a reason it is unrelated to the change. A required check that was never run, or a failure that is not mentioned, is a fail. If the repo requires no checks, the check passes.|required|
|Fix is visible, no debris|The unified diff, read hunk by hunk|The lines that implement the plan are easy to find, and no hunk is debris: no debug output, stray TODOs or temporary files, no dead or commented-out code, no formatting-only changes to lines the fix did not need to touch, and no drive-by renames or refactors. Debris that is small and explained in the package does not fail the check.|required|
|Template filled with real content|The repo-facts block's PR template sections and checklist, read against the candidate PR's description|Every template section is present with its original header and answered with content specific to this PR. Placeholder text, deleted or renamed headers, a "not applicable" with no reason, and checklist boxes ticked without support in the package are a fail. If the repo has no PR template, the check passes.|required|
|AI-use disclosure and stated policy honored|The repo-facts block's contributing instructions and stated policy (AI-use disclosure, branch or commit naming, issue-reference format), read against the description and commits|Every ask the repo states is visibly met in the form the policy asks for. If the policy requires disclosure, the disclosure is present and includes whatever details the policy names (a tool name, a description of use, a human-written statement). Details the policy does not ask for are not required. A stated ask that the package visibly skips is a fail. If the repo states no asks, nothing counts against the package.|required|
|Maintainer direction engaged|Maintainer comments in the issue or PR thread in the repo-facts block, read against the diff and description|Any explicit request or instruction from a maintainer in the thread is followed or answered in the package. A maintainer request that gets no response is a fail. If the thread contains no maintainer direction, the check passes.|required|
|Title says what and where|The candidate PR's title, read against the diff|The title names the specific thing that changed and where it changed, so a maintainer could tell what the PR proposes without opening it. A title like "fix bugs" or "add colors" does not pass.|preferred|

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->
Accept (submit) if every required check (No unplanned changes, Planned work delivered or disclosed, Description matches the diff, Behavior evidence is observable, Repo's own checks shown, Fix is visible no debris, Template filled with real content, AI-use disclosure and stated policy honored, Maintainer direction engaged) passes; otherwise reject (hold). A required check graded unclear counts as a fail on that check. A shortfall that the package honestly discloses, such as a dropped planned item, an unverifiable behavior, or an unrelated failing check, passes the relevant check and does not hold the package, because the verdict turns on whether the package is truthful and complete about what it did, not on whether it did everything. Preferred checks never change the verdict.