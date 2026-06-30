# Generate Frame Counters

Frame Counter renders the burned-in reference video that VFX vendors use to confirm exactly which frame they're looking at. It's standalone — it doesn't read your timeline or your Clip Inventory spreadsheet — so you can run it any time, independently of where you are in the rest of the pipeline.

## Before you start

Decide what frame rate you'll be counting against. This needs to match the timeline (and the spreadsheet metadata) you'll eventually use this video with — see [Add Metadata to a Timeline](add-metadata-to-timeline.md), which is the next step for most people.

## Steps

1. Open **Workspace → Scripts → Edit → 02 Frame Counter**. No timeline needs to be open.
2. Set **Video Size** — the default 200×80 burn-in box works well as a composited overlay; size up if you need it more readable or full-frame.
3. Set **Frame Range** — Start and End frame numbers. Pick a range comfortably wider than you currently expect; re-running later with a wider range is cheap, but matching an existing video's frame numbering after the fact is not.
4. Set **Frame Rate** to match your timeline.
5. Leave **Font** on the bundled default unless you have a reason to change it.
6. Set **Output Directory**, or leave the default `~/Downloads/frame-counters`.
7. Click **Go**. The log shows two passes: rendering the per-frame images and encoding them, then re-wrapping the result to embed the starting timecode.

## What you get

A single file named `frame_counter_<fps>fps.mov` (for example `frame_counter_24fps.mov`) in your output directory, with the frame range and rate you chose, and the correct timecode embedded starting at your chosen Start frame.

## Next: place it on the timeline

Hand this file to [Add Metadata](../tools/add-metadata.md) as the **Frame Counter File** — see [Add Metadata to a Timeline](add-metadata-to-timeline.md) to place individually-named copies of it on your timeline, one per shot, ready for [Shot List](../tools/shot-list.md) to read later.
