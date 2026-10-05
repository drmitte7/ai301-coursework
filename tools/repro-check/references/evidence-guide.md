# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-facts block, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; the rubric swap showed you what that feels
like. Write the map you wish your grader had.
-->

## Environment

**Where it lives:** In an eval bundle, look first in the **Candidate repro report** for the candidate’s stated tool/app version, OS/platform, install method, build profile, shell/runtime, or other relevant setup details. Also compare those details with the **Issue** section when the original report names a target environment or when the issue explains environment-specific behavior. In live mode, compare the environment stated in the GitHub issue with the environment written in the student’s draft repro comment.

**What good looks like:** The candidate records enough concrete environment information for another person to understand or repeat the result, and any meaningful difference from the issue’s original environment is explicitly called out. Environment can also be established indirectly when the observed output uniquely identifies a relevant condition, such as a specific build profile; if the output does not distinguish between plausible environments, the missing condition still needs to be stated.

<!-- Where the environment record lives, and what a sufficient one
looks like against the issue's stated target. -->

## Steps

**Where it lives:** In an eval bundle, look in the **Candidate repro report**, especially any numbered steps, command blocks, setup instructions, or action sequences that show how the candidate triggered the behavior. In live mode, look at the student’s draft repro comment for the exact commands, inputs, clicks, or setup actions they expect another person to repeat.

**What good looks like:** The steps give a clear starting state and enough concrete actions, commands, or inputs for a stranger to repeat the candidate’s procedure without guessing an essential detail. This section only asks whether the candidate’s own procedure is followable; whether those steps reproduce the original issue belongs under **Behavior shown**.
<!-- Where the reproduction steps live, and what makes them followable
by a stranger, starting state to trigger. -->

## Behavior shown

**Where it lives:** In an eval bundle, look in the **Candidate repro report** for the actual artifacts produced by the reproduction: terminal output, error messages, logs, screenshots, state checks, or control runs. Compare those artifacts with the **Issue** section’s reported behavior. In live mode, look at the student’s draft repro comment and any attached screenshots or pasted output, then compare them with the behavior described in the GitHub issue.

**What good looks like:** The artifacts should directly demonstrate the same behavior the issue reports, using materially matching inputs and actions. Strong reports often include more than one corroborating signal—such as an error plus a state check, or a failing case plus a control run—so the result is not based on one ambiguous output. If the candidate changes a material input or produces a different error or failure mode, that is an adjacent problem rather than evidence of the reported issue.

<!-- Where the artifacts live (output excerpts, logs, screenshots),
and what it means for an artifact to show the issue's behavior rather
than an adjacent one. -->

## Honesty

**Where it lives:** In an eval bundle, read both the **Candidate claim comment** and the **Candidate repro report**, then compare any statements about reproduction, cause, certainty, scope, understanding, or completion against the evidence actually shown in the report. In live mode, compare the student’s draft claim/repro wording with the commands, outputs, screenshots, logs, or other evidence they actually collected.

**What good looks like:** The wording should say only what the evidence supports. A careful “I could not reproduce this after trying X, Y, and Z; here is what happened instead” is still honest and acceptable. Overclaiming includes asserting an unproven cause, saying a bug was definitely reproduced when the evidence shows a different failure, claiming complete understanding without support, or presenting planned work as if it were already done.

<!-- Where claims and their backing meet: how to tell a report that
says exactly what happened (including an honest cannot-reproduce) from
one that claims more than its evidence shows. -->

## Comms

**Where it lives:** In an eval bundle, look at the **repo-facts** section for the repository’s bug-report template, contribution guide, and any AI-use or disclosure policy, then compare those expectations with the **Candidate claim comment** and **Candidate repro report**. In live mode, check the GitHub issue template and contribution docs, then compare them with the student’s draft comment and repro text.

**What good looks like:** The candidate should substantially follow the repo’s requested format and communication rules, including the core fields the bug template asks for and any required AI-assistance disclosure. Good communication is specific to the issue and backed by the candidate’s actual work; boilerplate, emotional filler, or generic claims should not replace the concrete details the repo asks for. If the repository explicitly requires disclosure of AI assistance, that disclosure must appear in the candidate’s comment or report.

<!-- Where the words meet the repo: the claim comment against the
issue, the comments against the repo's stated templates and
contribution policy (including AI-use disclosure requirements), and
what specific-and-honest looks like next to boilerplate. -->
