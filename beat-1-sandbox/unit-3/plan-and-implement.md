# Unit 3 — Plan and Build

## Posted upstream

**GitHub username**

drmitte7

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/63#issuecomment-6469840166

I reproduced issue #63 and confirmed that `test_readme_with_all_quality_signals` is using a README fixture that scores at 51 words and is classified as `minimal`, while the test expects a longer README and later expects the `comprehensive` category.

My plan is to inspect the test fixture and scorer thresholds together, then make the smallest change that brings the fixture in line with the behavior the test is intended to validate. If the test is meant to exercise the `comprehensive` path, I expect the change to be limited to expanding the fixture rather than changing the production scoring thresholds.

I’ll work on branch `fix/63-readme-fixture-length`, remove the issue #63 strict `xfail` marker once the test is fixed, and validate the change with the original `--runxfail` reproduction followed by the full README scorer test file.

I used Claude Code to help review the plan and wording; I verified the reproduction evidence and checked the planned commands myself.

---

## Your branch

**Branch**

`fix/63-readme-fixture-length`

**Evidence**

Before the fix:

Command:

```text
python -m pytest tests/unit/test_readme_scorer.py::TestReadmeScorer::test_readme_with_all_quality_signals -q --runxfail
```

Observed failure:

```text
assert data["word_count"] > 100
E       assert 51 > 100
```

Observed scorer output:

```text
readme_scored category=minimal score=0.8717142857142858 word_count=51
```

After the fix, the updated README fixture contained 561 words.

Targeted validation command:

```text
.venv\Scripts\python.exe -m pytest tests/unit/test_readme_scorer.py::TestReadmeScorer::test_readme_with_all_quality_signals -q --runxfail
```

Actual output:

```text
.                                                                    [100%]
1 passed in 1.01s
```

Full README scorer validation command:

```text
.venv\Scripts\python.exe -m pytest tests/unit/test_readme_scorer.py -q
```

Actual output:

```text
.......................                                              [100%]
23 passed in 0.29s
```

---

## Eval iterations

**Run history**

The eval runs, in order, were:

1. Full run: `17/19` scored items agreed, with `pkg-02` errored because of a Windows stdin encoding issue.
2. Targeted `pkg-02` run after fixing the runner: `0/1`.
3. Targeted run on `pkg-02,pkg-05,pkg-14,pkg-03,pkg-10`: `4/5`.
4. Targeted run on `pkg-14,pkg-01,pkg-07,pkg-11,pkg-16`: `5/5`.
5. Final full run: `20/20` scored items agreed.

The final full run matched every category:

```text
clear-accept 7/7
scope-creep 4/4
thread-convention 2/2
unbuildable 3/3
wrong-cause 4/4

agreement: 20/20 scored items  (bar: 18/20: PASS)
```

**Package analysis**

I analyzed `pkg-14`.

The gold label was `accept`, and my final rubric also decided `accept`.

Earlier, my rubric incorrectly rejected `pkg-14` because `diagnosis-supported` and `uncertainty-honest` required too much certainty before implementation. The package had a diagnosis that fit the reproduced reattach behavior and identified the relevant subsystem, but the exact mechanism still needed implementation-time tracing.

I revised the rubric so that an evidence-supported working diagnosis may pass when the plan explains how tracing or testing will confirm the uncertain mechanism before relying on it. After that revision, `pkg-14` was correctly accepted.

**Check rationale**

Current check from `rubric.md`:

```text
| diagnosis-supported | The plan's stated diagnosis read against the repro evidence, observed behavior, issue context, and any quoted failure output. | Pass if the diagnosis is consistent with the reproduced evidence and provides a plausible explanation for the observed behavior without contradicting known facts. The diagnosis may remain a working hypothesis when the plan identifies how implementation-time tracing or testing will confirm it. Fail if the diagnosis contradicts the evidence, ignores a materially better-supported cause, or states an unsupported mechanism as settled fact without any plan to verify it. | required |
```

I revised this check after `pkg-14` was falsely rejected. The earlier version effectively required the exact mechanism to already be proven before a plan could pass. I changed it to allow a well-grounded working hypothesis when it fits the reproduced evidence and the plan includes a concrete way to confirm it during implementation.

I rejected the alternative of simply making diagnosis uncertainty always acceptable, because that would weaken the check too much and could allow genuinely wrong-cause plans through.

**Trade-offs**

Loosening `diagnosis-supported` creates a risk that a plausible-sounding but incorrect diagnosis could be accepted before its mechanism has been fully traced.

To check that the change did not become too permissive, I reran four `wrong-cause` packages as canaries:

```text
pkg-01: reject
pkg-07: reject
pkg-11: reject
pkg-16: reject
```

All four remained correctly rejected, while `pkg-14` changed to the correct `accept` result.

I also used `pkg-10` as an `unbuildable` canary after loosening the `executable` check. It remained correctly rejected.

The final full run reached `20/20`, confirming that the revised checks fixed the false rejects without flipping the known bad-plan categories.