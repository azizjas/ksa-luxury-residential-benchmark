# Shape — Luxury Residential Ad Benchmark, latest

## 1. Feature Summary

A single-page competitive-intelligence brief covering Saudi luxury residential paid Meta over the **last twelve months**. The shift from prior iterations: a **sites-driven ownership classification** built directly from diriyahcompany.sa/en/diriyah-living and wadisafar.com/en/hotels.

- Anything listed on those two URLs = Diriyah-owned.
- Anything else advertising in Diriyah territory = competitor.
- ROSHN (Sedra) and Red Sea Global (The Red Sea, AMAALA) are tracked as separate competitor master plans.

Methodology: every Diriyah-relevant Meta page is scrolled exhaustively, every ad in the 12-month window captured, then each ad bucketed manually to its residence (text + image + landing-page URL signals). Adjacent-card text bleed is stripped before keyword scanning so a M.A.D. Muscat creative on the DarGlobal page does not falsely match Trump Mansions copy from the next card. Prismax ads are excluded entirely. Empty residences are dropped from the body but listed in an audit-trail block in the methodology footer.

## 2. Primary User Action

A reader scans the matrix in 30 seconds, sees a camp pill against every advertiser ("Diriyah-owned" / "Competitor" / "ROSHN" / "Red Sea Global" / "Mixed"), then drills into the section that matters. Empty rows do not exist. Audit-trail line tells them which canonical Diriyah residences ran zero paid Meta in window.

## 3. Sections (in order)

1. **Hero.** Headline question. Six at-a-glance stats. Compile date.
2. **Advertiser sweep.** Matrix sorted by volume, with a Camp column tagged with a small-caps pill.
3. **Diriyah master plan (Diriyah-owned).** Per diriyahcompany.sa: 8 residential lines. Render those with ads only.
4. **Wadi Safar (Diriyah-owned).** Per wadisafar.com: 6 brands. Render those with ads only.
5. **Competitors advertising in Diriyah territory.** Sub-grouped:
   - Rayana product line (DarGlobal).
   - Trump line (Dar Al Arkan + Dar Global + Trump Organization).
   - Other third parties (brokerages, architects).
6. **Sedra (ROSHN).**
7. **The Red Sea (RSG).**
8. **AMAALA (RSG).**
9. **Five takeaways.**
10. **Methodology** (collapsible). Audit trail block.

## 4. Design Direction

**Color strategy:** unchanged — restrained warm-dark palette, single champagne-gold accent, OKLCH tokens. New: camp pills in semantic colors (gold = Diriyah, terracotta = competitor, neutral = ROSHN, cyan = RSG, mute = Mixed).

**Theme scene sentence:** A Diriyah Marketing Director scans this on a 27-inch monitor at dusk. Bloomberg terminal page typeset by Wallpaper. Restrained, dense, every number earned. The camp pill is the new piece of design furniture, sitting on every matrix row, telling the reader who owns the residence behind that ad in one glance.

**Anchor references:**
- *FT Markets data pages* for tabular density.
- *Bloomberg Terminal* for stat-grid economy.
- *NB Studio / Pentagram editorial print* for breathing typographic markers.

**Anti-references:** no SaaS gradient hero metrics, no glassmorphism, no Looker tile grids, no version markers in body content, no narrative paragraphs beyond the hero deck.

## 5. Type ladder

Five distinct steps, each ≥1.25× the next. No flat-hierarchy detector flag.

- 12px — meta, captions, eyebrow labels.
- 16px — body, blurbs, table cells.
- 19px — residence titles, advertiser names in ad cards.
- 26px — sub-section titles, residence stat numbers.
- 36px — section H2s.
- 96px (clamp) — H1 hero.

## 6. Heading hierarchy

- H1 = hero only.
- H2 = each top-level section (Diriyah master plan, Wadi Safar, Competitors, Sedra, The Red Sea, AMAALA, Five takeaways, Methodology, At-a-glance).
- H3 = either residence title (in non-grouped sections) OR sub-section title (in Competitors).
- H4 = residence title inside a sub-section (Competitors only).

No skipped heading levels.

## 7. Bucketing rules

- Each ad's body is cleaned to its own card text only (strip everything from the next "Library ID:" line onwards; if own LID isn't in the body, take the pre-first-LID slice).
- Body matching uses ONLY the cleaned own-card body. Never `full_text` (the whole page transcript leaks keywords across ads).
- An ad can be attributed to multiple residences if its creative markets a portfolio.
- Generic-precedence: when both a line generic (rayana-generic) and a master-plan generic (wadi-safar-generic, diriyah-generic) match, keep only the line generic. Avoids triple-counting the same ad in three buckets.

## 8. Data plane

- `/tmp/lux_v6/sweep_<page>.json` + `/tmp/lux_v7/sweep_<page>.json` — per-advertiser sweep results.
- `/tmp/lux_v7/_buckets.json` — bucketed result, per residence, with owner_camp tag.
- `/tmp/lux_v6_shots/` — variant images on disk.
- `/tmp/build_lux_v7.py` — embeds verified-only ads into a single self-contained HTML, base64-encoding all variant images.

## 9. Key states

- **Default.** As described.
- **Print.** Warm cream + dark ink. Carousel becomes a wrap-flex grid.
- **Reduced motion.** Hover scale + lightbox fade disabled.
- **Mobile (390px).** Stat tiles re-flow. Carousel items span 78vw. Matrix horizontally scrollable.

## 10. Confirmation

```
IMPECCABLE_PREFLIGHT: context=pass product=pass command_reference=pass shape=pass image_gate=skipped:no_external_mocks_needed mutation=open
```
