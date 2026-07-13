# Installation

A single installer handles both parts of Theia: a Python environment and GUI scripts under `/Library/Application Support/Theia`, and a set of small "bridge" scripts that tell DaVinci Resolve how to launch each tool from its Scripts menu.

## Prerequisites

Before you run the installer, make sure you have:

| Requirement | Notes |
|---|---|
| **macOS** | The installer is macOS-only. |
| **DaVinci Resolve Studio** | The free version of Resolve does not include the scripting API that Theia depends on. |
| **Python 3.9 or newer** | On Apple Silicon Macs, Homebrew Python is recommended (`brew install python`). |
| **ffmpeg** | Used by Frame Counter to embed timecode metadata. The installer can install this for you via Homebrew if it's missing. |

## Step 1: Enable Resolve's scripting API

Theia talks to Resolve through its scripting API, which needs to be set up once per machine:

1. Open DaVinci Resolve.
2. Go to **Help → Documentation → Developer**.
3. In the folder that opens, find the **Scripting** folder and follow the instructions in its `README.txt`.

Look for this part:
```
...
You may need to set the these environment variables...
    Mac OS X:
    RESOLVE_SCRIPT_API="/Library/Application Support/Blackmagic Design/DaVinci Resolve/Developer/Scripting"
    RESOLVE_SCRIPT_LIB="/Applications/DaVinci Resolve/DaVinci Resolve.app/Contents/Libraries/Fusion/fusionscript.so"
    PYTHONPATH="$PYTHONPATH:$RESOLVE_SCRIPT_API/Modules/"
...
```

If you skip this step, Theia's tools will still open, but they won't be able to read your timeline (see [Troubleshooting](troubleshooting.md#could-not-import-davinci-resolve-api)).

## Step 2: Run the installer

1. Download the Theia project from `https://github.com/ming-qiu/theia`.

You may also `git clone https://github.com/ming-qiu/theia.git`.

2. In Finder, locate `install.command` inside the project folder.
3. Right-click it and choose **Open** (the first time you run it, macOS may warn that it's from an unidentified developer — this is expected for a script you downloaded yourself).
4. A Terminal window opens and walks through the install. You'll see it:
    * Check your Python version (3.9+ required) and pick the right Python — it prefers Homebrew Python on Apple Silicon.
    * Check for `ffmpeg`, and offer to install it via Homebrew if it isn't found.
    * Ask for your administrator password, so it can create `/Library/Application Support/Theia`.
    * Create a private Python virtual environment in that folder and install Theia's dependencies (`PySide6`, `openpyxl`, `Pillow`, `timecode`).
    * Copy the four GUI scripts and the `resources/` folder (fonts, icons) into `/Library/Application Support/Theia`.
    * Copy the four bridge scripts into Resolve's Edit-page script menu folder, at:
      `/Library/Application Support/Blackmagic Design/DaVinci Resolve/Fusion/Scripts/Edit/Theia`.
5. When you see **"Installation Complete!"**, you're done. You can close the Terminal window.

!!! note "Apple Silicon and Rosetta"
    The installer detects whether your Python is running natively as ARM64 or under Rosetta as x86_64, and installs packages for the matching architecture automatically. If you hit architecture-related errors, reinstalling with Homebrew Python (`brew install python`) usually resolves it.

## Step 3: Confirm the tools appear in Resolve

1. Open (or restart) DaVinci Resolve.
2. Open any project and go to the **Edit** page.
3. Go to **Workspace → Scripts → Theia** in the menu bar.
4. You should see:
    * `01 Clip Inventory`
    * `02 Frame Counter`
    * `03 Add Metadata`
    * `04 Shot List`
    * `Check for Updates`

If the menu is empty or missing entries, see [Troubleshooting](troubleshooting.md).

## Multiple users on one machine

Each person who wants to run Theia from their own Resolve needs to run `install.command` once under their own macOS user account, since the bridge scripts and Python environment are installed per-user.

## Re-installing Theia

Re-running `install.command` is safe — it removes and recreates the virtual environment and overwrites the copied scripts, so it always leaves you with the latest version from the project folder you ran it from.

## Updating Theia

Theia can check for and install updates without Git:

1. In DaVinci Resolve, go to **Workspace → Scripts → Theia → Check for Updates**.
2. The updater compares your installed version with the latest version available on GitHub.
3. If an update is available, click **Download and Install** and confirm when prompted.
4. The updater downloads the latest release and opens its `install.command` in Terminal.

If Theia is already current, the updater displays **"Theia is up to date."**

!!! note
    An internet connection is required to check for and download updates. The updater uses macOS's built-in download tools and does not require Git.

## Uninstalling

A matching `uninstall.command` ships alongside the installer. Double-click it (or right-click → **Open**), confirm with `y` when prompted, and it removes:

* `/Library/Application Support/Theia` (the Python environment, GUI scripts, and resources)
* `/Library/Application Support/Blackmagic Design/DaVinci Resolve/Fusion/Scripts/Edit/Theia` (the bridge scripts)

It does not touch any Excel files, frame counter videos, or other output you've generated — those live wherever you saved them.
