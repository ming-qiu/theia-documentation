# FAQ

### Does Theia work with the free version of DaVinci Resolve?

No. The free version doesn't include Resolve's scripting API, which every Theia tool depends on to read your timeline. You need **DaVinci Resolve Studio**.

### Does Theia work on Windows or Linux?

Not currently — `install.command` and `uninstall.command` are macOS-only shell scripts, and they install into macOS-specific paths (`/Library/Application Support/...`).

### Do I need to know Python or be comfortable with the Terminal to use this?

No. Installing is a double-click (or right-click → Open) on `install.command`, which handles everything else. Day-to-day use is entirely point-and-click windows launched from Resolve's Scripts menu. The only time you'd touch a command line is the optional direct-launch tip in [Quick Start](quick-start.md), which is purely a troubleshooting convenience.

### Do I need to run the tools in a specific order?

For Clip Inventory and Frame Counter, no — both can be run any time. For Add Metadata and Shot List, yes: Add Metadata expects a Clip Inventory-shaped spreadsheet, and Shot List expects a frame-counter track that Add Metadata creates. See [Quick Start](quick-start.md#5-where-to-go-from-here) and the [Workflows](workflows/export-clip-inventory.md) section for the order most editors use.

### Can I rename the columns in my Clip Inventory spreadsheet?

You can rename anything except **Record In** and **Record Out** — Add Metadata auto-detects those two by name (case-insensitive). If you do rename them, you can still pick the right columns manually in Add Metadata's Clip Data Columns dropdowns.

### Why is my Add Metadata export empty for a column I expected data in?

FCPXML/SRT export skips any row where that specific column is empty. Open the spreadsheet and confirm the rows you expected actually have a value typed into that column.

### Why does a thumbnail in my Clip Inventory export look like it's from the wrong clip?

Theia momentarily solos each video track to get a deterministic thumbnail grab, but extremely fast cuts on a busy multi-track section can occasionally still pull a neighboring frame. This is the one output worth a quick visual spot-check after export.

### What happens to dissolves and transitions in Clip Inventory's export?

They're never their own row. A dissolve between two clips becomes a hard cut at its midpoint; a dissolve at the start or end of a clip extends that clip's exported range to cover half the dissolve. See [How occlusion and transitions are handled](tools/clip-inventory.md#how-occlusion-and-transitions-are-handled) for the full explanation.

### Can I run Theia tools more than once against the same project?

Yes, for all four tools. Clip Inventory and Shot List always read live from whatever's currently on the timeline — there's no stale state. Add Metadata can be re-run against the same spreadsheet as you fill in more columns; each run only touches the operations you've enabled.

### Why does Shot List's background/foreground labeling look wrong?

The element labeled `ScanBg` is always whichever EDL-assigned track has the lowest track number — not necessarily whichever track you think of as "background." Put your background plate on the lowest-numbered track you assign an EDL to. See [Shot List's Track Configuration notes](tools/shot-list.md#track-configuration).

### Does updating Theia ever touch my exported files?

No. Re-running `install.command` only touches Theia's own installed program files; it never reads or modifies any `.xlsx`, `.mov`, `.fcpxml`, or `.srt` files you've generated. Same for `uninstall.command` — see [Uninstalling](installation.md#uninstalling).

### Where do I report a bug or request a feature?

Open an issue on the [GitHub repository](https://github.com/ming-qiu/theia/issues).
