---
name: capture-paper-dom-placeholder
description: Use when the user asks for placeholder, scaffold, reusable section-library, adaptation, brand-replacement, or structure-first website capture into Paper.
---

# Capture Paper DOM Placeholder

Read and follow the shared contract in `../capture-paper-dom/SKILL.md`, then force **Placeholder/Scaffold Capture Mode**.

This wrapper exists so the user can choose structure-first capture directly from the slash/skill picker.

## Required Override

- All shared quality gates still apply: device/content-width measurement, selected root/state boundary checks, layer inventory, card-internal fidelity, SVG handling, micro-element preservation, source-vs-Paper screenshot QA, and the final Skill Compliance Audit.
- Preserve measured structure: section boundary, breakpoint behavior, card count/order, slot geometry, masks, clipping, spacing, radius, shadows, surfaces, typography roles, button anatomy, state layout, and responsive alignment.
- Replace source-specific product/media/SVG/logo assets only when they are intended to become destination-brand content.
- Every placeholder must keep the measured source position, size, clipping, radius, aspect ratio, object-fit behavior, and z-order.
- Add source-reference evidence next to the Paper capture for every placeholdered section or repeated card cluster.
- Preserve generic UI controls and micro-elements normally; do not placeholder away arrows, chevrons, dividers, quantity controls, hairlines, badges, or functional icons.
- Treat hidden controls as hidden: do not render `opacity:0`, clipped, inactive, or off-state carousel controls unless the named state makes them visible.
- For hover/open states, verify the real live state visually before drawing it; CSS inspection alone is not enough.
- Preserve repeated-card differences and slot roles instead of cloning one placeholder template across promo, gift, upsell, bundle, featured, or expanded variants.
- Name outputs with `Placeholder Scaffold Capture`.
- In the Skill Compliance Audit, list placeholdered assets and where their source-reference evidence was placed.
