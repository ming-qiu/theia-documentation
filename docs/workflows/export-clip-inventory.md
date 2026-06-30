# Export a Clip Inventory

This is the first step in almost every Theia workflow — it turns whatever's cut on your timeline into a spreadsheet you can hand-annotate with VFX shot codes and other metadata. Everything else in Theia builds on this spreadsheet.

## Before you start

* DaVinci Resolve Studio is open, with the project and timeline you want to export active in the **Edit** page.
* You know which video tracks actually matter — Clip Inventory only looks at tracks you check, and treats unchecked tracks as if they didn't exist (including for occlusion purposes).

## Steps

1. Open **Workspace → Scripts → Edit → 01 Clip Inventory**.
2. In **Video Tracks**, leave everything checked unless you specifically want to exclude a track (for example, a temp music or graphics track that happens to be on a video track). Use **↻** if you opened a different timeline after the window was already open.
3. If your timeline already has shot codes marked some other way — a subtitle track, or duration markers — check **Existing VFX Shot Code** and choose the source. Check **Export VFX shots only** if you want the spreadsheet limited to just those marked clips.
4. Set **Output File**, or leave the default `~/Downloads/clip_inventory.xlsx`.
5. Click **Go** and watch the log. It reports each track as it's processed, and flags clips that were partially or fully occluded by something above them.
6. When the success dialog appears, click **Open File** to jump straight to the spreadsheet.

## What you get

One row per visible clip range: thumbnail, reel name, cut order, Record In/Record Out timecode, duration, and source in timecode. See [Clip Inventory](../tools/clip-inventory.md#what-ends-up-in-the-spreadsheet) for the full column reference, and how dissolves and multi-track occlusion get folded into clip ranges.

## Next: fill in your metadata

Open the spreadsheet and type your own data into the empty columns after Source In (and after VFX Shot Code, if that column is present) — shot codes, vendor assignments, descriptions, whatever your pipeline tracks. Don't rename **Record In** or **Record Out**; later tools auto-detect those columns by name.

From here:

* Need frame-numbered reference video for vendors? → [Generate Frame Counters](generate-frame-counters.md)
* Ready to push your shot codes back onto the timeline, or export FCPXML/SRT files? → [Add Metadata to a Timeline](add-metadata-to-timeline.md)
