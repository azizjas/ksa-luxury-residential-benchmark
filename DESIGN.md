# Design

## Theme & Atmosphere

A senior Diriyah strategist reads this on a 27-inch monitor in a hushed top-floor office at dusk, with the desk lamp on and the city lights coming up outside. The dominant theme is **dark, but warm**: a deep midnight-stone background with cream ink and a single champagne-gold accent. It is editorial more than corporate, expensive more than expensive-looking, and Najdi-aware without being heritage-cosplay. There is exactly one signature ornament (a folded geometric divider) used between major sections; everything else carries weight through type, space, and color contrast alone.

## Color strategy

**Restrained.** Tinted neutrals carry roughly 90% of the surface. Champagne gold is the only chromatic accent, used for the eyebrow rules, drop caps, active TOC dot, hover state on Meta library links, the geometric divider, and the print-watermark logotype. Never used on body text, never used as a button background. All colors specified in OKLCH; legacy hex provided alongside for tooling that does not yet support OKLCH.

| Token | OKLCH | Hex | Role |
|---|---|---|---|
| `--ink` | `oklch(94% 0.018 75)` | `#F4EDE0` | Primary text, headings, drop cap on dark sections |
| `--ink-soft` | `oklch(78% 0.014 75)` | `#C9BEA6` | Secondary text, captions, dates |
| `--ink-mute` | `oklch(58% 0.010 75)` | `#8E8576` | Eyebrows, label small caps, library-id links |
| `--bedrock` | `oklch(13% 0.008 60)` | `#0E0D0C` | Page background, "midnight stone" |
| `--ground` | `oklch(17% 0.010 60)` | `#1A1815` | First-elevation surfaces, sticky TOC, table rows alt |
| `--sand` | `oklch(20% 0.012 60)` | `#211E18` | Card surface, "warm sand" |
| `--rule` | `oklch(28% 0.012 60)` | `#332E25` | Hairlines, card borders, divider strokes |
| `--gold` | `oklch(76% 0.115 80)` | `#D4A857` | The single accent. Eyebrows, drop cap, active TOC |
| `--gold-soft` | `oklch(64% 0.090 80)` | `#A88240` | Hover state, secondary accent rule |
| `--print-bg` | `oklch(96% 0.008 75)` | `#F2EEE5` | Print stylesheet body, "warm cream" |
| `--print-ink` | `oklch(20% 0.012 60)` | `#211E18` | Print stylesheet body text |

## Typography

Two-family system. Heading serif is **DM Serif Display** for major H1 / H2 and the section drop cap, paired with **Inter** for body, captions, and UI. **Cormorant Small Caps** carries eyebrows and small-caps labels; tabular variant of Inter handles in-table numerals.

- `font-family-display: "DM Serif Display", "Big Caslon", "Hoefler Text", Georgia, serif;`
- `font-family-body: "Inter", -apple-system, "Segoe UI", system-ui, sans-serif;`
- `font-family-eyebrow: "Cormorant Garamond", "EB Garamond", serif;` with `font-variant-caps: all-small-caps; letter-spacing: 0.18em;`
- Numbers in tables and matrix cells use `font-variant-numeric: tabular-nums lining-nums;`

### Modular scale (base 17px, ratio 1.333 perfect fourth)

| Step | Size | Use |
|---|---|---|
| `--type-xs` | 12px / 1.4 | Library IDs, dates, tag chips |
| `--type-sm` | 14px / 1.5 | Eyebrows in caps, table cells, captions |
| `--type-base` | 17px / 1.65 | Body paragraphs |
| `--type-lg` | 22px / 1.45 | Lead paragraph, intro text |
| `--type-xl` | 30px / 1.3 | H3 cluster title |
| `--type-2xl` | clamp(40px, 4.6vw, 60px) / 1.1 | H2 section title |
| `--type-3xl` | clamp(58px, 7.5vw, 110px) / 1.0 | H1 hero |
| `--type-drop` | 96px / 0.9 | Section drop cap |

Body measure capped at 68ch. Heading measure capped at 22ch. `text-wrap: balance` on H1/H2/H3, `text-wrap: pretty` on long-form paragraphs.

## Spacing scale

Powers of-ish 8 with a minor step at 4 and 12:

