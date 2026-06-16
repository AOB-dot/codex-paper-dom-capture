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
- A later fidelity review found the first capture was still too simplified in the final CTA/footer blend:
  - newsletter helper text wrapped even though the source was one line
  - the CTA button missed its nested diagonal arrow box
  - the Bounti logo was missing because the SVG symbol reference was not resolved
  - footer heading weights looked too light because the fallback used computed `400` instead of the family-name weight
  - Company, Industries, Security, and their items were omitted
  - the bottom hairline divider was omitted
  - Imprint and Privacy Policy were darker than the copyright text but were not separated correctly
  - X and LinkedIn belonged on the right edge, not next to the legal links
  - the gap between the decorative `excellence` word treatment and CTA was too large

Skill lesson:

When a browser comment selector captures a broad DOM root, report that breadth and preserve the measured root unless the user explicitly wants a narrower visual slice.

Strict capture must use a layer inventory rather than a manual simplification pass. Dense footer sections need explicit checks for logos, SVG `<use>` symbols, button anatomy, column completeness, single-line text, legal/social alignment lanes, hairline dividers, and fallback font weights.

## Bounti Training Management Benefits Cards

URL:

`https://bounti.co/solutions/uses/training-management-software`

Selector observed from browser comment:

`div#main > div.framer-NckkP.framer-tibgww:nth-of-type(1) > div.framer-1iwvcmh:nth-of-type(5)`

Reason it mattered:

- rounded benefits section with centered heading and bullet list
- horizontally overflowing card carousel on laptop/tablet
- stacked card layout on mobile
- title chips over media/cards
- card-specific image crops
- floating callouts inside cards, including a sent-to style box over the automations image
- translation card with language selectors, divider, overlay panel, and multiple small SVG/icon details

Misses found in the first capture:

- Laptop title chips such as `Personalised learning paths` were visually off in placement.
- The automations card background image crop/placement was off.
- The sent-to box over the automations image was missing.
- `Automatically translate courses to multiple languages for a diverse audience.` wrapped to three lines in Paper, while the source rendered it as two lines.
- Dense vector/pill content inside a card was simplified without enough up-front reporting.

Skill lesson:

Section-level inventory is not enough for repeated marketing cards. The skill must run a card-internal fidelity gate that checks media crop/object-position, title-chip coordinates, overlay callouts, language/progress controls, line counts for descriptions, and visible carousel edge crops.

Misses found in the follow-up laptop-only capture:

- The main heading had the same number of lines, but the word `Training` moved from the end of the first line to the beginning of the second line.
- The card label chips were rendered as title case in Paper even though the source visual used uppercase labels.
- The card label chips lost the blurred/frosted iced surface treatment and looked like plain flat translucent boxes.
- The automations card image still had incorrect visible subject placement after copying the source image URL and CSS object-position.

Additional skill lessons:

- Text QA must compare per-line word membership, not only the number of rendered lines.
- The extractor must preserve rendered casing and `text-transform`, especially for chips, labels, nav items, and card labels.
- Frosted/glass chips require explicit extraction of alpha fills, gradients, filters, backdrop filters, borders, shadows, and pseudo-elements.
- Media crop QA needs source-vs-Paper visual comparison. Copied `object-fit`/`object-position` values are not sufficient if Paper renders the asset crop differently.
- The capture is not complete until the final Paper screenshot is compared against the live source at the same viewport and the mismatches are either fixed or reported.
