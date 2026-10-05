# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username**

drmitte7

---

## Posted upstream

**Claim comment**

Link: https://github.com/codepath/pathreview-ai301-fa26-s3/issues/63#issuecomment-5988476844
Text: "Hi, I'd like to work on issue #63 as a contribution. I'm planning to reproduce the failing README scorer test, understand how the fixture and xfail(strict=True) assertion interact, and then make the smallest change needed to bring the test in line with the intended behavior. I'll report back with what I find before opening a PR."

**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/63#issuecomment-5989080070

`````
Reproduction

Environment

- OS: Windows 11 Home, 64-bit
- Python: 3.14.6
- pytest: 9.1.1
- Commit: `2f4e82f52efbcfcc57d65b3fa5348672163ca088`
- Working tree: clean
- Dependencies: installed in the repository virtual environment with `python -m pip install -e ".[dev]"`

Steps
From the repository root, I activated the virtual environment and ran the affected test with the `xfail` behavior disabled so I could see the underlying failure directly:

```
.\.venv\Scripts\Activate.ps1
python -m pytest tests/unit/test_readme_scorer.py::TestReadmeScorer::test_readme_with_all_quality_signals -q --runxfail
```

Observed behavior
The test stops at this assertion:

```
assert data["word_count"] > 100
E       assert 51 > 100
```

The scorer output from the same run reports:

```
readme_scored category=minimal score=0.8717142857142858 word_count=51
```

So the README fixture currently contains 51 words and is classified as `minimal`.
Looking at the scorer logic helped clarify the mismatch:

- fewer than 100 words → `minimal`
- 100–499 words → `adequate`
- 500 or more words → `comprehensive`

The test expects both a word count above 100 and, later, a `word_count_category` of `comprehensive`. Since the fixture has only 51 words, it cannot satisfy either intended threshold. Simply increasing it slightly past 100 would satisfy the first assertion but would still leave it in the `adequate` category rather than `comprehensive`.

Expected behavior
The fixture used by `test_readme_with_all_quality_signals` should be long enough to match the expectations encoded in that test, including the `comprehensive` word-count category.

Result
On my setup, I confirmed the same fixture/assertion mismatch described in issue #63: the scorer counts the fixture as 51 words and classifies it as `minimal`, while the test expects a substantially longer README.

At this point I have only reproduced and inspected the failing test. I have not changed the fixture or validated a proposed fix against the complete test suite.
`````

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

 3/3 → 8/10 → 2/2 targeted → 1/2 targeted before the fix was saved → 2/2 targeted after saving → 19/20 full run → 3/3 targeted after the disclosure fix → 20/20 final full run with `--save-run`, matching the committed `eval-run.txt`.

**Package analysis:** The gold label for `pkg-05` was **accept**, but my original rubric incorrectly produced **reject**. The disagreement came from my first version being too strict about literal format. The package did not include the exact commands or output requested by the repository template, so my rubric treated that as a failure even though the candidate had provided enough equivalent information to understand the environment and reproduce the procedure. I revised the rubric so `steps-followable` and `conventions` judge whether the required substance is present, rather than requiring the exact template wording or command output. After that change, `pkg-05` correctly evaluated as **accept**, matching the gold label.

**Check rationale**

`steps-followable`:

> Pass if a stranger can reproduce the candidate's procedure from the information provided without guessing any behaviorally relevant step or input. Exact literal commands or file contents are not required when the report gives enough detail to reconstruct the essential setup and actions unambiguously. Fail if key steps or inputs are missing in a way that requires guessing something that could change the observed behavior.

I revised this check after `pkg-05` showed that my original version was too strict about literal commands and template formatting. The package provided enough information to understand and repeat the procedure, but my earlier wording could reject it simply because it did not reproduce the repository’s requested commands exactly.

I changed the check to focus on whether another person can reconstruct the behaviorally important setup and actions without guessing. I kept the requirement that missing information should still fail when the missing detail could affect the observed result. This lets the rubric accept equivalent, useful reproduction evidence without making the check so loose that incomplete procedures pass.


**Trade-offs**

 After loosening `steps-followable` to accept equivalent-substance evidence instead of requiring exact literal commands, I re-ran `pkg-06` as a canary with `--only`, and it stayed correctly rejected. That gave me confidence that the change did not simply make the check permissive across the board. The trade-off is that a report could still sound equivalent while quietly omitting a behaviorally important setup detail, so the check depends on judging whether the missing information could actually change the observed result.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
