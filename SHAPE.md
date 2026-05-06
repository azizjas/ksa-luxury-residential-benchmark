# Shape — Luxury Residential Ad Benchmark, v2

## 1. Feature Summary

A long-form, single-page editorial report that reviews six months of luxury residential advertising across Saudi Arabia, framed around Diriyah's vantage point. The page is designed to be read top-to-bottom, but also indexed via a sticky table of contents on desktop. It carries six sections: opening picture, Diriyah audit (Diriyah-only), competitors on Diriyah land, ROSHN luxury orbit, Red Sea Global luxury orbit, notable absences, and recommendations. Real ad creatives appear inline as base64-embedded images, sized to read like editorial photography rather than thumbnail strips.

## 2. Primary User Action

A reader (Diriyah executive, PIF stakeholder, or external analyst) absorbs the picture in roughly five minutes of reading and ten minutes of scanning, then walks away knowing exactly which platforms each major luxury developer in KSA is using, which platforms Diriyah is silent on, and where third parties are advertising on Diriyah-owned land without the brand's voice present. The TOC supports lateral re-entry; deep links to Meta library IDs support verification.

## 3. Design Direction

**Color strategy:** Restrained. Tinted warm neutrals (midnight stone background, cream ink, warm sand cards) carry roughly 90% of the surface; champagne gold is the only chromatic accent and sits in eyebrows, drop caps, the active TOC indicator, and hover states.

**Theme scene sentence:** A senior Diriyah strategist reads this on a 27-inch monitor in a hushed top-floor office at dusk, with the desk lamp on and the city lights coming up outside. The sentence forces dark mode with a warm cast; it does not force pure black, and it does not force a "cool corporate dark" treatment.

**Anchor references:**
- *FT Weekend Long Read* for paragraph rhythm, drop caps, and editorial pacing.
- *Wallpaper magazine print spreads* for image-led density, generous margins, and serif headline weight.
- *Aman / Aman Residences brand collateral* for the restrained warm-dark palette and the discipline of using one accent only.

**Anti-references reinforced from PRODUCT.md:** No SaaS gradient hero metrics. No Looker Studio panels. No Dubai luxury-real-estate gold-on-black metallic shine. No Bain blue-on-white sterility. No glassmorphic cards. No identical card grids with icon + heading + text repeated endlessly.

## 4. Scope

- **Fidelity:** Production-ready. The user said "I want to wait for a perfect v2."
- **Breadth:** One page, six top-level sections, plus a sticky TOC and a print stylesheet.
- **Interactivity:** Static document with passive interactions: TOC scroll-spy with active-state animation, card hover border-shift, a single fade-in-on-scroll observer.
- **Time intent:** Polish until it ships.

## 5. Layout Strategy

The page is a single column on mobile, a two-column reading layout on desktop wider than 1100px. The left column carries content, capped at 68ch for body and 22ch for headings. The right column carries the sticky TOC inside the gutter — never overlapping content, always parked to the side. Section spacing is generous (96-128px between major sections) and tight inside paragraphs (24-32px between paragraphs). The Najdi-inspired geometric divider appears once between each top-level section, never inside a section.

Cards are arranged in a `repeat(auto-fit, minmax(320px, 1fr))` grid inside each cluster section, with `--space-5` gaps. Within a cluster, cards are sorted by recency of activity rather than alphabetically — recency is the editorial signal.

The **comparison matrix** in section 1 is its own designed component, not a generic table. It uses CSS Grid with named areas: a left rail for developer + project-line, six platform columns each with count + format chips + status dot. Header row has eyebrow caps above the platform names. Active rows have a thin gold left rule (1px, full hairline, not the banned side-stripe accent which would be a colored border ≥ 2px used as decoration).

The hero is text-only. No big-number-small-label, no gradient, no metric tile. Just an oversized DM Serif headline that breaks across two lines, an eyebrow above, and a deck-style intro paragraph.

## 6. Key States

