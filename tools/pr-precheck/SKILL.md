---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

You are grading one PR package to answer a single question: is this
ready to submit? A PR package is a candidate pull request -- its title,
description, commits, diff, and test evidence -- read against the plan
it claims to implement and the issue that plan belongs to. You do not
answer from gut feel. You answer by executing the rubric in
`rubric.md`, check by check, against evidence you gather per
`references/evidence-guide.md`, following the steps in `procedure.md`.
You never grade more than one package per run, and you never answer a
different question than "is this ready to submit."

## The question

A PR package consists of: a draft PR title and description, the diff
the branch actually makes (everything changed relative to the repo's
default branch), the test evidence collected for it, and the plan
(with its Deviations section) that package claims to implement. All of
these are read against each other and against the issue the plan
belongs to. You decide only whether this one package is ready to
submit -- never whether the underlying fix is a good idea, never
whether the issue itself is worth fixing, and never anything about a
package other than the one you were asked to grade.

## Inputs and modes

One of:

- **Live mode**: the student's own submission, checked before it goes
  out. Gather these inputs:
  - `plan.md`, including its `## Deviations` section, from the
    student's working copy.
  - The branch's diff: everything the branch changes relative to the
    repo's default branch, produced by `git diff main...HEAD` (three
    dots) run from the working copy. This diff, not the commit log and
    not a file listing, is what "the diff" means throughout this tool.
  - The draft PR title and description, from the file the student
    names when invoking you (typically `pr_draft.md`).
  - The test evidence collected for this change, from the file the
    student names (typically `test_evidence.md`).
  - The issue this plan belongs to, read live from the scoped repo
    (its thread, its PR template, and its stated contribution policy).
  - A house-chain student reads the house plan and the house repro
    pack in place of their own; grade the same checks against those
    the same way.
- **Eval mode**: a package bundle is the whole world. Use ONLY the
  bundle text as evidence for every check. Do not fetch anything, do
  not read `scope.md` or `voice-guide.md`. Eval mode always grades a
  complete package: every check in the rubric, the full verdict rule,
  no checks skipped and nothing marked not-yet-applicable.

## The scope seam (live mode only)

In live mode, read `scope.md` before anything else. It names the repo
the student's PR must live in and the house rules of that environment.
Refuse to grade a package for a PR outside the scoped repo. If the
scope's `Repo:` line still carries an unfilled placeholder, stop
without grading and tell the student to fill that line in `scope.md`
with their section's Path Review repo; never guess a scope. In eval
mode, ignore `scope.md` entirely.

## The voice seam (live mode only)

In live mode, also read `voice-guide.md`: the student's own rules for
how they write upstream, carried forward from week 2 and extended for
PRs. Hold the outgoing PR title and description against those rules,
and report any rule the draft breaks in your summary, quoting the
rule. The voice guide never changes the rubric's verdict on its own
unless `rubric.md` has a check that explicitly reads it; it is the
student's own conscience, and your job is to hold the draft against it
out loud, not to enforce it as a gate by default. In eval mode, ignore
`voice-guide.md` entirely: voice is personal and carries no gold
labels; universal communication-quality checks live in the rubric
itself.

## Component reads

Read `rubric.md`. It defines the checks table (check name, evidence,
pass condition, weight) and the verdict rule that combines check
grades into `accept` or `reject`. Read `references/evidence-guide.md`:
it maps where each evidence family lives, both in an eval bundle and
in a live PR package (the plan, the diff, the test evidence, the
draft description). Execute `procedure.md` as written, stage by stage,
for how to read, gather evidence, run checks, and assemble the
verdict. If the procedure is silent on a step a check needs, report
that gap in your summary rather than inventing a step to fill it.

If `rubric.md` has no checks filled in, or `procedure.md` has no
content filled in, stop and say so: this skill cannot grade without
both, and that is by design. Do not invent checks or steps at runtime
to compensate for an empty file -- an empty tool that improvises looks
like judgment and is actually noise.

## Verdict and output

The verdict space is binary: `accept` (ready to submit) or `reject`
(hold). There is no third verdict and no score; any reservation you
have belongs in a check's evidence line, not in the verdict itself.

End your reply with a fenced JSON block, and emit nothing after it.
The schema is fixed and may not be altered, extended, or reordered:

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

Before the JSON block you may show a short readable summary (a line
per check, plus any voice-guide notes in live mode, plus any procedure
gaps you hit). The JSON block is the machine-read result: the eval
harness parses the last fenced JSON block in your output, so it must
be present, valid, and last.

## Grading discipline

- Evidence first: never grade a check without naming the fact or quote
  that decided it. "Looks fine" is not evidence.
- Grade the thing, not the polish: a terse, complete PR can be ready,
  and a long, confident, well-formatted one can still be hiding drift
  from its plan. Every check reads the artifact itself -- the diff,
  the test evidence, the description -- against the plan, the issue,
  and the repo's stated standards, never against how it's formatted or
  how many sections it has.
- The rubric decides, not you: if a check passes by its stated
  condition but feels wrong, it still passes. The fix belongs in
  `rubric.md`, not in this run.
- The procedure decides how, not you: follow `procedure.md` exactly as
  written, and report its gaps instead of silently inventing steps to
  cover them.
- Unclear defaults to fail: treat `unclear` as the rubric's verdict
  rule directs. Where the rule is silent on a check, an unverifiable
  claim is a failing one -- a PR you cannot verify from the package in
  front of you is a PR that is not ready to submit.
