---
layout: post
cover_color: #000000

keywords: EPLAN P8, Designation, Device, IEC 81346

title: EPLAN IEC 81346 Device Designation - Letter Table
description: A complete reference for EPLAN device designations based on IEC 81346, covering every device type across electrical, automation, instrumentation, IT, and mechanical disciplines, with examples and best practices.

author: Mahmoud Lotfi
date: 2024-03-01 10:00:00 +0800
file_name: 2024-03-01-eplan-iec-81346-designation-device-table-primary-letters.md
categories: [EPLAN, IEC 81346, tables, Designation, Device]
tags: [EPLAN, IEC 81346, device, tables]
pin: False
math: true
mermaid: true
comments: true
toc: true
render_with_liquid: false
image:
  path: /assets/img/posts/eplan.jpg
  alt: EPLAN Device Designation Reference with IEC 81346 and ISA-5.1 and common practice tag naming
  lqip: data:image/webp;base64,UklGRjoAAABXRUJQVlA4IC4AAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA

---


# IEC 81346 Device Reference Designation — Letter Codes

> **Standard basis:** IEC 81346-1:2009 (primary letters) and IEC 81346-2:2019 (two-letter combinations).  
> Replaces the older IEC 60750 / ISO 10209 designation systems.  
> Status badges used below: `[STD]` = defined in IEC 81346-2 | `[IND]` = established industry practice | `[EXT]` = external extension (NAMUR/other) | `[AMB]` = ambiguous or nationally inconsistent.

---

## Part 1 — Primary Letters (Device Kind)

The first letter defines the **object class** — what the device fundamentally *does*, not what it is called commercially. IEC 81346-1:2009 defines these classes as part of a hierarchical reference designation system.

| Letter | Device Kind | Typical Devices | Real-Life Example | Use Case | Domains |
|--------|------------|----------------|-------------------|----------|---------|
| `B` | Converts physical variable → signal | Sensors, transducers, encoders, detectors | PT100 temperature sensor on pump bearing; electromagnetic flow meter on main supply pipe | Any process variable converted to a 4–20 mA or digital signal for PLC/SCADA | Instrumentation, Automation |
| `C` | Stores energy or material | Capacitors, batteries, tanks, accumulators | Power factor correction capacitor bank; hydraulic accumulator | Energy buffering, reactive power compensation, pressure storage | Power, Automation |
| `D` | Processes / stores information | PLCs, computers, HMIs, recorders, displays | Siemens S7-1500 PLC; SCADA historian server; Weintek HMI panel | Logic execution, data logging, operator interface | Automation, SCADA |
| `E` | Provides radiation or thermal energy | Heaters, lamps, UV emitters | Trace heating on freeze-sensitive pipe; UV disinfection lamp | Process heating, sterilisation, space conditioning | Utility, Process |
| `F` | Protects against dangerous conditions | Fuses, breakers, protection relays, safety devices | Motor protection relay; MCCB on feeder circuit; earth-fault relay on MV panel | Overcurrent, earth fault, differential, and overvoltage protection | Power, Protection |
| `G` | Generates / supplies electrical energy | Power supplies, batteries, generators, UPS | Diesel generator as standby source; UPS for SCADA room; 24 VDC SMPS in control panel | Backup power, control voltage supply, embedded generation | Power |
| `H` | Signals / indicates state or condition | Lamps, buzzers, horns, displays, annunciators | Red/green pilot lamp on MCC door; audible alarm in pump station; mimic panel lamp | Operator notification, status indication, alarm annunciation | Automation, Safety |
| `K` | Processes signals / controls / switches | Relays, timers, contactors, PLC outputs | Motor contactor in MCC; star-delta timer relay; auxiliary relay for interlock | Motor starting/stopping, interlock logic, signal switching | Automation, Power |
| `M` | Provides mechanical energy | Motors, actuators, cylinders, pumps (motor part) | 37 kW submersible borehole pump motor; actuator on butterfly valve | Fluid movement, mechanical drive, valve actuation | Mechanical, Process |
| `N` | Regulates / controls process variable | VFDs, PID controllers, regulators | VFD on high-lift pump for pressure control; PID controller for chlorine dosing | Variable speed, flow regulation, closed-loop process control | Automation, Power |
| `P` | Measures / tests | Meters, analysers, instruments, gauges | kWh meter on MV feeder; pressure gauge on pump outlet; water quality analyser | Billing metering, energy management, process monitoring | Instrumentation, Power |
| `Q` | Switches / varies electrical energy | Isolators, circuit breakers, disconnectors | MV vacuum circuit breaker; load break switch on ring main unit; ACB on LV incomer | Circuit isolation, fault interruption, switching under load | Power |
| `R` | Restricts / stabilises energy or flow | Resistors, reactors, chokes, dampers | Line reactor on VFD input; braking resistor on crane motor; neutral earthing resistor | Harmonic mitigation, fault current limitation, energy dissipation | Power |
| `S` | Converts manual operation → signal | Push buttons, switches, selectors, keyboards | Start/stop push buttons on MCC; local/remote selector switch; emergency stop button | Operator control input, mode selection, manual override | Automation |
| `T` | Converts electrical quantities | Transformers, CT, VT, rectifiers, inverters | 11 kV/0.4 kV distribution transformer; 400/5 A metering CT; protection VT on MV busbar | Voltage transformation, instrument signal scaling, AC/DC conversion | Power, Instrumentation |
| `U` | Keeps objects in a defined position | Clamps, brakes, locks, holders | Electromagnetic brake on motor shaft; shaft locking pin | Position holding, overspeed restraint, maintenance safety | Mechanical |
| `V` | Processes materials or products | Conveyors, mixers, reactors, valves (flow) | Butterfly valve on pump discharge; control valve on chlorine dosing line | Flow control, chemical dosing, water treatment process | Process |
| `W` | Conducts / transmits / distributes | Cables, busbars, waveguides, antenna | 11 kV XLPE cable between substation and pump station; LV busbar in switchboard | Power distribution, signal transmission, network connectivity | Power, Comms |
| `X` | Connects / terminates | Terminal blocks, connectors, plugs, junction | DIN rail terminal block in control panel; SWA cable gland and termination kit | Organised, safe termination of multi-core cables | Automation, Power |
| `Y` | Positions / guides | Positioners, guides, stepper actuators | Valve positioner on modulating valve; solenoid-operated pneumatic actuator | Precise valve positioning, actuator control, motion guidance | Automation, Mechanical |

