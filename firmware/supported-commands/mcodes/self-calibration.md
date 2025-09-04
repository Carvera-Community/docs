# Self-Calibration

Using the 3D Touch probe you can calibrate a number of machine specific offsets increasing the accuracy of key locations in the machine.

{% hint style="warning" %}
This functionality requires a 3D Touch Probe
{% endhint %}

## M469.1 - Calibrate Anchor 1

### Description

M469.1 performs calibration of Anchor 1 position using a 3-axis probe. This is part of the ATC (Automatic Tool Changer) calibration system. The probe will move to the anchor 1 position and automatically perform the probing operation. Once the operation is done, check the MDI for results and run the specified config command.

### Parameters

* I: Invert probe direction (optional)
* 0: Normal probe direction (default)
* 1: Inverted probe direction (NC)

### Example

```
M469.1              ; Calibrate Anchor 1 with normal probe
M469.1 I1           ; Calibrate Anchor 1 with inverted probe
```

## M469.2 - Calibrate Anchor 2

### Description

M469.2 performs calibration of Anchor 2 position using a 3-axis probe. This is part of the ATC calibration system. The probe will move to the anchor 2 position and automatically perform the probing operation. Once the operation is done, check the MDI for results and run the specified config command.

### Parameters

* I: Invert probe direction (optional)
* 0: Normal probe direction (default)
* 1: Inverted probe direction

### Example

```
M469.2              ; Calibrate Anchor 2 with normal probe
M469.2 I1           ; Calibrate Anchor 2 with inverted probe
```

## M469.4 - Calibrate A-Axis Headstock

### Description

M469.4 calibrates the A-axis headstock center position using a 3-axis probe. The probe will move to the rotation offset location for the existing 4th axis and automatically perform the probing operation. Once the operation is done, check the MDI for results and run the specified config command.

### Parameters

* I: Invert probe direction (optional)
  * 0: Normal probe direction (default)
  * 1: Inverted probe direction
* Y: Headstock width (optional)
* E: Probe height (optional)

### Example

```
M469.4              ; Calibrate A-axis headstock with defaults
M469.4 Y50 E30      ; Calibrate at Y offset of 50, allowing 30mm
```

## M469.5 - Calibrate A-Axis Height

### Description

M469.5 calibrates the A-axis center height using a 3-axis probe. Full documentation in the works

### Parameters

* I: Invert probe direction (optional)
  * 0: Normal probe direction (default)
  * 1: Inverted probe direction
* X: X-axis offset (optional)
* E: Probe height (optional)
* R: Pin diameter (optional)

### Example

```
M469.5              ; Calibrate A-axis height with defaults
M469.5 X60 E40 R4   ; Calibrate with a 4mm pin, allowing the probe to move 40mm down, at the x offset of 60mm
```

