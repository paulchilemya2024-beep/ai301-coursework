# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce
is a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Claim is a promise | The candidate claim comment, read against the issue title and body | The comment states what the student intends to do next (further investigation, a fuller report, or a specific follow-up step), and does not assert a root-cause diagnosis or a fix/solution as already complete or certain. Reporting that an initial reproduction attempt succeeded or failed — when paired with a stated next step — is a promise, not an overclaim; only a comment that asserts a diagnosis or working fix as done, or that makes no forward commitment at all, fails this check. Graded from the claim's own wording as posted, not from what the later repro report goes on to find. | required |
| Environment fits the target | The repro report's environment record, compared with the issue context and any relevant environment details in the repo-facts block | The recorded environment includes the versions or platform details that the issue or repo identifies as relevant. Any material difference from the issue's stated target is disclosed; an undisclosed difference that could explain the behavior fails. Do not require details that have no bearing on the reported behavior. | required |
| Steps support the stated outcome | The report's setup and reproduction actions, read with its environment record and artifacts | A contributor starting from the described initial state can follow the actions that matter to reach the reported test or observation without guessing a missing prerequisite or trigger. For a cannot-reproduce result, the report still makes clear what was set up and what was tried; headings, step counts, and template compliance alone do not decide this check. | required |
| Outcome matches the issue | The report's output, logs, screenshots, or other artifacts, read against the issue's stated actual and expected behavior | Pass if the artifacts show the issue's described behavior, rather than a merely related symptom. Also pass when the report explicitly says the issue was not reproduced and the artifacts show the result of the stated attempt without claiming confirmation. Fail when the artifacts show a different behavior but the report presents it as the issue. | required |
| Claims stay within evidence | The repro report's outcome and diagnosis statements, compared with its artifacts and the candidate claim | Every statement about what happened is consistent with the recorded run. A cannot-reproduce conclusion passes when the attempted run and its result are shown and the report does not imply the issue is disproven. A claimed reproduction, cause, or fix fails when the package's evidence does not support it. | required |
| Comments respect repo rules | The candidate claim and repro comments, compared with the issue thread, repo-facts contribution-policy summary, and applicable repo instructions or templates | The comments do not violate an applicable contribution rule, including any required AI-use disclosure. They describe this student's own work and do not rely on another contributor's reproduction as their proof or claim priority without evidence. Repo-required wording or fields are followed when applicable; absent a stated requirement, a particular format is not required. When the repo-facts contribution policy requires AI-use disclosure (naming the tool and extent) for the type of comment posted, the candidate comment must contain an explicit disclosure statement meeting that requirement. Under this course's AI-assisted workflow, the absence of any disclosure statement in a comment posted to a repo whose policy mandates one is itself a failure of this check — do not infer that non-disclosure is acceptable merely because the comment's wording doesn't reference AI. | required |

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->

Accept only when every applicable `required` check passes; any `fail` or `unclear` on an applicable required check means reject. Preferred checks, if added later, never change the verdict. In claim-only mode, grade the claim and applicable repo-rule evidence; mark report-dependent checks `unclear` with `not yet applicable: claim-only draft` and exclude those checks from the verdict. In full-package mode, every check applies, and `unclear` counts as reject.
