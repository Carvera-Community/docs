---
description: 3D Probe crash protection was added in version 2.0.0c
---

# 3D Probe Crash Protection

When a **3D probe** is the active tool, Community firmware watches the probe input while the spindle is moving. If the stylus triggers outside of an actual probing or calibration move, the machine **halts** so the tip is less likely to be bent or broken.

## When it triggers

Crash protection runs only while all of the following are true:

* The active tool is classified as a **3D probe** (tool **0** with `zprobe.tool_zero_is_3axis` enabled, tool **9999**, or any tool **≥ 999990**)
* An **X, Y, or Z** motor is moving
* The probe input is active (stylus deflected)
* The machine is **not** currently probing, calibrating, or measuring TLO

## What you will see

The console prints:

```
error:3D Probe crash detected
Manually move the probe to a safe position
```

Then the machine enters a halt. After the halt is cleared, 3D Probe crash protection will not retrigger until the probe stops reporting contact.

## Requirements

The probe must actually report contact. If the LED on the probe body changes but the Controller diagnostic **Probe** input does not, crash protection cannot fire. Confirm the wiring and [test the probe](../supported-commands/mcodes/probing/3d-probe-support.md) before relying on it.

Crash protection does **not** replace watching the machine. It only reacts after the stylus has already triggered.
