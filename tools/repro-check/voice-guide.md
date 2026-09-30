# Voice guide: how I talk upstream

<!--
THIS IS THE PART YOU WRITE (new this week). Live mode reads this file
before any comment of yours goes out the door; eval mode ignores it
entirely, because your voice is yours and carries no gold labels.

This is not etiquette. "Be polite and concise" is advice for everyone
and therefore rules for no one. Write rules YOU need, in your own
words, each one concrete enough that the skill can hold a draft
against it and say which rule it breaks.

Three sections. Fill all three.
-->

## Who I am in threads

<!-- 2-3 lines. Who is talking when you comment on an issue: your
experience level stated plainly, what you are doing in this repo, what
readers can expect from you. This is the register your rules protect. -->

I'm a student contributor learning this project's code and contribution
workflow. I use AI-assisted tools, but I check what I post against my own
reproduction attempt; readers can expect me to separate what I observed
from what I still need to find out.

## Rules I write by

<!-- 3-5 rules, drafted from the lecture's slide-12 moment. Each rule
needs a wrong/right pair from your own hand: one line you might
actually have written that breaks the rule, and the line you would
post instead. The pair is what makes a rule executable; a rule without
one is a wish.

Format each rule like this:

### Rule: <short name>

<The rule, one or two sentences.>

- Wrong: "<a line that breaks it>"
- Right: "<the line to post instead>"
-->

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

## Things I never post

<!-- A short list. Promises you cannot keep, tones you refuse,
shortcuts you know you reach for when tired. The skill quotes this
list back at you when a draft crosses it. -->

- I never claim I reproduced, diagnosed, or fixed something before I have evidence for it.
- I never promise a fix, merge, or deadline that I do not control.
- I never use “same as above” or someone else's run as my proof; I post my own observations.
- I never hide an unsuccessful attempt or present “could not reproduce” as proof that the issue is not real.
- I never omit an AI-use disclosure when the repository requires one.
