# C1 Improved PID Spindle Control

There is an optional configuration setting for the carvera C1 machines that provides better performance and torque from the spindle. This feature should not be used on the Air or Z1\
\
To use this feature you have to enable it by setting a few console commands:<br>

* config-set sd spindle.type pid\_pwm
  * enables the new spindle control function. One the C1 the default is pwm.&#x20;
* config-set sd spindle.control\_P 0.0002
  * Pushing this higher led to a bit of rpm oscillation when unloaded. However, I haven't tested higher values with load and I think increasing this would be good to get tighter rpm control
* config-set sd spindle.control\_I 0.0002
  * This kind of corresponds to the original P value from the stock implementation. My quick testing with the I value didn't get me much improvement, but it might need a much higher value
* config-set sd spindle.control\_D 0
  * With the P and I at its current values, there isn't much need for D. However with higher P values D will be needed to limit overshoot and oscillation. Further testing is needed
* config-set sd spindle.control\_smoothing 0.001
  * This change is critical. The default value is 0.1, or 100ms of smoothing. At 0.01 and smaller, there is no smoothing with the 100hz update loop, but setting it to 0.001 can be safe in case the update loop is updated to 1000hz later on.
* config-set sd spindle.max\_rpm 16000
  * Not strictly necessary, but with better control the spindle can run a bit faster to better handle small diameter endmills without rpm drop

To get better performance, the peak current and acc/dec knobs on the spindle controller can be modified, at which point then pid parameters can be adjusted to P: 0.0001, I: 0.001, D: 0.00001.