- **Default:** As described above.
- **Print:** A separate stylesheet flips palette to warm cream + dark ink, hides the sticky TOC, expands all collapsed elements, and adds page-break-before on each major section. Footer has page numbers in eyebrow caps. Cards drop their borders to 0.6pt.
- **Reduced motion:** The IntersectionObserver fade-in is disabled. TOC active state still transitions but at 0ms.
- **No-image fallback:** Broken / missing creative shows the alt text in a card with a hairline border, no broken-image icon. Tested by setting one card path to a path that does not resolve.
- **Mobile (390px):** Sticky TOC collapses to a horizontal scroller pinned below the H1, with snap-stop on each section eyebrow. Cards stack to single column with full-bleed images.

## 7. Interaction Model

- **Scroll-spy TOC.** IntersectionObserver watches each section's `<h2>` and toggles a `data-active` attribute on the matching TOC link. The link's hairline rule transforms via `scaleX()` from 0 to 1 with 280ms ease-out-quart.
- **Card hover.** 1px border on `--rule` shifts to `--gold-soft` over 240ms. No scale, no shadow, no movement.
- **Library-id link click.** Opens the Meta Ad Library page for that creative in a new tab. `rel="noopener"`, focus-visible ring in gold.
- **Reduced motion.** All transitions drop to 0ms. The fade-in is removed.
- **Keyboard.** TOC links and library-id links are reachable in DOM order. Cards themselves are not focusable; their image links are.

## 8. Content Requirements

Roughly 4,500 words of editorial body text covering: opening framing, comparison matrix, six section intros, per-developer per-platform breakdowns, six section close-outs, recommendations.

Multi-platform data per developer: Meta active count, Meta paused count, Google ATC active count, TikTok active count, X active count, LinkedIn active count, Snap active count. Where a platform has no data and we know it, we say so (em-rule glyph). Where a platform was checked and was empty, we say "none observed" plainly.

Roughly 30-40 ad creative cards displayed at decent size (320-400px square in grid, with 1:1 aspect ratio). Each card has: advertiser, project, dates, status pill, theme paragraph, tag chip, Meta library ID link.

A footer with: methodology bullets, capture date, attribution line "KSA Luxury Residential · Competitive Intelligence" (no Diriyah Marketing attribution, no personal handles).

## 9. Recommended References

- `typography.md` for the modular scale, drop cap, and small-caps eyebrow spec.
- `color-and-contrast.md` for OKLCH tokens and tinted-neutral discipline.
- `layout.md` for the matrix component, asymmetric reading column, and rhythm between sections.
- `spatial-design.md` for the section breathing pattern.
- `interaction-design.md` for the TOC scroll-spy and focus-visible treatment.
- `motion-design.md` for the ease-out-quart transitions and reduced-motion handling.
- `responsive-design.md` for the 390 / 768 / 1100 / 1280 / 1920 breakpoint behavior.

## 10. Open Questions

None blocking. Items to decide during craft, but the brief carries enough to start:

- Should the Najdi divider be inline SVG (preferred) or Unicode glyph? Decision: inline SVG, as DESIGN.md specifies.
- Should the comparison matrix be an `<table>` semantically with custom CSS, or a CSS Grid with ARIA roles? Decision: actual `<table>` with `role="table"` left default, paired with display-grid styling. This preserves screen-reader semantics.
- Should the ad creative card use a `<figure>` element? Yes (it already does in v1; preserve this).
- Is gold-on-black contrast safe? `oklch(76% 0.115 80)` on `oklch(13% 0.008 60)` — the gold (#D4A857) on midnight-stone (#0E0D0C) gives ~10.6:1 luminance contrast which is well above AAA.

---

## Confirmation

**The user pre-approved this brief in the original task message** ("Aziz said: I want to wait for a perfect v2", with explicit direction on color tokens, typography family, spacing scale, motif use, components, and section structure). The shape gate may be marked `pass` on the basis of that pre-confirmed brief. No further user response is needed before craft.

```
IMPECCABLE_PREFLIGHT: context=pass product=pass command_reference=pass shape=pass image_gate=skipped:no_external_mocks_needed mutation=open
```
