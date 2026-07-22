---
description: VESC USB Spindle was added in version 2.2.0c
---

# VESC USB Spindle

Optional spindle driver that commands a VESC (FW 6.x) over USB CDC instead of the stock PWM/analog interface. Intended for custom spindle conversions — not a stock Carvera configuration.

Requires `usb_msc.enable false` so USB is available for the VESC link.

## Firmware config

Example `config.txt` keys (tune for your motor):

```
spindle.type                 vesc
usb_msc.enable               false
spindle.default_rpm          10000
spindle.min_rpm              3000
spindle.max_rpm              15000
spindle.delay_s              3
spindle.ignore_on_halt       false
spindle.stall_s              1
spindle.stall_alarm_rpm      2000
spindle.vesc_pole_pairs      2
spindle.vesc_poll_ms         200
spindle.vesc_stall_current_a 15
```

`spindle.vesc_pole_pairs` converts commanded spindle RPM to VESC eRPM (eRPM = RPM × pole pairs). See also [Spindle maximum RPM](../spindle-max-rpm.md) for `spindle.max_rpm`.

## VESC Tool setup

Configure the VESC for your motor in VESC Tool 6.x (FOC detection, hall sensors if fitted, current/RPM/voltage limits), then write the motor configuration to the VESC before connecting it to the machine USB. Detailed example limits for a 48 V / 12k RPM / 4-pole motor are in the firmware source comment block for [`VESCSpindleControl.cpp`](https://github.com/Carvera-Community/Carvera_Community_Firmware/blob/Dev/src/modules/tools/spindle/VESCSpindleControl.cpp).
