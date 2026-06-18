# Native Repair Workflow

Use this after a diagram exists but the exported PNG looks poor.

## Required Loop

1. Export PNG from the native `.mdj`.
2. Inspect the PNG.
3. Identify concrete defects:
   - clipped text;
   - line through text;
   - crossing count too high;
   - missing visual grouping;
   - labels touching borders;
   - diagram too dense for one canvas.
4. Repair using StarUML MCP/API:
   - move views;
   - resize views;
   - route edge points;
   - shorten labels;
   - delete non-essential dependencies;
   - split diagram if required.
5. Save working copy.
6. Export again.
7. Repeat until the diagram passes `visual-quality-gates.md`.

## Forbidden Repair Pattern

Do not call global `layout_diagram` repeatedly and accept the result without inspection.
Do not hide a poor native diagram behind a clean redrawn PNG and call the native diagram optimized.

## Mermaid Imports

Mermaid generation is allowed as a draft accelerator for supported diagram types.
It is not final evidence. A Mermaid-imported diagram must still pass native PNG review and local repair.

## Manifest Evidence

Record:

```json
{
  "engineeringStatus": "Verified",
  "visualStatus": "Verified | Unverified: <reason>",
  "repairPasses": 0,
  "source": "staruml-export"
}
```
