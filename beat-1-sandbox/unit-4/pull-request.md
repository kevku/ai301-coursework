# Unit 4 — Test and Submit

Path: `beat-1-sandbox/unit-4/pull-request.md`

Record of the pull request you opened against the Path Review repo, and of the evaluation
runs that produced `eval-run.txt`. This file is graded at the path above; a copy kept
anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your pull request

**Pull request**

[Link to Pull Request](https://github.com/codepath/pathreview-ai301-fa26-s1/pull/200)

**Branch**

feat/35-webhook-notifications

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

19/20 → 20/20 

**Package analysis**

I picked `pkg-11`. The gold label is accept (a clear-accept). My earlier rubric rejected it, and the deciding check was "AI-use disclosure and stated policy honored." All of my rubric except the AI-use disclosure has passed. 

The disclosure failed because my old pass condition required AI use to be disclosed and to name the tool. The description says the change "was AI-assisted with me reviewing and understanding every line, and this text is in my own words." It names no tool. The repo's policy (CONTRIBUTING.md "Use of AI" and AI_POLICY.md) asks only for a human in the loop who understands the work and for maintainer-facing text written in the contributor's own words. It never asks for a tool name. My rubric was stricter than the repo, so it rejected a package that met every ask the repo actually states. My revised rubric judges the disclosure against what the policy asks, so it now reads pkg-11 as accept.

**Check rationale**

> |AI-use disclosure and stated policy honored|The repo-facts block's contributing instructions and stated policy (AI-use disclosure, branch or commit naming, issue-reference format), read against the description and commits|Every ask the repo states is visibly met in the form the policy asks for. If the policy requires disclosure, the disclosure is present and includes whatever details the policy names (a tool name, a description of use, a human-written statement). Details the policy does not ask for are not required. A stated ask that the package visibly skips is a fail. If the repo states no asks, nothing counts against the package.|required|

It reads this way because of what I revised. The first version said disclosure had to "name the tool used." I took that from a lecture example, where the disclosure named the model, and treated it as a universal rule. I replaced the fixed standard with "whatever details the policy names," so the repo's own policy sets the bar. I rejected simply dropping the disclosure requirement. That would let a package that skips a required disclosure pass, and the standards-wall packages in the eval depend on that failing. So I kept "a stated ask that the package visibly skips is a fail."

**Trade-offs**

The AI rubric change gives up a uniform disclosure bar. Before, every package needed a tool name, which is simple and consistent. Now the grader has to read each repo's policy and apply it, so two graders could disagree on a policy with vague wording, such as one that asks for disclosure but doesn't say what it should contain. I accept that a package that discloses minimally to agree with the gold labels.

The change flipped pkg-11 from reject to accept, taking the eval from 19/20 to 20/20. 
---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/pr-precheck/`.
