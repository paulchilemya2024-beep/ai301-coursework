# Procedure: how this skill grades a PR package

## Read order

1. Read the issue (title, body, and thread) first. Note what behavior
   is expected and what behavior was reported as wrong.
2. Read `plan.md` next, in full, including its `## Deviations`
   section, before touching the diff. Note the stated diagnosis,
   scope, files-to-touch, approach, and test plan, plus anything the
   Deviations section says changed from the original plan. This has
   to come before the diff because several checks (Diff matches the
   plan, Fix targets the cause) can only be graded by comparing the
   diff against what the plan actually said -- reading the diff first
   risks grading it against an impression rather than the plan's
   actual words.
3. Read the diff (`git diff main...HEAD` in live mode, or the bundle's
   diff text in eval mode) in full, file by file.
4. Read the test evidence (`test_evidence.md` or the bundle's test
   evidence section) next, comparing it against the plan's test plan
   as you read.
5. Read the draft PR title and description (`pr_draft.md` or the
   bundle's description) last, alongside the repo's PR template and
   its stated contribution/AI-use policy.

## Evidence gathering

1. For "Diff matches the plan, no silent drift": list every file and
   behavior the diff changes. Compare each against the plan's scope,
   files-to-touch, and approach sections, and against anything named
   in Deviations. Record any diff change that appears in none of
   these as a quote.
2. For "Fix targets the cause, not the symptom": pull the plan's
   diagnosis (recorded in Read order step 2). Compare the diff's
   actual code change against it -- does the change act at the point
   the diagnosis names, or only where the symptom was visible? When
   the plan explicitly scoped the fix to narrow where a known-broken
   path is reachable, and named what stays deliberately unaddressed,
   treat that as acting on the cause within the plan's own stated
   boundary, not as masking the symptom.
3. For "Diff is clean and reviewable": re-read the full diff for debug
   statements, commented-out code, unrelated formatting changes, or
   edits outside the plan's named scope. Record any such lines found,
   with their file and line context.
4. For "Change is actually tested": identify which of the plan's test
   plan items is the PRIMARY repro (the behavior the issue is about)
   versus a SECONDARY control (confirming something else stays
   unchanged). For the primary repro, confirm the test evidence pastes
   actual before/after output, not just a claim. For a secondary
   control, a reported "unchanged" or "still passes" result is
   sufficient on its own -- do not require a second full transcript.
   Then check whether the package's own repo's test tooling was
   actually run and its result shown, identifying what that tooling is
   from the evidence itself. When the diff's change calls an existing
   function not shown in the diff (a shared formatter, logger, or
   error reporter), judge the test evidence's output for behavioral
   consistency with the change (the right error, the right exit code,
   the right data), not for literal traceability to the diff's visible
   lines. In live mode specifically, grading your own submission to
   Path Review, the expected checks are `make test-unit`, `make
   test-integration`, `make lint`, and `make typecheck`, including a
   "no tests ran" result from `make test-integration` pasted as-is;
   this specific command list applies only to Path Review submissions,
   never to an eval package from a different repo.
5. For "Description matches the diff": compare the draft description's
   Summary and Changes sections (from Read order step 5) against the
   diff's actual content (from Read order step 3). Record any
   described change absent from the diff, or any diff change absent
   from the description.
6. For "Standards and disclosure are met": pull the repo's PR template
   sections and its own stated AI-use/contribution policy from the
   package's repo-facts (eval mode) or the real repo's CONTRIBUTING.md
   / PR template (live mode). Compare each template section against
   the draft description to confirm it is filled in. Confirm the issue
   is correctly referenced. Check for an AI-assistance disclosure
   statement ONLY as a pass/fail factor when this specific package's
   own stated policy asks for or references AI-use disclosure -- when
   repo-facts says "no stated AI policy" (or equivalent), do not
   record a missing disclosure as a problem for this check. In live
   mode, grading your own submission to Path Review specifically, its
   stated policy does require disclosure, so apply that requirement
   there as Path Review's own stated ask, not as a universal rule
   applied to every package regardless of its own repo's policy.

## Check execution

1. Execute checks in the order they appear in the rubric's table, top
   to bottom.
2. Grade each check using only the evidence recorded for it in
   Evidence gathering -- do not re-read the whole package per check.
3. If the evidence needed for a check is genuinely absent from the
   package (not merely hard to find), grade that check `unclear` and
   record "not found in package" as the evidence line. Do not infer
   evidence that isn't there.
4. A check may be graded `pass` or `fail` only when the recorded
   evidence directly supports that grade per the rubric's pass
   condition -- if the evidence is ambiguous (could reasonably support
   either grade), grade it `unclear`.
5. If a check's required input genuinely does not exist yet for the
   mode being graded (for example, grading a draft description before
   a diff exists), grade it `unclear: not yet applicable` and exclude
   it from Verdict assembly rather than counting it as a fail.

## Verdict assembly

1. Apply the rubric's verdict rule: accept only if every applicable
   `required` check passed.
2. Any `fail` on an applicable required check means reject. Any
   `unclear` on an applicable required check also means reject, except
   a check explicitly marked not-yet-applicable, which is excluded
   rather than counted as a fail.
3. If the verdict is reject, quote the evidence line from the first
   required check (in table order) that failed or was unclear as the
   deciding reason in the output.
4. If the verdict is accept, quote the evidence line from "Diff
   matches the plan, no silent drift" as the deciding check in the
   output, since an accepted PR's integrity rests most on the diff
   actually being what the plan said it would be.
