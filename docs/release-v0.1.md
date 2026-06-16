# v0.1 Release Notes

`capture-paper-dom` v0.1 is the first public release of the Codex-to-Paper DOM capture workflow.

## Included

- Installable Codex skill folder: `capture-paper-dom/`
- Public origin story and positioning
- Fidelity checklist
- Current skill contract
- Public test-case notes
- Contribution guide
- Capture-miss issue template

## Positioning

The project exists because commercial DOM capture workflows can miss important visual details, especially when a capture needs to stay editable. The v0.1 workflow uses Codex's in-app browser to inspect the live rendered page and Paper MCP to recreate sections as editable design layers.

## Known Limitations

- No automated regression suite yet.
- No reusable extraction script yet; the skill currently describes the workflow for Codex to execute.
- Fidelity still depends on Paper's available fonts and rendering support.
- Canvas, video, WebGL, complex animations, and remote asset failures may require manual notes or fallbacks.

## Next

- Add a standard capture report format.
- Save extracted DOM/style JSON snapshots for test cases.
- Build a regression suite around micro-elements, pseudo-elements, gradients, SVG references, and responsive variants.
