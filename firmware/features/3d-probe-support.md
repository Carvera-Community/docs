# 3D Probe Support

The Community firmware supports 3D Touch probes, these are measurement devices that trigger when they make contact in either of the 3 axis. Such devices connect to the machine via the probe interface port and can have wiring that is either Normally Open (NO) or Normally Closed (NC). As the stock probes included with the machine are NO, it is preferred to also use a NO 3D Probe, however functionality to support NC models has also been added to the Community firmware.

The 3D Probe functionality is written generically so many different models are supported. A popular inexpensive model is sold as "V6 3D Touch Probe" can be found on many online marketplaces.

All of the probing functionality of the OEM probe can be performed by the 3D Probe. For many people this means the 3D Probe becomes the only probe they use.

## Getting Started

These are the initial steps required to be completed before a new 3D probe can be used regularly.

{% stepper %}
{% step %}
### Make sure you are running the Community Firmware

The [Community firmware is required](../installation-upgrade.md) to be used on the machine to support 3D probe hardware. The easiest way to confirm that you are running the Community firmware is to run the MDI command "version" and ensuring the version response contains the character "c" denoting that it is a community firmware. eg: `2.0.0c`
{% endstep %}

{% step %}
### Connect the probe

Set the tool to number to ≥ **999990** for the firmware to register that you are using a 3D probe. This can be done using the Controller by [setting/changing the tool to **3D Probe**](../../controller/features/3d-probing.md) or by running the command `M6 T999990` in the **MDI**.

