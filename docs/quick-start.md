# Quick Start

This is the fastest path from a freshly installed Theia to your first exported spreadsheet. It assumes you've already finished [Installation](installation.md).

## 1. Open a timeline

In DaVinci Resolve, open the project and timeline you want to export. Theia reads whatever timeline is currently active in the **Edit** page.

## 2. Launch a tool

Every Theia tool lives in the same place:

**Workspace → Scripts → Edit → [Tool Name]**

Click **01 Clip Inventory** to start. A standalone window opens — this is a normal Mac app window, not part of Resolve, so you can move it, resize it, or put it on a second monitor while you keep working in Resolve.

!!! tip
    You can also run any tool directly from Terminal without going through Resolve's menu, which is occasionally useful for troubleshooting:
    ```bash
    "/Library/Application Support/Theia/venv/bin/python3" \
      "/Library/Application Support/Theia/clip_inventory_gui.py"
    ```

## 3. Export your first clip inventory

1. Theia automatically lists the video tracks from your open timeline as checkboxes, all checked by default.
2. Leave them all checked for now (or uncheck any tracks you don't want included — see [Clip Inventory](tools/clip-inventory.md) for details on what each option does).
3. Set **Output File** to wherever you'd like the spreadsheet saved (it defaults to `Downloads/clip_inventory.xlsx`).
4. Click **Go**.
5. Watch the log panel — it reports track-by-track progress and flags anything occluded by clips above it.
6. When it finishes, click **Open File** in the success dialog to view it immediately in Excel (or your default spreadsheet app).

You now have a spreadsheet with one row per visible clip: a thumbnail, reel name, cut order, Record In/Out, duration, and Source In timecode.

## 4. Add your own metadata

Open the exported spreadsheet and start typing in the empty columns from **column H onward** — VFX shot codes, vendor assignments, shot descriptions, whatever your pipeline needs. Theia never touches columns to the left of H; that's reserved for the clip data it generated.

## 5. Where to go from here

That single spreadsheet is the seed for everything else in Theia:

* Want frame-numbered reference video for VFX vendors? See [Frame Counter](tools/frame-counter.md).
* Want to push your shot codes back onto the timeline as a track, or export FCPXML/SRT files from your metadata? See [Add Metadata](tools/add-metadata.md).
* Want a structured shot list (in/out frames, handles, retimes) for bidding or tracking? See [Shot List](tools/shot-list.md) — but read [Export a Clip Inventory](workflows/export-clip-inventory.md) and the workflow pages first, since Shot List depends on a frame counter track that Add Metadata creates.

The [Workflows](workflows/export-clip-inventory.md) section walks through each of these end-to-end, in the order most editors use them.
