---
layout: post
title: "ANSI Standard Device Protection Function Numbers"
description: >-
  ANSI Standard Device Protection Function Numbers. This list contains all the IEEE device function numbers, including suffixes, as well as the most common prefixes.
date: 2026-04-28
author: Mahmoud Lotfi
file_name: 2026-04-28-eplan-ansi-device-numbers.md

categories: [EPLAN, ANSI, protection_system, device_numbering]
tags: [EPLAN, ANSI, protection_system, device_numbering]

pin: False
math: true
mermaid: true
comments: true
toc: true
render_with_liquid: false

image:
  path: /assets/img/posts/eplan.jpg
  alt: ANSI Standard Device Numbers
  lqip: data:image/webp;base64,UklGRjoAAABXRUJQVlA4IC4AAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
---

# ANSI Standard Device Protection Function Numbers

> **Topic:** **All IEEE device function numbers**, including suffixes, as well as the most common prefixes
> **Level:** Beginner to Advanced

---

## Overview

### Suffix

Suffix letter or number may be used with the device number;

- for example, suffix N is used if the device is connected to a Neutral wire (example: 59N in a relay is used for protection against Neutral Displacement); and suffixes X, Y, Z are used for auxiliary devices.
- Similarly, the "G" suffix can denote a "ground", hence a "51G" is a time overcurrent ground relay. 
- The "G" suffix can also mean "generator", hence an "87G" is a Generator Differential Protective Relay while an "87T" is a Transformer Differential Protective Relay.
- "F" can denote "field" on a generator or "fuse", as in the protective fuse for a pickup transformer.
- Suffix numbers are used to distinguish multiple "same" devices in the same equipment such as 51–1, 51–2.

### Prefix

- Prefixes are used to provide additional information on the function of the device.
- For example, the prefix:
  - **P** is used for **Phase**,
  - **L** for **Line**,
  - **G** for **Ground**,
  - **N** for **Neutral**,
  - **R** for **Reverse**,
  - **S** for **Stator**,
  - **T** for **Transformer**,
  - **B** for **Bus**.

---

## Device Numbers

