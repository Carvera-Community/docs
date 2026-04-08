# Advanced Motion Control

## M400 — wait for moves

## Description

**M400** waits until **all motion already queued** in the planner has finished. Nothing **after** this line runs its motion until the machine is **idle** from the planner’s point of view (the conveyor has drained).

Use **M400** as a **sync point** before **M**-codes or other actions that must happen only after positioning moves complete. Internal sequences (for example **ATC** scripts) inject **M400** for the same reason.

## Parameters

None.

## Example

```gcode
G0 X10 Y10
G1 Z-5 F300
M400
; Planner idle: prior moves have finished before the next lines run
M118 after moves complete
```
