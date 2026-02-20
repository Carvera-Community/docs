# Firmware/Controller 2.1.0c

The v2.1.0 release of the Carvera Community Firmware/Controller is our biggest release to date with over 70 feature enhancements alone. It also contains a large number of bugfixes and changes to improve the stability and reliability of the machine.

Full list of changes is available on GitHub:

* [Carvera Community Firmware 2.1.0c](https://github.com/Carvera-Community/Carvera_Community_Firmware/releases/tag/v2.1.0c)
* [Carvera Community Controller 2.1.0](https://github.com/Carvera-Community/Carvera_Controller/releases/tag/v2.1.0-RC1)



Release highlights:

## 4th Axis

After careful examination of the codebase it has been found that the stock control implementation had a number of artificial and unnecessary restrictions affecting the max/resolution/accuracy of the 4th axis speed. These are addressed in this release and result in:

* removal of a hardcoded RPM cap of 5 RPM, now the machine configuration for max rotational speed will be correctly used. This is an outright max speed increase on the harmonic drive 4th axis from 5 to 6.6 RPM using the advertised/configured speeds from Makera. Testing has shown that the speed can be further increased to 12.5 RPM, but perform this at your own risk.
* removal of an artificial +30mm diameter padding, as an example on 20mm stock this change alone results in 2.5x increase in speed
* An increase in the frequency of the rotation speed calculations from 1mm to 0.1mm per line. The speed changes are now 10x smoother.
* Added logic to allow compound moves (Z+A or Y+A) to speed up if required to meet target surface speed
* Removal of speed caps when using G0 (rapid movement)

We have also added an Inverse Time mode of 4th axis operation (G93). In this mode the F parameter specifies the time to complete the move. This is a much more precise way of applying consistent feed along complex, combined rotary-and-linear paths. This mode makes for even smoother finishes, and more accurate machining. Requires CAM support to use.

## Start GCode Playback Mid-file

You can now specify a line number to start gcode playback on the config-n-run screen, or by right clicking a line number in the file viewer. Additionally the Controller will monitor the last line executed by the machine, and in case of interruptions (halt/stop) will populate the resume line number for playback resumption automatically (but not enable the resume checkbox). When starting gcode playback with this feature, it will show a prompt with the commands it will run. It will restore the machine state to what was expected at the line, move the spindle above the resume position, lower into the position, then start gcode playback from the line specified. While care has been taken to test this feature, it works parsing the gcode contents in the file by the Controller, so there may be situations that the Controller doesn’t interpret the gcode in the same way as the machine. Please review the gcode used to restore the state if you are familiar with gcode and if not be prepared to stop the machine if it doesn’t appear to be correct.

## USB (Serial) Throughput Increase

Standard USB throughput is 115Kb/s, with this release usb throughput can be configured to negotiate up to 3Mbps (matching wifi max speed). The controller will first ping the machine at the default USB rate and request the higher rate. If there is a disconnect or the higher speed is unavailable both the machine and controller will revert back to the slower rate.\
![](../.gitbook/assets/image.png)

## Machine configuration file backup

TBA

## Accurate Time Remaining Estimate

TBA

## Support for ATC equipped Carvera Air

TBA

## Quick Spindle RPM/Feed overrides

Spindle RPM/Feed overrides are now applied before next g-code line executed instead of 6 lines later when using the community controller and firmware. Under the hood this adds two new commands:\
$F S100 overrides the feed rate percentage\
$O S100 overrides the spindle speed percentage. \
In normal use the + and - buttons use these new commands if the firmware supports it and default back to the M220/224 commands if not.\
&#x20;![](<../.gitbook/assets/image (1).png>)

## Custom Tool Length Sensor location and ATC Tool racks

TBA



## General UI Improvements

* MDI got a lot of love. It now has terminal-like history access via up/down arrow keys and multi-line input
* Probing UI screen is continuing to evolve. Now has sane default values, has been re-organised to remove scrollbars for the parameter list, the addition of a new 4th Axis probing section, and more jogging options
* UI to connect a machine to a hidden wifi network
* Bed Background image select is now persisted across Controller runs
* Automatically re-connect to machine on Controller start
* Workspaces can now have configurable names
* Better halt reason details when encountered during gcode file playback now output to the MDI
* File explorer got a number of bug fixes and quality of life improvements
* 3D toolpath visualisation now synchronised with file viewer line selection
* TLO value is now the tool stickout instead of the length difference from a reference tool
* Long pressing the machine button now flashes the led when it’s been held long enough
* Laser and Spindle Status is now combined to save Window space. Which is shown is dependant on if Laser mode is active or not. Laser mode can be activated via the Tool dropdown.
* Manual tool changes on the Carvera now use the same Controller UI prompts/workflow as the Air

<br>