| Device No. | Description                                                                                   |
| :--------- | :-------------------------------------------------------------------------------------------- |
| 1          | Master Element                                                                                |
| 2          | Time Delay Starting or Closing Relay                                                          |
| 3          | Checking or Interlocking Realy                                                                |
| 4          | Master Contactor                                                                              |
| 5          | Stopping Device                                                                               |
| 6          | Starting Circuit Breaker                                                                      |
| 7          | Rate of Change Relay                                                                          |
| 8          | Control Power Disconnecting Device                                                            |
| 9          | Reversing Device                                                                              |
| 10         | Unit Sequence Switch                                                                          |
| 11         | Multifunction Device                                                                          |
| 12         | Overspeed Device/Protection                                                                   |
| 13         | Synchronous-Speed Device                                                                      |
| 14         | Underspeed Device                                                                             |
| 15         | Speed or Frequency Matching Device                                                            |
| 16         | Communication Networking Device                                                               |
| 17         | Shunting or Discharge Switch                                                                  |
| 18         | Accelerating or Decelerating Device                                                           |
| 19         | Motor Starter / Starting-to-Running Transition Contactor                                      |
| 20         | Electrically-Operated Valve                                                                   |
| 21         | Distance Relay                                                                                |
| 21G        | Ground Distance                                                                               |
| 21P        | Phase Distance                                                                                |
| 22         | Equalizer Circuit Breaker                                                                     |
| 23         | Temperature Control Device                                                                    |
| 24         | Volts-per-Hertz Relay / Overfluxing                                                           |
| 25         | Synchronizing or Synchronism-Check Device                                                     |
| 26         | Apparatus Thermal Device                                                                      |
| 27         | Undervoltage Relay                                                                            |
| 27P        | Phase Undervoltage                                                                            |
| 27TN       | Third Harmonic Neutral Undervoltage                                                           |
| 27X        | Auxiliary Undervoltage                                                                        |
| 27 AUX     | Undervoltage Auxiliary Input                                                                  |
| 27/27X     | Bus/Line Undervoltage                                                                         |
| 28         | Flame Detector                                                                                |
| 29         | Isolating Contactor                                                                           |
| 30         | Annunciator Relay                                                                             |
| 31         | Separate Excitation Device                                                                    |
| 32         | Directional Power Relay                                                                       |
| 32L        | Low Forward Power                                                                             |
| 32N        | Wattmetric Zero-Sequence Directional                                                          |
| 32P        | Directional Power                                                                             |
| 32R        | Reverse Power                                                                                 |
| 33         | Position Switch                                                                               |
| 34         | Master Sequence Device                                                                        |
| 35         | Brush-Operating or Slip-ring Short Circuiting Device                                          |
| 36         | Polarity or Polarizing Voltage Device                                                         |
| 37         | Undercurrent or Underpower Relay                                                              |
| 37P        | Underpower                                                                                    |
| 38         | Bearing Protective Device / Bearing Rtd                                                       |
| 39         | Mechanical Condition Monitor                                                                  |
| 40         | Field Relay / Loss of Excitation                                                              |
| 41         | Field Circuit Breaker                                                                         |
| 42         | Running Circuit Breaker                                                                       |
| 43         | Manual Transfer or Selector Device                                                            |
| 44         | Unit Sequence Starting Relay                                                                  |
| 45         | Atmospheric Condition Monitor                                                                 |
| 46         | Reverse-Phase or Phase Balance Current Relay or Stator Current Unbalance                      |
| 47         | Phase-Sequence or Phase Balance Voltage Relay                                                 |
| 48         | Incomplete Sequence Relay / Blocked Rotor                                                     |
| 49         | Machine or Transformer Thermal Relay / Thermal Overload                                       |
| 49RTD      | RTD Biased Thermal Overload                                                                   |
| 50         | Instantaneous Overcurrent Relay                                                               |
| 50BF       | Breaker Failure                                                                               |
| 50DD       | Current Disturbance Detector                                                                  |
| 50G        | Ground Instantaneous Overcurrent                                                              |
| 50N        | Neutral Instantaneous Overcurrent                                                             |
| 50P        | Phase Instantaneous Overcurrent                                                               |
| 50_2       | Negative Sequence Instantaneous Overcurrent                                                   |
| 50/27      | Accidental Energization                                                                       |
| 50/74      | Ct Trouble                                                                                    |
| 50/87      | Instantaneous Differential                                                                    |
| 50EF       | End Fault Protection                                                                          |
| 50IG       | Isolated Ground Instantaneous Overcurrent                                                     |
| 50LR       | Acceleration Time                                                                             |
| 50NBF      | Neutral Instantaneous Breaker Failure                                                         |
| 50SG       | Sensitive Ground Instantaneous Overcurrent                                                    |
| 50SP       | Split Phase Instantaneous Current                                                             |
| 51         | Ac Time Overcurrent Relay                                                                     |
| 51         | Overload                                                                                      |
| 51G        | Ground Time Overcurrent                                                                       |
| 51N        | Neutral Time Overcurrent                                                                      |
| 51P        | Phase Time Overcurrent                                                                        |
| 51V        | Voltage Restrained Time Overcurrent                                                           |
| 51R        | Locked / Stalled Rotor                                                                        |
| 51_2       | Negative Sequence Time Overcurrent                                                            |
| 52         | Ac Circuit Breaker                                                                            |
| 53         | Exciter or Dc Generator Relay                                                                 |
| 54         | Turning Gear Engaging Device                                                                  |
| 55         | Power Factor Relay                                                                            |
| 56         | Field Application Relay                                                                       |
| 57         | Short-Circuiting or Grounding Device                                                          |
| 58         | Rectification Failure Relay                                                                   |
| 59         | Overvoltage Relay                                                                             |
| 59B        | Bank Phase Overvoltage                                                                        |
| 59P        | Phase Overvoltage                                                                             |
| 59N        | Neutral Overvoltage                                                                           |
| 59NU       | Neutral Voltage Unbalance                                                                     |
| 59P        | Phase Overvoltage                                                                             |
| 59X        | Auxiliary Overvoltage                                                                         |
| 59_2       | Negative Sequence Overvoltage                                                                 |
| 60         | Voltage or Current Balance Relay                                                              |
| 60N        | Neutral Current Unbalance                                                                     |
| 60P        | Phase Current Unbalance                                                                       |
| 61         | Density Switch or Sensor                                                                      |
| 62         | Time-Delay Stopping or Opening Relay                                                          |
| 63         | Pressure Switch Detector                                                                      |
| 64         | Ground Protective Relay                                                                       |
| 64F        | Field Ground Protection                                                                       |
| 64S        | Sub-harmonic Stator Ground Protection                                                         |
| 64TN       | 100% Stator Ground                                                                            |
| 65         | Governor                                                                                      |
| 66         | Notching or Jogging Device/Maximum Starting Rate/Starts Per Hour/Time Between Starts          |
| 67         | Ac Directional Overcurrent Relay                                                              |
| 67G        | Ground Directional Overcurrent                                                                |
| 67N        | Neutral Directional Overcurrent                                                               |
| 67P        | Phase Directional Overcurrent                                                                 |
| 67SG       | Sensitive Ground Directional Overcurrent                                                      |
| 67_2       | Negative Sequence Directional Overcurrent                                                     |
| 68         | Blocking Relay / Power Swing Blocking                                                         |
| 69         | Permissive Control Device                                                                     |
| 70         | Rheostat                                                                                      |
| 71         | Liquid Switch                                                                                 |
| 72         | Dc Circuit Breaker                                                                            |
| 73         | Load-Resistor Contactor                                                                       |
| 74         | Alarm Relay                                                                                   |
| 75         | Position Changing Mechanism                                                                   |
| 76         | Dc Overcurrent Relay                                                                          |
| 77         | Telemetering Device                                                                           |
| 78         | Phase Angle Measuring or Out-of-Step Protective Relay                                         |
| 78V        | Loss of Mains                                                                                 |
| 79         | Ac Reclosing Relay / Auto Reclose                                                             |
| 80         | Liquid or Gas Flow Relay                                                                      |
| 81         | Frequency Relay                                                                               |
| 81O        | Over Frequency                                                                                |
| 81R        | Rate-of-Change Frequency                                                                      |
| 81U        | Under Frequency                                                                               |
| 82         | Dc Reclosing Relay                                                                            |
| 83         | Automatic Selective Control or Transfer Relay                                                 |
| 84         | Operating Mechanism                                                                           |
| 85         | Carrier or Pilot-Wire Receiver Relay                                                          |
| 86         | Locking-Out Relay                                                                             |
| 87         | Differential Protective Relay                                                                 |
| 87B        | Bus Differential                                                                              |
| 87G        | Generator Differential                                                                        |
| 87GT       | Generator/Transformer Differential                                                            |
| 87LG       | Ground Line Current Differential                                                              |
| 87S        | Stator Differential / Percent Differential                                                    |
| 87L        | Segregated Line Current Differential                                                          |
| 87M        | Motor Differential                                                                            |
| 87O        | Overall Differential                                                                          |
| 87PC       | Phase Comparison                                                                              |
| 87RGF      | Restricted Ground Fault                                                                       |
| 87T        | Transformer Differential                                                                      |
| 87V        | Voltage Differential                                                                          |
| 88         | Auxiliary Motor or Motor Generator                                                            |
| 89         | Line Switch                                                                                   |
| 90         | Regulating Device                                                                             |
| 91         | Voltage Directional Relay                                                                     |
| 92         | Voltage And Power Directional Relay                                                           |
| 93         | Field-Changing Contactor                                                                      |
| 94         | Tripping or Trip-Free Relay                                                                   |
| 50/74      | Ct Supervision                                                                                |
| 27/50      | Accidental Generator Energization                                                             |
| 27TN/59N   | 100% Stator Earth Fault                                                                       |

