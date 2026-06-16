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

## Backgrounds

- Effective background comes from computed ancestor chain.
- Browser annotation overlay tint is ignored.
- Transparent backgrounds are walked upward until a real background is found.
- Gradients are preserved where possible.

## Typography

- Source font family is checked against Paper availability.
- Fallbacks are noted to the user.
- Font size, weight, color, line height, and letter spacing are computed.
- Rendered line breaks match the source visual.
- Mixed-color or mixed-opacity inline text is split into separate editable layers when needed.
- Alpha text such as pale/hollow-looking statistics keeps its actual RGBA color.

## Images And SVG

- Use `currentSrc` where available.
- Preserve `object-fit`, crop, and border radius.
- Inline SVGs are copied directly.
- SVG `<use>` references are resolved or replaced with actual paths where possible.
- Missing icon fonts are recreated with acceptable visible equivalents only when unavoidable.

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
- compare with the live browser section
- inspect misses at high zoom
- patch with targeted edits
- update this project with any repeated miss pattern

