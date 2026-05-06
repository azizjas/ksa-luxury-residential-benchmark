# Shape — Luxury Residential Ad Benchmark, v5 (brand-first)

## 1. Feature Summary

A single-page competitive-intelligence brief covering Saudi luxury residential paid social, restructured **brand-first**. Each master plan groups its brands; each brand expands into its residences and verified ad creatives. Silent brands — those without detectable Meta presence — are listed at the bottom of each master plan, because absence is signal.

## 2. Primary User Action

A reader scans the brand-grouped matrix in 30 seconds — "How is Aman doing in KSA?" → one row across all master plans. Then they drill into a master plan section to see the brands that anchor it. Inside each brand, residences expand, then ads, then variants in scroll-snap carousels with click-to-enlarge lightbox.

## 3. Why v5 (structural shift)

v4 read like a residence inventory. v5 reads like a brand audit:

- Top level under each master plan = **brand bucket**, not residence.
- A brand can be: hospitality operator (Aman, Armani, Miraval...), starchitect / fashion-house lifestyle brand (Elie Saab), standalone luxury project brand (Nammos), broker brand (Christie's), architecture firm (Dar Al Omran), or developer brand where no operator anchors (DarGlobal Rayana, Diriyah Company own creative).
- Each brand carries its residences as nested sub-sections (DarGlobal → Amara at Rayana + Rayana Mansions; Elie Saab → Sedra Branded Villas + Etoile by Elie Saab).
- Silent brands appear in their own strip at the bottom of each master plan with one-line absence notes.
- Matrix rows = brands grouped by master plan, with a signal column (loud / quiet / silent) so the reader can scan competitive density at a glance.
- All v2 / v3 / v4 delta framing is stripped. Numbers stand on their own. The compile date appears as "Compiled 2026-05-06", not as a version marker.

## 4. Design Direction

**Color strategy:** unchanged — restrained warm-dark palette, single champagne-gold accent, OKLCH tokens. Silent brands desaturate to ink-mute / ink-veryfaint to visually quiet them.

**Theme scene sentence:** A Diriyah Marketing Director scans this on a 27-inch monitor at dusk, brand by brand. The page should feel like a Bloomberg terminal page typeset by Wallpaper — restrained, dense, every number earned, every variant visible.

**Anchor references:**
- *FT Markets data pages* for tabular density and tabular-numeral discipline.
- *Bloomberg Terminal* for stat-grid economy.
- *Apple Newsroom press kits* for the gallery feel of variant carousels.
- *NB Studio / Pentagram editorial print* for the shift between dense data zones and breathing typographic markers.

**Anti-references reinforced:** No narrative paragraphs. No version-delta framing. No SaaS gradient hero metrics. No glassmorphism. No Looker tile grids. No category-reflex aesthetics.

## 5. Scope

- **Fidelity:** Production-ready.
- **Breadth:** One page; hero, brand-grouped matrix, seven master-plan sections (each containing brand sub-sections + silent-brands strip), five takeaways, methodology footnote.
- **Interactivity:** Carousel scroll-snap on every ad; click-to-enlarge lightbox; Esc / click-outside close.
- **Time intent:** Polished until it ships.

## 6. Layout Strategy — brand-first redesign

### Hero
Editorial. Big DM Serif headline ("Bundle the brands. Then break down the residences."), eyebrow above, one short deck paragraph. Below: 6-stat at-a-glance row (brands inventoried, active, silent, ads captured, variant images, compile date).

### Brand-grouped matrix
Centerpiece. Rows = brands grouped by master plan; sorted within each master plan as loud → quiet → silent. Columns = master plan, brand (with kind subline), residences under brand, ads, active, variants, who's pushing in SA, signal pill. Silent rows desaturate.

### Master-plan sections (seven of them)
Each opens with eyebrow, single-line H2, one short blurb, four-stat strip (active brands, silent, ads, variants). Then per-brand sub-sections, then silent-brands strip.

### Brand sub-section
- H3 brand name + kind eyebrow (operator / lifestyle / developer / broker / etc.) + signal label.
- Brand blurb (one paragraph, max 60 words).
- 5-stat tile row (ads, active, variants, residences, advertisers).
- "Library scope" line.
- Indented (left-rule) brand-body containing residence sub-sections.

### Residence sub-section (nested inside brand)
- H4 residence name + blurb.
- 3-stat tile row (verified ads, active, variants).
- For each ad: metadata strip (advertiser, status, tag, date, platforms, variant indicator, library-id link), then horizontal scroll-snap carousel of variant images with `1/N` captions.
- 3-5 facts at the bottom of each residence.

### Silent-brands strip
Lives at the bottom of every master plan. Three columns: brand name, kind, one-line absence note. Visually quiet (dashed top rule, dimmed type).

### Carousel & lightbox
Unchanged from v4 — CSS scroll-snap horizontal strip, vanilla JS lightbox.

### Five takeaways
Five numbered items, max 15 words each. Lead with the brand-counts insight.

### Methodology
`<details>` collapsible. Source rules, brand-bucket definition, scope, disclosed limitations.

## 7. Data plane

`/tmp/lux_v4/_residence_search_results.json` — per-residence Meta Ad Library banner counts.
`/tmp/lux_v4/_variants.json` — per-LID detail-page scrape with explicit version count.
`/tmp/lux_shots/*.png` — variant images on disk.
The build script (`/tmp/build_lux_v5.py`) embeds verified-only ads into a single self-contained HTML, base64-encoding all variant images. Brand metadata is hard-coded in the script's `BRANDS` list, mapping each brand to its master plan, kind, signal level, library scope, advertisers, and nested residences.

## 8. Key States

- **Default:** As described.
- **Print:** Warm cream + dark ink. Carousel becomes a wrap-flex grid. Page-break before each master plan section.
- **Reduced motion:** Hover scale + lightbox fade disabled.
- **Mobile (390px):** Stat tiles re-flow to 3-up. Carousel items span 78vw. Matrix horizontally scrollable. Silent-row collapses to single column.

## 9. Interaction Model

- **Scroll-snap carousel.** `scroll-snap-type: x mandatory` on the strip, `scroll-snap-align: center` on each item.
- **Click to enlarge.** Each variant is a button; click opens the lightbox with full-res image.
- **Lightbox close.** Esc, click-outside, or Close button.
- **Reduced motion.** Transitions drop to 0ms.

## 10. Confirmation

```
IMPECCABLE_PREFLIGHT: context=pass product=pass command_reference=pass shape=pass image_gate=skipped:no_external_mocks_needed mutation=open
```
