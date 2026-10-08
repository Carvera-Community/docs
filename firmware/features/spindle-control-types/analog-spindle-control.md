---
description: Analog spindle PWM map and auto-tune were added in version 2.3.0c
---

# Analog Spindle Control

Carvera Air and Z1 spindles (including Z1 Pro) make use of closed speed loop inside the motor controller. Makera firmware (and Community firmware by default) runs an additional second feedback-loop based speed control on the control board (`spindle.type` `pwm`) in front of that loop, so the two speed control systems "fight" each other and speed changes take longer than if the most optimal system (the motor controller) was to control the rpm by itself. The `analog` spindle type replaces the default spindle control system on with a direct duty-cycle command to the motor controller, and makes speed control entirely the responsibly of the motor controller. No physical modification needs to be done to make use of this control method.

This change shortens the time it takes from the spindle to reach the commanded speed, which is most obvious on spindle start, and should also hold RPM more steadily under load. For one user the time it took for the spindle to go from 0-10k rpm, and reach within 100 RPM of 10k for at least 2 seconds dropped from 27s to less than 5s. 

Please note that the Carvera (C1) cannot make use of this spindle control method without replacing the spindle motor controller, only the Carvera Air and Z1 require no changes. The analog speed control functionality can also be used to replace the spindle motor controller on any of the machines.

## Firmware config

Available configuration keys:

| Key | Default if unset | Meaning |
| --- | --- | --- |
| `spindle.type` | analog | To use the analog control method, the spindle type must be set to the value `analog` |
| `spindle.min_rpm` | 100 | Lowest requested RPM while running |
| `spindle.max_rpm` | 5000 | RPM that corresponds to `scale`, and the command clamp |
| `spindle.pwm_deadzone_bottom` | 0 | Lowest running duty |
| `spindle.pwm_deadzone_top` | 0 | Unused duty at the top |
| `spindle.pwm_offset` | 0 | Duty added after scaling |
| `spindle.pwm_scale` | 1 | Duty change from 0 RPM to `max_rpm` |
| `spindle.delay_s` | 0 | Wait time in whole seconds, between speed changes |
| `spindle.delay_on_s` | `delay_s` | Wait time after spindle on, before the next move |
| `spindle.delay_off_s` | `delay_s` | Wait time after spindle off |
| `spindle.feedback_pin` | `nc` | Tachometer input. The pin has to be on port 0 or 2. Stock machines use `2.7`. |
| `spindle.pulses_per_rev` | 1 | Rising edges counted as one revolution. Stock Air is 2, stock Z1 is 4. |
| `spindle.acc_ratio` | 1 | Scale on the RPM calculated from that period. Stock Air and Z1 use 1. |
| `spindle.control_smoothing` | 0.1 | Low-pass time constant, in seconds, for the tachometer RPM. It does not change the duty command. |
| `spindle.alarm_pin` | `nc` | Spindle-controller alarm input. A steady active level halts the machine. Stock machines use `0.19^`. |

## Setup on CA1 or Z1
Commands below are entered in the [MDI console](../../../controller/features/mdi-terminal.md).

{% stepper %}
{% step %}
**Switch to analog control**
Change the spindle type to analog and reset:

```
config-set sd spindle.type analog
reset
```
{% endstep %}
{% step %}
**Run the autotune**
The analog control system needs a map of what a duty cycle from the control board means to the spindle motor controller.
If you can enter these values manually with [M959](../../supported-commands/mcodes/analog-spindle-control.md#m959---set-or-report-the-pwm-map), but since the system already has a functioning rpm feedback to the control board, you can simply run [M959.1](../../supported-commands/mcodes/analog-spindle-control.md#m959.1---auto-tune-the-pwm-map).

```
M959.1
```
{% endstep %}
{% step %}
**Save the autotune**
On completion of the auto-tune, the [`M959.1`](../../supported-commands/mcodes/analog-spindle-control.md#m959.1---auto-tune-the-pwm-map) command will output the `config-set` commands that you need to run to save the analog control duty cycle values. Run these commands, then reset to make sure.
{% endstep %}
{% endstepper %}

Command reference: [M959](../../supported-commands/mcodes/analog-spindle-control.md#m959---set-or-report-the-pwm-map), [M959.1](../../supported-commands/mcodes/analog-spindle-control.md#m959.1---auto-tune-the-pwm-map), [M959.2](../../supported-commands/mcodes/analog-spindle-control.md#m959.2---validate-the-pwm-map).

# Reverting back to original spindle control system on CA1 or Z1

Change the spindle type to analog and reset:
To revert back to the original control system of the CA1 or Z1 simply run:

```
config-set sd spindle.type pwm
reset
```

The `spindle.pwm_*` keys can stay in `config.txt`. The `pwm` spindle type does not read them.

## How the duty cycle is calculated

While the spindle is running, `M3 S` is clamped to `min_rpm`…`max_rpm` duty cycle is then:

```
duty = offset + scale × (requested RPM / max RPM)
```

Duty is limited to the window `[deadzone_bottom, 1 − deadzone_top]`. Spindle off outputs a duty of 0.

`deadzone_bottom` is the lowest duty that actually turns the spindle. `deadzone_top` is unused duty at the top of the scale, where higher PWM output no longer raises RPM. `offset` is added after scaling. `scale` is a duty change multiplier (defaults to 1x).

`M3` below `min_rpm` is raised to `min_rpm`. `M3` above `max_rpm` is clamped to `max_rpm`. See also [Spindle maximum RPM](../spindle-max-rpm.md).
