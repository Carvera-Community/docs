# Fusion 360

The Carvera Community Fusion 360 profiles can be downloaded from [here](https://github.com/Carvera-Community/Carvera_Community_Profiles/releases).

The Community developed version of the post-processor has a number of benefits and fixes above and beyond the Makera software:

* Separate profiles for the Carvera Air and Original Carvera
* Support for the Fusion 360 machine simulation functionality
* Ability to pass through Gcode directly into the nc files as an operation
* Ability to run machine specific macros such as turning vacuum/lights on/off using Action commands
* Allows the definition of tools numbered >6

## Installation

{% embed url="https://youtu.be/1xPcono_qTk" %}

## Post-Processor

### Action Commands

The following ACTION commands are supported by this post:\


* RapidA:# - rapids the a axis to degree position
* SaferA:# - Moves the z axis up to its clearance position then moves the a axis
* SafeZ -  Go to a safe z height (same height as the clearance position)
* SpindleOff - turns the spindle off
* Clearance - goes to carvea clearance position
* ClearAutoLevel - clears the auto level data from the machine
* ResetFeedOverride - resets the spindle override value to 100%
* FeedOverride:# - sets the feed override to a given percent. Useful for vetting new programs as well as speeding up an entire set of operations quickly
* AirOn -T urns the compressed air on
* AirOff - Turns the compressed air off
* VacOn - Turns on the vacuum
* VacOff - Turns off the vacuum
* AutoVacOn - turns on auto vacuum
* AutoVacOff - turns off auto vacuum
* LightOn - turns on the light
* LightOff - turns off the light
* ShrinkA - Shrinks the A axis with offset 0, so A365 will turn into A5



