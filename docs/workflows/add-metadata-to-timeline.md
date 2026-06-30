# Add Metadata to a Timeline

This is the workflow that turns a filled-in spreadsheet back into something usable inside Resolve — a frame counter track for [Shot List](../tools/shot-list.md) to read, and/or FCPXML/SRT files you can import as titles or subtitles.

## Before you start

You need:

* A [Clip Inventory](export-clip-inventory.md) spreadsheet with your metadata filled in — at minimum a VFX shot code column, if you're placing frame counters.
* The same timeline open in Resolve that the spreadsheet was exported from (or one with matching Record In/Out ranges).
* If you're placing frame counters: a rendered video from [Generate Frame Counters](generate-frame-counters.md).

## Steps

1. Open **Workspace → Scripts → Edit → 03 Add Metadata**.
2. Set **Excel File** to your filled-in spreadsheet. Theia reads the header row and populates everything below automatically.
3. Check **Clip Data Columns** — **Record In** and **Record Out** should auto-select if you didn't rename those columns. If they didn't, pick them manually; **Go** stays disabled until both are set.
4. Decide which operations you need, and enable any combination of the three:
    * **Frame Counter** — check **Add frame counter videos to timeline**, point **Frame Counter File** at your rendered `.mov`, set **Starting Frame Number** to match what you used in Frame Counter (default 1001), and choose the **VFX Shot Code Column**. This places one named frame-counter clip per shot (skipping rows with no shot code) on a new video track.
    * **FCPXML Titles** — check **Export metadata to FCPXML title files**, and choose an **Output Directory**. One `.fcpxml` file is written per checked column in **Metadata Columns**.
    * **SRT Subtitles** — same idea, one `.srt` file per checked column.
5. In **Metadata Columns**, check whichever columns should be exported by FCPXML/SRT (this has no effect on the Frame Counter operation).
6. Confirm **Set Frame Rate** matches your timeline.
7. Click **Go**.

## What you get

* If Frame Counter was enabled: a new video track on your open timeline, with one frame counter clip per shot, named by VFX shot code. **This track is what [Shot List](../tools/shot-list.md) reads as its "Frame Counter Track."**
* If FCPXML/SRT were enabled: one file per checked column, in your chosen output directory, named after the column (e.g. `VFX Shot Code.fcpxml`).

## Importing FCPXML/SRT back into Resolve

In Resolve's Media page, import the `.fcpxml` or `.srt` file like any other media, then drag it onto a new track in your timeline. FCPXML imports as Resolve title clips; SRT imports as a subtitle track. Either way, the clips will already be timed to match the Record In/Out ranges of the rows you exported.

## Next: build a shot list

Once the frame counter track exists on your timeline, head to [Export a Shot List](export-shot-list.md).
