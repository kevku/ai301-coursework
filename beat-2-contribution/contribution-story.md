# Contribution: [tank cart rescipie issue]

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** [1]
**Student:** [Kevin Kuang]
**GitHub Username:** [kevku]
**Issue:** [https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/issues/27211]
**Pull Request:** [PR Link](https://github.com/GTNewHorizons/Railcraft/pull/133)

One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that
is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

A Toolkit block looks like this (copy it into each story section and
fill it there):

```text
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to.

**Unit 5: [one line on the tool work]**

The tool I built was issue-scout which was an expansion of the issue-selection tool. Not only does it goes through the Github Issues page to look for issues that I would be interested in. The tool then chooses 5 issues and ranks them from my rubric. It narrows down issues where they're written in Java, Golang, and Python. In the original iteration, the scout found issues where it was out of my scope and expertise, so I gave some background information of what my skill level is an what I would want to improve on. Furthermore, it also goes through checks whether the issues are valid candidates to work on.

**Unit 6: [one line on the tool work]**

The voice-guard skill checks on how I should sound when making a claim, comment, nudge, or asking a question. It provides an extra safety check of my voice in public and ensures that I stay professional. What I had to change from my voice-guard is ensuring that I said Thank You for the issue-claim since many of the other claims from other contributors didn't have to say thank you.

**Unit 7: [one line on the tool work]**

ship-gate double checks the draft of my pr and lets me know if it passes my rubric and voice guard. It cross references the issue, the evidence I was able to reproduce, and check whether the code matches with the plan I've written. When I originally pushed my code into my own repo, the master was behind by 1 commit, so the ship-gate thought someone else's changes were part of my changes and failed. I had to sync and then re-run the tool.

**Unit 8: [one line on the tool work]**

pr-monitor checks on the current branch's PR and notifies the state. It provides any recent activity and suggests whether I should nudge or I need to address a comment. I set the rules where if they don't notice it within the next 1-2 weeks, I make a nudge to the reviewer about the PR. It also ensures the nudging and pinging format is correct and lets me know what's wrong with the nudge I'm about to make.

---

## Why I Chose This Issue

With the issue selection page, I chose the languages I was interested like Go, Python, and Java. Then I narrowed the search down to "good first issue" and "help wanted". This showed up the GTNewHorizons organization under Java and Python. The original issue was fixing a typo in one of the quest books which I wanted to claim. As a few days went by, someone else worked on it and made a PR. After a couple of days, I narrowed the search into the organization itself and then there were new issues that appeared and I chose the tank recipe issue. I chose this organization because I've played their modpack before and I was curious how bugs and integration of different mods worked. I think when comparing the scout and search on the issue selection site is that the scout definitely searched for the smaller repos that are maintained by a couple of people and does not have much of a reputation. Given that, those issues are not a well suited for this type of assignment because some may not be well documented.
[Link to Claim Comment](https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/issues/27211#issuecomment-6659287974)

**Toolkit**

- Tool: issue-scout 
### Search Strategy
#### Queries

gh search issues --label "good first issue" --language go --state open --no-assignee --updated ">2026-07-23" --limit 100
I'd like to practice Go.

gh search issues --label "help wanted" --language go --state open --no-assignee --updated ">2026-07-23" --limit 100
Issues labeled "good first issue" or "help wanted" are ideal.

gh search issues --label "good first issue" --language python --state open --no-assignee --updated ">2026-07-23" --limit 100
I'm most comfortable in Python and Java.

gh search issues "database" --label "good first issue" --language python --state open --no-assignee --limit 100
Backend programming: working with APIs, data and databases, and fixing bugs.

gh search issues "api" --label "help wanted" --language java --state open --no-assignee --limit 100
Developer tooling (CLIs, SDKs, API integrations).

#### Ranking filters

- drop any result with an assignee
- Golang and Python have higher ranking over Java and other languages
- Python is higher ranking than Golang
- feature addition will rank higher than bugs
- both feature and bugs are higher than documentation and tests

### Rubric
| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
|Maintainer activity|The last 5 default-branch commit dates and authors in the repo-facts block; maintainer comments/reviews/merges in the issue or PR history|At least one of the following within the past 60 days: a commit or PR merge to the default branch (merging implies maintainer/write access), or a comment/review from an account tagged OWNER, MEMBER, or COLLABORATOR|required|
|Issue is unclaimed|The issue's assignee field, labels, and the full comment thread on the issue.|The issue has no assignee and the issue body/comments do not indicate that someone has already committed to working on it|required|
|No active PR for the issue|The repository's open pull requests, including PR title, body, linked issues, and recent comments; see references/evidence-guide.md for the prescribed PR evidence|There is no open PR that addresses the issue or clearly claims to implement the same requested change|required|
|Locations are identifiable|Issue body, linked code references, comments|The issue body and/or comment thread describe a specific, reproducible symptom, behavior, or requested feature (including trigger conditions, affected command/flag/UI area,or expected vs. actual behavior) precise enough that a contributor could locate the relevant code through normal searching— without requiring an explicit file list, and regardless of whether the exact implementation approach is already decided.|required|
| scope-feasible |Issue body: the work it asks for|The issue describes one identifiable piece of work someone could start:a behavior, a gap, or a task you can point at. It fails only when there is no single piece of work in it: a codebase-wide checklist, an "improve X everywhere", or a container issue tracking many sub-tasks. An open design edge, an "etc.", or several files involved never fails this check; that raises the difficulty note instead.|required|
|AI contribution allowed|The repository's CONTRIBUTING.md, README.md, and CODE_OF_CONDUCT.md (or equivalent contribution policy documentation)|None of the repository's contribution policy documentation explicitly prohibits AI-generated or AI-assisted contributions|required|

- What it produced: the scan over the entire Github gave me 5 results that passed and it calibrated the issues with the goals, the check marks, and provides suggestions on which one is better than another. Then I reran the scout on the issues that I found interestin on the Codepath issue site.
- Difficulties: none met
- What changed: nothing

---

## Understanding the Issue

**Problem Description**

In the modpack of `GTNH`, the recipe of the `tank cart` uses a `hammer`, `wrench`, `screwdriver` from `GregTech`, `minecart`, and `tank` from `BC Factory`. There is an uncrafting feature where if the `tank cart` is placed in the crafting table on its own, it gives back a `tank` and `minecart` intended in `Railcraft`. The bug, is that when uncrafting the `tank cart` it gives back the user a `minecart` (intended) and an `iron tank gauge` (not intended). Rather than having it return a `iron tank gauge` from `Railcraft`, it should provide a `tank` from `BC Factory`.

**Expected Behavior**

When uncrafting the `tank cart`, it should give a `minecart` and `tank` from `BC Factory.`

**Current Behavior**

When uncrafting the `tank cart`, it gave a `minecart` and `iron tank gauge` from `Railcraft`.

**Affected Components**

In the `Railcraft` repo, theres a file called `EnumCart.java`, then in lines `101-104` there's a `getContents()` function. There's a switch case in there that if the item is type `TANK`, then it returns `EnumMachineBeta.TANK_IRON_GAUGE.getItem()`. This hardcodes the item of the `iron tank gauge` to return after uncrafting. This should just be a getter that returns the item stored which is a generic `iron tank gauge` defined when the cart is instantiated. Then to incorporate it with the other modpack, we need to work in the `NewHorizonsCoreMod` that integrates the multiple mods together. Given that there is a `setContents()`, we should be able to set the cart content to the `tank` from `BC Factory`.

**Toolkit**

- Tool: voice-guard
- What it produced: It provides a suggestion whether my claim comment needs to be changed and whether it matches with how I should sound on threads. It provides a json of pass or fail for each of the checks.
- Difficulties: none met
- What changed: I had to change the part where I needed to say "Thank you" for claims, sine the repo I check did not have many people say "Thank you", they just said "I would like to work on this" or "I start investigating this".

---

## Reproduction Process

**Environment Setup**

- OS: macOS Tahoe v26.4.1
- Java is version 25.0.1, using 64 (aarch64) architecture, from Microsoft
- Prism Launcher version: 11.1.1 (official)
- Modpack: GTNH 2.9.0 (final, official website). The issue reporter is on 2.9.0 rc2; the bug still reproduces on 2.9.0 final.
- Mod Suspected where the bug lives:
  - [GTNH Coremod](https://github.com/GTNewHorizons/GT-New-Horizons-Modpack)
  - [Railcraft](https://github.com/GTNewHorizons/Railcraft)

**Steps to Reproduce**

1. Download the Prism Launcher and Login with Minecraft Account
2. Download `zip` file of the official modpack `v2.9.0` from the official website. I've used the version running for Java 17-26.
3. Drag the `zip` file into Prism where it should create the new GTNH Instance and double click to launch.
4. In the game, hop into a Creative world and grab the `tank cart` item. Then in the crafting table place it anywhere in the crafting area.
5. This gives a `minecart` and an `iron tank gauge`, not the `tank` from `BCFactory`.
6. Double Check that it's not just the creative item, grab the materials for the recipe for the `tank cart`. Manually create an `hammer`, `screwdriver`, and `wrench` from `GregTech` using `iron ingots` and `sticks` which is used in the crafting recipe.
7. Follow anyone of the recipe for the `tank` from `BCFactory` which is needed for the `tank cart`. I used the `obsidian glass` version of the recipe.
8. Follow anyone fo the recipe for the `minecart`. I used the `iron plate` version of the recipe.
9. Follow the crafting recipe for the `tank cart` using the `hammer`, `screwdriver`, `wrench`, `tank`, and `minecart`.
10. Place the `tank cart` in the crafting table.
11. This gives a `minecart` and an `iron tank gauge`, not the  `tank` from `BCFactory` which is used in the crafting recipe.

**Reproduction Evidence**

- **Commit showing reproduction:** none
- **Screenshots/logs:** 

### Iron Tank gauge that Came Out of Uncrafting
<img width="1702" height="1014" alt="Uncraft Original" src="https://github.com/user-attachments/assets/9d49336d-e351-4e48-aa3c-d2144da3960a" />

These gif show the process of uncrafting 3 `tank minecart` which gave 3 `minecart` (as expected), but 3 `iron tank gauge` (should be 3 `tank` from `BCFactory`).
- **My findings:** 
I thought I would only need to work in one Repo, but turns out the modpack is decoupled, so I needed to work in both `Railcraft` and `NewHorizonsCoreMod` to integrate them properly.

**Toolkit**

- Tool: repro-check
- What it produced: 
It produced a JSON and told me what I needed to fix in the repro, and it was the environment step where it failed me. After changing how the mods versioning worked then it passed.
``` json
{
  "item": "https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/issues/27211",
  "checks": [
    {"name": "Environment Check", "grade": "fail", "evidence": "Two conflicting Modpack lines (line 8 'utilizing RC2' vs. line 9 'final'), and the parenthetical '(rc2 is not a version, it just specifies the mod)' contradicts the same line's statement that the reporter is on 2.9.0 rc2."},
    {"name": "Steps of Reproduction", "grade": "pass", "evidence": "Eleven numbered steps from Prism install through crafting and uncrafting the tank cart."},
    {"name": "Files & Commands", "grade": "pass", "evidence": "Recipe steps (hammer/screwdriver/wrench + BCFactory tank + minecart) match the issue's 'crafting tank cart uses minecart and rc tank' description."},
    {"name": "Expected vs Actual", "grade": "pass", "evidence": "'Expected: minecart and tank from BCFactory. Actual: minecart and iron tank gauge from BCFactory.' matches the issue's observed output."},
    {"name": "AI policy compliance", "grade": "pass", "evidence": "Repo has no CONTRIBUTING.md and no stated AI policy; README only links Discord/wiki."},
    {"name": "Claim comment", "grade": "pass", "evidence": "Posted claim (issuecomment-6659287974): 'I'll look into tank cart uncraft recipe in `EnumCart.java`. Thank you!' — intent + first step, no deadline."}
  ],
  "verdict": "reject"
}
{
  "item": "https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/issues/27211",
  "checks": [
    {"name": "Environment Check", "grade": "pass", "evidence": "Line 8: 'Modpack: GTNH 2.9.0 (final, linked). The issue reporter is on 2.9.0 rc2; the bug still reproduces on 2.9.0 final.' — both versions stated, delta called out, bug confirmed on newer."},
    {"name": "Steps of Reproduction", "grade": "pass", "evidence": "Eleven numbered steps from Prism install through crafting and uncrafting the tank cart."},
    {"name": "Files & Commands", "grade": "pass", "evidence": "Recipe steps (hammer/screwdriver/wrench + BCFactory tank + minecart) match the issue's 'crafting tank cart uses minecart and rc tank' description."},
    {"name": "Expected vs Actual", "grade": "pass", "evidence": "'Expected: minecart and tank from BCFactory. Actual: minecart and iron tank gauge from BCFactory.' matches the issue's observed output."},
    {"name": "AI policy compliance", "grade": "pass", "evidence": "Repo has no CONTRIBUTING.md and no stated AI policy; README only links Discord/wiki."},
    {"name": "Claim comment", "grade": "pass", "evidence": "Posted claim (issuecomment-6659287974): 'I'll look into tank cart uncraft recipe in `EnumCart.java`. Thank you!' — intent + first step, no deadline."}
  ],
  "verdict": "accept"
}
```
- Difficulties: When comparing the issue and my reproduction step, the main difficulty I had was that it kept saying my version is not correct due to the fact that the isse said `2.9.0 rc2`. 2.9.0 is the official and latest release of the modpack at the time of working on it. Then the contributor who wrote the issue specified what mod it focuses on, which is why they added `rc2` a.k.a `Railcraft`. My check took the versioning too seriously and kept saying I had an ambiguous version mismatch. Since this may be a one off due to a mod pack, I didn't change the check as majority of other repos requires exact version. Instead I just said this is the `final` release, which occurs the same as the `rc2` version.
- What changed: nothing

---

## Solution Approach

**Analysis**

Given with the hint provided from the comment in the issue, the `iron tank gauge` is hardcoded as the `setContents()` function. Since the uncrafting feature in implemented in `Railcraft`, we need to set the `Railcraft` content values to the `tank` from `BC Factory` through the `NewHorizonsMod`. All of the mods that are listed in the organization are standalone, so the `NewHorizonsMod` bridges the mods together and integrates into the modpack as a whole.

**Proposed Solution**

Utilizing the Java API, as suggested in the comment, allow other mods to interact and change the contents. This will allow the correct item to be returned on uncrafting of the `tank cart` that is already implemented in `Railcraft`.

**Implementation Plan**

1. Modify `EnumCart.java` in the `Railcraft Repo` where instead of returning the hardcoded `iron tank gauge` that is defined in `Railcraft`, return the stored valued of `contents` itself.
2. Utilizing the Java api, the rest of the work should be done in the `NewHorizonsMod`, which should utilize the `setContents()` from `Railcraft`. The `setContents()` should set the content as the `tank` from `BC Factory`.

[Record deviations here as they happen: what changed mid-build and
why. A recorded deviation is honest work; silent drift is not.]

**Toolkit**

- Tool: plan-check
- What it produced:
These were the json that it produced and gave me advice on how to change the comment and gave me a better understanding of the issue.
```json
{
  "item": "https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/issues/27211",
  "checks": [
    {"name": "Root Cause", "grade": "pass", "evidence": "plan-comment.md:1 'comes from 2 locations ... EnumCart.java and ... ModuleTransport.java' matches EnumCart.java:105 and ModuleTransport.java:198 plus maintainer link"},
    {"name": "Fix Targets Cause", "grade": "pass", "evidence": "Step 1 removes the EnumCart.java return; step 2 overrides the ModuleTransport.java:198 stored gauge with the BC Factory tank"},
    {"name": "Scope Files", "grade": "pass", "evidence": "EnumCart.java, ScriptRailcraft.java, and ModuleTransport.java (named as cause) all tie to the refund"},
    {"name": "Scope Features", "grade": "pass", "evidence": "setContents() Java API matches maintainer direction; BC Factory tank matches the GTNH recipe"},
    {"name": "Bounded Change", "grade": "pass", "evidence": "Two code changes plus existing repo checks; nothing unrelated"},
    {"name": "Planned Changes", "grade": "pass", "evidence": "Step 2 names ScriptRailcraft.java and recipe-creation timing; ScriptLoader runs at FMLLoadCompleteEvent (MainRegistry.java:404-406)"},
    {"name": "Actionability", "grade": "pass", "evidence": "Both steps name a file and the action to take there"},
    {"name": "Test Plan", "grade": "pass", "evidence": "plan.md:7 uncrafting 'should give me a minecart and tank from BC Factory instead of the iron tank guage'"},
    {"name": "Honest Uncertainty", "grade": "fail", "evidence": "plan-comment.md:1 'The NewHorizonsCoreMod also has iron tank guage as part of its contents' stated as fact; NHCoreMod has no setContents/EnumCart and ScriptRailcraft.java uses only machine.beta meta 0 (iron wall), never the gauge"},
    {"name": "Conventions", "grade": "pass", "evidence": "Follows maintainer's Java API direction; spotlessCheck and build match the CI workflow"},
    {"name": "Summary", "grade": "pass", "evidence": "plan.md:2 states the uncraft-gives-gauge issue (preferred)"},
    {"name": "AI policy compliance", "grade": "pass", "evidence": "GTNH AI_POLICY.md allows reviewed AI help on issues; disclosure only required in PRs (CONTRIBUTING.md:98)"}
  ],
  "verdict": "reject"
}

{
  "item": "https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/issues/27211",
  "checks": [
    {"name": "Root Cause", "grade": "pass", "evidence": "plan-comment.md:1 'comes from 2 locations ... EnumCart.java and ... ModuleTransport.java' matches EnumCart.java:105 and ModuleTransport.java:198 plus maintainer link"},
    {"name": "Fix Targets Cause", "grade": "pass", "evidence": "Step 1 removes the EnumCart.java return; step 2 sets contents to the BC Factory tank, replacing the ModuleTransport.java:198 gauge"},
    {"name": "Scope Files", "grade": "pass", "evidence": "EnumCart.java, ScriptRailcraft.java, and ModuleTransport.java (named as cause) all tie to the refund"},
    {"name": "Scope Features", "grade": "pass", "evidence": "setContents() Java API matches maintainer direction; BC Factory tank matches ScriptRailcraft.java:1009"},
    {"name": "Bounded Change", "grade": "pass", "evidence": "Two code changes plus existing repo checks; nothing unrelated"},
    {"name": "Planned Changes", "grade": "pass", "evidence": "Step 2 names ScriptRailcraft.java and recipe-creation timing; ScriptLoader runs at FMLLoadCompleteEvent (MainRegistry.java:404-406)"},
    {"name": "Actionability", "grade": "pass", "evidence": "Both steps name a file and the action to take there"},
    {"name": "Test Plan", "grade": "pass", "evidence": "plan.md:7 uncrafting 'should give me a minecart and tank from BC Factory instead of the iron tank guage'; dev runs check no crash or new errors"},
    {"name": "Honest Uncertainty", "grade": "pass", "evidence": "Comment's claims all match code (EnumCart.java:105, ModuleTransport.java:198, ScriptRailcraft.java:1009, no setContents in NHCoreMod); in-game outcome worded as 'should give me'"},
    {"name": "Conventions", "grade": "pass", "evidence": "Follows maintainer's Java API direction; spotlessCheck and build match the CI workflow"},
    {"name": "Summary", "grade": "pass", "evidence": "plan.md:2 states the uncraft-gives-gauge issue (preferred)"},
    {"name": "AI policy compliance", "grade": "pass", "evidence": "GTNH AI_POLICY.md allows reviewed AI help on issues; disclosure only required in PRs (CONTRIBUTING.md:98)"}
  ],
  "verdict": "accept"
}
```
- Difficulties:
First one failed it because the comment said "The NewHorizonsCoreMod also has iron tank guage as part of its contents", which the code doesn't back up. Your edit to plan-comment.md fixed that claim and the plan passed.
- What changed: nothing

---

## Testing Strategy

The check that proved my fix was going in game, getting the `tank cart` and uncrafting it. Then I only receive a `tank` from `BC Factory` and not an `iron tank gauge` from `Railcraft` shown here:

### Before Modification
<img width="1702" height="1014" alt="Uncraft Original" src="https://github.com/user-attachments/assets/9d49336d-e351-4e48-aa3c-d2144da3960a" />


### After Modification
<img width="1702" height="1014" alt="Uncrafting Modified" src="https://github.com/user-attachments/assets/31efe384-871a-483e-96da-3002044cf7c6" />

**Toolkit**

- Tool: No tool used, the testing is client side testing on the game, and the only tests are `./gradlew spotlessCheck`, and `./gradlew build` which is part of ship-gate
- What it produced: N/A
- Difficulties: none met
- What changed: Nothing

---

## Implementation Notes

**[11/10/26]**

In the `EnumCart.java` of the `Railcraft` repo, I removed the switch case that causes the uncrafting to always provide an `iron tank gauge` when `iron tank gauge` is available in the modpack. In this case, the GTNH modpack has it enabled. Then in the `NewHorizonsCoreMod` repository, I went to the `ScriptRailcraft.java` and added the import for the setter method from `Railcraft`, then after the crafting recipe of the `tank cart`, I used the setter method to set the content to be the `tank` from `BC Factory`.


**Toolkit**

- Tool: pr-check
- What it produced:
``` json
{
  "item": "GTNewHorizons/Railcraft#fix/27211-tank-cart-recipe",
  "checks": [
    {"name": "No unplanned changes", "grade": "fail", "evidence": ".github/workflows/build-and-test.yml adds release/** branches; not in plan boundary, no deviation note"},
    {"name": "Planned work delivered or disclosed", "grade": "unclear", "evidence": "Plan step 2 (NHCoreMod setContents) absent from diff; only the vague box 'requires another PR in order to merge' with no PR named"},
    {"name": "Description matches the diff", "grade": "fail", "evidence": "Claims it 'will give the Tank from BC Factory' but diff only removes the iron-gauge case; workflow hunk unmentioned"},
    {"name": "Behavior evidence is observable", "grade": "pass", "evidence": "test_evidence.md reruns steps; before = minecart + iron tank gauge, expected after = minecart + BC tank"},
    {"name": "Repo's own checks shown", "grade": "pass", "evidence": "Manifest: spotlessCheck ok, build ok"},
    {"name": "Fix is visible, no debris", "grade": "fail", "evidence": "Unrelated CI workflow hunk and merge commit 05f2c50f ride along with the EnumCart.java fix"},
    {"name": "Template filled with real content", "grade": "pass", "evidence": "Repo ships no PR template"},
    {"name": "AI-use disclosure and stated policy honored", "grade": "pass", "evidence": "'AI was used to help understand the structure of the mods and functions.' (tool unnamed; no policy text in package)"},
    {"name": "Maintainer direction engaged", "grade": "pass", "evidence": "No issue thread or maintainer direction found"},
    {"name": "Title says what and where", "grade": "pass", "evidence": "'Fixed Tank Cart Uncrafting Recipe' names the specific thing changed"}
  ],
  "verdict": "reject"
}
{
  "item": "GTNewHorizons/Railcraft#fix/27211-tank-cart-recipe",
  "checks": [
    {"name": "No unplanned changes", "grade": "pass", "evidence": "Only src/main/java/mods/railcraft/common/carts/EnumCart.java changed, matching plan step 1; the import removal follows from the removed switch."},
    {"name": "Planned work delivered or disclosed", "grade": "pass", "evidence": "Step 1 is in the diff; step 2 (CoreMod) is disclosed via 'This PR requires another PR in order to merge'."},
    {"name": "Description matches the diff", "grade": "pass", "evidence": "'just return the contents instead of going through the special case' matches the removed TANK switch case in getContents()."},
    {"name": "Behavior evidence is observable", "grade": "pass", "evidence": "test_evidence.md shows the reproduction before (iron tank gauge) and expected/after (BC Factory tank) with screenshots."},
    {"name": "Repo's own checks shown", "grade": "pass", "evidence": "Manifest: spotlessCheck ok and build ok, no checks excluded."},
    {"name": "Fix is visible, no debris", "grade": "pass", "evidence": "+2/-9 in one hunk plus an import removal; no debug, dead code or churn; commit message is descriptive."},
    {"name": "Template filled with real content", "grade": "pass", "evidence": "Repo ships no PR template."},
    {"name": "AI-use disclosure and stated policy honored", "grade": "pass", "evidence": "Description: 'AI was used to help understand the structure of the mods and functions.' No policy file asks for more; no AI co-author trailer on the commit."},
    {"name": "Maintainer direction engaged", "grade": "pass", "evidence": "No issue thread found, so no maintainer direction exists."},
    {"name": "Title says what and where", "grade": "pass", "evidence": "'Fixed Tank Cart Uncrafting Recipe' names the tank cart uncrafting change."}
  ],
  "verdict": "accept"
}
```
- Difficulties: 
At first I was confused as to why it passed a couple days prior, but then it failed when I was about to make the PR. This was because my main/master branch was behind by 1 commit, so I had to sync my master and branch in order to get it to pass. Additionally, since the pr does not include the evidence assets, I had to add comments saying that they'll be added on Github.
- What changed: nothing

---

## Pull Request

**PR Link:** [PR Link](https://github.com/GTNewHorizons/Railcraft/pull/133)

**PR Description:** 
# Fixed Tank Cart Uncrafting Recipe
## Summary
This pr addresses the uncrafting of the tank cart from Railcraft. In EnumCart.getContents(), it will just return the contents instead of going through the special case that forces the return to be an Iron Tank Gauge. Then with [NewHorizonsCoreMod PR](https://github.com/GTNewHorizons/NewHorizonsCoreMod/pull/2028), it will set the content to the Tank from BC Factory.

Fixes issue GTNewHorizons/GT-New-Horizons-Modpack#27211

### Before Modification
<img width="1702" height="1014" alt="Uncraft Original" src="https://github.com/user-attachments/assets/9d49336d-e351-4e48-aa3c-d2144da3960a" />


### After Modification
<img width="1702" height="1014" alt="Uncrafting Modified" src="https://github.com/user-attachments/assets/31efe384-871a-483e-96da-3002044cf7c6" />


AI was used to help understand the structure of the mods and functions.

## Checklist
- [x] I have tested this PR in DevEnv
- [x] I have tested this PR in Fullpack
- [x] This PR is in compliance with the [GTNH AI Policy](https://github.com/GTNewHorizons/GTNH-Dev-Doc/blob/master/AI_POLICY.md)
- [x] This PR requires another PR in order to merge

**Maintainer Feedback:**

- [11/10/2026]: none yet

**Status:** Awaiting Review

**Toolkit**

- Tool: ship-gate
- What it produced:
``` json
{
  "item": "GTNewHorizons/Railcraft#fix/27211-tank-cart-recipe",
  "checks": [
    {"name": "No unplanned changes", "grade": "pass", "evidence": "Only EnumCart.java changed, which plan step 1 names; removed import is a direct consequence."},
    {"name": "Planned work delivered or disclosed", "grade": "pass", "evidence": "Step 1 is in the diff; CoreMod step disclosed via 'This PR requires another PR in order to merge'."},
    {"name": "Description matches the diff", "grade": "pass", "evidence": "Claim that getContents() skips the special case matches the single hunk."},
    {"name": "Behavior evidence is observable", "grade": "fail", "evidence": "Results table after rows still read '[DevEnv / Fullpack]' and 'local build of [CoreMod branch/PR]'; after result cannot be tied to a build."},
    {"name": "Repo's own checks shown", "grade": "pass", "evidence": "Manifest: spotlessCheck ok, ./gradlew build ok."},
    {"name": "Fix is visible, no debris", "grade": "pass", "evidence": "+2/-9 in one hunk plus unused import removal; no debris."},
    {"name": "Template filled with real content", "grade": "pass", "evidence": "Repo ships no PR template."},
    {"name": "AI-use disclosure and stated policy honored", "grade": "pass", "evidence": "No repo asks found; draft states 'AI was used to help understand the structure of the mods and functions.'"},
    {"name": "Maintainer direction engaged", "grade": "pass", "evidence": "No issue thread found, so no maintainer direction to answer."},
    {"name": "Title says what and where", "grade": "pass", "evidence": "'Fixed Tank Cart Uncrafting Recipe' names the changed behavior."}
  ],
  "verdict": "reject"
}
{
  "item": "GTNewHorizons/Railcraft#fix/27211-tank-cart-recipe",
  "checks": [
    {"name": "No unplanned changes", "grade": "pass", "evidence": "Only src/main/java/mods/railcraft/common/carts/EnumCart.java changed, matching plan step 1; the import removal follows from the removed switch."},
    {"name": "Planned work delivered or disclosed", "grade": "pass", "evidence": "Step 1 is in the diff; step 2 (CoreMod) is disclosed via 'This PR requires another PR in order to merge'."},
    {"name": "Description matches the diff", "grade": "pass", "evidence": "'just return the contents instead of going through the special case' matches the removed TANK switch case in getContents()."},
    {"name": "Behavior evidence is observable", "grade": "pass", "evidence": "test_evidence.md shows the reproduction before (iron tank gauge) and expected/after (BC Factory tank) with screenshots."},
    {"name": "Repo's own checks shown", "grade": "pass", "evidence": "Manifest: spotlessCheck ok and build ok, no checks excluded."},
    {"name": "Fix is visible, no debris", "grade": "pass", "evidence": "+2/-9 in one hunk plus an import removal; no debug, dead code or churn; commit message is descriptive."},
    {"name": "Template filled with real content", "grade": "pass", "evidence": "Repo ships no PR template."},
    {"name": "AI-use disclosure and stated policy honored", "grade": "pass", "evidence": "Description: 'AI was used to help understand the structure of the mods and functions.' No policy file asks for more; no AI co-author trailer on the commit."},
    {"name": "Maintainer direction engaged", "grade": "pass", "evidence": "No issue thread found, so no maintainer direction exists."},
    {"name": "Title says what and where", "grade": "pass", "evidence": "'Fixed Tank Cart Uncrafting Recipe' names the tank cart uncrafting change."}
  ],
  "verdict": "accept"
}
```
- Difficulties: none met
- What changed: nothing

---

## Learnings and Reflections

**Technical Skills Gained**

One thing I learned about Java was during the testing phase after implementation. Generally, it was easy to test independently with `./gradlew runClient21`. But when doing this, most of the original behaviors act the same since both mods rely on each other. `Railcraft` mod relies on `NewHorizonsCoreMod` to set the new recipe and `Railcraft` needs to set the content when `NewHorizonsCoreMod` makes the setter call. Then when launching the modpack with the new changes I ran into a versioning issue with what was registered. I learned that you need to push a local Maven change of `Railcraft` and then in the `NewHorizonsCoreMod`, `gradle.dependencies` add the local maven to apply those changes. This taught me how these `jar` files work interconnectedly during development.

**Challenges Overcome**

What I found a bit difficult was understanding how the mods within the modpack integrates with each other. I was confused as to how recipes and properties are transferred from one mod to another. After having AI help me understand the structure of the modpack and learning that the `NewHorizonsCoreMod` is the bridge and requiring the mods itself like `Railcraft`. Originally I was not sure how the recipe integrated where an item like the `tank` from `BC Factory` turns into the `tank cart` from `Railfactory`.

**What I'd Do Differently Next Time**

Next time I'll need to be more careful of the modpack version, and each of the individual mod versions because when plugging back into the main modpack, I had to temporarily pull an older version of the mod, make the changes, build the mod and test in the full modpack. The developer version of the mods off of Github may be many commits ahead and the documentation of the version will not be official.

---

## Resources Used

The Wiki from GTNH gave me the information on how to get the developer's version of the mod running and how to troubleshoot common issues with Gradle. Additionally, it gave information on how to get build running and the format of contributing. Then the comment gave a massive hint on where to start the issue.

- [GTNH Wiki](https://wiki.gtnewhorizons.com/wiki/Main_Page)
- [GTNH Contribution](https://wiki.gtnewhorizons.com/wiki/GTNH_Contribution_Guide_for_Beginners)
- [GTNH Development](https://wiki.gtnewhorizons.com/wiki/Development)
- [Comment that Lead to the Bug](https://github.com/GTNewHorizons/GT-New-Horizons-Modpack/issues/27211#issuecomment-6557974136)
