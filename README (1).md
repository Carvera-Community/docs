# About

The Community developed version of the Carvera Firmware has a number of benefits and fixes above and beyond the Makera software:

* Support for 3D Touch Probe devices
* Ability to use LinuxCNC/Faunic style [math](firmware/features/math.md) and [variable](firmware/features/variables.md) storage
* [File macros](firmware/supported-commands/mcodes/macros.md) to run one file inside another
* Ability to use multiple workspaces not just G54
* Support for tools numbered beyond 99 up to 999999
* Manual tool change automation for the original Carvera when using tool > 6
* WCS rotation support
* Better diagnostic commands
* [Optional stops](firmware/supported-commands/mcodes/optional-stop-mode.md)
* [Line by line execution](firmware/supported-commands/mcodes/line-by-line-execution-mode.md) mode
* [Tool Length Offset Management](firmware/supported-commands/mcodes/tool-offset-management.md) options such as setting tool length offset via a known offset (like a pin) and testing for tool breakage

See [version.txt](https://github.com/Carvera-Community/Carvera_Community_Firmware/blob/Dev/version.txt) for more detailed change log of changes.
