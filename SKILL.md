---
name: skill-design-system-flat
description: Apply the instyle.group flat design system — opaque warm-neutral surface tones (white → #F3F1EE → #E6E2D7 → #E1DCD0 → #35362D) with separation done by background-color steps, NOT borders or shadows. 8px grid spacing, Lato + Noto Sans JP typography, Major Third 1.25 modular type scale on a 14px base, and superellipse corner-shape. Use this when the user asks for "flat"/"フラット"/"ミニマル"/"contrast-based" UI, when they want the instyle.group look without translucency or backdrop blur, when a project's CLAUDE.md declares this design system, or when generating dashboards, reports, slides, or landing pages that should feel quiet and editorial rather than glassy.
---

# instyle.group Flat Design System

This skill makes Claude generate UIs in the instyle.group **flat** style —
warm neutral palette where regions are distinguished by **background-color
contrast**, never by borders or drop shadows.

> Sister skill: `skill-design-system-liquid` for the translucent / glassy
> variant of the same brand. They are mutually exclusive — pick the one the
> user asks for, never mix tokens.

---

## Quick rules — must follow in every output

### 1. Contrast through surface tone, never borders

The single most important rule. Stack regions by stepping along:
`--color-bg` (white) → `--color-surface` → `--color-surface-2` →
`--color-surface-3` → `--color-text` (darkest).

Do **not** use `border: 1px solid var(--color-border)` for structural
separation. If you find yourself reaching for a hairline, choose a different
surface tone instead. Borders are reserved for the rare case where contrast
genuinely fails (e.g. on a print-style detail block).

### 2. No drop shadows on cards

Cards lift off the page **because their surface is darker than the page**.
A `box-shadow: 0 2px 8px rgba(0,0,0,.08)` is a flat-system smell — delete it.

### 3. Typography

- `--font-sans: 'Lato', 'Noto Sans JP', sans-serif` — Lato for Latin, Noto
  Sans JP for Japanese, in that order.
- Modular type scale **Major Third (1.25) on a 14px base** (Display 43 /
  H1 34 / H2 27 / H3 22 / H4 18 / Body 14 / Small 11 / Caption 9).
- Min font-size 11px. Caption 9px is for chart axis labels only.
- Heading hierarchy is at most 3 levels (typically H2 → H3 → Body).
- Serif (`Shippori Mincho`) is **opt-in only**. Do not use it unless the
  user explicitly says "明朝" / "serif" / "editorial". For eyebrow labels
  and step numbers, use the tracked-sans `.eyebrow` style.

### 4. Color usage

- Hex codes are forbidden in component CSS. Use `--color-*` tokens.
- Same-screen accent diversity: at most **two accent colors** in use at once.
- `--color-accent` is for label / tag backgrounds; `--color-accent-dark`
  is for sidebar / strong panel backgrounds. Don't blanket-fill content
  blocks with accent.

### 5. Radius — superellipse, not circular

- Apply `corner-shape: var(--corner-shape)` (= `superellipse(2.5)`) to
  every element via `*` selector. Tokens.css does this for you.
- Sizes: `--r-sm: 8px` / `--r: 12px` / `--r-lg: 20px` / `--r-xl: 28px`
  / `--r-pill: 999px`.
- Pills are stadium-shaped — `corner-shape` has no effect there, that's fine.

### 6. Highlight color `#E2DD2A`

**Inline text marker only.** Use it through `<mark>` or `.mark`. Never use
it for CTA fills, badges, icon backgrounds, sidebar tints, or panel
washes. 2–3 uses per page maximum.

### 7. Spacing & motion

- 8px grid: `4 / 8 / 12 / 16 / 24 / 32 / 48 / 64 / 96`.
- Generous whitespace is part of the brand voice.
- Transitions: `150ms` for hover, `250ms` for expand/transition. Easing
  `cubic-bezier(0.4, 0, 0.2, 1)`.

---

## Files in this skill

| Path | Purpose |
|------|---------|
| `rules/tokens.css`          | Full CSS variable set. **Copy into the project.** |
| `rules/snippets.css`        | Component snippets (card, panel, btn, input, type scale). |
| `rules/design.md`           | Full spec. Read this when the quick rules are not enough. |
| `rules/claude-md-template.md` | Template for the project's own `CLAUDE.md`. |
| `assets/ig_logo_2026.svg`   | instyle.group logo (use at height ~14px in headers). |
| `assets/ig_favicon_2026.png`| Favicon. |
| `assets/ig_ogp_2026-100.jpg`| OGP image (1200×630). |
| `examples/preview.html`     | Reference implementation. Open in a browser to see the target. |

---

## Bootstrap a new project (5 steps)

1. Copy `rules/claude-md-template.md` to the project root as `CLAUDE.md`,
   replace the `[...]` placeholders with project specifics.
2. Copy `rules/tokens.css` and `rules/snippets.css` into the project's
   stylesheet folder, import them before any component CSS.
3. Set the page background to `--color-bg` (white) and use cards with
   `--color-surface` to lift content off it.
4. Load Google Fonts in `<head>`:
   ```html
   <link rel="preconnect" href="https://fonts.googleapis.com">
   <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
   <link href="https://fonts.googleapis.com/css2?family=Lato:wght@100;300;400;700&family=Noto+Sans+JP:wght@400;500;700&family=Shippori+Mincho:wght@400;500;600;700;800&display=swap" rel="stylesheet">
   ```
5. Drop in the brand favicon/logo from `assets/` if the project carries the
   instyle.group identity.

---

## When you need full detail

`rules/design.md` is the authoritative specification. Read it when you need:

- Color rationale and contrast tables
- Component variations (nav, table, chart, form, sidebar)
- Layout / grid / breakpoint patterns
- Motion patterns and edge cases
- Accessibility specifics

---

## Common mistakes to avoid

- ❌ Using `border: 1px solid` for structural separation
- ❌ Adding `box-shadow` to cards "for depth"
- ❌ Filling panels or CTAs with `#E2DD2A`
- ❌ Stacking 3+ accent colors on one screen
- ❌ Using Shippori Mincho without explicit user opt-in
- ❌ Hardcoding hex colors instead of tokens
- ❌ Round-arc `border-radius` only — must pair with `corner-shape`
- ❌ More than 3 heading levels in one view

---

*Skill version 1.0 · instyle.group Creative Team*
