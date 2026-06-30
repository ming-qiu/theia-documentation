# Updating Screenshots

Each tool page embeds a screenshot of that tool's main window. This page is the reference for retaking one when a tool's interface changes.

## Current files

| File | Used on | What it shows |
|---|---|---|
| `clip-inventory-main.png` | [Clip Inventory](../tools/clip-inventory.md) | The main window with tracks listed and a completed export logged. |
| `frame-counter-main.png` | [Frame Counter](../tools/frame-counter.md) | The main window with default values. |
| `add-metadata-main.png` | [Add Metadata](../tools/add-metadata.md) | The main window after loading a real spreadsheet, with Clip Data Columns and Metadata Columns populated. |
| `shot-list-main.png` | [Shot List](../tools/shot-list.md) | The main window with track EDL fields filled in. |

## How to capture a replacement

1. Open the tool from Resolve's Scripts menu as normal.
2. Fill in a few representative fields (not just defaults) so the screenshot shows the window doing something, not an empty form.
3. Use macOS's window screenshot shortcut — **⇧ Cmd 4**, then **Space**, then click the window — to capture just the window with its drop shadow, rather than the whole screen.
4. Save as a `.png`, named exactly as shown in the table above — this overwrites the existing file.

## Replacing the file

1. Save the new `.png` into `docs/assets/screenshots/` in this folder, using the exact filename from the table (overwriting the old one).
2. Nothing else needs to change — each tool page already points at that filename.
3. Rebuild or refresh the site locally (`mkdocs serve`) to confirm the new image renders before committing.

There's no dependency between the four images — retake just the one tool's screenshot whose interface changed.
