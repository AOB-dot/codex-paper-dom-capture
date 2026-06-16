# v0.2 Release Notes

`capture-paper-dom` v0.2 hardens the strict capture workflow around real capture misses found while recreating public website sections in Paper.

## Included

- Stronger layer inventory requirements before building Paper variants.
- Footer, nav, legal-link, social-link, and CTA button anatomy checks.
- Required SVG `<use>` symbol resolution for logos and icon systems.
- Card-internal fidelity checks for repeated marketing cards.
- Source-vs-Paper verification gate before completion.
- Expanded public test-case notes and fidelity checklist.

## What Changed

This release turns several observed misses into explicit capture rules:

- Preserve nested CTA arrow/icon boxes instead of reducing buttons to text on a pill.
- Keep dense footer columns, logo assets, bottom hairlines, and separate legal/social alignment lanes.
- Preserve single-line text and heading line membership under font fallback.
- Map font weights from family names such as Medium and Semibold when computed CSS is misleading.
- Preserve rendered casing from CSS `text-transform`, especially labels and card chips.
- Capture frosted/glass/iced surfaces using alpha fills, filters, backdrop filters, borders, shadows, and overlays where possible.
- Verify image crops by visible subject placement, not only by copied image URL or `object-position`.

## Known Limitations

- No automated regression runner yet.
- Fidelity still depends on Paper's available fonts and rendering support.
- Backdrop blur, video, canvas, WebGL, and complex animation states may require approximations with explicit reporting.

## Next

- Add reusable DOM/style extraction scripts.
- Save source snapshots for public regression cases.
- Build automated checks for line membership, SVG symbol resolution, media crop geometry, and dense footer inventories.
