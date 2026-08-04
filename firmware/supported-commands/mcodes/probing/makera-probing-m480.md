---
description: Makera Probing Compatibility was added in version 2.2.0c
---

# Makera Probing Compatibility (M480)

Makera Studio / stock firmware probing commands **M480.1–M480.10**. Community firmware implements them as thin wrappers around the community probing macros ([M461](./#m461-probe-bore-rectangular-pocket)–[M464](./#m464-probe-outside-corner)). Prefer the community macros when writing new jobs; use M480 only when you need stock/Makera command compatibility.

All distances in the examples below are positive; the subcode chooses corner/side direction.

| Command | Purpose | Community equivalent (approx.) |
| ------- | ------- | ------------------------------ |
| M480.1 | Outside corner, top-left | [M464](./#m464-probe-outside-corner) with signed X+/Y− |
| M480.2 | Outside corner, top-right | [M464](./#m464-probe-outside-corner) X−/Y− |
| M480.3 | Outside corner, bottom-right | [M464](./#m464-probe-outside-corner) X−/Y+ |
| M480.4 | Outside corner, bottom-left | [M464](./#m464-probe-outside-corner) X+/Y+ |
| M480.5 | Inside corner, top-left | Z touch-off, move into corner, then [M463](./#m463-probe-inside-corner) |
| M480.6 | Inside corner, top-right | same pattern |
| M480.7 | Inside corner, bottom-right | same pattern |
| M480.8 | Inside corner, bottom-left | same pattern |
| M480.9 | Inside pocket / bore centre | [M461](./#m461-probe-bore-rectangular-pocket) |
| M480.10 | Outside boss centre | [M462](./#m462-probe-boss-rectangular-block) |

### Parameters (all subcodes)

* D: Probe tip diameter (optional, default: 2)
* X / Y: Probe travel / feature half-size (optional, default: 20)
* Z: Side probe depth below the top surface (optional, default: 4; used where a Z drop applies)

### Notes

* Requires a probe tool: **0**, **9999** (Makera convention), or **≥ 999990**
* Machine must be homed
* Inside-corner variants (M480.5–8) probe Z first ([M466](./#m466-single-axis-probe-double-tap)), then move into the corner before side probes — matching [Makera stock behaviour](https://github.com/MakeraInc/CarveraFirmware)
* These set WCS from the probed feature (same idea as `S1`/`S2` on the community macros)

### Example

```
M480.1 D2 X20 Y20 Z4    ; Outside corner
M480.9 D2 X20 Y20       ; Pocket centre
M480.10 D2 X20 Y20 Z4   ; Boss centre + top Z
```
