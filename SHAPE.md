# Shape — Luxury Residential Ad Benchmark, v3 (metrics-first revalidation)

## 1. Feature Summary

A single-page competitive-intelligence brief covering six months of luxury residential paid-media activity in Saudi Arabia. **v3 is a metrics-first redesign** of v2: stat grids replace narrative paragraphs, every Meta count has been revalidated against the page-scoped Meta Ad Library banner, and four auth-walled platforms (TikTok, X, LinkedIn, Snap) are dropped in favor of SimilarWeb and Google Trends as alternative directional signals.

## 2. Primary User Action

A reader scans the page in 60-90 seconds and walks away with the per-cluster numbers. Drill-down is via the comparison matrix and the per-cluster stat grids; ad creative samples remain inline as evidence; the methodology footnote explains how every cell was sourced. The TOC supports lateral re-entry.

## 3. Why v3 (deltas vs v2)

v2 produced under-counts driven by **keyword-leak attribution** — sample ad-library IDs returned by keyword search were assigned to the wrong advertiser. v3 fixes this:

- Every count uses **page-scoped** Meta Ad Library URLs (`view_all_page_id=<id>`).
- Every page id was **verified by walking an ad's owner page_id JSON**, not inferred from keyword matches.
- The single biggest correction: Red Sea Global goes from 17 → ~570 ads in SA (33×).
- DarGlobal corrects from 16 → ~120 (7.5×).
- Christie's KSA corrects from 5 → ~20 (4×).
- Diriyah Company stays close to v2 (6 → 5; one ad expired since v2 capture).

## 4. Design Direction

**Color strategy:** unchanged from v2 — restrained warm-dark palette, single champagne-gold accent, OKLCH tokens.

**Theme scene sentence:** A senior strategist scans this on a 27-inch monitor at dusk; the page should feel like a Bloomberg terminal page typeset by Wallpaper — restrained, dense, every number earned.

**Anchor references:**
- *FT Markets data pages* for tabular density and tabular-numeral discipline.
- *Bloomberg Terminal* for stat-grid economy and the "every cell counts" feel.
- *NB Studio / Pentagram editorial print* for the shift between dense data zones and breathing typographic markers.

**Anti-references reinforced:** No narrative paragraphs. No "the takeaway is..." prose. No SaaS gradient hero metrics. No glassmorphism. No Looker tile grids.

## 5. Scope

- **Fidelity:** Production-ready.
- **Breadth:** One page, six top-level sections (hero, comparison matrix, four cluster sections, recommendations-as-bullets), plus footnotes/methodology.
- **Interactivity:** Static document with TOC scroll-spy and card hover.
- **Time intent:** Polish until it ships.

## 6. Layout Strategy — metrics-first redesign

### Hero
Stays editorial. Big DM Serif headline, eyebrow above, one short deck paragraph (max 3 sentences) framing the v3 revalidation. Below the deck: a 4-stat **at-a-glance grid** with the highest-impact corrections (e.g. "Red Sea Global: 17 → 570 ads, +553").

### Comparison matrix
Centerpiece. Real `<table>` with custom CSS Grid styling. Rows = clusters; columns = SA all-status, SA active, SA inactive, SA last-6-mo, GLOBAL all-status, SimilarWeb monthly visits, top channel. Each cell is a tabular figure. Header row uses small-caps eyebrows. Active rows have a thin gold left rule. Numbers dominate.

### Per-cluster sections (4 of them: Diriyah, Competitors-on-Diriyah-land, ROSHN orbit, RSG orbit)
Each section opens with: eyebrow, single-line H2, optional one-line tag.
Then a **stat grid** (4-up to 6-up) with the cluster's primary numbers — banner count, active/inactive split, deltas vs v2, SimilarWeb traffic.
Then **bullet facts** under the grid: 4-7 bullets per advertiser, max 12 words per bullet. No paragraphs.
Then **ad creative samples** at decent size (320-400px). Captions condensed: advertiser, project, dates, status, library-id link. No theme paragraphs.

### What this means (replaces v2 recommendations prose)
A single section at the bottom: 5 bullet points, max 15 words each. Prescriptive, not narrative.

### Methodology
Footnote / details element. Strict, short, sourced.

## 7. Data plane

The structured input is `/tmp/lux_v3_data.json`, which encodes:
- Per-advertiser page_id (or null if no Meta presence)
- Per-advertiser Meta count buckets (sa_all, sa_active, sa_inactive, sa_last6mo, global_all)
- v2 number, delta vs v2
- SimilarWeb signal where available
- Per-advertiser bullet-fact list (3-7 each, terse)

The build script turns this into the page; no live re-querying at render time.

## 8. Key States

- **Default:** As described.
- **Print:** Warm cream + dark ink. Cards drop borders to 0.6pt. Page-break before each major section.
- **Reduced motion:** All transitions disabled.
- **Mobile (390px):** TOC collapses to horizontal scroller. Stat grids stack 2-up. Cards stack single column with full-bleed images. Comparison matrix becomes horizontally scrollable; first column sticky.

## 9. Interaction Model

- **Scroll-spy TOC.** IntersectionObserver toggles the active TOC link.
- **Card hover.** 1px `--rule` border shifts to `--gold-soft` over 240ms. No movement, no shadow.
- **Library-id link click.** Opens the Meta Ad Library page for that creative in a new tab.
- **Reduced motion.** All transitions drop to 0ms.

## 10. Content Requirements (v3 budget — terse)

- Hero: 1 eyebrow, 1 H1, 1 deck paragraph (≤3 sentences), 4-stat at-a-glance grid.
- Comparison matrix: 1 header row, 8-10 advertiser rows, 7 columns.
- Per-cluster sections (×4): each ~1 short eyebrow paragraph (≤2 sentences), 4-6 stat tiles, 4-7 bullet facts per advertiser, 2-4 ad creative samples.
- "What this means": 5 bullets ≤15 words each.
- Methodology: ≤120 words, bulleted.

Total prose budget: under 600 words across the entire page (down from v2's ~4,500). Numbers and bullets carry the rest.

## 11. Recommended References

- `typography.md` — modular scale, tabular-numeral handling.
- `color-and-contrast.md` — OKLCH tokens, tinted-neutral discipline.
- `layout.md` — designed comparison matrix, stat grid construction.
- `spatial-design.md` — section breathing pattern.
- `responsive-design.md` — 390 / 768 / 1280 / 1920 behavior.
- `cognitive-load.md` — bullet brevity discipline.

## 12. Confirmation

The revalidation findings invalidate v2 in critical places (RSG 33×, DarGlobal 7.5×, Christie's 4×). The user (in the original v3 prompt) pre-confirmed:
- Drop TikTok, X, LinkedIn, Snap.
- Replace prose with stats + bullets.
- Re-source counts from page-scoped banner numbers.

```
IMPECCABLE_PREFLIGHT: context=pass product=pass command_reference=pass shape=pass image_gate=skipped:no_external_mocks_needed mutation=open
```
