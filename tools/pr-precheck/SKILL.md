---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

<!--
THIS IS THE PART YOU WRITE, and it is the last one: the frame itself.
Weeks 1 through 3 handed you a working SKILL.md and you filled the
files behind it; this week the frame ships as headings, and you write
what it says. The frontmatter above and the section headings below are
fixed (CONTRACT.md's layout rule); the instructions under each heading
are yours. Write instructions to the tool, in the imperative, the way
weeks 1-3's frames spoke to you: what to read, in what order, what to
refuse, what to emit. Your executor in the rotation is the test: a
frame gap they hit (cannot tell what the tool reads, or how a verdict
gets assembled) is a missing sentence here.

One section is not yours: the JSON schema in "Verdict and output" is
reproduced from CONTRACT.md verbatim and may not be altered. Your
words decide everything around it.
-->

## The question

<!-- State, in your words, the one question this tool answers and what
a PR package is: what artifacts it contains and what they are read
against. CONTRACT.md fixes the question; your frame has to say it so
the tool cannot wander into grading something else. -->
Answer one question: is this pull request ready to submit to a maintainer? Grade only that. Do not grade the quality of the plan itself, the quality of the issue, or the author's skill, and do not suggest rewrites unless a check's evidence line needs to name the problem. A PR package has three parts, and you always read them against each other. The plan context holds the plan's scope pair (the in-scope statement and the boundary, with the files or areas it names), its test plan, and any deviation notes. The candidate PR holds the title, the description, the commit list, the unified diff, and the test evidence. The repo facts hold the PR template's sections and checklist, the contributing instructions, any stated policy (including AI-use disclosure), the repo's own checks, and any maintainer direction in the thread. Read the diff against the plan, the evidence against the test plan and the repo's checks, and the description against both the diff and the repo's asks.

## Inputs and modes

<!-- Define both modes. Live mode: name every input (your plan.md with
its deviation notes, your branch's diff, your draft PR title and
description, your test evidence, your issue), where each comes from,
and what a house-chain student reads instead. The branch's diff is
everything the branch changes relative to the repo's default branch:
`git diff main...HEAD` (three dots), run from the working copy, is
the command that produces it; name the source that concretely. Eval
mode: state that the bundle is the whole world, nothing is fetched,
and every check runs with the full verdict rule. -->
Decide the mode before reading anything. If you were handed an eval package bundle, run eval mode. If you were pointed at a working copy and a draft PR, run live mode.

Live mode grades your own branch before the pull request is opened. Read these inputs and nothing else: plan.md from the working copy, including its scope pair, test plan, and deviation notes; the branch's diff, produced by running `git diff main...HEAD` (three dots) from the working copy, which shows everything the branch changes relative to the repo's default branch; the draft PR title and description, from the draft file or text you were given; the test evidence, meaning your captured before and after output from rerunning the reproduction steps plus the outcome of the repo's own checks; the issue the plan belongs to, from the issue thread; and the repo facts, from the repo's PR template (`.github/PULL_REQUEST_TEMPLATE.md`), CONTRIBUTING.md, any agent instructions file such as AGENTS.md, and any maintainer direction in the issue thread. If you are a house-chain student, read the equivalent inputs your chain supplies in the same roles (plan, diff, draft text, test evidence, issue, repo asks) instead of the files named above, and run the same checks against them. If an input is missing (no plan.md, an empty diff, no draft description), treat it as absent evidence and follow the procedure's rule for absent evidence rather than guessing. CI runs only after a PR is opened, so in live mode an unticked CI box in the draft is expected and is not a failure.

Eval mode grades a bundle. The bundle is the whole world: read only what it contains, fetch nothing, and never fill a gap from memory, from the open web, or from what a repo of that kind usually does. A missing part of the bundle is absent evidence. In both modes, every check in the rubric runs and the full verdict rule applies.

## The scope seam (live mode only)

<!-- Tell the tool when to read scope.md, what to do with the rules it
finds there, what to refuse, and what to do when the scope's repo line
is an unfilled placeholder. State that eval mode ignores scope.md
entirely. CONTRACT.md names the required behavior; your frame has to
instruct it. -->
In live mode, read scope.md before grading anything, because it says which repo this tool may grade a PR for. Compare the repo line in scope.md with the repo your branch and draft PR target. If they match, apply any other rules scope.md states and continue. If the target repo is not the one scope.md allows, refuse to grade: say the target repo is outside the stated scope, name both repos, and give no verdict. If the repo line in scope.md is still an unfilled placeholder, refuse to grade as well: say scope.md has no repo filled in, ask for it to be filled in, and give no verdict. Never edit scope.md, never widen its scope yourself, and never present a scope refusal as a reject. In eval mode, ignore scope.md entirely: do not read it, do not apply its rules, do not mention it, and never let it change a check, a grade, or the verdict.

## The voice seam (live mode only)

<!-- Tell the tool when to read voice-guide.md, which outgoing text it
gates (the PR title and description), how to report a broken rule, and
why it never changes the verdict on its own. State that eval mode
ignores it entirely. -->
In live mode, after the checks are graded and before you write the final reply, read voice-guide.md and check the outgoing text against it. The outgoing text is the draft PR title and the draft PR description, because those are the words a maintainer will read under your name. Do not check the diff, the plan, or the commit messages against it. For each rule the title or description breaks, report one finding: name the rule, quote the offending words, and say in one sentence what to change. Put the findings in a separate voice section in the reply, after the check rows and before the JSON block. Voice findings never change a check grade or the verdict on their own, because voice is about how the text reads and the verdict is about whether the PR is ready; a PR can be ready and still need its wording fixed. Do not add voice findings to the JSON checks array. If voice-guide.md is missing or empty, say so in one line and continue. In eval mode, ignore voice-guide.md entirely: do not read it, do not check any text against it, and do not report voice findings.

## Component reads

<!-- Tell the tool how the pieces connect: rubric.md defines the
checks and the verdict rule, references/evidence-guide.md maps where
each evidence family lives, procedure.md is executed as written. Say
what the tool does when the procedure is silent on a step (report the
gap, never improvise around it) and what it does when rubric.md or
procedure.md has no content (the refusal rule, stated as an
instruction). -->
Read three files before grading anything. Read rubric.md first: it defines every check, with its evidence, pass condition, and weight, and the verdict rule that turns grades into accept or reject. Read references/evidence-guide.md second: it says where each evidence family (plan fidelity, test evidence, diff quality, standards and comms) lives in the package and what good looks like there. Read procedure.md third and execute it as written, in its stated order: read order, evidence gathering, check execution, verdict assembly. Do not reorder its steps, skip any, or substitute your own method. If the procedure is silent on a step you need, report the gap in the reply by naming the missing step, grade the affected check as unclear, and never improvise around it. If rubric.md has no checks or no verdict rule, or procedure.md is empty or still holds only its template comments, refuse to grade: say which file is empty and that no verdict can be given. Do not fall back to your own judgment, and never emit an accept in that case.

## Verdict and output

<!-- State the binary verdict space (accept means submit, reject means
hold) and instruct the tool to end its reply with the fenced JSON
block below, valid and last, with nothing after it. The schema is
CONTRACT.md's, verbatim; do not edit it. -->
The verdict is binary: accept means the package is ready to submit, and reject means hold it. There is no third value. Build the verdict only by applying the rubric's verdict rule to the per-check grades, as the procedure's verdict assembly directs. In the reply, show one row per check with its grade and evidence, quote the deciding check as the procedure requires, and state the verdict in one sentence. In live mode, add the voice findings section after the check rows. End the reply with the fenced JSON block below: valid JSON, the very last thing in the reply, with nothing after it. Set `item` to the PR URL in live mode if one exists (otherwise the branch name) and to the bundle id in eval mode. Include every check from the rubric, use only the grades pass, fail, or unclear, and keep each evidence value to one line holding the fact or quote that decided it. The verdict in the JSON must match the verdict stated in the prose.

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

<!-- Write the standing rules the tool grades under: evidence first,
grade the thing not the polish, the rubric decides, the procedure
decides how, and how unclear grades are treated when the rubric's
verdict rule is silent. CONTRACT.md states each as a guarantee; your
frame has to make them instructions. -->
Find the evidence before you grade: for every check, locate the specific line in the package (a file path, a hunk, a sentence from the description, a line of test output) and cite it. Never grade from a general impression, and never grade a check with no cited line. Grade the thing itself, not the polish: judge whether the diff matches the plan, whether the evidence shows an observable behavior, and whether the repo's asks are met, never how well written, long, or confident the description sounds. The rubric decides what counts as a pass and what weight each check carries, and the procedure decides how you gather and run them; do not add checks, drop checks, or change a weight. Treat every claim in the package as unverified until the diff, the evidence, or the repo facts back it, and fail a claim that cannot be verified from the package, because an unverifiable claim is not evidence. Grade a check unclear only when the evidence exists but cannot settle the pass condition. If the rubric's verdict rule is silent on unclear grades, count an unclear grade on a required check as a fail and an unclear grade on a preferred check as no effect. Never let a pass that feels wrong turn into a different verdict: if the verdict seems wrong, report that the fix belongs in the rubric and still emit the verdict the rubric produces. A package that honestly discloses a shortfall is graded on whether it is truthful and complete about what it did, not on whether it did everything.