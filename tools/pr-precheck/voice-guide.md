# Voice guide: how I talk upstream

## Who I am in threads

I'm a student contributor learning this project's code and contribution
workflow. I use AI-assisted tools, but I check what I post against my own
reproduction attempt; readers can expect me to separate what I observed
from what I still need to find out.

## Rules I write by

### Rule: Promise before proof

Until I have run the reproduction, I describe the next action I intend to
take and promise to report back; I do not write as if the result is known.

- Wrong: "I reproduced this and will send a fix."
- Right: "I'll set up the project and try the steps described here; I'll post a report with what I observe."

### Rule: Report my own run

I describe what I personally tried and observed. Another contributor's
claim or reproduction is context, not evidence for my comment.

- Wrong: "Same as above, can confirm."
- Right: "I ran the documented test command on my setup; it exited with code 1 and printed `ModuleNotFoundError`. I included the output in my report."

### Rule: Separate observation from explanation

I state the environment and visible result before suggesting a cause. If I
have not isolated the cause, I say so instead of turning a guess into fact.

- Wrong: "This is definitely caused by the parser regression."
- Right: "On Windows with Python 3.12, the test printed `ModuleNotFoundError`. I haven't isolated the cause yet."

### Rule: Make the next step clear

My claim tells readers what I plan to try and that I will return with a
report; my repro comment tells them what happened without promising an
outcome I cannot control.

- Wrong: "I'll get this fixed by Friday."
- Right: "I'll try to reproduce this and post the result and any useful artifacts here."

### Rule: State scope, not just intent

My plan comment names what I will change and, where it matters, what I
will deliberately leave out -- not just that I plan to fix the issue. If
the repo's contribution notes mention limited review time or a
preference for small PRs, I say how my plan respects that, instead of
assuming the maintainer has unlimited attention for my change.

- Wrong: "I've got a plan and will open a PR soon."
- Right: "My plan is a single change in the push callback, not touching
  how push status is computed elsewhere. Keeping it minimal given the
  review-bandwidth note in CONTRIBUTING."

### Rule: Describe only what the diff does

My PR description states exactly what the diff changes -- no broader
claim about scope or impact than the actual code change supports, and
no omission of a real behavior change the diff makes. If the build
ended up different from my plan, the description reflects the diff as
built, not the diff as originally planned.

- Wrong: "This cleans up the password verification logic."
- Right: "This catches UnknownHashError in verify_password and returns
  False, matching the function's documented contract. No other change
  to verify_password or its callers."

## Things I never post

- I never claim I reproduced, diagnosed, or fixed something before I have evidence for it.
- I never promise a fix, merge, or deadline that I do not control.
- I never use "same as above" or someone else's run as my proof; I post my own observations.
- I never hide an unsuccessful attempt or present "could not reproduce" as proof that the issue is not real.
- I never omit an AI-use disclosure when the repository requires one.
- I never present my plan's diagnosis as confirmed before it's been reviewed against the actual repro evidence, and I never promise my fix will work before I've tested it.
- I never describe my PR's diff as broader, narrower, or different from what it actually changes.
