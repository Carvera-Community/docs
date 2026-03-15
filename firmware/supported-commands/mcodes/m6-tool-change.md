# Tool Change

## M6 - Tool Change

### Description

M6 performs an automatic tool change. The **T** parameter specifies which tool to select: **T0** for the wireless probe, **T-1** for no tool (empty spindle), or **T1**, **T2**, and so on for a tool number from the ATC or a manual tool slot.

After a tool change, the machine typically runs TLO (tool length offset) calibration for the new tool unless disabled. When you use the optional **S** parameter (S1–S6), the machine moves to the manual tool change position so you can install the correct collet before the change; this applies only when ATC is enabled.

### Parameters

* T: Tool number (required). T0 = wireless probe, T-1 = none, T1+ = tool slot
* S: Collet type 1–6 (optional). When specified during an ATC tool change, the machine moves to the manual tool change position for you to change the collet. Only applies when ATC is enabled. See collet values below.
* R: Number of TLO measurement repeats (optional, default: 1). For facemills: the machine probes multiple times; rotate the face mill between cycles to find the lowest cutting edge
* H: Custom TLO value (optional). When set, automatic TLO calibration is skipped and this value is used
* C: Enable or disable automatic TLO calibration after the tool change (optional). 1 = calibrate, 0 = do not calibrate

#### Collet values (S parameter)

| S value | Collet size |
|---------|-------------|
| S1 | 3mm |
| S2 | 1/8" |
| S3 | 4mm |
| S4 | 6mm |
| S5 | 1/4" |
| S6 | 8mm |

### Example

```
M6 T1                    ; Change to tool 1 and set TLO
M6 T0                    ; Change to wireless probe
M6 T-1                   ; Drop tool / empty spindle
M6 T3 S2                 ; Change to tool 3, use collet type 2 (machine goes to manual tool change position first)
M6 T1 R3                 ; Change to tool 1, repeat TLO measurement 3 times (e.g. for a facemill)
M6 T2 H-15.2             ; Change to tool 2 and set TLO to -15.2 (no calibration)
```
