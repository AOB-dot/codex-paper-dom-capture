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

## Dot Header Boundary Discipline

URL:

`https://dotcards.net/`

Selector:

`#shopify-section-header`

Reason it mattered:

- self-directed capture chose the correct closed header root but added a black rounded slice from the hero below as "source context"
- the adjacent hero pixels were visible in the screenshot but were not part of the header component
- mobile/tablet closed headers also tempted the capture to include the first visible hero edge below the sticky tray
- the same page exposes off-canvas menu and drawer DOM inside or near the header subtree, so component/state boundaries must be explicit

Skill lesson:

For self-directed component captures, crop the Paper artboard to the selected root/state boundary. Do not include adjacent sibling sections, hero beginnings, previous-section tails, or comparison context as editable Paper layers unless the requested capture explicitly names a combined transition. Keep adjacent pixels only in source screenshots/notes for QA.

Regression check:

- Extract root rect and previous/next sibling rects at each breakpoint.
- If the header is fixed/sticky or the DOM root is taller than the painted tray, capture the painted tray/header surface as the artboard boundary.
- Paper QA fails if even a thin black hero strip appears under the closed header. The fix is to adjust selector, artboard height, clipping, or root/state boundary before moving on.

## Dot Menu State Availability

URL:

`https://dotcards.net/`

Observed behavior:

- Desktop `Shop` is a normal link to `/collections/basics`; hover did not reveal a mega menu and click navigated to the collection page.
- Mobile and tablet hamburger controls open a translucent menu surface with `Shop`, `Packs`, `Custom`, and `Platform` rows plus nested product cards.
- Product-page desktop `Packs` hover opens a full dropdown state: the fixed header grows to a rounded white tray, the background page is dimmed/blurred, Packs receives the active underline, and the dropdown shows a `SAVE UP TO 25% / Buy in Bulk and Save` promo card plus visible `dot.bundle`, `dot.duos`, and `dot.cards` product cards.

Skill lesson:

Interactive capture plans must verify state availability per breakpoint and per nav item. If the requested state does not exist on one item but does exist on another, record that distinction. CSS inspection alone is not enough for hover states; use a hover-capable verification path and capture the full post-hover state before drawing.

## Reusable Library Scaffold Asset Slots

Source examples:

- Dot cart drawer product cards
- Dot mobile menu product cards
- Bounti image/video-led storytelling cards

Observed workflow need:

- The destination library will replace source-specific logos, media, product renders, SVG wordmarks, and videos with destination-brand content.
- Recreating every source-specific asset exactly slowed the capture without improving the reusable section structure.
- The important reusable value is the measured layout, masks, surfaces, card anatomy, state behavior, and asset slot roles.

Skill lesson:

When the user explicitly asks for a reusable section library scaffold, preserve every measured asset slot but placeholder source-specific brand/media assets. Do not import exact Dot/Bounti logo and product SVG detail unless it is needed to understand the structure. Generic controls, button anatomy, dividers, shadows, card shells, and state layout remain strict DOM capture items.

Follow-up scaffold rule:

Placeholdered design assets need visible source-reference evidence on the Paper canvas without overwhelming the scaffold workflow. Put one labeled screenshot/reference strip near each scaffolded section or repeated card cluster, outside the reusable artboard when possible, so the destination scaffold stays clean while the original source visuals remain inspectable. Add individual close-up tiles only for special source treatments such as logos, unusual media crops, video frames, frosted overlays, masks, or branded icon systems.

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

## Strict vs Placeholder Mode Separation

Source:

`https://dotcards.net/`

Representative selector:

`section#shopify-section-template--20060300673199__home_collection_H3Ry7q`

Scenario:

During a section-library capture marathon, the workflow allowed placeholder/scaffold thinking to bleed into captures where the user wanted exact source DOM fidelity. The user then asked for the Dot `Shop Basics` section as a strict DOM capture while still working inside the broader section-library project.

Expected behavior:

