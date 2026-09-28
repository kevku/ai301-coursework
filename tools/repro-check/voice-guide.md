# Voice guide: how I talk upstream

## Who I am in threads

I am a software developer starting my journey into contributting to open sourced software. I plan to reproduce issues from the repo and then work towards a solution to the issue. Readers should expect that I by following the reported steps exactly before proposing a fix. I post threads that are concise and get to points directly.
## Rules I write by

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
- Promises I cannot keep
- Exact timelines
