---
title: EPLAN Device Designation Reference Guide — Comprehensive `-` Tag System for All Disciplines
description: >-
  A complete reference for EPLAN device designations based on IEC 81346, covering every device type across electrical, automation, instrumentation, IT, and mechanical disciplines, with examples and best practices.
author: Mahmoud Lotfi
date: 2024-06-01 10:00:00 +0800
file_name: 2024-06-01-eplan-device-designation-reference-1.md
categories: [EPLAN, Device Designation, IEC 81346, Reference Guide]
tags: [Eplan, device designation, IEC 81346]
pin: False
math: true
mermaid: true
comments: true
toc: true
render_with_liquid: false
image:
  path: /assets/img/posts/eplan.jpg
  alt: EPLAN Device Designation Reference
  lqip: data:image/webp;base64,UklGRjoAAABXRUJQVlA4IC4AAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA

---

# EPLAN P8 — Device Designation (`-`) Reference Guide
> Based on IEC 81346 | IEC 61346 | ISO 10628 | ISA-5.1 | Expert conventions across electrical, automation, instrumentation, IT, and mechanical disciplines

**34 sections** covering every device type across all disciplines:

**Foundation:**
- Full **IEC 81346 primary letter table** (A–Y) with two-letter combinations and typical devices
- **IEC vs ISA vs common practice cross-reference table** — so you know which standard applies when

**Power & Protection:**
- LV breakers (`QF`, `MCB`, `MCCB`, `ACB`, `RCBO`) with descriptive suffixes for every feeder type
- MV switching (`QB`, `QD`, `QS`, `QE`, `FU`) + VCB-specific (`CLOSING_COIL`, `TRIP_COIL1/2`, `ANTI_PUMP_K`, `SPRING_CHARGED`, draw-out interlock switches)
- Protection relays — all types (`F_OC`, `F_EF`, `F_DIFF`, `F_DIST`, `F_REF`, `F_BUCHH`, `F_WTI`, `F_ARC`)
- CTs, VTs, power analysers, energy meters, phase monitors

**Motor Control:**
- Contactors — every type (`KM_MAIN`, `KM_STAR`, `KM_DELTA`, `KM_FWD`, `KM_REV`, `KM_VFD`, `KM_BP`, `KM_NORM`, `KM_ALT`)
- Relays, timers (`KT_SD`, `KT_ON`, `KT_OFF`, `KT_RETRANS`, `KT_FLASH`)
- VFDs, soft starters, braking resistors

**Instrumentation (both worlds):**
- IEC `BT`, `BP`, `BF`, `BL`, `BA` sensor codes
- Full **ISA-5.1 tag system** — first letter table, last letter table, and every common tag (`FT101`, `PT201`, `TT301`, `LT401`, `AT501`) with H/L/HH/LL safety suffix convention

**PLC & Safety:**
- Every PLC module type (`CPU_A/B`, `PM`, `IM`, `DI01`, `DO01`, `AI01`, `RTD01`, `CM_PN`, `CM_PB`, `SYNC_MOD`)
- Safety relays and devices (`F3_ESTOP`, `F3_GUARD`, `F3_LIGHT`, `RFID_SAFE`, `AREA_SCAN`, `LIGHT_CRT`)
- SIS modules (`CPU_S_A/B/C`, `DI_S01`, `DO_S01`)

**Complete worked examples** — DOL starter, star-delta, PLC panel, DCS instrumentation loop, MV feeder panel, SIL2 safety shutdown loop (all six showing full `=FUNCTION+LOCATION-DEVICE` tags)

---

