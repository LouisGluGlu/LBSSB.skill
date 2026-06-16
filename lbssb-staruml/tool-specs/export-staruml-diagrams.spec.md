# export_staruml_diagrams.mjs Spec

## Purpose

Export selected StarUML diagrams to PNG and write manifest records.

## CLI

```text
node export_staruml_diagrams.mjs --api http://127.0.0.1:58321 --map diagram-export-map.json --out <output-dir>
```

## Inputs

- API base URL.
- Diagram export map:

```json
[
  {
    "id": "",
    "title": "",
    "type": "",
    "filename": ""
  }
]
```

## Outputs

- PNG files.
- `diagram-manifest.json` or manifest fragment.

## Required Behavior

- Fail if an expected diagram ID cannot export.
- Decode base64 image responses.
- Record source as `staruml-export`.
- Record consistency as `native`.
- Do not guess stale IDs; reread diagram list when export fails.

## Fallback

If the API returns unreadable dark PNGs, use `normalize_png_background.py`. If still unreadable, use `draw_from_plan.py` and mark manifest honestly.
