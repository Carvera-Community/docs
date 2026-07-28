---
description: Hardware Health Checks were added in version 2.2.0c
---

# Hardware Health Checks

Community firmware includes diagnostic checks for identifying hardware issues with the machine. Full command reference: [Hardware Health Checks](../supported-commands/mcodes/hardware-health-checks.md).

## Endstop repeatability — M575

This check repeatedly taps each selected endstop and reports how consistent the trigger position is. The machine requires high endstop repeatability to consistently home the machine to the same location. If repeatability this will affect the WCS Origin restores across powercycles, and can cause issues with any of the machine configuration that relies on MCS positioning, for example ATC Tool Slots or 4th Axis centerline.

**Run when:**

* Work offsets or probing results seem to drift between sessions
* After replacing or reseating an endstop, cable, or axis assembly
* As a baseline after unboxing or major mechanical work

Command details: [M575](../supported-commands/mcodes/hardware-health-checks.md#m575---endstop-repeatability-test)

## File integrity — M576

Compares G-code files under `/sd/gcodes/` against MD5 hashes saved at upload time. Reports each file as intact or corrupt. This can help identify SD cards that are dying.

**Run when:**

* If a job fails mid-file, stalls on open, or behaves as if the program was truncated
* If file uploads are intermittently erroring out
* After swapping or rewriting the SD card, to confirm uploads survived

Command details: [M576](../supported-commands/mcodes/hardware-health-checks.md#m576---check-all-hashed-files)
