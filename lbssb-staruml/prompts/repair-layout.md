# Prompt: Repair Layout

```text
Route: repair.

Inputs:
- working .mdj
- diagram IDs/names
- screenshots or exported PNGs
- layout problems

Repair order:
1. Fix semantic errors before visual spacing.
2. Move groups, not isolated nodes, when possible.
3. Keep class diagram domain model central.
4. Route technical dependencies around core areas.
5. Re-export PNG and compare.
6. Update manifest and next-action.

Do not modify the source .mdj directly.
```
