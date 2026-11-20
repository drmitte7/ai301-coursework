# Toolkit Portfolio

**Student:** Dimitar Krastev

## Featured Tools

I selected these four tools because they represent the core lifecycle of my open-source contribution workflow—from filtering out unviable repositories to validating pull requests before submission. Together, they show how my toolkit shifted from simple automated prompts to structured, criteria-driven checks after hitting real-world friction during issue selection and codebase verification.

**issue-select**

**What it is, and the judgment hole I wrote:** A triage tool initially scoped to evaluate candidate issues within my course's Path Review repository against repository health, contribution policies, and technical fit before committing engineering time. The judgment hole I authored is the scoring rubric and fit profile—defining explicit thresholds for maintainer responsiveness, AI contribution policies, and Python/backend scope alignment so I avoid stalled or restricted issues.

**How it evolved, dated:** On 2026-10-04 (`18df72c`), I built the initial implementation to automate basic issue filtering within the Path Review repository. That same day (`aac6830`), I expanded the maintainer-alive rubric to recognize recent human maintainer commits, even when maintainers had not directly responded in issue threads. Finally, on 2026-10-04 (`5791586`), I updated the scope and fit profile to add my personal technical fit profile, specify the Path Review repository, and clarify rules around existing classmate pull requests.

**Evidence:**

```text
2026-10-04  18df72c  Initial issue-select implementation
2026-10-04  aac6830  Expanded maintainer-alive check
2026-10-04  5791586  Updated scope and fit profile

item      gold    verdict  agree
issue-10  reject  accept   NO
issue-20  reject  accept   NO

categories: claimed 4/4  clear-accept 8/8
dead-repo 3/3  policy 1/1  scope 2/4
agreement: 18/20 scored items  (bar: 18/20: PASS)
```

**issue-scout**

**What it is, and the judgment hole I wrote:** A discovery and triage tool that extends issue selection beyond a single repository to live GitHub searches. The judgment hole I authored is the search strategy, ranking filters, and detailed evaluation rubric used to score live candidate issues for technical scope, clarity, and contribution feasibility.

**How it evolved, dated:** During an initial live GitHub scan, the ranking process surfaced issues that looked viable on the surface but were poorly scoped for a single contribution. On November 16, 2026, after applying a scope patch to the rubric, I regraded three candidate issues—resulting in two accepted issues and one rejected issue based on scope feasibility.

**Evidence:**

```text
Unit 6 — Regrading After Scope Patch
Date: 2026-11-16

Accepted:
1. emfcamp/Website#176
2. SciML/OrdinaryDiffEq.jl#82

Rejected:
3. python/cpython#94808
   scope-feasible: fail
   Tracking issue covering approximately 136 sub-tasks.
```

**plan-check**

**What it is, and the judgment hole I wrote:** A pre-implementation gate that evaluates whether a proposed engineering plan is ready to post in an issue thread and build from. The judgment hole I authored is a seven-point verification rubric requiring a supported diagnosis, a cause-targeted solution, bounded scope, an executable plan, observable testing, honest uncertainty, and adherence to repository conventions so I do not write code against flawed assumptions or over-engineered designs.

**How it evolved, dated:** On October 28, 2026 (`b811758`), I created and evaluated the `plan-check` skill in a single implementation pass, validating the rubric against a 20-item test suite covering clear accepts, scope creep, wrong root causes, unbuildable plans, and thread conventions.

**Evidence:**

```text
2026-10-28  b811758  Initial plan-check implementation

categories: clear-accept 7/7  scope-creep 4/4
thread-convention 2/2  unbuildable 3/3
wrong-cause 4/4
agreement: 20/20 scored items  (bar: 18/20: PASS)
```

**pr-precheck**

**What it is, and the judgment hole I wrote:** A final submission gate that evaluates whether a pull request and its supporting evidence are ready for maintainer review. The judgment hole I authored is a seven-check rubric requiring plan fidelity, description accuracy, test credibility, documented results for required repository checks, diff reviewability, pull request template compliance, and explicit AI-use disclosure so I can identify unverified changes, unsupported claims, and unrelated modifications before requesting final review.

**How it evolved, dated:** On November 13, 2026 (`a98b053`), I created and evaluated `pr-precheck` against a 20-item test suite covering clear accepts, untested changes, silent drift, standards violations, and unreviewable diffs. Later in November 2026, I integrated `pr-precheck` into the ship-gate and ran it against my Feast draft PR #7187 (`feature/latest-historical-retrieval`). While the focused tests and Ruff lint and formatting checks passed, `pr-precheck` returned a `reject` verdict—causing the ship-gate to report `STOP`—because broader repository checks were still incomplete and the scoped `mypy` check reported unresolved errors.

**Evidence:**

```text
2026-11-13  a98b053  Complete AI301 Unit 4 PR precheck

categories: clear-accept 7/7  not-tested 4/4
silent-drift 4/4  standards-wall 2/2
unreviewable 3/3
agreement: 20/20 scored items  (bar: 18/20: PASS)

Feast PR #7187 — ship-gate integration:
ship-gate: repo check 1/3 `Latest retrieval and regression tests`: ok (7s)
ship-gate: repo check 2/3 `Ruff lint`: ok (0s)
ship-gate: repo check 3/3 `Ruff formatting`: ok (0s)
ship-gate: STOP. your own pr-precheck rejected feature/latest-historical-retrieval: verdict reject.
```

## Inventory

- **repro-check:** Created on October 5, 2026 (`9b3bfe7`) to evaluate bug reproduction evidence before posting—verifying issue alignment, environment details, followable steps, outcome accuracy, and repository conventions—and achieved a 20/20 evaluation score.
- **ship-gate:** Tested in November 2026 using Ubuntu WSL2 and native Linux Claude Code to run focused Feast tests, Ruff lint, and Ruff formatting before invoking `pr-precheck`, passing all three focused checks while returning `STOP` after `pr-precheck` rejected the incomplete broader verification.

## The Arc

**Beat 1**

Date: October 4, 2026

Friction: Initial filtering in `issue-select` missed active repositories where human maintainers were pushing commits without replying in issue threads, and lacked explicit rules for my technical fit profile and existing classmate pull requests in the Path Review repository.

Change: Expanded the maintainer-alive rubric to recognize recent human maintainer commits (`aac6830`) and added my fit profile, repository target, and classmate PR boundaries (`5791586`).

Result: `issue-select` reached 18/20 agreement on its evaluation suite, passing all claimed, clear-accept, dead-repo, and policy cases while surfacing two remaining scope edge cases.

**Beat 2**

Date: October 5, 2026

Friction: Posting incomplete or unverified bug reproductions risked wasting maintainer attention and misdiagnosing root causes before writing code.

Change: Built `repro-check` (`9b3bfe7`) with a five-point rubric enforcing issue alignment, environment capture, reproducible steps, accurate outcome reporting, and repository conventions.

Result: `repro-check` scored 20/20 on its evaluation suite, demonstrating that the rubric correctly classified all 20 evaluation cases before I applied it to broader workflows.

**Beat 3**

Date: October 28, 2026

Friction: Without a structured check prior to implementation, proposed fixes risked scope creep, addressing the wrong root cause, or violating repository conventions.

Change: Created `plan-check` (`b811758`) to enforce seven pre-implementation criteria—including supported diagnosis, bounded scope, executable steps, and observable testing.

Result: `plan-check` achieved 20/20 agreement across all test categories, correctly classifying all four scope-creep and three unbuildable-plan test cases.

**Beat 4**

Date: November 13, 2026

Friction: Needed an objective final check to ensure pull request diffs, descriptions, test evidence, and AI-use disclosures matched repository standards before requesting maintainer review.

Change: Built and evaluated `pr-precheck` (`a98b053`) with a seven-check submission rubric covering plan fidelity, test credibility, diff reviewability, and repository checks.

Result: `pr-precheck` scored 20/20 on its evaluation benchmark and was subsequently wired into the automated `ship-gate` workflow.

**Beat 5**

Date: November 16, 2026

Friction: Extending issue triage from a single course repository to live GitHub searches via `issue-scout` initially surfaced oversized tracking issues that were unfeasible for a single contribution.

Change: Applied a scope patch to the `issue-scout` rubric and regraded the candidate issues from the live GitHub scan.

Result: The regrade classified two issues as acceptable under the rubric (`emfcamp/Website#176` and `SciML/OrdinaryDiffEq.jl#82`) and rejected `python/cpython#94808` (`scope-feasible: fail`) due to its approximately 136 sub-tasks. Later manual investigation of `emfcamp/Website#176` uncovered AI contribution restrictions that led me to pivot to Feast #1687.

**Beat 6**

Date: November 2026

Friction: Even after focused feature tests and Ruff checks passed on my Feast draft PR #7187 (`feature/latest-historical-retrieval`), broader repository checks had not been completed, and the scoped `mypy` check still failed with seven errors.

Change: Integrated `pr-precheck` into `ship-gate` across Ubuntu WSL2 and native Linux Claude Code and ran the full pre-submission check against the live Feast branch.

Result: `ship-gate` passed the three focused repo checks (`Latest retrieval and regression tests`, `Ruff lint`, and `Ruff formatting`) and then halted with `STOP` when `pr-precheck` returned `reject`, demonstrating that the draft was not yet ready for final review.

## Limitations and What's Next

While my toolkit performed well on controlled 20-item evaluation benchmarks, high scores do not guarantee reliable performance across every live repository. Automated triage checks can still miss nuanced contribution restrictions—such as the AI policy limits on `emfcamp/Website#176`—or underestimate the underlying complexity of a codebase. Furthermore, chaining multiple skills together across different environments like Ubuntu WSL2 and native Linux introduced setup and verification friction when running repository-wide test suites and type checkers.

Next, I plan to tighten issue-scoping rules and pair automated discovery with an explicit manual check of repository `CONTRIBUTING` guidelines before selecting an issue. I also want to test `plan-check` and `pr-precheck` across a wider variety of active open-source repositories and streamline the `ship-gate` configuration so full repository checks and type verification run consistently with less manual setup.

**Tool limits.**

issue-select: Incorrectly accepted two scope-related edge cases in its evaluation suite (scoring 18/20) and remained confined to the Path Review repository rather than general GitHub discovery.

issue-scout: Initially surfaced poorly scoped candidate issues before its scope patch and did not reliably detect repository-specific AI contribution restrictions without manual follow-up.

plan-check: Achieved 20/20 on its synthetic evaluation cases, but its reliability across diverse, real-world repository conventions and complex architectural changes is not yet established.

pr-precheck: Depends on complete, accurate test evidence and configured repository checks, meaning it can flag missing verification but cannot execute or substitute for those missing checks itself.
