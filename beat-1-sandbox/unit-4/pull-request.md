# Unit 4 — Test and Submit

## Your pull request

**Pull request**

https://github.com/codepath/pathreview-ai301-fa26-s3/pull/271

**Branch**

`fix/72-malformed-password-hash`

## Eval iterations

**Run history**

1. Initial full evaluation with rubric v1: **13/20**. The `clear-accept` category floor was unmet at 0/7.
2. Eleven-package diagnostic after the initial full run and before the first rubric revisions: **5/11**.
3. Three-package diagnostic run (`pkg-05`, `pkg-08`, `pkg-11`): **0/3**.
4. Thirteen-package canary after the first evidence-rule clarification: **10/13**. `pkg-13`, `pkg-16`, and `pkg-19` still disagreed; all were expected accepts rejected on “Change is actually tested.”
5. A subsequent thirteen-package attempt hit Claude's individual spend limit; all items errored, so it produced no scored agreement result.
6. Five-package canary (`pkg-13`, `pkg-16`, `pkg-19`, `pkg-01`, `pkg-04`): **5/5**.
7. Final full evaluation: **20/20**. The committed `eval-run.txt` records `agreement: 20/20 scored items (bar: 18/20: PASS)` and every category matched.

After that final evaluation, I added a live-mode-only carve-out for an honestly unchecked CI-green box on a pre-PR draft. It does not change eval-mode behavior or the saved 20/20 result. The uploaded rubric includes this refinement.

**Package analysis**

`pkg-16` (gold: `accept`) was rejected by the intermediate rubric on “Change is actually tested.” The evidence showed a failing image-load repro returning an error and exit code 1, but the grader judged the formatted error inconsistent with the diff because the diff called the existing `exit.Error(...)` reporter, whose formatting was not shown in the diff. I revised the check to assess whether output from existing shared functions is behaviorally consistent with the change—such as the right error and exit code—instead of requiring every output character to be derivable from changed lines. The final evaluation accepted `pkg-16`, matching gold.

**Check rationale**

Exact quote from the uploaded `rubric.md`:

> A secondary control case the plan's test plan also names (e.g. confirming an unrelated code path is unchanged) satisfies this check when reported as unchanged/passing, even without a full repeated transcript, PROVIDED the primary repro's before/after is fully shown -- do not fail this check merely because a control's identical-to-before result wasn't separately re-pasted.

I added this criterion after the canary showed that requiring a full repeated transcript for every control rejected packages whose primary repro had complete before/after evidence and whose named controls were reported unchanged. It preserves the requirement for concrete primary repro evidence while avoiding a redundant-transcript requirement for secondary controls.

**Trade-offs**

The change from requiring pasted raw output to accepting concrete action-to-result observations risks accepting plausible but fabricated test reports; the grader sees package text rather than executing every package's code. I kept safeguards: the evidence must identify the primary repro and its before/after outcome, name the repository's test command or suite and its result, and remain behaviorally consistent with the diff. I reran canaries after revising the criterion: the 5-package canary scored 5/5, including the three previously missed accepts and two correctly rejected cases. The final full run scored 20/20, with all category floors met.
