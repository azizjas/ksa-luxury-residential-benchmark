# Shape — Luxury Residential Ad Benchmark, v4 (per-residence)

## 1. Feature Summary

A single-page competitive-intelligence brief covering Saudi luxury residential paid social, restructured **by residence project**. Each residence is mapped to its real advertisers, every captured ad shows every variant in a horizontal scroll-snap carousel with click-to-enlarge lightbox, and pages with no detectable Meta presence are reported as such (absence is signal too).

## 2. Primary User Action

A reader scans the per-residence matrix in 30 seconds, then drills into a master plan section to review the actual creatives running. The carousel lets them flip through every variant of an ad in place; the lightbox exposes full-resolution detail without leaving the page.

## 3. Why v4 (structural shift)

v3 read like an advertiser report. v4 reads like a residence inventory:

- Restructured the entire spine: master plans → residences → ads → variants.
- Every LID was re-verified against its Meta Ad Library detail page; ads belonging to keyword-leak pages (drama apps, news outlets, sponsorship awards) were dropped.
- Each ad now exposes Meta's "this ad has multiple versions" indicator where present.
- Each ad renders a CSS scroll-snap carousel of its captured variant images, with vanilla JS lightbox.
- Residences with no verified Meta paid presence are listed explicitly — silence is reported.
- All v2 / v3 delta framing is stripped. Numbers stand on their own.

## 4. Design Direction

**Color strategy:** unchanged — restrained warm-dark palette, single champagne-gold accent, OKLCH tokens.

**Theme scene sentence:** A Diriyah Marketing Director scans this on a 27-inch monitor at dusk, drilling residence by residence. The page should feel like a Bloomberg terminal page typeset by Wallpaper — restrained, dense, every number earned, every variant visible.

**Anchor references:**
- *FT Markets data pages* for tabular density and tabular-numeral discipline.
- *Bloomberg Terminal* for stat-grid economy.
- *Apple Newsroom press kits* for the gallery feel of variant carousels.
- *NB Studio / Pentagram editorial print* for the shift between dense data zones and breathing typographic markers.

**Anti-references reinforced:** No narrative paragraphs. No "v3 reported" framing. No SaaS gradient hero metrics. No glassmorphism. No Looker tile grids. No category-reflex aesthetics.

## 5. Scope

- **Fidelity:** Production-ready.
- **Breadth:** One page; hero, per-residence matrix, seven master-plan sections, five takeaways, methodology footnote.
- **Interactivity:** Carousel scroll-snap on every ad; click-to-enlarge lightbox; Esc / click-outside close.
- **Time intent:** Polished until it ships.

## 6. Layout Strategy — per-residence redesign

### Hero
Editorial. Big DM Serif headline, eyebrow above, one short deck paragraph. Below: 5-stat at-a-glance row (residences inventoried, with verified ads, ads captured, variant images, capture date).

### Per-residence matrix
Centerpiece. Rows = residences with verified ads. Columns = total ads, active, inactive, variants, advertisers, who's pushing in SA. Every cell is a tabular figure.

### Master-plan sections (seven of them)
Each opens with eyebrow, single-line H2, one short blurb, three-stat strip (ads, variants, residences). Then per-residence sub-sections:

- Residence name as h3 + blurb.
- 4-stat tile row (ads, active, variants, advertisers).
- "Library scope" line: page-scoped banner from the verified advertiser page.
- For each ad: a metadata strip (advertiser, status, tag, date, platforms, variant indicator, library-id link), then a horizontal scroll-snap carousel of variant images with `1/N` / `2/N` captions.
- 3-5 facts at the bottom of each residence, max 12 words each.

### Carousel
CSS scroll-snap horizontal strip. Each item is a square `aspect-ratio: 1/1` card with a button that opens the lightbox. On mobile, full-bleed item width. On desktop, 3-4 visible at once.

### Lightbox
Full-screen background overlay. Esc + click-outside + Close button all dismiss. No animation libraries — vanilla JS.

### Five takeaways
Five numbered items, max 15 words each. Replaces v3's "what this means".

### Methodology
`<details>` collapsible. Source rules, scope, disclosed limitations.

## 7. Data plane

`/tmp/lux_v4/_residence_search_results.json` — per-residence Meta Ad Library banner counts.
`/tmp/lux_v4/_variants.json` — per-LID detail-page scrape with explicit version count.
`/tmp/lux_shots/*.png` — variant images on disk.
The build script (`/tmp/build_lux_v4.py`) embeds verified-only ads into a single self-contained HTML, base64-encoding all variant images.

## 8. Key States

- **Default:** As described.
- **Print:** Warm cream + dark ink. Carousel becomes a wrap-flex grid. Page-break before each master plan section.
- **Reduced motion:** Hover scale + lightbox fade disabled.
- **Mobile (390px):** Stat tiles stack 2-up. Carousel items span 78vw. Matrix horizontally scrollable.

## 9. Interaction Model

- **Scroll-snap carousel.** `scroll-snap-type: x mandatory` on the strip, `scroll-snap-align: center` on each item.
- **Click to enlarge.** Each variant is a button; click opens the lightbox with full-res image.
- **Lightbox close.** Esc, click-outside, or Close button.
- **Reduced motion.** Transitions drop to 0ms.

## 10. Confirmation

```
IMPECCABLE_PREFLIGHT: context=pass product=pass command_reference=pass shape=pass image_gate=skipped:no_external_mocks_needed mutation=open
```