`--space-1: 4px`, `--space-2: 8px`, `--space-3: 12px`, `--space-4: 16px`, `--space-5: 24px`, `--space-6: 32px`, `--space-7: 48px`, `--space-8: 64px`, `--space-9: 96px`, `--space-10: 128px`.

Section spacing leans on `--space-9` and `--space-10`. Card internal padding is `--space-5` to `--space-6`. Gaps inside the comparison matrix are `--space-3` vertical, `--space-5` horizontal.

## Elevation

Minimal. Surfaces separate by tone-shift, not by shadow:

- Card: 1px hairline border in `--rule`, no shadow
- Sticky TOC: `--ground` background, no shadow
- Hover lift on cards: scale `--rule` border to `--gold-soft`, transition 240ms ease-out-quart, no movement, no shadow
- Print: cards are 0.6pt rule on warm cream, never shaded fills

## Heritage motif

A single geometric divider between top-level sections, drawn in inline SVG, stroked at `--gold` 1.5px on dark and `--gold-soft` 1px on print. The motif is a folded eight-point Najdi star reduced to its outer envelope and a horizontal rule, 80px wide × 16px tall, never repeated more than once per section break. Do not use it as a watermark, do not use it inside cards, do not animate it.

## Components

### Eyebrow

Small-caps Cormorant, 12px, letter-spacing 0.22em, color `--gold`, paired with a 16px gold horizontal hairline above. Lives above every H2 and on each card meta row.

### Drop-cap section opener

The first paragraph of each major section uses `::first-letter` styled with DM Serif Display at 96px, color `--gold`, float left, line-height 0.85, 4px right margin. Only on the first paragraph of the section, never on subsequent paragraphs.

### Ad creative card

Image at top, no rounding. Caption block below with `--space-5` padding. Caption layout: advertiser (Inter 600 weight, `--ink`) and status pill (filled in `--ground`, text in `--gold` for active, `--ink-mute` for inactive) on one row; project name in `--ink` 17px serif; dates in `--ink-mute` small caps; theme paragraph in `--ink-soft` 14px / 1.6; tag chip and library-id link on the foot row. Hover: border shifts to `--gold-soft`. Image is `aspect-ratio: 1 / 1` with `object-fit: cover`, `loading: lazy`.

### Comparison-matrix cell

Real designed component, not a generic table. Each developer row has: a left rail with the developer name in serif and the project-line in eyebrow caps, then six platform cells (Meta, Google, TikTok, X, LinkedIn, Snap) on a 12-column grid. Each cell shows count in tabular figures, format chips below, and a status dot (gold = active, mute = inactive, hairline = no data). Cells without data show a single em-rule glyph in `--ink-mute`. Header row has an eyebrow above each platform name.

### Sticky TOC

Right-aligned column on desktop wider than 1100px, floats inside the page gutter. Each entry is a small-caps eyebrow plus a 16px hairline that fills `--gold` when the section is in view. Mobile collapses to a top horizontal scroller with the same dot-fill pattern.

### Tag chip

Outline only, no fill. 1px `--rule` border, 2px corner radius, 11px Inter caps, 0.16em letter-spacing, padding `--space-1 --space-2`. Color `--ink-mute`.

## Motion

- TOC active dot fills via `width` transition? No: width is a layout property. Use `transform: scaleX()` with `transform-origin: left` and `transition: transform 280ms cubic-bezier(0.22, 1, 0.36, 1)` (ease-out-quart).
- Card hover border transition 240ms ease-out-quart on `border-color` only.
- Section reveal: opacity 0 → 1 over 600ms ease-out-quart, IntersectionObserver-driven, threshold 0.1. Disabled under `prefers-reduced-motion: reduce`.
- No bounce, no elastic, no stagger choreography on scroll.

## Print stylesheet

`@media print`: body becomes `--print-bg`, ink becomes `--print-ink`, accent stays `--gold` but slightly desaturated to `--gold-soft`. Sticky TOC and hover effects are hidden. Each major section starts on a new page with `break-before: page` (except section 1). Cards drop their hairline border to 0.6pt; image inside cards keeps `print-color-adjust: exact`. The Najdi divider stays. Page numbers in the footer in eyebrow caps. Page margin 16mm.
