# Rubric: is this pull request ready to submit?

<!--
THIS IS THE PART YOU WRITE (fourth week running; this is the rubric's
final form in the sandbox). Your frame in SKILL.md executes whatever
checks you define here, via your procedure.md. It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the diff read against the plan's scope, the test
     evidence read against the plan's test plan, the description read
     against the diff, the repo-facts block's template asks) or a
     location from your references/evidence-guide.md. "The PR" is not
     a source; "the diff's changed files read against the plan's
     stated boundary" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself
     (does the diff fall inside the plan plus its deviation notes? is
     the claimed evidence observable?), never the write-up's shape
     (how long the description is, how many commits there are).
     Structure-shaped checks are what make graders disagree with
     themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (submit) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. State the `unclear`
   treatment explicitly: the frame here is YOUR SKILL.md, so a rubric
   that stays silent is only covered if your frame's grading
   discipline says what happens (the contract's own default is that
   an unverifiable claim fails).

Cover what actually gets bad PRs submitted. The failure families the
lecture named ARE the harness's scoring categories, same names as the
eval README: silent drift (the diff silently does more or less than
the posted plan, or the description claims fidelity the diff
contradicts), not tested (the evidence proves nothing observable, or
the repo's own checks were never run), unreviewable (debris or
unrelated hunks bury the change), and standards wall (the repo's
stated template and disclosure asks are ignored). Your evidence
guide's four headings map onto these one to one (plan fidelity =
silent drift, test evidence = not tested, diff quality =
unreviewable, standards and comms = standards wall), and the category
floor is scored on exactly these names plus clear accept. A rubric
that ignores a category will fail the eval packages built around
that category. And remember the honest-outcome
rule, fourth week running: a PR that honestly discloses a shortfall
can be ready; a rubric that equates "less than everything" with
"hold" fails the set.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Issue and plan fidelity | Compare the issue requirements and plan.md, including Deviations, with the diff's changed files and behavior. | Every meaningful change addresses the issue and falls within the plan or an explicitly documented, justified deviation. No required planned behavior is silently missing. Honestly disclosed limitations do not automatically fail this check. | required |
| Description accuracy | Compare the PR title, summary, changes, and testing claims with the actual diff and test evidence. | Material claims are supported by the implementation and test evidence. The description does not falsely claim completed work, successful tests, or unchanged scope. Omissions or limitations are accurately disclosed. | required |
| Test evidence credibility | Compare the plan's test cases and reproduction steps with the provided before-and-after results and test outputs. | Evidence demonstrates an observable attempt to verify the change, identifies commands or reproduction steps, and reports actual outcomes. A disclosed failure does not automatically cause rejection if its impact is explained honestly. | required |
| Repository checks | Compare the repository's documented testing requirements with the actual results of unit tests, integration tests, lint, and type checking in the evidence. | Every applicable, runnable repository-required check has a recorded outcome. A check that cannot run because of a documented repository limitation may be marked unavailable with an accurate explanation. Merely explaining why a runnable check was skipped does not satisfy this condition. | required |
| Diff quality and reviewability | Inspect the changed files and hunks in the diff against the issue's scope and plan. | The diff contains a focused, understandable implementation without unrelated changes, debugging debris, accidental generated files, or unexplained modifications that obstruct review. | required |
| PR template compliance | Compare the PR description with the repository's PR template and requirements in the repo-facts or contribution-policy evidence. | All mandatory template requests are addressed with meaningful information, or an appropriate N/A explanation where permitted. The issue reference, changes, and test reporting satisfy applicable repository requirements. | required |
| AI-use disclosure | Compare the PR description and reviewer notes with the repository's stated AI-use disclosure requirements. | The PR includes the required AI-use disclosure, accurately describing how AI was used or stating that it was not used when appropriate. | required |
| Communication clarity | Review the PR title and description against the actual scope and evidence. | A reviewer can understand what changed, why it changed, and what was verified without misleading or contradictory wording. Concise descriptions are acceptable. | preferred |

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->

Grade every check as pass, fail, or unclear.

- Assign pass when specific evidence satisfies the check's pass condition.
- Assign fail when evidence demonstrates that the pass condition is not satisfied.
- Assign unclear when available evidence cannot establish whether the condition is satisfied.

Return `accept` only when every required check passes.

Return `reject` when any required check receives fail or unclear.

Preferred checks provide recommendations but never change the final verdict.

Do not reject a PR solely because a disclosed limitation remains, a test reports an expected repository limitation, or the description is concise. Apply the specific pass condition to determine whether the available evidence is truthful, sufficient, and reviewable.

Do not accept a PR containing undisclosed scope drift, unsupported testing claims, unrelated changes, or violations of mandatory repository standards.

The final verdict must be exactly `accept` or `reject`.



