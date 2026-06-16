# Contributing

This project improves by collecting real capture misses and turning them into repeatable extraction rules.

When reporting a miss, include:

- source URL
- selector
- viewport size
- screenshot of source
- screenshot of Paper result
- what was missed
- whether the missed detail exists in computed DOM/CSS, pseudo-elements, SVG, canvas, image, or font rendering

Useful miss categories:

- layout/order
- typography/wrapping
- image crop/object-fit
- background/effective color
- border/radius/stroke
- shadow/filter
- gradient/blend mode
- pseudo-element
- SVG/icon
- responsive breakpoint
- interactive/hover state

The preferred fix is to improve the extraction/recreation rule, not to hand-patch one example forever.

## Privacy

Do not include private project names, personal filesystem paths, private design files, proprietary planning docs, credentials, or customer/client information in issues, examples, screenshots, or test fixtures.

Use public websites, synthetic fixtures, or carefully anonymized descriptions when documenting capture misses.
