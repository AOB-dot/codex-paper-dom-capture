# New Chat Handoff Prompt

Paste this into a new Codex chat inside the `Codex Paper DOM Capture` project folder.

---

We are developing the `capture-paper-dom` Codex skill as an open-source Codex-to-design-canvas DOM capture workflow.

Project goal:

Develop, document, harden, and publish a Codex workflow that captures selected sections from the Codex in-app browser into editable Paper.design frames with very high visual fidelity across laptop, mobile, and tablet breakpoints.

Context:

This began inside a private design-engineering workflow where commercial DOM capture tools were not precise enough. Paper.design browser capture and Magicpath AI-style extensions were useful but missed details such as computed backgrounds, responsive ordering, pseudo-elements, tiny controls, shadows, gradients, SVG references, and text wrapping.

The discovery was that Codex's in-app browser plus Paper MCP can act as an inspectable capture loop: Codex controls viewport size, reads live computed DOM styles, inspects pseudo-elements, captures responsive variants, reasons over missed details, and writes directly into Paper as editable layers.

Current skill:

`capture-paper-dom/SKILL.md`

Please first read:

- `README.md`
- `docs/origin-and-context.md`
- `docs/current-skill-contract.md`
- `docs/fidelity-checklist.md`
- `docs/test-cases.md`
- `docs/roadmap.md`
- `capture-paper-dom/SKILL.md`

Important defaults:

- Laptop L: `1440 x 900`
- Samsung Galaxy S24 Ultra: `430 x 932`
- iPad Air portrait: `820 x 1180`
- optional iPad Air landscape: `1180 x 820`

Known public test URLs:

- Dot Cards product: `https://dotcards.net/products/dot-metal?variant=44754759614639`
- Bounti homepage: `https://bounti.co/`

Known Dot Cards selector:

`section#MainProduct-template--20060300148911__main`

Known Bounti Customers selector:

`div#customers`

Known Bounti Operations selector:

`div#main > div.framer-sZkVM.framer-QKmvY:nth-of-type(1) > section.framer-xb5esk`

Important lessons already learned:

- Do not sample screenshot colors when browser annotation overlays are visible; use computed backgrounds.
- Preserve tiny visual controls such as 1px separators and empty radio circles.
- Preserve `box-shadow`, `filter`, opacity, gradients, and blend modes.
- Inspect `::before` and `::after` pseudo-elements, including decorative ones with no text.
- Color swatches can have shine/shader overlays implemented as pseudo-element gradients.
- Font fallback in Paper can change line breaks; match rendered wrapping intentionally.
- Keep captures editable in Paper; screenshots are only QA/reference unless explicitly requested.

Current near-term task:

Keep improving the skill from real capture work while preserving privacy. Public docs and fixtures should avoid private project names, local filesystem paths, personal information, and proprietary design details.

---
