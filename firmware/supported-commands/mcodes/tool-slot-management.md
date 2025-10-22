# Tool Slot Management

These are the commands relating to the [Custom Tool Slot functionality](../../features/custom-tool-slots.md)

{% include "../../../.gitbook/includes/dev-feature-warning-banner.md" %}

### M889 - View Tool Slot Configuration

### Description

Outputs the current tool slot configuration. This shows both default (stock) tool slot configuration as well as custom defined slots.

### Parameters

None

### Example

```gcode
;Stock Carvera example
M889
Default Tool Slots Configuration:
Tool 0: X=-4.965 Y=-24.480 Z=-114.400
Tool 1: X=-4.965 Y=-84.480 Z=-114.400
Tool 2: X=-4.965 Y=-114.480 Z=-114.400
Tool 3: X=-4.965 Y=-144.480 Z=-114.400
Tool 4: X=-4.965 Y=-174.480 Z=-114.400
Tool 5: X=-4.965 Y=-204.480 Z=-114.400
Tool 6: X=-4.965 Y=-234.480 Z=-114.400

;Custom tools defined example
M889
Custom Tool Slots Configuration:
Tool 1: X=-11.450 Y=-21.525 Z=-117.000
Tool 2: X=-3.500 Y=-33.517 Z=-117.000
Tool 3: X=-11.330 Y=-45.550 Z=-117.000
Tool 4: X=-3.525 Y=-61.640 Z=-117.000
```
