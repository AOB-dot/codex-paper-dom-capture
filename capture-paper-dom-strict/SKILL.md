---
name: capture-paper-dom-strict
description: Use when the user asks for strict, exact, faithful, no-placeholder DOM capture from the Codex in-app browser into Paper or another scriptable design canvas.
---

# Capture Paper DOM Strict

Read and follow the shared contract in `../capture-paper-dom/SKILL.md`, then force **Strict DOM Capture Mode**.

This wrapper exists so the user can choose strict capture directly from the slash/skill picker.

## Required Override

- All shared quality gates still apply: device/content-width measurement, selected root/state boundary checks, layer inventory, card-internal fidelity, SVG handling, micro-element preservation, source-vs-Paper screenshot QA, and the final Skill Compliance Audit.
- Preserve all visible source assets: product images, media, videos, logos, SVGs, wordmarks, branded marks, badges, swatches, icons, and decorative imagery.
- Do not use placeholders for source-specific visible assets.
- Preserve visible inline SVGs as the actual extracted SVG first. Dense SVG paths are not a reason to approximate with editable text; try isolated inline SVG insertion or SVG asset import before any fallback.
- Treat hidden controls as hidden: do not render `opacity:0`, clipped, inactive, or off-state carousel controls unless the named state makes them visible.
- For hover/open states, verify the real live state visually before drawing it; CSS inspection alone is not enough.
- Preserve repeated-card differences instead of cloning one card template across promo, gift, upsell, bundle, featured, or expanded variants.
- Use source-reference screenshots only as QA evidence beside the editable capture, never as replacements for missing layers.
- If an asset cannot be reproduced directly in Paper, use the closest faithful fallback and report the limitation.
- Name outputs with `Strict DOM Capture`.
- In the Skill Compliance Audit, state that strict mode was used and confirm no source-specific visible assets were intentionally placeholdered.
