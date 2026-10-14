# Evidence guide: where evidence lives in a PR package

<!--
THIS IS THE PART YOU WRITE (third week running: the map stays in your
hands). Your tool uses this guide as its map: for every kind of
evidence a rubric check names, this file says WHERE to find it in a PR
package and WHAT GOOD LOOKS LIKE when you do.

The four families below are the harness's failure categories under
the names the eval README uses: plan fidelity = silent-drift, test
evidence = not-tested, diff quality = unreviewable, standards and
comms = standards-wall. A package that fails none of them is a
clear-accept. Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the plan-context block's scope pair and test
  plan, the candidate PR's diff, commits, description, or
  test-evidence section, the repo-facts block's template asks and
  stated policy). In live mode (where in your working copy and on
  GitHub: your plan.md and its deviation notes, your branch's diff,
  your draft title and description, your captured test output, the
  repo's PR template and CONTRIBUTING.md).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("every changed file falls inside the
  plan's stated boundary or a deviation note") over adjectives ("the
  diff is clean").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts three ways: your
procedure says WHEN to gather each family, this guide says WHERE, and
your SKILL.md says the tool reads both. Write the map you wish your
executor had.
-->

## Plan fidelity (harness category: silent-drift)

<!-- Where the plan states its scope, boundary, and deviation notes,
and where the diff shows what actually changed. What it means for a
diff to match the plan, for an honest deviation to re-tie a mismatch,
and what silent drift looks like in each direction (more than the
plan, or less with no note). The description's fidelity claims read
against the diff live here too: a description claiming more or less
than the diff delivers is silent drift, not a comms problem. -->
The plan's intent lives in the plan-context block: its scope pair says what the change will do and where it must stay, and any deviation notes sit alongside it. What actually changed lives in the candidate PR's diff (the file list and every hunk), its commit list, and its description. A diff matches the plan when every changed file and hunk falls inside the stated boundary or is covered by a deviation note that names it and gives a reason, and every item the plan promised shows up in the diff or has a note saying it was dropped. Silent drift runs in both directions: more than the plan (a file or hunk outside the boundary, such as an unrequested helper or refactor, with no note anywhere) or less than the plan (a promised change missing with no note). A description that claims a change the diff doesn't contain, or omits one it does, is also silent drift rather than a comms problem. An honest deviation re-ties the mismatch by naming the specific change, saying it differs from the plan, and explaining why. In live mode, compare plan.md (scope, boundary, and deviation notes) against the diff of your branch versus the upstream main branch, and against your draft title and description.

## Test evidence (harness category: not-tested)

<!-- Where the PR shows its proof: the test-evidence section's
before/after against the plan's test plan and the reproduction's own
steps, and the outcome of the repo's own checks or suite. What
decisive looks like (an observable behavior named, the expected-after
stated, the checks' outcome visible) next to "tests pass". -->
The proof lives in the candidate PR's test-evidence section, read against the plan-context block's test plan and the reproduction steps (the steps that trigger the original problem), along with the visible outcome of the repo's own checks, such as CI status, the test suite, the linter, and the build. Decisive evidence reruns the reproduction steps before and after the change, names the observable behavior (for example, "10 rows in, 9 written" before and "10 written" after), states the expected result after the change explicitly, and shows the checks' actual outcome. "Tests pass" or "works for me" with no behavior named, no before, no expected-after, or a test plan that was never run is not enough. A failing check can still pass only if the package names it and explains why it is unrelated to the change; a hidden or unmentioned failure counts as not tested. In live mode, look at your captured before and after output from rerunning the reproduction on your built change, the test plan in plan.md, and the testing section of your draft description. CI only runs once the PR is opened, so an unticked CI box in a draft is expected.

## Diff quality (harness category: unreviewable)

<!-- Where the change itself lives: the unified diff and the commit
list. What a reviewable change looks like (the fix visible, nothing
unrelated riding along) and the debris tells: debug leftovers, dead
code, commented-out blocks, formatting churn, drive-by edits. -->
The change itself lives in the candidate PR's unified diff and its commit list. A reviewable change lets a reader find the fix within seconds: the lines that implement the plan are easy to spot, every other hunk is small, explained, or absent, and each commit message says what that commit does so the commits tell a coherent story. The tells of an unreviewable diff are debug leftovers (print or console statements, stray TODOs, temporary files), dead code or commented-out blocks the change doesn't use, formatting churn on lines the fix didn't need to touch, drive-by edits such as renames or refactors in unrelated functions or files (even good ones), and a size mismatch where a few lines of fix are buried in many lines of noise or the diff is far larger than the plan's scope would produce. In live mode, run the diff of your branch against the upstream main branch before opening the PR and check the branch's commit history with git log.

## Standards and comms (harness category: standards-wall)

<!-- Where the repo states its asks (the repo-facts block's PR
template sections, contributing instructions, and stated policy,
including AI-use disclosure) and where the PR honors them: the
stated sections filled with real content, the disclosure present,
explicit maintainer direction in the thread engaged. What compliant
looks like next to boilerplate or a visibly ignored ask. (Whether
the description's claims match the diff is plan fidelity, above.) -->
The repo's asks live in the repo-facts block: the PR template's sections and checklist, the contributing instructions, and any stated policy, including AI-use disclosure. The PR's honoring of them lives in the candidate PR's title, description, and any maintainer comments in the thread. A compliant package has every template section present with its original header and filled with real content specific to this PR, checklist items ticked only where true, the issue reference included if the template asks for one, AI use disclosed in the place the policy specifies and naming the tool, "not applicable" answers given with a reason, and any explicit maintainer direction acknowledged or followed. Boilerplate looks like placeholder text left in sections, deleted or renamed headers, "N/A" with no reason, or boxes ticked that the evidence doesn't support. An ignored ask is a stated policy (such as required AI disclosure or a branch naming format) that the package visibly skips, or a maintainer request that gets no response. If the repo asks for nothing, nothing counts against the package. In live mode, read the repo's PR template (.github/PULL_REQUEST_TEMPLATE.md), CONTRIBUTING.md, and any agent instructions file such as AGENTS.md against your draft title and description and any maintainer direction in the linked issue thread.