---
description: Many G-code Viewer enhancements were added in version 2.2.0
---

# G-Code Viewer

A number of enhancements are present on the G-Code Viewer page:

* View Controls
* File Viewer
* Playback progress
* Tool visualization
* Ghost display
* Bed visualization
* Stock simulation
* Intellisense
* Time estimates

<figure><img src="../../.gitbook/assets/Screenshot 2026-08-04 at 10.38.36 pm.png" alt=""><figcaption></figcaption></figure>

## View controls

Toolbar options include:

* **View cube** — click a face to orient the camera
* **Orthographic projection** — toggle perspective vs ortho
* **Grid** — machine grid overlay (visibility is remembered)
* **Color scheme** — colour by move type, tool, feed speed, or Z height (with legend)

The view fits the path bounding box.

<figure><img src="../../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

## File viewer

The text G-code view supports syntax highlighting for G/M codes, comments, and O-code / math constructs.

<figure><img src="../../.gitbook/assets/image (24).png" alt="" width="375"><figcaption></figcaption></figure>

Syntax highlighting colours can be customised in the Controller settings:

<figure><img src="../../.gitbook/assets/Screenshot 2026-07-23 at 4.31.49 pm.png" alt=""><figcaption></figcaption></figure>

## Playback progress

Tool-change locations can be shown as markers on the playback progress bar. Toggle under Controller settings (`show_playbar_tool_change_markers`).

<figure><img src="../../.gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>

## Tool visualization

The viewer reads tool definitions from comments written by supported CAM post-processors and uses them for a more accurate 3D tool mesh, toolbar icons, hover tooltips, and the manual tool-change popup text.

Supported sources:

* Fusion 360 (Carvera Community post-processor)
* Makera Studio
* FreeCAD (Carvera Community post-processor)

When at least one tool definition is found, tool icons appear in the viewer toolbar (space permitting). Hover a tool for diameter, length, flute/shoulder, and related details. Manual tool-change prompts include the same summary so you know which cutter to load.

If no definition is present for a tool, a generic mesh is used.

<figure><img src="../../.gitbook/assets/814d3198-edd3-4167-ab0e-bc3b8e0ac57a.png" alt=""><figcaption><p>Tool tooltip on hover</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/4fe16264-199c-4eb6-a5c5-81a6ced41c74.png" alt=""><figcaption><p>Manual tool-change popup with tool details</p></figcaption></figure>

### Screenshots
<div><figure><img src="../../.gitbook/assets/467c5cad-3e5e-448a-9ce4-8184ba527b04.png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/f2b6a7a4-f5a4-4093-961a-a5b243c00857.png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/8a554448-e9ec-4de5-bc09-10b5b49e9275.png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/12373be3-4a70-4a22-af12-fc576da3f522.png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/05ac37e6-fe6f-4879-a7f9-651aa4507a79.png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/9cd81ade-1e44-4252-983d-ff3dccc1319a.png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/10dcef0c-7ce7-48d0-b299-41e4b3034ec9.png" alt=""><figcaption></figcaption></figure></div>

## Ghost display

The **Ghost** display mode makes older toolpath moves faint and draws recent moves at full opacity. This creates a trailing highlight that follows the playback position, making it easier to see where the tool is and where it has been.

Toggle Ghost mode from the display options in the G-Code viewer toolbar (setting `gcode_viewer_ghost_paths`). When Ghost is off, all toolpath lines draw at full opacity as before.

## Bed visualization

A machine bed model can be shown behind the toolpath in the 3D viewer. The bed button on the toolbar opens the bed settings where you can:

* **Select a bed** — choose from built-in beds for the Carvera C1, Carvera Air, and Makera Z1, or add a custom bed
* **Add / delete** custom beds — import your own fixture-plate or vice model
* **Position the bed** relative to the machine origin

Bed images in the Config and Run preview screen are filtered to show only beds that match the connected machine model. The bed is sized using the machine's configured `worksize_x` / `worksize_y`.

## Stock simulation

The viewer can simulate how the loaded toolpath carves into stock for a 3D preview of the finished part. See the dedicated [Stock Simulation](stock-simulation.md) page for full details.

## Intellisense

Hovering over or selecting a line in the G-code file viewer shows an **Intellisense-like popup** explaining the commands on that line. The same popups appear while typing in the [MDI Terminal](mdi-terminal.md).

Recognised commands include G-codes, M-codes, and console (SimpleShell) commands. Each popup shows the command name, a short description, and parameter details.

## Time estimates

The progress bar shows the estimated total run time after a file is selected (before the job starts). During playback, tool-change flags along the bar have **hover tooltips** showing the time remaining until each tool change. The remaining-time text in the bar alternates between time to the next tool change and time to job completion.
