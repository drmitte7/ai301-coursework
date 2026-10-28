# Rubric: is this plan ready to post and build from?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here (via your procedure.md). It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the plan's scope statement, the test plan read against
     the repro evidence's steps, the plan comment read against the
     thread highlights, the repo-facts block) or a location from your
     references/evidence-guide.md. "The plan" is not a source; "the
     plan's stated cause read against what the repro evidence shows"
     is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (is
     this one bounded change? could a stranger start executing it?),
     never the write-up's shape (how many sections it has, how long it
     is, whether it uses headings). Structure-shaped checks are what
     make graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad plans posted. The lecture named the
failure families: the diagnosis ignores or contradicts the reproduced
evidence, the change is unbounded (scope creep), the plan targets the
symptom while the evidence points at the cause, a stranger could not
start executing it, the test plan proves nothing observable, the
unknowns are dressed up as certainty, and the comment ignores what the
thread or the repo's stated conventions ask. A rubric that ignores a
family will fail eval packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| diagnosis-supported | The plan's stated diagnosis read against the repro evidence, observed behavior, issue context, and any quoted failure output. | Pass if the diagnosis is consistent with the reproduced evidence and provides a plausible explanation for the observed behavior without contradicting known facts. The diagnosis may remain a working hypothesis when the plan identifies how implementation-time tracing or testing will confirm it. Fail if the diagnosis contradicts the evidence, ignores a materially better-supported cause, or states an unsupported mechanism as settled fact without any plan to verify it. | required |
| cause-targeted | The proposed implementation approach read against the diagnosis and repro evidence. | Pass if the proposed change addresses the likely cause identified by the evidence rather than only masking the visible symptom. Fail if the plan changes an unrelated surface or only suppresses the symptom without addressing the evidence-supported cause. | required |
| scope-bounded | The plan's scope, files to change, implementation approach, and explicit out-of-scope statements. | Pass if the plan describes one bounded change with clear limits and does not include unrelated refactors, cleanup, or feature work. Fail if the change is open-ended, unnecessarily broad, or includes work not needed to resolve the reproduced issue. | required |
| executable | The files or areas to inspect/change, implementation steps, and any repo facts needed to begin the work. | Pass if a stranger familiar with the repository could begin executing the plan without inventing the intended behavior or solution direction. Exact function names, line numbers, or every implementation detail do not need to be known in advance when the plan identifies the relevant area and explains how remaining details will be located during implementation. Fail if key targets or behaviorally important steps are missing enough that the builder would have to invent the approach. | required |
| test-observable | The test plan read against the repro steps and expected post-fix behavior. | Pass if the test plan re-runs the relevant reproduction or equivalent real-code path and states an observable result that would distinguish the fixed behavior from the reproduced failure. Fail if the tests only say to "verify" or "run tests" without showing what behavior should change. | required |
| uncertainty-honest | The diagnosis, risks, unknowns, assumptions, limitations, and conditional language in the plan. | Pass if material uncertainty is represented honestly and the plan does not rely on an unsupported assumption as if it were already proven. A working diagnosis may be stated confidently when it fits the evidence, provided the plan includes tracing, testing, or inspection that can confirm or revise the uncertain mechanism before the implementation depends on it. A plan does not need to invent risks or unknowns when none are apparent. Fail if it hides a material uncertainty, overstates what the evidence establishes, or relies on an unverified assumption that could materially change the fix without acknowledging or checking it. | required |
| conventions-aligned | The draft plan comment read against the issue thread, repo-facts, scope rules, and repository-stated conventions. | Pass if the comment and plan respect relevant thread context and repository conventions, including ownership, branch, scope, or required coordination rules. Fail if they ignore a stated convention or contradict relevant issue-thread instructions. | required |

## Verdict rule

Accept only if every required check passes.

A required check graded `unclear` counts as a failure because the plan is not ready to post or build from when a behaviorally important judgment cannot be made from the available evidence.

Preferred checks, if added later, may provide feedback but never change the final verdict.

If any required check fails or is unclear, reject the package.

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->
