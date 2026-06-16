# Fidelity Checklist

Use this checklist for every capture before calling the result done.

## Layout

- Target section dimensions match measured DOM rect.
- Major content order matches the source.
- Repeated cards preserve their original order.
- Image/text pairings are not swapped.
- Spacing and alignment use measured positions, not visual guesses.
- Background surfaces extend to the same edges as the source.
- Overflow and clipping match the source where visible.

## Layer Inventory

Before building each variant, list the visible source inventory and check it off after Paper QA.

- Background media and section-wide images are present.
- All logos, images, inline SVGs, and SVG `<use>` references are present or explicitly reported.
- Buttons preserve their surface, label, icon/arrow box, icon glyph, shadow, radius, and spacing.
- Card-internal overlays such as title chips, sent-to boxes, metadata pills, language selectors, progress bars, and floating panels are accounted for.
- Footer/nav columns preserve every heading and visible item.
- Legal links, social links, and copyright text keep separate positions, colors, and alignment lanes.
- Hairlines, separators, pseudo-elements, badges, bullets, stars, and empty controls are accounted for.
- No visually distinct source item is collapsed into a generic text block when it differs by position, color, weight, or alignment.

## Backgrounds

- Effective background comes from computed ancestor chain.
- Browser annotation overlay tint is ignored.
- Transparent backgrounds are walked upward until a real background is found.
- Gradients are preserved where possible.

## Typography

- Source font family is checked against Paper availability.
- Fallbacks are noted to the user.
- Font size, weight, color, line height, and letter spacing are computed.
- `text-transform`, `white-space`, and rendered casing are computed.
- Font family names are checked for encoded weights such as Medium, Semibold, Bold, Regular, or Book when computed `fontWeight` is misleading.
- Rendered line breaks match the source visual.
- Heading line membership matches word-for-word, not only by total line count.
- Source one-line copy remains one-line in Paper unless explicitly reported as a fallback limitation.
- Card descriptions and captions preserve their rendered line count, such as two source lines staying two Paper lines.
- Labels and card chips preserve rendered uppercase/lowercase casing even when DOM text differs.
- Mixed-color or mixed-opacity inline text is split into separate editable layers when needed.
- Alpha text such as pale/hollow-looking statistics keeps its actual RGBA color.

## Images And SVG

- Use `currentSrc` where available.
- Preserve `object-fit`, `object-position`, parent clipping, crop, and border radius.
- If an image crop is wrong in Paper, wrap the image in a clipped frame and offset/scale it to match the rendered source crop.
- Compare source and Paper card crops by visible subject placement, not only by copied CSS values.
- Inline SVGs are copied directly.
- SVG `<use>` references are resolved from document `symbol`/`defs` content or replaced with actual visible paths. An unresolved blank logo or icon is not acceptable for strict capture.
- Missing icon fonts are recreated with acceptable visible equivalents only when unavoidable.

## Cards

For each repeated card:

- Card shell, clipping, radius, shadow, and background match the source.
- Image/media crop matches the rendered source, not only the asset URL.
- Title chip or badge position and size match the source card.
- Title chip or badge casing matches rendered source casing, including uppercase `text-transform`.
- Frosted/glass/iced chip texture is represented with alpha fill, blur/filter, border, shadow, and overlay where Paper supports it.
- Overlay scrims, gradients, and translucent panels are present.
- Floating callouts such as sent-to boxes, language selectors, progress bars, and metadata pills are present.
- Card title and description line counts match the source.
- Off-artboard carousel cards preserve the visible edge crop.
- Dense SVG/image panels are preserved as original assets when full editable recreation is impractical; any simplification is reported.

## Buttons

Button anatomy must be checked as separate parts:

- outer surface
- label
- nested icon or arrow container
- icon glyph, including diagonal arrows
- shadow
- border radius
- internal spacing

Do not recreate a CTA as only a rounded rectangle with text if the source has a separate arrow box or icon.

## Footers And Dense Nav Areas

Footers and final CTA/footer blends often carry many small details.

- Brand logo is present.
- Newsletter copy keeps source line breaks.
- Every column heading and item is captured.
- Heading weights survive font fallback.
- Bottom divider or hairline is present.
- Copyright/legal/social text keeps separate colors.
- Right-aligned social links stay on the right rather than flowing next to legal links.

## Micro-Elements

Explicitly check for:

- 1px dividers
- separator lines between rating and review text
- stars
- small badges
- bullets
- empty radio circles
- selected radio/check circles
- selected-state rings
- discount pills
- tiny state indicators
- hover/active visual state markers if captured

## Surface Effects

Preserve:

- `box-shadow`
- `filter`
- `backdrop-filter` where relevant
- frosted/glass/iced chip treatments
- opacity
- gradients
- `mix-blend-mode`
- pseudo-element overlays

## Pseudo-Elements

Inspect both:

- `::before`
- `::after`

Capture pseudo-elements when they have:

- visible text content
- background color
- gradient
- border
- shadow
- meaningful width/height
- opacity
- blend mode

## Color Swatches

Color swatches often have more than a flat fill.

Check for:

- base background color
- border
- selected ring
- diagonal shine
- clipped gradient overlay
- `mix-blend-mode`
- white/black special cases

For Dot Cards, the color swatch shine was a `::before` circular overlay with a diagonal linear gradient and `mix-blend-mode`.

## Controls

Do not filter out empty-looking elements if they represent controls.

Examples:

- unselected option circles
- selected check circles
- tiny close buttons
- cart count badges
- dropdown chevrons

## Screenshot QA

After building in Paper:

- screenshot the Paper artboard
- compare with the live browser section at the same viewport and scroll position
- inspect misses at high zoom
- compare against the layer inventory before calling the capture complete
- compare heading line membership word-for-word
- compare rendered casing for chips, labels, nav headings, and card labels
- compare frosted/glass chip treatments
- compare card media crops by visible focal point placement
- patch with targeted edits
- update this project with any repeated miss pattern
