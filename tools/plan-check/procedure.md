# Procedure: how this skill grades a plan package

<!--
THIS IS THE PART YOU WRITE, and it is a new kind of part. Weeks 1 and
2, SKILL.md carried a numbered workflow and you only wrote judgment
files. This week the workflow is gone from the frame: SKILL.md says
"execute procedure.md", and these are the operating steps you author.
The machinery is in your hands now.

Your operator swap is the design brief. When your executor stalled
because your rubric said WHAT to decide but not HOW to find the
evidence, that was a procedure gap. This file is where those gaps get
closed: a complete procedure lets someone who has never seen a plan
package before (a groupmate, or the skill itself) grade one exactly the
way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
repro evidence before the plan, and note what behavior it pins down"
is a step; "understand the context" is a wish.
-->

## Read order

<!-- What gets read, in what order, before any check is graded, and
what to note down from each part while reading. A complete procedure
decides the order (issue first? repro evidence first?) and says why
the order matters for the checks that come later. -->

1. **Issue description.** Note the reported behavior (what happens vs.
   what should happen) and the exact trigger conditions (inputs,
   environment, versions, steps). These are what the cause, fix, and
   tests get judged against.
2. **Comments and thread.** Note every maintainer constraint or repo
   convention (for example "don't change the public API", "assign
   first", required test style) and any clue that narrows or
   contradicts the issue's own explanation. If there are none, write
   "none found".
3. **Reproduction evidence.** Note the observable behavior it pins down
   (error text, output, failing input) and each distinguishing
   condition when there is more than one.
4. **The plan, last.** Note its claimed cause, every file and feature
   it names, the proposed fix, the listed changes, and each test.

Why this order: reading the evidence first lets you form your own view
of the cause before the plan can anchor you. Every check from Root
Cause onward compares the plan against facts you already noted, not
against the plan's own framing.

## Evidence gathering

<!-- For each evidence family your rubric's checks name, the concrete
gathering move: which part of the package (or, live, which page or
thread location per your evidence guide) to pull the fact from, and
what to record. A complete procedure leaves no check whose evidence an
executor would have to hunt for. -->

Pull each fact once into short notes, with a quote or location, so no
check needs a second hunt.

- **Summary:** copy the plan's opening description. Record whether it
  names the same problem the issue reports.
- **Root Cause:** quote the plan's stated cause word for word. Beside
  it, list the issue, repro, or comment facts that support it and any
  that contradict it.
- **Fix Targets Cause:** quote the proposed fix. Record whether it
  removes the cause or only hides the symptom (swallowing the error,
  special-casing the repro input, adding a retry or suppression).
- **Scope Files / Scope Features:** list every file, module, and
  feature the plan names. Mark each "tied to the issue by [source:
  description, repro, or comment]" or "no tie found". If the plan names
  no files at all, record whether it names any module, function, or
  area instead.
- **Bounded Change:** list each change the plan makes. Mark any that
  the issue does not need (unrelated refactors, renames, dependency
  upgrades, extra features) and whether the evidence justifies them.
- **Planned Changes:** record, for each change, what changes, where,
  and how, and whether it maps to the cause you recorded.
- **Actionability:** record where the plan says to start and what to
  do, and list anything a newcomer would have to ask before beginning.
- **Test Plan:** for each test, record the setup, the expected
  observable result (a specific output, behavior, or assertion), and
  which issue condition it covers. Note any condition left uncovered.
- **Honest Uncertainty:** go through every causal or fix claim in the
  plan. Mark each as "hedged" (for example "likely", "to be verified
  by X") or "stated as fact", and note whether the evidence confirms
  it.
- **Conventions:** from the notes taken in Read order, list each
  maintainer or repo constraint, then record whether the plan respects
  or contradicts it. If the list is "none found", record that.

## Check execution

<!-- How one check runs against gathered evidence: in what order the
checks execute, what an executor does when evidence for a check is
genuinely absent, and when a check may be graded without re-reading
the whole package. A complete procedure makes two executors grade the
same package the same way. -->

**Order.** Run the checks in this fixed order:

1. Root Cause
2. Fix Targets Cause
3. Scope Files
4. Scope Features
5. Bounded Change
6. Planned Changes
7. Actionability
8. Test Plan
9. Honest Uncertainty
10. Conventions
11. Summary

Root Cause goes first because Fix Targets Cause, Planned Changes, and
Test Plan all depend on it.

**Grading one check.** Compare the evidence notes for that check
against its pass condition in the rubric, then assign `pass`, `fail`,
or `unclear`. Write a one-line reason for every grade, with a short
quote from the plan or the evidence.

**When evidence is absent.**
- If the plan leaves out something it should contain (no cause named, no
  expected test result, no location to start from), grade `fail`.
- If the package itself lacks the material the check needs (for
  example, no conventions anywhere in the thread), apply the rubric's
  stated rule for that case. Conventions with none found is `pass`;
  Scope Features with none listed and none needed is `pass`; Scope
  Files with none listed and no module or area named is `fail`.
- If you cannot tell whether the evidence is present or sufficient
  after checking your notes, grade `unclear`.

**When to re-read.** Grade from your notes whenever they already hold
the quote and source the check needs. Go back to the package only to
resolve an `unclear` grade, and record what you found.

Judge only what the plan writes down. Do not credit intent, or
plausible-sounding language that lacks concrete detail.

## Verdict assembly

<!-- How the per-check grades become the final accept or reject:
apply your rubric's verdict rule, state how unclear grades enter it,
and say what gets quoted in the output for the deciding check. A
complete procedure produces the same verdict from the same grades,
every time. -->

1. **Treat `unclear` as `fail`.** Convert every `unclear` grade to
   `fail` before combining.
2. **Apply the rubric's verdict rule.** Accept only if every `required`
   check is `pass`. Reject if any `required` check is `fail`.
   `preferred` checks never change the verdict; use them only for
   feedback.
3. **Pick the deciding check.** On reject, it is the earliest failing
   `required` check in the execution order above, so the same set of
   grades always names the same check. A failure on Root Cause, Fix
   Targets Cause, or Test Plan is never offset by passes elsewhere.
   On accept, the deciding check is Root Cause.
4. **Quote for the deciding check.**
   - On reject: quote the plan text for that check (or state that the
     plan has no such text), then quote the evidence it conflicts with
     or fails to meet.
   - On accept: quote the plan's stated cause and its fix.
5. **Write the output** in this format:
   - Verdict line: `ACCEPT` or `REJECT`.
   - Per-check table with columns: check, grade, one-line reason.
   - The deciding check's quotes from step 4.