> **Note on unused letters:** The letters `A`, `I`, `J`, `L`, `O`, and `Z` are not defined as primary object-class letters in IEC 81346-1. `Z` in particular appears in many plant documents (see `ZA`, `ZI`, `ZF` below) but those codes originate from NAMUR and industry extensions, not the core standard.

---

## Part 2 — Two-Letter Combinations

The second letter further qualifies the device type within its primary class. Many are defined in IEC 81346-2:2019; others are well-established industry conventions not explicitly listed in the standard. Verification notes are included where a code requires clarification.

### B — Sensors and Transducers

| Code | Description | Typical Device | Status | Real-Life Example | Use Case |
|------|------------|----------------|--------|-------------------|----------|
| `BK` | Encoder / speed sensor | Rotary encoder | `[IND]` | Shaft encoder on VFD-driven pump to verify speed feedback | Closed-loop speed control, motor tachometry |
| `BP` | Pressure sensor / transmitter | Pressure switch, 4–20 mA pressure transmitter | `[STD]` | 4–20 mA pressure transmitter on pump discharge header (0–10 bar) | Pump protection (low suction pressure trip), pressure control loop |
| `BT` | Temperature sensor | Thermocouple, PT100/PT1000 | `[STD]` | PT100 in motor winding for thermal protection; thermowell in process pipe | Motor protection, bearing monitoring, process temperature control |
| `BL` | Level sensor | Float switch, ultrasonic level transmitter | `[STD]` | Ultrasonic level sensor in clear water storage tank; float switch in sump pit | Tank high/low alarms, pump start/stop on level, overflow prevention |
| `BF` | Flow sensor | Electromagnetic flow meter, flow switch | `[STD]` | Electromagnetic flow meter (DN200) on water main supply pipe | Billing, water loss calculation, pump performance monitoring |
| `BA` | Analyser sensor | Gas analyser input, pH/chlorine sensor | `[IND]` | Residual chlorine analyser after dosing point; pH sensor in treatment tank | Water quality compliance monitoring, dosing control feedback |
| `BG` | Position / limit switch | Proximity sensor, mechanical limit switch | `[STD]` | Proximity switch detecting valve open/closed position on butterfly valve | Valve position feedback to SCADA, interlock condition for pump start |

