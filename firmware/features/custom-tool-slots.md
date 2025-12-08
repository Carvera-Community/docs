# Custom Tool Slots

{% include "../../.gitbook/includes/dev-feature-warning-banner.md" %}

This functionality enables the capability to configure up to 255 custom tool slots. If any custom tool slots are defined, the machine default slots are ignored. It's expected that you are either have defined all the slots via the Custom Tool Slot functionality, or are using the stock tool slots. Custom tool slots are defined by the individual slot's X/Y/Z MCS location, and is not affected by changes in other machine position offsets.

\
It is possible to migrate the stock tool slots definition to the custom tool slot config if desired. This might be useful for a few reasons:

* To fine tune the individual tool slot or anchor 1 locations. Since the stock tool slot locations are configured as as group based on an offset from anchor 1, adjusting anchor 1 has the effect of also adjusting the tool rack location. This is not desirable if the stock tool slot locations is correct but the anchor 1 position is not.
* If supplementing the existing tool rack with additional slots.

Of course this functionality can be used to completely replace the Carvera tool rack with a higher slot count one.

<figure><img src="../../.gitbook/assets/PXL_20251014_053932230.MP.jpg" alt="" width="375"><figcaption><p>19 Slot Carvera Tool Rack made by <a href="https://serge.industries/shop">Serge Industries</a></p></figcaption></figure>

### Viewing the Tool Slot Config

The current tool slot configuration in memory (stock or custom) can be viewed with the `M889` command.

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

;Custom tools defined example
M889
Tool Slots Configuration:
Tool 1: X=-11.450 Y=-21.525 Z=-117.000
Tool 2: X=-3.500 Y=-33.517 Z=-117.000
Tool 3: X=-11.330 Y=-45.550 Z=-117.000
Tool 4: X=-3.525 Y=-61.640 Z=-117.000
```

### Configuring Custom Tool Slots

Custom tool slots are added/updated using the `M890` command. Any changes are immediately written to config file and loaded into memory. If no custom tool slot config currently exists the current config is stored to file. Thus by adjusting the tool definition for the stock slots (for example adding and removing a slot) will results in the rest of the stock config being migrated to a custom tool slot config.

In the config each tool slot has a separate position value for it's X/Y/Z Machine Coordinate System center position.\
\
Use the parameters `T` `X` `Y`and optionally `Z` to define the tool slot position, where `T` is the slot number. For example to configure a slot 7 would run `M890 T7 X-20 Y-30` . If no `Z` value is provided the last tool slot's Z value is used.

The best way to determine the MCS location of each tool slot is by using the [3D Probe](3d-probe-support.md) and performing a [bore probe (M461)](../supported-commands/mcodes/probing.md#m461-probe-bore-rectangular-pocket) inside the tool holder.

Note that the Z height configuration is the depth that the machine will lower the spindle before releasing the tool. It is recommended that at this height the tool holder is depressed into the spring mechanism by 1-2mm to ensure the tool is fully seated into the slot. The easiest way to get the right height is to use the original tool rack height as a baseline, and adjust up/down from there based on visual observation. Probing the inside lip of the slot is also possible however as the lip is very thin this can be challenging.

Note that tool 0 is a special slot for probes. Tools loaded as slot 0 have special behavior such as preventing the spindle from spinning. If no probes are stored in the rack, simply do not define a tool slot 0 in the custom tool slots definitions. There is no requirement that the slots are defined sequentially, only that the slot numbers do not exceed 99.

### Removing Custom Tool Slots

Custom tool slots can be removed using the `M891` command by proving the slot number as a `T` parameter. For example `M891 T7` would remove the slot 7 definition. Changes are immediately written to config file and loaded into memory

### Tool Slot Config File

The configuration is stored on the machine's SD card, on the root of the filesystem in a file called `custom_tool_slots.txt`. The syntax of the file is to have a separate line per tool slot definition in the format of `slot_number X_pos Y_pos Z_pos` for example `0 -10 -20 -120` would define slot 0 as having the MCS location as X -10, Y -20, Z -120.

Comments can be written into the text file as long as they are preceded with the `#` character.
