---
name: capture-paper-snapshot-repair
description: Use when the user asks Codex to fix, repair, QA, clean up, or perfect an existing Paper Snapshot, MagicPath, imported webpage capture, or AI-generated design-tool snapshot by comparing it against the live source in the Codex in-app browser or Playwright and patching the Paper frame.
---

# Capture Paper Snapshot Repair

Read and follow the shared contract in `../capture-paper-dom/SKILL.md`, then force **Snapshot Repair Mode**.

This wrapper exists so the user can choose a repair workflow directly from the slash/skill picker when a Paper Snapshot, MagicPath-style import, or other design-tool capture is already on the canvas but contains conversion artifacts.

## Required Override

- Start from the selected Paper frame or the user-named Paper frame, not from a blank recreation, unless repair would be slower or less faithful than rebuilding.
- Use the live source page as ground truth. Open or reuse the matching source URL in the Codex in-app browser. Use Playwright as a backup when hover states, snapshots, or browser evaluation fail in the in-app browser.
- Keep the existing Paper capture's useful structure, images, and layer grouping when they are already correct. Patch only the mismatched areas unless the user asks for a full rebuild.
- Identify snapshot/import artifacts before editing:
  - inline text fragments stacked vertically instead of flowing as one line
  - superscript, footnote, legal, trademark, or financing markers (`†`, `‡`, `§`, `±`, `™`, `®`, etc.) detached into their own line or node instead of staying attached to the preceding word, sentence, or price
  - aggregate text boxes created from multiple source items
  - missing tiny controls, hairlines, badges, stars, separators, or radio/check circles
  - unresolved SVG wordmarks, icons, or `<use>` references
  - wrong media crop, object position, clipping, or card edge crop
  - closed or narrow carousel labels spilling into neighboring label lanes instead of clipping at the source boundary
  - flattened or simplified glass/blurred/frosted surfaces
  - adjacent section contamination from sloppy component boundaries
  - hidden off-state controls made visible
  - hover/open state captured as the default state
- For each artifact class, compare the selected Paper frame against the live DOM and a same-viewport source screenshot before patching.
- Preserve the user's intended mode:
  - If the selected frame is a strict capture, repair toward strict source fidelity.
  - If the selected frame is a placeholder/scaffold capture, repair measured structure and placeholders while preserving source-reference evidence.
- For broken text fragments, inspect the rendered source text, expected line count, font styles, and measured text box width. Replace stacked fragments with editable no-wrap or explicitly wrapped text that matches the source line membership. When a marker is detached, join it back into the preceding editable text run, then remove or hide the orphan marker node so it does not remain as a stray line.
- For source text that is supposed to clip inside a closed card, tab, or narrow carousel lane, wrap the text in a measured `overflow:hidden` frame and hide or remove spill-prone imported text nodes. Do not count a Paper text-node width as sufficient until the screenshot proves clipping.
- For card and carousel repairs, check each distinct card type, including off-artboard cards that remain inside the selected frame.
- For interactive-state repairs, restore the real state first in the browser. Do not infer hover/menu/dropdown content from CSS alone.
- After each meaningful patch, screenshot the Paper frame and compare it against the live source at the same viewport and scroll position.
- Name repaired outputs or notes with `Snapshot Repair` when creating a new comparison frame. If editing in place, add the repair mode to the completion audit.
- In the Skill Compliance Audit, state that Snapshot Repair Mode was used, list the repaired artifact classes, and confirm whether the repair was in-place or a new comparison frame.
