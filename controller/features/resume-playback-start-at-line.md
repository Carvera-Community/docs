# Resume at line number

On the **Config and Run** screen you can start G-code playback from a chosen line instead of from the beginning of the file.

When this feature is used the machine will restore the machine state (tool inserted, spindle speed, feed rate etc), move the spindle above the resume location, lower the spindle into the correct location, the restart gcode playback from the line number specified.

## Setting the start line
There are a number of ways the start line can be set:

* Enter a line number in the resume / start-at-line control on **Config and Run**, then run the program as usual.
* **Right-click** a line in the G-code file view (or **long-press** on a touchscreen) to open a context menu. Choose the option to use that line for resume playback.
* You can **clear** the resume-at-line setting from the same context menu when it is available.

## Preview and file view

When you preview G-code, the **selected line in the file list** and the **progress slider** in the preview can stay **in sync**, so the line you are looking at matches the position in the preview.

## After halt or stop

If the machine **halts** during playback or you **stop** the program, the Controller will **fill in the last run line** in the resume input so you can continue from near where execution stopped. It won't enable the Start-at-Line option, you must enable that manually if you want to resume after a halt.

## Unsupported gcode
There are a situations that cannot be safely resumed:
* Gcode with relative movements (G91)
* Gcode that cannot be visualised by the Controller

If those are found in the file the Controller will raise and error and not start playback.
