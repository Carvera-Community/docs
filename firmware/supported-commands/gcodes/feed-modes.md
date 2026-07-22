# Feed Modes

{% include "../../../.gitbook/includes/dev-feature-warning-banner.md" %}

### G93 - Inverse Time Feed Mode

#### Description

Sets the feed rate mode to inverse time. In this mode, the F parameter specifies the inverse of the time (in minutes) required to complete the move.&#x20;

The feed rate value represents 1/F minutes, where a higher value means a faster move. The firmware multiplies the feed rate by the move distance to convert it to mm/min for internal calculations. This mode is useful when you need consistent time per move regardless of distance, such as in synchronized multi-axis operations or when maintaining constant material removal rates.

If the requested location/time exceeds the maximum of any axis involved in the movent, the movement speed will be reduced to the max speed of the limiting axis and take longer than requested. See [anatomy-of-a-carvera.md](../../../anatomy-of-a-carvera.md "mention") for the Axis speed limits.

#### Parameters

None. This is a modal command that affects how subsequent F parameters are interpreted until G94 is called.

Note: The `F` parameter in subsequent G1, G2, or G3 commands is interpreted as F/min (inverse time) rather than mm/min. The actual feed rate in mm/min is calculated as: feed\_rate\_mm\_per\_min = F × distance\_mm

{% hint style="warning" %}
When operating under Inverse Time Feed mode note that the F parameter that is normally optional in G1/2/3 becomes mandatory
{% endhint %}

#### Example

```
G93             ; Enable inverse time feed mode
G1 X10 Y10 F60  ; Move 10mm in X and Y, taking 1/60 minute (1 second)
G1 X20 Y20 F30  ; Move 20mm in X and Y, taking 1/30 minute (2 seconds)
G94             ; Return to mm/min feed mode
```

<br>

### G94 - Feed Rate Per Minute Mode

#### Description

Sets the feed rate mode to feed rate per minute (mm/min). This is the default feed rate mode. In this mode, the `F` parameter directly specifies the feed rate in millimeters per minute. The move will be executed at the specified feed rate regardless of the distance traveled. This is the standard feed rate mode used in most G-code programs and is the default mode when the machine starts.

#### Parameters

None. This is a modal command that affects how subsequent `F` parameters are interpreted until G93 is called.

Note: The `F` parameter in subsequent G1, G2, or G3 commands is interpreted directly as mm/min.

#### Example

```
G94              ; Enable feed rate per minute mode (default)
G1 X10 Y10 F300  ; Move 10mm in X and Y at 300 mm/min
G1 X20 Y20 F300  ; Move 20mm in X and Y at 300 mm/min (same speed, longer time)
G93              ; Switch to inverse time feed mode
```
