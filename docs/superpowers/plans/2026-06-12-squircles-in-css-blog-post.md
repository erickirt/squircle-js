# Squircles in CSS Flagship Blog Post — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Publish one new MDX blog post, `apps/web/content/blog/squircles-in-css.mdx`, that captures the trending CSS `corner-shape` / `superellipse()` / browser-support query cluster, without modifying any existing post.

**Architecture:** The blog is file-driven. Dropping a new `.mdx` file into `apps/web/content/blog/` auto-registers it everywhere — the blog index (`getAllContent("blog")`), the `[slug]` route, `sitemap.ts`, and per-post `generateMetadata`. No code wiring is needed. The post body is MDX rendered by `mdxComponents`; the H1 title and date come from frontmatter (the body must NOT include its own `# H1`). Live demo components available in MDX are `<SquircleComparison />` and `<SquircleDemo />` (both prop-less). Markdown tables are styled, so the browser-support table is plain Markdown.

**Tech Stack:** Next.js (App Router), MDX via `lib/mdx`, Biome/ultracite (`pnpm check`), Turbo. Spec: `docs/superpowers/specs/2026-06-12-squircles-in-css-flagship-post-design.md`.

---

## House-style reference (read before drafting)

Match these existing posts for tone, length, and structure:
- `apps/web/content/blog/squircles-in-web-design.mdx` (closest analogue — CSS-focused)
- `apps/web/content/blog/squircles-in-apple-design.mdx` (the top performer)

