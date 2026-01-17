---
description: Using a probe to measure the bed level
---

# Measuring Bed Flatness

You can easily measure the bed's flatness using the autolevel feature (`G32`). This will probe a grid around the bed and output an mesh array for visualisation. Knowing where you have high/low spots can help you make informed decisions about stock placement or even where to put shims to correct the level.&#x20;

The trick to this technique is for the autolevel probe points to avoid the mounting holes. To achieve this users have determined the right number of probe points and starting locations for the different model machines. Follow the below instructions to measure the bed flatness.

### Carvera Air

1. With your dominant hand, find the red emergency stop button. Become well acquainted. You and only you are responsible for the safe operation of your machine. E-stop the machine if you are in doubt. We not liable for damage to your machine.
2. Home the machine
3. Install and calibrate the Probe
4. Move the probe to roughly the center of the front left bolt. I like to be more to the right of center of the bolt just a touch (1mm). For me, this is the MCS location `X-293 Y-206`
5. Go to MDI and run `G32 R1 X17 Y8 A239 B196 I13 J11 H1`
6. Clear and disable the bed compensation map with the command `M370`
7. Grab the [log file](../controller/features/logging.md) from the Kivy directory. It can be found here:

```
Windows: C:\Users\USERNAME\.kivy\logs\
macOS: /Users/USERNAME/.kivy/logs/
Linux: /home/USERNAME/.kivy/logs/
```

7. At the end, there will be a grid of numbers. Remove `[INFO ] MDI Received:` from the lines.
8. Paste the numbers into [https://i.chillrain.com/index.php/3d-printer-auto-bed-leveling-mesh-visualizer/](https://i.chillrain.com/index.php/3d-printer-auto-bed-leveling-mesh-visualizer/) and click "Visualize"
