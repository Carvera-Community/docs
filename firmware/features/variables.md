# Variables

The firmware implements a comprehensive and sophisticated variable system that enables dynamic G-code programming, parameter storage, and mathematical computations. This system allows users to store, retrieve, and manipulate numerical values throughout the execution of G-code providing significant flexibility and power for complex machining operations.

The syntax for variable assignment is `#variable_number = expression`

{% code title="Example of Variable Assignment" %}
```
#101 = 10.5                   ; Simple assignment
#102 = [5+3*2]                ; Mathematical expression
#103 = [#101+#102]            ; Using other variables
#104 = [sin[45]*10]           ; Using functions
#501 = 25.0                   ; Permanent variable
```
{% endcode %}

## Variable Categories

1. Local Variables (#101-#120): Stored in RAM, lost on power cycle
2. Permanent Variables (#501-#520): Stored in EEPROM, persistent
3. Probe Variables (#151-#156): Read-only, set by probe commands
4. System Variables: Most are read-only, except #150

| Variable Name | Function                                          | read only? |
| ------------- | ------------------------------------------------- | ---------- |
| #101-120      | general purpose variables. not saved on power off | n          |
| #501-520      | general purpose variables. saved on power off     | n          |
| #150          | probe tip diameter                                | y          |
| #151          | probed diameter X                                 | y          |
| #152          | probed diameter y                                 | y          |
| #153          | probed angle value                                | y          |
| #154          | probed corner center X                            | y          |
| #155          | probed corner center Y                            | y          |
| #156          | probed z position (M466)                          | y          |
| #2000         | current tool length offset                        | y          |
| #3026         | tool in spindle                                   | y          |
| #3027         | spindleRPM                                        | y          |
| #3033         | Is Optional Stop Mode Enabled?                    | y          |
| #5021         | machine position X Axis                           | y          |
| #5022         | machine position Y Axis                           | y          |
| #5023         | machine position Z Axis                           | y          |
| #5024         | machine position A Axis                           | y          |
| #5041         | Current WCS position X axis                       | y          |
| #5042         | Current WCS position Y axis                       | y          |
| #5043         | Current WCS position Z axis                       | y          |
| #5044         | Current WCS position A axis                       | y          |

## Examples

### Probe-Based Quality Control

```
; Probe workpiece dimensions
M461 X20 Y20                  ; Probe bore
#101 = #151                   ; Store X center
#102 = #152                   ; Store Y center
#103 = #154                   ; Store X diameter
#104 = #155                   ; Store Y diameter

; Check tolerances
#105 = [abs[#103 - 20]]       ; X diameter deviation
#106 = [abs[#104 - 20]]       ; Y diameter deviation
#107 = [#105 le 0.1]          ; X tolerance check (1=pass, 0=fail)
#108 = [#106 le 0.1]          ; Y tolerance check (1=pass, 0=fail)

; Report results
M118.1 P#107                  ; Print X tolerance result
M118.1 P#108                  ; Print Y tolerance result
```
