# Changelog

## v0.4 - 2026-06-19

- Added `capture-paper-snapshot-repair` as a separate skill entrypoint for fixing existing Paper Snapshot, MagicPath-style import, or AI-generated design-tool captures against the live source.
- Added Snapshot Repair Mode to the shared contract so Codex starts from the selected Paper frame, builds a repair inventory, and patches conversion artifacts rather than rebuilding from scratch.
- Documented snapshot-specific failure classes such as stacked inline text fragments, aggregate text boxes, missing micro-elements, unresolved SVGs, wrong media crops, visible hidden controls, boundary contamination, and incorrect hover/open states.
- Added the Apple Store carousel pricing-fragment repair as a regression test case for one-line source text becoming stacked Paper fragments.
- Updated viewport-gutter guidance so Playwright captures also measure and compensate for `15px` content-width loss when present, instead of treating it as Codex in-app-browser-only.
- Added first-class manual range capture when browser annotation cannot select a section, including explicit start/stop landmarks and bounded composite roots.
- Added strict handling for live video/MP4-backed sections: preserve measured structure and media provenance, while allowing representative still fallbacks when Paper cannot embed the moving video.
- Added clipping guidance for closed or narrow carousel captions, requiring measured overflow-hidden wrapper frames when Paper text nodes spill past their lanes.
- Added checks for title-cluster adornments, centered text groups, and breakpoint-specific CTA visibility.

## v0.3 - 2026-06-18

- Added self-directed source selection rules for capture batches without browser annotations.
- Added interactive-state capture rules for mega menus, drawers, accordions, tabs, hover/open states, and cart states.
- Added a required Skill Compliance Audit after each capture so long-running capture marathons do not drift away from the skill workflow.
- Added selectable `capture-paper-dom-strict` and `capture-paper-dom-placeholder` skill entrypoints.
- Added strict-vs-placeholder capture-mode gates so exact source capture and reusable scaffold capture cannot bleed into each other.
- Updated the standard mobile target to Samsung Galaxy S24 Ultra `430 x 932`.
- Added viewport request/content width accounting for browser scrollbar gutters.
- Hardened strict SVG handling for dense inline product wordmarks, swatches, badges, and icon assets.
- Added hover-state verification guidance requiring real post-hover visual evidence when CSS inspection is insufficient.
- Added visibility filtering for `opacity:0`, hidden, clipped, and inactive carousel controls.
- Added repeated-card special-case inventory guidance for promo, gift, upsell, bundle, featured, and expanded card types.

## v0.2 - 2026-06-16

- Hardened the strict capture workflow after a detailed Bounti employee training footer review.
- Added a required layer inventory gate before building Paper variants.
- Added explicit fidelity rules for:
  - SVG `<use>` symbol resolution for logos and button icons
  - CTA button anatomy, including nested arrow/icon boxes
  - dense footer/nav column completeness
  - legal and social link alignment lanes
  - single-line text preservation under font fallback
  - fallback font-weight mapping from family names such as Medium and Semibold
- Added a card-internal fidelity gate after the Bounti training-management benefits capture:
  - preserve `object-position`, parent clipping, and rendered media crop
  - check title-chip coordinates and dimensions inside repeated cards
  - inventory card overlays such as sent-to boxes, language selectors, progress bars, and metadata pills
  - preserve rendered line count for card descriptions and captions
  - report any dense SVG/image panel simplification explicitly
- Added a source-vs-Paper verification gate after follow-up Bounti benefits review:
  - compare heading line membership word-for-word, not just line count
  - preserve rendered casing and CSS `text-transform` for labels and chips
  - capture frosted/glass/iced chip surfaces via alpha fills, filters, backdrop filters, borders, and overlays
  - visually compare card media crops against the live source before accepting copied image CSS values
- Expanded the checklist and test-case notes for the Bounti final CTA/footer blend misses.

## v0.1 - 2026-06-16

- Published the initial public `capture-paper-dom` skill package.
- Documented the origin story in privacy-safe terms.
- Explained the limitations observed in commercial DOM capture workflows, including Paper.design capture and Magicpath AI-style extensions.
- Documented the Codex in-app browser plus Paper MCP workflow.
- Preserved the default laptop, mobile, and tablet capture triad.
- Documented public Bounti and Dot Cards test cases.
- Added fidelity rules for:
  - computed backgrounds over screenshot sampling
  - pseudo-elements
  - box shadows and filters
  - color swatch shine gradients
  - empty selector controls
  - tiny divider lines
  - font fallback wrapping issues
- Added post-release test notes from the Bounti employee training hero/footer capture:
  - add large background media before overlay surfaces
  - report when a selected DOM root includes below-fold content
  - widen text boxes when font fallback wraps button labels
