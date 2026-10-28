# Procedure: how this skill grades a plan package

<!--
THIS IS THE PART YOU WRITE, and it is a new kind of part. Weeks 1 and
2, SKILL.md carried a numbered workflow and you only wrote judgment
files. This week the workflow is gone from the frame: SKILL.md says
"execute procedure.md", and these are the operating steps you author.
The machinery is in your hands now.

Your operator swap is the design brief. When your executor stalled
because your rubric said WHAT to decide but not HOW to find the
evidence, that was a procedure gap. This file is where those gaps get
closed: a complete procedure lets someone who has never seen a plan
package before (a groupmate, or the skill itself) grade one exactly the
way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
repro evidence before the plan, and note what behavior it pins down"
is a step; "understand the context" is a wish.
-->

## Read order

1. Read the issue summary and thread context first. Record the reported problem, any explicit constraints, and any instructions or conventions that affect the proposed work.
2. Read the reproduction evidence next. Record the observed behavior, failure output, environment details, and any facts that identify or narrow the likely cause.
3. Read the plan after the reproduction evidence so that the plan's diagnosis and proposed change can be checked against what was actually reproduced rather than judged in isolation.
4. While reading the plan, record:
   - the stated diagnosis,
   - the proposed files or components to change,
   - the implementation approach,
   - the stated scope and out-of-scope work,
   - the test plan,
   - any risks, assumptions, or unknowns.
5. Read the draft plan comment after the plan. Record what it claims about the cause, scope, and intended next steps.
6. Read repo facts, scope rules, and any relevant repository conventions last. Record any branch, ownership, coordination, testing, or contribution rules that apply to the package.
7. Do not grade any rubric check until the evidence above has been gathered.

<!-- What gets read, in what order, before any check is graded, and
what to note down from each part while reading. A complete procedure
decides the order (issue first? repro evidence first?) and says why
the order matters for the checks that come later. -->

## Evidence gathering

1. For `diagnosis-supported`, compare the plan's stated diagnosis with the reproduction evidence and observed failure output. Record whether the diagnosis is directly supported, merely plausible, contradicted, or not established.
2. For `cause-targeted`, compare the proposed implementation approach with the diagnosis and reproduction evidence. Record whether the planned change addresses the evidence-supported cause or only changes the visible symptom.
3. For `scope-bounded`, collect the plan's stated scope, out-of-scope statements, files to change, and implementation steps. Record any unrelated refactor, cleanup, feature work, or open-ended investigation included in the proposed change.
4. For `executable`, collect the implementation steps, target files or components, and any repository facts needed to begin. Record whether a stranger familiar with the repository could start the work without inventing a behaviorally important step.
5. For `test-observable`, compare the test plan with the reproduction steps. Record:
   - what command or real-code path will be run,
   - what failed before,
   - what observable result is expected after the change,
   - whether the test would actually distinguish fixed behavior from the original failure.
6. For `uncertainty-honest`, collect all assumptions, risks, unknowns, and conditional statements in the plan. Record any claim presented as fact even though the available evidence does not establish it.
7. For `conventions-aligned`, compare the plan and draft comment with the issue thread, repo facts, scope rules, and repository conventions. Record any conflict with stated coordination, branch, scope, ownership, testing, or contribution requirements.
8. If an evidence source named by a rubric check is absent from the package, record that absence explicitly rather than inferring the missing information.


<!-- For each evidence family your rubric's checks name, the concrete
gathering move: which part of the package (or, live, which page or
thread location per your evidence guide) to pull the fact from, and
what to record. A complete procedure leaves no check whose evidence an
executor would have to hunt for. -->

## Check execution

1. Grade checks in this order:
   1. `diagnosis-supported`
   2. `cause-targeted`
   3. `scope-bounded`
   4. `executable`
   5. `test-observable`
   6. `uncertainty-honest`
   7. `conventions-aligned`
2. For each check, use only the evidence gathered for that check and apply the pass condition exactly as written in `rubric.md`.
3. Grade a check `pass` when the available evidence satisfies the pass condition.
4. Grade a check `fail` when the available evidence shows the pass condition is not met.
5. Grade a check `unclear` only when the evidence required to decide is genuinely missing, ambiguous, or internally conflicting.
6. Do not treat lack of a particular heading, template phrase, number of steps, or formatting choice as failure unless the rubric explicitly requires that structure.
7. Do not infer missing behaviorally important details from what would be typical or likely in the repository.
8. A later check may reuse evidence already gathered for an earlier check. Do not re-read the whole package unless the evidence conflicts or a required source was missed.
9. When a check fails or is unclear, identify the specific evidence or missing evidence that caused that grade.


<!-- How one check runs against gathered evidence: in what order the
checks execute, what an executor does when evidence for a check is
genuinely absent, and when a check may be graded without re-reading
the whole package. A complete procedure makes two executors grade the
same package the same way. -->

## Verdict assembly

1. After all checks are graded, apply the verdict rule from `rubric.md`.
2. Accept the package only if every required check is graded `pass`.
3. Treat any required check graded `unclear` as a failure.
4. Reject the package if any required check is graded `fail` or `unclear`.
5. Preferred checks, if any are added later, may be reported but never change the final verdict.
6. In the output, include each check's grade with a short evidence-based reason.
7. For every failed or unclear required check, quote or identify the specific plan, repro, comment, thread, or repo evidence that determined the grade.
8. End with the required JSON block using the final binary verdict:
   - `accept` when every required check passes
   - `reject` otherwise

<!-- How the per-check grades become the final accept or reject:
apply your rubric's verdict rule, state how unclear grades enter it,
and say what gets quoted in the output for the deciding check. A
complete procedure produces the same verdict from the same grades,
every time. -->
