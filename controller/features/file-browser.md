---
description: The tab-based File Browser was added in version 2.3.0
---

# File Browser

The Controller uses a tab-based file browser for managing G-code files on the machine and on your computer.

The file browser can be opened from the main control screen or with the keyboard shortcut **Ctrl+O** (customisable in [Keyboard Shortcuts](keyboard-shortcuts.md)).

## Tabs

| Tab | Contents |
| --- | --- |
| **CNC machine** | Files stored on the connected machine's SD card |
| **This device** | Local files on the computer running the Controller |
| **History** | Recently accessed files from either location |

The current path is displayed under the tab name while browsing.

## Actions

* **Single-click** a file to select it. Single-click a folder to open it.
* **Double-click** a local file to upload it to the machine and select it for playback.
* **Double-click** a remote file to select it for playback.
* **Upload** one or more local files to the machine.
* **Download** one or more files from the machine to your computer.
* **Delete** selected files.

## Multi-select

Long-press a file (or use the multi-select toggle) to enter multi-select mode. In this mode, checkboxes appear next to each item and the action bar updates to show batch operations.

* **Shift-click** selects a contiguous range of files, and automatically enters multi-select mode if it is not already active.
* Upload and download actions work on the full selection — a single progress popup tracks the entire batch.
* Deleting a multi-selection removes all selected files in one step.

## Makera Studio Preview

Files created in Makera Studio may embed thumbnail images. The file browser displays these previews when available.
