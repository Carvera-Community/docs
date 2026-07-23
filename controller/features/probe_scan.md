---
description: Probe Scan was added in version 2.2.0
---

# Probe Scan

CMM-style probing tool for building a 2D sketch of probed and constructed features, then exporting the result as design file. Basically a way of using a 3D Probe to reverse engineer physical objects.

{% hint style="warning" %}
A 3D probe is required for X/Y side probing. The stock machine probe only works in Z.
{% endhint %}

You can open Probe Scan from the Tools section of the main control page of the Controller UI.

<figure><img src="../../.gitbook/assets/Screenshot 2026-07-23 at 4.03.07 pm.png" alt=""><figcaption></figcaption></figure>

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

## Screenshots

<div><figure><img src="../../.gitbook/assets/593271445-85587db7-9838-409c-b44f-52f2b1a637a6.png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/595805422-33025bb7-80aa-40bd-9328-165134e36e53.png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/595805595-65474793-8404-4a4b-96b2-1603705468af.png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/595805648-6bd1088d-a3c9-4cac-aee2-6e567e912d64.png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/595805685-67a3c8f6-b975-4f1c-a049-6d2b6ac5241b.png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/595805725-021f6c83-2c63-4fe5-8b9e-1c6a732839dc.png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/595805755-4385607a-a9fb-4354-9242-12537afdd5ad.png" alt=""><figcaption></figcaption></figure></div>