### C — Storage

| Code | Description | Typical Device | Status | Real-Life Example | Use Case |
|------|------------|----------------|--------|-------------------|----------|
| `CM` | Motor capacitor | Run / start capacitor | `[IND]` | Run capacitor on single-phase booster pump motor | Power factor improvement for single-phase motors, starting torque |

### D — Information Processing

| Code | Description | Typical Device | Status | Real-Life Example | Use Case |
|------|------------|----------------|--------|-------------------|----------|
| `DD` | Data / logic processor | PLC, computer, industrial PC | `[STD]` | Siemens S7-300 PLC controlling pump station; local SCADA server in MCC room | Sequence logic, data acquisition, remote SCADA node |

### E — Radiation / Thermal Energy

| Code | Description | Typical Device | Status | Real-Life Example | Use Case |
|------|------------|----------------|--------|-------------------|----------|
| `EH` | Heating element | Trace heating, panel heater | `[STD]` | Self-regulating trace heat on exposed water pipe; anti-condensation heater in LV switchboard | Freeze protection, switchgear moisture control |
| `EL` | Lighting element | Lamp, LED strip | `[STD]` | LED luminaire in pump station; emergency lighting in switchroom | Working illumination, safety egress lighting |

### F — Protection

| Code | Description | Typical Device | Status | Real-Life Example | Use Case |
|------|------------|----------------|--------|-------------------|----------|
| `FA` | Fuse (general) | Cartridge fuse | `[STD]` | 2A control fuse protecting 24 VDC PLC supply circuit | Control circuit protection, secondary transformer protection |
| `FB` | Overcurrent protective device | MCCB, MCB | `[STD]` | 63A MCCB protecting motor feeder cable in MCC | Feeder overcurrent protection, discrimination co-ordination study |
| `FC` | Combined protective device | RCBO, motor circuit breaker | `[STD]` | Moeller PKZM motor circuit breaker combining short-circuit and overload protection on 11 kW pump | Space-saving combined protection in small MCC |
| `FD` | Residual current device | RCD, RCCB | `[STD]` | 30 mA RCD on convenience socket circuit in control room | Personnel protection against electric shock in wet utility areas |
| `FU` | HV fuse | HRC fuse, expulsion fuse | `[IND]` | MV HRC fuse in ring main unit protecting 11 kV/0.4 kV transformer | Transformer primary overcurrent protection at MV level |

### G — Generation / Supply

| Code | Description | Typical Device | Status | Real-Life Example | Use Case |
|------|------------|----------------|--------|-------------------|----------|
| `GA` | Battery | Lead-acid, Li-ion battery | `[AMB]` | 48 V DC battery bank for substation protection relay backup supply | Protection system independence from AC supply, uninterrupted relay operation |
| `GB` | Battery charger | Float charger, SMPS charger | `[IND]` | Float charger maintaining 48 V DC substation battery at full charge | Maintains battery state-of-charge, provides DC bus during AC presence |
| `GS` | Power supply (AC/DC) | SMPS, linear PSU | `[STD]` | 24 VDC / 5 A SMPS supplying PLC and I/O racks in control panel | Stable control voltage from raw AC supply |
| `GU` | UPS | UPS system | `[STD]` | Online double-conversion 3 kVA UPS for SCADA workstation and network switch in control room | Ride-through mains interruptions, clean power for sensitive equipment |

> **`GA` ambiguity note:** Batteries can logically be classified under `C` (stores energy) or `G` (generates/supplies energy) depending on perspective. IEC 81346-2 does not resolve this cleanly. Industry convention has settled on `GA` for the complete battery unit, but both designations appear in real documentation. Clarify in your project's design basis.

### H — Signalling / Indication

