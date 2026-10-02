---
description: LED colour control (M337/M338) was added in version 2.1.0c and extended in 2.3.0c
---

# LED Colour Control

**M337** sets the LED colour on the **Carvera Air** LED bar and the **Carvera (C1)** main-button LED. **M338** restores the LEDs to the current machine-state colour.

Machine-state colours (idle, run, home, alarm, and so on) are described in [LED Behaviour](../../features/led-behavior.md). Those patterns still take over when the machine **state changes**.

## M337 — Set LED colour

### Description

Sets the LEDs to an RGB colour. Each channel is **0–255**. Omitted channels default to **0** (so `M337` with no parameters turns the LEDs off).

Green uses **U**, not **G**, because **G** is reserved for motion words (G0–G3).

When called **with** R, U, or B parameters, the firmware applies the colour and overrides the normal state-driven LED behaviour. The override is cleared when the machine state changes to a blinking state (HOLD, SUSPEND, WAIT, TOOL) or when M338 is sent.

When called **without** R, U, or B, M337 **reports** the current LED colour instead of setting it.

### Parameters

* **R**: Red 0–255 (optional, default 0)
* **U**: Green 0–255 (optional, default 0)
* **B**: Blue 0–255 (optional, default 0)
* **I**: LED index 1–5 (optional). Omit to address all LEDs. On the C1 only index 1 is available. On the Air, indices 1–5 address individual segments of the bar.

### Examples

```gcode
M337 R255 U0 B0        ; set all LEDs to red
M337 R0 U255 B0        ; set all LEDs to green
M337 R0 U0 B255        ; set all LEDs to blue
M337 R255 U255 B255    ; set all LEDs to white
M337                   ; report current colour of all LEDs
M337 I3                ; report current colour of LED 3
M337 I2 R255 U128 B0   ; set LED 2 to orange
```

### Query output

When querying without colour parameters:

* If all LEDs share the same colour: `R:255G:128B:0`
* If individual LEDs differ: one line per LED, e.g. `I1 R:255G:0B:0` / `I2 R:0G:255B:0` / ...
* When querying a single LED with I: `I3 R:0G:0B:255`

## M338 — Restore LED status colour

### Description

Restores the LEDs to the current machine-state colour, clearing any override set by M337.

### Parameters

None.

### Example

```gcode
M337 R255 U0 B0        ; override to red
; ... do work ...
M338                   ; revert to normal status colour
```
