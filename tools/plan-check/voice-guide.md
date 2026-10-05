# Voice guide: how I talk upstream

<!--
THIS IS A CARRY-OVER SLOT, not a new hole. You wrote this guide in
week 2; paste your filled week-2 voice-guide.md here, whole. It is not
re-authored and it is not graded as new work this week.

Then reread it with the plan comment in mind. Your claim and repro
comments promised and reported; a plan comment commits you to an
approach in front of the people who maintain the code. If your rules
do not cover that register (for example: how you state an approach you
are not certain of, or how you respond when a maintainer already
suggested a direction), extend the guide with what it needs. Extending
is allowed and encouraged; starting over is not required.

Live mode reads this file before your plan comment goes out and
reports any rule your draft breaks. Eval mode ignores it entirely,
because your voice is yours and carries no gold labels.
-->

## Who I am in threads

<!-- Paste your week-2 section here. -->
I am a software developer starting my journey into contributting to open sourced software. I plan to reproduce issues from the repo and then work towards a solution to the issue. Readers should expect that I by following the reported steps exactly before proposing a fix. I post threads that are concise and get to points directly.

## Rules I write by

<!-- Paste your week-2 rules here, wrong/right pairs and all. Add any
rule the plan-comment register needs that your week-2 comments did
not. -->
### Rule: Appreciating a Request

Say "Thank You!" when you're asking for something like a help, a review, an assignment. Leave it off when the comment is just reporting a fact or update.

- Wrong: "I would like to be assigned this issue."
- Right: "I would like to be assigned this issue. Thank you!"

### Rule: Keep Narrative in Prose, Split Out the Diagnostic List

When a comment mixes what you did (a sequence of actions) with what it could be (multiple causes/tools), tell the narrative as prose and break only the causes/tools into a bullet list - don't bullet the sequence, and don't bury the causes back inside the narrative sentence.

- Wrong: "I tried restarting the worker, then checked the logs, then it seemed to point to either stale cache in Redis or a race condition in the webhook handler, so I also looked at the retry config."
- Right: "I restarted the worker, checked the logs, and looked at the retry config. It could be:
  - Stale cache in Redis
  - Race condition in the webhook handler"

### Rule: No Templated Sign-offs

Don't close comments with a generic wrap-up line ("Please let me know if you have any questions," "Thanks for your patience") unless it's actually true in context.

Wrong: "I've made the fix. Please let me know if you have any further questions or concerns!"
Right: "Fixed - should be good now."

## Things I never post

<!-- Paste your week-2 list here; extend it if planning tempts you
toward new ones (overpromised timelines are the classic). -->
- Promises I cannot keep
- Exact timelines