- `$capture-paper-dom` remains strict by default unless the user explicitly asks for placeholders.
- `$capture-paper-dom-strict` forces exact source capture even inside a reusable-library project.
- `$capture-paper-dom-placeholder` is the only wrapper that forces placeholder/scaffold behavior.
- If the user says strict, exact, faithful, clone, or no placeholders, source-specific Dot/Bounti assets must be preserved rather than converted into placeholders.
- If placeholder mode is used, each placeholder requires nearby source-reference evidence.

Skill lesson:

Capture mode must be a first-class gate before extraction. Project context such as "section library" cannot silently override a strict capture request.

## Browser Runtime DOM API Fallback

Source:

`https://dotcards.net/`

Representative selector:

`section#shopify-section-template--20060300673199__home_collection_H3Ry7q > div.presale.presale-home > div.presale-collections > div.presale-collection.basic:nth-of-type(1)`

Scenario:

During a strict Dot `Shop Basics` capture, the in-app browser read-only page scope threw errors for `NodeFilter`, `document.createTreeWalker`, and `document.createRange`.

Expected behavior:

- The extraction does not stop merely because those DOM helpers are unavailable.
- Text traversal falls back to recursive `childNodes` and `nodeType === 3`.
- If `createRange()` is unavailable, rendered text line geometry falls back to visible leaf text element rectangles.
- The completion audit records that line membership used fallback extraction and must be verified visually against source/Paper screenshots.

Skill lesson:

The capture script should use progressive DOM API fallbacks because the Browser plugin page scope can be more restricted than a normal page console.

## Dot Shop Basics: Dense SVG And Hidden Carousel Controls

Source:

`https://dotcards.net/`

Representative selector:

`section#shopify-section-template--20060300673199__home_collection_H3Ry7q > div.presale.presale-home > div.presale-collections > div.presale-collection.basic:nth-of-type(1)`

Findings from the strict capture:

- The Dot product wordmarks and swatch rows were available as inline SVGs with no unresolved `<use>` references.
- Rebuilding those wordmarks as editable text was a strict-mode miss. Dense inline SVG paths should be preserved as SVG layers/assets first.
- The carousel right-arrow controls were present in the DOM with `display:flex`, but computed `opacity:0`. Capturing them as visible grey arrows created extra background arrows in the Paper desktop/mobile frames.
- The initial `1440`, `430`, and `820` browser viewport requests all produced content/root widths that were `15px` narrower because the browser reserved a scrollbar gutter. For target capture widths of `1440`, `430`, and `820`, the in-app browser needed initial requests of `1455`, `445`, and `835`.
- The mobile `Give The Gift Of Networking` card was a special expanded gift-card layout, not a normal product card. It needed a two-line source heading, actual `gift.card` SVG mark, rainbow strip, separate `Starting at`/price spans, and a top-right image crop. Reusing the normal product-card template missed those details.

Expected behavior:

- Strict mode tries direct inline SVG insertion, isolated per-SVG writes, or local SVG asset import before any wordmark/swatch approximation.
- `opacity:0`, `display:none`, `visibility:hidden`, zero-area, clipped, or inactive carousel controls are excluded from visible Paper layers unless the requested state explicitly shows them.
- Capture notes distinguish requested viewport size from measured visual/content/root size. For the standard breakpoints, request `1455`, `445`, and `835` first so the measured content/root widths land at `1440`, `430`, and `820`. If the measured gutter differs, adjust the requested viewport and re-extract instead of stretching an already captured narrower frame.
- Repeated-card QA must branch by card type. Promo/gift/upsell/featured cards inside a product grid get their own internal inventory instead of inheriting the neighboring product-card anatomy.

Skill lesson:

Visible dense SVGs are strict assets, not optional detail. Visibility filters must consider opacity, not only display and nonzero rects. Device request width and root content width need separate accounting, and the browser request should include the measured gutter allowance before extraction. Special promo cards inside repeated grids require their own inventory pass.
