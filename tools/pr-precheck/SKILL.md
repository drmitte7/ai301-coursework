---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

<!--
THIS IS THE PART YOU WRITE, and it is the last one: the frame itself.
Weeks 1 through 3 handed you a working SKILL.md and you filled the
files behind it; this week the frame ships as headings, and you write
what it says. The frontmatter above and the section headings below are
fixed (CONTRACT.md's layout rule); the instructions under each heading
are yours. Write instructions to the tool, in the imperative, the way
weeks 1-3's frames spoke to you: what to read, in what order, what to
refuse, what to emit. Your executor in the rotation is the test: a
frame gap they hit (cannot tell what the tool reads, or how a verdict
gets assembled) is a missing sentence here.

One section is not yours: the JSON schema in "Verdict and output" is
reproduced from CONTRACT.md verbatim and may not be altered. Your
words decide everything around it.
-->

## The question

<!-- State, in your words, the one question this tool answers and what
a PR package is: what artifacts it contains and what they are read
against. CONTRACT.md fixes the question; your frame has to say it so
the tool cannot wander into grading something else. -->

Determine whether exactly one pull request package is ready
to submit.

A PR package includes its title, description, commits,
code diff, test evidence, and implementation plan. Compare
these artifacts against the issue requirements and the
repository's contribution standards.

Answer only: Is this PR ready to submit?

Use the rubric and procedure provided with this skill.
Never invent requirements or grade unrelated work.

## Inputs and modes

<!-- Define both modes. Live mode: name every input (your plan.md with
its deviation notes, your branch's diff, your draft PR title and
description, your test evidence, your issue), where each comes from,
and what a house-chain student reads instead. The branch's diff is
everything the branch changes relative to the repo's default branch:
`git diff main...HEAD` (three dots), run from the working copy, is
the command that produces it; name the source that concretely. Eval
mode: state that the bundle is the whole world, nothing is fetched,
and every check runs with the full verdict rule. -->

Determine which mode is requested before grading.

### Live mode

Use live mode to review the student's actual pull request.

Read the following evidence:
1. The issue and its GitHub discussion thread.
2. plan.md, including documented deviations.
3. The committed branch diff using `git diff main...HEAD`.
4. The PR title and description from pr_draft.md.
5. Test results from test_evidence.md.
6. The repository's .github/PULL_REQUEST_TEMPLATE.md.
7. The repository's docs/CONTRIBUTING.md.

Run the diff command from the Path Review working directory.

Compare the implementation with the issue, plan, and tests.

For house-chain students, use the instructor's house plan
and reproduction package instead of their own Unit 3
plan and reproduction evidence.

Apply the same rubric to house-chain submissions.

### Eval mode

Use eval mode when the evaluation harness provides a
frozen PR package.

Treat the supplied bundle as the only evidence source.

Read the issue, plan, code changes, test evidence,
PR description, and standards contained in the bundle.

Do not fetch GitHub information or read outside files.

Evaluate every rubric check using the full verdict rule.
Do not invent missing evidence.

## The scope seam (live mode only)

Read scope.md before reviewing a live PR.
Verify that the repository matches the configured Repo value.
Refuse to grade an out-of-scope repository or an unfilled
repository placeholder.

Apply the repository's house rules during the review.
Ignore scope.md entirely in eval mode.

<!-- Tell the tool when to read scope.md, what to do with the rules it
finds there, what to refuse, and what to do when the scope's repo line
is an unfilled placeholder. State that eval mode ignores scope.md
entirely. CONTRACT.md names the required behavior; your frame has to
instruct it. -->

## The voice seam (live mode only)

<!-- Tell the tool when to read voice-guide.md, which outgoing text it
gates (the PR title and description), how to report a broken rule, and
why it never changes the verdict on its own. State that eval mode
ignores it entirely. -->

Read voice-guide.md when reviewing a live PR.
Evaluate the PR title and description against its rules.
Report violations in the review summary.

Voice violations affect the verdict only when a rubric
check explicitly makes them relevant.

Ignore voice-guide.md in eval mode.

## Component reads

<!-- Tell the tool how the pieces connect: rubric.md defines the
checks and the verdict rule, references/evidence-guide.md maps where
each evidence family lives, procedure.md is executed as written. Say
what the tool does when the procedure is silent on a step (report the
gap, never improvise around it) and what it does when rubric.md or
procedure.md has no content (the refusal rule, stated as an
instruction). -->

Read rubric.md for grading checks and the verdict rule.
Read references/evidence-guide.md to locate evidence.
Follow procedure.md for the grading workflow.

If the procedure does not specify a necessary step,
report the gap rather than inventing instructions.

If rubric.md or procedure.md contains no substantive
instructions, refuse to grade.

## Verdict and output

<!-- State the binary verdict space (accept means submit, reject means
hold) and instruct the tool to end its reply with the fenced JSON
block below, valid and last, with nothing after it. The schema is
CONTRACT.md's, verbatim; do not edit it. -->

Return exactly one of two verdicts:

- `accept`: The PR satisfies the rubric and is ready
  to submit.
- `reject`: The PR does not satisfy the rubric and
  should be held for corrections.

Do not produce a third verdict or numerical score.

Apply the verdict rule defined in rubric.md.

For each rubric check, report:
- The check name.
- A grade of pass, fail, or unclear.
- One line of specific supporting evidence.

Provide a concise, readable per-check summary.

End every completed grading response with the
following fenced JSON block.

Replace placeholders with actual values while preserving
the exact schema and key order.

Do not write anything after the final JSON block.


```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

<!-- Write the standing rules the tool grades under: evidence first,
grade the thing not the polish, the rubric decides, the procedure
decides how, and how unclear grades are treated when the rubric's
verdict rule is silent. CONTRACT.md states each as a guarantee; your
frame has to make them instructions. -->

### Evidence first

Use specific facts, quotes, code changes, or test
results to justify every check grade.

Do not assign grades based on assumptions or
general impressions.

### Grade the artifact, not the polish

Evaluate whether the PR implements the issue,
follows the plan, provides credible test evidence,
and meets repository standards.

Do not accept a polished description that hides
missing tests or unrelated changes.

Do not reject a concise PR simply because its
writing is brief.

### The rubric decides

Apply the checks and verdict rule exactly as
written in rubric.md.

Do not change grading conditions based on personal
preference or confidence.

### The procedure decides how

Follow procedure.md in its specified order.

If a necessary step is missing, report the procedural
gap rather than inventing another step.

### Handle unclear evidence

Assign `pass` when specific evidence satisfies a check.

Assign `fail` when evidence shows the check is not met.

Assign `unclear` when the evidence is insufficient to
determine whether the check passes.

Apply the treatment of unclear grades specified in
rubric.md.

If the rubric is silent, treat unverifiable required
claims as failures.

Never fabricate missing evidence, test results,
or implementation details.
