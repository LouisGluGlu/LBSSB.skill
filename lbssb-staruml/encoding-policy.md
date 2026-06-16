# Encoding Policy

## 1. Default Encoding Contract

All text files created by this Skill must use UTF-8.

Applies to:

- `.md`
- `.json`
- `.toml`
- `.yaml`
- `.mjs`
- `.js`
- `.py`
- `.txt`
- `.lbssb/*`
- generated README / manifest / reports

StarUML `.mdj` files must be treated as UTF-8 JSON-like project files unless proven otherwise.

## 2. Do Not Guess Silently

If reading a file fails because of encoding, do not silently corrupt content.

Use this order:

1. Try UTF-8.
2. Try UTF-8 with BOM.
3. Try GBK / CP936 only for legacy Chinese files.
4. If still unreadable, mark `Encoding Unverified` and ask for confirmation.

Never rewrite the source file just to fix encoding.

## 3. Source File Safety

Do not normalize or rewrite original user files.

Allowed:

- read source file
- copy source file to working copy
- write UTF-8 outputs

Forbidden:

- convert original `.mdj`
- convert original `.docx`
- convert original `.md`
- convert original screenshots
- overwrite source files because of encoding errors

## 4. Python Rules

Always read/write text files with explicit encoding:

```python
from pathlib import Path

text = Path(path).read_text(encoding="utf-8")
Path(path).write_text(text, encoding="utf-8")
```

If uncertain:

```python
def read_text_safe(path):
    from pathlib import Path
    p = Path(path)
    for enc in ("utf-8", "utf-8-sig", "gbk", "cp936"):
        try:
            return p.read_text(encoding=enc), enc
        except UnicodeDecodeError:
            continue
    raise UnicodeDecodeError("unknown", b"", 0, 1, f"Cannot decode {path}")
```

When writing JSON:

```python
import json
Path(path).write_text(
    json.dumps(data, ensure_ascii=False, indent=2),
    encoding="utf-8"
)
```

## 5. Node.js Rules

Always specify UTF-8:

```js
const fs = require("fs");

const text = fs.readFileSync(filePath, "utf8");
fs.writeFileSync(filePath, text, "utf8");
```

When writing JSON with Chinese:

```js
fs.writeFileSync(
  filePath,
  JSON.stringify(data, null, 2),
  "utf8"
);
```

Do not use Buffer-to-string defaults without checking.

## 6. PowerShell Rules

Before running scripts involving Chinese paths or output, set UTF-8 output:

```powershell
[Console]::OutputEncoding = [System.Text.UTF8Encoding]::new()
$OutputEncoding = [System.Text.UTF8Encoding]::new()
```

When reading/writing files:

```powershell
Get-Content -Raw -Encoding UTF8 path
Set-Content -Encoding UTF8 path value
```

If using Windows PowerShell 5.1, note that its encoding behavior may differ from PowerShell 7.

Prefer PowerShell 7 when available.

## 7. Path Safety

Chinese paths are allowed.

Rules:

- Use quoted paths.
- Use `Path` / `pathlib` / Node `path` APIs.
- Do not manually concatenate paths with raw backslashes.
- Do not assume ASCII-only paths.
- Do not rename user folders to English automatically.

Good:

```python
from pathlib import Path
out = Path("作业2") / "系统类图.png"
```

Bad:

```python
out = "作业2\\系统类图.png"
```

## 8. Markdown Encoding Marker

For generated Markdown files, add this comment at the top when appropriate:

```md
<!-- encoding: UTF-8 -->
```

This marker is only a human/agent hint. The actual file must still be written as UTF-8.

## 9. JSON / MDJ Marker

Do not add comments to JSON or `.mdj`.

Instead, record encoding assumptions in:

```text
.lbssb/encoding.md
```

or:

```text
.lbssb/toolchain.md
```

Example:

```md
# Encoding

- Markdown outputs: UTF-8
- JSON outputs: UTF-8, ensure_ascii=false
- StarUML `.mdj`: treated as UTF-8
- Legacy fallback: GBK/CP936 only for read-only recovery
```

## 10. Preflight Encoding Check

Before major execution, check:

- current working directory contains Chinese characters or spaces
- source `.mdj` can be read safely
- `.lbssb/` files can be written as UTF-8
- Node/Python scripts can handle Chinese output paths
- PowerShell output encoding is set if PowerShell is used

Compact output:

```text
Encoding check:
- source mdj:
- output dir:
- shell UTF-8:
- node UTF-8:
- python UTF-8:
- status: Verified / Unverified
```

## 11. Failure Labels

Use these labels:

```text
Encoding Verified
Encoding Unverified: <reason>
Encoding Failed: <reason>
```

Do not continue destructive operations if encoding is failed.
