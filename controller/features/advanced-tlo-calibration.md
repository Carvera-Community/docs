---
description: Advanced TLO Calibration was added in version 2.2.0
---

# Advanced TLO Calibration

Runs tool length calibration with optional XY offset from the tool setter and repeated measurements. This is in particular useful for probing large tools such as facemills.

You can open the Advanced TLO screen from the TOOL dropdown option as **Adv Calibrate**. Using this screen sends `M491` with optional `X`, `Y`, and `R` (repeat count).

<figure><img src="../../.gitbook/assets/Screenshot 2026-07-23 at 4.34.20 pm.png" alt=""><figcaption></figcaption></figure>



<figure><img src="../../.gitbook/assets/Screenshot 2026-07-23 at 4.35.21 pm.png" alt="" width="375"><figcaption></figcaption></figure>

## Parameters

* **Repeats (R)** — number of TLO measurements (default 1). For face mills: probe once per cycle and rotate the cutter between cycles; firmware keeps the lowest cutting edge.
* **X / Y offset** — offset from the configured tool-setter position for this calibration only. Unless you have relocated your TLO sensor, you probably will want to offset in the negative direction. The below video shows TLO probing at the offset X -15:

{% embed url="https://youtube.com/shorts/QoxUf1ruP8o" %}
Demonstration of M491 X-15
{% endembed %}
