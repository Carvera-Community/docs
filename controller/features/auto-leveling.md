# Auto-Leveling

The Controller **Auto Level** feature probes a grid over the stock or bed and leaves bed-leveling compensation on so later cuts follow the measured surface. This is used for measuring a surface that is known to be imperfect, and retaining these imperfections. This is useful for engraving and PCB milling.

Community Controller can **shrink the probe area** (offsets) so the grid skips clamps, screws, or the tool rack. That setting is on the auto-level configuration screen:

<figure><img src="../../.gitbook/assets/autolevel_with_offsets_config.png" alt="Autolevel with offset configuration"><figcaption><p>Autolevel with offset config</p></figcaption></figure>

## Auto Z Probe

Enabling Auto-Leveling automatically enables **Auto Z Probe**. The Z-probe location can be configured to any position, or Auto Z Probe can be disabled entirely if you prefer to set Z manually.

{% hint style="warning" %}
Running Auto-Leveling with Auto Z Probe disabled will show a warning. The leveling grid relies on an accurate Z reference, so disabling the probe is only recommended when you have set Z manually and are confident in the value.
{% endhint %}