Conventions observed in those files:
- Body opens with 1–2 intro paragraphs, **no `# H1`** (frontmatter supplies it).
- 6–7 `## H2` sections, explanatory prose, ~600–1100 words total.
- CSS property/value names in backticks: `` `corner-shape` ``, `` `border-radius` ``.
- Fenced code blocks use a language tag (e.g. ` ```css `).
- A demo component is placed early (after the intro) — typically `<SquircleComparison />`.
- No internal links currently exist in posts; this post will add them (new file only).

**Constraint from spec:** Do NOT edit, "refresh," or touch any existing `.mdx` post. Internal links are added only inside the new file.

---

## File Structure

- **Create:** `apps/web/content/blog/squircles-in-css.mdx` — the entire deliverable.
- **Create (scratch, deleted before final commit):** `apps/web/content/blog/.corner-shape-research.md` — temporary notes from Task 1.
- **No other files are created or modified.**

---

## Task 1: Verify CSS `corner-shape` browser support (live research)

**Why:** Author knowledge cutoff is Jan 2026; today is 2026-06-12. `corner-shape` shipping status may have moved. The support table MUST be verified, not guessed.

**Files:**
- Create (temporary): `apps/web/content/blog/.corner-shape-research.md`

- [ ] **Step 1: Run web searches**

Use the `WebSearch` tool for each of these queries:
- `CSS corner-shape property browser support 2026`
- `corner-shape superellipse() CSS caniuse`
- `Firefox corner-shape support`
- `Safari corner-shape WebKit support`

- [ ] **Step 2: Fetch the authoritative sources**

Use `WebFetch` on the canonical references (whichever the searches surface):
- `https://developer.mozilla.org/en-US/docs/Web/CSS/corner-shape`
- `https://caniuse.com/mdn-css_properties_corner-shape`

Prompt each fetch for: "Which browsers (Chrome, Edge, Safari, Firefox) support `corner-shape` and the `superellipse()` value, from which version, and is it behind a flag?"

- [ ] **Step 3: Record verified facts**

Write `apps/web/content/blog/.corner-shape-research.md` capturing, per browser: name, supported-from version (or "not yet" / "behind flag"), and the date the fact was checked (2026-06-12). Include the source URLs. If sources conflict, note the conflict and prefer MDN/caniuse.

- [ ] **Step 4: Sanity gate**

If `corner-shape` turns out to be widely shipped across all major browsers, the post's framing still holds (it becomes "now supported — here's how, plus the fallback for older browsers"). If it is still largely unsupported, the framing is "coming soon — here's the status and what to use today." Note which framing applies at the top of the research file. Do not commit this scratch file.

---

## Task 2: Create the post with frontmatter, intro, and first demo

**Files:**
- Create: `apps/web/content/blog/squircles-in-css.mdx`

- [ ] **Step 1: Write the frontmatter and opening**

Create `apps/web/content/blog/squircles-in-css.mdx` with exactly this frontmatter, followed by two intro paragraphs and the comparison demo:

````mdx
---
title: "Squircles in CSS: corner-shape, superellipse() and Browser Support (2026)"
description: "Can you make a squircle in pure CSS yet? A practical guide to the new corner-shape property and superellipse() value, current browser support in 2026, and how to ship smooth corners everywhere today."
date: "2026-06-12"
keywords: ["css corner-shape", "corner-shape squircle", "corner-shape browser support", "firefox corner-shape", "superellipse css", "ios corner smoothing css", "squircle css browser support 2026"]
slug: "squircles-in-css"
---

For years, the honest answer to "can you make a squircle in pure CSS?" was no. `border-radius` produces rounded rectangles — circular arcs at the corners — not the continuously smooth curve of a true squircle. That gap is finally closing. CSS now has a `corner-shape` property and a `superellipse()` value designed to draw exactly this shape natively.

This guide covers what `corner-shape` is, how to draw a squircle with it, where browser support stands in 2026, and how to ship smooth corners in every browser today while support catches up.

<SquircleComparison />
````

- [ ] **Step 2: Verify the file parses (frontmatter + MDX)**

Run: `cd /Users/antoni/Projects/squircle-js && pnpm --filter web typecheck`
Expected: PASS (no type errors introduced; the content loader reads the new file).

- [ ] **Step 3: Commit the skeleton**

```bash
cd /Users/antoni/Projects/squircle-js
git add apps/web/content/blog/squircles-in-css.mdx
git commit -m "feat(blog): scaffold Squircles in CSS post (frontmatter + intro)"
```

---

## Task 3: Write Sections 1–2 (what `corner-shape` is + how-to)

**Files:**
- Modify: `apps/web/content/blog/squircles-in-css.mdx` (append after `<SquircleComparison />`)

- [ ] **Step 1: Append Section 1 — "What `corner-shape` Is"**

Append this section. Write 2–3 paragraphs covering: `corner-shape` is a new CSS property that controls the *shape* of a corner, working alongside `border-radius` (which controls the *size*); it accepts values like `round` (the default, today's behavior), `bevel`, `scoop`, `notch`, and `squircle`/`superellipse()`; it is the first native way to get a real superellipse corner in the browser. Use this heading and lead-in exactly, then continue the prose:

```mdx
## What `corner-shape` Is

`corner-shape` is a new CSS property that controls the *geometry* of a corner, while `border-radius` continues to control its *size*. Where `border-radius` alone always draws a circular or elliptical arc, `corner-shape` lets you tell the browser to draw a different curve in that same corner box.
```

(Continue with prose listing the values — `round`, `bevel`, `scoop`, `notch`, and the superellipse family — and explaining that `superellipse()` is what produces the iOS-style squircle.)

- [ ] **Step 2: Append Section 2 — "Making a Squircle with `corner-shape`"**

Append a how-to section with the heading below and a runnable CSS example. Write 1–2 paragraphs explaining that you combine a `border-radius` with `corner-shape: superellipse(...)`, and that the `superellipse()` parameter controls how aggressively the curve flattens (higher = squarer/smoother sides, closer to Apple's look):

````mdx
## Making a Squircle with `corner-shape`

To draw a squircle, pair a `border-radius` (the corner size) with `corner-shape` set to a superellipse (the corner curve):

```css
.squircle {
  border-radius: 24px;
  corner-shape: superellipse(2.5);
}
```

The number passed to `superellipse()` controls how square the sides become before they curve. Higher values flatten the sides and tighten the curve into the corner — closer to the shape Apple uses for iOS icons. `corner-shape: superellipse(infinity)` approaches a sharp rectangle; lower values approach a normal `round` corner.
````

> NOTE: Confirm the exact `superellipse()` argument semantics against the MDN page fetched in Task 1. If MDN documents a different parameter form (e.g. a keyword like `squircle` or a different numeric range), update the snippet and the explanatory sentence to match the verified syntax before committing. Do not ship unverified syntax.

- [ ] **Step 3: Lint the file**

Run: `cd /Users/antoni/Projects/squircle-js && pnpm check`
Expected: PASS (or auto-fixable; if it flags the MDX, run `pnpm fix` and re-run `pnpm check`).

- [ ] **Step 4: Commit**

```bash
cd /Users/antoni/Projects/squircle-js
git add apps/web/content/blog/squircles-in-css.mdx
git commit -m "feat(blog): add corner-shape explainer and how-to sections"
```

---

## Task 4: Write Section 3 (browser support table)

**Files:**
- Modify: `apps/web/content/blog/squircles-in-css.mdx`
- Read: `apps/web/content/blog/.corner-shape-research.md` (Task 1 output)

- [ ] **Step 1: Append the browser-support section using verified facts**

Append the heading below and a Markdown table populated **only** from the verified facts in `.corner-shape-research.md`. Do not invent versions. Use the exact structure; fill the cells from research:

```mdx
## Browser Support in 2026

`corner-shape` is a young feature, so support is the deciding factor in whether you can rely on it in production today. Here is where the major browsers stand as of June 2026:

| Browser | `corner-shape` support |
| --- | --- |
| Chrome / Edge | <from research> |
| Safari | <from research> |
| Firefox | <from research> |
```

Follow the table with 1–2 sentences interpreting it for the reader: if support is partial, say plainly that production use needs a fallback today; if broad, note that older browsers still need one. State the check date ("as of June 2026") so the freshness is explicit.

- [ ] **Step 2: Lint**

Run: `cd /Users/antoni/Projects/squircle-js && pnpm check`
Expected: PASS.

- [ ] **Step 3: Commit**

```bash
cd /Users/antoni/Projects/squircle-js
git add apps/web/content/blog/squircles-in-css.mdx
git commit -m "feat(blog): add verified 2026 corner-shape browser support table"
```

---

## Task 5: Write Sections 4–6 (iOS smoothing, fallback, FAQ) + demo + internal links

**Files:**
- Modify: `apps/web/content/blog/squircles-in-css.mdx`

- [ ] **Step 1: Append Section 4 — "iOS-style Corner Smoothing in CSS"**

Append the heading below; write 2 paragraphs. Explain that Apple's squircle is a specific superellipse (continuous "corner smoothing", the same idea exposed by Figma's smoothing slider), that `corner-shape: superellipse()` is the CSS lever that reproduces it, and roughly which value range lands near the iOS look. Link to the existing post for the deeper Apple story:

```mdx
## iOS-style Corner Smoothing in CSS

The squircle most people picture is Apple's — the shape of every iOS app icon. It is a superellipse with *continuous* corner smoothing, the same property Figma exposes as a "corner smoothing" slider. With `corner-shape: superellipse()`, CSS can finally target that exact look rather than approximating it.
```

In the prose, include this internal link inline: `[how Apple adopted the squircle](/blog/squircles-in-apple-design)`.

- [ ] **Step 2: Append Section 5 — "The Fallback: Smooth Corners in Every Browser Today"**

Append the heading below. Frame `@squircle-js` honestly as the cross-browser fallback **until** `corner-shape` is universal — not as superior to native CSS. Include the `<SquircleDemo />` component and one short install/usage snippet. Add the internal link to the web-design post:

````mdx
## The Fallback: Smooth Corners in Every Browser Today

Until `corner-shape` ships everywhere your users are, you still need a way to render squircles that works in every browser. That is what `@squircle-js/react` does: it generates an SVG clip-path for the exact superellipse and applies it as a CSS `clip-path`, so the shape is identical across browsers regardless of `corner-shape` support.

<SquircleDemo />

```bash
npm install @squircle-js/react
```

When `corner-shape` reaches full support, this same markup can be progressively enhanced — or replaced — with the native property. For the deeper background on why `border-radius` cannot do this and how the clip-path approach works, see [squircles in web design](/blog/squircles-in-web-design).
````

- [ ] **Step 3: Append Section 6 — "Frequently Asked Questions"**

Append a short FAQ using `### H3` sub-headings for each question, answering in 1–2 sentences each. Cover at least: "Can you make a squircle with pure CSS?", "What is `superellipse()` in CSS?", "Does Firefox support `corner-shape`?", "Is `corner-shape` the same as `border-radius`?". Keep answers consistent with the verified support table. Example shape:

```mdx
## Frequently Asked Questions

### Can you make a squircle with pure CSS?

<1–2 sentence answer consistent with the support table above.>

### What is `superellipse()` in CSS?

<1–2 sentence answer.>
```

- [ ] **Step 4: Lint**

Run: `cd /Users/antoni/Projects/squircle-js && pnpm check`
Expected: PASS (run `pnpm fix` then re-check if needed).

- [ ] **Step 5: Commit**

```bash
cd /Users/antoni/Projects/squircle-js
git add apps/web/content/blog/squircles-in-css.mdx
git commit -m "feat(blog): add iOS smoothing, library fallback, and FAQ sections"
```

---

## Task 6: Verify build, render, and constraints

**Files:**
- No source changes (verification + cleanup only)

- [ ] **Step 1: Typecheck and lint clean**

Run: `cd /Users/antoni/Projects/squircle-js && pnpm check && pnpm --filter web typecheck`
Expected: both PASS.

- [ ] **Step 2: Build the web app**

Run: `cd /Users/antoni/Projects/squircle-js && pnpm --filter web build`
Expected: PASS; build output lists the statically generated `/blog/squircles-in-css` route (from `generateStaticParams`).

- [ ] **Step 3: Clean up orphaned build workers** (per CLAUDE.md)

Run: `pkill -9 -f "jest-worker/processChild" || true`

- [ ] **Step 4: Visual check in the browser**

Run: `cd /Users/antoni/Projects/squircle-js && pnpm --filter web dev` (background), then open `http://localhost:3000/blog/squircles-in-css`.
Confirm: title and date render in the header; both `<SquircleComparison />` and `<SquircleDemo />` render real squircles; the support table renders; both internal links (`/blog/squircles-in-apple-design`, `/blog/squircles-in-web-design`) resolve. Also open `http://localhost:3000/blog` and confirm the new post appears at the top of the list (newest date). Stop the dev server when done.

- [ ] **Step 5: Confirm no existing post was modified**

Run: `cd /Users/antoni/Projects/squircle-js && git diff --name-only main -- apps/web/content/blog/`
Expected: the ONLY listed file is `apps/web/content/blog/squircles-in-css.mdx`. If any other blog `.mdx` appears, revert that change.

- [ ] **Step 6: Remove the scratch research file**

Run: `cd /Users/antoni/Projects/squircle-js && rm -f apps/web/content/blog/.corner-shape-research.md && git status --porcelain apps/web/content/blog/`
Expected: only `squircles-in-css.mdx` shows as added/committed; the dotfile is gone and was never committed.

---

## Task 7: Final review and wrap-up

- [ ] **Step 1: Read the finished post end-to-end**

Read `apps/web/content/blog/squircles-in-css.mdx` in full. Check: no `# H1` in the body; backticked CSS property names; the support table matches the research; the library framing is "fallback until native," not "better than native"; both internal links present; word count roughly 700–1100 to match house style.

- [ ] **Step 2: Confirm clean tree and branch**

Run: `cd /Users/antoni/Projects/squircle-js && git status && git log --oneline main..HEAD`
Expected: clean working tree; commits for the post are on branch `blog/squircles-in-css`.

- [ ] **Step 3: Report and hand off for integration**

Summarize what was published and stop. Do NOT push or merge automatically — per the user's workflow, they merge feature branches locally and push to main. Offer to run the finishing-a-development-branch flow if they want help integrating.

---

## Self-Review (completed by plan author)

**Spec coverage:**
- Post spec (title/slug/date/description/keywords) → Task 2, Step 1 (exact frontmatter). ✓
- Outline sections 1–6 → Tasks 3, 4, 5 (each H2 mapped). ✓
- Cannibalization guardrail (don't re-target generic "squircle css") → keywords in Task 2 omit the generic head term; covered. ✓
- Live demos (`<SquircleComparison />`, `<SquircleDemo />`) → Task 2 Step 1 and Task 5 Step 2. ✓
- Internal links (new → existing only) → Task 5 Steps 1–2; verified by Task 6 Step 5. ✓
- Guardrail 1 (verify browser support live) → Task 1 (dedicated). ✓
- Guardrail 2 (honest library framing) → Task 5 Step 2 + Task 7 Step 1 check. ✓
- Guardrail 3 (house style) → House-style reference section + Task 7 Step 1. ✓
- Hard constraint (no existing post edited) → Task 6 Step 5 (git diff gate). ✓
- Success criteria (builds, renders, lints, accurate table, no existing post touched) → Task 6. ✓

**Placeholder scan:** The only intentional "fill from research" cells are in Task 4's table and are explicitly sourced from Task 1's verified output — this is required because the data is live, not a placeholder for undefined logic. Prose sections give exact headings/lead-ins plus explicit content requirements rather than full ghostwritten paragraphs, appropriate for content work.

**Type/name consistency:** Component names (`SquircleComparison`, `SquircleDemo`) match the registry in `components/mdx/mdx-components.tsx`. Slug (`squircles-in-css`), package filter (`web`), and commands (`pnpm check`, `pnpm --filter web typecheck`/`build`/`dev`) match the repo. ✓
