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

In an eval bundle, look in the candidate repro report for its environment
record, then compare it with the issue context and any environment or
version details in the repo-facts block. In live mode, use the student's
draft repro report and the issue body/comments; check the repository's
setup documentation when the report depends on a repo-specific runtime
or configuration. A useful record names the environment dimensions the
issue says may matter (for example, operating system, runtime, or
dependency versions). Differences from the issue's target are acceptable
when they are made explicit; a missing irrelevant version is not a
failure by itself.

## Steps

<!-- Where the reproduction steps live, and what makes them followable
by a stranger, starting state to trigger. -->

In an eval bundle, find the candidate repro report's setup and actions;
read them alongside its environment record and artifacts. In live mode,
read those same parts of the draft report and consult the repo's own
installation or test instructions for prerequisites. Look for enough
information to understand the starting state, required setup, trigger,
and observation—not a prescribed number of numbered steps. For a
cannot-reproduce result, the attempted setup and trigger still need to
be identifiable so the reader can understand what was tested.

## Behavior shown

<!-- Where the artifacts live (output excerpts, logs, screenshots),
and what it means for an artifact to show the issue's behavior rather
than an adjacent one. -->

In an eval bundle, inspect the report's quoted command output, logs,
screenshots, or other artifacts and compare them with the issue context's
expected and actual behavior. In live mode, inspect the artifacts included
or quoted in the draft report; if a linked artifact is necessary to assess
the result, open it. Good evidence lets a reader identify the same
observable symptom the issue describes, not merely a nearby error or a
successful command. If the student says they could not reproduce it, the
evidence should show the result of the attempted run and should not be
described as confirmation of the bug.

## Honesty

<!-- Where claims and their backing meet: how to tell a report that
says exactly what happened (including an honest cannot-reproduce) from
one that claims more than its evidence shows. -->

In an eval bundle, compare each result or diagnosis in the candidate
report with the report's artifacts and the issue context; compare the
claim comment with what the report later says was done. In live mode,
make the same comparison within the student's drafts and any linked
artifacts. A report is honest when its conclusion is no stronger than
its evidence: a documented attempt that did not show the bug can support
“I could not reproduce this,” but cannot establish that the bug does not
exist. Treat a root-cause or fix statement as a claim that needs its own
support, not as a fact just because it appears in the report.

## Comms

<!-- Where the words meet the repo: the claim comment against the
issue, the comments against the repo's stated templates and
contribution policy (including AI-use disclosure requirements), and
what specific-and-honest looks like next to boilerplate. -->

In an eval bundle, read the candidate claim and repro comments against
the issue context and the contribution-policy summary in repo facts; use
any quoted repo instructions or templates there as well. In live mode,
read the proposed comments in context on the issue thread, then check
`CONTRIBUTING.md`, linked contributor docs, AI-use policy files, and
issue/PR templates in the repository. Follow explicit requirements such
as disclosure or required fields. The claim should say what the student
will try and promise a report before the work is done; the repro comment
should report that student's own run and evidence. Boilerplate that
claims an unobserved result, borrows someone else's proof, or asserts
priority without support is not an acceptable substitute for specific
accounting. Do not invent a format requirement when the repo states
none.
