# Compatibility

## Hardware

What CNC mills does the Carvera Community firmware support?

<table><thead><tr><th width="152"></th><th width="525.5">Compatibility Status</th></tr></thead><tbody><tr><td>Carvera</td><td>Fully Supported</td></tr><tr><td>Carvera Air</td><td><p>Fully Supported on machines with Control Boards &#x3C; revision v1.9</p><p><a href="https://github.com/Carvera-Community/Carvera_Community_Firmware/issues/243">Investigation in progress to support the 1.9 revision</a>.</p></td></tr><tr><td>Z1</td><td>Planned to be supported</td></tr></tbody></table>

## Software

The Community stance is as follows:

> As we have no control over Makera, cross support between Makera and Community developed software (Controller/Firmware) is best effort. The **best** experience will be using both Community Firmware with Community Controller.&#x20;

The following matrix tables shows the tested cross compatibility status.

### Makera Firmware with Community Controller

|                             | Community Controller 2.0.0                              |
| --------------------------- | ------------------------------------------------------- |
| **Makera Firmware** >=1.0.4 | Non functioning                                         |
| **Makera Firmware** 1.0.3   | Functions correctly                                     |
| **Makera Firmware** 1.0.2   | Functions correctly                                     |
| **Makera Firmware** <=1.0.1 | Diagnostic Screen is non-functioning. Rest of app works |

### Makera Controller with Community Firmware

It is expected that if you are using the Community Firmware, that you are also using the Community Controller. Community development efforts have not been spent testing the Makera Controller + Community firmware scenarios.



## How to install Community Firmware if running **Makera Firmware** >=1.0.4

As Makera Firmware >=1.0.4 is not functioning with the Community Controller 2.0.0 if you want to install Community firmware, you need to follow this sequence:

1. Using [Makera Controller ≥ v0.9.13](https://github.com/MakeraInc/CarveraController/releases) follow the [Firmware Installation procedure ](firmware/installation-upgrade.md#installation)
2. After the machine resets it will be running the Community Firmware and you can now use the Community Controller

Alternatively if you have issues using the Makera Controller to upload the firmware, you can use the [SD Card method](firmware/installation-upgrade.md#alternative-install-method).
