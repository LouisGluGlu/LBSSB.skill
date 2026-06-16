# draw_from_plan.py Spec

## Purpose

Render clear white-background PNGs from a structured diagram plan when StarUML export is unavailable or visually unacceptable.

## CLI

```text
python draw_from_plan.py --plan diagram-plan.json --theme layout-theme.json --out <output-dir>
```

## Inputs

- `diagram-plan.json`: project and diagram data.
- `layout-theme.json`: visual theme, fonts, spacing, line style.

## Outputs

- `<output-dir>/*.png`
- `<output-dir>/README.md`
- `<output-dir>/diagram-manifest.json`

## Supported Types

- `class`: classes, attributes, operations, relationships, multiplicities.
- `sequence`: participants, messages, returns, alt blocks.
- `communication`: objects, numbered messages, branch labels.
- `activity`: actions, decisions, merges, start/end, lanes.

## Required Behavior

- Never modify `.mdj`.
- Use deterministic layout from plan/theme.
- Keep text readable.
- Record manifest source as `draw_from_plan`.
- Mark consistency as `semantic-consistent` unless native parity is verified.

## Worth Extracting From Existing Prototype

From `test/draw_clear_uml.py`:

- font loading fallback
- class box drawing
- sequence lifeline drawing
- communication object/message drawing
- activity action/decision drawing
- README/manifest generation

Replace hard-coded business data with JSON/YAML input.
