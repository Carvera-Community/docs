# Tool Offset Management

## Tool Length Offset (TLO) System

During normal usage, the Tool Length Offset (TLO) is measured using the tool setter on the Carvera bed. The machine doesn't actually know the absolute height of the tool setter - it only knows that the probe triggers consistently when tools touch it. In order to support the ability to change tools the machine maintains knowledge of two tool positions, the current tool and the reference tool. This is needed to maintain consistency in the workspace between different tool lengths.

When the very first tool is probed, the Z height in Machine Coordinate Space (MCS) is recorded as the **reference tool position**. This tool becomes the "reference tool" that all other tools will be measured against.

Any subsequent tools that are probed afterwards update the **current tool position**. The TLO is then calculated as the difference between these two positions:

$$
TLO = current\_tool\_position - reference\_tool\_position
$$

### Example

1. First tool: Probed at machine Z position -72.300 → becomes reference tool
2. Second tool: Probed at machine Z position -105.688 → current tool
3. TLO calculation: -105.688 - (-72.300) = -33.388

## M491 - Tool Length Calibration

### Description

Measures the length of the current tool.

### Parameters

* X: Offset the tool setter location by this amount (positive or negative) in X (optional)
* Y: Offset the tool setter location by this amount (positive or negative) in Y (optional)
* Z: Offset the tool setter location by this amount (positive or negative) in Z (optional)

### Example

```gcode
M491  ;Regular TLO measurement
M491 X-15  ;Measure the TLO offsettting the setter by 15mm to the left
```

## M491.1 - Tool Break Test

### Description

M491.1 performs a tool break check by calibrating the current tool and comparing its length to a previously stored tool length offset (TLO). If the difference exceeds the specified tolerance, it indicates potential tool breakage and halts the machine.

### Parameters

* H: Tolerance value for break detection (optional, defaults to 0.1mm)
  * Must be >= 0.02mm
  * If set too small, the command will halt with an error

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

M493.4 reports the current tool length offset values to the console.

### Parameters

None

### Example

```
M493.4              ; Report current TLO values
current tool offset [-67.880] , reference tool offset [-67.880]
no one-off tool setter position offsets configured
Tool setter position (MCS): X[-3.300] Y[-14.900] Z[nan]
```
