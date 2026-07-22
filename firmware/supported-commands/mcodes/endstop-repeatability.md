---
description: Endstop Repeatability Test was added in version 2.2.0c
---

# Endstop Repeatability Test

## M575 - Endstop Repeatability Test

### Description

M575 homes the selected axes, then repeatedly approaches each endstop and reports the relative trigger position of each sample. Use this to check endstop mechanical and electrical consistency.

Cannot run while halted or while a file is playing. Compensation transforms are disabled for the test. After samples are collected the axes are re-homed.

Output includes a resolution floor (larger of one motor step and the distance travelled between 1 ms endstop polls at the tap feed rate). Differences at or below that floor are not meaningful.

### Parameters

* X / Y / Z / A / B / C: Limit the test to the listed axes (optional). If none are given, all configured homing endstops are tested.
* R: Number of samples per axis (optional, default: 5, range: 1–50)
* F: Tap feed rate override in mm/min or deg/min (optional; default is each axis slow homing rate)

### Example

```
M575              ; Test all homing endstops, 5 samples each
M575 X Y R10      ; X and Y only, 10 samples
M575 Z F100       ; Z only, override tap feed
```
