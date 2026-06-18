# Release v0.4

`v0.4` turns the post-`v0.3` capture lessons into a public, privacy-safe skill update.

## Highlights

- Adds `capture-paper-snapshot-repair` for repairing existing Paper Snapshot, MagicPath-style import, or AI-generated webpage captures against live source evidence.
- Treats Playwright and the Codex in-app browser the same way for viewport measurement: request size, measured content size, and scrollbar gutter must all be recorded before building Paper.
- Adds manual range capture when browser annotation cannot select the requested section.
- Adds rules for video/MP4-backed sections: preserve measured structure, clipping, overlays, and source provenance, while allowing a representative still fallback when Paper cannot embed the moving video.
- Adds a clipping rule for closed or narrow carousel captions so Paper output uses measured overflow-hidden wrapper frames when text should disappear at a lane boundary.
- Adds checks for heading adornments, centered eyebrow/subheading groups, and breakpoint-specific CTA visibility.

## Public Test Lessons

- Apple Store carousel imports showed why snapshot repair needs one-line text reconstruction from live source line membership.
- Public product and marketing pages showed that the `15px` content-width loss can appear in Playwright as well as the in-app browser.
- Manual range capture cases showed that annotation failure should be a supported workflow, not a blocker.
- Carousel and video-led sections showed when strict source structure and convenient media fallbacks need to be separated in the audit.

## Privacy

This release intentionally excludes private project planning files, local filesystem paths, raw capture artifacts, and proprietary design work. Public examples remain generalized around publicly reachable websites and reusable capture failure classes.
