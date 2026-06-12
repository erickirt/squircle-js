# Flagship Blog Post: Squircles in CSS — Design Spec

**Date:** 2026-06-12
**Status:** Approved (design), pending implementation plan
**Type:** SEO content / new blog post (no changes to existing content)

## Goal

Add one new flagship blog post to `apps/web/content/blog/` that captures the
*trending* CSS `corner-shape` / `superellipse()` / browser-support query cluster
surfaced in Google Search Console. The post must consolidate that intent on a
single authoritative, kept-current URL — not a multi-post cluster.

**Hard constraint:** Do not modify any existing blog post. Existing content is
performing and must be left untouched. No edits to existing files are permitted;
new internal links live in the new post only.

## Why this topic (data justification)

GSC export (`2026-06-12`) shows a small-but-rising cluster of feature-specific
CSS queries that the existing content does not own:

- "css corner-shape squircle browser support" (+ 2025 / 2026 variants)
- "firefox corner-shape"
- "css superellipse", "css squircle" (215 impr), "squircle shape css"
- "ios corner smoothing css", "corner smoothing css", "apple border radius css"
- "css corner-shape squircle browser support 2026"

These are status-checking / how-to intents for a brand-new CSS feature —
distinct from the generic "how do I do squircles today" intent already served by
the `squircles-in-web-design` winner.

## Cannibalization guardrail

The existing **`squircles-in-web-design`** post (91 clicks, pos ~7.5) already
targets `squircle css`, `corner smoothing css`, `css superellipse` and frames
"why CSS border-radius can't → use squircle-js". To avoid cannibalizing a winner:

- The new post does **not** re-target the generic "squircle css" head term.
- The new post owns the **feature-specific and browser-support** terms
  (`corner-shape`, `superellipse()`, support-by-year, `firefox corner-shape`).
- The two posts **interlink** to reinforce the cluster around existing winners.

## Post specification

- **Title / H1:** "Squircles in CSS: `corner-shape`, `superellipse()` and Browser Support (2026)"
- **Slug:** `squircles-in-css`
- **Date (frontmatter):** `2026-06-12`
- **Meta description:** "Can you make a squircle in pure CSS yet? A practical
  guide to the new `corner-shape` property and `superellipse()` value, current
  browser support in 2026, and how to ship smooth corners everywhere today."
- **keywords (frontmatter array):**
  `["css corner-shape", "corner-shape squircle", "corner-shape browser support",
  "firefox corner-shape", "superellipse css", "ios corner smoothing css",
  "squircle css browser support 2026"]`

### Frontmatter format (match existing posts)

```
---
title: "..."
description: "..."
date: "2026-06-12"
keywords: ["...", "..."]
slug: "squircles-in-css"
---
```

### Outline (H2 sections → intent captured)

1. **What `corner-shape` is (the new CSS property)** — "css corner-shape",
   "corner-shape css property".
2. **Making a squircle with `corner-shape: superellipse()` — how-to + code** —
   "how to make a squircle in css", "superellipse() css".
3. **Browser support in 2026 (Chrome / Safari / Firefox table)** —
   "corner-shape browser support 2025/2026", "firefox corner-shape".
4. **iOS-style corner smoothing in CSS** — "ios corner smoothing css",
   "apple border radius css".
5. **The fallback: smooth corners in every browser today → `@squircle-js`** —
   honest library tie-in (fallback *until* support is universal, not "better
   than CSS").
6. **Quick reference / FAQ** — long-tail ("can you do squircles in css", etc.).

### Live demos (existing MDX components)

- A `<SquircleComparison>` near the top: border-radius vs corner-shape vs
  squircle-js.
- A `<SquircleDemo>` (or `<Squircle>`) inside the how-to section.

### Internal links (new → existing only)

- Link to `squircles-in-web-design` ("why border-radius can't make squircles").
- Link to `what-is-a-squircle` ("what the shape actually is").
- No edits to those files; links are added only within the new post.

## Implementation guardrails

1. **Verify browser-support facts live at write time.** Author knowledge cutoff
   is Jan 2026; it is now June 2026, so `corner-shape` shipping status in
   Chrome / Safari / Firefox may have changed. The implementation plan MUST
   include a fresh `WebSearch` / `WebFetch` check (caniuse, MDN, browser release
   notes) before writing the support table. No guessed support data.
2. **Honest library framing.** Position `@squircle-js` as the cross-browser
   fallback until `corner-shape` is universally supported — accurate and
   ages well.
3. **Match house style.** ~6–7 H2 sections, explanatory prose like
   `squircles-in-apple-design` / `squircles-in-web-design`; use backticked code
   for CSS properties; real, runnable CSS snippets.

## Out of scope

- Editing or "refreshing" any existing post.
- A second/third satellite post (may be spun out *later* based on which H2
  sections earn impressions — explicitly a future, data-driven decision).
- Any changes to the library code, blog routing, or MDX component set.

## Success criteria

- One new MDX file `apps/web/content/blog/squircles-in-css.mdx` that builds,
  renders, and lints clean.
- Accurate 2026 browser-support table (verified, not guessed).
- No existing post modified.
- Internal links resolve; demos render.
