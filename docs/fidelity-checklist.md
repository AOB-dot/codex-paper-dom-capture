# Fidelity Checklist

Use this checklist for every capture before calling the result done.

## Capture Mode

- Capture mode is declared before extraction: strict or placeholder/scaffold.
- Strict mode is the default for `$capture-paper-dom`, exact DOM capture, and any request that says strict, exact, faithful, clone, no placeholders, or similar.
- Strict mode preserves visible source-specific assets, including logos, product images, media, SVGs, wordmarks, swatches, badges, and decorative imagery. No visible source asset is replaced with a placeholder unless reported as an unavoidable limitation.
- Strict mode preserves visible inline SVGs as actual SVG layers/assets first. Dense wordmark or swatch SVGs are not approximated with text until inline SVG insertion, isolated SVG writes, and SVG asset import have been tried and failed.
- Placeholder/scaffold mode is used only by explicit request or `$capture-paper-dom-placeholder`.
- Placeholder/scaffold mode keeps measured structure while replacing source-specific assets with role-labeled placeholders and nearby source-reference evidence.
- If a user asks for strict capture inside a reusable-library project, strict wins for that capture.

## Layout

- Target section dimensions match measured DOM rect.
- If no annotation was provided, the chosen selector is the smallest complete DOM root for the planned section/state.
- Component captures are cropped to the selected root/state boundary; no adjacent hero, footer, previous section, or next section pixels are included unless the capture explicitly asks for a combined transition.
- Root boundary evidence is recorded for component captures: root rect, painted surface rect when different, visible previous/next sibling rects, and any fixed/sticky/portal layers intentionally included.
- A boundary contamination check has passed: no black hero sliver below a header, previous-section tail above a card row, next-section strip below a drawer/menu, or other source-context pixels are present in the editable Paper artboard.
- Source URL, selector, viewport, scroll position, and state recipe are recorded.
- Requested viewport, `innerWidth`, `visualViewport`, document/client width, body width, root rect width, and scrollbar gutter are recorded. Standard target content widths are `1440`, `430`, and `820`; initial browser requests should be `1455`, `445`, and `835` to allow for the observed `15px` gutter.
- If the measured content/root width misses the target width, the viewport request is adjusted and the DOM is re-extracted. Do not stretch a narrower Paper capture after extraction to make it look like the target width.
- Paper artboards for section-library/component captures use the measured target content/root width, not the wider browser request width, unless a separate device shell/gutter context is intentionally represented.
- Interactive state availability is verified per breakpoint; no-open or navigate-only behavior is recorded instead of inventing a missing menu/drawer/hover state.
- Major content order matches the source.
- Repeated cards preserve their original order.
- Image/text pairings are not swapped.
- Spacing and alignment use measured positions, not visual guesses.
- Background surfaces extend to the same edges as the source.
- Overflow and clipping match the source where visible.
- If source context is needed for QA, it is kept in notes/screenshots rather than as editable Paper layers.

## Layer Inventory

Before building each variant, list the visible source inventory and check it off after Paper QA.

- Background media and section-wide images are present.
- All logos, images, inline SVGs, and SVG `<use>` references are present or explicitly reported.
- Buttons preserve their surface, label, icon/arrow box, icon glyph, shadow, radius, and spacing.
- Card-internal overlays such as title chips, sent-to boxes, metadata pills, language selectors, progress bars, and floating panels are accounted for.
- Footer/nav columns preserve every heading and visible item.
- Legal links, social links, and copyright text keep separate positions, colors, and alignment lanes.
- Hairlines, separators, pseudo-elements, badges, bullets, stars, and empty controls are accounted for.
- `opacity:0`, `display:none`, `visibility:hidden`, zero-area, clipped, or inactive carousel controls are not rendered as visible layers unless capturing a named active/open state.
- No visually distinct source item is collapsed into a generic text block when it differs by position, color, weight, or alignment.

## Placeholder/Scaffold Capture Mode

Use this section only when the user explicitly wants a reusable library scaffold rather than an exact source clone.

- The capture notes declare scaffold mode rather than strict asset mode.
- Source-specific logos, product images, branded SVG wordmarks, illustrations, videos, or company media are represented as role-labeled placeholders when they will be replaced by the destination brand.
- Each placeholder keeps the measured slot position, size, radius, crop, clipping, z-order, and aspect ratio from the source.
- Placeholdered assets have visible source-reference evidence near the Paper capture, usually as one companion screenshot/reference strip per section or repeated card cluster outside the reusable scaffold artboard.
- Individual close-up reference tiles are added only when a source asset treatment matters on its own, such as a special SVG/logo, video frame, unusual crop, frosted overlay, mask, or branded icon system.
- Reference strips or tiles are labeled by role and source, and show enough original context to understand the asset, crop, mask, radius, video frame, SVG/logo detail, and overlay relationship.
- No design element disappears just because its content is placeholdered; every logo/media/SVG slot remains visible and labeled.
- Generic UI controls and micro-elements remain rendered normally, not placeholdered away.
- The completion audit lists which assets were placeholdered, why, and where the source-reference strip or necessary close-up tile was placed.

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
- Dense inline SVG wordmarks, swatches, and badges are preserved through actual SVG insertion/import before any approximation is allowed.
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

## Interactive States

For menus, drawers, accordions, tabs, hover panels, and cart states:

- State is opened/activated in the live in-app browser before extraction.
- State recipe is recorded, such as click trigger, selected tab, filled cart setup, or expanded accordion.
- Open surface is captured as its own named artboard or named group.
- Trigger, overlay/scrim, drawer/menu panel, portal content, sticky/fixed positioning, and body scroll-lock effects are accounted for.
- Empty and filled states are captured separately when visually different.
- Quantity steppers, remove buttons, checkout buttons, disabled/enabled states, upsells, price rows, dividers, and shadows are preserved where relevant.

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

## Skill Compliance Audit

After each capture, check and record:

- `capture-paper-dom` was explicitly used.
- Required device variants were captured or the narrowing was user-requested.
- Layer inventory was created before building.
- Paper screenshot QA was performed against the live source.
- Pseudo-elements, SVG `<use>`, image crops, micro-elements, and interactive state details were inspected.
- Reusable misses were fixed in the skill or added to test notes.
