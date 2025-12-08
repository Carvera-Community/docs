# Tool Slot Management

These are the commands relating to the [Custom Tool Slot functionality](../../features/custom-tool-slots.md)

{% include "../../../.gitbook/includes/dev-feature-warning-banner.md" %}

### M889 - View Tool Slot Configuration

### Description

Outputs the current tool slot configuration. This shows the tool slot configuration being used in memory.&#x20;

### Parameters

None

### Example

```gcode
;Stock Carvera example
M889
Tool Slots Configuration:
Tool 0: X=-4.965 Y=-24.480 Z=-114.400
Tool 1: X=-4.965 Y=-84.480 Z=-114.400
Tool 2: X=-4.965 Y=-114.480 Z=-114.400
Tool 3: X=-4.965 Y=-144.480 Z=-114.400
Tool 4: X=-4.965 Y=-174.480 Z=-114.400
Tool 5: X=-4.965 Y=-204.480 Z=-114.400
Tool 6: X=-4.965 Y=-234.480 Z=-114.400
```

### M890 - Define/update Tool Slot Config

### Description

Adds or updates a tool slot configuration. This command immediately updates the running config in memory and saves the config to file.&#x20;

### Parameters

* T: The tool slot number
* X: MCS X coordinate of the tool slot centre point
* Y: MCS Y coordinate of the tool slot centre point
* Z: MCS Z coordinate of the tool slot centre point. For convenience the Z parameter is optional, and if omitted the command will use the Z value from the previously numbered tool slot.

### Example

```gcode
M890 T4 X-10 Y-20 Z-110
Added tool slot 4: X=-10.000 Y=-20.000 Z=-110.000
Total custom tool slots: 4
Saved custom tool slot config to /sd/custom_tool_slots.txt
```

### M891 - Remove a Tool Slot from Config

### Description

Removes a tool slot from configuration. This command immediately updates the running config in memory and saves the config to file.&#x20;

### Parameters

* T: The tool slot number

### Example

```gcode
M891 T4
Removed tool slot 4
Saved custom tool slot config to /sd/custom_tool_slots.txt
```
