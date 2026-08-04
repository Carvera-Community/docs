# Self-Calibration

Using the 3D Touch probe you can calibrate a number of machine specific offsets increasing the accuracy of key locations in the machine.

{% hint style="info" %}
This functionality requires a [3D Touch Probe](probing/3d-probe-support.md)
{% endhint %}

## M469.1 - Calibrate Anchor 1

### Description

M469.1 performs calibration of Anchor 1 position using a 3-axis probe. This is part of the ATC (Automatic Tool Changer) calibration system. The probe will move to the anchor 1 position and automatically perform the probing operation. Once the operation is done, check the MDI for results and run the specified config command.

{% hint style="warning" %}
The Anchor 1 position is used as part of the configuration for Anchor 2, the Tool rack (C1 only), and the tool length setter. If you adjust the anchor 1 position, you must also adjust the others.
{% endhint %}

### Parameters

* I: Invert probe direction (optional, default: 0)
  * 0: Normal probe direction
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

* I: Invert probe direction (optional, default: 0)
  * 0: Normal probe direction
  * 1: Inverted probe direction

### Example

```
M469.2              ; Calibrate Anchor 2 with normal probe
M469.2 I1           ; Calibrate Anchor 2 with inverted probe
```

{% hint style="info" %}
**Before you get too far into calibrating your 4th axis module. Ensure that you don't have any chips or burrs between the module and bed, or between the module and the track that it is bolted.**
{% endhint %}

## M469.4 - Calibrate A-Axis Headstock

### Description

M469.4 calibrates the A-axis headstock center position using a 3-axis probe. The probe will move to the rotation offset location for the existing 4th axis and automatically perform the probing operation. Once the operation is done, check the MDI for results and run the specified config command.

### Parameters

* I: Invert probe direction (optional, default: 0)
  * 0: Normal probe direction
  * 1: Inverted probe direction
* Y: Headstock width (optional, default: from config rotation\_width/2 + 5)
* E: Probe height (optional, default: from config rotation\_offset\_z - 6)

### Example

```
M469.4              ; Calibrate A-axis headstock with defaults
M469.4 Y50 E30      ; Calibrate at Y offset of 50, allowing the probe 30mm of downwards travel
```

## M469.5 - Calibrate A-Axis Height

### Description

M469.5 calibrates `rotation_offset_z` by probing a known-diameter pin in the 4th-axis chuck from four A orientations, after first probing the module reference surface (same surface used for absolute Z probe). Requires the machine to be homed and a 3-axis probe installed.

Check the MDI for suggested `config-set` values when finished.

### Parameters

* I: Invert probe for NC probe (optional, default: 0)
* X: Distance along the chuck axis from the headstock centreline to probe (optional, default: 60mm)
* C: Retract height between pin probes (optional, default: 4mm)
* R: Pin diameter (optional, default: 6mm)

### Example

```
M469.5              ; Calibrate A-axis height with defaults
M469.5 X60 C4 R4    ; 4mm pin, 4mm retract, X offset 60mm
```

## M469.6 - Calibrate A-Axis Centre of Rotation

### Description

M469.6 finds the true 4th-axis centre of rotation in Y and Z by probing a round artifact (for example the chuck body) from multiple directions. Unlike pin-based height calibration, this is not skewed by runout or surface imperfections on a single contact. For this reason this calibration routine is recommended over M469.4/5

M469.6 probes the module reference surface (same as M469.5) and temporarily sets both `coordinate.rotation_offset_y` and `coordinate.rotation_offset_z`. Run the printed `config-set` commands to make them permanent.

Requirements:

* Machine homed
* 3-axis probe selected (tool **0**, **9999**, or **≥ 999990**) with TLO already calibrated
* Probe tip positioned above the artifact centre, within clearance of its surface

### Parameters

* R: Artifact diameter (optional, default: 50mm — typical Sanou K02-50 chuck body)
* D: Probe tip diameter (optional, default: `zprobe.probe_tip_diameter` or 2mm)
* C: Clearance around the artifact (optional, default: 2mm)
* F: Positioning feed rate (optional, default: 400 mm/min)
* I: Invert probe for NC probe (optional, default: 0)

### Example

```
M469.6                 ; 50mm chuck body
```
