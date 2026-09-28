# Rubric: is this reproduction package ready to post?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
|Environment Check|Provides information about OS, Versions of Software Required|If the issue occured in a certain version of software or OS matches with what the user has also used to reproduce with|required|
|Steps of Reproduction|Provides a paragraph or list of steps of how the issue is recreated|The steps should be commands of recreation, if it's UI based, record the actions that are needded to get to the result|required|
|Files & Commands|Documentation should be provided on how the issue was created. Some include contents of test files. Others can only be composed of command lines.|If commands and/or files are included, the recreation should match the posted issue exactly. If the report uses a file or script it did not paste, it passes when either (a) the issue text fully determines the contents (exact inputs, options, versions), or (b) the issue references something the reporter cannot supply (e.g. a private or long URL), the report states what it substituted and the feature of the substitute that matters, and the observed output matches the issue's output. Otherwise it fails.|required|
|Expected vs Actual|Provides the report of the expected issue and a report of the result the user actually got when reproducing|The actual result should match the expected issue. If it differs, the check still passes only if the report explicitly states the mismatch (e.g. "could not reproduce"), gives the observed output, and Environment Check, Steps of Reproduction, and Files & Commands all pass. A different result that is not acknowledged as different fails.|required|
|AI policy compliance|The contribution-policy line in the package's Repo facts section, plus the candidate's claim comment and repro report|Fail if the policy prohibits AI-assisted contributions. If the policy requires AI usage to be disclosed for issues or comments, the claim comment or repro report must contain an explicit statement about AI use (the tool and extent, or an explicit "no AI used"); the absence of any such statement fails, regardless of whether AI use is suspected. If the policy has no disclosure requirement for issues or comments, pass.|required|
|Claim comment|The candidate's claim comment|Pass only if the comment states a concrete next step specific to the issue (what they will read, trace, or test). Fail if it asks the maintainers to reserve the issue, promises a delivery deadline or guarantee. Saying "I'd like to work on this" is fine or something similar.|required|

## Verdict rule
For environment check, sometimes an OS version would not match with the original issue. In this case look for context whether the OS version would play a major role. Software versions must match, with one exception: a newer version of the same software than the issue names passes if the report states both versions and shows the bug still reproduces. An older version, or an unstated version, fails.
If the steps refer to a script or file that is not shown, treat the steps as clear when the issue text fully determines that script's contents, and unclear otherwise.

