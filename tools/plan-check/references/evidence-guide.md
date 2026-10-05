# Evidence guide: where evidence lives in a plan package

<!--
THIS IS THE PART YOU WRITE (second week running: the judgment files
stay in your hands). The skill uses this guide as its map: for every
kind of evidence a rubric check names, this file says WHERE to find it
in a plan package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repro-evidence block,
  the candidate plan's scope statement or test plan, the plan comment,
  the repo-facts block). In live mode (where on GitHub or in the
  draft: the issue thread, the student's posted repro comment, the
  repo's docs, the draft plan and comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the stated cause cites behavior the
  repro evidence actually shows") over adjectives ("diagnosis is
  solid").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts twice: your
procedure.md tells the skill WHEN to gather each family, and this
guide tells it WHERE. Write the map you wish your executor had.
-->

## Diagnosis and grounding

<!-- Where the plan states its cause, and where the repro evidence
pins down the behavior that cause must explain. What it means for a
diagnosis to follow from the evidence rather than contradict or
ignore it. -->
The plan states its cause in the diagnosis part of the Candidate plan (usually a line or paragraph labeled cause, diagnosis, or root cause). The behavior it has to explain lives in the Issue section (reported behavior, expected result, stated version) and the Repro evidence block (the steps, then the Expected and Actual lines). The stated cause should explain every observation the repro shows and should not contradict any of them. If the repro environment differs from the version the issue targets, the plan or its comment calls the difference out. In live mode, the cause is in the draft plan, and the evidence is the issue thread and the student's posted repro comment.

## Scope

<!-- Where the plan bounds itself: the in-scope statement, the
not-in-scope line, the files or areas named. What one bounded change
looks like next to a drive-by rewrite. -->
The scope lives in the Candidate plan's change or scope statement: the in-scope part, any not-in-scope line, and the files, modules, or features it names. Each named file or feature should tie back to something in the Issue or the Repro evidence. A bounded change names what will be edited and says what will be left alone. A drive-by rewrite adds refactors, renames, dependency changes, or extra features the evidence never asks for, or gives no limit on what it will touch. In live mode, look in the draft plan for the same in and out statements.

## Executability

<!-- Where the plan says what will actually be done: files or areas,
approach, order of work. What it means for a stranger to be able to
start executing without asking the author anything. -->
The "what will be done" lives in the change statement of the Candidate plan, with the order of work visible in how the change leads into the test. The plan comment should agree with both. A stranger should be able to tell from the plan where to start (file, module, or area), what to change there, and in what order, without asking the author anything. A goal with no location or edit, such as "fix the bug", fails this. In live mode, check the draft plan and its comment for the same details.

## Test plan

<!-- Where the plan says how success will be observed, and how that
maps onto the repro evidence's steps and artifacts. What a decisive
test plan names that a vague one does not. -->
The test plan lives in the test section of the Candidate plan. Map each test onto the Repro evidence: which step is the failing observation, which steps set up the state, and which artifact proves the outcome. A decisive test plan names the observable result (a specific output, behavior, or assertion that flips from failing to passing), ties it to a repro step, and covers each distinguishing condition the evidence or the change touches. A vague one says "verify it works" or "test the fix". In live mode, compare the draft plan's tests against the steps in the student's posted repro comment.

## Honesty

<!-- Where claims meet uncertainty: risks, unknowns, and deviations.
How to tell stated unknowns from false confidence, and where an
honest mid-build deviation gets recorded. -->
The claims live in the cause statement, the test section, and the plan comment. Check each one against the Repro evidence, which shows behavior and not necessarily code. A claim the evidence backs can be stated plainly. A claim the evidence doesn't back (a cause in code the repro never touched, an assumption about other code paths) should be hedged or marked as something to check, and say how it will be checked. False confidence looks like every claim stated flat with no unknowns or risks anywhere. A mid-build deviation belongs in an updated plan or a follow-up comment on the thread, not silently dropped. In live mode, look in the draft plan and its comment for the same signals.

## Comms

<!-- Where the words meet the thread and the repo: the plan comment
read against the issue's maintainer signals (thread highlights, or
the live thread) and against the repo-facts block's stated templates,
contributing asks, and contribution policy (including AI-use
disclosure requirements). What thread-aware looks like next to
boilerplate. -->
The plan comment lives in the Candidate plan comment section. Read it against the Thread highlights (maintainer replies, requests, or claimed work; if there are no comments, there are no signals to contradict) and against the Repo facts block (bug or PR templates, CONTRIBUTING asks, and any AI-use disclosure requirement). Thread-aware looks like a comment that names the issue's specific problem, points to the repro it builds on, and responds to what the thread and repo actually ask for. If the repo requires AI disclosure, the comment includes it; if none is stated, none is expected. It makes no promises or timelines it can't keep. Boilerplate is a generic "I'd like to work on this" that would fit any issue. In live mode, read the draft comment against the real thread and the repo's docs.