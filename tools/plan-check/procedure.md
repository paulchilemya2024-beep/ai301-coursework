# Procedure: how this skill grades a plan package

## Read order

1. Read the issue (title, body, and thread highlights) first. Note
   what behavior is expected and what behavior was reported as wrong.
2. Read the repro evidence next (the repro comment or repro pack),
   before touching the plan. Note exactly what was observed: the
   actual output, error, or behavior, and the steps that produced it.
   This has to come before the plan because several checks (Diagnosis
   matches the evidence, Fix targets the cause, Test plan reuses the
   repro) can only be graded by comparing the plan against what the
   repro evidence actually showed — reading the plan first risks
   grading it against its own claims instead of the real evidence.
3. Read the plan (plan.md or the plan section of the package) in full,
   section by section, in the order it's written: diagnosis, scope,
   files to touch, approach, test plan, risks/unknowns.
4. Read the draft plan comment (comment.md) last, alongside the
   issue's thread highlights and the repo-facts contribution-policy
   summary.

## Evidence gathering

1. For "Diagnosis matches the evidence": pull the plan's stated root
   cause from its diagnosis section. Pull the actual observed
   behavior from the repro evidence gathered in Read order step 2.
   Record both as short quotes.
2. For "Scope is bounded": pull the plan's scope statement and its
   files-to-touch list. Record whether a boundary (what will NOT
   change) is explicitly stated, and list the named files/functions.
3. For "Fix targets the cause, not the symptom": pull the plan's
   approach section. Compare it against the diagnosis recorded in
   step 1 — does the approach act on the named cause, or does it only
   change behavior at the point the symptom appears?
4. For "A stranger could start executing it": re-read the approach and
   files-to-touch list as a set of instructions, not an explanation.
   Record whether a first concrete action is identifiable without
   outside context.
5. For "Test plan is observable and reuses the repro": pull the plan's
   test plan section and the repro comment's steps from Read order
   step 2. Record whether the same steps are reused, and whether the
   stated expected result is a concrete, checkable observation (not a
   general claim like "works now").
6. For "Unknowns are stated as unknowns": read the risks/unknowns
   section first. Then check each of the plan's other confident
   claims (diagnosis, approach) against whether it's backed by the
   repro evidence, a control comparison, or a thread conclusion
   already recorded in steps 1-3. Only record a claim as a problem if
   it goes beyond what that cited evidence actually established — do
   NOT flag a claim merely for being stated with confidence when it is
   properly grounded.
7. For "Comment respects the thread and repo conventions": pull the
   draft plan comment's text, the issue thread highlights, and the
   repo-facts contribution-policy line (especially any AI-use
   disclosure requirement). Record whether the comment acknowledges
   relevant thread context and whether disclosure is present when
   required.

## Check execution

1. Execute checks in the order they appear in the rubric's table,
   top to bottom.
2. Grade each check using only the evidence recorded for it in
   Evidence gathering — do not re-read the whole package per check.
3. If the evidence needed for a check is genuinely absent from the
   package (not merely hard to find), grade that check `unclear` and
   record "not found in package" as the evidence line. Do not infer
   evidence that isn't there.
4. A check may be graded `pass` or `fail` only when the recorded
   evidence directly supports that grade per the rubric's pass
   condition — if the evidence is ambiguous (could reasonably support
   either grade), grade it `unclear`.
5. In plan-only mode (before comment.md exists), skip "Comment
   respects the thread and repo conventions" and grade it `unclear:
   not yet applicable: plan-only draft`; exclude it from Verdict
   assembly.

## Verdict assembly

1. Apply the rubric's verdict rule: accept only if every applicable
   `required` check passed.
2. Any `fail` on an applicable required check means reject. Any
   `unclear` on an applicable required check also means reject, except
   a check explicitly marked not-yet-applicable in plan-only mode,
   which is excluded rather than counted as a fail.
3. If the verdict is reject, quote the evidence line from the first
   required check (in table order) that failed or was unclear as the
   deciding reason in the output.
4. If the verdict is accept, quote the evidence line from "Diagnosis
   matches the evidence" as the deciding check in the output, since an
   accepted plan's validity rests most on the diagnosis being correct.