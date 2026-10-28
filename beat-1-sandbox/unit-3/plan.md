# Plan for issue #63

## Diagnosis

The reproduced failure is in `tests/unit/test_readme_scorer.py::TestReadmeScorer::test_readme_with_all_quality_signals`.

The README fixture used by the test is only 51 words, and the scorer reports:

`readme_scored category=minimal score=0.8717142857142858 word_count=51`

The test first expects the README to be longer than 100 words and later expects `word_count_category` to be `comprehensive`.

From reading the README scorer implementation, the word-count thresholds are:

- fewer than 100 words: `minimal`
- 100–499 words: `adequate`
- 500 or more words: `comprehensive`

This means increasing the fixture only above 100 words would satisfy the first assertion but would still leave it in the `adequate` category. The likely issue is that the fixture no longer matches the behavior that this test is intended to exercise.

Before making the change, I will confirm from the surrounding test and scorer code that the test is intentionally validating the `comprehensive` README path rather than an outdated expectation.

## Scope

In scope:

- inspect the README fixture used by `test_readme_with_all_quality_signals`
- confirm the scorer's word-count thresholds
- update the fixture so it reaches the intended category if the surrounding assertions confirm that `comprehensive` is the expected behavior
- remove the issue #63 `@pytest.mark.xfail(strict=True, ...)` marker once the underlying test is fixed
- add or adjust only the minimum test data needed to make the fixture consistent with the scenario being tested
- rerun the original reproduction and relevant README scorer tests

Out of scope:

- changing the production word-count thresholds unless code inspection shows that the test expectation is incorrect
- redesigning README scoring
- unrelated scorer refactors or cleanup

## Branch

Implementation branch:

`fix/63-readme-fixture-length`

## Files

Expected file to change:

- `tests/unit/test_readme_scorer.py`

Files to inspect:

- `tests/unit/test_readme_scorer.py`
- the production README scorer implementation that defines the word-count categories

If source inspection shows the intended behavior differs from the current test expectation, I will record that as a deviation before changing the implementation direction.

## Approach

1. Inspect `test_readme_with_all_quality_signals` and identify the exact README fixture used by the test.
2. Inspect the production README scorer code to confirm the current word-count thresholds and the intended meaning of `minimal`, `adequate`, and `comprehensive`.
3. Compare those thresholds with all assertions in the test.
4. If the test is intentionally exercising the `comprehensive` path, expand the fixture to at least 500 words while preserving the other quality signals the test is meant to cover.
5. Remove the `@pytest.mark.xfail(strict=True, reason="issue #63: ...")` marker from `test_readme_with_all_quality_signals` after the test behavior is corrected.
6. Avoid changing production scoring behavior unless inspection shows that the test expectation itself is outdated.
7. Re-run the original failing test and the broader README scorer test file.

## Test plan

Re-run the original Unit 2 reproduction:

`python -m pytest tests/unit/test_readme_scorer.py::TestReadmeScorer::test_readme_with_all_quality_signals -q --runxfail`

Before the fix, this reproduced:

`assert data["word_count"] > 100`

with:

`E       assert 51 > 100`

After the fixture change, the targeted test should pass with `--runxfail`, and the scorer should place the fixture in the category expected by the test.

Before removing the strict xfail marker, running the test normally should produce an `XPASS(strict)` result once the underlying failure has been fixed.

Then remove the issue #63 `@pytest.mark.xfail(strict=True, ...)` marker and run:

`python -m pytest tests/unit/test_readme_scorer.py -q`

Expected result: the README scorer test file changes from `22 passed, 1 xfailed` to `23 passed`.

If practical, I will also run the broader relevant test suite after the targeted file passes.

## Risks and unknowns

- The first failing assertion only requires more than 100 words, but the later `comprehensive` assertion requires at least 500 words under the current scorer thresholds.
- The fixture may be shared with other assertions or tests, so expanding it could affect other quality-signal calculations.
- The current evidence strongly suggests a fixture/test mismatch, but I will verify the surrounding test and production scorer before treating that as the final implementation direction.
- If inspection shows the `comprehensive` expectation is outdated rather than the fixture, the implementation plan will need to change.

## Reproduction evidence

Unit 2 reproduction command:

`python -m pytest tests/unit/test_readme_scorer.py::TestReadmeScorer::test_readme_with_all_quality_signals -q --runxfail`

Observed failure:

`assert data["word_count"] > 100`

`E       assert 51 > 100`

Observed scorer output:

`readme_scored category=minimal score=0.8717142857142858 word_count=51`

Observed thresholds from the scorer implementation:

- `<100` → `minimal`
- `100–499` → `adequate`
- `>=500` → `comprehensive`

## Deviations

None yet. Any change from this plan will be recorded here before implementation continues.