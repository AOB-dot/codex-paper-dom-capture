# Test Cases

This document records real sections used to evolve the skill.

## Bounti Customers Section

URL:

`https://bounti.co/`

Selector:

`div#customers`

Reason it mattered:

- dark card on light background
- mobile layout
- customer logo/image cards
- statistic cards with pale/alpha large numbers
- section ordering mattered

Early misses:

- some card ordering was wrong
- logo placement inside boxes was missed
- pale statistic text was not matched

Fixes added to skill:

- preserve original ordering
- preserve alpha text colors
- use computed styles instead of visual guessing
- keep small visual controls and cards even when text extraction is noisy

## Bounti Operations Section

URL:

`https://bounti.co/`

Selector observed from annotation:

`div#main > div.framer-sZkVM.framer-QKmvY:nth-of-type(1) > section.framer-xb5esk`

Reason it mattered:

- large centered headline
- exact line break mattered
- CTA button details mattered
- video/image card surface
- tab bar overlay
- background color was affected by browser annotation overlay

Early misses:

- background looked too blue because screenshot/annotation tint affected visual interpretation
- headline wrapping differed because fallback font and text box width changed line breaks
- CTA button shape and nested arrow box needed more precision

Fixes added to skill:

- use computed background from DOM, not screenshot sampling
- match rendered line breaks
- preserve nested button/icon details

## Dot Cards Product Section

URL:

`https://dotcards.net/products/dot-metal?variant=44754759614639`

Selector:

`section#MainProduct-template--20060300148911__main`

Reason it mattered:

- product hero/detail layout
- color swatches
- option selector cards
- rating/review cluster
- add-to-cart button
- responsive product section variants

Successful Paper captures created:

- `Dot Metal Product - Laptop L - Strict DOM Capture`
- `Dot Metal Product - S24 Ultra - Strict DOM Capture`
- `Dot Metal Product - iPad Air Portrait - Strict DOM Capture`

Effective computed page background:

`#F5F5F7`

Product image URL used:

`https://dotcards.net/cdn/shop/files/metal2_tap_black-min.png?v=13583388470016597441`

Manual review said the captures were very close, with small misses:

- thin divider line between `4.9` star/rating and `7,000+ reviews`
- unselected selector circles inside Double and Pack boxes
- slight shadow below the Add to Cart button
- color swatch shine/shader in the upper-left/diagonal surface

Fixes added to skill:

- preserve tiny separators
- preserve selected and unselected option controls
- preserve box shadows
- inspect pseudo-elements for gradient overlays and blend modes
- recreate swatch shine as overlay circles/clipped overlay frames

## Dot Cards Swatch Shine Finding

The swatch shine was readable from live CSS rather than needing visual guessing.

The relevant structure:

- parent swatch element: `.color-circle`
- pseudo-element: `::before`

Observed behavior:

- circular overlay
- same size or nearly same size as swatch
- diagonal `linear-gradient`
- often `mix-blend-mode: soft-light`
- black swatch used a lower-alpha variation

Implementation lesson:

The extraction must inspect pseudo-elements even when they have no text. Decorative pseudo-elements can carry important surface fidelity.

## Bounti Employee Training Hero/Footer Section

URL:

`https://bounti.co/product/employee-training-platform`

Selector observed from browser comment:

`div#main > div.framer-Dqmvx.framer-0jGo1:nth-of-type(1) > div.framer-d0dh3w:nth-of-type(11)`

Reason it mattered:

- image-led hero with a large rounded photo
- editable headline layered over a decorative SVG word treatment
- CTA button shadow and rounded shape
- footer/newsletter panel overlapping the hero image
- responsive layout changes from desktop footer columns to mobile product cards
- selected root included below-fold content beyond the visible browser marker screenshot

Findings from the test:

- The initial Paper build put overlay surfaces before the full hero image, so the image covered the footer and buttons.
- The skill now says to add full-bleed or section-wide media before overlay surfaces.
- Graphik was unavailable in Paper and Inter was used as fallback.
- Inter fallback changed button label wrapping, so text boxes needed targeted widening while preserving measured button positions.
- Mobile rendered the source text typo `Weclome to the`; the capture preserved the rendered DOM text rather than correcting it.

Skill lesson:

When a browser comment selector captures a broad DOM root, report that breadth and preserve the measured root unless the user explicitly wants a narrower visual slice.
