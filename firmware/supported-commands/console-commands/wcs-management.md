# WCS Management

## get wcs - Work Coordinate System Status Command

### Description

The get wcs command is a console command that displays comprehensive information about all Work Coordinate Systems (WCS) and related coordinate system data. This command provides detailed status information about coordinate system offsets, rotations, and current positions.\


### Parameters

None

### Output Format

The command outputs a structured report containing:

1. Current active coordinate system (G54, G55, G56, etc.)
2.  WCS Offset Data

    1. Each coordinate system's X, Y, Z, A, B offsets
    2. Rotation angle for each coordinate system

    In Format: \[G54:X.XXXX,Y.YYYY,Z.ZZZZ,A.AAAA,B.BBBB,R.RRRR]
3. Reference Positions:
   1. G28 position (machine home position)
   2. G30 position (secondary home position)
   3. G92 offset (temporary coordinate system offset)
4. Tool length offset (TLO)
5. Probe Information: Last probe position and status

#### Example Output

```
[current WCS: G54]
[G54:-197.0750,-61.7250,0.0000,0.0000,0.0000,0.0000]
[G55:10.0000,20.0000,5.0000,0.0000,0.0000,0.0000]
[G56:0.0000,0.0000,0.0000,0.0000,0.0000,0.0000]
[G57:0.0000,0.0000,0.0000,0.0000,0.0000,0.0000]
[G58:0.0000,0.0000,0.0000,0.0000,0.0000,0.0000]
[G59:0.0000,0.0000,0.0000,0.0000,0.0000,0.0000]
[G28:0.0000,0.0000,0.0000]
[G30:0.0000,0.0000,0.0000]
[G92:0.0000,0.0000,0.0000,0.0000,0.0000]
[Tool Offset:0.0000,0.0000,-13.8500]
[PRB:0.0000,0.0000,0.0000:0]
```

## Setting WCS Rotation

The WCS can be rotated using `G10` with the R parameter.  This is useful to compensate for work holding that might not be parallel with the X/Y axis.
