# Procedure: how this tool grades a PR package

<!--
THIS IS THE PART YOU WRITE (second week running for the procedure).
Week 3 you wrote these steps for a plan package; this week the graded
object is a PR package, and the read that matters most is a
side-by-side: the diff against the plan, the evidence against the test
plan, the description against both. Your week-3 procedure is the
pattern; do not paste it unchanged, because its read order was built
for a different object.

Your rotation is the design brief again, and this week friction routes
three ways: a stall on WHAT to decide is a rubric gap, a stall on
WHERE to look is a procedure gap (this file), and a stall on what the
tool even reads or outputs is a frame gap (your SKILL.md). A complete
procedure lets someone who has never seen a PR package before grade
one exactly the way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
plan's scope pair before opening the diff, and list the files the plan
names" is a step; "understand the change" is a wish.
-->

## Read order

<!-- What gets read, in what order, before any check is graded, and
what to note down from each part while reading. A complete procedure
decides where the plan sits in the order (before the diff? before the
description?) and says why the order matters for the side-by-side
checks that come later. -->

1. Determine whether the request is live mode or eval mode.

2. In live mode, read scope.md first. Verify that the
   repository is in scope. Stop without grading if the
   Repo line is unfilled or the repository is outside
   the permitted scope.

3. Read rubric.md, procedure.md, and
   references/evidence-guide.md before grading.
   Refuse to grade if rubric.md or procedure.md
   contains no substantive instructions.

4. In live mode, read voice-guide.md and record the
   communication requirements for the outgoing PR.
   In eval mode, ignore scope.md and voice-guide.md.

5. Read the issue requirements first. In live mode,
   inspect the issue and discussion thread. In eval
   mode, use only the issue evidence in the bundle.
   Record the issue number, expected behavior,
   acceptance criteria, and stated limitations.

6. Read the implementation plan before the code diff.
   Record the planned files, intended behavior,
   test plan, and any documented deviations.
   Reading the plan first prevents the diff from
   redefining the expected scope.

7. Read the complete code diff. In live mode, run
   `git diff main...HEAD` from the Path Review
   working directory. In eval mode, read the diff
   supplied in the frozen package.

   Record all changed files, meaningful additions,
   deletions, and unrelated modifications.

8. Read the test evidence. Record the reproduction
   steps, before-and-after behavior, test commands,
   actual results, failures, and unavailable checks.

9. Read the PR title and description. Record its
   summary, issue reference, claimed changes,
   testing claims, limitations, and reviewer notes.

10. Read the repository standards. In live mode,
    inspect .github/PULL_REQUEST_TEMPLATE.md and
    docs/CONTRIBUTING.md. In eval mode, use only
    the standards supplied in the bundle.

    Record required template sections, tests,
    disclosures, and other applicable rules.

11. Do not grade any check until the relevant
    issue, plan, diff, tests, description, and
    standards have been gathered.

## Evidence gathering

1. Plan fidelity:
   Compare the issue requirements and plan.md
   against the changed files and implementation.

   Record which planned changes are present,
   which planned changes are missing, and which
   actual changes were not included in the plan.

   Check whether differences are documented in
   the plan's Deviations section.

2. Description accuracy:
   Compare each material claim in the PR title,
   summary, changes, and testing sections with
   the actual diff and recorded test evidence.

   Record any claim that is contradicted by the
   implementation or unsupported by evidence.

   Check whether omissions and limitations
   are disclosed accurately.

3. Test evidence credibility:
   Compare the plan's test cases and reproduction
   steps with the supplied test evidence.

   Record the test commands, observable results,
   before-and-after behavior, and any failures.

   Distinguish actual test output from statements
   claiming that tests passed.

4. Repository checks:
   Read the repository's required checks from
   the template or contribution standards.

   Compare those requirements with the recorded
   results for unit tests, integration tests,
   lint, and type checking.

   Record which checks ran, their outcomes, and
   which checks were unavailable.

   Distinguish a documented repository limitation
   from a runnable check that was simply skipped.

5. Diff quality and reviewability:
   Inspect every changed file and meaningful diff hunk.

   Record unrelated changes, debug statements,
   commented-out code, accidental generated files,
   unexplained modifications, and other debris.

   Determine whether the changes are focused enough
   for a reviewer to understand.

6. PR template compliance:
   Compare the PR description with the mandatory
   template and contribution requirements.

   Record whether the issue reference, summary,
   changes, testing evidence, reviewer notes,
   and other required sections are addressed.

   Accept an N/A explanation only when the
   repository's standards permit it.

