# Ancestor Tree (anc-tree)

Static family-tree viewer built with HTML + Mermaid + CSV.

## What is in this repo

- `index.html`: main page with:
  - multiple Mermaid family subtrees
  - overview map and section navigation
  - searchable table view of `db.csv`
- `db.csv`: people/relationships source data

## Quick start

Because `index.html` fetches `db.csv`, run through a local HTTP server (do not open with `file://`).

### Option 1: Python

```bash
python3 -m http.server 8000
```

Then open:

- `http://localhost:8000/`

### Option 2: Node

```bash
npx serve .
```

Open the URL printed in the terminal.

## Data model (`db.csv`)

Current columns:

- `id`
- `name`
- `dadId`
- `momId`
- `brotherId1`, `brotherId2`, `brotherId3`
- `sisterId1`, `sisterId2`, `sisterId3`

Notes:

- IDs are the relation keys used in parent/sibling fields.
- The page computes and displays a combined `siblings` column in the UI.

## Editing workflow

1. Update `db.csv` first for factual relationships.
2. Update the relevant Mermaid diagram block(s) in `index.html`.
3. Keep names and relationships aligned between diagram labels and CSV rows.
4. Refresh the browser and verify:
   - diagram renders without Mermaid errors
   - section nav/overview links still scroll to the right section
   - CSV search still works

## Mermaid files

At the moment, diagrams are embedded inline in `index.html`.

- External `.mmd` files are not required for runtime.
- If you keep external Mermaid source files in the future, treat them as authoring artifacts only unless you explicitly wire them into the page.

## Known conventions

- Hebrew + English section descriptions are used in most subtree sections.
- Tree display numbering in UI may not match section ID numbers exactly (for example, displayed tree `4` can map to `id="tree-5"`).
- Overview map click targets are mapped in `jumpToTree` inside `index.html`.

## Troubleshooting

- Blank CSV table or fetch errors:
  - ensure you are serving with `http://localhost...` and not `file://`
- Mermaid parse error:
  - check recent edits for unmatched quotes, invalid arrows, or malformed labels in a Mermaid block
- Overview map node does not navigate:
  - verify target IDs exist and mapping in `jumpToTree` is up to date
