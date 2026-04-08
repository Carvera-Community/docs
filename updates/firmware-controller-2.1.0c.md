---
description: Posted 2026/04/08
---

# Firmware/Controller 2.1.0c

The v2.1.0 release of the Carvera Community Firmware/Controller is our biggest release to date with over 70 feature enhancements alone. It also contains a large number of bugfixes and changes to improve the stability and reliability of the machine.

You can download the releases and see the full changelog on GitHub:

* [Carvera Community Firmware 2.1.0c](https://github.com/Carvera-Community/Carvera_Community_Firmware/releases/tag/v2.1.0c)
* [Carvera Community Controller 2.1.0](https://github.com/Carvera-Community/Carvera_Controller/releases/tag/v2.1.0-RC1)

## Release highlights

### 4th Axis

After careful examination of the codebase it has been found that the stock control implementation had a number of artificial and unnecessary restrictions affecting the max/resolution/accuracy of the 4th axis speed. These are addressed in this release and result in:

* removal of a hardcoded RPM cap of 5 RPM, now the machine configuration for max rotational speed will be correctly used. This is an outright max speed increase on the harmonic drive 4th axis from 5 to 6.6 RPM using the advertised/configured speeds from Makera. Testing has shown that the speed can be further increased to 12.5 RPM, but perform this at your own risk.
* removal of an artificial +30mm diameter padding, as an example on 20mm stock this change alone results in 2.5x increase in speed
* An increase in the frequency of the rotation speed calculations from 1mm to 0.1mm per line. The speed changes are now 10x smoother.
* Added logic to allow compound moves (Z+A or Y+A) to speed up if required to meet target surface speed
* Removal of speed caps when using G0 (rapid movement)

We have also added an [Inverse Time mode](../firmware/supported-commands/gcodes/inverse-time-feed-g93-g94.md) of 4th axis operation (G93). In this mode the F parameter specifies the time to complete the move. This is a much more precise way of applying consistent feed along complex, combined rotary-and-linear paths. This mode makes for even smoother finishes, and more accurate machining. Requires CAM support to use.

### Start GCode Playback Mid-file

You can now [specify a line number](../controller/features/resume-playback-start-at-line.md) to start gcode playback on the config-n-run screen, or by right clicking a line number in the file viewer. Additionally the Controller will monitor the last line executed by the machine, and in case of interruptions (halt/stop) will populate the resume line number for playback resumption automatically (but not enable the resume checkbox). When starting gcode playback with this feature, it will show a prompt with the commands it will run. It will restore the machine state to what was expected at the line, move the spindle above the resume position, lower into the position, then start gcode playback from the line specified. While care has been taken to test this feature, it works parsing the gcode contents in the file by the Controller, so there may be situations that the Controller doesn’t interpret the gcode in the same way as the machine. Please review the gcode used to restore the state if you are familiar with gcode and if not be prepared to stop the machine if it doesn’t appear to be correct.

### USB (Serial) Throughput Increase

Standard USB throughput is 115Kb/s, with this release[ usb throughput can be configured](../controller/features/usb-serial-speed.md) to negotiate up to 3Mbps (matching wifi max speed). The controller will first ping the machine at the default USB rate and request the higher rate. If there is a disconnect or the higher speed is unavailable both the machine and controller will revert back to the slower rate.<br>

### Machine Configuration File Backup

The Community Controller can now [back up key machine configuration files](../controller/features/machine-config-backup.md) from the machine SD card onto your computer. This provides an easy way to keep a safe copy of your machine specific calibration/config (including things like machine unique offsets) before doing upgrades, resets, or other major changes. It's recommended to at least have one config file backup to protect against failing SD cards.

Backup is started from Settings → Machine → Backup, and is also available on the **Firmware Upgrade** screen. The Controller will download a known set of config/compensation files. This workflow is desktop-only; restoring is done by copying the files back to the SD card manually. See the online doc for the [restore guide](../controller/features/machine-config-backup.md#restore).

### Accurate Time Remaining Estimate

Related to the gcode parsing work done to support  the resume-at-line Controller functionality, capability in the Controller has been added to read the actual gcode line movement locations and feed speed to give accurate gcode time estimates for completion. This even is adjusted if global feed overrides are used. The new time remaining estimate functionality is enabled by default in v2.1.0 on all gcode that can be visualised by the Controller. This adds a small amount of calculation time whenever a gcode file is selected, and can be disabled to return to the original machine based time estimate functionality via the Controller Settings screen.

### Support for ATC equipped Carvera Air

An exciting development is the work done by the Carvera Community member and fellow code contributor Warioo to [retrofit Automatic Tool Changer capability to the Carvera Air](https://www.instructables.com/Carvera-Air-ATC-Mod/). This is the functionality present in the big brother Carvera (C1) that allows the machine to switch between tools by itself. This release of Controller and Firmware include functionality to support this modification. See his work-in-progress Instructable for a view into how you can modify your Air to have similar capability.

### Custom Tool Length Sensor location and ATC Tool racks

The firmware now supports [customizing the tool setter (tool length sensor) location ](../firmware/features/custom-tool-setter-position.md)directly in Machine Coordinates using `coordinate.probe_mcs_x` and `coordinate.probe_mcs_y`. This is especially useful for non-stock setups where the setter is moved, replaced, or when your tool rack/anchor configuration is no longer a good reference for the setter location.

Additionally [custom tool slot definitions](../firmware/features/custom-tool-slots.md) allow you to configure your tool rack slot positions explicitly (and expand beyond the stock rack layout). When custom slots are defined the stock slot layout is ignored, and the rack positions are stored on the SD card in `custom_tool_slots.txt`. This can also be used to fine tune the slot positions of the stock C1 machine configuration if the standard definition is not sufficient.

### General UI Improvements

* [MDI got a lot of love](../controller/features/mdi-terminal.md). It now has terminal-like history access via up/down arrow keys and multi-line input
* Probing UI screen is continuing to evolve. Now has sane default values, has been re-organised to remove scrollbars for the parameter list, the addition of a new 4th Axis probing section, and more jogging options
* UI to connect a machine to a [hidden wifi network](../controller/features/wifi-auto-connect-and-hidden-networks.md)
* Bed Background image selection is now persisted across Controller runs
* [Automatically re-connect](../controller/features/auto-reconnect.md) to machine on Controller start
* Different Workspaces (WCS) can now have configurable names
* Better halt reason details when encountered during gcode file playback now output to the MDI making it clearer why a machine has stopped and what line caused the issue.
* File explorer got a number of bug fixes and quality of life improvements
* 3D toolpath visualisation now synchronised with file viewer line selection
* The TLO value is now the tool stickout instead of the length difference from a reference tool
* [LEDs on the machine are now more informative](../firmware/features/led-behavior.md) with a number of changes including long pressing the machine button now flashing the led when it’s been held long enough
* Laser and Spindle Status is now combined to save Window space. Which is shown is dependant on if Laser mode is active or not. Laser mode can be activated via the Tool dropdown.
* Manual tool changes on the Carvera now use the same Controller UI prompts/workflow as the Air