## Table of Contents
1. [Fundamentals](#fundamentals)
2. [IEC 81346 Device Reference Designation — Letter Codes](#iec-81346-device-reference-designation--letter-codes)
3. [Power Devices — Breakers, Isolators, Switches](#power-devices--breakers-isolators-switches)
4. [Protection & Measuring Devices](#protection--measuring-devices)
5. [Contactors, Relays & Timers](#contactors-relays--timers)
6. [Transformers & Power Conversion](#transformers--power-conversion)
7. [Drives, Starters & Motor Control](#drives-starters--motor-control)
8. [Motors, Actuators & Prime Movers](#motors-actuators--prime-movers)
9. [Power Supplies & Energy Storage](#power-supplies--energy-storage)
10. [Terminals, Connectors & Cabling](#terminals-connectors--cabling)
11. [Sensors & Detectors (Digital / Binary)](#sensors--detectors-digital--binary)
12. [Instrumentation — Analog Measurement](#instrumentation--analog-measurement)
13. [Instrumentation — ISA Tag Naming (P&ID)](#instrumentation--isa-tag-naming-pid)
14. [Control & Signal Conditioning Devices](#control--signal-conditioning-devices)
15. [Indication & Signalling Devices](#indication--signalling-devices)
16. [Operator Interface Devices (Buttons, Switches, Selectors)](#operator-interface-devices-buttons-switches-selectors)
17. [PLC & Controller Modules](#plc--controller-modules)
18. [Safety Devices & Safety Relays](#safety-devices--safety-relays)
19. [Communications & Network Devices](#communications--network-devices)
20. [HMI, Computers & IT Hardware](#hmi-computers--it-hardware)
21. [Heating, Cooling & Environmental](#heating-cooling--environmental)
22. [Pneumatic & Hydraulic Devices](#pneumatic--hydraulic-devices)
23. [Mechanical & Structural Components](#mechanical--structural-components)
24. [Cables, Conduits & Routing](#cables-conduits--routing)
25. [Panel Building Hardware](#panel-building-hardware)
26. [MV Switchgear Specific Devices](#mv-switchgear-specific-devices)
27. [Battery & DC System Devices](#battery--dc-system-devices)
28. [Fire, Gas & Safety Detectors](#fire-gas--safety-detectors)
29. [Building Services Devices](#building-services-devices)
30. [Numbering Conventions & Suffixes](#numbering-conventions--suffixes)
31. [Full Tag Examples — Complete Projects](#full-tag-examples--complete-projects)
32. [Cross-Reference: IEC 81346 vs ISA-5.1 vs Common Practice](#cross-reference-iec-81346-vs-isa-51-vs-common-practice)
33. [Common Mistakes](#common-mistakes)
34. [Expert Tips](#expert-tips)

---

## Fundamentals

### The Three Pillars of EPLAN Referencing (IEC 81346)
```
=   Function designation     → WHAT it does
+   Location designation     → WHERE it is
-   Device designation       → WHAT it is (the component itself)
```

### What Device Designation Represents
The `-` designation is the **tag of the actual component** — it uniquely identifies the physical device within its location and function context. It answers:
> *"Which specific component is this?"*

### Full Tag Syntax
```
=FUNCTION+LOCATION-DEVICE

=CTRL+CP1-CPU1             PLC CPU, in panel CP1, control function
=PWR+MCC1.M01-KM1          Contactor KM1, in MCC drawer M01, power function
=INST+FIELD-FT101          Flow transmitter FT101, in field, instrumentation
=SAFE+CP1.SAFE-F3_ESTOP    Safety relay, in safety section of CP1
```

### Numbering Structure
```
[Letter Code] + [Number]          Basic form
[Letter Code] + [Number] + [Suffix]   Extended form

Examples:
-K1            Relay 1
-KM1           Main contactor 1
-KM_STAR       Star contactor (named suffix)
-F1            Protection device 1
-F_OC_A        Overcurrent relay, incomer A (descriptive suffix)
-QF1           Circuit breaker 1 (Q = switching, F = protection)
-PQ1           Power quality analyser 1
-FT101         Flow transmitter tag 101 (ISA style)
```

### When to Use Numbers vs Descriptive Suffixes
```
Numbers alone (recommended for simple panels):
-K1, -K2, -K3          Easy, sequential, no ambiguity

Descriptive suffixes (recommended for complex panels):
-KM_MAIN               Immediately clear this is the main contactor
-KM_STAR               Star contactor in star-delta
-KM_DELTA              Delta contactor in star-delta
-K_WD                  Watchdog relay
-F_OC                  Overcurrent protection

ISA instrument tags (process / P&ID projects):
-FT101                 Flow transmitter loop 101
-PT302                 Pressure transmitter loop 302
-TIC401                Temperature indicating controller loop 401
```

---

## IEC 81346 Device Reference Designation — Letter Codes

> The first letter(s) define the device type. IEC 81346 uses a two-level system.

### Primary Letter — Device Kind
| Letter | Device Kind | Typical Devices |
|--------|------------|----------------|
| `B` | Converts physical variable → signal | Sensors, transducers, encoders, detectors |
| `C` | Stores energy or material | Capacitors, batteries, tanks, accumulators |
| `D` | Processes / stores information | PLCs, computers, HMIs, recorders, displays |
| `E` | Provides radiation or thermal energy | Heaters, lamps, UV emitters |
| `F` | Protects against dangerous conditions | Fuses, breakers, protection relays, safety devices |
| `G` | Generates / supplies electrical energy | Power supplies, batteries, generators, UPS |
| `H` | Signals / indicates state or condition | Lamps, buzzers, horns, displays, annunciators |
| `K` | Processes signals / controls / switches | Relays, timers, contactors, PLC outputs |
| `M` | Provides mechanical energy | Motors, actuators, cylinders, pumps (motor part) |
| `N` | Regulates / controls process variable | VFDs, PID controllers, regulators |
| `P` | Measures / tests | Meters, analysers, instruments, gauges |
| `Q` | Switches / varies electrical energy | Isolators, circuit breakers, disconnectors |
| `R` | Restricts / stabilises energy or flow | Resistors, reactors, chokes, dampers |
| `S` | Converts manual operation → signal | Push buttons, switches, selectors, keyboards |
| `T` | Converts electrical quantities | Transformers, CT, VT, rectifiers, inverters |
| `U` | Keeps objects in a defined position | Clamps, brakes, locks, holders |
| `V` | Processes materials or products | Conveyors, mixers, reactors, valves (flow) |
| `W` | Conducts / transmits / distributes | Cables, busbars, waveguides, antenna |
| `X` | Connects / terminates | Terminal blocks, connectors, plugs, junction |
| `Y` | Positions / guides | Positioners, guides, stepper actuators |

### Common Two-Letter Combinations Used in Practice
| Code | Meaning | Example Device |
|------|---------|----------------|
| `BK` | Encoder / speed sensor | Rotary encoder |
| `BP` | Pressure sensor | Pressure switch |
| `BT` | Temperature sensor | Thermocouple, PT100 |
| `BL` | Level sensor | Float switch, level switch |
| `BF` | Flow sensor | Flow switch |
| `BA` | Analyser sensor | Gas analyser input |
| `BG` | Position / limit switch | Proximity sensor, limit switch |
| `CM` | Motor capacitor | Run / start capacitor |
| `DD` | Data / logic processor | PLC, computer |
| `EH` | Heating element | Trace heating, panel heater |
| `EL` | Lighting element | Lamp, LED strip |
| `FA` | Fuse (general) | Cartridge fuse |
| `FB` | Overcurrent protective device | MCCB, MCB |
| `FC` | Combined protective device | RCBO, motor circuit breaker |
| `FD` | Residual current device | RCD, RCCB |
| `FU` | HV fuse | HRC fuse, expulsion fuse |
| `GA` | Battery | Lead-acid, Li-ion battery |
| `GB` | Battery charger | Float charger, SMPS charger |
| `GS` | Power supply (AC/DC) | SMPS, linear PSU |
| `GU` | UPS | UPS system |
| `HA` | Acoustic alarm | Buzzer, horn, siren |
| `HL` | Indicator lamp | Pilot lamp, LED indicator |
| `HR` | Digital display / readout | Digital panel meter |
| `KA` | Auxiliary relay | General purpose relay |
| `KC` | Contactor | Motor contactor |
| `KM` | Main contactor | Main power contactor |
| `KT` | Timer relay | On-delay, off-delay, star-delta timer |
| `KW` | Watchdog relay | PLC watchdog output |
| `MA` | Motor (asynchronous) | AC induction motor |
| `MB` | Brake (motor) | Electro-mechanical brake |
| `MC` | Motor (DC) | DC motor |
| `MS` | Servo motor | Servo / stepper motor |
| `MT` | Motor (special) | Torque motor, linear motor |
| `NA` | VFD / frequency converter | Variable frequency drive |
| `NC` | PID controller | Process controller |
| `NR` | Regulator | Voltage regulator, pressure regulator |
| `PA` | Ammeter | Current meter |
| `PB` | Power analyser | Power quality analyser |
| `PC` | Counter | Event counter, hour meter |
| `PF` | Frequency meter | Hz meter |
| `PH` | Phase sequence relay | Phase monitor relay |
| `PJ` | Energy meter | kWh meter |
| `PQ` | Power quality analyser | PQ meter with harmonics |
| `PV` | Voltmeter | Voltage panel meter |
| `PW` | Power meter | kW meter |
| `QA` | Switch / disconnector | Load break switch, isolator |
| `QB` | Circuit breaker (HV) | Vacuum/SF6 circuit breaker |
| `QD` | Disconnector / isolator (HV) | Air-break disconnector |
| `QE` | Earthing switch | Earth switch (MV/HV) |
| `QF` | Circuit breaker (LV) | MCCB, MCB, ACB |
| `QM` | Motor circuit breaker | Combined contactor + breaker |
| `QS` | Load break switch | LBS, on-load switch |
| `RA` | Resistor | Fixed resistor |
| `RB` | Braking resistor | Dynamic brake resistor |
| `RL` | Inductor / reactor | Line reactor, choke |
| `RR` | Variable resistor | Rheostat, potentiometer |
| `SA` | Selector switch | Multi-position rotary switch |
| `SB` | Push button | Momentary push button |
| `SK` | Key switch | Key-operated switch |
| `SL` | Limit switch (manual) | Mechanical limit switch |
| `SS` | Selector switch (maintained) | Mode selector, local/remote |
| `TA` | Current transformer | Metering / protection CT |
| `TC` | Thyristor / SCR | Power thyristor, soft starter |
| `TF` | Filter transformer | Isolation transformer |
| `TM` | Power transformer | Distribution transformer |
| `TV` | Voltage transformer | Metering / protection VT/PT |
| `TY` | Rectifier / converter | AC/DC converter |
| `VA` | Valve (process) | Control valve, on/off valve |
| `VF` | Fan | Cooling fan, ventilation fan |
| `VP` | Pump | Process pump |
| `XB` | Busbar | Busbar connection point |
| `XD` | Distribution terminal | DIN rail terminal block |
| `XP` | Plug / socket | Connector plug |
| `XS` | Socket | Socket outlet |
| `XT` | Terminal block | Screw/spring terminal |
| `YA` | Solenoid actuator | Solenoid coil, solenoid valve |
| `YB` | Brake | Electromechanical brake |
| `YV` | Solenoid valve | Pneumatic / hydraulic solenoid valve |
| `ZA` | Zener barrier | Intrinsic safety barrier |
| `ZI` | Galvanic isolator | HART isolator, signal isolator |
| `ZF` | EMC filter | Line filter, EMC filter |

---

## Power Devices — Breakers, Isolators, Switches

### LV Circuit Breakers & Isolators
```
-QF_MAIN           Main incomer air circuit breaker (ACB) — mains level
-QF_INC            Incomer MCCB (moulded case circuit breaker)
-QF1 .. -QFn       Numbered outgoing circuit breakers / MCBs
-QF_MCC1           Feeder breaker to MCC1
-QF_DB1            Feeder breaker to DB1
-QF_UPS            Feeder breaker to UPS
-QF_PLC            MCB for PLC power
-QF_HMI            MCB for HMI power
-QF_FIELD          MCB for field device power
-QF_SAFE           MCB for safety system power
-QF_HEAT           MCB for panel heater
-QF_LIGHT          MCB for panel lighting
-QF_24V            MCB for 24VDC supply
-QS1 .. -QSn       Load break switch / isolator (maintained open/close)
-QS_LOCAL          Local isolator switch
-QS_MBP            Maintenance bypass switch (UPS)
-QR1               Residual current circuit breaker (RCCB)
-RCBO1             RCBO (RCD + MCB combined)
-MCB_L1            MCB for lighting circuit 1
-MCB_P1            MCB for power circuit 1
-MCB_H1            MCB for HVAC circuit 1
-MCB_E1            MCB for emergency circuit
```

### HV / MV Switching Devices
```
-QB1 .. -QBn       Vacuum / SF6 circuit breaker (HV/MV)
-QB_INC            Incomer VCB
-QB_TIE            Bus tie / bus section VCB
-QB_FDR1           Feeder VCB 1
-QB_TX1            Transformer feeder VCB
-QB_MTR1           MV motor feeder VCB
-QD1 .. -QDn       Disconnector / isolator (air-break, HV)
-QD_LINE           Line side disconnector
-QD_BUS            Bus side disconnector
-QS1 .. -QSn       Load break switch (MV — ring main, RMU)
-QS_RING_IN        Ring incomer LBS
-QS_RING_OUT       Ring outgoing LBS
-QS_TX             TX feeder LBS
-QE1 .. -QEn       Earthing switch (MV/HV)
-ES1 .. -ESn       Earthing switch (alternative common naming)
-ES_LINE           Line earth switch
-ES_BUS            Busbar earth switch
-FU1 .. -FUn       HRC fuse (MV transformer feeder)
```

### Manual Isolation & Changeover
```
-QS_MAINS          Mains isolation switch
-QS_GEN            Generator isolation switch
-QS_ATS            ATS changeover switch (manual)
-QS_NORM           Normal supply isolator
-QS_ALT            Alternative supply isolator
-COS1              Changeover switch (manual 2-position)
-MTS1              Manual transfer switch
-ISOL1             Panel isolation switch (lockable)
```

---

## Protection & Measuring Devices

### Protection Relays
```
-F1 .. -Fn         General protection device (numbered)
-F_OC              Overcurrent protection relay
-F_EF              Earth fault protection relay
-F_DIFF            Differential protection relay
-F_DIST            Distance protection relay
-F_REF             Restricted earth fault relay
-F_BUCHH           Buchholz relay (oil transformer)
-F_WTI             Winding temperature indicator / relay
-F_OTI             Oil temperature indicator / relay
-F_PRD             Pressure relief device / relay
-F_OSL             Oil surge relay / gas relay
-F_UV              Undervoltage relay
-F_OV              Overvoltage relay
-F_PHASE           Phase sequence / phase loss relay
-F_MOTOR           Motor protection relay (multifunction)
-F_THERM           Thermal overload relay (standalone)
-F_SAFE            Safety relay (non-SIL general purpose)
-F_BUSBAR          Busbar protection relay
-F_ARC             Arc flash detection relay
-F_FREQ            Under/over frequency relay
```

### Measurement & Metering
```
-CT1 .. -CTn       Current transformer (protection / metering)
-CT_INC            Incomer CT
-CT_FDR1           Feeder CT 1
-VT1 .. -VTn       Voltage transformer / potential transformer
-VT_BUS            Busbar VT
-VT_METER          Metering VT
-PA1               Ammeter (panel-mount)
-PV1               Voltmeter (panel-mount)
-PW1               Wattmeter / power meter
-PF1               Power factor meter
-PQ1 .. -PQn       Power quality analyser (full PQ with harmonics)
-PQ_MAIN           Main incomer power quality analyser
-PQ_FDR1           Feeder 1 power quality analyser
-KWH1 .. -KWHn     Energy meter / kWh meter
-KWH_MAIN          Main energy meter
-KWH_LIGHT         Lighting sub-meter
-KWH_POWER         Power sub-meter
-FREQ1             Frequency meter
-PH1               Phase sequence indicator
-PC1               Hour meter / event counter
-PLC_METR1         Power line carrier meter
-THD1              Total harmonic distortion analyser
```

---

## Contactors, Relays & Timers

### Contactors
```
-KM1 .. -KMn       Main contactor (general numbered)
-KM_MAIN           Main power contactor (DOL starter)
-KM_STAR           Star contactor (star-delta starter)
-KM_DELTA          Delta contactor (star-delta starter)
-KM_FWD            Forward contactor (reversing starter)
-KM_REV            Reverse contactor (reversing starter)
-KM_VFD            VFD output contactor
-KM_BP             Bypass contactor (VFD bypass)
-KM_RUN            Run bypass contactor (soft starter inline type)
-KM_NORM           Normal supply contactor (ATS)
-KM_ALT            Alternative supply contactor (ATS)
-KM_COOL           Cooling fan contactor (transformer)
-KM_AUX            Auxiliary contactor (signal/interlock duty)
```

### Auxiliary & Interposing Relays
```
-K1 .. -Kn         General relay (numbered)
-KA1 .. -KAn       Auxiliary relay (IEC 81346 style)
-K_START           Start permissive relay
-K_STOP            Stop command relay
-K_RUN             Running confirm relay
-K_TRIP            Trip / fault relay
-K_FAULT           General fault relay
-K_ALARM           General alarm relay
-K_READY           Ready / healthy relay
-K_REMOTE          Remote command relay
-K_LOCAL           Local command relay
-K_ATS             ATS changeover relay
-K_INC_A           Incomer A auxiliary relay
-K_TIE             Bus tie interlock relay
-K_WD              Watchdog relay (PLC healthy)
-K_INTERLOCK       Interlock relay (general)
-K_PERMISSIVE      Permissive relay
-K_INHIBIT         Inhibit relay
-K_LATCH           Latching relay
-KP1               Pulse relay
-KR1               Reed relay
-KM_AUX1           Auxiliary contact block (add-on)
```

### Timers
```
-KT1 .. -KTn       Timer relay (general numbered)
-KT_SD             Star-delta changeover timer
-KT_ON             On-delay timer
-KT_OFF            Off-delay timer
-KT_RETRANS        Retransfer delay timer (ATS)
-KT_TRANS          Transfer delay timer (ATS)
-KT_START          Start delay timer
-KT_RESTART        Auto-restart delay timer
-KT_FLASH          Flasher / pulse timer
-KT_WD             Watchdog timer
```

---

## Transformers & Power Conversion

### Power Transformers
```
-TM1 .. -TMn       Power transformer (general)
-TM_MAIN           Main power transformer
-TX1 .. -TXn       Transformer (alternative common tag)
-T1 .. -Tn         Transformer (simple projects)
-T_CTRL            Control transformer (230V to 24VAC)
-T_ISO             Isolation transformer
-T_AUTO            Autotransformer
-TF1               Filter / EMC transformer
```

### Instrument Transformers
```
-CT1 .. -CTn       Current transformer
-VT1 .. -VTn       Voltage transformer (potential transformer)
-TA1               Current transformer (IEC 81346 two-letter)
-TV1               Voltage transformer (IEC 81346 two-letter)
```

### Power Conversion
```
-TY1               Rectifier / AC-DC converter
-INV1              Inverter (DC-AC)
-CONV1             Converter (general)
-TC1               Thyristor controller / soft starter power stack
-CHRG1             Battery charger
-GB1               Battery charger (IEC 81346 style)
```

### Reactors & Filters
```
-RL1 .. -RLn       Line reactor / choke (VFD, harmonic)
-L1                Inductor (simple notation)
-EMC1 .. -EMCn     EMC line filter
-ZF1               EMC filter (IEC 81346 style)
-THF1              Tuned harmonic filter
-HF1               High-frequency filter
-C1 .. -Cn         Capacitor (power factor / filter)
-CM1               Motor run capacitor
```

---

## Drives, Starters & Motor Control

### Variable Frequency Drives (VFDs)
```
-VFD1 .. -VFDn     VFD unit (general numbered)
-VFD_X             VFD for X-axis
-VFD_Y             VFD for Y-axis
-VFD_Z             VFD for Z-axis
-VFD_SP            VFD for spindle
-VFD_P1            VFD for pump 1
-VFD_FAN1          VFD for fan 1
-NA1 .. -NAn       VFD / frequency converter (IEC 81346 two-letter)
-INV_MAIN          Main drive inverter
```

### Soft Starters
```
-SS1 .. -SSn       Soft starter unit (general numbered)
-SS_P1             Soft starter for pump 1
-TC1 .. -TCn       Thyristor controller / soft starter (IEC 81346)
```

### Motor Protection & Starter Components
```
-F_THERM1          Thermal overload relay
-F_MOTOR1          Motor protection relay (multifunction — Siemens 3RU, ABB EF, Sprecher)
-QM1               Motor circuit breaker (combined QF + thermal protection)
-KM_MAIN           Main contactor
-KM_AUX            Auxiliary contact block
-PTC1              PTC thermistor trip relay (winding temperature)
-NTC1              NTC temperature monitoring relay
```

### Braking
```
-RB1 .. -RBn       Braking resistor (dynamic brake for VFD)
-BR1               Brake resistor (alternative notation)
-YB1               Electromechanical brake (motor-mounted)
-MB1               Brake (IEC 81346 two-letter)
-BC1               Brake controller / rectifier
```

---

## Motors, Actuators & Prime Movers

### Motors
```
-M1 .. -Mn         Motor (general numbered — most common)
-MA1 .. -MAn       AC induction motor (IEC 81346 two-letter)
-MC1               DC motor
-MS1               Servo motor
-MT1               Torque motor / special motor
-P1 .. -Pn         Pump motor (process / P&ID convention — see ISA section)
-FAN1 .. -FANn     Fan motor (common in HVAC)
-COMP1             Compressor motor
-CONV1             Conveyor drive motor
-SP1               Spindle motor
-AG1               Agitator motor
-MIX1              Mixer motor
-BLW1              Blower motor
-PUMP1             Pump motor (descriptive)
-HYD_MTR1          Hydraulic power unit motor
-EXT1              Extruder motor
```

### Actuators & Valves
```
-YA1 .. -YAn       Solenoid actuator / solenoid valve coil
-YV1 .. -YVn       Solenoid valve (pneumatic / hydraulic)
-YV_FWD            Forward solenoid valve
-YV_REV            Reverse solenoid valve
-YV_CLAMP          Clamp solenoid valve
-YV_UNCLAMP        Unclamp solenoid valve
-VA1               Control valve (process — motorised)
-VA_CTRL1          Control valve positioner
-MOV1              Motor-operated valve
-AOV1              Air-operated valve / pneumatic valve
-HOV1              Hand-operated valve (if monitored)
-POS1              Valve positioner
-ACT1              Linear actuator (electric)
-ACT_SERVO1        Servo actuator
-CYL1 .. -CYLn     Hydraulic / pneumatic cylinder
-GRAB1             Gripper actuator
```

### Mechanical Drives
```
-GB1               Gearbox (monitored — speed feedback)
-CLUTCH1           Clutch (electric)
-BRAKE1            Mechanical brake (release coil)
-COUPLING1         Flexible coupling (if instrumented)
```

---

## Power Supplies & Energy Storage

### Power Supplies
```
-PS1 .. -PSn       Power supply unit (general numbered)
-PS_A              Power supply A (redundant pair)
-PS_B              Power supply B (redundant pair)
-GS1               SMPS / switch-mode power supply (IEC 81346)
-SMPS1             Switch-mode power supply
-PSU1              Power supply unit
-PS_PLC            PLC power supply (system power module)
-PS_IO             I/O power supply
-PS_LOOP1          Loop power supply (4-20mA instrument loops)
-PS_SAFE           Safety system power supply (isolated)
-PM1               Power module (PLC-integrated, e.g. Siemens PM)
```

### UPS & Buffering
```
-UPS1 .. -UPSn     UPS unit
-GU1               UPS (IEC 81346 two-letter)
-UPS_BUF1          24VDC UPS buffer module (DIN rail, e.g. SITOP UPS1600)
-BATT_BUF1         Battery buffer module
-BATT_MGT1         Battery management module
```

### Batteries & Capacitors
```
-GA1 .. -GAn       Battery / battery bank
-BATT1             Battery (common industrial notation)
-C1 .. -Cn         Capacitor (power / filter)
-CAP1              Supercapacitor module
-CB1               Capacitor bank (PFC step)
```

---

## Terminals, Connectors & Cabling

### Terminal Blocks
```
-X1 .. -Xn         Terminal block / terminal strip (general — most common)
-XT1               Terminal block (IEC 81346 two-letter)
-X_DI1             Digital input terminal group
-X_DO1             Digital output terminal group
-X_AI1             Analog input terminal group
-X_AO1             Analog output terminal group
-X_RTD1            RTD input terminal group
-X_SAFE1           Safety circuit terminal group
-X_PWR1            Power terminal group
-X_COMM1           Communications terminal group
-X_EARTH           Earth / PE terminal bar
-X_SCREEN          Cable screen / shield terminal
-XD1               DIN rail terminal (IEC 81346)
-PE1               Protective earth terminal bar
-N1                Neutral terminal bar
```

### Connectors & Plugs
```
-XP1 .. -XPn       Plug / male connector
-XS1 .. -XSn       Socket / female connector
-XP_PWR            Power connector plug
-XP_COMM           Communications connector (M12, RJ45 on device)
-XP_HMI            HMI connection plug
-XP_USB            USB connector
-XP_SD             SD card / memory card
-XB1               Busbar connector (IEC 81346)
-JB1               Junction block (multi-pin)
-MC1               Multi-pin connector (general)
```

### Cable & Wiring References
```
-W1 .. -Wn         Cable / wire (IEC 81346 — W = conducting)
-WC1               Control cable
-WP1               Power cable
-WS1               Signal cable
-WF1               Fibre optic cable
-WN1               Network cable (Cat6, etc.)
-CAB1              Cable (common industrial notation)
-PIGTAIL1          Fibre pigtail
-JUMPER1           Jumper wire / patch lead
-LOOM1             Wire loom / harness
```

---

## Sensors & Detectors (Digital / Binary)

### Position & Presence
```
-B1 .. -Bn         Sensor / detector (general — most common simple notation)
-BG1 .. -BGn       Position / limit sensor (IEC 81346)
-SL1 .. -SLn       Mechanical limit switch
-SQ1 .. -SQn       Proximity / position switch (common European notation)
-BQ1               Proximity switch (IEC 81346)
-PROX1             Inductive proximity sensor
-PROX_EXT1         Extended range proximity sensor
-CAP1              Capacitive proximity sensor
-ULTRA1            Ultrasonic proximity sensor
-PHOTO1            Photoelectric sensor
-REFLX1            Retro-reflective photosensor
-THR_BEAM1         Through-beam sensor
-LASER1            Laser distance / presence sensor
-COLOUR1           Colour sensor
-RFID1             RFID reader
-LS1               Level switch (discrete — float or electrode)
-FS1               Flow switch (discrete — paddle or thermal)
-PS_SW1            Pressure switch (discrete)
-TS_SW1            Temperature switch (discrete — bimetal or capillary)
-VS1               Vibration switch
-TILT1             Tilt switch
-SLIP1             Slip detection sensor
-ROPE_SW1          Rope / cable pull switch (conveyor safety)
-SKIRT1            Skirt monitoring switch
-BELT_ALIGN1       Belt alignment switch
-ZERO_SPD1         Zero speed switch
-OVERSPD1          Overspeed switch / detector
```

### Door, Guard & Safety Sensing
```
-SL_DOOR1          Door limit switch
-SL_GUARD1         Guard door limit switch
-SL_HATCH1         Hatch / access panel switch
-MAG_SW1           Magnetic door switch
-RFID_GUARD1       RFID guard lock / interlock
-TPSW1             Trapped key switch
-HANDLE1           Handle switch
```

### Rotational & Motion
```
-BK1 .. -BKn       Encoder (IEC 81346)
-ENC1              Rotary encoder (absolute or incremental)
-ENC_ABS1          Absolute encoder
-ENC_INC1          Incremental encoder
-RESOLVER1         Resolver feedback
-TACHO1            Tachometer (analogue speed feedback)
-SPEED1            Speed sensor (magnetic pickup)
```

---

## Instrumentation — Analog Measurement

### Temperature
```
-BT1 .. -BTn       Temperature sensor (IEC 81346)
-TT1 .. -TTn       Temperature transmitter (ISA style — 4-20mA output)
-TE1 .. -TEn       Temperature element (thermocouple or RTD — ISA)
-RTD1              RTD sensor (PT100/PT1000 — direct)
-TC_THERMO1        Thermocouple element (K, J, T type)
-TW1               Thermowell (protective pocket for TE)
-TSTAT1            Thermostat (discrete control — see also SB / SS)
-WT1               Winding temperature sensor (transformer)
-OT1               Oil temperature sensor (transformer)
```

### Pressure
```
-BP1 .. -BPn       Pressure sensor (IEC 81346)
-PT1 .. -PTn       Pressure transmitter (ISA style)
-PE1 .. -PEn       Pressure element (ISA)
-PDT1              Pressure differential transmitter
-PG1               Pressure gauge (local — no signal output)
-PSV1              Pressure safety valve (relief — not a sensor but appears on I/O)
```

### Flow
```
-BF1 .. -BFn       Flow sensor (IEC 81346)
-FT1 .. -FTn       Flow transmitter (ISA style)
-FE1 .. -FEn       Flow element (orifice plate, venturi — ISA)
-FIT1              Flow indicating transmitter
-FC1               Flow controller
-FM1               Flow meter (volumetric, Coriolis, magnetic)
-MAG1              Magnetic flow meter
-CORI1             Coriolis flow meter
-ULTRA_F1          Ultrasonic flow meter
-VORTEX1           Vortex flow meter
-ROTA1             Rotameter / variable area flow meter
```

### Level
```
-BL1 .. -BLn       Level sensor (IEC 81346)
-LT1 .. -LTn       Level transmitter (ISA style — continuous)
-LE1 .. -LEn       Level element (ISA)
-LIT1              Level indicating transmitter
-LG1               Level gauge / sight glass (local)
-RADAR1            Radar level transmitter (guided wave or free space)
-ULTRA_L1          Ultrasonic level transmitter
-BUBBLER1          Bubbler level system
-DISPL1            Displacer level transmitter
-FLOAT1            Float-type level sensor
-HYDRO1            Hydrostatic level transmitter
-LOAD_CELL1        Load cell (for level by weight)
```

### Analytical
```
-BA1 .. -BAn       Analyser sensor (IEC 81346)
-AT1 .. -ATn       Analytical transmitter (ISA style)
-AE1 .. -AEn       Analytical element (ISA)
-PH_METER1         pH analyser / transmitter
-COND1             Conductivity analyser
-DO2_1             Dissolved oxygen analyser
-TURB1             Turbidity analyser
-CL2_1             Chlorine residual analyser
-TOC1              Total organic carbon analyser
-GAS_IR1           Infrared gas analyser (CO2, CH4, etc.)
-GAS_CATA1         Catalytic gas detector (%LEL)
-GAS_EC1           Electrochemical gas detector (H2S, CO, O2, etc.)
-GAS_OP1           Open-path gas detector (IR beam)
-FLUE1             Flue gas analyser
-MOISTURE1         Moisture / humidity transmitter
-VISCOSITY1        Viscosity analyser
```

### Position & Displacement (Analog)
```
-LVDT1             LVDT position transducer
-POT1              Potentiometer (position feedback)
-LINEAR_ENC1       Linear encoder
-DRAW_WIRE1        Draw-wire / cable extension transducer
```

### Force, Torque & Vibration
```
-LOAD_CELL1        Load cell (force / weight)
-TORQUE1           Torque transducer
-STRAIN1           Strain gauge transmitter
-VIB_TX1           Vibration transmitter (4-20mA, proximity probe)
-ACCEL1            Accelerometer (vibration / shock)
-BEARING_TX1       Bearing temperature / vibration transmitter
```

---

## Instrumentation — ISA Tag Naming (P&ID)

> ISA-5.1 standard. First letter(s) = measured variable, last letter(s) = function/device type.

### First Letter — Measured Variable
| Letter | Variable |
|--------|---------|
| A | Analysis (composition) |
| C | Conductivity |
| D | Density |
| F | Flow |
| H | Hand (manual) |
| I | Current (electrical) |
| J | Power |
| K | Time |
| L | Level |
| M | Moisture / humidity |
| P | Pressure |
| Q | Quantity / event |
| R | Radiation |
| S | Speed / frequency |
| T | Temperature |
| U | Multivariable |
| V | Vibration / viscosity |
| W | Weight / force |
| X | Unclassified |
| Y | Event / state (relay) |
| Z | Position / dimension |

### Last Letter(s) — Function / Device Type
| Letter(s) | Function |
|-----------|---------|
| `E` | Primary element (sensing element, no output) |
| `T` | Transmitter (4-20mA / HART / FF output) |
| `I` | Indicator (local display only) |
| `C` | Controller |
| `R` | Recorder |
| `S` | Switch (discrete output) |
| `V` | Control valve (final control element) |
| `IT` | Indicating transmitter |
| `IC` | Indicating controller |
| `IR` | Indicating recorder |
| `ICV` | Indicating control valve (with positioner) |

### Common ISA Tags Used as Device Designations
```
--- Flow ---
-FE101             Flow element (orifice plate) loop 101
-FT101             Flow transmitter loop 101
-FIT101            Flow indicating transmitter
-FS101             Flow switch (discrete)
-FC101             Flow controller
-FCV101            Flow control valve
-FM101             Flow meter (totalisers)

--- Pressure ---
-PE201             Pressure element loop 201
-PT201             Pressure transmitter
-PIT201            Pressure indicating transmitter
-PS201             Pressure switch (discrete)
-PC201             Pressure controller
-PCV201            Pressure control valve
-PSV201            Pressure safety valve
-PDT201            Differential pressure transmitter

--- Temperature ---
-TE301             Temperature element (thermocouple/RTD)
-TT301             Temperature transmitter
-TIT301            Temperature indicating transmitter
-TS301             Temperature switch (discrete)
-TC301             Temperature controller
-TW301             Thermowell

--- Level ---
-LE401             Level element
-LT401             Level transmitter
-LIT401            Level indicating transmitter
-LS401             Level switch (discrete — high or low)
-LSH401            Level switch high
-LSL401            Level switch low
-LSHH401           Level switch high-high (SIL — safety trip)
-LSLL401           Level switch low-low (SIL — safety trip)
-LG401             Level gauge (local — no signal)
-LC401             Level controller
-LCV401            Level control valve

--- Analytical ---
-AE501             Analytical element
-AT501             Analytical transmitter
-AIT501            Analytical indicating transmitter
-AS501             Analytical switch

--- Vibration ---
-VT601             Vibration transmitter
-VS601             Vibration switch
-VIT601            Vibration indicating transmitter

--- Speed ---
-ST701             Speed transmitter
-SS701             Speed switch (discrete — zero speed / overspeed)
-SE701             Speed element (magnetic pickup)

--- Position / Valve Status ---
-ZT801             Position transmitter (valve)
-ZS801             Position switch (limit switch — valve open/closed)
-ZSO801            Position switch — open
-ZSC801            Position switch — closed

--- Multifunction transmitters ---
-UT901             Multivariable transmitter
-TDT1001           Temperature differential transmitter
```

---

## Control & Signal Conditioning Devices

### Isolators & Signal Conditioners
```
-Z1 .. -Zn         Zener barrier / isolator (general)
-ZA1 .. -ZAn       Zener barrier (intrinsic safety — IEC 81346)
-ZI1 .. -ZIn       Galvanic isolator (IEC 81346)
-ISO1              Galvanic isolator (common notation)
-HART_ISO1         HART-transparent galvanic isolator
-SC1               Signal conditioner (4-20mA repeater / splitter)
-SC_SPLIT1         Signal splitter (1 in → 2 out)
-SC_CONV1          Signal converter (0-10V → 4-20mA, etc.)
-SC_LIMIT1         Signal limiter / trip amplifier
-SC_ALARM1         Alarm trip amplifier
-MTL1              MTL Zener barrier (by brand — common usage)
-P&F1              Pepperl+Fuchs isolator (by brand — common usage)
```

### Loop & Power Conditioning
```
-PS_LOOP1          Loop power supply (for 4-20mA sensors)
-SPLITTER1         Power / signal splitter
-REPEATER1         Signal repeater (RS485, etc.)
-CONVERTER1        Protocol converter
-MODEM1            Modem (RS232/485 to TCP/IP, etc.)
```

---

## Indication & Signalling Devices

### Indicator Lamps
```
-HL1 .. -HLn       Indicator lamp / pilot light (general — most common)
-HL_POWER          Power on / system healthy (green)
-HL_RUN            Running / active (green)
-HL_STOP           Stopped / off (white or blue)
-HL_FAULT          Fault / alarm (red)
-HL_WARN           Warning (amber / yellow)
-HL_READY          Ready (green or white)
-HL_TRIP           Trip / protection operated (red)
-HL_CLOSED         Breaker/contactor closed (red — IEC convention)
-HL_OPEN           Breaker/contactor open (green — IEC convention)
-HL_REMOTE         Remote mode active (blue or white)
-HL_LOCAL          Local mode active (amber)
-HL_AUTO           Auto mode active (green)
-HL_MANUAL         Manual mode active (amber)
-HL_ESTOP          E-stop active (red)
-HL_SAFE           Safe / guard active (amber)
-HL_COMM           Communications fault (red)
-HL_BATT           Battery / UPS on battery (amber)
-HL_NORM           Normal supply (green)
-HL_ALT            Alternative supply (amber)
-HL_STAR           Star mode (star-delta — amber)
-HL_DELTA          Delta mode (star-delta — green)
```

### Audible & Visual Alarms
```
-HA1 .. -HAn       Audible alarm — buzzer / horn (IEC 81346)
-HORN1             Alarm horn / siren
-BUZZ1             Buzzer
-SIREN1            Siren (multi-tone)
-BELL1             Bell
-BEAC1             Beacon / revolving light
-STACK_LIGHT1      Stack light / signal tower (combined)
-HL_STACK_G        Stack light — green section
-HL_STACK_A        Stack light — amber section
-HL_STACK_R        Stack light — red section
-HL_STACK_B        Stack light — blue section
-ANNUNC1           Annunciator panel / window annunciator
-DISPLAY1          Digital display / alphanumeric readout
-HR1               Panel meter / digital readout (IEC 81346)
```

---

## Operator Interface Devices (Buttons, Switches, Selectors)

### Push Buttons
```
-SB1 .. -SBn       Push button (general — most common)
-SB_START          Start push button (green)
-SB_STOP           Stop push button (red)
-SB_RESET          Fault reset push button (blue or black)
-SB_ACK            Alarm acknowledge push button
-SB_JOG            Jog / inch push button (black)
-SB_FWD            Forward push button
-SB_REV            Reverse push button
-SB_UP             Up push button
-SB_DOWN           Down push button
-SB_OPEN           Open push button (valve / door)
-SB_CLOSE          Close push button (valve / door)
-SB_TEST           Test push button (lamp test)
-SB_LAMP_TEST      Lamp test push button
-SB_ESTOP          Emergency stop (mushroom head, latching red)
-SB_SAFE_RESET     Safety reset push button
-SB_ENABLE         Enable / enable-for-jog push button
```

### Selector & Maintained Switches
```
-SS1 .. -SSn       Selector switch (general maintained — most common)
-SS_LOCAL          Local / Remote / Off selector
-SS_MODE           Mode selector (Auto / Manual / Maintenance)
-SS_SPEED          Speed selector (Low / Medium / High)
-SA1               Rotary selector switch (IEC 81346)
-SS_3POS           3-position selector (Left / Off / Right)
-SS_HAND_OFF_AUTO  Hand / Off / Auto selector (HOA — common in process)
-SS_VFD_BP         VFD / Bypass selector
-SS_DIR            Direction selector (Forward / Off / Reverse)
```

### Key Switches
```
-SK1 .. -SKn       Key switch (general)
-SK_MAINT          Maintenance mode key switch
-SK_BYPASS         Safety bypass key switch
-SK_ENABLE         Enable key switch
-SK_MASTER_RESET   Master reset key switch
-TPKS1             Trapped key switch (safety interlock system)
```

### Potentiometers & Analogue Operator Devices
```
-RR1               Potentiometer / rheostat (speed setpoint)
-SPEED_POT1        Speed reference potentiometer
-SETPOINT1         Analogue setpoint adjuster
```

### Joysticks & Human Input
```
-JOYSTICK1         Joystick (multi-axis)
-THUMBWHEEL1       Thumbwheel switch (BCD input)
-FOOT_SW1          Foot switch / foot pedal
```

---

## PLC & Controller Modules

### CPU & System Modules
```
-CPU1 .. -CPUn     PLC CPU module
-CPU_A             CPU A (primary — redundant system)
-CPU_B             CPU B (standby — redundant system)
-PM1               Power module (PLC-integrated supply)
-IM1               Interface module (rack-to-rack expansion)
-IM_SEND1          IM send module (left rack)
-IM_RECV1          IM receive module (right/remote rack)
-SYNC_MOD          Synchronisation module (redundant CPU)
-RACK1             Rack / backplane (if tagged separately)
-BM1               Backplane module
```

### I/O Modules
```
-DI01 .. -DIn      Digital input module (numbered)
-DO01 .. -DOn      Digital output module
-AI01 .. -AIn      Analog input module (4-20mA / 0-10V)
-AO01 .. -AOn      Analog output module
-RTD01             RTD / thermocouple input module
-CNT01             Counter / high-speed input module
-ENC01             Encoder interface module
-IO_LINK01         IO-Link master module
-PWM01             PWM output module
-DI_SAFE01         Safety digital input module
-DO_SAFE01         Safety digital output module
-AI_SAFE01         Safety analog input module
-HART_MUX1         HART multiplexer module
-FF_H1_01          Foundation Fieldbus H1 card
-DP_SLAVE1         PROFIBUS DP slave module (IM for ET200)
```

### Communications Modules
```
-CM_PN1            PROFINET communications module
-CM_PB1            PROFIBUS DP master module
-CM_DP1            PROFIBUS DP (alternative)
-CM_485_1          RS485 / Modbus RTU module
-CM_232_1          RS232 serial module
-CM_ETH1           Ethernet module (TCP/IP)
-CM_IEC104_1       IEC 60870-5-104 comms module
-CM_DNP3_1         DNP3 comms module
-CM_MQTT1          MQTT / IoT gateway module
-CM_IOLINK1        IO-Link master communications
-CM_ASI1           AS-Interface master
-CM_CAN1           CANopen master module
-CM_MODBUS1        Modbus TCP/RTU module
-NIC1              Network interface card (PC/server)
-GPS_SYNC1         GPS time synchronisation module
```

### Safety PLC Modules
```
-CPU_S1            Safety CPU (SIL-rated)
-CPU_S_A           Safety CPU A (redundant)
-CPU_S_B           Safety CPU B (redundant)
-CPU_S_C           Safety CPU C (TMR)
-DI_S01            Safety DI module
-DO_S01            Safety DO module
-AI_S01            Safety AI module
-DIAG_MOD1         Diagnostic module (SIS health monitoring)
```

---

## Safety Devices & Safety Relays

### Safety Relays & Controllers
```
-F3_ESTOP          Safety relay — E-stop category (e.g. PILZ PNOZ X, Siemens 3SK)
-F3_GUARD          Safety relay — guard door monitoring
-F3_LIGHT          Safety relay — light curtain / area scanner
-F3_TWO_HAND       Safety relay — two-hand control
-F3_ENABLE         Safety relay — enabling device
-F3_MAT            Safety relay — safety mat / pressure mat
-F3_MUTE           Safety relay — muting function
-SAFE_CTRL1        Safety controller (e.g. PILZ PNOZmulti, B&R SafeLogic)
-F_SAFE_PLC        Safety PLC integrated module
-SIM1              Safety integrity monitor module
```

### Safety Sensors & Detection
```
-SB_ESTOP          Emergency stop push button (latching, twist-to-release)
-SB_ESTOP_ROPE     Rope pull / cable pull e-stop switch
-SL_GUARD1         Guard door interlock switch (solenoid lock type)
-MAG_SAFE1         Magnetic safety switch (non-contact guard)
-TPSW1             Trapped key switch (key exchange system)
-RFID_SAFE1        RFID safety switch (coded — IEC 60947-5-3 type 4)
-LIGHT_CRT1        Light curtain (safety — Type 4 AOPD)
-AREA_SCAN1        Safety area scanner (laser — SICK, LEUZE, Keyence)
-SAFETY_MAT1       Safety pressure mat / floor mat
-SAFE_EDGE1        Safety edge / bumper (robot perimeter)
-TWO_HAND1         Two-hand control device
-ENABLE_DEV1       Enabling device (3-position switch — pendant)
-SAFE_DOOR1        Safety door interlock (EUCHNER, Schmersal)
-SAFE_HINGE1       Safety hinge switch
-INTERLOCK1        Mechanical / trapped key interlock
```

---

## Communications & Network Devices

### Ethernet & Industrial Network
```
-SW_CORE_OT        Core OT Ethernet switch (managed Layer 2/3)
-SW_DIST_OT1       Distribution OT switch
-SW_PN1            PROFINET switch (DIN rail — Scalance, Moxa, etc.)
-SW_EIP1           EtherNet/IP switch
-SW_MGMT1          Management network switch (out-of-band)
-SW_CORE_IT        Core IT switch
-RTR_WAN1          WAN router
-RTR_4G1           4G / LTE router (cellular)
-FW_OT_IT1         OT/IT firewall / industrial firewall
-FW_CORP1          Corporate perimeter firewall
-AP_INDUS1         Industrial WiFi access point
-FC_FIBER1         Fibre / copper media converter
-FDP1              Fibre distribution panel
-PATCH_ETH1        Ethernet patch panel
-HUB1              Network hub (legacy — avoid in new designs)
```

### Serial & Fieldbus
```
-CM_485_1          RS485 module / repeater
-CONV_485_TCP1     RS485 to Modbus TCP converter
-DP_COUPLER1       PROFIBUS DP Y-coupler / repeater
-FF_COUPLER1       Foundation Fieldbus H1 coupler / power conditioner
-ASI_MOD1          AS-Interface module / slice
-IOLINK_HUB1       IO-Link hub
-HART_MOD1         HART modem / interface
```

### Telemetry & WAN
```
-MODEM_4G1         4G LTE modem
-MODEM_3G1         3G UMTS modem (legacy)
-RADIO_UHF1        UHF radio modem (licensed)
-RADIO_900M1       900MHz licence-exempt radio
-SAT_MODEM1        Satellite modem (VSAT, Ku-band)
-FIBER_MOD1        Fibre optic modem
-MW_IDU1           Microwave indoor unit
-ANT_4G1           4G antenna
-ANT_RADIO1        Radio antenna (Yagi, omni)
-ANT_GPS1          GPS antenna
-LIGHTNING_ARR1    Antenna lightning arrester
```

### Time & Synchronisation
```
-NTP_SRV1          GPS-disciplined NTP server
-GPS_RCV1          GPS receiver module
-PTP_GM1           IEEE 1588 PTP grandmaster clock
-TIME_CODE1        IRIG-B time code receiver (substation)
```

---

## HMI, Computers & IT Hardware

### HMI & Operator Terminals
```
-TP1               HMI touchpanel (Siemens TP, comfort series)
-TP_700            Siemens TP700 / KTP700 (by model — common)
-OP1               Operator panel (button-based, no touch)
-KTP1              Key touchpanel (combined keys + touch)
-MP1               Multi-panel HMI
-PC_HMI1           HMI PC / industrial PC with SCADA client
-PC_IPC1           Industrial PC (panel PC, DIN rail PC)
-THIN1             Thin client / zero client
-WS_HMI1           HMI workstation (office-type PC)
-WS_ENG1           Engineering workstation
-WS_SCADA1         SCADA operator workstation
-MON1 .. -MONn     Monitor / display
-TOUCH_MON1        Touchscreen monitor
-VIDEO_WALL1       Video wall processor
```

### Servers
```
-SRV1 .. -SRVn     Server (general)
-SRV_SCADA1        SCADA primary server
-SRV_SCADA_STB     SCADA standby server
-SRV_HIST1         Historian server
-SRV_OPC1          OPC server (DA / UA)
-SRV_APP1          Application server
-SRV_ENG1          Engineering / development server
-SRV_DR1           Disaster recovery server
-SRV_WEB1          Web server
-SRV_BACKUP1       Backup server
-ESXI1             VMware ESXi host
-HYPER_V1          Microsoft Hyper-V host
-VM1 .. -VMn       Virtual machine (if tagged individually)
```

### Storage & Peripherals
```
-NAS1              Network attached storage
-SAN1              SAN storage array
-HDD1              Hard disk drive (if tagged)
-TAPE_LIB1         Tape library
-KVM_SW1           KVM switch
-KVM_TX1           KVM extender — transmitter (server end)
-KVM_RX1           KVM extender — receiver (desk / console end)
-IPKVM1            IP KVM aggregator / console server
-SCS1              Serial console server
-USB_HUB1          USB hub
-PRINTER1          Alarm printer / label printer
-SCANNER1          Barcode scanner / document scanner
-UPS_RACK1         Rack-mount UPS
-PDU_A1            Rack PDU A side
-PDU_B1            Rack PDU B side
```

### Cybersecurity Appliances
```
-DATA_DIODE1       Data diode (unidirectional security gateway)
-FW_OT_IT1         OT/IT boundary firewall appliance
-IDS_SENSOR1       OT intrusion detection sensor
-PAM_APPLN1        Privileged access management appliance
-SRV_SIEM1         SIEM server
-SRV_JUMP1         Jump server / bastion host
```

---

## Heating, Cooling & Environmental

### Panel Heating & Thermostat
```
-HTR1 .. -HTRn     Anti-condensation heater / panel heater
-EH1               Heating element (IEC 81346)
-THERM1            Thermostat (for panel heater control)
-HYGROSTAT1        Hygrostat (humidity-based heater control)
-PTC_HTR1          PTC self-regulating heater
```

### Panel Cooling & Ventilation
```
-FAN1 .. -FANn     Panel cooling fan (filter fan unit)
-VF1               Ventilation fan (IEC 81346)
-FFU1              Filter fan unit (complete assembly)
-HEAT_EXC1         Heat exchanger / air conditioner (panel-mount)
-VORTEX1           Vortex cooler (pneumatic, Ex areas)
-AC_UNIT1          Panel air conditioning unit
```

### Environmental Sensors
```
-THERM_PANEL1      Panel internal thermostat / temperature monitor
-HUMID1            Humidity sensor (internal)
-FLAME_DET1        Flame detector (cabinet fire protection)
-SMOKE_DET1        Smoke detector (inside cabinet)
```

---

## Pneumatic & Hydraulic Devices

### Valves
```
-YV1 .. -YVn       Solenoid valve (pneumatic / hydraulic)
-YV_FWD            Forward solenoid valve
-YV_REV            Reverse solenoid valve
-YV_CLAMP          Clamp solenoid
-YV_UNCLAMP        Unclamp solenoid
-YV_BRAKE          Brake release solenoid
-YV_VENT           Vent solenoid valve
-YV_SAFETY         Safety / dump solenoid valve
-VA_CTRL1          Motorised control valve (process)
-VA_ON_OFF1        Motorised on/off valve
-VA_ISOL1          Motorised isolation valve
-PV1               Proportional valve (hydraulic)
-SERVO_V1          Servo valve (hydraulic)
```

### Actuators & Cylinders
```
-CYL1 .. -CYLn     Pneumatic / hydraulic cylinder
-CYL_EXT1          Cylinder extend solenoid
-CYL_RET1          Cylinder retract solenoid
-ACT_LIN1          Linear actuator (electric)
-ACT_ROT1          Rotary actuator
-POSITIONER1       Valve positioner (electropneumatic — 4-20mA input)
-EP_POSITIONER1    EP positioner (electro-pneumatic)
-TRANSDUCER_IP1    I/P transducer (current to pneumatic)
```

### Pneumatic Control
```
-AIR_REG1          Pressure regulator (instrument air)
-FRL1              Filter-regulator-lubricator unit
-MFLD1             Pneumatic manifold
-CHECK_V1          Check valve (if monitored)
```

---

## Mechanical & Structural Components

### Machine Hardware (tagged when wired)
```
-ENC_DOOR1         Enclosure door (if interlocked)
-LOCK1             Solenoid lock (door or guard)
-LIMIT_MECH1       Mechanical limit switch (cam-operated)
-HOME_SW1          Home position switch
-BUFFER1           Mechanical buffer / end stop (if wired)
-SCALE1            Linear scale (glass or magnetic)
-RULER1            Ruler / measuring tape sensor
-LEVEL_SITE1       Spirit level sensor (machine levelling)
```

---

## Cables, Conduits & Routing

> IEC 81346 uses `-W` prefix for cables / conductors. In practice many engineers use project-specific cable numbering.

### Cable Numbering Conventions
```
--- IEC 81346 style ---
-W1 .. -Wn         Cable (general)
-WC1               Control cable
-WP1               Power cable
-WS1               Signal cable (instrument)
-WF1               Fibre optic cable
-WN1               Network cable

--- Project number style (most common in practice) ---
-CAB001 .. -CABnnn Sequential cable number
-CC001             Control cable 001
-PC001             Power cable 001
-SC001             Signal cable 001
-FC001             Fibre cable 001
-NC001             Network cable 001

--- Area / route coded style ---
-CAB_A_001         Cable in area A, number 001
-CAB_MCC1_M01      Cable from MCC1 to motor M01

--- Trunkings & Conduits ---
-TRNK1             Cable trunking run 1
-CNDUIT1           Conduit run 1
-TRAY1             Cable tray run 1
-DUCT1             Underground cable duct
```

---

## Panel Building Hardware

### Panel Structure Components
```
-DIN1 .. -DINn     DIN rail (mounting rail)
-DUCT1 .. -DUCTn   Cable duct / wireway
-GLAND1            Cable gland (if individually tagged)
-GLAND_PG16_1      PG16 cable gland
-GLAND_M20_1       M20 metric cable gland
-GLAND_EX1         Ex-rated cable gland
-EARTH_BAR1        Earth busbar / earth rail
-PE_BAR            PE (protective earth) terminal bar
-N_BAR             Neutral terminal bar
-LOCK_OFF1         Lockout hasp / lockout device
-DOOR_LOCK1        Panel door lock
-WINDOW1           Viewing window (if referenced)
-LABEL1            Panel / device label (if in BOM)
```

### Surge Protection
```
-SPD1 .. -SPDn     Surge protection device (SPD / lightning arrester)
-SPD_AC1           AC surge arrester (Type 1, 2, or 3)
-SPD_DC1           DC surge arrester
-SPD_DATA1         Data line surge arrester (RS485, analogue)
-SPD_ETH1          Ethernet surge arrester
-MOV1              Metal oxide varistor
-TVS1              Transient voltage suppressor
```

---

## MV Switchgear Specific Devices

> Devices specific to MV switchgear not covered in earlier sections

```
-QB1               Vacuum / SF6 circuit breaker
-QD1               Air-break disconnector / pantograph
-QS1               Load break switch (ring main)
-QE1 / -ES1        Earthing switch
-FU1               HRC fuse (MV TX feeder)
-CT1               Current transformer (protection / metering)
-VT1               Voltage transformer (metering / synch)
-CLOSING_COIL1     Closing coil (VCB)
-TRIP_COIL1        Trip coil 1 (VCB — main)
-TRIP_COIL2        Trip coil 2 (VCB — backup)
-ANTI_PUMP_K1      Anti-pump relay
-MOT_OP1           Motor operator (VCB / LBS motorised operation)
-POSITION_IND1     Position indicator (mechanical — open/close)
-SPRING_CHARGED1   Spring charged indicator / switch
-DRAW_OUT_LOCK1    Draw-out position interlock
-TEST_POS1         Test position switch (draw-out equipment)
-INSERT_POS1       Inserted / service position switch
-EARTH_POS1        Earthed position switch
-ARC_DETECT1       Arc flash detector (fibre / light)
```

---

## Battery & DC System Devices

```
-BATT1 .. -BATTn   Battery cell / battery string
-BATT_BANK1        Battery bank (complete assembly)
-CELL_MON1         Battery cell monitoring module
-BMS1              Battery management system module
-CHRG_A            Charger A (float / boost)
-CHRG_B            Charger B (standby)
-FLOAT_CHRG1       Float charger
-BOOST_CHRG1       Boost / equalise charger
-DC_QF1            DC MCB (for DC distribution feeders)
-DC_FUSE1          DC fuse (blade or cartridge)
-DIODE1            Isolation diode (parallel charger coupling)
-SHUNT1            Current shunt (for DC current measurement)
-BATT_MON1         Battery monitor / impedance tester
-LOW_V_DISC1       Low voltage disconnect relay
-HI_V_DISC1        Overvoltage disconnect relay
-EARTH_FAULT_MON1  DC earth fault monitor (Bender, etc.)
```

---

## Fire, Gas & Safety Detectors

### Fire Detection
```
-SD1 .. -SDn       Smoke detector (general)
-SMOKE_ION1        Ionisation smoke detector
-SMOKE_OPT1        Optical smoke detector
-HEAT_DET1         Heat detector (rate-of-rise or fixed temperature)
-FLAME_IR1         IR flame detector
-FLAME_UV1         UV flame detector
-FLAME_UV_IR1      UV/IR combined flame detector
-MULTI_DET1        Multi-criteria detector (heat + smoke)
-VESDA1            VESDA / aspirating smoke detector (sampling point)
-BEAM_DET1         Beam smoke detector (projected)
-CALL_POINT1       Manual call point / break glass
-SIRN_FIRE1        Fire alarm sounder / siren
-STRB_FIRE1        Fire alarm strobe
-SOUNDER_BASE1     Detector sounder base
```

### Gas Detection
```
-GD_GAS1           Gas detector (general)
-GD_CATA1          Catalytic bead gas detector (%LEL — combustible)
-GD_IR_FIXED1      Fixed infrared gas detector (CH4, CO2, etc.)
-GD_OP1            Open-path gas detector (IR beam — area coverage)
-GD_H2S1           H2S toxic gas detector (electrochemical)
-GD_CO1            CO toxic gas detector
-GD_O2_DEF1        Oxygen deficiency detector
-GD_O2_ENR1        Oxygen enrichment detector
-GD_CL2_1          Chlorine gas detector
-GD_NH3_1          Ammonia gas detector
-GD_SONIC1         Acoustic gas leak detector (ultrasonic)
-GD_CTRL1          Gas detection controller / addressable module
-BEACON_GAS1       Warning beacon (gas detection alarm)
```

### Life Safety
```
-SPRINKLER1        Sprinkler flow switch (if wired to I/O)
-SUPPRS_VALVE1     Suppression system valve (FM200, CO2)
-HAND_HELD_EXT1    Portable extinguisher monitor
-PULL_STN1         Pull station (Halon / clean agent release)
-ABORT_SW1         Abort switch (suppression system)
-SOUNDER_VAC1      Evacuation sounder
-STRB_EVAC1        Evacuation strobe
-PA_SPKR1          PA / EVAC loudspeaker
-INTERCOM1         Intercom station (safety / emergency)
```

---

## Building Services Devices

### Access Control & Security
```
-CARD_RDR1         Card reader (access control)
-KEYPAD1           PIN keypad
-INTERCOM_DR1      Door intercom
-MAG_LOCK1         Magnetic door lock
-ELEC_STRIKE1      Electric door strike
-EXIT_BTN1         Exit button (green — door release)
-PIR1              PIR motion sensor (security / building)
-CCTV_CAM1         CCTV camera
-CCTV_DOM1         CCTV dome camera
-CCTV_PTZ1         CCTV PTZ camera
-VIDEO_REC1        Video recorder / NVR
-SIREN_SEC1        Security siren / intruder alarm sounder
```

### Lighting
```
-EL1 .. -ELn       Luminaire / light fitting (IEC 81346)
-LIGHT1            Light fitting
-EMERG_LIGHT1      Emergency light fitting (maintained)
-EMERG_SIGN1       Emergency exit sign
-EMERG_CENTRAL1    Central battery emergency lighting system
-DALI_CTRL1        DALI lighting controller
-DALI_BUS1         DALI bus coupler / power supply
-DIM1              Dimmer module
-SENS_LIGHT1       Daylight sensor / photocell
-MOTION_LIGHT1     Motion-activated lighting switch
```

---

## Numbering Conventions & Suffixes

### Sequential Numbering (most common)
```
-K1, -K2, -K3, -K4       Simple sequential — good for small panels
-KM1, -KM2, -KM3         Sequential by type — good for MCCs
-DI01, -DI02, -DI03      Zero-padded — essential for sorted reports
-FT101, -FT102, -FT103   ISA loop-based — process industry
```

### Alphabetical Suffixes (for duplicates / phases)
```
-CT_A, -CT_B, -CT_C      Phase A, B, C CTs
-CPU_A, -CPU_B            Redundant pair A/B
-PS_A, -PS_B              Redundant power supplies
-QF_INC_A, -QF_INC_B     Dual incomer A and B
```

### Descriptive Suffixes (for clarity in complex panels)
```
-KM_MAIN               Immediately identifies main contactor
-KM_STAR               Identifies star contactor clearly
-F_OC_A                Overcurrent relay incomer A
-HL_RUN                Run indicator (no ambiguity)
-SB_ESTOP              E-stop button (safety critical — must be obvious)
-SW_PN_A1              Switch for PROFINET in area A1
```

### ISA Loop Number Convention
```
-FT101     First two letters = variable + device type, three digits = loop number
-FT101A    Suffix letter = multiple devices in same loop (transmitter A)
-FT101B    Second transmitter in same loop (e.g. 2oo3 voting)
-FT101C    Third transmitter in loop (TMR / 2oo3)
-LS401H    Level switch high (H suffix = high trip)
-LS401L    Level switch low (L suffix = low trip)
-LS401HH   Level switch high-high (HH = safety trip)
-LS401LL   Level switch low-low (LL = safety trip)
```

### Panel / Location Coded Prefixes (alternative style)
```
-CP1_K1    Relay in panel CP1 — location embedded in device tag
           (Not recommended in EPLAN — this is what the + location is for)
```

---

## Full Tag Examples — Complete Projects

### Example 1 — DOL Motor Starter in MCC
```
=PWR.INC+MCC1.INC-QF_INC                Main incomer MCCB
=METER+MCC1.INC-CT_INC                  Incomer CT
=METER+MCC1.INC-PQ1                     Power analyser
=MOTOR.DOL+MCC1.M01-QF1                 Motor M01 feeder MCCB
=MOTOR.DOL+MCC1.M01-F_MOTOR1            Motor protection relay
=MOTOR.DOL+MCC1.M01-KM_MAIN             Main contactor
=CTRL+MCC1.M01-SS_LOCAL                 Local/remote selector
=CTRL+MCC1.M01-SB_START                 Start push button
=CTRL+MCC1.M01-SB_STOP                  Stop push button
=CTRL+MCC1.M01-HL_RUN                   Run indicator lamp
=CTRL+MCC1.M01-HL_TRIP                  Trip indicator lamp
=CTRL+MCC1.M01-X1                       Terminal block (field wiring)
=MOTOR+FIELD-M1                         Motor (in field)
```

### Example 2 — Star-Delta Starter
```
=MOTOR.STAR_D+MCC1.M02-QF1             Feeder MCCB
=MOTOR.STAR_D+MCC1.M02-F_MOTOR2        Motor protection relay
=MOTOR.STAR_D+MCC1.M02-KM_MAIN         Line contactor
=MOTOR.STAR_D+MCC1.M02-KM_STAR         Star contactor
=MOTOR.STAR_D+MCC1.M02-KM_DELTA        Delta contactor
=MOTOR.STAR_D+MCC1.M02-KT_SD           Star-delta timer
=CTRL+MCC1.M02-SB_START                Start button
=CTRL+MCC1.M02-SB_STOP                 Stop button
=CTRL+MCC1.M02-HL_STAR                 Star mode indicator
=CTRL+MCC1.M02-HL_DELTA                Delta mode indicator
=CTRL+MCC1.M02-HL_TRIP                 Trip indicator
=MOTOR+FIELD-M2                        Motor (in field)
```

### Example 3 — PLC Control Panel
```
=PWR.CTRL+CP1.POWER-QF_MAINS           Mains incoming MCB
=PWR.24V+CP1.POWER-PS1                 24VDC SMPS primary
=PWR.24V+CP1.POWER-PS2                 24VDC SMPS redundant
=PWR.UPS+CP1.POWER-UPS_BUF1            24VDC UPS buffer module
=PWR.24V+CP1.DIST_24V-FT1              PLC fused terminal block
=PWR.24V+CP1.DIST_24V-FT2              I/O fused terminal block
=PWR.24V+CP1.DIST_24V-FT3              Field sensor fused terminal
=CTRL.PLC+CP1.PLC-CPU1                 PLC CPU
=CTRL.IO+CP1.IO-DI01                   Digital input module 01
=CTRL.IO+CP1.IO-DO01                   Digital output module 01
=CTRL.IO+CP1.IO-AI01                   Analog input module 01
=CTRL.COMM+CP1.COMM-CM_PN1             PROFINET module
=CTRL.SAFE+CP1.SAFE-F3_ESTOP           E-stop safety relay
=CTRL.SAFE+CP1.SAFE-F3_GUARD           Guard door safety relay
=CTRL+CP1.RELAY-K_WD                   Watchdog relay
=CTRL.HMI+CP1.DOOR.HMI-TP_700         HMI touchpanel
=SAFE.ESTOP+CP1.DOOR.OP-SB_ESTOP       E-stop push button
=CTRL+CP1.DOOR.OP-SS_MODE              Mode selector
=CTRL+CP1.DOOR.OP-SB_RESET             Reset button
=CTRL+CP1.DOOR.OP-HL_POWER            Power indicator
=CTRL+CP1.DOOR.OP-HL_RUN              Run indicator
=CTRL+CP1.DOOR.OP-HL_FAULT            Fault indicator
=CTRL+CP1.TERM.DI-X_DI1               DI terminal block
=CTRL+CP1.TERM.AI-X_AI1               AI terminal block
=CTRL+CP1.TERM.SAFE-X_SAFE1           Safety terminal block
```

### Example 4 — Process Instrumentation Loop (Flow)
```
=INST+FIELD-FE101                      Flow element (orifice plate)
=INST+FIELD-FT101                      Flow transmitter (HART 4-20mA)
=INST+INST_CAB_01.BARRIER.AI-Z_FT101   Zener barrier for FT101
=INST+MARSH_CAB_A.AI-X_AI_FT101       Marshalling terminal block
=DCS.IO+DCS_CAB1.IO_RACK_A-AI01       DCS AI card (receives FT101 signal)
=DCS+CTRL_RM.DESK1.PC_HMI1-WS_DCS1   DCS HMI workstation
=PWR+MCC1.M01-KM_MAIN                 Pump contactor (flow control output)
```

### Example 5 — MV Switchgear Feeder Panel
```
=MV.FDR+MV_SW1.FDR_1-QB1              Feeder VCB
=MV.FDR+MV_SW1.FDR_1-QD1             Line disconnector
=MV.FDR+MV_SW1.FDR_1-QE1             Earth switch
=MV.FDR+MV_SW1.FDR_1-CT1             Protection CT phase A
=MV.FDR+MV_SW1.FDR_1-CT2             Protection CT phase B
=MV.FDR+MV_SW1.FDR_1-CT3             Protection CT phase C
=PROT.OC+MV_SW1.FDR_1-F_OC1          Overcurrent relay (e.g. REF615, SEL-751)
=PROT.EF+MV_SW1.FDR_1-F_EF1          Earth fault relay
=METER+MV_SW1.FDR_1-PQ1              Power quality analyser
=CTRL+MV_SW1.FDR_1-CLOSING_COIL1     VCB closing coil
=CTRL+MV_SW1.FDR_1-TRIP_COIL1        VCB trip coil 1
=CTRL+MV_SW1.FDR_1-TRIP_COIL2        VCB trip coil 2 (backup)
=CTRL+MV_SW1.FDR_1-ANTI_PUMP_K1      Anti-pump relay
=CTRL+MV_SW1.FDR_1-HL_CLOSED         Breaker closed indicator (red)
=CTRL+MV_SW1.FDR_1-HL_OPEN           Breaker open indicator (green)
=CTRL+MV_SW1.FDR_1-SB_CLOSE          Close push button
=CTRL+MV_SW1.FDR_1-SB_OPEN           Open push button
=CTRL+MV_SW1.FDR_1-SS_LOCAL          Local/remote selector
=CTRL+MV_SW1.FDR_1-X1                Control wiring terminal strip
=DC+MV_SW1.FDR_1-QF_DC1              DC MCB for trip circuit
```

### Example 6 — Safety PLC SIL2 Shutdown Loop
```
--- Field sensing ---
=SIS.IO+FIELD-PT201A                  Pressure transmitter A (SIL2 — 2oo3)
=SIS.IO+FIELD-PT201B                  Pressure transmitter B
=SIS.IO+FIELD-PT201C                  Pressure transmitter C

--- Marshalling ---
=SIS.IO+MARSH_CAB_B.DI_SAFE-X_PT201  Safety PT terminal (2oo3 wiring)
=SIS.IO+MARSH_CAB_B.BARRIER_S-Z_PT201A  Safety barrier for PT201A

--- SIS Logic Solver ---
=SIS.IO+SIS_CAB1.IO_A-DI_S01_A       Safety DI module (1oo2D architecture)
=SIS.IO+SIS_CAB1.IO_B-DI_S01_B       Safety DI module B
=SIS.LOGIC+SIS_CAB1.LOGIC_A-CPU_S_A  SIS logic solver A
=SIS.LOGIC+SIS_CAB1.LOGIC_B-CPU_S_B  SIS logic solver B
=SIS.POWER+SIS_CAB1.POWER_A-PS_S_A   SIS power supply A
=SIS.POWER+SIS_CAB1.POWER_B-PS_S_B   SIS power supply B

--- Final Element ---
=SIS.IO+SIS_CAB1.IO_A-DO_S01_A       Safety DO module A
=ESD.L2+FIELD-SDV201                  Shutdown valve (solenoid — de-energise to close)
=ESD.L2+FIELD-YV_SDV201              Solenoid valve coil on SDV201
=ESD.L2+FIELD-ZS_SDV201_O            Position switch — open
=ESD.L2+FIELD-ZS_SDV201_C            Position switch — closed
```

---

## Cross-Reference: IEC 81346 vs ISA-5.1 vs Common Practice

| Device | IEC 81346 | ISA-5.1 | Common Practice |
|--------|-----------|---------|-----------------|
| Circuit breaker (LV) | `QF` | — | `QF`, `CB`, `MCB`, `MCCB` |
| Circuit breaker (MV) | `QB` | — | `QB`, `VCB`, `ACB` |
| Contactor | `KC` / `KM` | — | `KM`, `K` |
| Fuse | `FA` | — | `FU`, `F`, `FA` |
| Motor | `MA` | — | `M`, `MA` |
| Solenoid valve | `YV` / `YA` | — | `YV`, `SV`, `VA` |
| Relay (aux) | `KA` | — | `K`, `KA`, `CR` |
| Timer | `KT` | — | `KT`, `TR`, `T` |
| Indicator lamp | `HL` | — | `HL`, `PL`, `IL` |
| Push button | `SB` | — | `SB`, `PB`, `BS` |
| Selector switch | `SS` / `SA` | — | `SS`, `CS`, `SA` |
| Transformer | `TM` / `T` | — | `T`, `TR`, `TM` |
| CT | `TA` | — | `CT`, `TA` |
| VT | `TV` | — | `VT`, `PT`, `TV` |
| Power supply | `GS` | — | `PS`, `GS`, `PSU` |
| UPS | `GU` | — | `UPS`, `GU` |
| Terminal block | `XT` / `X` | — | `X`, `XT`, `TB` |
| Flow transmitter | `BF` | `FT` | `FT` (process), `BF` (IEC) |
| Pressure transmitter | `BP` | `PT` | `PT` (process), `BP` (IEC) |
| Temperature transmitter | `BT` | `TT` | `TT` (process), `BT` (IEC) |
| Level transmitter | `BL` | `LT` | `LT` (process), `BL` (IEC) |
| Control valve | `VA` | `CV` / `FCV` | `FCV`, `PCV`, `LCV` (ISA) |
| VFD | `NA` | — | `VFD`, `VSD`, `NA` |
| Safety relay | `KF` | — | `F3`, `KF`, `SR` |
| Zener barrier | `ZA` | — | `ZA`, `ZB`, `MTL` |
| Encoder | `BK` | — | `ENC`, `BK`, `EC` |

---

## Common Mistakes

| ❌ Wrong | ✅ Correct | Reason |
|----------|------------|--------|
| `-PANEL_A` | `+PANEL_A` | Panel is a location, not a device |
| `-CONTROL_SYSTEM` | `=CTRL` | Control system is a function, not a device |
| `-M_01` (inconsistent spacing) | `-M01` | Spaces / inconsistency breaks EPLAN sort order |
| `-K1`, `-k1`, `-K_1` for same relay type | Pick one style — `-K1` | Inconsistent capitalisation and separators = different devices |
| `-FT101` without context | `=INST+FIELD-FT101` | Always needs `=` and `+` to be complete |
| Using name only: `-MAIN_CONTACTOR` | `-KM_MAIN` | No type letter = can't filter by device type in reports |
| Same tag in two locations: `+CP1-K1` and `+MCC1-K1` | Both valid if function differs | Duplicate tags across different `=+` combinations are OK — EPLAN uses full path |
| `-1K` (number before letter) | `-K1` | IEC 81346 requires letter code first |
| `-QF001` and `-QF01` in same project | `-QF01` throughout | Mixed zero-padding breaks alphabetical sort in reports |
| `-PT_HIGH_PRESSURE_TRANSMITTER_LOOP_201` | `-PT201` | Too long — truncated in reports, hard to read on diagrams |
| Omitting device tag entirely | Always assign `-` tag | Blank device tag = invisible in BOM and terminal reports |
| Using `-WIRE1` for every wire | Reserve `-W` for cables, not individual wires | EPLAN handles internal wiring differently from cables |

---

## Expert Tips

### 1. Always use a letter code — never just a number
> `-K1` not `-1`. The letter is what lets EPLAN and IEC reports group, filter, and sort by device type. Reports like parts lists, terminal diagrams, and cable schedules all depend on it.

### 2. Zero-pad your numbers from the start
> `-DI01` not `-DI1`. When you have `-DI01` through `-DI12`, they sort correctly. `-DI1` through `-DI12` sorts as 1, 10, 11, 12, 2, 3... which makes every report painful.

### 3. Choose IEC 81346 codes OR ISA codes — not both
> Process plant? Use ISA (`-FT101`, `-PT201`). Machine or panel? Use IEC (`-KM1`, `-QF1`). The worst projects mix both. Decide at project kick-off.

### 4. Descriptive suffixes add value in complex panels
> `-KM_MAIN`, `-KM_STAR`, `-KM_DELTA` is better than `-KM1`, `-KM2`, `-KM3` in a star-delta starter. The person wiring the cabinet shouldn't need to look up which `-KM2` is.

### 5. ISA loop numbers carry meaning — use them consistently
> `-FT101` means flow transmitter, loop 101. The loop number should match your P&ID. Don't start loops at 1 — use area-coded numbers (100-series = area 1, 200-series = area 2) for large plants.

### 6. Use letter suffixes for redundant devices in the same loop
> `-FT101A`, `-FT101B`, `-FT101C` for three transmitters in a 2oo3 SIL voting loop. This is the ISA convention and immediately tells the instrument engineer the devices belong to the same loop.

### 7. High-high / low-low convention for safety trips
> `-LSH401` = level switch high, `-LSHH401` = level switch high-high (safety). The H/L/HH/LL suffixes are recognised across industries. Use them for anything connected to an SIS/ESD.

### 8. Terminal blocks get `-X1`, `-X2` etc. — not `-T1` or `-TB1`
> EPLAN specifically uses `-X` prefix for terminal blocks in its terminal diagram generation engine. Using other letters means your terminal reports may not auto-populate correctly.

### 9. Never embed location into the device tag
> `-CP1_K1` is wrong — the panel CP1 information belongs in `+CP1`. The device tag should just be `-K1`. The full reference `=CTRL+CP1-K1` already carries the location.

### 10. Document your device tag convention in a legend page
> Create a `EAC` (explanatory documents) page at the front of the project listing all device tag abbreviations used. Future engineers, clients, and maintenance teams will spend hours less confused.

---

*Based on IEC 81346 | IEC 61346 | ISA-5.1 | ISA-20 | IEC 60617 | IEC 61131 | IEC 61511 | IEC 62271 | IEC 61439 | IEC 61850*
*Expert conventions compiled from electrical, automation, instrumentation, process, power, safety, and IT engineering disciplines*
