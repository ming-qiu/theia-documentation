# Export a VFX Shot List

The last step in the chain: turning a timeline that already has a frame counter track into a structured shot list, with work/scan handles, retime and reposition flags, and (optionally) a diff against a previous version.

## Before you start

You need a timeline with a frame counter track already placed by [Add Metadata](add-metadata-to-timeline.md) — Shot List reads its shot boundaries and shot codes from that track's named clips, not from any spreadsheet. You'll also want EDLs exported for each plate track you want included (background and any foreground elements), from the exact same cut that's currently on the timeline.

## Steps

1. Export an EDL per relevant track from Resolve's **Deliver** page (or wherever you normally export EDLs), one for the background plate track and one for each foreground/element track you want broken out.
2. Open **Workspace → Scripts → Edit → 04 Shot List**.
3. Set **Frame Counter Track** to the track Add Metadata placed.
4. For each plate track, browse to its matching EDL in the **Track Configuration** rows. Leave any track blank to exclude it.
    !!! warning
        Put your background plate on the lowest-numbered track you assign an EDL to — that track is always treated as the background (`ScanBg`) for editorial name and source timecode purposes. See [Shot List](../tools/shot-list.md#track-configuration) for the full naming rule.
5. Optionally set **Sequence Name** if you want to override the name Theia derives from each shot code.
6. If you have a previous shot list export and want a frame-change diff, browse to it under **Old Shot List**.
7. Set **Work Handle** and **Scan Handle** (defaults 8 and 24).
8. Confirm **Frame Rate** matches the timeline.
9. Set **Output File**, then click **Go**.

## What you get

A two-sheet spreadsheet:

* **Shots** — one row per shot, with cut order, editorial name, shot code, work/cut in-out, duration, retime flags, and (if you supplied an old shot list) a `Change to Cut` column.
* **Elements** — one row per plate per shot, with source timecode/frames, scan handles, retime percentages, and any scale/reposition applied.

See [Shot List](../tools/shot-list.md#what-ends-up-in-the-spreadsheet) for the full column reference, and [the Change to Cut diff](../tools/shot-list.md#the-change-to-cut-diff) for exactly how frame changes are reported.

## Re-running after a recut

Keep each export. When the cut changes, re-run [Add Metadata](add-metadata-to-timeline.md)'s Frame Counter step against the updated timeline, then run Shot List again with the previous export set as **Old Shot List** — the `Change to Cut` column will flag exactly which shots moved and by how many frames, ready to send to vendors.
