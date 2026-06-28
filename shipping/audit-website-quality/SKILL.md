---
name: audit-website-quality
description: Audit a website or page against the full quality policy bank — SEO, accessibility, performance, responsive layout, security, content/anti-slop, link integrity, and structured data — and produce graded findings. Use when reviewing a site before launch, auditing an AI- or template-generated site, checking "is this site actually good", or diagnosing why a page ranks/converts/reads poorly. Works on any site regardless of how it was built. Triggers include "audit my site", "review this website", "is this page ready to ship", "check SEO and accessibility", "why does this site feel generic".
---

# Audit Website Quality

A website is judged on many axes at once, and AI- or template-generated sites tend to look finished while failing the boring, structural ones — weak SEO, broken accessibility, invented facts, layout that collapses on a phone. These are not matters of taste. They are **validations**: each one is either satisfied or it is not, and you can check it. Treat this as an inspection, not a vibe.

The deepest failure is content the page cannot back up — invented hours, hallucinated claims, generic AI copy. A good site only states facts that trace to a real source. Hold every page to that.

## 1. Map the surface first

Before checking anything, establish what you're auditing:

- The pages/templates in scope and what each is *for* (convert, inform, rank, capture a lead).
- How it's built and served (static, SSR, client-only SPA) — this decides crawlability and performance lenses.
- What's a real fact vs. filler copy — you'll need this for the content lens.

## 2. Run each lens

Check every lens that applies. Each produces pass/fail observations, not opinions.

### Structure & semantics
Exactly one `<h1>` per page. Headings nest in order (no skipping levels for size). Landmark elements (`header`, `nav`, `main`, `footer`) present. Content is in semantic HTML, not a soup of `<div>`s. Required `<title>` and `<meta name="description">` present and page-specific.

### SEO
Unique, descriptive `<title>` and meta description per page. One canonical URL. `robots.txt` and an XML sitemap exist and are reachable. Headings describe content, not decoration. No orphan pages; internal links resolve.

### Accessibility
Every meaningful image has real alt text (decorative ones empty `alt=""`). Text/background contrast meets WCAG AA. Every interactive element is keyboard-reachable with a visible focus ring. Form inputs have associated labels. ARIA used only to fill real gaps, never to paper over bad markup.

### Performance
Images sized and lazy-loaded below the fold; no multi-MB hero. No render-blocking scripts in `<head>`. A stated budget for page weight and request count. Fonts don't block first paint. Measure, don't guess — pull real numbers (Lighthouse / web-vitals) where you can.

### Responsive layout
Renders cleanly at 375 / 768 / 1440 with zero horizontal overflow. Tap targets large enough on touch. Text reflows instead of being shrunk to unreadable. Nothing critical hidden only on small screens.

### Security
All dynamic content is escaped/sanitized — no raw HTML interpolation. No secrets, keys, or internal URLs in the served source. External links use `rel="noopener"`. Sensible security headers (CSP, X-Content-Type-Options) where the host allows.

### Content & anti-slop
Every factual claim — hours, prices, address, credentials, testimonials — traces to a real source. No invented specifics. No generic AI filler ("In today's fast-paced world…", "we pride ourselves on…", empty superlatives). Copy is specific to this business, not interchangeable with any competitor's.

### Structured data & shareability
JSON-LD present for the page's type (Organization, LocalBusiness, Product, FAQ…). Open Graph + Twitter card metadata so shares render a real preview. Canonical and OG URLs agree. (For the full machine-legibility pass — `llms.txt`, AI-crawler access, deep structured data — hand off to [`prep-site-for-ai`](../prep-site-for-ai/SKILL.md).)

### Link integrity
No dead internal links or broken anchors. External links resolve. Nav and footer point where they claim. Redirect chains kept short.

## 3. Grade and report

For each finding:

- **Lens** it came from.
- **Severity** — blocker (ship-stopping: broken a11y, invented facts, security leak) · major · minor · polish.
- **Location** — page + element/selector.
- **What's wrong and the fix** — concrete, not "improve SEO."

Lead with blockers. Separate "measured" findings (you ran a tool, saw the number) from "inspected" ones (you read the markup) so the reader knows what's proven. End with a one-line verdict: ship, fix-then-ship, or rebuild.

## The principle underneath

This skill mirrors the policy bank of a website *compiler*: SEO, a11y, performance, security, and content quality are guaranteed structurally rather than hoped for in a prompt. If you're building a system that produces sites — not just auditing one — see [`build-sites-as-specs`](../../code-engineering/build-sites-as-specs/SKILL.md), which turns this same checklist into enforceable policies the generator structurally cannot violate.
