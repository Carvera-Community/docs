---
description: WCS Rotation was added in version 0.10.0
---

# WCS Rotation

If you are using a vise you will know that you need to tram the workholding to be parallel with the machine's X/Y axis, otherwise the workpiece will experience misalignment during machining, resulting in out-of-square parts, inaccurate features, and potential clamping issues that can compromise both dimensional accuracy and part quality.

No more! With the _**Rotated WCS**_ feature a 3D Probe can be used to determine the stock rotation and correct the machine movements entirely in software without needing to make any physical changes. This WCS rotation is even applied for subsequent probing operations.

To use this feature you need the Community Firmware 1.0.9c or above, and v0.10.0 of the Community Controller.

<figure><img src="../../.gitbook/assets/rotated_wcs_support.png" alt=""><figcaption><p>Preview visualization showing rotated WCS applied</p></figcaption></figure>

## Usage

There are a few ways the WCS rotation can be set.

### Via Probing Screen

{% stepper %}
{% step %}
#### Secure your stock to the bed

No need to tram it in!
{% endstep %}

{% step %}
#### Use a 3D probe to determine the rotation

Use the Angle probing with the "Set WCS Rotation" option enabled to probe the fixed jaw of your vise

<figure><img src="../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
#### Probe the WCS origin

Now the WCS rotation correction has been set continue as normal probing your WCS origin
{% endstep %}
{% endstepper %}

### Via Workspace

If you know the rotation angle you can apply it directly via the `Set Rotation option` on the WCS Workspace Top Bar dropdown

<figure><img src="../../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

## How to know if WCS Rotation Correction is being Applied?

You can quickly tell if a WCS Rotation Correction is being applied as the WCS WorkSpace Top Bar button text will be Blue and a rotation degree will be shown below it:

<figure><img src="../../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

## Clearing a WCS Rotation <a href="#clearing-a-rotation" id="clearing-a-rotation"></a>

The WCS Rotation can be cleared by `Set Rotation option` to 0 degrees, or using the Advanced WCS Settings screen and pushing <img src="../../.gitbook/assets/image (3) (1).png" alt="Clear Rotation" data-size="line"> on the workspace.
