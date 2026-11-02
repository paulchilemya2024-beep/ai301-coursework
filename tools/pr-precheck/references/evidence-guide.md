# Evidence guide: where evidence lives in a PR package

## Plan fidelity (harness category: silent-drift)

- **Where it lives:** in a bundle, compare the "Plan context" block's
  Plan paragraph (its stated scope, files-to-touch, and boundaries)
  against the "### Diff" section and the "### Description" section.
  In live mode, compare `plan.md`'s scope/files-to-touch/approach
  sections and its `## Deviations` notes against `git diff
  main...HEAD` and `pr_draft.md`'s Summary/Changes sections.
- **What good looks like:** every changed file and every behavior
  change in the diff falls inside the plan's stated boundary, or is
  explicitly named in a Deviations note with a reason. The
  description claims exactly what the diff delivers -- no broader, no
  narrower. A diagnosis-to-fix mismatch also lives here: the diff's
  actual code change should act on the plan's stated root cause, not
  merely mask where the symptom was visible.

## Test evidence (harness category: not-tested)

- **Where it lives:** in a bundle, the "### Test evidence" section,
  compared against the "Plan context" block's Test plan sentence. In
  live mode, `test_evidence.md`, compared against `plan.md`'s test
  plan.
- **What good looks like:** the plan's repro is re-run with concrete
  before-and-after observations, shown as output or a precise account
  of the action and observed result; a raw transcript is not required.
  Each planned control has an observed outcome or is covered by a
  specifically identified automated test. A named control explicitly
  reported unchanged counts when the plan states its expected baseline;
  an unqualified "controls pass" does not. The package's own test
  tooling is identified from its evidence (for example, pytest, cargo
  test, or a named functional suite), and its result is stated; counts
  are useful when provided, but full logs are not required. A bare
  "tested" or "all tests pass" claim without a concrete repro outcome
  and identifiable test command or suite is insufficient. A reported
  failure still counts as evidence when shown honestly. Before calling
  an output inconsistent with the diff, trace the relevant value or
  error through the full changed path, including wrappers and
  propagated underlying errors. Missing outcomes or a contradiction
  that remains after this trace fail this family.
  In live mode specifically, grading your own Path Review submission,
  the expected checks are `make test-unit`, `make test-integration`,
  `make lint`, and `make typecheck`, with a "no tests ran" result from
  `make test-integration` pasted as-is -- this specific list is Path
  Review's own ask and does not apply to eval packages from other
  repos.

## Diff quality (harness category: unreviewable)

- **Where it lives:** in a bundle, the "### Diff" section read on its
  own, as a reviewer would read it. In live mode, the full `git diff
  main...HEAD` output.
- **What good looks like:** the fix is visible and nothing unrelated
  rides along. Debris tells to watch for: leftover debug print
  statements, dead or commented-out code, formatting-only churn
  across unrelated lines, and drive-by edits to files the plan never
  named. A diff can fail this family even when its core fix is
  entirely correct, if a reviewer would have to wade through unrelated
  noise to find it.

## Standards and comms (harness category: standards-wall)

- **Where it lives:** in a bundle, the "Repo facts" block's "pull
  requests" (template/contribution asks) and "contribution policy"
  lines, compared against the "### Description" section. In live
  mode, the repo's actual `.github/PULL_REQUEST_TEMPLATE.md` and
  `docs/CONTRIBUTING.md` (or stated AI-use policy), compared against
  `pr_draft.md`.
- **What good looks like:** every section the repo's own template asks
  for is filled with real content, and the issue is correctly
  referenced. AI-assistance disclosure only counts against a package
  when THAT package's own stated policy asks for or references it --
  a repo whose repo-facts says "no stated AI policy" should not fail
  this family merely for a description that doesn't mention AI. A
  repo that does state a disclosure requirement, and gets a
  description with no disclosure, fails here. In live mode, grading
  your own submission to Path Review, its own stated policy does
  require disclosure, so that requirement applies there as Path
  Review's own ask, not as a rule carried over onto every package
  regardless of what that package's own repo actually requires.