---

## Quick Reference Tables (Color-Coded)

Here are color-coded tables for quick reference:

### Basic Devices (1-20)

| Color Code | Device # | Description                 | Color Code | Device # | Description                  |
| :--------: | :------: | :-------------------------- | :--------: | :------: | :--------------------------- |
|  **RED**   |    1     | Master Contactor            |  **GREEN** |    11    | Selector Switch              |
|  **BLUE**  |    2     | Steam Inlet Valve           |  **GREEN** |    12    | Special Control Selector     |
|  **BLUE**  |    3     | Circuit Breaker             |  **GREEN** |    13    | Special Control Selector     |
|  **BLUE**  |    4     | Stop Valve                  |  **GREEN** |    14    | Special Control Selector     |
|  **BLUE**  |    5     | Stopping Device             |  **RED**   |    15    | Under Voltage Relay          |
|  **RED**   |    6     | Speed Switch                |  **RED**   |    16    | Compensator Device           |
|  **RED**   |    7     | Cylinder Drain Valve        |  **RED**   |    17    | Dc Reclosing Relay           |
|  **GREEN** |    8     | Operating Circuit           |  **GREEN** |    18    | Special Control Device       |
|  **GREEN** |    9     | Starting Device             |  **GREEN** |    19    | Starting Circuit             |
|  **GREEN** |    10    | Operating Circuit           |  **RED**   |    20    | Cylinder Drain Valve         |

