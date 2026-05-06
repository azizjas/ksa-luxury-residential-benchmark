# Shape — Luxury Residential Ad Benchmark, v6 (12-month broad sweep)

## 1. Feature Summary

A single-page competitive-intelligence brief covering Saudi luxury residential paid social over the **last twelve months**. The methodology shifts from keyword-search-by-residence to **broad advertiser-page sweep**: every Diriyah-relevant Meta page is scrolled exhaustively, every ad in the 12-month window captured, then each ad bucketed manually to the residence(s) it promotes (text + image + landing-page URL signals). Prismax ads are excluded. Silent residences and silent brands are dropped — only what has ads is shown.

## 2. Primary User Action

A reader scans the brand-grouped matrix in 30 seconds — "How is Aman doing in KSA?" → one row across master plans. Then they drill into a master plan section, into a brand, into a residence, into ad creatives. Empty rows/sections do not exist; their absence is itself the signal.

## 3. Why v6 (methodology shift)

v5 read like an audit of named residences. v6 reads like a market census. Two changes:

- **Period extends to 12 months** (since 2025-05-06). Prior versions were 6 months.
- **Broad advertiser-page sweep, not keyword search.** Keyword search misses ads where the residence name lives only in the image. v6 scrolls every Diriyah-relevant page (developers, architecture firms, brokerages, marketplaces, hospitality operators) end-to-end and buckets each ad by image + copy + landing URL. Result: residences Aziz knew were running ads but were missing from v5 are now caught.

**Consequences:**
- No more "silent brands" or "silent residences" sections. Empty buckets are dropped silently.
- Prismax (page_id 259143187971) excluded entirely.
- Brand sub-sections survive only if at least one residence under them has at least one ad.
- The matrix now sorts by ad volume; brands with zero ads are absent.

## 4. Design Direction

**Color strategy:** unchanged — restrained warm-dark palette, single champagne-gold accent, OKLCH tokens.

**Theme scene sentence:** A Diriyah Marketing Director scans this on a 27-inch monitor at dusk, brand by brand. Bloomberg terminal page typeset by Wallpaper. Restrained, dense, every number earned, every variant visible.

**Anchor references:**
- *FT Markets data pages* for tabular density.
- *Bloomberg Terminal* for stat-grid economy.
- *Apple Newsroom press kits* for the gallery feel of variant carousels.
- *NB Studio / Pentagram editorial print* for the breathing typographic markers.

**Anti-references:** no narrative paragraphs, no version-delta framing, no SaaS gradient hero metrics, no glassmorphism, no Looker tile grids, no category-reflex aesthetics, no "v6" markers in body content.

## 5. Scope

- **Fidelity:** Production-ready.
- **Breadth:** One page; hero, advertiser-sweep matrix, master-plan sections (only those with hits), brand sub-sections (only those with hits), residence sub-sections (only those with hits), takeaways, methodology footnote.
- **Interactivity:** Carousel scroll-snap on every ad; click-to-enlarge lightbox; Esc / click-outside close.
- **Time intent:** Polished until it ships.

## 6. Layout Strategy — broad-sweep edition

### Hero
Editorial. Big DM Serif headline. Eyebrow above. One short deck paragraph that names the methodology shift in one breath. Below: 6-stat at-a-glance row (advertisers swept, advertisers active, residences with ads, ads captured, variant images, compile date).

### Advertiser sweep matrix
Centerpiece. Rows = advertisers, sorted by ad volume in the 12-month window. Columns = page name, kind (developer / broker / operator / etc.), ads, active ads, residences they advertised, variants. No silent rows.

### Master-plan sections
Only master plans with at least one bucketed ad. Each opens with eyebrow, single H2, one short blurb, four-stat strip (brands with ads, residences with ads, ads, variants). Then per-brand sub-sections.

### Brand sub-section
- H3 brand name + kind eyebrow + ad count.
- Brand blurb (max 60 words, sourced from operator/developer factsheet).
- 4-stat tile row (ads, active, variants, residences).
- "Library scope" line — which advertisers actually ran the ads.
- Indented brand-body containing residence sub-sections.

### Residence sub-section
- H4 residence name + blurb.
- 3-stat tile row (verified ads, active, variants).
- For each ad: metadata strip (advertiser, status, date range, platforms, variant count, library-id link), then horizontal scroll-snap carousel of variant images with `1/N` captions.
- 3-5 facts at the bottom of each residence.

### Carousel & lightbox
Unchanged from v5 — CSS scroll-snap horizontal strip, vanilla JS lightbox.

### Five takeaways
Five numbered items, max 15 words each. Lead with the methodology insight ("broad sweep surfaces N residences that keyword search missed").

### Methodology
`<details>` collapsible. Sources, sweep procedure, bucketing rules, scope, disclosed limitations, Prismax exclusion note.

## 7. Data plane

- `/tmp/lux_v6/sweep_<page>.json` — per-advertiser sweep results (every ad card scraped).
- `/tmp/lux_v6/_buckets.json` — bucketed result, per residence.
- `/tmp/lux_v4_shots/`, `/tmp/lux_v6_shots/` — variant images on disk.
- `/tmp/build_lux_v6.py` — embeds verified-only ads into a single self-contained HTML, base64-encoding all variant images. Brand and residence metadata is hard-coded; only buckets with non-empty ad lists render.

## 8. Key States

- **Default:** As described.
- **Print:** Warm cream + dark ink. Carousel becomes a wrap-flex grid. Page-break before each master plan section.
- **Reduced motion:** Hover scale + lightbox fade disabled.
- **Mobile (390px):** Stat tiles re-flow. Carousel items span 78vw. Matrix horizontally scrollable.

## 9. Interaction Model

- **Scroll-snap carousel.** `scroll-snap-type: x mandatory` on the strip, `scroll-snap-align: center` on each item.
- **Click to enlarge.** Each variant is a button; click opens the lightbox with full-res image.
- **Lightbox close.** Esc, click-outside, or Close button.
- **Reduced motion.** Transitions drop to 0ms.

## 10. Confirmation

```
IMPECCABLE_PREFLIGHT: context=pass product=pass command_reference=pass shape=pass image_gate=skipped:no_external_mocks_needed mutation=open
```
