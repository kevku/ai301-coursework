# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-facts block, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; the rubric swap showed you what that feels
like. Write the map you wish your grader had.
-->

## Environment

<!-- Where the environment record lives, and what a sufficient one
looks like against the issue's stated target. -->
The environment record lives at the top of the Repro Report, should contain the OS, name of tools and its versions. The versions/OS named match what the issue targets, or the difference is called out. It should be in a list format of the environment.

## Steps

<!-- Where the reproduction steps live, and what makes them followable
by a stranger, starting state to trigger. -->
The steps should live under the Environment. Make a numbered list of actions that were taken and if they were commands, the commands should be in code blocks.

## Behavior shown

<!-- Where the artifacts live (output excerpts, logs, screenshots),
and what it means for an artifact to show the issue's behavior rather
than an adjacent one. -->
The artifacts of output excerpts, logs, screenshots should live under the steps and reference any steps that lead to the artifacts. For example it can be "These logs were generated from step #2". The error message or output matches what the issue describes, not just some error.
## Honesty

<!-- Where claims and their backing meet: how to tell a report that
says exactly what happened (including an honest cannot-reproduce) from
one that claims more than its evidence shows. -->
The expected claims and actual findings should live under the behavior shown. The expected and the actual should be bullet points and expected is always first. Every claim in the report is backed by an artifact, and if the steps didn't reproduce the issue, the report says so instead of implying success.
## Comms

<!-- Where the words meet the repo: the claim comment against the
issue, the comments against the repo's stated templates and
contribution policy (including AI-use disclosure requirements), and
what specific-and-honest looks like next to boilerplate. -->
The comments should be made below the honesty and claims and state any use of external sources or AI was used to help recreate the issue. It names the issue's specific problem and what was actually done, and it makes no promises or timelines it can't keep. Any additional comments are checked against the issue context and the repo-facts block (CONTRIBUTING, templates, AI policy).
