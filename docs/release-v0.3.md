# v0.3 Release Notes

`capture-paper-dom` v0.3 splits the workflow into selectable skill entrypoints while keeping one shared fidelity contract.

## Included

- New `$capture-paper-dom-strict` wrapper for exact source capture.
- New `$capture-paper-dom-placeholder` wrapper for reusable scaffold and destination-brand replacement workflows.
- Default `$capture-paper-dom` chooser workflow remains strict unless placeholders are explicitly requested.
- Updated mobile target to Samsung Galaxy S24 Ultra `430 x 932`.
- Browser viewport accounting for the observed `15px` scrollbar gutter in the Codex in-app browser.
- Stronger SVG preservation rules for dense inline wordmarks, swatches, badges, and icons.
- Hover-state verification rules requiring real post-hover visual evidence when needed.
- Hidden-control filtering for `opacity:0`, clipped, inactive, and otherwise invisible DOM controls.
- Repeated-card inventory rules for promo, gift, upsell, bundle, featured, and expanded card variants.

## What Changed

This release keeps strict and scaffold captures from drifting into each other:

- Strict mode preserves source-specific visible assets and reports any fallback explicitly.
- Placeholder/scaffold mode preserves measured structure while using role-labeled placeholders for assets intended to be replaced.
- All modes still share the same quality gates: root-boundary checks, viewport/content measurement, layer inventory, card-internal fidelity, SVG handling, micro-element preservation, and source-vs-Paper QA.

## Privacy

The public release uses generalized section-library language. Private project names, local filesystem paths, personal details, and proprietary planning artifacts are excluded.

## Known Limitations

- No automated regression runner yet.
- Fidelity still depends on Paper's available fonts and rendering support.
- Backdrop blur, video, canvas, WebGL, and complex animation states may require approximations with explicit reporting.

## Next

- Add reusable DOM/style extraction scripts.
- Save sanitized public source snapshots for regression cases.
- Build automated checks for viewport/content widths, SVG preservation, hidden controls, line membership, and media crop geometry.
