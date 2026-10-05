# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/63

**Verdict output**


**The verdict must record `accept` for this issue.** Choose an issue your own skill
accepts. If your skill rejects every candidate you try, that is a signal about your
rubric rather than about the issues: revise it and re-run — retries are unlimited and a
partial re-run costs about $0.20 — or run the skill on different candidates. Output
recording `reject` for the issue you chose earns no credit for this field.

````
#63 is accepted. I re-checked the live issue just now. Your rubric and scope are unchanged since the last run, and so is the issue: still 4 comments, nobody assigned, no PRs referencing it, and no maintainer replies.

- maintainer-alive: pass. Nobody with repo access has replied on the issue, but human Collaborator Aburke225 committed to main on 2026-09-16. That's 18 days ago, inside your 30-day window.
- repo-in-use: pass. The last push was 2026-09-16, and the repo isn't archived.
- unclaimed: pass. Nobody is assigned and no PR references it. The two classmate claim comments don't block it under your house rule.
- contribution-policy: pass. docs/CONTRIBUTING.md and the PR template say nothing about AI.
- newcomer-scope (preferred): pass. The issue names the test, gives the failing assertion (assert 51 > 100), shows how to reproduce it, and suggests a fix.

It fits your profile well: it's a Python test fix with a one-command reproduction (pytest tests/unit/test_readme_scorer.py -q). Fixing it means reading how the README scorer counts words, which gets you into the backend code. No classmate PR exists to compete with, and there's no frontend or CSS work.

When you open the PR, docs/CONTRIBUTING.md asks you to remove the test's @pytest.mark.xfail(strict=True) marker. If you leave it, CI fails once the test passes.

```json
{
  "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/63",
  "checks": [
    {"name": "maintainer-alive", "grade": "pass", "evidence": "No maintainer reply on #63, but human Collaborator Aburke225 committed to main on 2026-09-16 (18 days ago, within 30)"},
    {"name": "repo-in-use", "grade": "pass", "evidence": "Last push to any branch 2026-09-16, 18 days before 2026-10-04; not archived"},
    {"name": "unclaimed", "grade": "pass", "evidence": "No assignees, no linked or mentioned PRs; two classmate claim comments ignored per house rule"},
    {"name": "newcomer-scope", "grade": "pass", "evidence": "Names test_readme_with_all_quality_signals, expected vs actual (assert 51 > 100), repro `pytest tests/unit/test_readme_scorer.py -q` and suggested fix"},
    {"name": "contribution-policy", "grade": "pass", "evidence": "docs/CONTRIBUTING.md and PR template state no AI restriction"}
  ],
  "verdict": "accept"
}
```
````

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

3/3 → 9/10 → 3/3 targeted → 16/20 → 2/5 targeted → 4/4 targeted → 18/20 → 18/20 after re-save → 18/20 targeted after the `maintainer-alive` revision → 18/20 final, matching the committed rubric.

**Issue analysis**

My rubric's verdict for issue-10 was accept, while the gold label is reject. My rubric incorrectly accepted this issue because the required checks focused on repository activity, maintainer responsiveness, and whether the issue was currently claimed, while newcomer-scope was only a preferred check. The issue is actually a documentation megaissue containing roughly 115 links to other issues, not one clearly bounded task. A newcomer would first need to choose and investigate a separate linked issue before doing any implementation work, so the issue itself is not independently actionable. This exposed a weakness in my scope rule: a tracking issue or megaissue should not count as newcomer-scoped unless it identifies one specific subtask to complete.

**Check rationale**

**Check quoted from `rubric.md`:**

| maintainer-alive | This issue's own thread (response + how old it is), the 5-issue response-time sample (fastest response time in the sample), and the repo-facts "last 5 default-branch commits" (author and date, to check for recent human maintainer commit activity). | Pass if any of the following is true: (1) this issue has received a substantive owner/member/collaborator response; (2) the 5-issue response-time sample contains at least one maintainer response in under 60 days; or (3) a human owner/member/collaborator has made a default-branch commit within the last 30 days, showing recent direct maintenance activity even if maintainers do not normally comment on issue threads. If this issue has no maintainer response and was opened less than 14 days before the snapshot, treat its silence as unclear, not a failure. Fail only when there is no substantive response on this issue, the fastest maintainer response in the sample is 60 days or more (or there are no maintainer responses at all), and there has been no human maintainer default-branch commit within the last 30 days. Automated bot commits do not count as maintainer activity. | required |

**Reasoning:** I designed this check to avoid treating issue comments as the only sign that maintainers are active. A substantive response on the issue is the strongest direct evidence, while the five-issue response-time sample shows whether the team responds to contributors more generally. I use the fastest response in that sample because even one reasonably quick reply shows that maintainers are still engaging; if the quickest response is 60 days or more, that is much stronger evidence of inactivity.

I also added recent human default-branch commits as an independent activity signal because some maintainers actively work on the repository without regularly commenting on issue threads. The 30-day cutoff keeps that signal recent, and automated bot commits are excluded so repository automation cannot create a false impression of maintainer activity. Finally, an unanswered issue that is less than 14 days old is treated as `unclear` rather than failed, because there has not been enough time to fairly judge whether maintainers are unresponsive.

**Trade-offs**

After adding the commit-based pass condition, I re-ran the full eval set and got the same 18/20 result, with the same two issues (issue-10, issue-20) still disagreeing — no previously-correct verdict flipped. I know this because I compared the per-issue results of both full runs directly before committing the change.

What this check gives up: a maintainer who commits code regularly but would never actually respond to a newcomer's question or review a first-time contributor's PR would still pass this check, because recent commits alone satisfy clause (3) regardless of how that maintainer treats contributors. The check can't distinguish "actively maintains the codebase" from "actively engages with contributors," which are related but not the same thing.

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

#63 fits what I was looking for because it is a small Python debugging task with a clear test command, no frontend work, and a manageable scope for the time I have. The rubric correctly identified that #63 had no competing PR while #64 had two, and that both were active, unclaimed-in-practice, and well within policy. Beyond what the rubric showed me, I personally preferred #63 because I felt more confident debugging a focused Python test failure than working through the broader relevance-scoring logic in #64. The main challenge will be understanding why the xfail(strict=True) test is failing and how the scorer counts words before changing the fixture or assertion, along with normal first-PR friction such as CI and review feedback.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
