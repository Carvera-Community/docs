# Anatomy of a Carvera

This section provides details of the specifications and components inside the Carvera family of CNC machines. Remember that this article is fan written, and is not authoritative. If you have any doubts about what to expect from your machine, you should consult the manufacturer.

## Physical Dimensions

| Basic Info             | Carvera                                           | Carvera Air                                   | Z1                                            |
| ---------------------- | ------------------------------------------------- | --------------------------------------------- | --------------------------------------------- |
| Work Area (3 Axis)     | 36cm (X) \* 24cm (Y) \* 14cm (Z)                  | 30cm (X) \* 20cm (Y) \* 13cm (Z)              | 20cm(X) \* 20cm(Y) \* 10cm                    |
| Work Area (4 axis)     | 9.2cm (Diameter) \* 24cm (Length)                 | 9.2cm (Diameter) \* 20cm (Length)             | 8cm(Diameter)  \* 15cm (Length)               |
| Gantry Clearance       | 12cm                                              | 12cm                                          | 12cm                                          |
| Max Height (Lid Open)  | 84cm                                              | 84cm                                          | 84cm                                          |
| Footprint (Lid Closed) | 57.9cm (Width) \* 52cm (Depth) \* 54.1cm (Height) | 50cm (Width) \* 45cm (Depth) \* 45cm (Height) | 35cm (Width) \* 48cm (Depth) \* 45cm (Height) |
| Weight (Approx)        | 50kg                                              | 30kg                                          | 20kg                                          |

### Work Area Limitations&#x20;

#### Carvera

The Carvera has a cutting area of around 374mm (X) \* 256mm (Y). One thing to consider is that this cutting area is somewhat larger than the bed area which is 360mm (X) \* 240mm (Y)

Some implications of the design may not be immediately apparent:

* Due to the proximity of the tool holder to the bed, part of the bed is in difficult to use due to risks of crashing tools into the raised tool holder bar
* Due to the black plastic used by the tool proximity sensor approximately 15mm of the bed is lost in the X direction.

#### Carvera Air and Z1

Note that part of the bed is taken up by the tool setter. This prevents the complete use of the bed

### Electronics <a href="#electronics" id="electronics"></a>

