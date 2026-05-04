# 3D Probing

{% hint style="warning" %}
A 3D probe is required to use most of the options. The probe included with the machine can only probe in the Z axis.
{% endhint %}

## Probing types in the Controller

Open the probing flows from the **Probing** button <img src="../../.gitbook/assets/image (37).png" alt="Probing" data-size="line"> in the center control panel. Geometry routines use **M** codes documented in [**Probing**](../../firmware/supported-commands/mcodes/probing.md). **Calibration** options in the UI use the **M469.x** machine calibration commands in [**Self-calibration**](../../firmware/supported-commands/mcodes/self-calibration.md).

| Probing type              | Firmware reference                                                                                                                                                                                                                                                                                                                                                                                                  | Notes                                                                                                                           |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| Outside corner            | [M464](../../firmware/supported-commands/mcodes/probing.md#m464-probe-outside-corner)                                                                                                                                                                                                                                                                                                                               | Finds outside corner locations                                                                                                  |
| Inside corner             | [M463](../../firmware/supported-commands/mcodes/probing.md#m463-probe-inside-corner)                                                                                                                                                                                                                                                                                                                                | Inside corner location                                                                                                          |
| Single axis               | [M466](../../firmware/supported-commands/mcodes/probing.md#m466-single-axis-probe-double-tap)                                                                                                                                                                                                                                                                                                                       | X, Y, and/or Z touch-off                                                                                                        |
| Bore / pocket             | [M461](../../firmware/supported-commands/mcodes/probing.md#m461-probe-bore-rectangular-pocket)                                                                                                                                                                                                                                                                                                                      | Inside circular or rectangular features                                                                                         |
| Boss / Block              | [M462](../../firmware/supported-commands/mcodes/probing.md#m462-probe-boss-rectangular-block)                                                                                                                                                                                                                                                                                                                       | Outside bosses and blocks                                                                                                       |
| Axis angle                | [M465](../../firmware/supported-commands/mcodes/probing.md#m465-probe-axis-angle)                                                                                                                                                                                                                                                                                                                                   | Angle for **WCS rotation** when used with that option                                                                           |
| Calibration               | [M469.1](../../firmware/supported-commands/mcodes/self-calibration.md#m469.1-calibrate-anchor-1), [M469.2](../../firmware/supported-commands/mcodes/self-calibration.md#m469.2-calibrate-anchor-2), [M469.4](../../firmware/supported-commands/mcodes/self-calibration.md#m469.4-calibrate-a-axis-headstock), [M469.5](../../firmware/supported-commands/mcodes/self-calibration.md#m469.5-calibrate-a-axis-height) | Measures and suggests machine calibration changes to offsets for anchor 1, anchor 2, A-axis headstock, A-axis height (4th axis) |
| Probe tip                 | [M460.1](../../firmware/supported-commands/mcodes/probing.md#m460.1-calibrate-probe-with-bore)                                                                                                                                                                                                                                                                                                                      | Measures the effective tip diameter on the probe                                                                                |
| 4th axis — stock leveling | [M465.1](../../firmware/supported-commands/mcodes/probing.md#m465.1-probe-4th-axis-a-axis-stock)                                                                                                                                                                                                                                                                                                                    | Angular alignment of **A-axis** stock (Controller **4th axis** probing section)                                                 |

## 3D Probing Screens

A number of [Probing routines](../../firmware/supported-commands/mcodes/probing.md) have been added to the firmware; the Controller provides graphical setup for many of them via the probing button above.

## Setting 3D Probe Tool

The option to set the current tool to 3D Probe is available under the set menu. Remember that this doesn't automatically Calibrate the Tool Length Offset, so you should run the Calibrate routine from the dropdown after setting the probe.

<figure><img src="../../.gitbook/assets/image (35).png" alt=""><figcaption></figcaption></figure>

If you start probing without a probe tool selected, the Controller may show a **popup** with suggestions to pick the correct tool.

## Usage Video

Below is a video from Fae showing how to use the 3 axis probe to probe the centre of an existing bore.

{% embed url="https://youtu.be/kcf5v0oKhDI" %}
