---
name: humanize-ai-prose
description: Rewrite AI-generated text into genuinely human prose with seven ordered transform passes: add real named specifics, fix the structure, kill the tells (em-dashes, intensifiers, negative parallelism, meta-signposts), admit real limits, and read it aloud.
---

# Humanize AI Prose

A reusable, ordered editing system that turns model-generated prose into writing that
reads like an actual person wrote it. It's two layers: seven **mechanical** transform
passes (each tell is detectable and rewritable), then a **taste** checklist of judgment
calls no find-and-replace can make.

## Why ordering matters

The passes run **truth → structure → paragraph → sentence → word → friction → ear**, and
the order is load-bearing. Inserting one real specific reshapes everything downstream (it
forces you to delete the vague sentence that was standing in for it), so specifics come
first. Word-level fixes come late, because there's no point polishing a sentence you're
about to cut. Read-aloud is last, after the text has stopped changing. Run them in order;
don't jump to the word pass because it feels productive.

## The seven passes, in order

**1. TRUTH: insert real specifics.** AI prose names categories, never instances ("various
campuses," "a meaningful experience," "a typical user"). Give every section at least one
true, named, datable detail: a first name, a place, a month-and-year, a product, a number
that isn't round. This is the highest-leverage move in the whole system. If you don't know
the fact, do **not** invent it. Use the bracket rule below.

**2. STRUCTURE: de-signpost, fix intro and ending.** Delete sentences whose only job is
pointing at other sentences ("Here's the part that surprised me," "In this article we
will," "That's the whole flaw, stated cleanly"). Humans just say the thing. Rewrite the
intro and conclusion completely rather than patching them: they're the most
template-shaped parts of any draft. The ending should *add* something (an implication, an
open question, a last concrete image), never re-list the points. Cap dramatic one-line
closers ("mic drops") at two per piece; one is voice, five is a metronome.

**3. PARAGRAPH: break the isomorphism.** When every paragraph ends by extracting its
lesson and tying it to the thesis, that uniform closure reads as machine even if each
sentence is fine. Let at most a third of paragraphs end on a significance statement; let
the rest end on a fact, an image, or nothing. Vary paragraph openers (scan the first word
of each in a column: no grammatical shape twice in a row) and paragraph sizes (include at
least one one-sentence paragraph and one 5+ sentence paragraph; open one with a question).

**4. SENTENCE: restore burstiness in both directions.** Human writing spikes in
sentence length; AI flatlines, usually at 18–24 words, sometimes (post-editing) at a
relentless punchy 6–12. Find any three consecutive sentences of similar length, cut one
under 8 words, let another run 30–45 with subordinate clauses. Restore parenthetical asides
(2–4 per page: they hold the spoken register flat prose lacks). Break decorative
rule-of-three triads ("skill, compassion, and steadiness"): keep one item and make it
concrete. Allow at most one **negative parallelism** ("it's not X, it's Y" / "that's not a
glitch, it's...") per piece; rewrite the rest as direct statements that just say what it
*is*.

**5. WORD: lexicon and punctuation purge.** Run this for human readers, not detectors
(see below). Zero em-dashes: replace with a period, a comma, or parentheses, not a
semicolon spree. Delete the abstract intensifier lexicon: *profoundly, transformative,
unwavering, invaluable, leverage, delve, harness, streamline, robust, seamless, nuanced,
multifaceted, landscape, realm, tapestry, testament, crucial, pivotal, groundbreaking.*
Replace each with the plain word for the actual thing. Contract by default ("that's,"
"it's," "doesn't") and cap full-form "It is / That is / Here is" sentence-openers at two: surgical apostrophe-avoidance reads as machine. Delete cliché connectors (*Furthermore,
Moreover, Additionally, In conclusion, Ultimately*); paragraph breaks do the connecting.

**6. FRICTION: admit what was hard, boring, or wrong.** AI prose is frictionless: nothing fails, drags, or stays unresolved. Readers flag that false omniscience faster than
any word choice. Per piece, include at least: one thing that was boring or unglamorous, one
limit or failure stated honestly, and one uncertainty left standing ("I'm not sure this
scales past one case" beats fake confidence). Every admitted flaw must be **true**: invented friction is worse than none.

**7. EAR: read it aloud.** No transforms, just a final gate. Read it out loud (or
subvocalize slowly). Any sentence you stumble on, or wouldn't say to a person across a
table, gets rewritten in the words you'd actually use. Any sentence that exists only to
sound good gets cut. Human looseness is allowed (a comma splice, a sentence a beat too
long); typos and broken grammar are not.

## Detectors vs. humans (the structural insight)

As of 2026, the strong detectors (GPTZero, Pangram, Binoculars-style) score **statistical
structure**: sentence-length variance ("burstiness"), paragraph shape, token
predictability, transition-word frequency, not vocabulary. So the **structural passes
(2–4) move detection scores 20–35 points; the word pass (5) moves them under 5.** If you're
trying to pass a detector, the structure work is what matters. The word pass is for the
human reading it. Do both, but know which job each one is doing.

The dangerous tells are the *second-generation* ones, because the obvious lexical ones
(em-dashes, "delve," triads) are already widely scrubbed: uniform punchiness, uncontracted
"It is / That is" anaphora, frictionless confidence, and missing specifics. The single
highest-leverage fix remains one true, named detail per section.

## The taste checklist

After the passes, walk the judgment calls in `reference/checklist.md`. A "no" sends the piece back.
The three that matter most:

- **Could only this author have written it?** Swap the byline. Is there at least one
  detail, opinion, or aside that wouldn't survive the swap? Generic prose survives any swap.
- **Does it take a side?** A real position someone could disagree with, stated without
  hedging. Perfect argumentative balance is itself a tell.
- **Is every admitted flaw true, and every added specific real?** A fake-specific detail is
  the one failure mode this whole system can't recover from.

## The bracket-placeholder rule: never invent facts

When a section needs a real specific (Pass 1) or an honest limit (Pass 6) and you don't
have the fact, **do not fabricate it.** Insert a bracket placeholder that names exactly
what's missing and hand it back to the author:

> `[BRACKET: need one real moment here: a name, a date, one thing that actually happened.
> A first name and one sentence beats a paragraph of reflection.]`

The piece is **not done** while a bracket is open. This is the line between humanizing and
lying: a humanized draft surfaces what only the author can supply; it never makes it up.
