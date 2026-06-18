# Layout Rules

## General

- White background, dark lines.
- Text must not overlap lines or borders.
- Key elements must not be clipped.
- Prefer stable grouped layout over scattered manual moves.
- Build a LayoutPlan before drawing complex diagrams.
- Use global auto-layout only for drafts; final diagrams require local repair.
- Export PNG after pilot/high-risk diagram before batch generation.

## Required Visual Status

Each diagram must record:

- engineeringStatus:
- visualStatus:
- repairPasses:
- sourcePreservationStatus:

## Diagram-Specific

- Use case: group by business module; actor lines connect to main use cases; include/extend stays close to base use case.
- Class: preserve source identifiers; role inheritance top; core domain center; support classes on edges.
- Sequence: stable participant order; visible branch frames; message spacing checked after export.
- Activity: clear main direction; guards on decisions; no line crossing action text.
- Communication:
- State: short transition labels; state boxes sized for text; no label overlap.
- Component:
- Deployment:
