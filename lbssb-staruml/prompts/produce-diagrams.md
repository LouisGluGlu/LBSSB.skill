# Prompt: Produce Diagrams

```text
Route: produce_single_diagram or produce_full_project.

Steps:
1. Confirm authorization phrase is satisfied.
2. Load .lbssb and source requirements.
3. Build DiagramPlan and LayoutSpec.
4. Use MCP to update a working .mdj copy.
5. Export PNG.
6. Use draw_from_plan only when PNG is unreadable or StarUML export is unavailable.
7. Write manifest.
8. Run QualityGate.
9. Update .lbssb/next-action.md.

Final status must be Verified, Unverified: <reason>, or Failed: <reason>.
```
