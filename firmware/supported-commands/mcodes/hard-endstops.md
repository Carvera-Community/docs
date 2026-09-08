# Hard Endstops

Community firmware adds M-codes to **suppress hard (physical) endstops** for the rest of the session. The flag is not saved to config and reverts on power cycle. Homing itself always uses the endstops; **M885** does not disable that.

{% hint style="danger" %}
**M885** removes hard-limit protection. Use it only for diagnosis (for example an endstop that is stuck triggered) and turn protection back on with **M886** as soon as you can. Soft limits ([M211](README.md)) are a separate system.
{% endhint %}

## M885 — Disable hard endstops

### Description

Sets a process-wide flag so **hard-limit** trips are ignored. Motor-alarm inputs are still checked. The console prints `Hard Endstops Disabled` (no newline). The flag is **not** stored in config.

Homing (**G28.2** / `$H`) temporarily forces endstops **on**, then restores whatever **M885**/**M886** you had afterwards.

### Parameters

None

### Example

```gcode
M885
```

## M886 — Enable hard endstops

### Description

Clears the **M885** flag. Prints `Hard Endstops Enabled`. This is the power-on default.

### Example

```gcode
M886
```
