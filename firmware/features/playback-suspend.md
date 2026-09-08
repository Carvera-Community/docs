---
description: Playback suspend and spindle restore were added in version 2.2.0c
---

# Playback Suspend and Resume

Pausing a running gcode program **suspends** playback: the planner finishes the queued moves, the machine records its position, and you can resume from there.

By default the Community firmware also **stops the spindle on pause and restore it on resume** so a feed-hold does not leave the cutter spinning in the work.

## Spindle restore

On suspend, if the spindle was running, firmware saves that state and issues **M5**. On resume it issues **M3** or **M4** again with the saved RPM, then moves back to the saved XYZ before continuing the file.

This is **on** by default. To keep the older “leave the spindle as-is” behaviour:

```
config-set sd spindle_suspend_restore_enable false
```

Then `reset`. 
