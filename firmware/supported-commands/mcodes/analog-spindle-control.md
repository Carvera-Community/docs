---
description: Analog spindle PWM map commands (M959) were added in version 2.3.0c
---

# Analog Spindle Control

`M959` sets or reports the analog spindle PWM map. `M959.1` auto-tunes it from RPM feedback, and `M959.2` checks the current map. These commands require `spindle.type` `analog`. See the [analog spindle control feature](../../features/spindle-control-types/analog-spindle-control.md) for setup details.

## M959 - Set or Report the PWM Map

### Description

With no parameters, `M959` prints the map that is currently in memory. With parameters, it updates that map immediately. It does not write to `config.txt`.

### Parameters

* L: Minimum RPM (optional)
* H: Maximum RPM (optional)
* B: Bottom dead zone, as a fraction of full duty (optional)
* T: Top dead zone, as a fraction of full duty (optional)
* O: Offset (optional)
* S: Scale (optional)

Omitted letters keep their current value.

### Example

```
M959
M959 L1000 H12000 B0.12 T0.05 O0.10 S0.80
```

Example response:

```
min_rpm: 1000
max_rpm: 12000
deadzone_bottom: 0.1200
deadzone_top: 0.0500
offset: 0.1000
scale: 0.8000
delay_s: 8
delay_on_s: 8
delay_off_s: 4
```

## M959.1 - Auto-Tune the PWM Map

{% hint style="warning" %}
Auto-tune and validation run the spindle, including full duty cycle, for several minutes.
{% endhint %}

### Description

`M959.1` measures this spindle and fits a map from the rpm feedback signal. `spindle.feedback_pin` must be configured and working.

1. It runs at full duty until the speed settles, then times the spin-down. Those times become `delay_on_s` and `delay_off_s`. `delay_s` becomes the longer of the two. Each time is a whole number of seconds.
2. It steps pwm output from 0 to 1 in 0.05 increments, waits for the speed to settle at each step, and fits `min_rpm`, `max_rpm`, both dead zones, `offset`, and `scale`. The bottom dead zone is the duty that is still stopped. The top dead zone is the duty that no longer increases RPM, and `max_rpm` is the speed on that plateau.
3. It commands speeds across the fitted range and prints the worst miss.

The measured delays are written into memory as soon as the timing pass succeeds, and on successful completion updates the map.

`A0` puts the previous map and delays back when the routine ends, and still prints the `config-set` lines for a successful fit. Send `M5` to abort. If the sweep is aborted, the previous map stays. Save the printed lines only after the routine finishes and the worst-error line is acceptable.

With `D` omitted, each step is held for 1.5 times the measured `delay_s`, so a slow spindle gets more time to settle. `N` repeats the sweep and averages the RPM readings.

### Parameters

* P: Duty step as a fraction of full scale (optional, default: 0.05, range: 0.02–0.20). The step is adjusted so the sweep lands on even fractions of full duty.
* D: Seconds to hold each step (optional, default: 1.5 × measured `delay_s`, range: 0.2–30)
* N: Sweeps to average (optional, default: 1, range: 1–5)
* A: Apply the result in memory (optional, default: 1). `A0` reports a successful fit and restores the previous map and delays.
* V: Run the validation pass (optional, default: 1). `V0` skips it.

### Example

```
M959.1
M959.1 N3 P0.05
M959.1 A0
```

The console prints one `pwm` / `rpm` line per step, then a block like:

```
Measuring spindle start time
Measuring spindle stop time
delay_on_s: 8
delay_off_s: 4
delay_s: 8
Analog spindle auto-tune, PWM step 0.050, step time 12.0 s, 1 sweeps. The spindle will run.
sweep 1
pwm 0.000 rpm     0
Validating the calculated auto-tune values
commanded 1000, got 980 rpm
Auto-tune fit worst error observed requesting 10000 rpm, got 10120 rpm output
These values are temporarily applied to the in-memory config
and will need to be saved to the config file with
config-set sd spindle.min_rpm ...
```

## M959.2 - Validate the PWM Map

### Description

`M959.2` commands speeds from `min_rpm` to `max_rpm` and compares them with the rpm feedback signal. It does not change the map or the delays. Use it after saving a map, or any time you want to recheck it.

Hold time at each speed is the larger of `delay_on_s` and `delay_s`. If both are 0, each step waits until the speed settles, between 1 and 5 seconds. The same abort rules as auto-tune apply: remove the tool, and send `M5` to stop.

### Parameters

* P: Step through the RPM range as a fraction of that range (optional, default: 0.05, range: 0.02–0.20)

### Example

```
M959.2
M959.2 P0.1
```

Example response:

```
Analog spindle map validation, PWM step 0.050, hold 8 s. The spindle will run.
commanded 1000, got 980 rpm
commanded 5500, got 5620 rpm
commanded 12000, got 11940 rpm
Auto-tune fit worst error observed requesting  5500 rpm, got  5620 rpm output
```
