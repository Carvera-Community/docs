# About

The Community forked version of the Carvera Firmware that has a number of benefits and fixes above and beyond the Makera software.\
\
**Makera Support have stated that using the Community Firmware/Controller does not void the machine warranty.** If you need support you may be asked to reinstall Makera firmware to facilitate that support.

The following are some of the features added in the Community Firmware:

* Support for **3D Touch Probe** devices [Commands](supported-commands/mcodes/probing/) [Probe Install](https://www.instructables.com/Carvera-Touch-Probe-Modifications/), including macros to calibrate anchor 1 & 2 positions and automatically probe corners, bores, bosses, angles and 4th axis stock for high precision **wcs origin** settings (especially useful for **two sided operations**)
* 3D Probe crash protection
* Ability to use LinuxCNC/Faunic style [math](features/math.md) and [variable](features/variables.md) storage
* [O-codes](supported-commands/o-codes.md) for conditionals, loops, and in-file subroutines
* [File macros](supported-commands/mcodes/macros.md) to run one file inside another
* Ability to use **multiple workspaces** not just G54
* Support for tools numbered beyond 99 **up to 999999**
* Manual tool change automation for the original Carvera when using tool > 6
* Work coordinate system **(WCS) rotation** support
* Better diagnostic commands
* [Optional stops](supported-commands/mcodes/optional-stop-mode.md)
* [Line by line execution](supported-commands/mcodes/line-by-line-execution-mode.md) mode
* [Tool Length Offset Management](supported-commands/mcodes/tool-offset-management.md) options such as **setting tool length offset** via a known offset (like a pin) and testing for tool breakage
* [**Continuous Jog**](features/jog-modes.md#continuous-jog-mode) mode for smoother jogging motion that also **enables manual milling**
* [Flex Compensation System](features/flex-compensation-system.md) for the Carvera Air that **compensates** for the X Axis **rods flexing**
* Ability to **store/load the bed leveling information** on/from the SD card
* [Makera communication protocol](features/communication-protocol.md) compatibility

See the [youtube page](https://www.youtube.com/@carvera-community) and [version.txt](https://github.com/Carvera-Community/Carvera_Community_Firmware/blob/Dev/version.txt) for more detailed change log of changes.
