# MCP Setup

## Goal

Define how to detect, suggest, register, validate, and degrade StarUML MCP capabilities. Do not install or modify user IDE configuration without explicit authorization.

## Capability Model

Judge MCPs by capability, not by hard-coded server name.

### Read / Validation MCP

Recommended name: `staruml_official`

Minimum capabilities:

- `get_project_info`
- `get_all_diagrams_info`
- `get_diagram_image_by_id`
- `export_diagram` or equivalent image export

Responsibilities:

- Read the open project.
- List diagrams.
- Fetch diagram images.
- Export PNGs.
- Support acceptance validation.

### Edit / Write MCP

Recommended name: `staruml_third_party`

Minimum capabilities:

- `open_project`
- `create_element_with_view`
- `create_edge_with_view`
- `update_element`
- `delete_element`
- `save_project_as`

Responsibilities:

- Open `.mdj`.
- Create diagrams, elements, views, and relationships.
- Modify layout.
- Save a working copy.

## Preflight Before Confirmation Phrase

Before the authorization phrase, only check:

- StarUML process is running.
- `http://127.0.0.1:58321` is reachable.
- `http://127.0.0.1:58322` is reachable.
- Read MCP is exposed.
- Edit MCP is exposed.
- Shell is available.
- Current directory has `mcp/`.

Do not read business diagrams, screenshots, requirements, or `.mdj` contents. Do not write files.

## Missing MCP Options

If no suitable MCP is available, present options:

- A. Install into current project `mcp/`.
- B. Use an existing local MCP and generate registration examples.
- C. Degrade to StarUML HTTP API / extension.
- D. Do read-only analysis.

Without user authorization, do not download, run `npm install`, create `mcp/`, edit `.codex/config.toml`, or edit Claude Code, Trae, WorkBuddy, Hermes, Cursor, or Windsurf configuration.

## Authorized Bootstrap Plan

Use this only after explicit user authorization to bootstrap MCP assets. Before authorization, do not create `mcp/` and do not install packages.

Authorized bootstrap must create or update these project assets:

- `mcp/README.md`: purpose, expected StarUML ports, installed/available MCP routes, verification commands.
- `mcp/mcp-config.example.*`: IDE-specific example configuration only; never overwrite live IDE config.
- `mcp/validate-staruml-mcp.md`: checklist for read, write, save-copy, and PNG export validation.

After install or registration, validate all of:

1. Read project info and diagram list.
2. Create or update a harmless test diagram/element in a working copy.
3. Save a copy with `save_project_as` or equivalent.
4. Export PNG or fetch a diagram image.

If any validation step fails, mark `MCP Unverified: <failed step>` and continue only through an approved fallback route.

## Recommended Project MCP Directory

```text
project/
  mcp/
    staruml-mcp/
    staruml-mcp-server/
    staruml-mcp-extension/
    mcp-config.example.toml
    README.md
```

Configuration snippets are examples only. Do not overwrite real IDE config unless authorized.

## Validation Flow

Minimum successful validation:

1. Open target project or inspect the currently open project.
2. Read project info.
3. Read diagram list.
4. Create/read a small test diagram or verify a known existing diagram.
5. Save a copy, never the source `.mdj`.
6. Export PNG or fetch diagram image.

If any mandatory step fails, mark `MCP Unverified` and choose a fallback path.

## Fallback Order

1. Formal MCP.
2. StarUML HTTP API on `58321`.
3. `staruml-mcp-extension` on `58322`.
4. Local Node/Python scripts.
5. Computer Use / GUI.
6. Read-only analysis.

## IDE Registration Guidance

Supported targets:

- Codex
- Claude Code
- Trae
- WorkBuddy
- Hermes
- Cursor
- Windsurf

For each target, provide an example server entry with command, args, working directory, and environment. Keep examples in `mcp/mcp-config.example.*` unless the user explicitly asks to modify live config.

## Common Failures

- StarUML is not running.
- API server disabled in StarUML settings.
- Multiple StarUML processes point ports to different projects.
- Port `58321` or `58322` is blocked.
- MCP server exposes read tools but no write tools.
- Extension is installed but not enabled.
- Diagram IDs changed after regeneration.
- Export succeeds but image theme is unreadable.

## New Project Check

Run preflight in this order:

```text
check shell
check StarUML process
check 58321
check 58322
list MCP tools
validate read capability
validate write capability
choose route
```
