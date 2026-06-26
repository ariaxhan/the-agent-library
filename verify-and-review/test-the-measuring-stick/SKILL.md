---
name: test-the-measuring-stick
description: Check whether a score, grade, or ranking actually has teeth before you trust it. Use when relying on any quality number — an AI grading its own or another AI's output, a rubric score on writing, a relevance ranking, a benchmark result. Triggers include "is this quality score real", "does my grader/eval actually work", "can I trust this ranking", "does this benchmark mean anything". Produces a dummy-answer result, a cheap-floor comparison, and a verdict on whether the measure is trustworthy.
---

# Test the Measuring Stick

Before you trust what a score says about the work, test what the score says about garbage. A grader that rates a worthless answer highly is not measuring quality — it is measuring something else, and every "good" score it gave is unverifiable. This finds that out cheaply.

Use it whenever a number is about to drive a decision, especially when an AI assigned the number.

## 1. Build the laziest fake answer

Construct a response that does zero real work but has the right shape:

- Copy the question back as the "answer".
- Return an empty-but-correctly-formatted result.
- Give a single canned, content-free line.

The goal is something that should obviously score near the bottom if the grader works.

## 2. Run the dummy through the exact same scoring

Use the identical grader, rubric, prompt, or ranking — unchanged. No special-casing. Whatever scored the real work scores the dummy.

## 3. Read what the dummy score tells you

- **Dummy scores low** → the stick has teeth. The real scores mean something.
- **Dummy scores high** → the stick is **broken**. A presence/format/length signal is being rewarded instead of quality. The real scores are now unverified, not good — treat every one of them as suspect.

A format or structure bonus is the usual culprit: it can float an empty answer to the top.

## 4. Check for a saturated ceiling

If almost everything — good, mediocre, dummy — clusters near the top, the test is too easy to separate quality at all. Reaching for a bigger, more expensive grader to push the winners higher is p-hacking, not science. Make the test harder, not the grader stronger.

## 5. Compare against the cheap floor, not zero

"Beats chance" or "beats nothing" is the wrong bar. Name the cheapest thing that already works — the free tool, a one-line baseline, copy-paste, the incumbent — and confirm the expensive option beats **that**. An expensive signal that loses to a free baseline is not an improvement, however high its raw score.

## Output

Return:

- The dummy answer used and the score it received.
- The verdict: stick has teeth / task is trivially easy (saturated ceiling) / stick is broken.
- The cheap-floor comparison: what the cheapest working alternative scores, and whether the expensive option actually beats it.
- If the stick is broken, name the signal it is actually rewarding (presence, format, length) so it can be fixed.
