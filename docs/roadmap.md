# Roadmap

## Phase 0: Publish The Working Skill

- Package the current `capture-paper-dom` skill in an installable folder.
- Document setup requirements without local machine paths.
- Document known test cases using public websites or synthetic fixtures.
- Preserve lessons from real capture work without naming private projects.

## Phase 1: Make Captures Repeatable

- Create a standard capture report format.
- Record source URL, selector, viewport, timestamp, and effective background.
- Record unavailable fonts and fallbacks.
- Record known limitations per capture.
- Save extracted DOM/style JSON snapshots for test cases when possible.

## Phase 2: Improve CSS Fidelity

Focus areas:

- pseudo-elements
- gradients
- `box-shadow`
- `filter`
- `backdrop-filter`
- `mix-blend-mode`
- transforms
- masks and clipping
- SVG symbol references
- icon fonts
- CSS variables
- responsive image `srcset`

## Phase 3: Build A Regression Suite

Create repeatable tests around:

- public e-commerce product sections
- public SaaS/customer sections
- product option cards and color swatches
- nav menus and hover states
- cart drawers
- mega menus
- sticky headers
- mobile accordions
- synthetic fixtures for hard CSS cases

The test suite should compare:

- extracted style JSON
- expected layer inventory
- screenshot similarity
- known micro-elements checklist

## Phase 4: Package For Open Source

Add or expand:

- examples folder
- screenshots folder
- before/after gallery
- installation instructions
- Paper MCP setup notes
- Browser plugin setup notes
- contribution guide
- issue templates for missed CSS/features

## Phase 5: Developer Program Story

Shape the public narrative:

- Problem: designers and builders need editable high-fidelity captures, but browser extensions and AI capture tools miss details.
- Solution: Codex uses controlled browser inspection plus design-canvas MCP writes to create editable responsive captures.
- Proof: real-world captures from public sites and privacy-safe private workflow lessons.
- Value: Codex can be a design-engineering bridge, not only a coding assistant.
