# Self-Calibration

Using the 3D Touch probe you can calibrate a number of machine specific offsets increasing the accuracy of key locations in the machine.

{% hint style="warning" %}
This functionality requires a 3D Touch Probe
{% endhint %}

## M469.1 - Calibrate Anchor 1

### Description

M469.1 performs calibration of Anchor 1 position using a 3-axis probe. This is part of the ATC (Automatic Tool Changer) calibration system.

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

M469.2 performs calibration of Anchor 2 position using a 3-axis probe. This is part of the ATC calibration system.

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

M469.4 calibrates the A-axis headstock center position using a 3-axis probe.

### Parameters

* I: Invert probe direction (optional)
* 0: Normal probe direction (default)
* 1: Inverted probe direction
* Y: Headstock width (optional)
* E: Probe height (optional)

### Example

```
M469.4              ; Calibrate A-axis headstock with defaults
M469.4 I1 Y50 E10   ; Calibrate with custom parameters
```

## M469.5 - Calibrate A-Axis Height

### Description

M469.5 calibrates the A-axis center height using a 3-axis probe.

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
M469.5 I1 X60 E10 R6 ; Calibrate with custom parameters
```

