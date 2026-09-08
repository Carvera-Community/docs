# Manual Tool Change on ATC Machines

Community firmware is not limited to 6 tools of the stock **T1–T6** rack. You can run any tool number the machine will accept, up to **999999** in the tool-number range, and mix them with ATC slots on **Carvera (C1)**.

The [M6](../supported-commands/mcodes/tool-change.md) command drives both automatic and manual changes. The Community Controller uses the **same tool-change prompts** for manual tools on C1 as on Air.

## Tool numbers

| Number | Meaning |
| ------ | ------- |
| **T-1** | Empty spindle (drop / no tool) |
| **T0** | Stock probe (and, with `zprobe.tool_zero_is_3axis`, a 3D probe) |
| **T1 …** in the rack or [custom slots](custom-tool-slots.md) | Automatic change on C1 (or on an Air with an ATC mod) |
| **T1 …** **not** in the slot list | **Manual** change: the machine walks you through drop/pick |
| **T9999** or **T≥999990** | Treated as a **3D probe** (no spindle spin; [crash protection](probe-crash-protection.md) applies) |

If you define [custom tool slots](custom-tool-slots.md), only those slot numbers are ATC tools. Any other positive number is manual (unless it is a probe class above).

On C1, asking **M6** for a slot that is **not** in the slot table is an error (`ERROR: Tool T… not defined in tool slots`). Use a number **outside** the rack range for a hand-loaded mill, or add the slot with **M890**.

## What a manual change does

1. Drops the current ATC tool if one is loaded, or prompts you to remove a previous manual tool
2. Moves to the **manual tool-change** position
3. Waits for you to install the cutter (and collet, if you passed **S**) and press the main button on the machine
4. Optionally measures **TLO** on the setter, unless you disable that with **C0** or supply **H**

See [M6](../supported-commands/mcodes/tool-change.md) for **S**, **R**, **H**, and **C**.

## Collet clamp without M6

On C1 you can clamp or unclamp the collet directly:

```gcode
M490.1               ; clamp / tighten
M490.2               ; unclamp / drop
```

The Controller Tool dropdown exposes the same actions. A front-button long press can run this cycle when `main_button_long_press_enable` is `ToolChange`.
