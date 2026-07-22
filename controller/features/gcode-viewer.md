---
description: G-code Viewer enhancements were added in version 2.2.0
---

# G-code Viewer

3D toolpath preview on Config and Run (and related screens).

## View controls

Toolbar options include:

* **View cube** — click a face to orient the camera
* **Orthographic projection** — toggle perspective vs ortho
* **Grid** — machine grid overlay (visibility is remembered)
* **Color scheme** — colour by move type, tool, feed speed, or Z height (with legend)

The view fits the path bounding box.

## File viewer

The text G-code view supports syntax highlighting for G/M codes, comments, and O-code / math constructs.

When a file contains O-codes, playback automatically passes `-O` so the firmware pre-scans subroutines (see [O Codes](../../firmware/supported-commands/o-codes.md)).

Syntax highlighting colours can be customised in the Controller settings.

## Playback progress

Tool-change locations can be shown as markers on the playback progress bar. Toggle under Controller settings (`show_playbar_tool_change_markers`).