| Code | Description | Typical Device | Status | Real-Life Example | Use Case |
|------|------------|----------------|--------|-------------------|----------|
| `HA` | Acoustic alarm | Buzzer, horn, siren | `[STD]` | High-decibel horn on pump station panel for critical fault alarm | Audible notification of trip condition when no operator is present |
| `HL` | Indicator lamp | Pilot lamp, LED indicator | `[STD]` | Green RUN lamp and red FAULT lamp on MCC motor starter door | Visual status at a glance without opening panel |
| `HR` | Digital display / readout | Digital panel meter | `[IND]` | Digital panel meter showing motor current (0–100 A) on MCC door | Local current/voltage readout without SCADA access |

### K — Signal Processing / Switching

| Code | Description | Typical Device | Status | Real-Life Example | Use Case |
|------|------------|----------------|--------|-------------------|----------|
| `KA` | Auxiliary relay | General purpose relay | `[STD]` | 24 VDC auxiliary relay for PLC digital output isolation in control panel | Signal voltage conversion, contact multiplication for interlocks |
| `KC` | Contactor | Motor contactor | `[STD]` | Siemens 3RT 45 A contactor switching 22 kW pump motor in MCC | Frequent motor starting/stopping under automatic or SCADA control |
| `KM` | Main contactor | Main power contactor | `[IND]` | Main incoming contactor for bus-tie switching in paralleled switchboard | Main switching operation with auxiliary contact feedback to PLC |
| `KT` | Timer relay | On-delay, off-delay, star-delta timer | `[STD]` | Star-delta timer (5 s) on 37 kW pump motor starter to limit starting current | Reduced voltage starting, timed sequence operations |
| `KW` | Watchdog relay | PLC watchdog output relay | `[IND]` | Watchdog relay driven by PLC heartbeat signal — de-energises if PLC halts | Fail-safe detection of PLC software freeze or CPU fault |

### M — Mechanical Energy

| Code | Description | Typical Device | Status | Real-Life Example | Use Case |
|------|------------|----------------|--------|-------------------|----------|
| `MA` | Motor (asynchronous / AC induction) | AC induction motor | `[STD]` | 55 kW IE3 squirrel cage motor driving high-lift centrifugal pump at water treatment plant | Main process driver — coupled to pump, fan, or compressor |
| `MB` | Brake (motor-mounted) | Electro-mechanical brake | `[STD]` | Spring-applied electromagnetic brake on hoist motor in screenings handling equipment | Immediate stop on power loss, load holding for vertical loads |
| `MC` | Motor (DC) | DC motor | `[STD]` | DC motor on chemical dosing pump where precise speed control is required | Variable-speed applications, historically used before VFDs became dominant |
| `MS` | Servo / stepper motor | Servo / stepper motor | `[STD]` | Stepper motor on automated valve positioner in chemical dosing skid | Precise positional control, low-inertia actuation |

### N — Regulation / Control

| Code | Description | Typical Device | Status | Real-Life Example | Use Case |
|------|------------|----------------|--------|-------------------|----------|
| `NA` | VFD / frequency converter | Variable frequency drive | `[STD]` | ABB ACH580 VFD on 37 kW pump motor for pressure-based speed control | Energy saving, soft start, flow regulation without throttling valve |
| `NC` | PID controller | Standalone process controller | `[IND]` | Standalone PID controller for chlorine residual control loop | Closed-loop dosing, temperature, or pressure control |
| `NR` | Regulator | Voltage regulator, pressure regulator | `[IND]` | Automatic voltage regulator (AVR) on standby diesel generator | Generator terminal voltage stabilisation under varying load |

### P — Measurement / Testing

