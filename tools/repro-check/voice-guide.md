# Voice guide: how I talk upstream

<!--
THIS IS THE PART YOU WRITE (new this week). Live mode reads this file
before any comment of yours goes out the door; eval mode ignores it
entirely, because your voice is yours and carries no gold labels.

This is not etiquette. "Be polite and concise" is advice for everyone
and therefore rules for no one. Write rules YOU need, in your own
words, each one concrete enough that the skill can hold a draft
against it and say which rule it breaks.

Three sections. Fill all three.
-->

## Who I am in threads

I’m a newer open-source contributor with experience in Python and Java, but I’m still learning each codebase I work in. I use issues to investigate carefully, reproduce problems before making claims, and be clear about what I have and have not verified. Maintainers can expect me to ask when I’m unsure, follow the project’s contribution rules, and report back with concrete evidence.

<!-- 2-3 lines. Who is talking when you comment on an issue: your
experience level stated plainly, what you are doing in this repo, what
readers can expect from you. This is the register your rules protect. -->

## Rules I write by
### Rule: Separate evidence from guesses

I can share a hypothesis, but I should label it as a hypothesis until I have traced or tested it.

- Wrong: "This is obviously caused by the null result handling."
- Right: "My current guess is that the null-result path may be involved, but I have not traced that code yet."

### Rule: Be honest when I cannot reproduce

If I try seriously and still cannot trigger the bug, I should say that clearly and document what I tested instead of forcing a success claim.

- Wrong: "I confirmed the bug even though my output was different."
- Right: "I could not reproduce the reported failure with this setup; here are the exact steps I tried and what happened instead."

### Rule: Follow the repo’s AI policy

Before posting, I check whether the repository requires AI-use disclosure and say exactly what assistance I used when disclosure applies.

- Wrong: "No mention of AI assistance even though the repo requires disclosure."
- Right: "I used Claude Code to help review my reproduction steps and wording; I verified the commands and results myself."

<!-- 3-5 rules, drafted from the lecture's slide-12 moment. Each rule
needs a wrong/right pair from your own hand: one line you might
actually have written that breaks the rule, and the line you would
post instead. The pair is what makes a rule executable; a rule without
one is a wish.

Format each rule like this:

### Rule: <short name>

<The rule, one or two sentences.>

- Wrong: "<a line that breaks it>"
- Right: "<the line to post instead>"
-->

## Things I never post

A comment of mine never does any of the following:

- Promises a fix by a specific date, or implies my PR is guaranteed to merge.
- Piggybacks on someone else's reproduction ("same as above, can confirm") instead of posting my own evidence.
- Claims a root cause, a successful reproduction, or complete understanding unless I have actually verified it.
- Reads as demanding, dismissive, or entitled, even if I'm frustrated or rushed when I write it.

<!-- A short list. Promises you cannot keep, tones you refuse,
shortcuts you know you reach for when tired. The skill quotes this
list back at you when a draft crosses it. -->
