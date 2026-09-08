---
description: 4th-axis feed-rate handling was changed in version 2.1.0c
---

# 4th Axis Feed Rate

Community firmware changes how **A-axis** (rotary) speed is planned so rotary moves can use the **configured** maximum rate, without several stock limits that made 4th-axis work slower than the hardware allows.

## What changed versus stock

* The old **hard cap of 5 RPM** on rotary speed is gone. The machine uses the **configured** A-axis maximum rate. On the C1/CA1 harmonic-drive 4th axis that is about **6.6 RPM** at Makera’s advertised settings. Higher values are possible if you raise the config; that is at your own risk.
* Surface-speed math no longer adds an extra **+30 mm** to the stock diameter. On small diameters that padding made programmed feeds much slower than intended.
* Rotary rate is recalculated more often (on the order of **0.1 mm** of path instead of **1 mm**), so speed changes along a path are smoother.
* Combined moves (for example **Y+A** or **Z+A**) can speed up when needed so the **surface** feed stays closer to the programmed **F**.
* **G0** rapids are not held back by those rotary cutting-feed limits.

## How surface rate is chosen

For a G1/G2/G3 move that includes **A**, firmware estimates the radius of the cut from the current **Y** and **Z** work coordinates, then limits **A** so the **surface** speed is consistent with **F**. Pure **G0** and internal positioning moves skip that compensation.

In **G94** (mm/min), **F** is still millimetres per minute of **path**. Rotary-only moves convert that through the estimated circumference. In **[G93](../supported-commands/gcodes/inverse-time-feed-g93-g94.md)**, **F** is inverse time and the rotary path is timed that way instead.