Once connected and correct tool number has been selected, the probe should have a LED light to show that it is powered and ready for use. The "V6 3D Touch Probe" has a green led that shines through the clear plastic in the probe body (part #5 in [Figure 1](3d-probe-support.md#notes-for-v6-3d-touch-probe)).
{% endstep %}

{% step %}
### Test the probe

It's important to test that the machine registers when the probe is triggered. The Community firmware has 3D Probe Crash Protection which will halt the machine if the probe is activated while the spindle is moving and a probe macro is not being executed. This will help protect the probe stylus from damage from unexpected collisions, however this functionality requires the machine correctly receive the signal that the probe has been triggered.

You can test that the machine is receiving probe trigger signals by lightly pressing the probe tip with your hands. On the "V6 3D Touch Probe" the green led will change to red when it is triggered, and in the Diagnostic Panel of the Controller the Probe input should be lite green.

<figure><img src="../../.gitbook/assets/image (32).png" alt="" width="563"><figcaption></figcaption></figure>
{% endstep %}

{% step %}
### Physical Probe Calibration

When you first receive the probe you should consult the manufacturer about how it should be calibrated. More expensive probes have self-calibration functionality, but the inexpensive probes typically will require some adjustment out of the box to get the best results. See notes below for the "V6 3D Touch Probe" [calibration](3d-probe-support.md#calibration).
{% endstep %}

{% step %}
### Probe tip diameter config

Inexpensive probes like the V6 3D Touch probe do not have a way to compensate for the probe tip tilt and activation distance. Thus probe tip diameter needs to be adjusted to reflect the distance before the probe registers contact. This value is best determined using one of the [M460 ](../supported-commands/mcodes/probing.md#m460-probe-calibration)macros and probing against geometry of known dimensions. This means the probe tip diameter is not just it's physical diameter but also adjusted by the activation distance. On probe tips of 2mm diameter and length 22mm the effective probe tip diameter is typically around 1.6-1.8mm.

The text output of `M460` will provide the command to run which saves the probe tip diameter to the machine config eg. `config-set sd zprobe.probe_tip_diameter 1.700`  Once this is set the probe tip diameter does not need to be provided during usage.

You are now ready to use the probe!
{% endstep %}
{% endstepper %}

## Usage

Regular usage of the probe involves the following steps:

{% stepper %}
{% step %}
### Load the Probe into the spindle collet

Users of the CA1 will be familiar for how to manually load tools.

Users of the C1 will need to drop other tools and Unclamp/Clamp the collet to manually load a tool not in the tool rack. This can be done using the Controller buttons <img src="../../.gitbook/assets/image (33).png" alt="" data-size="line"> and <img src="../../.gitbook/assets/image (34).png" alt="" data-size="line"> (found in the ATC Topbar drop down) or using the MDI commands `M490.1` /`M490.2`&#x20;

Hold the probe in the collet until the machine has clamped it.
{% endstep %}

{% step %}
### Connect the probe wiring to the probe port
{% endstep %}

{% step %}
### Set the current tool to Probe

By [setting/changing the tool to **3D Probe**](../../controller/features/3d-probing.md) **in the Controller** or by running the command `M6 T999990` in the **MDI**.
{% endstep %}

{% step %}
### Calibrate the TLO

For Z probing to be accurate the machine needs to perform a TLO calibration. This can be triggered via the ATC Topbar drop down option <img src="../../.gitbook/assets/image (30).png" alt="" data-size="line"> or by running the MDI command `M491` .
{% endstep %}

{% step %}
### Ready to use Probing Commands

Now the probe can be used in the [Controller ](../../controller/features/3d-probing.md)or [MDI](../supported-commands/mcodes/probing.md)
{% endstep %}
{% endstepper %}

## Notes for V6 3D Touch Probe

[Fae Corrigan](https://www.patreon.com/propsmonster) has written up an [Instructable guide](https://www.instructables.com/Carvera-Touch-Probe-Modifications/) for wiring up and using the 3D Touch Probe on the Carvera Air (**CA1**), and multiple methods for the Original Carvera (**C1**).

To use this probe on the **CA1** a JST connector simply needs to be attached to the cabling, after which it can be plugged in and used in-place of the stock wired probe.

On the **C1** it is much easier to power and connect the 3D Probe when the additional electrical harness for the [Harmonic Drive 4th axis](https://app.gitbook.com/u/2Uxw6VVk0BgMm2btzVcpMw1FwPH3) is present on the machine as it uses the same JST connector as the CA1. Without the Harmonic Drive wiring box, Fae provides recommends using _**method 3: GX12 aviation 3 pin connector** for this situation_.

### Shank Size

Another consideration which applies to both the CA1 and C1 is the probe shank diameter. These probes are only available in 4 and 6mm shanks. The collet system used by the Carvera has collets of these sizes but they are additional purchases. The only collet that comes with the machine is 1/8" and thus too small to use unmodified.&#x20;

One option to avoid this challenge is to modify the tail shaft from the probe turning it down to 1/8" diameter on a lathe or mill using the Carvera 4th Axis. The tail shaft is removed by loosening the calibration set screws **(**&#x69;tem _**#14**_ in Fig 1).

<figure><img src="../../.gitbook/assets/image (31).png" alt="" width="563"><figcaption><p>Figure 1: Exploded part diagram of V6 3D Touch Probe</p></figcaption></figure>

### Calibration

It is essential for the probe tip to be concentric to the tail shaft, otherwise the probe's accuracy and repeatability in different directions will be affected.

The way the probe is calibrated is by turned the 4 set screws **(**&#x69;tem _**#14**_ in Figure 1). Two opposing set screws need to be adjusted together, one loosened while the other tightened. This will result in the probe's body moving in relation to the tail shaft.

The most accurate way to calibrate the probe is to use a dial test indicator to indicate in the probe tip, there will be a video of this process linked here soon. An alternative is to repeatedly probe in a single axis against something secured to the bed (for example one of the L anchors). By comparing the results of the output while rotating the probe to face the different sides will give indication to the alignment. Ideally all of the sides should register the same value. It's possible to achieve 0.01mm accuracy with this adjustment, however adjustment beyond 0.05mm requires very fine changes to the set screws (less than 1/8th rotations).

It's recommended to first align two opposing sides, then the other two, then repeat for the first set, before reviewing all 4. This is required because the stylus holder (part #8 in Figure 1) of the probe is connected to the body via 3 points, and adjustments to the second set of faces results in slight movement of the initial set.

The probe should be calibrated any time the probe stylus (**item #10**) is replaced.