| Code | Description | Typical Device | Status | Real-Life Example | Use Case |
|------|------------|----------------|--------|-------------------|----------|
| `PA` | Ammeter | Current meter | `[STD]` | Analogue ammeter 0–60 A on MCC starter door showing motor running current | Local current monitoring, overload identification |
| `PB` | Power analyser | Power quality analyser (portable) | `[IND]` | Portable power analyser connected to 11 kV/0.4 kV transformer LV terminals during commissioning | Power quality survey, harmonic assessment, THD measurement |
| `PC` | Counter | Event counter, hour meter | `[STD]` | Hour-run meter on pump motor recording total operating hours for maintenance scheduling | Predictive maintenance trigger based on running hours |
| `PF` | Frequency meter | Hz meter | `[STD]` | Panel frequency meter on generator output to verify 50 Hz before synchronising | Generator synchronisation check, grid frequency monitoring |
| `PH` | Phase sequence / phase monitor relay | Phase monitor relay | `[IND]` | Phase sequence relay on pump MCC to prevent reverse rotation on rewired cable | Motor protection against phase reversal and phase loss |
| `PJ` | Energy meter (kWh) | kWh meter | `[AMB]` | MID-approved kWh meter on 11 kV feeder for energy billing at water treatment plant | Electricity cost allocation, ISO 50001 energy baseline monitoring |
| `PQ` | Power quality analyser (permanent) | PQ meter with harmonics | `[IND]` | Permanently installed PQ recorder on LV switchboard to log voltage sags and THD over time | Ongoing power quality monitoring, compliance with EN 50160 |
| `PV` | Voltmeter | Voltage panel meter | `[STD]` | Voltmeter 0–500 V (AC) on LV switchboard incomer to monitor supply voltage | Supply quality check, phase voltage imbalance detection |
| `PW` | Power meter | kW meter / power transducer | `[IND]` | kW transducer feeding 4–20 mA signal to PLC for real-time power monitoring of pump set | Energy efficiency KPI tracking, demand management |

> **`PJ` consistency note:** The second letter `J` for energy meter is widely used in plant documentation and supported by several national implementations, but it is not consistently defined across all national editions of IEC 81346-2. Some projects use `PA` with a qualifier note instead. Document your choice in the project design basis to ensure consistency across drawings.

### Q — Electrical Switching

| Code | Description | Typical Device | Status | Real-Life Example | Use Case |
|------|------------|----------------|--------|-------------------|----------|
| `QA` | Switch / disconnector (LV) | Load break switch, isolator | `[STD]` | 400 V load break switch as bus-section isolator in LV switchboard | Safe isolation for maintenance, bus-section switching |
| `QB` | Circuit breaker (HV) | Vacuum / SF6 circuit breaker | `[STD]` | 11 kV vacuum circuit breaker in ring main unit feeder to pump station transformer | MV fault interruption, remote switching via SCADA |
| `QD` | Disconnector / isolator (HV) | Air-break disconnector | `[STD]` | 33 kV air-break disconnector on main substation busbar for maintenance isolation | Safe de-energisation of MV/HV equipment, maintenance isolation point |
| `QE` | Earthing switch | Earth switch (MV/HV) | `[STD]` | Earthing switch on 11 kV cable bay to earth cable before cable jointing work | Safety earthing, maintenance personnel protection |
| `QF` | Circuit breaker (LV) | MCCB, MCB, ACB | `[STD]` | 250 A ACB as LV main incomer with shunt trip coil for SCADA-commanded tripping | Main LV supply protection, remote emergency tripping |
| `QM` | Motor circuit breaker | Combined contactor + breaker | `[IND]` | Moeller PKZM motor circuit breaker on small auxiliary pump (2.2 kW) | Space-saving protection for small motors without separate overload relay |
| `QS` | Load break switch | On-load switch | `[STD]` | 400 A load break switch on transformer secondary for no-break bus transfer | On-load switching without interrupting the load |

### R — Restriction / Stabilisation

| Code | Description | Typical Device | Status | Real-Life Example | Use Case |
|------|------------|----------------|--------|-------------------|----------|
| `RA` | Resistor | Fixed resistor | `[STD]` | Neutral earthing resistor (NER) limiting earth fault current to 400 A on 11 kV system | Earth fault current limitation, reducing step/touch voltages |
| `RB` | Braking resistor | Dynamic brake resistor | `[STD]` | Stainless steel braking resistor on VFD for rapid deceleration of fan motor | Fast stopping without mechanical brake, regenerative energy dissipation |
| `RL` | Inductor / reactor | Line reactor, choke | `[STD]` | 5% line reactor on VFD input to reduce harmonic current injection into LV network | Harmonic mitigation, VFD input protection, short-circuit limitation |
| `RR` | Variable resistor | Rheostat, potentiometer | `[STD]` | 10 kΩ potentiometer providing 0–10 V speed reference signal to VFD | Manual analogue setpoint adjustment |

### S — Manual Signal Conversion

