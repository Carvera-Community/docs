# Jog Modes

The `$J` command allows manual movement of machine axes for positioning and setup operations. It supports both single-move (step) jogging and continuous jogging modes. The command can move multiple axes simultaneously and automatically handles acceleration/deceleration profiles.

### Parameters

* Axis Parameters: Specify the axis and distance to move and the distance
  * X - Move X axis
  * Y - Move Y axis
  * Z - Move Z axis
  * A - Move A axis
* F - Feedrate in mm/min. If not specified the system will uses 100% of the maximum rate for the slowest moving axis (if multiple axis are moved at the same time).
* S - Scale in % (continuous jog mode only)
* `-c` - Continuous jog mode

## **Continuous Jog Mode**

When used with the `-c` option the machine moves at a continuous speed in the direction specified by the move parameter, the distance part of the move command is ignored. It keeps moving in this direction until it is either stopped with `^Y` (Ctrl+Y), an emergency stop request, approaches a soft endstop, or if the keep-alive command is not received in 400ms. The keep-alive command:  `?1` . To use Continuous Jog properly requires sending the keep alive command repeatedly.

If Soft Limits are enabled and the spindle is approaching them the machine will slow down and stop within a  1mm way from the limit without raising a halt status. If the same direction is commanded again, the axis will move directly to the soft limit.

Example

```
$J -c X0.1  ; This will move the spindle in the X positive direction
```
