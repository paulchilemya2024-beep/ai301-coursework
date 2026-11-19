# Toolkit Portfolio

Student: Paul Chilemya

## Featured Tools

I chose pr-precheck, plan-check, and issue-scout because each one forced a real rewrite after a real miscalibration, and because pr-precheck's arc ends in a concrete, external result: a pull request actually open on the shared repo.

### pr-precheck

What it is, and the judgment hole I wrote: pr-precheck grades a full PR package (diff, test evidence, description) against the plan it claims to implement, deciding accept/reject. I wrote both the rubric and, for the first time this term, the SKILL.md frame itself: the read order, the scope and voice seams, and the six checks covering silent drift, cause-vs-symptom, diff cleanliness, testing, description accuracy, and standards/disclosure.

How it evolved, dated: On 2026-10-26 my first full eval scored 13/20, with every "clear-accept" package in the eval set wrongly rejected (0/7). The "Change is actually tested" check had baked in Path Review's specific command names (make test-unit, etc.) as the only acceptable evidence, and "Standards and disclosure" assumed every repo requires AI disclosure the way our course does. I rewrote both checks to judge each package against its own repo's actual tooling and actual stated policy instead of one fixed standard. A follow-up canary (2026-10-26) surfaced a narrower bug: the testing check demanded a full repeated transcript for secondary controls and literal diff-traceability for output from existing, unshown functions. I loosened it to accept "unchanged" reports for controls and judge shared-function output by behavioral consistency instead. The confirming full run on 2026-10-26 scored 20/20, every category matched. Later, grading my own real draft PR in live mode, the tool correctly rejected it once more for an unticked "CI green" checkbox that the course's own instructions say must stay unticked before a PR is opened — a live-mode-only case none of the 20 eval packages tested. I added a narrow carve-out for that one template item.

Evidence: the live-mode precheck's own JSON verdict on my real draft, after the fix: `"name": "Standards and disclosure are met", "grade": "pass", "evidence": "The draft fills the PR template, references issue #72, includes the AI-assistance disclosure, uses the required fix/72-<slug> branch name, and leaves the not-yet-green CI checkbox honestly unchecked as the rubric requires for a pre-PR draft."` That accept led directly to a real, open pull request: https://github.com/codepath/pathreview-ai301-fa26-s3/pull/271.

### plan-check

What it is, and the judgment hole I wrote: plan-check grades a fix plan (diagnosis, scope, test plan, risks) and a draft plan comment before either goes out, deciding whether the plan is ready to post and build from. My rubric covers seven checks, including whether the diagnosis is actually supported by repro evidence and whether stated risks are genuinely unknown rather than dressed-up certainty.

How it evolved, dated: My first full eval (2026-10-18) scored 16/20, with all four misses in the "clear-accept" category, every one failing "Unknowns are stated as unknowns." Reading the actual failing packages, I found the check was treating any confidently-worded claim as unjustified overconfidence, even when that claim was directly backed by cited repro evidence or multiple control comparisons. I rewrote the check to explicitly say confidence earned from cited evidence is not overconfidence, and only flag a claim that goes beyond what the evidence actually shows. A confirming full run the same day scored 19/20, clearing the 18/20 bar with every category matched.

Evidence: the check's rewritten pass condition, as uploaded: "A claim directly supported by the quoted repro evidence, by multiple corroborating control observations, or by a conclusion the issue thread already settled is NOT an unknown and needs no hedging, however confidently it is stated — confidence earned from cited evidence is not overconfidence."

### issue-scout

What it is, and the judgment hole I wrote: issue-scout extends my Unit 1 issue-select rubric with automated search: a fit profile, gh search issues queries tied to that profile, and ranking filters, so it can find and grade candidate issues on its own instead of me browsing manually.

How it evolved, dated: My first manual test queries (2026-11-11) returned mostly noise — beginner-practice "issue farm" repos stacked with generic labels like leetcode and 5-minutes, and templated auto-generated issues. I added an "api" keyword tied to my fit profile and a ranking filter dropping any issue from a repo with excessive generic labels. The re-tested query then surfaced genuinely relevant candidates (a Proxmox API client missing tests, a FastAPI response-model typing fix). My first real scan that same day still accepted an issue (optora#103) whose own timeline referenced a commit saying "closes #103" — my "Nobody already on it" check only looked at assignees and linked PRs, with no check for closing-keyword commit references. I fixed the check to flag that signal too.

Evidence: scan-notes.md, 2026-11-11: "First scan surfaced optora#103 as an accept, but a referenced commit message said 'closes #103' -- the rubric's 'Nobody already on it' check only looked at assignees and linked PRs, with no check for a closing-keyword reference in recent commit history. Fixed by adding commit-message checking to that check's evidence and pass condition."

## Inventory

- issue-select: Unit 1's original rubric (maintainer alive, repo in use, newcomer scope, nobody already on it). Still the base every later rubric was adapted from; carried forward unchanged into issue-scout.
- repro-check: Grades a claim comment and repro report for honesty and evidence. Used to post my claim and repro comments on Path Review issue #72, including a disclosure-wall check I had to add after it missed a repo requiring AI-use disclosure.

## The Arc

Beat 1
Date: 2026-09
Friction: My first issue-select rubric scored below the 18/20 bar because checks like "Scope fits a newcomer" were reading short, informal issue bodies as automatically too vague, when short isn't the same as unscoped.
Change: Rewrote the scope check's pass condition to only fail on specific disqualifying signals (umbrella issues, unresolved design disputes, failed prior PRs), not on brevity itself.
Result: Reached 19/20 agreement with every category matched, and used the rubric to pick Path Review issue #72.

Beat 2
Date: 2026-09
Friction: My repro-check rubric missed a disclosure-wall package in eval: a repo requiring AI-use disclosure, paired with a non-disclosing comment, that my rubric passed anyway.
Change: Added an explicit rule that silence on a mandatory disclosure requirement is itself a failure, not a neutral case.
Result: Reached