| Code | Description | Typical Device | Status | Real-Life Example | Use Case |
|------|------------|----------------|--------|-------------------|----------|
| `SA` | Selector switch | Multi-position rotary switch | `[STD]` | 3-position rotary selector LOCAL / OFF / REMOTE on MCC door for each pump | Mode selection, hand-off-auto (HOA) control switching |
| `SB` | Push button | Momentary push button | `[STD]` | Green START / Red STOP illuminated push buttons on pump panel door | Manual pump start/stop, local operator control |
| `SK` | Key switch | Key-operated switch | `[IND]` | Key switch for enabling maintenance bypass of level protection interlock | Prevents unauthorised override of safety interlocks |
| `SL` | Limit switch (mechanical) | Mechanical limit switch | `[STD]` | Mechanical limit switch detecting fully open/closed position of sluice gate | Gate end-of-travel detection, SCADA status feedback |
| `SS` | Selector switch (maintained) | Mode selector, local/remote | `[IND]` | Maintained key-operated local/remote selector at pump station for SCADA lockout | Operator safety: prevents remote start while personnel working on pump |

### T — Electrical Quantity Conversion

| Code | Description | Typical Device | Status | Real-Life Example | Use Case |
|------|------------|----------------|--------|-------------------|----------|
| `TA` | Current transformer | Metering / protection CT | `[STD]` | 400/5 A Class 0.5 metering CT on 11 kV feeder for energy billing; 400/1 A Class 5P20 protection CT | Isolates instruments from HV, scales current to safe secondary level |
| `TC` | Thyristor / SCR / soft starter | Power thyristor, soft starter | `[IND]` | Thyristor-based soft starter on 90 kW pump motor limiting starting current to 350% | Reduced voltage starting without star-delta transition step |
| `TF` | Filter / isolation transformer | Isolation transformer | `[IND]` | 1:1 isolation transformer feeding sensitive analytical instruments in water quality lab | Galvanic isolation, safety separation, noise reduction for instruments |
| `TM` | Power transformer | Distribution transformer | `[STD]` | 11 kV / 0.4 kV, 1000 kVA ONAN distribution transformer supplying pump station LV switchboard | Voltage step-down for utilisation, fault level limitation |
| `TV` | Voltage transformer | Metering / protection VT/PT | `[STD]` | 11 kV / 110 V Class 0.5 metering VT on MV busbar for energy meter and voltmeter | Safely scales MV/HV voltage to instrument level (110 V) |
| `TY` | Rectifier / converter | AC/DC converter | `[IND]` | 3-phase rectifier unit converting 400 V AC to 220 V DC for substation DC control bus | DC control power supply, battery charger front-end |

### V — Process / Material Handling

| Code | Description | Typical Device | Status | Real-Life Example | Use Case |
|------|------------|----------------|--------|-------------------|----------|
| `VA` | Valve (process / flow) | Control valve, on/off valve | `[STD]` | DN150 pneumatic butterfly valve on pump discharge with positioner for flow control | Remote-operated isolation, throttle control, emergency shut-off |
| `VF` | Fan / ventilation | Cooling fan, ventilation fan | `[STD]` | Axial cooling fan in MCC switchroom forced ventilation system | Switchroom temperature control, transformer cooling |
| `VP` | Pump (process) | Process pump | `[IND]` | Vertical turbine pump in booster pump station; chemical dosing peristaltic pump | Water conveyance, chemical injection, pressure boosting |

### X — Connection / Termination

| Code | Description | Typical Device | Status | Real-Life Example | Use Case |
|------|------------|----------------|--------|-------------------|----------|
| `XB` | Busbar connection | Busbar connection point | `[STD]` | LV main busbar tapping point in distribution switchboard | Distribution circuit attachment, bus coupler junction |
| `XD` | Distribution terminal | DIN rail terminal block | `[STD]` | Phoenix Contact UTTB 2.5 terminal blocks on DIN rail for field wiring in junction box | Organised, safe termination of multi-core cables |
| `XP` | Plug / socket connector | Connector plug | `[STD]` | Harting Han connector on motor cable for maintenance disconnection | Quick connect/disconnect for portable equipment or routine maintenance |
| `XS` | Socket outlet | Socket outlet | `[STD]` | 16A IP67 industrial socket outlet in pump station for maintenance power tools | Maintenance power, test equipment supply |
| `XT` | Terminal block | Screw/spring terminal | `[STD]` | Weidmüller WDU 2.5 terminal blocks for CT/VT secondary wiring in metering panel | Field wiring interface, test point access, circuit separation |

