# Compatibility

## Hardware

What CNC mills does the Carvera Community firmware support?

<table><thead><tr><th width="152"></th><th width="525.5">Compatibility Status</th></tr></thead><tbody><tr><td>Carvera</td><td>Fully Supported</td></tr><tr><td>Carvera Air</td><td>Fully Supported <a href="compatibility.md#id-1-rare-issue-with-carvera-air-and-v1.9-boards"><sup>[1]</sup></a></td></tr><tr><td>Z1</td><td>Planned to be supported</td></tr></tbody></table>

## Software

The Community stance is as follows:

> As we have no control over Makera, cross support between Makera and Community developed software (Controller/Firmware) is best effort. The **best** experience will be using both Community Firmware with Community Controller.

The following matrix tables shows the tested cross compatibility status.

### Makera Firmware with Community Controller

|                             | Community Controller 2.1.0                              |
| --------------------------- | ------------------------------------------------------- |
| **Makera Firmware** ≥1.0.4  | Non functioning                                         |
| **Makera Firmware** 1.0.3   | Functions correctly                                     |
| **Makera Firmware** 1.0.2   | Functions correctly                                     |
| **Makera Firmware** <=1.0.1 | Diagnostic Screen is non-functioning. Rest of app works |

### Makera Controller with Community Firmware

It is expected that if you are using the Community Firmware, that you are also using the Community Controller. Community development efforts have not been spent testing the Makera Controller + Community firmware scenarios.

## How to install Community Firmware if running **Makera Firmware** >=1.0.4

As Makera Firmware >=1.0.4 is not functioning with the Community Controller 2.1.0 if you want to install Community firmware, you need to follow this sequence:

1. Using [Makera Controller ≥ v0.9.13](https://github.com/MakeraInc/CarveraController/releases) follow the [Firmware Installation procedure](firmware/installation-upgrade.md#installation)
2. After the machine resets it will be running the Community Firmware and you can now use the Community Controller

Alternatively if you have issues using the Makera Controller to upload the firmware, you can use the [SD Card method](firmware/installation-upgrade.md#alternative-install-method).

## Community Firmware with Community Controller

The best experience will be running matching versions of the Community Firmware and Controller, as both are tested and released in lockstep.

The following table notes any known issues when not using matching versions:

|                               | Community Controller Support                                                                                                                                                                                                  |
| ----------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Community Firmware** ≥2.1.0 | <p>Requires Controller ≥ 2.1.0. <br></p><p>Using earlier versions will experience an issue after each gcode playback where the Controller will think that the file is still playing, and prevent subsequent file playback</p> |

## \[1] Rare boot issue with Carvera Air and v1.9 revision control boards

A small number of users have reported an [boot issue](https://github.com/Carvera-Community/Carvera_Community_Firmware/issues/243) running the Community Firmware on Carvera Air v1.9 control board. This has been investigated by both Makera and Carvera Community teams, and is concluded to be an isolated issue with some individual boards. If you encounter this issue, open a warranty claim with Makera for a replacement board.&#x20;

If you are experiencing this issue a known workaround is to rapidly cycle the power twice when cold-booting the machine. Once successfully booted, subsequent soft-resets are unaffected.
