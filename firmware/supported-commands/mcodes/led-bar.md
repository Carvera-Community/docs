---
description: LED bar colour (M337) was added in version 2.1.0c
---

# LED Bar Colour

**M337** drives the addressable **LED bar** on **Carvera Air** . 

{% hint style="warning" %}
It does not currently apply to the **Carvera (C1)**, which uses discrete RGB LEDs on the main button instead of a bar.

[PR433](https://github.com/Carvera-Community/Carvera_Community_Firmware/pull/433) will extend this functionality to the C1.
{% endhint %}

Machine-state colours (idle, run, home, alarm, and so on) are described in [LED Behaviour](../../features/led-behavior.md). Those patterns still take over when the machine **state changes**.

## M337 — Set LED bar colour

### Description

Sets the LED bar to an RGB colour. Each channel is **0–255**. Omitted channels default to **0** (so `M337` with no parameters turns the bar off).

Green uses **U**, not **G**, because **G** is reserved for motion words (G0–G3).

The firmware replies with the colour it applied, for example `R: 255G:0B:0`. Values above 255 are ignored.

### Parameters

* **R**: Red 0–255 (optional, default 0)
* **U**: Green 0–255 (optional, default 0)
* **B**: Blue 0–255 (optional, default 0)

### Example

```gcode
M337 R255 U0 B0        ; red
M337 R0 U255 B0        ; green
M337 R0 U0 B255        ; blue
M337 R255 U255 B255    ; white
M337                   ; off
```
