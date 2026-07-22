---
description: Advanced TLO Calibration was added in version 2.2.0
---

# Advanced TLO Calibration

Runs tool length calibration with optional XY offset from the tool setter and repeated measurements. This is in particular useful for probing large tools such as facemills.

You can open the Advanced TLO screen from the TOOL dropdown option as **Adv Calibrate**.
Using this screen sends `M491` with optional `X`, `Y`, and `R` (repeat count).

## Parameters

* **Repeats (R)** — number of TLO measurements (default 1). For face mills: probe once per cycle and rotate the cutter between cycles; firmware keeps the lowest cutting edge.
* **X / Y offset** — offset from the configured tool-setter position for this calibration only.

{% embed url="https://youtube.com/shorts/QoxUf1ruP8o" %}
Demonstration of M491 X-15
{% endembed %}
