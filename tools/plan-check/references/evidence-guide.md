# Evidence guide: where evidence lives in a plan package

<!--
THIS IS THE PART YOU WRITE (second week running: the judgment files
stay in your hands). The skill uses this guide as its map: for every
kind of evidence a rubric check names, this file says WHERE to find it
in a plan package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repro-evidence block,
  the candidate plan's scope statement or test plan, the plan comment,
  the repo-facts block). In live mode (where on GitHub or in the
  draft: the issue thread, the student's posted repro comment, the
  repo's docs, the draft plan and comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the stated cause cites behavior the
  repro evidence actually shows") over adjectives ("diagnosis is
  solid").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts twice: your
procedure.md tells the skill WHEN to gather each family, and this
guide tells it WHERE. Write the map you wish your executor had.
-->

## Diagnosis and grounding

### Where it lives
In an eval package, look at:
- the issue context for the reported problem,
- the repro-evidence block for observed behavior, commands, failures, and outputs,
- the candidate plan's diagnosis or stated cause,
- any quoted evidence inside the plan.

In live mode, look at:
- the GitHub issue thread,
- the student's posted reproduction comment from Unit 2,
- the draft `plan.md`,
- the draft plan comment if it repeats or summarizes the diagnosis.

### What good looks like

The plan's stated cause should explain behavior that the reproduction evidence actually shows. A good diagnosis does not contradict the observed failure, invent facts not present in the evidence, or claim certainty when the evidence only supports a hypothesis.

If the evidence only narrows the cause rather than proving it, the plan should say what still needs to be verified before the implementation depends on that assumption.

<!-- Where the plan states its cause, and where the repro evidence
pins down the behavior that cause must explain. What it means for a
diagnosis to follow from the evidence rather than contradict or
ignore it. -->

## Scope

### Where it lives
In an eval package, look at:
- the candidate plan's in-scope and out-of-scope statements,
- the files or components the plan says it will change,
- the implementation approach,
- the issue context for the size and boundaries of the reported problem.

In live mode, look at:
- `plan.md`,
- the issue thread for any maintainer scope guidance,
- repository docs or contribution guidance when they limit what should change.

### What good looks like
The plan should describe one bounded change that is proportional to the reproduced issue. The planned files, components, and steps should all contribute directly to resolving that issue.

Unrelated refactoring, cleanup, feature work, or open-ended investigation should not be included unless the evidence shows it is necessary to complete the fix.

<!-- Where the plan bounds itself: the in-scope statement, the
not-in-scope line, the files or areas named. What one bounded change
looks like next to a drive-by rewrite. -->

## Executability

### Where it lives
In an eval package, look at:
- the candidate plan's files or components to inspect or change,
- the implementation approach,
- the order of work,
- repo-facts that identify relevant paths, commands, or conventions.

In live mode, look at:
- `plan.md`,
- the repository tree and relevant docs,
- any file paths or commands referenced by the student's Unit 2 reproduction.

### What good looks like
A stranger familiar with the repository should be able to begin the work without asking the author to explain a behaviorally important step.

The plan does not need to contain exact code, but it should identify the target area and intended change clearly enough that the builder does not have to invent the solution direction.

<!-- Where the plan says what will actually be done: files or areas,
approach, order of work. What it means for a stranger to be able to
start executing without asking the author anything. -->

## Test plan

### Where it lives
In an eval package, look at:
- the candidate plan's test plan,
- the repro-evidence block's original commands, inputs, outputs, and failure artifacts,
- repo-facts for the repository's relevant test commands or conventions.

In live mode, look at:
- the Unit 2 reproduction comment,
- `plan.md`,
- repository test documentation or existing test files when needed to understand the real-code path.

### What good looks like
The test plan should re-run the original reproduction or an equivalent real-code path and name an observable result that would distinguish the fixed behavior from the reproduced failure.

A good test plan states what will be run and what successful behavior should look like. "Run tests" or "verify the fix" is not enough when no observable outcome is given.


<!-- Where the plan says how success will be observed, and how that
maps onto the repro evidence's steps and artifacts. What a decisive
test plan names that a vague one does not. -->

## Honesty

### Where it lives
In an eval package, look at:
- the diagnosis,
- assumptions,
- risks,
- unknowns,
- conditional language,
- any deviations section included in the plan package.

In live mode, look at:
- `plan.md`,
- especially its diagnosis, risks and unknowns, and `## Deviations`,
- the issue thread or repro evidence when a claim in the plan appears more certain than the available evidence supports.

### What good looks like
Known facts should be stated as facts, and uncertain conclusions should be labeled as hypotheses, risks, or unknowns.

If a material uncertainty could change the implementation, the plan should say what will be checked before relying on it. Mid-build changes should be recorded honestly under `## Deviations` rather than hidden or rewritten as if they were always planned.


<!-- Where claims meet uncertainty: risks, unknowns, and deviations.
How to tell stated unknowns from false confidence, and where an
honest mid-build deviation gets recorded. -->

## Comms

### Where it lives
In an eval package, look at:
- the draft plan comment,
- issue-thread highlights,
- the repo-facts block,
- stated contribution or communication conventions,
- any AI-use disclosure requirement or required template language.

In live mode, look at:
- the GitHub issue thread,
- the draft `comment.md`,
- `scope.md`,
- repository contribution docs,
- any issue or PR templates that apply.

### What good looks like
The plan comment should reflect the actual issue, diagnosis, scope, and intended next steps rather than reading like generic boilerplate.

It should respect the issue thread and repository conventions, including coordination, branch, ownership, testing, or disclosure requirements when those are stated.

<!-- Where the words meet the thread and the repo: the plan comment
read against the issue's maintainer signals (thread highlights, or
the live thread) and against the repo-facts block's stated templates,
contributing asks, and contribution policy (including AI-use
disclosure requirements). What thread-aware looks like next to
boilerplate. -->
