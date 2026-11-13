# Evidence guide: where evidence lives in a PR package

<!--
THIS IS THE PART YOU WRITE (third week running: the map stays in your
hands). Your tool uses this guide as its map: for every kind of
evidence a rubric check names, this file says WHERE to find it in a PR
package and WHAT GOOD LOOKS LIKE when you do.

The four families below are the harness's failure categories under
the names the eval README uses: plan fidelity = silent-drift, test
evidence = not-tested, diff quality = unreviewable, standards and
comms = standards-wall. A package that fails none of them is a
clear-accept. Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the plan-context block's scope pair and test
  plan, the candidate PR's diff, commits, description, or
  test-evidence section, the repo-facts block's template asks and
  stated policy). In live mode (where in your working copy and on
  GitHub: your plan.md and its deviation notes, your branch's diff,
  your draft title and description, your captured test output, the
  repo's PR template and CONTRIBUTING.md).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("every changed file falls inside the
  plan's stated boundary or a deviation note") over adjectives ("the
  diff is clean").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts three ways: your
procedure says WHEN to gather each family, this guide says WHERE, and
your SKILL.md says the tool reads both. Write the map you wish your
executor had.
-->

Use this guide to locate concrete evidence for each check
in rubric.md.

In eval mode, use only the frozen PR package supplied by
the evaluation harness. Never fetch outside evidence.

In live mode, use the student's Path Review working copy,
GitHub issue, plan, PR draft, and test evidence.

For every check, record specific evidence rather than
assuming that a claim is true.

## Plan fidelity (harness category: silent-drift)

<!-- Where the plan states its scope, boundary, and deviation notes,
and where the diff shows what actually changed. What it means for a
diff to match the plan, for an honest deviation to re-tie a mismatch,
and what silent drift looks like in each direction (more than the
plan, or less with no note). The description's fidelity claims read
against the diff live here too: a description claiming more or less
than the diff delivers is silent drift, not a comms problem. -->

### Where it lives in eval mode

Read the package's plan-context block, including:
- Issue requirements and expected behavior.
- The plan's scope and file boundaries.
- Planned implementation steps.
- Any documented deviations.

Read the candidate PR's unified diff and description.

Compare the diff's actual changes with the plan's
stated scope and the PR description's claims.

### Where it lives in live mode

Read:
- The GitHub issue and discussion thread.
- plan.md, including the Deviations section.
- The committed diff from `git diff main...HEAD`.
- The PR title and description in pr_draft.md.

For house-chain submissions, use the supplied house
plan and reproduction materials.

### What good evidence looks like

Every meaningful changed file and implementation behavior
is within the issue's scope and the plan's stated boundary,
or is explained by a documented, justified deviation.

The PR description accurately represents the changes
visible in the diff.

A disclosed limitation or justified deviation does not
automatically make the PR unacceptable.

### Warning signs

- The diff changes files unrelated to the issue.
- A planned behavior is silently missing.
- The description claims functionality not implemented.
- The implementation differs from the plan without
  an explanation in the deviation notes.

## Test evidence (harness category: not-tested)

<!-- Where the PR shows its proof: the test-evidence section's
before/after against the plan's test plan and the reproduction's own
steps, and the outcome of the repo's own checks or suite. What
decisive looks like (an observable behavior named, the expected-after
stated, the checks' outcome visible) next to "tests pass". -->

### Where it lives in eval mode

Read:
- The plan-context block's test plan.
- The reproduction steps included in the package.
- The candidate PR's test-evidence section.
- The package's reported test commands and outcomes.
- Repository-required checks listed in repo facts.

Compare the actual results against the tests the
plan said would verify the fix.

### Where it lives in live mode

Read:
- The test plan and reproduction steps in plan.md.
- test_evidence.md, including before-and-after results.
- The repository's required commands from its PR template
  and docs/CONTRIBUTING.md.

Check the recorded results for:
- Unit tests.
- Integration tests.
- Lint.
- Type checking.
- The issue-specific reproduction.

### What good evidence looks like

The evidence identifies the behavior being tested,
the command or reproduction steps used, and the
observable result.

Before-and-after evidence demonstrates what changed.
The test results are consistent with the PR's claims.

Applicable, runnable repository checks have recorded
outcomes. Documented repository limitations may explain
why a particular check could not run.

### Warning signs

- The description says "tests pass" without results.
- No observable reproduction or test output is supplied.
- Required runnable checks were skipped.
- A failure is hidden or described as a success.
- Test evidence does not exercise the reported change.

An honestly disclosed test failure is not automatically
a rejection. Evaluate its significance using the
specific rubric pass condition and repository requirements.


## Diff quality (harness category: unreviewable)

<!-- Where the change itself lives: the unified diff and the commit
list. What a reviewable change looks like (the fix visible, nothing
unrelated riding along) and the debris tells: debug leftovers, dead
code, commented-out blocks, formatting churn, drive-by edits. -->

### Where it lives in eval mode

Read the candidate PR's:
- Unified diff.
- Changed-file list.
- Commit list and descriptions.

Compare these artifacts against the plan-context
block's declared scope.

### Where it lives in live mode

Inspect the committed branch changes:

`git diff main...HEAD`

Also inspect the changed-file summary:

`git diff main...HEAD --stat`

Compare the changed files with plan.md and any
documented deviations.

### What good evidence looks like

The diff clearly shows the intended fix and related
tests without unrelated changes that obscure review.

Changed files serve the issue or are explained by
justified deviations.

A reviewer can identify what behavior was changed
and why.

### Warning signs

- Debugging statements left in production code.
- Large blocks of commented-out or dead code.
- Unrelated formatting changes.
- Accidental generated files.
- Unrelated refactoring or drive-by fixes.
- Commits or hunks unrelated to the planned issue.

Do not reject a PR merely because it has multiple
commits or contains a legitimate supporting change.

Judge the substance and relevance of the diff.


## Standards and comms (harness category: standards-wall)

<!-- Where the repo states its asks (the repo-facts block's PR
template sections, contributing instructions, and stated policy,
including AI-use disclosure) and where the PR honors them: the
stated sections filled with real content, the disclosure present,
explicit maintainer direction in the thread engaged. What compliant
looks like next to boilerplate or a visibly ignored ask. (Whether
the description's claims match the diff is plan fidelity, above.) -->

### Where it lives in eval mode

Read:
- The repo-facts block.
- PR template requirements supplied in the package.
- Contribution rules and stated policies.
- Any explicit maintainer requirements included
  in the package's issue thread.
- The candidate PR's title, description, and notes.

Look for required issue references, testing information,
template sections, and AI-use disclosure.

### Where it lives in live mode

Read:
- .github/PULL_REQUEST_TEMPLATE.md.
- docs/CONTRIBUTING.md.
- The GitHub issue thread.
- pr_draft.md, including Notes for Reviewers.
- voice-guide.md for personal communication rules.

The voice guide is used only in live mode.
Its requirements affect the verdict only if a
rubric check explicitly makes them mandatory.

### What good evidence looks like

The PR addresses every mandatory template section
with specific, relevant information.

The issue reference is correct. Testing information
and limitations are described accurately.

The AI-use disclosure satisfies the applicable
repository or course requirement.

Explicit maintainer requests are addressed where
relevant to the proposed change.

An N/A response is acceptable only when the stated
requirements permit it and the explanation is credible.

### Warning signs

- Missing required PR template sections.
- Boilerplate left without meaningful information.
- Missing or inaccurate issue reference.
- Required AI-use disclosure omitted.
- Repository contribution rules ignored.
- Explicit applicable maintainer directions ignored.

Do not reject a PR merely because the writing is
short or stylistically simple.

Evaluate whether the actual repository requirements
have been satisfied.

Whether the PR's claims match the diff is evaluated
under Plan fidelity, not under this section.