Both the original Carvera, and Carver Air use very similar control boards and as a result the same firmware files, the firmware is written with switches to change config/functionality based which board is detected. The major differences in the board are the absence of vacuum and air assist headers on the Air board. The board uses a 32-bit ARM Cortex-M3 microcontroller called the NXP LPC1768 and runs a firmware based on [Smoothieware v1](https://github.com/Smoothieware/Smoothieware). A ESP8266 is used for Wifi connectivity.

The Z1 is similar in that it primarily uses a LPC1768 for motion control and a Smoothieware based firmware. It differs from the previous two models through it's use of a ESP32 for wifi connectivity. This ESP32 is connected to a camera inside the machine for remote monitoring of the enclosure.

#### Power Supply <a href="#power-supply" id="power-supply"></a>

|                          | Carvera                           | Carvera Air                       | Z1                                |
| ------------------------ | --------------------------------- | --------------------------------- | --------------------------------- |
| Supported Mains Input    | 100-120VAC / 200-240VAC @ 50/60Hz | 100-120VAC / 200-240VAC @ 50/60Hz | 100-120VAC / 200-240VAC @ 50/60Hz |
| System PSU               | 200w w/ 12v output                | 450w w/ 12v output                | Unknown                           |
| Spindle PSU              | 200w w/ 48v output                | shared with system PSU            | shared with system PSU            |
| System PSU Model         | Mean Well EPP-200-12              | Mean Well LRS-450-24              | Unknown                           |
| Spindle PSU Model        | Mean Well EPP-200-48              | N/A                               | N/A                               |
| Max AC Current (Typical) | 3.6A/115VAC 2A/230VAC             | 10A/115VAC 6A/230VAC              | Unknown                           |

### Spindle <a href="#spindle" id="spindle"></a>

|                       | Carvera                                      | Carvera Air                                  | Z1                                           |
| --------------------- | -------------------------------------------- | -------------------------------------------- | -------------------------------------------- |
| Max Motor Input Power | 200w                                         | 200w                                         | 150W                                         |
| Speed                 | 1000 - 15000 RPM                             | 3000 - 13000 RPM                             | 1000 - 13000 RPM                             |
| Motor Type            | Brushless DC                                 | Brushless DC                                 | Brushless DC                                 |
| Motor Speed Feedback  | Hall Effect                                  | None                                         | Unknown                                      |
| Included Collet       | 1/8in                                        | 1/8in                                        | 1/8in                                        |
| Available Collets     | 1/8in, 1/4in, 6mm, 4mm, 3mm, 8mm             | 1/8in, 1/4in, 6mm, 4mm, 3mm, 8mm             | 1/8in, 1/4in, 6mm, 4mm, 3mm, 8mm             |
| Collet System Type    | 263504                                       | 263504                                       | 263504                                       |
| Tool Library Size     | 6                                            | N/A                                          | N/A                                          |
| Cooling               | Air-cooled controlled by temperature monitor | Air-cooled controlled by temperature monitor | Air-cooled controlled by temperature monitor |
| Spindle Runout        | Less than 0.01mm                             | Less than 0.01mm                             | Less than 0.02mm                             |

### Motion System <a href="#motion-system" id="motion-system"></a>

|                         | Carvera                                                                                                 | Carvera Air                                                                                      | Z1                                                                                       | Z1 Pro                                                                                           |
| ----------------------- | ------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------ |
| X Drive System          | Ball screws with linear rails                                                                           | Ball screws with linear rods                                                                     | ACME Leadscrew with linear rails                                                         | Ball screws with linear rails                                                                    |
| X Max Movement Speed    | 300cm per minute                                                                                        | 300cm per minute                                                                                 | Unknown                                                                                  | Unknown                                                                                          |
| Y Drive System          | Ball screws with linear rods                                                                            | Ball screws with linear rods                                                                     | ACME Leadscrew with linear rails                                                         | Ball screws with linear rails                                                                    |
| Y Max Movement Speed    | 300cm per minute                                                                                        | 300cm per minute                                                                                 | Unknown                                                                                  | Unknown                                                                                          |
| Z Drive System          | Ball screws with linear rails                                                                           | Ball screws with linear rails                                                                    | ACME Leadscrew with linear rails                                                         | Ball screws with linear rails                                                                    |
| Z Max Movement Speed    | 200cm per minute                                                                                        | 200cm per minute                                                                                 | Unknown                                                                                  | Unknown                                                                                          |
| Motor Type              | <p>Closed loop Servo motors for X/Y/Z axis<br><br>Open Loop Nema17 stepper motor for A axis<br><br></p> | <p>Closed loop Smart Stepper for X/Y/Z axis<br><br>Open Loop Nema17 stepper motor for A axis</p> | <p>Open Loop Stepper for X/Y/Z axis<br><br>Open Loop Nema17 stepper motor for A axis</p> | <p>Closed loop Smart Stepper for X/Y/Z axis<br><br>Open Loop Nema17 stepper motor for A axis</p> |
| Motion Motor Resolution | 0.005 mm                                                                                                | 0.005 mm                                                                                         | 0.01mm                                                                                   | Unknown                                                                                          |
| Motion Driver IC        | BigTreeTech TMC2209                                                                                     | <p>Onboard stepper for X/Y/Z<br><br>A Axis driver DRV8825<br></p>                                | Unknown                                                                                  | Unknown                                                                                          |
| 4th Axis Max RPM        | <p>New Harmonic Drive: 6.6<br><br>Original 4th Axis: 30</p>                                             | 6.6                                                                                              | Unknown                                                                                  | Unknown                                                                                          |

### Dust/Chip Control <a href="#dust-chip-control" id="dust-chip-control"></a>

|                                       | Carvera                       | Carvera Air      | Z1              |
| ------------------------------------- | ----------------------------- | ---------------- | --------------- |
| Dust Control System                   | Integrated or external vacuum | External vacuum  | External vacuum |
| Dust Tank Volume                      | 0.8 liter                     | N/A              | N/A             |
| External Dust Port OD Size            | 26mm                          | 26mm             | 26mm            |
| External Compressed Air Input OD Size | 8mm                           | 8mm              | N/A             |
| External Compressed Air Input Fitting | Pushlock                      | Pushlock         | N/A             |
| Recommended Compressed Air Pressure   | 3.5 bar (50 psi)              | 3.5 bar (50 psi) | N/A             |
| Recommended Compressed Air Flow       | 40L/min                       | 40L/min          | N/A             |

### Laser Engraver <a href="#laser-engraver" id="laser-engraver"></a>

The laser module is in-built in the Carvera spindle head, and is an optional accessory for the Carvera Air and Z1

|             | Carvera           | Carvera Air       | Z1               |
| ----------- | ----------------- | ----------------- | ---------------- |
| Laser power | 2.5w              | 5w                | 5w               |
| Laser Type  | 445nm diode laser | 445nm diode laser | 445nm diode lase |
| Cooling     | Air-cooled        | N/A               | Unknown          |
