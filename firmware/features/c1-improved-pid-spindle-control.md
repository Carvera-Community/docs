# C1 PID Spindle Control

There is an optional configuration setting for the carvera C1 machines that provides better performance and torque from the spindle. This feature should not be used on the Air or Z1 as those machines have closed loop control in the motor controller.

## tl;dr
```
config-set sd spindle.type pid_pwm
config-set sd spindle.control_P 0.0002
config-set sd spindle.control_I 0.0002
config-set sd spindle.control_D 0
config-set sd spindle.control_smoothing 0.001
```
And then restart your machine for the settings to take affect.

## Configuration

To use this feature you'll have to enable it by setting a few console commands:<br>

* `config-set sd spindle.type pid_pwm`
  * enables the new spindle control function. On the C1 the default is `pwm`, which has a broken implementation of PID.
* `config-set sd spindle.control_P 0.0002`
  * Pushing this higher led to a bit of rpm oscillation when unloaded. However, I haven't tested higher values with load and I think increasing this would be good to get tighter rpm control
* `config-set sd spindle.control_I 0.0002`
  * This kind of corresponds to the original P value from the stock implementation. My quick testing with the I value didn't get me much improvement, but it might need a much higher value
* `config-set sd spindle.control_D 0`
  * With the P and I at its current values, there isn't much need for D. However with higher P values D will be needed to limit overshoot and oscillation. Further testing is needed
* `config-set sd spindle.control_smoothing 0.001`
  * This change is critical. The default value is 0.1, or 100ms of smoothing. At 0.01 and smaller, there is no smoothing with the 100hz update loop, but setting it to 0.001 can be safe in case the update loop is updated to 1000hz later on.
* `config-set sd spindle.max_rpm 16000`
  * Not strictly necessary, but with better control the spindle can run a bit faster to better handle small diameter endmills without rpm drop
 
### Motor Controllor Adjustment

While this can be used without any physical modifications to the machine, there are 2 knobs to adjust on the motor controller in the back of the machine if you want maximum performance:
* The acc/dec knob should be adjusted to 2 ticks from the minimum
  * If you lower the acc/dec time further, the motor controller will fault any time you attempt to spin it up. This is as low as I could get it.
* The peak power knob adjusted to the maximum.
  * Theoretically this is higher than the power supply is capable of supplying, but in reality the motor controller doesn't draw >200W sustained, even under heavy cuts.

Now adjust the PID parameters to better suit the new kinematics
```
config-set sd spindle.control_P 0.0001
config-set sd spindle.control_I 0.001
config-set sd spindle.control_D 0.00001
```
And don't forget to restart the machine afterwards.

## Go back to default spindle control

If for some reason you need to reset back to default spindle control, run the following:
```
config-set sd spindle.type pwm
config-set sd spindle.control_P 0.00001
config-set sd spindle.control_I 0.00005
config-set sd spindle.control_D 0.00005
config-set sd spindle.control_smoothing 0.1
```
This will set the changed values back to their default state. Restart after changing.

