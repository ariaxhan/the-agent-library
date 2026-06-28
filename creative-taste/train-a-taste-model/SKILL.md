---
name: train-a-taste-model
description: Train a small model on your own archive that learns your personal taste and ranks new items the way you would, using implicit curation signals you already produced instead of hand-labeling thousands of examples.
---

# Train a Personal Taste Model

## What this is

You have an archive (photos, drafts, tracks, saved articles, anything) and a real but
unstated aesthetic that decides what you keep, surface, and discard. This trains a tiny
model to predict *your* judgment and rank new items the way you would. It runs on CPU, on
low data, and it learns from the curation signals you already generate by living, so you
never sit down and label thousands of examples by hand.

## The architecture: frozen backbone + tiny head

```
item ──▶ [frozen pretrained encoder] ──▶ embedding ──▶ [tiny trainable head] ──▶ scalar score
              (CLIP / DINOv2 / etc.)        (768-d)      Linear→GELU→Dropout→Linear
```

- **Frozen backbone.** A large pretrained encoder, used only for inference, turns each
  item into one L2-normalized embedding. Images: CLIP or DINOv2. Text: a sentence encoder.
  Audio: a domain encoder. You never fine-tune it: your archive is far too small to move
  a backbone without wrecking it, and the embeddings are already excellent.
- **Tiny head.** The only thing you train: `Linear(d, h) → GELU → Dropout(0.3) → Linear(h, 1)`
  emitting a single taste score. A few hundred KB of weights, minutes to train on CPU.
- **Embed once, reuse forever.** Cache embeddings for the whole archive to disk. Then
  every training run reads vectors, never re-decodes raw items: that decoupling is what
  keeps iteration fast.

## Why pairwise, not absolute scores

Do **not** train the head to predict an absolute 1–10 rating. People are wildly
inconsistent at absolute scores and consistent at comparisons. Train on **pairs**: "A is
preferred over B." The loss is a margin-ranking loss that pushes `score(A) > score(B)` by a
margin; the resulting scalar is a *relative ranking signal*, exactly what you need to sort
new items. It also means every preference signal you own, even a weak one, becomes a
usable training pair.

## Building pairs from implicit curation signals (the tiering)

The whole trick: harvest pairs from curation you already did, weighted by how trustworthy
each signal is. Tier your **positives**:

| Tier | Signal | Strength | Weight |
|------|--------|----------|--------|
| 1 | You explicitly favorited / liked / shipped it | strong | ~0.80 |
| 2 | A platform quality score (continuous) | medium | ~0.05, sampled ∝ the score |
| 3 | You filed it in a collection/album but didn't favorite | medium-weak | ~0.15 |

**Negatives** are a deliberate mix, ~30% hard / 70% soft:

- **Hard negatives**, things you actively rejected: hidden, trashed, low platform score.
- **Random unlabeled**, sampled from the unlabeled pool, *inverse-weighted* by any quality
  prior so you lean toward genuinely "meh," not accidental gems you never got around to.

Then sample (positive, negative) pairs by those weights, shuffle, drop self-pairs. A few
thousand pairs from an archive you never hand-labeled. Run hygiene first: drop dupes,
near-dupes, machine-generated junk, and items lacking provenance, since those leak as fake
negatives or noise as fake positives.

## The honesty rule: eval on YOUR held-out labels

This is the discipline that keeps the project honest. **Evaluate only on held-out pairs
built from your own curation, never on a generic benchmark.** A public aesthetic dataset
measures the *average* person's taste, which is precisely the thing you are trying not to
build. Hold out ~20% of your pairs, and report held-out pairwise accuracy: "on items I
labeled and the model never saw, it agreed with my preference X% of the time." That number,
on your labels, is the only score that means anything.

## Surfacing results: non-max suppression

When you surface a top-N gallery, raw top-scores will clump: one session, one shoot, one
burst, one writing sprint dominates because similar items score similarly. Apply
**non-max suppression** before display: walk items high-to-low, and skip any that are too
close to one already kept along a clustering axis (timestamp + location for photos; source/
date/topic for text). One event can't eat the whole gallery. The ranking stays honest;
only what you *show* gets de-clustered.

## Known failure modes

- **Favorites-alone → mode collapse.** Training on one positive tier collapses the top
  ranking onto a few lookalikes. Mix tiers and keep hard + soft negatives.
- **Borrowed platform scores inject a foreign bias.** A vendor "quality" score encodes
  *their* priors (faces, brightness, sharpness), not yours. Overweight it and the model
  drifts toward their taste. Keep it as a weak input/negative-miner, never a primary positive.
- **Curation signal is noisy and uneven.** You saved things for reasons other than quality
  (the moment mattered, not the craft), and coverage skews toward categories you curate
  most. Expect noisy positives; design for correction loops, not one-shot truth.
- **Tastes drift over time.** An old archive encodes an old eye. Consider a recency cutoff
  or time-weighting so the head learns who you are *now*.

## Generalizing to other domains

Nothing here is image-specific. Swap the frozen encoder and the curation signals:

- **Writing**: sentence-embedding backbone; positives = published/pinned pieces, negatives
  = drafts you abandoned.
- **Music**: audio encoder; positives = playlisted/replayed tracks, negatives = skipped.
- **Anything with implicit curation**: saves, likes, shares, deletes, time-on-item. If you
  already produced a trail of keep/discard decisions, you can train a taste head on it.

The recipe is constant: frozen encoder → cache embeddings → tier implicit signals into
pairs → train a tiny ranking head → evaluate on *your* held-out labels → de-cluster the
surfaced top-N.
