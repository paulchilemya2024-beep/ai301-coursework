# Rubric: is this a good first issue?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Maintainer alive | "last 5 default-branch commits" and "maintainer first-response sample" under Repo facts | At least 1 of the last 5 default-branch commits is dated within 90 days of the capture date, OR the maintainer first-response sample shows a reply within 30 days | required |
| Repo not archived | "archived:" on the repo line | The archived flag is false or absent | required |
| Repo in active use | "latest release" and "last push to any branch" under Repo facts | The latest release is within 12 months of the capture date, OR the last push to any branch is within 90 days of the capture date | required |
| Scope fits a newcomer | Issue body, comment thread, and "linked PRs:" history under Repo facts | Fails only if: (a) the issue is explicitly a tracking/umbrella issue meant to be split into separate sub-issues, (b) the thread shows an unresolved design disagreement with no maintainer resolution, (c) a maintainer states the fix requires touching core internals beyond newcomer scope, or (d) 2+ closed/unmerged linked PRs previously attempted and failed to resolve it. A short body, informal or absent repro steps, or one bug listing several possible causes/fix angles does NOT by itself fail this check. | required |
| Nobody already on it | "this issue: assignees:" and "linked PRs:" under Repo facts; comment thread claim comments with dates | Assignees is empty, no linked PR is currently open, AND any claim comment in the thread is either followed by a sign it lapsed (an unassignment notice, a closed/abandoned linked PR, or 60+ days of no follow-up before the capture date) — only an unaddressed claim within 60 days of the capture date counts as active | required |
| Contribution policy allows AI-assisted work | "contribution policy" line under Repo facts | The policy contains no outright ban on AI-generated or AI-assisted contributions (stated conditions, or no policy at all, both pass) | required |
| Has clear acceptance criteria | Issue body | States expected vs. actual behavior, or gives an acceptance-criteria checklist, or clearly describes the feature to add | preferred |
| Maintainer engaged on this thread | Comments section, `author_association` per comment | At least one comment on this specific issue has `author_association` of OWNER, MEMBER, or COLLABORATOR | preferred |
| Freshly labeled good-first-issue | Label event timeline in the thread | The "good first issue" (or equivalent) label was added within the last 90 days | preferred |

## Verdict rule

Accept only if every `required` check passes. Any `required` check that fails or is `unclear` causes a reject — `unclear` is treated the same as an explicit fail, never as a pass. `preferred` checks never affect accept/reject; among accepted issues, rank by number of `preferred` checks passed (more passes = higher rank), with ties broken by recency of the "maintainer first-response sample."