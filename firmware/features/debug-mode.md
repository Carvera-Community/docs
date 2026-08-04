---
description: Debug Mode was added in version 2.2.0c
---

# Debug Mode

The [`debugmode`](../supported-commands/console-commands/README.md) console command turns on continuous firmware diagnostics. Output prints to the MDI/console about once per second. Modes are off by default and do not persist across reboot.

## Usage

List available modes (active ones marked with `*`):

```
debugmode
```

Enable a mode:

```
debugmode slowticker
debugmode cpuload
```

Disable all:

```
debugmode off
```

## Modes

### `slowticker`

Profiles the SlowTicker ISR. Each second prints:

```
SlowTicker: freq=<Hz>  last=<us>  max=<us>  budget=<us>
```

* **last** — duration of the most recent tick
* **max** — peak tick duration since the last print (reset each second)
* **budget** — available time per tick at the configured SlowTicker frequency

Use this when investigating missed steps, LED flicker under load, or whether periodic work is overrunning its ISR budget.

### `cpuload`

Estimates how much of each second is spent outside `ON_IDLE` (main loop work plus interrupts):

```
CPU: <n>% busy
```

Higher busy % means less idle headroom. Useful when checking whether a job or feature is starving background tasks.

## Notes

* Both modes can be enabled at the same time.
* Extra console traffic can affect timing-sensitive serial use; turn modes off when finished.
