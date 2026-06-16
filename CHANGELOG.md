# Changelog

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
