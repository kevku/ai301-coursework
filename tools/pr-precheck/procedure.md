# Procedure: how this tool grades a PR package

<!--
THIS IS THE PART YOU WRITE (second week running for the procedure).
Week 3 you wrote these steps for a plan package; this week the graded
object is a PR package, and the read that matters most is a
side-by-side: the diff against the plan, the evidence against the test
plan, the description against both. Your week-3 procedure is the
pattern; do not paste it unchanged, because its read order was built
for a different object.

Your rotation is the design brief again, and this week friction routes
three ways: a stall on WHAT to decide is a rubric gap, a stall on
WHERE to look is a procedure gap (this file), and a stall on what the
tool even reads or outputs is a frame gap (your SKILL.md). A complete
procedure lets someone who has never seen a PR package before grade
one exactly the way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
plan's scope pair before opening the diff, and list the files the plan
names" is a step; "understand the change" is a wish.
-->

## Read order

<!-- What gets read, in what order, before any check is graded, and
what to note down from each part while reading. A complete procedure
decides where the plan sits in the order (before the diff? before the
description?) and says why the order matters for the side-by-side
checks that come later. -->
1. Read the repo-facts block first. Note every section the PR template requires, every checklist item, and any stated policy, including AI-use disclosure and branch or commit naming rules. Reading the asks first means a missing section or disclosure is recognized as a gap instead of being mistaken for the repo's norm.
2. Read the plan-context block next. Write down the scope pair: the in-scope statement, the boundary, and the list of files or areas the plan names. Write down the test plan and any deviation notes. The plan is read before the diff on purpose: it is the yardstick, and if the diff is read first, the plan gets bent to fit what the diff happens to contain.
3. Read the candidate PR's description and title, noting each claim it makes about what changed, what was tested, and what was left alone. Read it before the diff so that its claims are recorded as claims, to be checked, rather than absorbed as facts.
4. Read the commit list and the diff last, file by file. For each changed file, write down its path and a one-line summary of the hunks. Mark any hunk that is formatting-only, debug output, dead code, or in a file the plan never named.
5. Read the test-evidence section after the diff, so you know what the change does before judging whether the evidence demonstrates it. Note the behavior named, the before, the expected-after, and the outcome of the repo's own checks.
6. Do not grade anything during the read. Finish all five reads and keep the notes, because the side-by-side checks depend on having the plan's list, the description's claims, and the diff's file list all in front of you at once.

## Evidence gathering

<!-- For each evidence family your rubric's checks name, the concrete
gathering move: which part of the package (or, live, which file, diff,
or page per your evidence guide) to pull the fact from, and what to
record. The load-bearing gathers this week are pairings: diff files
against plan scope, claimed evidence against the plan's test plan and
the repo's checks, description claims against diff contents. A
complete procedure leaves no check whose evidence an executor would
have to hunt for. -->
**Plan fidelity.** Build a two-column pairing. In one column, list every file and area the plan's scope pair names. In the other, list every file the diff changes. Mark each changed file as inside the boundary, covered by a deviation note (record the note's wording), or outside with no note. Mark each planned item as present in the diff, dropped with a note, or missing with no note. Then pair the description with the diff: for each change the description claims, find the hunk that delivers it, and for each hunk, find the sentence that mentions it. Record every claim with no hunk and every hunk with no mention.

**Test evidence.** Pair the test-evidence section with the plan's test plan. Record whether the same steps were rerun, whether a before and an after are both shown, which observable behavior is named, and whether the expected-after is stated in words. Then record the outcome of each of the repo's own checks (CI status, test suite, linter, build) as passing, failing, or not shown. For any failing check, record whether the package names it and gives a reason it is unrelated.

**Diff quality.** Go through the diff hunk by hunk and tally the debris tells from the evidence guide: debug leftovers, dead or commented-out code, formatting churn, and drive-by edits. Record the approximate count of lines that implement the plan against the lines that do not, and record whether each commit message says what its commit does.

**Standards and comms.** Pair the repo-facts asks with the description. For every required template section, record whether the header is intact and whether the content is specific to this PR or placeholder text. Record each checklist item as ticked and supported, ticked and unsupported, or unticked. Record whether AI use is disclosed where the policy asks and whether it names the tool. Record every "not applicable" and whether it gives a reason. Record any maintainer direction in the thread and whether the package responds to it.

## Check execution

<!-- How one check runs against gathered evidence: in what order the
checks execute, what an executor does when evidence for a check is
genuinely absent, and when a check may be graded without re-reading
the whole package. A complete procedure makes two executors grade the
same package the same way. -->
1. Run the checks in rubric order, one at a time. Do not skip ahead and do not revise an earlier grade because of a later one.
2. For each check, grade only from the notes gathered for its family, and cite at least one specific line from the package as the evidence: a file path, a hunk, a sentence from the description, or a line of test output. A grade with no cited line is not allowed.
3. Apply the check's pass condition exactly as the rubric states it. If a condition is observable (for example, every changed file is inside the boundary or covered by a note), answer it from the pairing table. Do not substitute an overall impression.
4. If the evidence for a check is genuinely absent (the package has no test-evidence section, no description, or no plan context to compare against), grade the check as failing when the absence is the package's own omission, and say "evidence absent" with the missing part named. Grade it as unclear only when the evidence exists but the notes cannot settle the pass condition, for example an ambiguous deviation note or a diff too truncated to read. Never guess a pass.
5. A check may be graded from the gathered notes without re-reading the whole package, provided the cited line is quoted from the package and not from memory. Go back to the package only for a check whose notes are incomplete or whose cited line you cannot find.
6. When two checks depend on the same evidence, such as a description claim that exceeds the diff, grade it once under the family the evidence guide assigns it to (plan fidelity) and do not penalize it again under standards and comms.

## Verdict assembly

<!-- How the per-check grades become the final accept or reject:
apply your rubric's verdict rule, state how unclear grades enter it,
and say what gets quoted in the output for the deciding check: the
check whose failure the verdict turned on. When more than one check
failed, your procedure picks which one gets quoted (first failing
required check in rubric order is a fine rule); nothing picks it for
you, so write the rule down. A complete procedure produces the same
verdict from the same grades, every time. -->
1. Collect every per-check grade (pass, fail, or unclear) into the per-check rows of the output, each with its cited evidence.
2. Apply the rubric's verdict rule exactly as written: the verdict is accept only if every required check passes, and reject if any required check fails. Do not adjust the verdict for a general feeling about the package. If a pass feels wrong, the fix belongs in the rubric, not in the verdict.
3. Treat an unclear grade on a required check as a fail for the verdict, and label it "unclear" in its row so the reader can see it was not a confirmed failure. An unclear grade on a non-required check does not change the verdict.
4. Choose the deciding check by rule: the first failing required check in rubric order. If the only failing required checks are unclear ones, the first unclear required check in rubric order is the deciding check.
5. In the output, quote the deciding check's cited evidence: the specific line from the package (the unexplained hunk, the claim with no hunk, the test-evidence sentence, or the skipped template section) and state in one sentence why it fails the check. Quote only that one check in full. Other failing checks are listed in their rows without extended quotes.
6. Write the verdict and the fenced JSON block last, in the reply, with the verdict in the JSON matching the verdict stated in the prose. The same grades must always produce the same verdict and the same deciding check.