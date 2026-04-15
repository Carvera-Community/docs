# Tool Offset Management

## Tool Length Offset (TLO) System

During normal usage, the Tool Length Offset (TLO) is measured using the tool setter on the Carvera bed. The machine does not need the absolute height of the setter in world coordinates; it only needs a **repeatable datum** so that each tool’s length can be expressed consistently when changing tools.

The firmware uses a fixed reference position in Machine Coordinate Space (MCS) that corresponds to the tool setter contact point with an empty collet (no cutter installed). That value is given by the configuration key **`coordinate.reference_tool_mz`** (default **−115.34** mm on Carvera C1 and Carvera Air; adjust only if your machine or calibration differs). The config key is named this for legacy reasons.

When you probe a tool, the machine records the MCS **Z** coordinate where the tool tip touches the setter (current tool contact position). Thus the TLO value is the length that the **cutter stickout**: how far the installed tool extends beyond that empty-collet reference.

$$
TLO = current\_tool\_contact\_mz - reference\_tool\_mz
$$

Here `reference_tool_mz` is the configured empty-collet reference (`coordinate.reference_tool_mz`). The stored TLO is therefore the **length** (stickout).

### Example

Assume `coordinate.reference_tool_mz` is **−115.340** (empty collet touching the setter).

1. A tool is probed; the tip touches the setter at machine Z **−105.340**.
2. TLO (stickout): −105.340 − (−115.340) = **10.000** mm.

## M491 - Tool Length Calibration

### Description

Measures the length of the current tool. With the **R** parameter you can repeat the measurement multiple times (e.g. for facemills): the machine probes once per cycle; rotate the face mill between cycles to find the lowest cutting edge, and the TLO is taken from that measurement.

### Parameters

* X: Offset the tool setter location by this amount (positive or negative) in X (optional)
* Y: Offset the tool setter location by this amount (positive or negative) in Y (optional)
* Z: Offset the tool setter location by this amount (positive or negative) in Z (optional)
* R: Number of TLO measurement repeats (optional, default: 1). For facemills: probe once per cycle, rotate the face mill between cycles; the TLO uses the lowest cutting edge

### Example

```gcode
M491  ;Regular TLO measurement
M491 X-15  ;Measure the TLO offsettting the setter by 15mm to the left
M491 R3   ;Repeat TLO measurement 3 times (e.g. for a facemill — rotate tool between cycles)
```

## M491.1 - Tool Break Test

### Description

M491.1 performs a tool break check by calibrating the current tool and comparing its length to a previously stored tool length offset (TLO). If the difference exceeds the specified tolerance, it indicates potential tool breakage and halts the machine.

### Parameters

* H: Tolerance value for break detection (optional, default: 0.1mm, minimum: 0.02mm)

{% embed url="https://youtu.be/28P2BoFFpco?t=174" %}
Demo of M491.1
{% endembed %}

### Example

```
M491.1              ; Perform tool break check with default tolerance (0.1mm)
M491.1 H0.05        ; Perform tool break check with 0.05mm tolerance
```

## M493 - Tool Length Offset (TLO) Management

### Description

M493 manages tool length offset (TLO) settings for the current tool. It can set tool offsets, change tools, and report TLO values.

### Parameters

* Subcode 0/1: Set tool offset from last probe position
* Subcode 2: Set new tool number
* T: Tool number (required)
* Subcode 3: Set current tool offset manually
* Z: Tool length value (optional)
* H: Offset above Z0 (optional)
* Subcode 4: Report current TLO values

### Example

```
M493                ; Set tool offset from last probe
M493.2 T1           ; Set tool 1 as active
M493.3 Z10.5        ; Set tool length to 10.5mm
M493.3 H2.0         ; Set TLO from current position with 2mm offset
M493.4              ; Report current TLO values
```

## M493.1 - Set Tool Offset (Same as M493)

### Description

M493.1 sets the tool offset from the last probe position. This is identical to M493 with subcode 0 or 1.

### Parameters

None

### Example

```
M493.1              ; Set tool offset from last probe position
```

## M493.2 - Set New Tool

### Description

M493.2 sets a new tool as the active tool and updates the system accordingly.

### Parameters

* T: Tool number (required)

### Example

```
M493.2 T5           ; Set tool 5 as active
```

## M493.3 - Set Current Tool Offset Manually

### Description

M493.3 sets the current tool offset manually using either a Z value or an H offset from the current position.

### Parameters

* Z: Tool length value (optional)
* H: Offset above Z0 (optional)

{% embed url="https://youtu.be/28P2BoFFpco?t=291" %}
Demo of M493.3
{% endembed %}

### Example

```
M493.3 Z-15.2        ; Set tool length offset to 15.2mm
M493.3 H3.0         ; Set TLO from current position with 3mm offset

; Adding 2.9mm length to the current tool
M493.4 ; returns current tool offset [-105.688], reference tool offset [-72.300]
; tool offset is cur_tool_mz - ref_tool_mz or -105.688 - (-72.300) = -33.387
; increasing it by  2.9mm  -33.387 + 2.9 = -30.488
M493.3 Z-30.488
```

## M493.4 - Report Current TLO

### Description

M493.4 reports the current tool length offset values to the console. The first line prints the **current tool’s MCS Z contact position** and the configured **`reference_tool_mz`** (empty collet datum). Subtract reference from current to get the active **TLO (stickout)**. It may also list one-off setter offsets and the configured tool setter position in MCS.

### Parameters

None

### Example

```
M493.4              ; Report current TLO values
current tool offset [-105.340] , reference tool offset [-115.340]
no one-off tool setter position offsets configured
Tool setter position (MCS): X[-3.300] Y[-14.900] Z[nan]
```
