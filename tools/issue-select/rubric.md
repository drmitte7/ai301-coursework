# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| maintainer-alive | This issue's own thread (response + how old it is) and the 5-issue response-time sample (fastest response time in the sample) | Pass if this issue has a real response, or the sample's fastest response is under 60 days. Unclear if this issue has no response but was opened less than 14 days before the snapshot. Fail if no response here and the sample's fastest is 60+ days or all five got no response.  | required |
| repo-in-use | Repo-facts block: "last push to any branch" date | Pass if last push is within 90 days of the snapshot's captured date; fail otherwise | required |
| unclaimed | Check the repo-facts metadata and the full issue discussion for current assignees, open linked PRs, recent `/assign` or equivalent claim commands, explicit statements that someone is actively working on the issue, and repeated historical claim/unassign cycles or closed, unmerged PR attempts. | Pass if there is no current assignee and no open or otherwise clearly active PR or work claim for the issue. Fail if someone is currently assigned, an open PR exists, or the thread shows that someone is actively working on the issue with no indication that the work was closed, abandoned, or superseded. Also fail if the issue shows a repeated abandonment pattern: 3 or more separate claim-and-unassign/abandon cycles, or 2 or more closed, unmerged PR attempts associated with the issue. A single old abandoned claim or one closed PR does not by itself fail the check. | required |
| newcomer-scope | Issue description and discussion thread, checked for three concrete scope signals: a specific file or line named, clear expected-vs-actual behavior described, and a reproduction or suggested fix included. The good first issue label may be noted as context but does not affect the result. | Pass if 2 or more of the three signals are clearly present. Unclear if exactly 1 is present. Fail if none are present. | preferred |
| contribution-policy | Check the repository’s contribution policy captured in the repo-facts block, especially any section about generative AI, AI-assisted contributions, machine-generated code/documentation, or required human review. | Pass if the policy explicitly allows AI-assisted or generative-AI use when the contributor reviews, understands, tests, or takes responsibility for the work, or if no AI restriction is stated. Fail if the policy explicitly prohibits AI-generated code or documentation with no stated allowance for assistive or reviewed AI use. Unclear if the policy discourages or restricts AI only for certain contribution types, or its wording does not clearly establish whether the intended AI-assisted workflow is permitted. | required |

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict, they
rank accepted issues; unclear counts as fail." -->

Accept if none of the required checks fail. For required checks, unclear is non-blocking and counts the same as pass for the final accept/reject decision. Reject if any required check is a clear fail. The newcomer-scope check is preferred, not required, so its result does not determine the verdict.
