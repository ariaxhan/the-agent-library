---
name: prep-site-for-ai
description: Make a website legible to LLMs, AI search engines, and autonomous agents — structured data (JSON-LD), llms.txt, semantic server-rendered HTML, machine-readable facts, crawler access, and provenance signals — so AI systems quote you correctly instead of skipping or hallucinating about you. Use when prepping a site for AI search / generative engines (GEO), making content agent-readable, exposing facts to LLM crawlers, or fixing why AI tools misrepresent a business. Triggers include "prep my site for AI", "make this AI-readable", "GEO / generative engine optimization", "why does ChatGPT get my business wrong", "add structured data / llms.txt", "is my site crawlable by AI".
---

# Prep a Site for AI

AI search engines, chat assistants, and autonomous agents now read your site and answer *for* you. If your facts aren't machine-legible, two things happen: the AI skips you, or it guesses — and a guessed fact is a wrong fact attributed to your business. The job here is to make every claim a machine can read directly, trace to a source, and reproduce without inventing anything.

This is a narrower, deeper pass than a general quality audit. It cares about one axis: **can a non-human reader extract correct, current facts about you?** (For the broad pass — a11y, performance, responsive, etc. — use [`audit-website-quality`](../audit-website-quality/SKILL.md).)

## 1. Make the content actually reachable

An AI crawler that can't see your content can't quote it.

- **Server-render the facts.** Critical content (hours, prices, address, product details) must be in the initial HTML, not painted in later by JavaScript. Many AI crawlers don't execute JS. View source — if the fact isn't there, it doesn't exist to them.
- **Don't gate facts** behind auth, cookie walls, or "load more" interactions for the parts you want quoted.
- **Reachable `robots.txt` + XML sitemap.** Don't block AI user-agents you want to be cited by; do decide deliberately which ones you allow.

## 2. Express facts in structured data

Prose is ambiguous; markup is not. Add JSON-LD for every entity type the page represents:

- `Organization` / `LocalBusiness` — name, address, phone, hours, geo, sameAs (social profiles).
- `Product` / `Offer` — price, availability, currency.
- `FAQPage`, `Article`, `Event`, `Review` — as applicable.

Every value in the JSON-LD must match the visible page. Structured data that contradicts the rendered text is worse than none — it reads as deceptive and gets discounted.

## 3. Make facts machine-readable in the markup too

- Hours, prices, addresses as **text**, never baked into an image. An AI can't read a JPEG of your menu.
- Use semantic time/address elements (`<time datetime>`, `<address>`) so the value is unambiguous.
- One clear, declarative sentence per fact beats a clever paragraph. AI extracts atomic claims.

## 4. Add an `llms.txt`

Publish `/llms.txt` (and optionally `/llms-full.txt`) — a plain-Markdown summary of what the site is, the key facts, and links to the canonical pages for each topic. It's the AI-era equivalent of a sitemap aimed at language models: a curated, unambiguous source you control, so the model reads your framing instead of reconstructing one.

## 5. Signal provenance and freshness

AI systems weight sources they can trust and date.

- Show **when** a fact was last updated (visible date + `dateModified` in structured data). Stale-looking pages get discounted.
- Attribute claims to a real author/source where it matters (`Article.author`, bylines).
- Make the canonical URL explicit so the AI cites the right page, not a duplicate.

## 6. Render correct previews

- Open Graph + Twitter card metadata so links shared into AI/chat surfaces render a real title, description, and image.
- Canonical URL and OG URL agree.

## 7. Ground every fact — anti-slop

This is the rule that protects you from amplifying your own mistakes: **only publish facts that trace to a real source.** Invented hours, hallucinated awards, or generic AI filler don't just read as slop — once an AI ingests them, it confidently repeats them everywhere. A machine-legible site full of unverified claims is a hallucination amplifier. Verify the source of each fact before you make it easy to extract.

## Output

Produce a checklist of what's present vs. missing per section above, the specific markup to add (with the actual JSON-LD / `llms.txt` content drafted), and a flag on any fact that's currently in an image, behind JavaScript, or unverifiable. End with the one highest-leverage fix.

## The principle underneath

This mirrors a website compiler's rule that *everything factual traces to a source and nothing is invented*. If you're building a system that generates many sites, bake these as policies the generator must pass rather than a manual checklist — see [`build-sites-as-specs`](../../code-engineering/build-sites-as-specs/SKILL.md).