### Y — Positioning / Actuation

| Code | Description | Typical Device | Status | Real-Life Example | Use Case |
|------|------------|----------------|--------|-------------------|----------|
| `YA` | Solenoid actuator | Solenoid coil | `[STD]` | 24 VDC solenoid coil piloting pneumatic actuator on process valve | PLC digital output → air-operated valve conversion |
| `YB` | Electromechanical brake | Spring-applied brake | `[STD]` | Spring-applied 24 VDC brake on vertical pump motor preventing reverse flow on shutdown | Anti-reverse on vertical pumps, load holding on conveyors |
| `YV` | Solenoid valve | Pneumatic / hydraulic solenoid valve | `[STD]` | 5/2-way solenoid valve controlling double-acting pneumatic actuator on butterfly valve | Pneumatic circuit control, actuator direction selection |

### Z — Industry Extensions (Non-Standard Primary Letter)

> **Important:** The letter `Z` is **not defined as a primary object-class letter in IEC 81346-1:2009**. The codes below originate from **NAMUR NE 21** and general instrument/safety engineering conventions. They are universally recognised in plant documentation for process industries, but their use represents a deliberate departure from the core standard. Document this in your project design basis if IEC 81346 conformance is formally required.

| Code | Description | Typical Device | Status | Real-Life Example | Use Case |
|------|------------|----------------|--------|-------------------|----------|
| `ZA` | Zener barrier (intrinsic safety) | Intrinsic safety barrier | `[EXT]` | MTL 787+ Zener barrier in Zone 1 instrument loop for pressure transmitter in explosive area | Limits energy entering hazardous area — IEC 60079 intrinsic safety compliance |
| `ZI` | Galvanic isolator | HART isolator, signal isolator | `[EXT]` | Phoenix MINI MCR-2 galvanic isolator converting 4–20 mA loop to isolated 4–20 mA for PLC AI card | Ground loop breaking, signal isolation, impedance matching between instruments and PLC |
| `ZF` | EMC filter | Line filter, EMC filter | `[EXT]` | Schaffner FN 3258 EMC filter on VFD power input to comply with EN 61800-3 Category C2 | Conducted EMI suppression, VFD compliance with EMC directive |

---

## Verification Summary

The following table consolidates all verification flags in one place for easy reference.

| Code | Issue | Recommendation |
|------|-------|----------------|
| `GA` | Ambiguous classification — battery fits both `C` (stores energy) and `G` (generates/supplies). IEC 81346-2 does not resolve cleanly. | Use `GA` by convention for the complete battery unit; document the choice in your design basis. |
| `PJ` | Second letter `J` for energy meter is not consistently defined across national implementations of IEC 81346-2. | Use `PJ` if your national/project standard endorses it; alternatively use `PA` with a qualifier note. Document the decision. |
| `ZA`, `ZI`, `ZF` | `Z` is not a primary letter in IEC 81346-1:2009. These codes originate from NAMUR NE 21 and are industry extensions. | Acceptable for use in practice — they are universally understood. State in the design basis that these are NAMUR extensions adopted by project convention. |
| `FU` | Second letter `U` for HV fuse is not explicitly in IEC 81346-2; it is an established industry convention. | Acceptable; widely understood in HV switchgear documentation. |

---

## Quick Reference — Status Codes

- **`[STD]`** — Defined in IEC 81346-2:2019. Fully conformant.  
- **`[IND]`** — Not explicitly in the standard, but universally established industry practice with no ambiguity.  
- **`[EXT]`** — External extension from NAMUR NE 21 or another industry body. Departs from core IEC 81346.  
- **`[AMB]`** — Ambiguous or nationally inconsistent. Document the project-specific interpretation.

---

*Reference compiled from IEC 81346-1:2009, IEC 81346-2:2019, NAMUR NE 21, and industry documentation practice.*  
*Real-life examples are drawn from water utility (pump stations, treatment plants, MV/LV substation), SCADA, and electrical power engineering contexts.*