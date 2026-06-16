# Origin And Context

This project began inside a private design-engineering workflow for a polished e-commerce-style website. The team needed to collect reference sections from high-quality websites, adapt them on a design canvas, and eventually translate the best ideas into a production web app.

The first plan was to use commercial DOM capture tools. Paper.design's own browser capture workflow and Magicpath AI-style extensions were useful starting points, but they struggled with the details that make a captured section trustworthy enough to reuse:

- layout order changed in repeated content
- text wrapping drifted after capture
- subtle backgrounds were sampled from screenshots instead of computed styles
- pseudo-elements disappeared
- small controls such as empty option circles and 1px separators were dropped
- shadows, filters, gradients, and blend modes were flattened or missed
- image crop and SVG references did not always survive

The breakthrough was to use Codex as an active inspector instead of a passive capture tool. Codex can control its own in-app browser viewport, evaluate the live DOM, read computed styles, inspect pseudo-elements, capture responsive variants, and then write directly into Paper through MCP.

## Why The Workflow Is Different

Most DOM capture tools are one-shot transformations. They copy a selected DOM subtree, make a best effort, and leave the user to hand-fix the result.

This workflow is iterative:

1. Capture the selected section from the live browser.
2. Recreate it as editable layers in a structured design canvas.
3. Screenshot the Paper result.
4. Compare against the source.
5. Convert visible misses into improved extraction rules.

That loop matters. A missed swatch highlight can become a pseudo-element rule. A wrong card order can become an ordering rule. A tinted background can become a computed-ancestor-background rule. Over time, the skill becomes better because its failures are inspectable.

## Why Paper, And Why Not Only Paper

Paper is a strong first target because it exposes a code-like design canvas through MCP. Codex can create artboards, frames, text, images, and styled surfaces as editable layers rather than flattening the page into a bitmap.

The broader idea is not Paper-specific. Any design tool with a scriptable canvas and enough layout/style primitives could benefit from the same Codex-controlled browser extraction loop.

## Public Scope

The public project intentionally avoids private product names, personal paths, proprietary planning docs, and client-specific design decisions.

Public examples should use public websites or synthetic fixtures. Private capture work can still inform the skill, but only generalized lessons should be added here.