### Protection Relays (21-40)

| Color Code | Device # | Description                       | Color Code | Device # | Description                  |
| :--------: | :------: | :-------------------------------- | :--------: | :------: | :--------------------------- |
|  **RED**   |    21    | Backup Protection Relay           |  **GREEN** |    31    | Trip Contact                 |
|  **RED**   |    22    | Backup Protection Relay           |  **GREEN** |    32    | Directional Device           |
|  **RED**   |    23    | Temperature Control Device        |  **RED**   |    33    | Position Switch              |
|  **RED**   |    24    | Rate-of-Change Frequency          |  **RED**   |    34    | Starting-Frequency Limit     |
|  **RED**   |    25    | Synchronizing or Sync-Check       |  **GREEN** |    35    | Frequency Indicating         |
|  **RED**   |    26    | Thermal Device                    |  **GREEN** |    36    | Polarity Contact             |
|  **RED**   |    27    | Under Voltage Relay               |  **RED**   |    37    | Undercurrent Relay           |
|  **GREEN** |    28    | Automatic Voltage Regulator       |  **RED**   |    38    | Special Control Device       |
|  **RED**   |    29    | Blocking Relay                    |  **RED**   |    39    | Power-Factor Relay           |
|  **RED**   |    30    | Auxiliary Relay                   |  **GREEN** |    40    | Voltage Limiting Device      |

### Control Devices (41-60)

