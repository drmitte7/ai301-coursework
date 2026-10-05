# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| `behavior-matches-issue` | Compare the candidate repro's exact input, command/actions, and observed output against the issue's reported behavior. Look for at least two corroborating signals when possible, such as matching output/error plus a second command, state check, or control case that independently supports the same failure. | Pass if the candidate targets the same behavior described in the issue and the evidence honestly shows either (a) that behavior being reproduced, or (b) a concrete, well-documented attempt that could not reproduce it. Fail if the candidate demonstrates a different or adjacent failure, changes a material input or step, or merely repeats the issue's description without verifiable evidence. Unclear only when the bundle genuinely lacks enough information to determine whether the candidate tested the same behavior. | required |
| `environment-recorded` | Check the candidate repro for the runtime details needed to understand or repeat the result, such as application/tool version, OS/platform, installation method, build profile, shell/runtime, or other environment-specific context. These may be stated explicitly or established indirectly by distinctive output that reliably identifies the relevant environment or build mode. | Pass if the repro records enough environment detail to reproduce or correctly interpret the observed behavior. Explicit details count, and indirect evidence also counts when it uniquely identifies the relevant environment condition or build mode. Fail if it gives no concrete environment information and only uses vague statements such as "all my machines." Unclear only when some environment information is present but the relevant condition still cannot be distinguished from plausible alternatives using either the stated setup or the observed output. | required |
| `steps-followable` | Check whether the candidate repro gives concrete, ordered actions, commands, inputs, or setup steps that another person could perform exactly as written and reasonably obtain the candidate's reported result. Do not judge here whether those steps match the original issue; that belongs to `behavior-matches-issue`. | Pass if a stranger can reproduce the candidate's procedure from the information provided without guessing any behaviorally relevant step or input. Exact literal commands or file contents are not required when the report gives enough detail to reconstruct the essential setup and actions unambiguously. Fail if key steps or inputs are missing in a way that requires guessing something that could change the observed behavior. | required |
| `honest-outcome` | Read both the candidate claim comment and the repro report. Compare every statement of success, failure, certainty, cause, scope, and completion against the evidence actually shown in the package. | Pass if the candidate describes only what the evidence supports, including an honest cannot-reproduce result when they clearly document what they tried and what happened instead. Fail if the wording overstates the evidence, claims a cause or reproduction that was not demonstrated, presents an adjacent failure as confirmation of the reported bug, or asserts completion/understanding without support. Unclear only when the wording is cautious but the bundle does not contain enough evidence to determine whether the stated conclusion is justified. | required |
| `conventions` | Check the repo-facts contribution policy and bug-report guidance, then compare those expectations against the candidate claim comment and repro report. Pay particular attention to requested template fields, required disclosures, prohibited content, and any explicit policy about AI-assisted contributions. | Pass if the candidate substantially follows the repository's reporting and contribution conventions by providing the core information those conventions are trying to collect, even if equivalent information is presented in a different form. If the repository requires AI-use disclosure for issue comments, claim comments, repro reports, or other content of this type, the candidate must include the required disclosure statement there. A disclosure rule that applies only to pull requests does not require disclosure in an issue comment or repro report. Fail if a disclosure required for this type of content is missing, if the candidate omits most of the repo's requested substance, or if they violate an explicit contribution rule. Unclear only if the policy is ambiguous about whether it applies to this kind of content. | required |


## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->

Accept only if all five required checks pass. Treat both `fail` and `unclear` as blocking for the final verdict, because an unclear result means the package does not yet provide enough evidence to confidently say it is ready to post.
