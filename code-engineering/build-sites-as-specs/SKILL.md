---
name: build-sites-as-specs
description: Architect a website-generation system that structurally cannot produce slop, by compiling a validated specification into output instead of generating HTML directly. Use when building an AI site generator, a templating/CMS pipeline, a multi-tenant site builder, or any system where a model or template produces web pages and you keep getting hallucinated facts, inconsistent structure, weak SEO/accessibility, and unmaintainable markup. Triggers include "build a website generator", "AI keeps generating slop sites", "how do I make site generation reliable", "spec-driven site building", "stop the model inventing facts on the page".
---

# Build Sites as Specs

Most AI site builders go straight from a prompt to HTML. That single shortcut is the source of every recurring failure: hallucinated facts, inconsistent structure, broken accessibility, weak SEO, vendor lock-in, output you can't diff or edit. The fix is to stop treating the website as the artifact. **The specification is the artifact. HTML is just one compiled output of it.**

```
Business Data → Brief → SiteSpec → Renderer → HTML
```

Reframed as a compiler: the Brief is source code, the SiteSpec is the intermediate representation, the design system is the standard library, the Renderer is the backend target, HTML is the compiled output. Once you see it this way, the model stops being the center of the system: it fills slots in a spec, it never writes markup, controls design, or invents facts.

## The rule above all others

> **Do not build the AI part first.** Build the grammar (the spec), the compiler (the renderer), and the validator (the policies) so well that the AI becomes the least interesting, most replaceable part of the system.

Build order, inside-out, do not skip ahead:

```
Specification → Validation → Rendering → Generation
```

Generation comes last. If a hand-authored spec can't be validated and rendered into a production-quality site *offline, with zero network and zero model calls*, the architecture isn't done, and adding generation on top will only multiply the cracks.

## The six load-bearing principles

1. **Everything is a policy.** SEO, accessibility, performance, security, content quality. Don't build a separate system for each. Represent them all as uniform `Policy` checks the validator runs against the spec. One small validator, many policies, guarantees that hold *structurally* instead of being hoped for in a prompt.
2. **Everything renders through primitives.** Section authors never write raw HTML. They call `ui.image(ref, { alt, loading })`, `ui.cta(...)`, not `<img>`/`<a>` strings. The primitive enforces alt text, lazy loading, escaping, and analytics centrally. Make the correct thing easier than the incorrect thing; keep escape hatches loud and rare.
3. **Everything vertical lives in packs.** The engine stays generic: it knows how to validate, render, and generate. A *pack* holds what's specific to a domain: which sections exist, what content is allowed, the palettes, typography, and voice. The engine never learns what a restaurant or a photo booth is; the pack does.
4. **Everything factual traces to the Brief.** The model fills slots; it does not invent facts. Hours, prices, claims: all flow from the Brief (real business data), and a `facts-grounded` policy fails the build if any factual field has no source. This is the anti-slop core.
5. **Everything editable has an ID; everything translatable is a key.** Stable section IDs make future editing and regeneration-safety possible (protect human edits across regenerations). Copy referenced by key makes i18n and diffing fall out for free.
6. **Rendering is deterministic.** Same spec + same pack → byte-identical output. Determinism is what makes the system testable, cacheable, and diffable, and what separates a compiler from a slot machine.

## Why this kills slop

The model is *structurally unable* to produce the usual failures:

- It can't write Tailwind soup or inline CSS: it doesn't emit markup, primitives do.
- It can't invent business hours: factual fields fail validation without a source.
- It can't ship a missing `<h1>`, an unlabeled image, or a generic AI paragraph: policies reject the spec before it ever renders.

Quality stops being a prompt you beg for and becomes a gate the artifact must pass. The same checklist a human would run by hand (see [`audit-website-quality`](../../shipping/audit-website-quality/SKILL.md) and [`prep-site-for-ai`](../../shipping/prep-site-for-ai/SKILL.md)) becomes executable policies the generator can't bypass.

## Before you commit

- **Stress-test the plan first.** Challenge the architecture against your real verticals before executing it. Don't blindly scaffold.
- **Start with the smallest spec that proves the loop:** a schema, one pack, a handful of section types, a renderer, a validator, a few policies, and hand-authored fixture specs that render offline. Add generation only once that's solid.
- **Know when it's overkill.** A single one-off landing page does not need a compiler. Just build the page. This pattern earns its weight when you're producing *many* sites, regenerating them, or letting a model drive, i.e. exactly where slop compounds.

## The vocabulary, in one line each

- **Brief**: the validated input facts (source code).
- **SiteSpec**: the portable, versionable intermediate representation (the product).
- **Pack**: the per-vertical design system + allowed content (standard library).
- **Policy**: a uniform validation the spec must pass (the gatekeeper).
- **Primitive**: a safe UI building block that enforces correctness centrally.
- **Renderer**: a deterministic backend that compiles a spec to an output (HTML today, React/PDF/email tomorrow).
