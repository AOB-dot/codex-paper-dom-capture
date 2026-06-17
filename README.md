# Codex Paper DOM Capture

High-fidelity editable DOM-to-design capture using the Codex in-app browser and Paper MCP.

`capture-paper-dom` is a Codex skill for recreating live webpage sections as editable frames in Paper.design. It uses Codex's controllable in-app browser to inspect the rendered DOM, extract computed styles, and write structured layers into a design canvas instead of flattening the result into a screenshot.

This is version `0.3`: a public skill package with selectable strict and placeholder/scaffold capture modes, documented from real capture work and intended to improve through practical misses and repeatable test cases.

## Why This Exists

The project started during a private design-engineering workflow for a polished e-commerce-style website. The goal was straightforward: collect high-quality website references in a design canvas, then adapt them as editable design material.

Commercial DOM capture tools were helpful, but not precise enough for the level of reuse needed. Paper.design's browser capture workflow and Magicpath AI-style extensions could get the broad shape of a section, but repeatedly missed details that matter in real interface work:

- responsive ordering and exact card/image pairings
- computed ancestor backgrounds
- pseudo-elements
- 1px separators, empty selector circles, badges, and other micro-controls
- box shadows, filters, gradients, opacity, and blend modes
- SVG symbol references and icon details
- image crop and `object-fit`
- rendered text wrapping and font fallback behavior

The useful discovery was that Codex can act less like a one-shot extension and more like a design-engineering inspector. It can control the browser viewport, evaluate live DOM state, read computed CSS, inspect pseudo-elements, compare the result, and then update the workflow from concrete misses.

## Why Codex Browser Plus Paper

Paper is valuable here because its canvas is close enough to code that Codex can create editable frames, text, images, and surfaces through MCP. The idea is not limited to Paper specifically. The same pattern can apply to design tools that expose a structured, scriptable canvas.

The important loop is:

1. Codex controls a real browser viewport.
2. Codex reads the rendered DOM and computed CSS.
3. Codex recreates the section as editable design layers.
4. Codex screenshots the result, compares it with the source, and patches misses.
5. Repeated misses become better extraction and recreation rules.

That feedback loop is the advantage over ordinary capture extensions. The workflow can learn.

## What The Skill Captures

For a selected section in the Codex in-app browser, the skill captures:

- measured layout boxes
- effective ancestor background color
- text content and typography
- images and responsive image sources
- inline SVGs and referenced symbols
- borders, radii, shadows, filters, opacity, transforms, and clipping
- `::before` and `::after` pseudo-elements
- tiny controls and surface details that often get filtered out as "noise"

The final output should be editable Paper layers. Screenshots are used for QA and reference, not as the final deliverable unless explicitly requested.

## Default Device Triad

Unless the user asks otherwise, captures produce three variants:

- Laptop L: `1440 x 900`
- Samsung Galaxy S24 Ultra mobile: `430 x 932`
- iPad Air portrait: `820 x 1180`

iPad Air landscape, `1180 x 820`, can be added when the section is clearly landscape-led.

## Install

Copy the skill folder into your Codex skills directory:

```bash
mkdir -p ~/.codex/skills
cp -R capture-paper-dom ~/.codex/skills/
```

Then start a new Codex session and ask to use `$capture-paper-dom` against a selected browser section.

The root `capture-paper-dom/` folder is the installable Codex skill. Project-level docs, issue templates, and release notes live outside that folder so the skill stays small enough to load efficiently.

## Selectable Capture Modes

The default skill is strict unless placeholders are explicitly requested:

- `$capture-paper-dom`: shared workflow, strict by default.
- `$capture-paper-dom-strict`: force exact source capture with real source images, SVGs, logos, media, and micro-details.
- `$capture-paper-dom-placeholder`: force structure-first scaffold capture for reusable section libraries and future brand replacement. Source-specific assets become measured placeholders with nearby source-reference evidence.

## Requirements

- Codex with the in-app Browser plugin
- Paper MCP connected to a Paper.design file
- A target webpage open in the Codex in-app browser

The skill assumes Paper MCP tools are available for canvas inspection and writes. It also assumes Codex can evaluate the active in-app browser tab for read-only DOM extraction.

## Test Cases

The first public test cases use public websites only:

- Dot Cards product page: `https://dotcards.net/products/dot-metal?variant=44754759614639`
- Bounti homepage: `https://bounti.co/`

See [docs/test-cases.md](docs/test-cases.md) for selectors, observed misses, and the rules added from those misses.

## Privacy Note

This repository intentionally excludes private project names, local filesystem paths, client-specific planning docs, and personal information. The origin story is included because it explains the problem and the workflow, but the public project is generalized around DOM-to-design capture.

## Status

`v0.3` is a working skill package with strict, placeholder/scaffold, and chooser entrypoints. The near-term roadmap is to make captures more repeatable with capture reports, saved style snapshots, and a regression suite around known fidelity traps.

## License

MIT