| Color Code | Device # | Description                        | Color Code | Device # | Description                     |
| :--------: | :------: | :--------------------------------- | :--------: | :------: | :------------------------------ |
|  **GREEN** |    41    | Transfer Trip                      |  **GREEN** |    51    | Time-Delay Overcurrent          |
|  **GREEN** |    42    | Voltage Control Switch             |  **GREEN** |    52    | Circuit Breaker                 |
|  **GREEN** |    43    | Automatic Selection or Transfer    |  **GREEN** |    53    | Control Switch                  |
|  **GREEN** |    44    | Differential Device                |  **GREEN** |    54    | Starting-Frequency Selector     |
|  **RED**   |    45    | Overload Alarm Contact             |  **RED**   |    55    | Time-Delay Overcurrent          |
|  **GREEN** |    46    | Current-Balance or Negative-Seq.   |  **RED**   |    56    | Transfer Switch                 |
|  **GREEN** |    47    | Undervoltage Protection            |  **RED**   |    57    | Special Control Device          |
|  **RED**   |    48    | Time Delay or Inhibit              |  **GREEN** |    58    | Protection Relay                |
|  **GREEN** |    49    | Thermal Overload Relay             |  **GREEN** |    59    | Over Voltage Relay              |
|  **RED**   |    50    | Instantaneous Overcurrent Relay    |  **GREEN** |    60    | Voltage Regulation Device       |

### High-Speed & Critical Protection (61-80)

| Color Code | Device # | Description                        | Color Code | Device # | Description                     |
| :--------: | :------: | :--------------------------------- | :--------: | :------: | :------------------------------ |
|  **GREEN** |    61    | Density Switch or Sensor           |  **GREEN** |    71    | Liquid Level Switch             |
|  **GREEN** |    62    | Time-Delay Stopping or Opening     |  **RED**   |    72    | Dc Circuit Breaker              |
|  **GREEN** |    63    | Pressure Switch Detector           |  **GREEN** |    73    | Load-Resistor Contactor         |
|  **RED**   |    64    | Ground Protective Relay            |  **GREEN** |    74    | Alarm Relay                     |
|  **GREEN** |    65    | Governor                           |  **GREEN** |    75    | Position Changing Mechanism     |
|  **GREEN** |    66    | Notching or Jogging Device         |  **RED**   |    76    | Dc Overcurrent                  |
|  **RED**   |    67    | Directional Overcurrent            |  **GREEN** |    77    | Telemetering Device             |
|  **RED**   |    68    | Blocking Relay / Power Swing       |  **RED**   |    78    | Phase Angle or Out-of-Step      |
|  **GREEN** |    69    | Permissive Control                 |  **RED**   |    79    | Reclosing Relay / Auto Reclose  |
|  **GREEN** |    70    | Rheostat                           |  **GREEN** |    80    | Liquid or Gas Flow              |

### Major Equipment & Specialized Protection (81-94)

| Color Code | Device # | Description                          | Color Code | Device # | Description                  |
| :--------: | :------: | :----------------------------------- | :--------: | :------: | :--------------------------- |
|  **RED**   |    81    | Frequency Relay                      |  **RED**   |    91    | Voltage Directional Relay    |
|  **RED**   |    82    | Dc Reclosing Relay                   |  **RED**   |    92    | Voltage & Power Directional  |
|  **GREEN** |    83    | Selective Control                    |  **GREEN** |    93    | Field-Changing Contactor     |
|  **GREEN** |    84    | Operating Mechanism                  |  **GREEN** |    94    | Tripping or Trip-Free Relay  |
|  **RED**   |    85    | Carrier/Pilot-Wire Receiver          |            |          |                              |
|  **GREEN** |    86    | Locking-Out Relay                    |            |          |                              |
|  **RED**   |    87    | Differential Protection              |            |          |                              |
|  **GREEN** |    88    | Auxiliary Motor                      |            |          |                              |
|  **RED**   |    89    | Line Switch                          |            |          |                              |
|  **GREEN** |    90    | Regulating Device                    |            |          |                              |

## Other Device Numbers

|  COLOR     |  ABBRAVATION  |
| :--------: | :-----------: |
|  **BLUE**  |  BL           |
|  **GREEN** |  GN           |
|  **RED**   |  RD           |
|  **WHITE** |  WH           |
|  **YELLOW**|  YW           |
|  **BLACK** |  BK           |
|  **GRAY**  |  GY           |
|  **ORANGE**|  OG           |
|  **PURPLE**|  PR           |
|  **BROWN** |  BN           |
|            |               |


