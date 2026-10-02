# Compatibility

## Hardware

What CNC mills does the Carvera Community firmware support?

<table><thead><tr><th width="152"></th><th width="525.5">Compatibility Status</th></tr></thead><tbody><tr><td>Carvera</td><td>Fully Supported</td></tr><tr><td>Carvera Air</td><td>Fully Supported <a href="compatibility.md#id-1-rare-issue-with-carvera-air-and-v1.9-boards"><sup>[1]</sup></a></td></tr><tr><td>Z1 / Z1 Pro</td><td>Supported (≥ 2.3.0). See <a href="compatibility.md#z1-firmware-compatibility">Z1 notes</a></td></tr></tbody></table>

## Software

The Community stance is as follows:

> As we have no control over Makera, cross support between Makera and Community developed software (Controller/Firmware) is best effort. The **best** experience will be using both Community Firmware with Community Controller.

The following matrix tables shows the tested cross compatibility status.

### Makera Firmware with Community Controller

|                             | Community Controller 2.3.0                              |
| --------------------------- | ------------------------------------------------------- |
| **Makera Firmware** ≥1.0.4  | Functions correctly                                     |
| **Makera Firmware** 1.0.3   | Functions correctly                                     |
| **Makera Firmware** 1.0.2   | Functions correctly                                     |
| **Makera Firmware** <=1.0.1 | Diagnostic Screen is non-functioning. Rest of app works |

### Makera Controller with Community Firmware

It is expected that if you are using the Community Firmware, that you are also using the Community Controller. Community development efforts have not been spent testing the Makera Controller + Community firmware scenarios.

Basic Makera Studio connectivity with Community Firmware may work but this is best-effort only and none of the new Community features will be present in the UI. Use Community Controller for full support.


## Community Firmware with Community Controller

The best experience will be running matching versions of the Community Firmware and Controller, as both are tested and released in lockstep.

The following table notes any known issues when not using matching versions:

|                               | Community Controller Support                                                                                                                                                                                                  |
| ----------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Community Firmware** ≥2.1.0 | <p>Requires Controller ≥ 2.1.0. <br></p><p>Using earlier versions will experience an issue after each gcode playback where the Controller will think that the file is still playing, and prevent subsequent file playback</p> |

## Z1 Firmware Compatibility

As of version 2.3.0, Community Controller and Firmware support for the Makera Z1 and Z1 Pro is on-parity with the other machine models. There is no functionality present in the Makera firmware that is missing from the Community firmware.

However, a small number of Community-exclusive features are **not available on the Z1** due to its dual-MCU architecture. The Z1 has both an LPC1768 (same as C1 and Air) and an ESP32. The ESP32 controls SD card access, WiFi, USB, and the camera. The Community project currently uses the stock Makera ESP32 firmware, and the limitations below stem from that:

### Features not available on Z1

| Feature | Reason |
| --- | --- |
| [O-Code](../firmware/supported-commands/o-codes.md) support | O-Codes require seeking to specific G-code file locations on the SD card, which is not supported by the Makera ESP32 firmware |
| [Firmware-based macros](../firmware/supported-commands/mcodes/macros.md) | ESP32 file access limitations prevent macro files from being loaded during playback |
| [WiFi AP auto-disable](../firmware/features/wifi-ap-auto-disable.md) | No ESP32 command interface exists for the LPC to control the AP state |
| [USB serial speed](../firmware/features/usb-serial-baud-rate.md) | The Z1's USB is not serial-based — it is implemented in the ESP32 as a vendor-class interface, so baud rate negotiation does not apply |
| Save/load bed-leveling grid ([M374](../firmware/supported-commands/mcodes/README.md)/M375) | File I/O on the ESP32 does not support the grid save/load paths |
| [VESC USB spindle](../firmware/features/spindle-control-types/vesc-usb-spindle.md) | The USB port on the Z1 is connected to the ESP32, not the LPC — USB-host peripherals cannot be used |

### Behavioural differences on Z1

| Behaviour | Detail |
| --- | --- |
| 3D Probe TLO calibration | TLO calibration uses a single-tap method (same as Makera firmware) rather than the spring-compensation method used on C1 and Air. The Z1's tool length sensor spring is significantly softer than the 3D probe stylus spring, so the compression-compensation technique used on other models does not produce meaningful results on the Z1. |

{% hint style="info" %}
These limitations will be revisited if and when a Community ESP32 firmware is developed for the Z1.
{% endhint %}

## \[1] Rare boot issue with Carvera Air and v1.9 revision control boards

A small number of users have reported an [boot issue](https://github.com/Carvera-Community/Carvera_Community_Firmware/issues/243) running the Community Firmware on Carvera Air v1.9 control board. This has been investigated by both Makera and Carvera Community teams, and is concluded to be an isolated issue with some individual boards. If you encounter this issue, open a warranty claim with Makera for a replacement board.&#x20;

If you are experiencing this issue a known workaround is to rapidly cycle the power twice when cold-booting the machine. Once successfully booted, subsequent soft-resets are unaffected.
