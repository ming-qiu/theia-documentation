# Troubleshooting

Fixes for the messages and situations you're most likely to run into, grouped by where they happen.

## Installation

### "ERROR: Python 3 not found." / "ERROR: Python \<version\> found, but 3.9+ required"

The installer couldn't find a Python 3.9+ interpreter. Install Python from [python.org](https://www.python.org/downloads/), or on Apple Silicon, install Homebrew Python with `brew install python@3.11`, then re-run `install.command`.

### "ERROR: Homebrew is not installed."

You answered yes to letting the installer install ffmpeg, but Homebrew itself isn't present. Either install Homebrew first (the installer prints the official install command), or choose not to auto-install ffmpeg and install it yourself — see the next item.

### ffmpeg not found, and you don't want the installer to install it

Install it yourself with `brew install ffmpeg`, or download a build from [ffmpeg.org](https://ffmpeg.org/download.html), then re-run `install.command`. Frame Counter cannot embed timecode without ffmpeg.

### "ERROR: Failed to create virtual environment" / "ERROR: Failed to install dependencies"

Usually a sign of a broken or unusual Python install. Reinstalling Python via Homebrew (`brew install python`) and re-running `install.command` resolves most of these. If it persists, note the exact error text from the Terminal window — you'll need it if asking for help.

### macOS warns the script is from an "unidentified developer"

Expected, since you downloaded the script yourself rather than installing it from the App Store. Right-click the `.command` file and choose **Open** (rather than double-clicking) — this gives you an explicit "Open anyway" option that a plain double-click doesn't.

## Tools don't appear in Resolve's Scripts menu

1. Confirm the install finished with **"Installation Complete!"** in the Terminal window, without an `ERROR:` line above it.
2. Fully quit and reopen DaVinci Resolve — the Scripts menu is only rebuilt at launch.
3. Confirm you're looking in the right place: **Workspace → Scripts → Edit** (not the Color or Fusion page's Scripts menu — Theia's bridge scripts are installed specifically for the Edit page).
4. If you have multiple macOS user accounts, remember the installer only installs for the account it was run under — see [Multiple users on one machine](installation.md#multiple-users-on-one-machine).

## Could not import DaVinci Resolve API

If Resolve's scripting API isn't enabled, or a tool is run outside of Resolve's Scripts menu (and outside Resolve entirely) without the API initialized, every tool degrades the same way: the window still opens, but anything that needs Resolve fails. You'll typically see one of:

* `⚠️ DaVinci Resolve API not available` in the log.
* `⚠️ Could not connect to Resolve` (Resolve isn't running, or scripting isn't initialized yet).
* `⚠️ No project open` or `⚠️ No timeline open`.

**Fix:** make sure DaVinci Resolve is running, a project and timeline are open, and scripting is enabled per [Step 1 of Installation](installation.md#step-1-enable-resolves-scripting-api). Launching the tool from **Workspace → Scripts → Edit** (rather than double-clicking the `.py` file directly) also ensures Resolve's Python path is set up correctly.

## Clip Inventory

| Message | Meaning / fix |
|---|---|
| "Please specify output file" | The Output File field is empty. Enter a path or use Browse. |
| "Please select at least one track" | Every track checkbox is unchecked. Check at least one. |
| "Please select a subtitle track for VFX shot codes" | "Existing VFX Shot Code" → Subtitle Track is selected, but no track is chosen in the subtitle checklist below it. |
| Thumbnail looks like it's from the wrong clip | See the [Tips](tools/clip-inventory.md#tips) on busy multi-track sections — extremely fast cuts can occasionally grab a neighboring frame even with track soloing. |

## Frame Counter

| Message | Meaning / fix |
|---|---|
| "End frame must be greater than start frame" | Adjust the Frame Range so End > Start. |
| "Please enter a valid FPS value" | Custom FPS field is empty, non-numeric, or zero/negative. |
| "Font file not found: ... Continue with default font?" | The font path doesn't exist. Choosing **Yes** continues with PIL's built-in default font (less polished, but functional); **No** lets you fix the path first. |
| "Please specify an output directory" | The Output Directory field is empty. |

## Add Metadata

| Message | Meaning / fix |
|---|---|
| "Please specify a valid Excel file" | The Excel File path is empty or doesn't exist. |
| "Please enable at least one operation:\n- Enable SRT export, or\n- Enable FCPXML export, or\n- Enable frame counter addition" | All three operation checkboxes are unchecked. Enable at least one. |
| "Please select at least one metadata column to export" | FCPXML or SRT is enabled, but no column is checked in Metadata Columns. |
| "Please specify a valid SRT output directory" / "...FCPXML output directory" | The relevant output directory field is empty or invalid. |
| "Please specify a valid frame counter video file" | Frame Counter is enabled, but the Frame Counter File path is empty or doesn't exist. |
| "Please enter a valid FPS value (must be positive)" | Custom FPS field is empty, non-numeric, or not positive. |
| Go button stays disabled | Record In and Record Out both need to be set under Clip Data Columns — see [Add Metadata's Clip Data Columns](tools/add-metadata.md#clip-data-columns). |
| FCPXML/SRT file comes out empty for a column | Check that the rows you expected actually have that column filled in — empty cells produce no title/subtitle entry. |

## Shot List

| Message | Meaning / fix |
|---|---|
| "Please enter a valid FPS value" | Custom FPS field is empty, non-numeric, or zero/negative. |
| "Please select a Frame Counter Track" | No track is chosen in the Frame Counter Track dropdown. |
| "Please specify an output file" | The Output File field is empty. |
| "Old Shot List file not found" | The path entered under Old Shot List doesn't exist on disk — check it, or clear the field if you don't need the diff. |
| "No clips found on Frame Counter Track \<n\>" | The selected track has no clips — confirm [Add Metadata](tools/add-metadata.md) actually placed frame counter clips there. |
| Metadata looks misaligned between elements and shots | Almost always an EDL/timeline mismatch — see [EDL events are matched by position, not by name or timecode](tools/shot-list.md#track-configuration). Re-export the EDL from the exact cut currently on the track. |

## Still stuck?

Open an issue on the [GitHub repository](https://github.com/ming-qiu/theia/issues) with the exact message text, which tool, and what you were trying to do.
