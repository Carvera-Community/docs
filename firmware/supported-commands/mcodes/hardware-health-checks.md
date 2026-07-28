---
description: Hardware Health Checks were added in version 2.2.0c
---

# Hardware Health Checks

Diagnostic M-codes for endstop consistency and SD card file integrity. See the [feature guide](../../features/hardware-health-checks.md) for when to run them.

## M575 - Endstop Repeatability Test

### Description

M575 homes the selected axes, then repeatedly approaches each endstop and reports the relative trigger position of each sample. Use this to check endstop mechanical and electrical consistency.

Cannot run while halted or while a file is playing. Compensation transforms are disabled for the test. After samples are collected the axes are re-homed.

Output includes a resolution floor (larger of one motor step and the distance travelled between 1 ms endstop polls at the tap feed rate). Differences at or below that floor are not meaningful.

### Parameters

* X / Y / Z / A / B / C: Limit the test to the listed axes (optional). If none are given, all configured homing endstops are tested.
* R: Number of samples per axis (optional, default: 5, range: 1–50)
* F: Tap feed rate override in mm/min or deg/min (optional; default is each axis slow homing rate)

### Example

```
M575              ; Test all homing endstops, 5 samples each
M575 X Y R10      ; X and Y only, 10 samples
M575 Z F100       ; Z only, override tap feed
```

## M576 - Check All Hashed Files

### Description

When G-code files are uploaded through the Controller, firmware stores an MD5 sidecar under `/sd/gcodes/.md5/` mirroring the file path. M576 recomputes each file’s hash and compares it to that sidecar.

Walks `/sd/gcodes/` and verifies every file that has a stored MD5. Progress is printed as `[current/total]`, then `Intact` or `Corrupt` per file, followed by a summary count. Files without a sidecar are skipped. Cannot run while halted.

M576.1 is equivalent to M576.

Use the console [`md5sum`](../console-commands/README.md) command to hash an arbitrary path without comparing to a sidecar.

### Parameters

None

### Example

```
M576
M576.1
```

Example response:

```
Scanning for files with MD5 hashes...
Checking 3 file(s)...
[1/3] - /sd/gcodes/job.cnc
Intact
[2/3] - /sd/gcodes/macros/1001.cnc
Intact
[3/3] - /sd/gcodes/parts/bracket.cnc
Corrupt
File integrity check complete: 2 intact, 1 corrupt
```

## M576.2 - Check File or Directory

### Description

Checks a single file, or recursively checks a directory under `/sd/gcodes/`. Relative paths are resolved under `/sd/gcodes/`.

For a single file with no sidecar, the command errors rather than skipping.

### Parameters

* Path: File or directory under `/sd/gcodes/` (required). Examples: `job.cnc`, `macros`, `/sd/gcodes/parts/bracket.cnc`

### Example

```
M576.2 job.cnc
M576.2 macros
M576.2 /sd/gcodes/parts
```
