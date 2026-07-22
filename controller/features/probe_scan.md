---
description: Probe Scan was added in version 2.2.0
---

# Probe Scan

CMM-style probing tool for building a 2D sketch of probed and constructed features, then exporting the result as design file.

{% hint style="warning" %}
A 3D probe is required for X/Y side probing. The stock machine probe only works in Z.
{% endhint %}

Use the Probe Scan entry from the main control page of the Controller UI.

## Workflow

1. Jog / position the probe as usual (keyboard jogging is available while the modal allows it).
2. Run a probe operation (outside/inside corner, bore, boss, single-axis, angle, and related macros). Results are captured into the feature list.
3. Construct derived geometry from selected features: segments, polylines, midpoints, intersections, tangents, circumcircles, and so on.
4. Optionally hide features in the 2D sketch without deleting them.
5. Export CSV / DXF / JSON, or load a previous scan (DXF/CSV). 

{% hint style="warning" %}
Save/Load is disabled on iOS currently.
{% endhint %}

## Notes

* Probe tip diameter can be set in the tool; the UI also shows the machine’s configured tip diameter.
* Probed angles can appear as labels on the sketch.
* Cancel / timeout ignores stale probe results so a late reply does not corrupt the session.
