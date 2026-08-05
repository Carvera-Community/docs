---
description: Auto Ext. Out was added in version 2.2.0
---

# Auto Ext. Out

Toggles firmware **extend-out mode** so an external vacuum or compressor connected on the extend port is turned on when the spindle is running.\
\
Users of the Original Carvera please note that to support the Makera Vacuum we have changed the default pin that Ext. Out toggles to the USB, if you want to revert it to controlling the Ext Out port on the Control board please use the command `config-set sd switch.extendout.output_pin 2.2` and then `reset` to apply.

This option can be enabled in one of two places:

* Spindle dropdown — **Auto Ext. Out**
* Config and Run screen — same toggle

<figure><img src="../../.gitbook/assets/Screenshot 2026-07-23 at 4.38.27 pm.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/Screenshot 2026-07-23 at 4.37.56 pm.png" alt=""><figcaption></figcaption></figure>