7. AI-use disclosure:
   Identify the repository's applicable AI-use
   disclosure requirement.

   Read the PR description and reviewer notes
   to find the disclosure.

   Record whether the disclosure addresses the
   stated requirement and whether it contradicts
   the provided evidence.

8. Communication clarity:
   Read the PR title and description against
   the issue and implementation.

   Record any misleading, contradictory, or
   confusing wording that prevents a reviewer
   from understanding the change.

   Do not penalize a description merely
   because it is concise.

9. In live mode, also compare the outgoing PR
   title and description against voice-guide.md.

   Record any voice-guide violations separately
   unless a rubric check explicitly applies.


<!-- For each evidence family your rubric's checks name, the concrete
gathering move: which part of the package (or, live, which file, diff,
or page per your evidence guide) to pull the fact from, and what to
record. The load-bearing gathers this week are pairings: diff files
against plan scope, claimed evidence against the plan's test plan and
the repo's checks, description claims against diff contents. A
complete procedure leaves no check whose evidence an executor would
have to hunt for. -->

## Check execution

<!-- How one check runs against gathered evidence: in what order the
checks execute, what an executor does when evidence for a check is
genuinely absent, and when a check may be graded without re-reading
the whole package. A complete procedure makes two executors grade the
same package the same way. -->

1. Execute every check in the exact order
   in which it appears in rubric.md:

   - Issue and plan fidelity
   - Description accuracy
   - Test evidence credibility
   - Repository checks
   - Diff quality and reviewability
   - PR template compliance
   - AI-use disclosure
   - Communication clarity

2. For each check, read its Evidence column
   and use the facts recorded during evidence
   gathering.

3. Compare the gathered facts against the
   check's stated Pass condition.

4. Assign exactly one grade:

   - pass: Specific evidence satisfies the
     pass condition.

   - fail: Evidence demonstrates that the
     pass condition is not satisfied.

   - unclear: Available evidence cannot establish
     whether the condition is satisfied.

5. If relevant evidence is genuinely absent,
   assign unclear rather than assuming success.

   Do not fetch missing information in eval mode.

6. Record one concise evidence statement per check.

   The statement must name a concrete fact,
   file, test result, diff entry, or quote.

7. Do not change a check's grade based on
   personal preference or overall impression.

8. Do not automatically fail an honestly
   disclosed limitation. Apply the individual
   pass condition and distinguish transparent
   shortfalls from hidden problems.

9. Use the previously gathered evidence.
   Re-read a source only when resolving a
   specific contradiction or unclear fact.

10. Complete every rubric check before
    assembling the verdict.

## Verdict assembly

<!-- How the per-check grades become the final accept or reject:
apply your rubric's verdict rule, state how unclear grades enter it,
and say what gets quoted in the output for the deciding check: the
check whose failure the verdict turned on. When more than one check
failed, your procedure picks which one gets quoted (first failing
required check in rubric order is a fine rule); nothing picks it for
you, so write the rule down. A complete procedure produces the same
verdict from the same grades, every time. -->

1. Collect the grade, evidence statement,
   and weight of every rubric check.

2. Apply rubric.md's verdict rule exactly:

   - Return accept only if every required
     check receives pass.

   - Return reject if any required check
     receives fail or unclear.

   - Preferred checks never independently
     change the verdict.

3. If the verdict is reject, identify the
   first required check in rubric order
   that received fail or unclear.

   Quote that check's decisive evidence
   first in the readable summary.

   Then report the remaining failed or
   unclear required checks.

4. If the verdict is accept, summarize
   the strongest evidence that the PR
   matches the issue, plan, testing, and
   repository standards.

5. Produce a readable per-check summary
   with the exact rubric check names,
   grades, and supporting evidence.

6. Include any applicable live-mode
   voice-guide findings in the summary.

7. Produce the final fenced JSON block
   using the exact schema defined in
   SKILL.md and CONTRACT.md.

   Set item to the PR URL in live mode
   or the bundle identifier in eval mode.

   Include every rubric check in the
   checks array in rubric order.

   Use only pass, fail, or unclear grades.

   Set verdict to exactly accept or reject.

8. Validate that the JSON is syntactically
   valid and has no additional keys.

9. End the response immediately after the
   closing JSON code fence.

   Do not append commentary, suggestions,
   or other text after the JSON block.
