---

title: "EPLAN PLC, SCADA, DCS, IT & Server Panel Designation Reference Guide"

description: >-
  A comprehensive reference guide to the standard report and form structure of an EPLAN Electric P8 project, including form types, purposes, examples, and applicable standards.

date: 2024-03-10 10:00:00 +0800
author: Mahmoud Lotfi
file_name: 2024-03-10-eplan-plc-scada-dcs-it-server-panel-designation-reference-1.md
categories: [EPLAN, PLC, SCADA, DCS, IT, Server, Panel, Designation, Reference]
tags: [Eplan, PLC, SCADA, DCS, IT, Server, Panel, designation, reference]
pin: False
math: true
mermaid: true
comments: true
toc: true
render_with_liquid: false

image:
  path: /assets/img/posts/eplan.jpg
  alt: EPLAN PLC, SCADA, DCS, IT & Server Panel Designation Reference Guide
  lqip: data:image/webp;base64,UklGRjoAAABXRUJQVlA4IC4AAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
---

# EPLAN P8 — PLC, SCADA, DCS, IT & Server Panel Designation Reference Guide
> Specialized for: PLC Panels | SCADA Systems | DCS Cabinets | Safety Controllers (SIS/ESD) | RTU Panels | Marshalling Cabinets | Server Racks | Network Cabinets | Comms Panels | Historian Servers | HMI Stations | Engineering Workstations | Patch Panels | KVM Systems

---

## Table of Contents
1. [Fundamentals](#fundamentals)
2. [Naming Philosophy for Automation & IT](#naming-philosophy-for-automation--it)
3. [PLC Panel — Small (Standalone Machine / Process)](#plc-panel--small-standalone-machine--process)
4. [PLC Panel — Medium (Multi-Rack / Remote I/O)](#plc-panel--medium-multi-rack--remote-io)
5. [PLC Panel — Large (Redundant CPU / High Availability)](#plc-panel--large-redundant-cpu--high-availability)
6. [Remote I/O Cabinets & Field Panels](#remote-io-cabinets--field-panels)
7. [Safety PLC / Safety Controller (SIS / ESD)](#safety-plc--safety-controller-sis--esd)
8. [DCS — Distributed Control System](#dcs--distributed-control-system)
9. [SCADA System Panels](#scada-system-panels)
10. [RTU — Remote Terminal Unit Panels](#rtu--remote-terminal-unit-panels)
11. [Marshalling Cabinets (Automation-Focused)](#marshalling-cabinets-automation-focused)
12. [Instrumentation Cabinets (Loop-Powered)](#instrumentation-cabinets-loop-powered)
13. [HMI Stations & Operator Consoles](#hmi-stations--operator-consoles)
14. [Engineering Workstation Panels](#engineering-workstation-panels)
15. [Historian & Application Server Racks](#historian--application-server-racks)
16. [Network Infrastructure Cabinets](#network-infrastructure-cabinets)
17. [Industrial Network Cabinets (OT Network)](#industrial-network-cabinets-ot-network)
18. [IT / Corporate Network Racks (IT Network)](#it--corporate-network-racks-it-network)
19. [Server Racks & Blade Centres](#server-racks--blade-centres)
20. [Storage & Backup Systems](#storage--backup-systems)
21. [KVM & Console Access Systems](#kvm--console-access-systems)
22. [Patch Panels & Structured Cabling](#patch-panels--structured-cabling)
23. [UPS for Control & IT Systems](#ups-for-control--it-systems)
24. [PDU — Power Distribution Units (Rack Level)](#pdu--power-distribution-units-rack-level)
25. [Fibre Optic Distribution Panels](#fibre-optic-distribution-panels)
26. [Communications & Telecom Panels](#communications--telecom-panels)
27. [Cybersecurity & Demilitarized Zone (DMZ) Equipment](#cybersecurity--demilitarized-zone-dmz-equipment)
28. [Time Synchronisation (GPS / NTP)](#time-synchronisation-gps--ntp)
29. [Control Room Layout — Full Example](#control-room-layout--full-example)
30. [DCS Control System — Full Example](#dcs-control-system--full-example)
31. [SCADA / RTU Network — Full Example](#scada--rtu-network--full-example)
32. [IT / OT Convergence Architecture](#it--ot-convergence-architecture)
33. [Common Device Tags Reference](#common-device-tags-reference)
34. [Common Mistakes](#common-mistakes)
35. [Expert Tips](#expert-tips)

---

## Fundamentals

### EPLAN Structure Reminder
```
=   Function designation     → WHAT the panel / system does
+   Location designation     → WHERE the panel / cabinet physically is
-   Device designation       → WHAT the component is
```

### The Automation & IT Engineer's Primary Concern
Unlike power panels where function = electrical role, in automation and IT:
- `=` reflects the **system layer** (PLC, SCADA, DCS, network, safety)
- `+` reflects the **physical cabinet, rack, or room**
- `-` reflects the **specific module, card, server, or device**

### Full Tag Syntax Example
```
=CTRL.PLC+CTRL_RM.CAB1-CPU01          PLC CPU in cabinet 1, control room
=SCADA.SERVER+SERVER_RM.RACK_A-SRV1   SCADA server in rack A, server room
=DCS.IO+FLD_CAB_A1-AI01               DCS AI module in field cabinet A1
=SIS.LOGIC+SAFE_RM.SIS_CAB1-CPU_S1    SIS logic solver in safety cabinet 1
=NETW.OT+CTRL_RM.NET_CAB-SW_PN1       PROFINET switch in network cabinet
```

---

## Naming Philosophy for Automation & IT

### System Layer Convention (Function `=`)
```
=CTRL          General control system
=CTRL.PLC      PLC layer
=CTRL.IO       I/O layer
=CTRL.HMI      HMI / operator interface layer
=CTRL.COMM     Communications layer
=CTRL.SAFE     Integrated safety (within PLC)
=DCS           Distributed control system
=DCS.CTRL      DCS controller layer
=DCS.IO        DCS I/O layer
=DCS.HMI       DCS operator station
=SCADA         SCADA system
=SCADA.SERVER  SCADA server layer
=SCADA.HMI     SCADA client / HMI layer
=SCADA.COMM    SCADA communications layer
=SIS           Safety instrumented system
=SIS.LOGIC     SIS logic solver layer
=SIS.IO        SIS I/O layer
=ESD           Emergency shutdown system
=RTU           Remote terminal unit
=HIST          Historian system
=MES           Manufacturing execution system
=NETW          Network infrastructure
=NETW.OT       OT / industrial network
=NETW.IT       IT / corporate network
=NETW.DMZ      Demilitarised zone
=NETW.SAFE     Safety network (black channel)
=SERVER        Server infrastructure
=STORAGE       Storage / backup
=COMMS         Communications and telecom
=TIME          Time synchronisation
=KVM           KVM / console access
=PATCH         Structured cabling / patch
=FIBER         Fibre optic distribution
=CYBER         Cybersecurity infrastructure
=PWR.CTRL      Control power distribution
=PWR.24V       24VDC control power
=PWR.UPS       UPS-backed supply
=PWR.IT        IT power (230VAC clean)
```

### Physical Cabinet Convention (Location `+`)
```
+CTRL_RM                   Control room (room level)
+CTRL_RM.CAB1              PLC/control cabinet 1 in control room
+CTRL_RM.CAB2              PLC/control cabinet 2
+CTRL_RM.HMI_CAB           HMI server cabinet
+CTRL_RM.NET_CAB           Network cabinet
+CTRL_RM.UPS_CAB           UPS cabinet
+SERVER_RM                 Server room (room level)
+SERVER_RM.RACK_A          Server rack A
+SERVER_RM.RACK_B          Server rack B
+SERVER_RM.NET_RACK        Network rack
+SAFE_RM                   Safety equipment room
+SAFE_RM.SIS_CAB1          SIS cabinet 1
+FIELD                     Field (no enclosure)
+FLD_CAB_A1                Field remote I/O cabinet A1
```

---

## PLC Panel — Small (Standalone Machine / Process)

> Typical: single rack, compact PLC, up to ~256 I/O points
> Brands: Siemens S7-1200/1500, Allen-Bradley CompactLogix, Schneider M241/M340, Beckhoff CX series, Omron NX1P

### Function Designations
```
=CTRL                    Overall control function
=CTRL.PLC                PLC CPU and rack
=CTRL.IO                 I/O modules
=CTRL.HMI                HMI interface
=CTRL.COMM               Communications modules
=CTRL.SAFE               Safety modules (if integrated)
=PWR.CTRL                Control panel power
=PWR.24V                 24VDC control power rail
=PWR.UPS                 UPS buffer module
=SAFE                    Safety function (if separate)
=SAFE.ESTOP              Emergency stop function
=SAFE.GUARD              Guard monitoring function
```

### Location Designations
```
+CP1                     Control panel 1 (the enclosure)
+CP1.POWER               Power supply section (top DIN rail)
+CP1.PLC                 PLC rack / mounting area
+CP1.IO                  I/O module expansion area
+CP1.SAFE                Safety relay / safety module section
+CP1.RELAY               Auxiliary relay section
+CP1.BARRIER             Zener barrier / galvanic isolator section
+CP1.DIST_24V            24VDC distribution (DIN rail fuse terminal blocks)
+CP1.COMM                Communications modules section
+CP1.TERM                Terminal section (field wiring)
+CP1.TERM.DI             Digital input terminals
+CP1.TERM.DO             Digital output terminals
+CP1.TERM.AI             Analog input terminals (4-20mA / 0-10V)
+CP1.TERM.AO             Analog output terminals
+CP1.TERM.RTD            RTD / thermocouple input terminals
+CP1.TERM.SAFE           Safety I/O terminal section
+CP1.TERM.COMM           Communications terminals (RS485, etc.)
+CP1.TERM.POWER          Power terminal section (mains in, 24VDC out)
+CP1.DOOR                Door-mounted devices
+CP1.DOOR.HMI            HMI touchscreen (door mounted)
+CP1.DOOR.OP             Operator buttons, lamps, selectors (door)
+CP1.DOOR.USB            USB / memory card access port
```

### Full Tag Examples — Small PLC Panel
```
--- Power Supply Section ---
=PWR.CTRL+CP1.POWER-QF_MAINS          230VAC incoming MCB
=PWR.CTRL+CP1.POWER-QF_CTRL           Control circuits MCB
=PWR.CTRL+CP1.POWER-T1                Control transformer (if 230V→24VAC)
=PWR.24V+CP1.POWER-PS1                24VDC SMPS (e.g. SITOP, Phoenix QUINT)
=PWR.24V+CP1.POWER-PS2                24VDC SMPS redundant module
=PWR.UPS+CP1.POWER-UPS_BUF1           24VDC UPS buffer module (e.g. SITOP UPS1600)
=PWR.24V+CP1.DIST_24V-FT1             24VDC fuse terminal block — PLC supply
=PWR.24V+CP1.DIST_24V-FT2             24VDC fuse terminal block — I/O supply
=PWR.24V+CP1.DIST_24V-FT3             24VDC fuse terminal block — field sensors
=PWR.24V+CP1.DIST_24V-FT4             24VDC fuse terminal block — solenoids/outputs
=PWR.24V+CP1.DIST_24V-FT5             24VDC fuse terminal block — HMI supply
=PWR.24V+CP1.DIST_24V-FT6             24VDC fuse terminal block — safety system

--- PLC Rack ---
=CTRL.PLC+CP1.PLC-CPU1                PLC CPU module (e.g. S7-1515, L30ER)
=CTRL.PLC+CP1.PLC-PM1                 PLC power module (system power)
=CTRL.PLC+CP1.PLC-IM1                 Interface module (if expansion rack)

--- I/O Modules ---
=CTRL.IO+CP1.IO-DI01                  Digital input module 01 (e.g. 16DI 24VDC)
=CTRL.IO+CP1.IO-DI02                  Digital input module 02
=CTRL.IO+CP1.IO-DO01                  Digital output module 01 (e.g. 16DO 24VDC)
=CTRL.IO+CP1.IO-DO02                  Digital output module 02
=CTRL.IO+CP1.IO-AI01                  Analog input module 01 (e.g. 8AI 4-20mA)
=CTRL.IO+CP1.IO-AI02                  Analog input module 02
=CTRL.IO+CP1.IO-AO01                  Analog output module 01
=CTRL.IO+CP1.IO-RTD01                 RTD / thermocouple input module 01
=CTRL.IO+CP1.IO-CNT01                 Counter / encoder input module 01

--- Communications ---
=CTRL.COMM+CP1.COMM-CM_PN1            PROFINET communications module
=CTRL.COMM+CP1.COMM-CM_PB1            PROFIBUS DP master module
=CTRL.COMM+CP1.COMM-CM_RS485          RS485 / Modbus RTU module
=CTRL.COMM+CP1.COMM-CM_ETH1           Ethernet module / port
=CTRL.COMM+CP1.COMM-CM_IOLINK1        IO-Link master module
=CTRL.COMM+CP1.COMM-CM_ASI1           AS-Interface master module
=CTRL.COMM+CP1.COMM-SW_PN1            PROFINET managed switch (in cabinet)

--- Safety ---
=CTRL.SAFE+CP1.SAFE-F3_ESTOP          Safety relay — E-stop (e.g. PILZ PNOZ, Siemens 3SK)
=CTRL.SAFE+CP1.SAFE-F3_GUARD          Safety relay — guard door monitoring
=CTRL.SAFE+CP1.SAFE-F3_LIGHT          Safety relay — light curtain
=CTRL.SAFE+CP1.SAFE-F3_TWO_HAND       Safety relay — two-hand control
=CTRL.SAFE+CP1.SAFE-F_SAFE_PLC        Safety PLC module (e.g. S7-1500F CPU, GuardLogix)
=CTRL.SAFE+CP1.SAFE-DI_SAFE1          Safety digital input module
=CTRL.SAFE+CP1.SAFE-DO_SAFE1          Safety digital output module

--- Auxiliary Relays ---
=CTRL+CP1.RELAY-K1                    Auxiliary relay 1 (signal amplification / isolation)
=CTRL+CP1.RELAY-K2                    Auxiliary relay 2
=CTRL+CP1.RELAY-K3                    Auxiliary relay 3
=CTRL+CP1.RELAY-K_WD                  Watchdog relay (PLC healthy output)
=CTRL+CP1.RELAY-K_FAULT               General fault relay (common alarm)

--- Door Devices ---
=CTRL.HMI+CP1.DOOR.HMI-TP1           HMI touchpanel (e.g. Siemens KTP700, Allen-Bradley PV Plus)
=CTRL+CP1.DOOR.OP-SS_MODE             Mode selector (Auto/Manual/Maintenance)
=CTRL+CP1.DOOR.OP-SS_LOCAL            Local/Remote selector
=CTRL+CP1.DOOR.OP-SB_RESET            Fault reset push button
=CTRL+CP1.DOOR.OP-SB_ACK              Alarm acknowledge push button
=CTRL+CP1.DOOR.OP-HL_POWER           Power on indicator (green)
=CTRL+CP1.DOOR.OP-HL_RUN             System running indicator (green)
=CTRL+CP1.DOOR.OP-HL_FAULT           System fault indicator (red)
=CTRL+CP1.DOOR.OP-HL_WARN            Warning indicator (amber)
=CTRL+CP1.DOOR.OP-HL_COMM           Communications fault indicator
=SAFE.ESTOP+CP1.DOOR.OP-SB_ESTOP     Emergency stop mushroom head button
=CTRL+CP1.DOOR.USB-USB1              USB port (for program transfer / HMI update)
```

---

## PLC Panel — Medium (Multi-Rack / Remote I/O)

> Typical: main rack + 1-4 expansion racks or remote I/O drops, 256–2048 I/O points
> Brands: Siemens S7-1500 / ET200, Allen-Bradley ControlLogix + Flex/Point I/O, Schneider M580 + STB/EIO

### Location Designations — Multi-Rack
```
+CP1                     Main PLC cabinet
+CP1.MAIN_RACK           Main CPU rack section
+CP1.EXP_RACK1           Expansion rack 1 section (within same cabinet)
+CP1.EXP_RACK2           Expansion rack 2 section
+CP1.POWER               Power supply section
+CP1.DIST_24V            24VDC distribution section
+CP1.COMM                Communications section
+CP1.SAFE                Safety section
+CP1.RELAY               Auxiliary relay section
+CP1.TERM                Terminal section

+FLD_CAB_A1              Remote I/O cabinet A1 (field location)
+FLD_CAB_A1.PWR          Power supply section
+FLD_CAB_A1.IO_RACK      Remote I/O rack / modules
+FLD_CAB_A1.SAFE         Safety I/O section (if SIL-rated)
+FLD_CAB_A1.TERM         Terminal section (field wiring)
+FLD_CAB_A1.COMM         Comms / network section (switch, fibre converter)

+FLD_CAB_A2              Remote I/O cabinet A2
+FLD_CAB_A2.PWR          Power supply section
+FLD_CAB_A2.IO_RACK      Remote I/O rack
+FLD_CAB_A2.TERM         Terminal section

+FLD_CAB_B1              Remote I/O cabinet B1 (different area)
+FLD_CAB_C1              Remote I/O cabinet C1 (different area)
```

### Full Tag Examples — Remote I/O Drop
```
=PWR.24V+FLD_CAB_A1.PWR-PS1           Remote I/O 24VDC power supply
=PWR.24V+FLD_CAB_A1.PWR-PS2           Remote I/O 24VDC redundant supply
=PWR.24V+FLD_CAB_A1.PWR-FT1           Fused terminal block — I/O modules
=PWR.24V+FLD_CAB_A1.PWR-FT2           Fused terminal block — field sensors
=CTRL.IO+FLD_CAB_A1.IO_RACK-IM1       Interface / coupling module (ET200 IM, FlexBus)
=CTRL.IO+FLD_CAB_A1.IO_RACK-DI01      DI module 01
=CTRL.IO+FLD_CAB_A1.IO_RACK-DI02      DI module 02
=CTRL.IO+FLD_CAB_A1.IO_RACK-DO01      DO module 01
=CTRL.IO+FLD_CAB_A1.IO_RACK-AI01      AI module 01
=CTRL.IO+FLD_CAB_A1.IO_RACK-AO01      AO module 01
=CTRL.IO+FLD_CAB_A1.IO_RACK-RTD01     RTD module 01
=CTRL.COMM+FLD_CAB_A1.COMM-SW_PN1     PROFINET switch (managed, DIN rail)
=CTRL.COMM+FLD_CAB_A1.COMM-FC_FIBER1  Fibre optic / media converter
=CTRL.COMM+FLD_CAB_A1.TERM-X_PN       PROFINET patch connection terminals
=CTRL.SAFE+FLD_CAB_A1.SAFE-DI_S1      Safety DI module
=CTRL.SAFE+FLD_CAB_A1.SAFE-DO_S1      Safety DO module
=HEAT+FLD_CAB_A1.PWR-HTR1             Cabinet anti-condensation heater
=CTRL+FLD_CAB_A1.PWR-THERM1           Cabinet thermostat
```

---

## PLC Panel — Large (Redundant CPU / High Availability)

> Typical: redundant CPU pair, redundant power supplies, redundant I/O, redundant comms
> Brands: Siemens S7-400H / S7-1500H, Allen-Bradley ControlLogix SIL2/Redundancy, Schneider M580 Hot Standby, ABB AC500-S

### Location Designations — Redundant PLC
```
+CP1                     Main PLC cabinet (CPU A side)
+CP1.CPU_A               CPU A rack section
+CP1.CPU_A.RACK          CPU A physical rack
+CP1.CPU_A.PWR           CPU A power supply
+CP1.CPU_B               CPU B rack section (redundant partner)
+CP1.CPU_B.RACK          CPU B physical rack
+CP1.CPU_B.PWR           CPU B power supply
+CP1.SYNC                Synchronisation module section (CPU A–B link)
+CP1.IO_A                I/O rack A (primary)
+CP1.IO_B                I/O rack B (redundant — same signals, parallel)
+CP1.COMM_A              Communications rack A
+CP1.COMM_B              Communications rack B
+CP1.PWR_MAIN            Main cabinet power supply section
+CP1.DIST_24V_A          24VDC distribution rail A
+CP1.DIST_24V_B          24VDC distribution rail B (redundant)
+CP1.SAFE                Safety section
+CP1.TERM                Terminal section

+CP2                     Secondary PLC cabinet (I/O expansion)
+CP2.IO_RACK1            I/O rack 1
+CP2.IO_RACK2            I/O rack 2
+CP2.PWR                 Power supply
+CP2.TERM                Terminal section
```

### Full Tag Examples — Redundant PLC
```
=CTRL.PLC+CP1.CPU_A.RACK-CPU_A        PLC CPU module A (primary)
=CTRL.PLC+CP1.CPU_B.RACK-CPU_B        PLC CPU module B (standby)
=CTRL.PLC+CP1.SYNC-SYNC_MOD           Sync / redundancy module (CPU A–B link)
=CTRL.PLC+CP1.CPU_A.PWR-PM_A          Power module CPU A side
=CTRL.PLC+CP1.CPU_B.PWR-PM_B          Power module CPU B side
=CTRL.IO+CP1.IO_A-DI01_A              DI module 01 side A
=CTRL.IO+CP1.IO_B-DI01_B              DI module 01 side B (redundant)
=CTRL.COMM+CP1.COMM_A-CM_PN_A         PROFINET module A
=CTRL.COMM+CP1.COMM_B-CM_PN_B         PROFINET module B (redundant)
=PWR.24V+CP1.DIST_24V_A-PS_A          24VDC power supply A
=PWR.24V+CP1.DIST_24V_B-PS_B          24VDC power supply B
=CTRL.PLC+CP1.CPU_A.RACK-IM_A         Interface module rack A (for expansion)
```

---

## Remote I/O Cabinets & Field Panels

> Distributed around the plant, connected back to main PLC via PROFINET / EtherNet/IP / PROFIBUS / Modbus TCP

### Location Designations — Field Panel Types
```
+RIO_CAB_01               Remote I/O cabinet 01 (process area 1)
+RIO_CAB_02               Remote I/O cabinet 02 (process area 2)
+RIO_CAB_03               Remote I/O cabinet 03 (process area 3)

+JB_CTRL_A1               Control junction box area A, box 1
+JB_CTRL_A2               Control junction box area A, box 2
+JB_CTRL_B1               Control junction box area B, box 1

+IOLINK_BOX_01            IO-Link master box 01 (near sensors)
+IOLINK_BOX_02            IO-Link master box 02

+ASI_BOX_01               AS-Interface junction box 01
+DP_BOX_01                PROFIBUS DP junction box 01 (Y-coupler area)

+EX_RIO_01                Ex-rated remote I/O cabinet 01 (hazardous area Zone 2)
+EX_RIO_02                Ex-rated remote I/O cabinet 02
```

### Location Sub-Structure for Field Cabinet
```
+RIO_CAB_01               Remote I/O cabinet 01
+RIO_CAB_01.PWR           Power supplies
+RIO_CAB_01.RACK          I/O rack modules
+RIO_CAB_01.SAFE          Safety I/O (if SIL-rated field cabinet)
+RIO_CAB_01.BARRIER       Zener barriers / galvanic isolators (Ex area)
+RIO_CAB_01.RELAY         Output relay modules (if high current)
+RIO_CAB_01.COMM          Communications / network section
+RIO_CAB_01.TERM.DI       Digital input field terminals
+RIO_CAB_01.TERM.DO       Digital output field terminals
+RIO_CAB_01.TERM.AI       Analog input field terminals
+RIO_CAB_01.TERM.AO       Analog output field terminals
+RIO_CAB_01.TERM.PWR      Power supply field terminals
+RIO_CAB_01.TERM.EARTH    Earth / screen terminals
```

---

## Safety PLC / Safety Controller (SIS / ESD)

> Standards: IEC 61508, IEC 61511
> Brands: HIMA HIMax/HIMatrix, Triconex Tricon/Trident, Pilz PSS 4000, Siemens S7-1500 FSC, Rockwell GuardLogix, ABB AC500-S

### Function Designations — Safety System
```
=SIS               Safety instrumented system (overall)
=SIS.LOGIC         Logic solver function
=SIS.IO            Safety I/O function
=SIS.COMM          Safety communications function
=SIS.POWER         Safety system power function
=ESD               Emergency shutdown system
=ESD.L1            ESD Level 1 — process shutdown
=ESD.L2            ESD Level 2 — emergency shutdown
=ESD.L3            ESD Level 3 — abandon platform (offshore)
=F&G               Fire and gas system
=F&G.DET           Detection function
=F&G.CTRL          F&G control logic function
=SAFE.ESTOP        Emergency stop function
=SAFE.GUARD        Guard / access interlock function
=BPCS              Basic process control system (interface to SIS)
```

### Location Designations — SIS Cabinet
```
+SIS_CAB1                    SIS cabinet 1 (main logic solver)
+SIS_CAB1.LOGIC_A            Logic solver A (CPU / main module)
+SIS_CAB1.LOGIC_B            Logic solver B (redundant)
+SIS_CAB1.LOGIC_C            Logic solver C (triple modular redundancy — TMR)
+SIS_CAB1.IO_A               Safety I/O rack A
+SIS_CAB1.IO_B               Safety I/O rack B (redundant I/O)
+SIS_CAB1.POWER_A            Safety system power supply A
+SIS_CAB1.POWER_B            Safety system power supply B
+SIS_CAB1.COMM               Safety communications section
+SIS_CAB1.TERM               Safety terminal section
+SIS_CAB1.TERM.SIS_DI        Safety DI terminals (SIL-rated sensors)
+SIS_CAB1.TERM.SIS_DO        Safety DO terminals (final elements — SDV, ESD valves)
+SIS_CAB1.TERM.VOTING        Voting / comparison terminals (2oo3 wiring)
+SIS_CAB1.TERM.BPCS_IFX      BPCS interface terminals (read-only hardwired)

+SIS_CAB2                    SIS cabinet 2 (additional I/O)
+SIS_CAB2.IO_RACK1           I/O rack 1
+SIS_CAB2.IO_RACK2           I/O rack 2
+SIS_CAB2.POWER              Power supply
+SIS_CAB2.TERM               Terminal section

+ESD_CAB1                    ESD relay cabinet (hardwired ESD)
+ESD_CAB1.RELAY              ESD relay section
+ESD_CAB1.POWER              ESD power supply
+ESD_CAB1.TERM               ESD terminal section

+F_G_CAB1                    Fire and gas controller cabinet
+F_G_CAB1.CTRL               F&G controller section
+F_G_CAB1.IO                 F&G I/O modules
+F_G_CAB1.POWER              F&G power supply
+F_G_CAB1.TERM               F&G terminal section
```

### Full Tag Examples — SIS
```
=SIS.LOGIC+SIS_CAB1.LOGIC_A-CPU_S_A      SIS logic solver CPU A (e.g. HIMA F3 CPU)
=SIS.LOGIC+SIS_CAB1.LOGIC_B-CPU_S_B      SIS logic solver CPU B (redundant)
=SIS.LOGIC+SIS_CAB1.LOGIC_C-CPU_S_C      SIS logic solver CPU C (TMR third)
=SIS.IO+SIS_CAB1.IO_A-DI_S01_A           Safety DI module 01 side A
=SIS.IO+SIS_CAB1.IO_B-DI_S01_B           Safety DI module 01 side B
=SIS.IO+SIS_CAB1.IO_A-DO_S01_A           Safety DO module 01 side A
=SIS.POWER+SIS_CAB1.POWER_A-PS_S_A       Safety 24VDC supply A (isolated)
=SIS.POWER+SIS_CAB1.POWER_B-PS_S_B       Safety 24VDC supply B (isolated)
=SIS.COMM+SIS_CAB1.COMM-CM_SIS_PN        SIS PROFINET / Modbus comm module
=SIS.COMM+SIS_CAB1.COMM-CM_BPCS_IFX     BPCS hardwired interface module
=ESD.L1+ESD_CAB1.RELAY-K_L1_01          ESD Level 1 relay 01
=ESD.L2+ESD_CAB1.RELAY-K_L2_01          ESD Level 2 relay 01
=F&G.CTRL+F_G_CAB1.CTRL-FG_CTRL1         F&G controller (e.g. Hochiki, Notifier ONYX)
=F&G.DET+F_G_CAB1.IO-DI_FG01            F&G detection input module
```

---

## DCS — Distributed Control System

> Brands: Honeywell Experion PKS, ABB 800xA / System 500, Emerson DeltaV, Yokogawa CENTUM VP, Siemens PCS 7, Rockwell PlantPAx

### Function Designations — DCS
```
=DCS               DCS overall system
=DCS.CTRL          DCS controller layer
=DCS.IO            DCS I/O layer
=DCS.FCS           Field control station function
=DCS.IOP           I/O processor function
=DCS.COMM          DCS communications / control network
=DCS.HMI           DCS operator station function
=DCS.ENG           DCS engineering station function
=DCS.HIST          DCS integrated historian
=DCS.OPC           OPC server / gateway function
=DCS.REDUND        Redundancy function
=DCS.POWER         DCS system power function
=DCS.SAFE          DCS safety layer (if integrated)
```

### Location Designations — DCS Cabinets
```
+DCS_CAB1                    DCS cabinet 1 (main controller)
+DCS_CAB1.FCS_A              Field control station A (main CPU / controller)
+DCS_CAB1.FCS_B              Field control station B (redundant CPU)
+DCS_CAB1.IO_RACK_A          I/O rack A (primary I/O modules)
+DCS_CAB1.IO_RACK_B          I/O rack B (redundant I/O)
+DCS_CAB1.IOP1               I/O processor 1
+DCS_CAB1.IOP2               I/O processor 2
+DCS_CAB1.POWER_A            DCS power supply A
+DCS_CAB1.POWER_B            DCS power supply B (redundant)
+DCS_CAB1.COMM               DCS control network section
+DCS_CAB1.COMM.CNT_A         Control network interface A
+DCS_CAB1.COMM.CNT_B         Control network interface B (redundant)
+DCS_CAB1.TERM               Terminal section

+DCS_CAB2                    DCS cabinet 2 (additional I/O)
+DCS_CAB2.IO_RACK_1          I/O rack 1
+DCS_CAB2.IO_RACK_2          I/O rack 2
+DCS_CAB2.IO_RACK_3          I/O rack 3
+DCS_CAB2.POWER              Power supply section
+DCS_CAB2.TERM               Terminal section

+DCS_CAB3                    DCS cabinet 3 (safety / SIS — if integrated)
+DCS_CAB3.SIS_IO             SIS I/O modules
+DCS_CAB3.POWER              Safety power supply
+DCS_CAB3.TERM               Safety terminal section

+DCS_SERVER_CAB              DCS server cabinet
+DCS_SERVER_CAB.APP_SRV      Application server / history server
+DCS_SERVER_CAB.OPC_SRV      OPC DA/UA server
+DCS_SERVER_CAB.PRINT_SRV    Print server
+DCS_SERVER_CAB.NET_SW       Control network managed switch
+DCS_SERVER_CAB.UPS          Cabinet UPS / power conditioner
```

### Full Tag Examples — DCS
```
=DCS.FCS+DCS_CAB1.FCS_A-FCS_A1           DCS field control station A (e.g. DeltaV M-series)
=DCS.FCS+DCS_CAB1.FCS_B-FCS_B1           DCS FCS B (redundant)
=DCS.IO+DCS_CAB1.IO_RACK_A-AI_01A        DCS AI module 01 side A (8-ch 4-20mA HART)
=DCS.IO+DCS_CAB1.IO_RACK_B-AI_01B        DCS AI module 01 side B (redundant)
=DCS.IO+DCS_CAB1.IO_RACK_A-AO_01A        DCS AO module 01 side A
=DCS.IO+DCS_CAB1.IO_RACK_A-DI_01         DCS DI module 01
=DCS.IO+DCS_CAB1.IO_RACK_A-DO_01         DCS DO module 01
=DCS.IO+DCS_CAB1.IO_RACK_A-HART_MUX1     HART multiplexer module
=DCS.IO+DCS_CAB1.IO_RACK_A-FF_01         Foundation Fieldbus H1 card
=DCS.POWER+DCS_CAB1.POWER_A-PS_DCS_A     DCS power supply A (24VDC, isolated)
=DCS.POWER+DCS_CAB1.POWER_B-PS_DCS_B     DCS power supply B
=DCS.COMM+DCS_CAB1.COMM.CNT_A-NIC_CNT_A  Control network NIC A
=DCS.COMM+DCS_CAB1.COMM.CNT_B-NIC_CNT_B  Control network NIC B
=DCS.HIST+DCS_SERVER_CAB.APP_SRV-SRV_HIST DCS historian / application server
=DCS.OPC+DCS_SERVER_CAB.OPC_SRV-SRV_OPC  OPC DA/UA server
=DCS.COMM+DCS_SERVER_CAB.NET_SW-SW_CNT1   Control network switch
```

---

## SCADA System Panels

> Typical SCADA stack: RTUs in field → comms network → SCADA server → HMI clients

### Function Designations — SCADA
```
=SCADA                   SCADA system overall
=SCADA.SERVER            SCADA server function
=SCADA.HMI               SCADA HMI client function
=SCADA.HIST              SCADA historian function
=SCADA.ENG               Engineering / development workstation
=SCADA.OPC               OPC server / gateway function
=SCADA.COMM              SCADA WAN / LAN communications
=SCADA.FRONT_END         SCADA front-end processor / data concentrator
=SCADA.RTU_IFX           RTU interface gateway function
=SCADA.ALARM             Alarm management system function
=SCADA.REPORT            Report server function
=SCADA.DR                Disaster recovery system function
=SCADA.WEB               Web client / thin client function
```

### Location Designations — SCADA Panels
```
+CTRL_RM                       Control room (room level)
+CTRL_RM.SCADA_CAB1            SCADA primary server cabinet
+CTRL_RM.SCADA_CAB1.MAIN_SRV   Primary SCADA server
+CTRL_RM.SCADA_CAB1.STBY_SRV   Standby SCADA server (hot standby)
+CTRL_RM.SCADA_CAB1.OPC_SRV    OPC server
+CTRL_RM.SCADA_CAB1.FEP        Front-end processor (data concentrator)
+CTRL_RM.SCADA_CAB1.COMM_GW    Communications gateway / router
+CTRL_RM.SCADA_CAB1.NET_SW     LAN switch
+CTRL_RM.SCADA_CAB1.UPS        Cabinet UPS
+CTRL_RM.SCADA_CAB1.PDU        PDU (rack power)
+CTRL_RM.HIST_CAB              Historian server cabinet
+CTRL_RM.HIST_CAB.HIST_SRV     Historian server
+CTRL_RM.HIST_CAB.HIST_SRV_STB Standby historian server
+CTRL_RM.NET_CAB               Network cabinet (OT LAN)
+CTRL_RM.NET_CAB.CORE_SW       Core OT network switch
+CTRL_RM.NET_CAB.FIREWALL      OT/IT firewall
+CTRL_RM.NET_CAB.ROUTER        WAN router
+CTRL_RM.DESK1                 Operator desk / console 1
+CTRL_RM.DESK1.PC_HMI1         HMI workstation 1
+CTRL_RM.DESK1.MON1            Monitor 1
+CTRL_RM.DESK1.MON2            Monitor 2
+CTRL_RM.DESK2                 Operator desk 2
+CTRL_RM.DESK2.PC_HMI2         HMI workstation 2
+CTRL_RM.ENG_DESK              Engineering desk
+CTRL_RM.ENG_DESK.PC_ENG       Engineering workstation

+SERVER_RM                     Server room
+SERVER_RM.RACK_A              Server rack A (SCADA primary)
+SERVER_RM.RACK_B              Server rack B (SCADA DR / backup)
+SERVER_RM.NET_RACK            Network rack
```

### Full Tag Examples — SCADA
```
=SCADA.SERVER+CTRL_RM.SCADA_CAB1.MAIN_SRV-SRV_SCADA1     Primary SCADA server
=SCADA.SERVER+CTRL_RM.SCADA_CAB1.STBY_SRV-SRV_SCADA2     Standby SCADA server
=SCADA.OPC+CTRL_RM.SCADA_CAB1.OPC_SRV-SRV_OPC1           OPC DA/UA server
=SCADA.FRONT_END+CTRL_RM.SCADA_CAB1.FEP-FEP1              Front-end processor
=SCADA.COMM+CTRL_RM.SCADA_CAB1.COMM_GW-RTR1               WAN router / comm gateway
=SCADA.COMM+CTRL_RM.NET_CAB.CORE_SW-SW_OT_CORE            Core OT switch
=SCADA.HIST+CTRL_RM.HIST_CAB.HIST_SRV-SRV_HIST1           Historian server
=SCADA.HMI+CTRL_RM.DESK1.PC_HMI1-WS_HMI1                 HMI workstation 1
=SCADA.ENG+CTRL_RM.ENG_DESK.PC_ENG-WS_ENG1               Engineering workstation
=SCADA.DR+SERVER_RM.RACK_B-SRV_SCADA_DR                  DR SCADA server
=PWR.UPS+CTRL_RM.SCADA_CAB1.UPS-UPS_SCADA                SCADA cabinet UPS
```

---

## RTU — Remote Terminal Unit Panels

> Used for remote unmanned sites: pump stations, gas gates, substations, water reservoirs
> Brands: Schneider SCADAPack, ABB RTU560, GE D20/D400, Yokogawa STARDOM, SEL RTAC, Moxa V2406, Advantech

### Function Designations — RTU
```
=RTU               RTU system overall
=RTU.CPU           RTU processor / controller function
=RTU.IO            RTU I/O function
=RTU.COMM          RTU communications function
=RTU.COMM.WAN      WAN / telemetry link (GPRS/4G/radio/fibre)
=RTU.COMM.LOCAL    Local communications (RS485, PROFIBUS, Modbus)
=RTU.POWER         RTU power supply function
=RTU.BATT          RTU battery backup function
=RTU.METER         RTU metering integration function
=RTU.IED           IED interface function (for substations)
=RTU.SAFE          RTU safety output function
```

### Location Designations — RTU Panel
```
+RTU_PNL1                    RTU panel 1 (remote site enclosure)
+RTU_PNL1.POWER              Power supply section (230VAC and 24VDC)
+RTU_PNL1.BATT               Battery backup section
+RTU_PNL1.CPU                RTU processor / controller module section
+RTU_PNL1.IO                 I/O modules section
+RTU_PNL1.IO.DI              Digital input modules
+RTU_PNL1.IO.DO              Digital output modules
+RTU_PNL1.IO.AI              Analog input modules
+RTU_PNL1.IO.AO              Analog output modules
+RTU_PNL1.IO.PULSE           Pulse / counter inputs (for meters)
+RTU_PNL1.COMM               Communications section
+RTU_PNL1.COMM.WAN           WAN modem / radio / fibre section
+RTU_PNL1.COMM.LOCAL         Local serial / fieldbus comms section
+RTU_PNL1.COMM.ETH           Ethernet switch section
+RTU_PNL1.METERING           Metering / IED interface section
+RTU_PNL1.TERM               Terminal section
+RTU_PNL1.TERM.FIELD         Field instrument terminals
+RTU_PNL1.TERM.POWER         Power terminals (mains, 24VDC)
+RTU_PNL1.TERM.COMM          Communications terminals

+RTU_PNL2                    RTU panel 2 (second remote site)
+RTU_PNL3                    RTU panel 3
```

### Full Tag Examples — RTU Panel
```
=RTU.POWER+RTU_PNL1.POWER-QF_MAINS          230VAC incoming MCB
=RTU.POWER+RTU_PNL1.POWER-PS1               24VDC SMPS
=RTU.BATT+RTU_PNL1.BATT-BATT1              12V/24V lead-acid or Li-ion backup battery
=RTU.BATT+RTU_PNL1.BATT-CHRG1             Battery charger / UPS module
=RTU.CPU+RTU_PNL1.CPU-RTU_CPU1             RTU processor module
=RTU.IO+RTU_PNL1.IO.DI-DI01               RTU DI module 01
=RTU.IO+RTU_PNL1.IO.AI-AI01               RTU AI module 01 (4-20mA)
=RTU.IO+RTU_PNL1.IO.DO-DO01               RTU DO module 01
=RTU.IO+RTU_PNL1.IO.PULSE-CNT01           Pulse counter module (for kWh meters)
=RTU.COMM.WAN+RTU_PNL1.COMM.WAN-MODEM1    4G LTE modem / cellular router
=RTU.COMM.WAN+RTU_PNL1.COMM.WAN-RADIO1    Licensed radio modem (900MHz / UHF)
=RTU.COMM.LOCAL+RTU_PNL1.COMM.LOCAL-CM_485_1  RS485 Modbus serial port 1
=RTU.COMM.LOCAL+RTU_PNL1.COMM.LOCAL-CM_IEC104  IEC 60870-5-104 comms module
=RTU.COMM.ETH+RTU_PNL1.COMM.ETH-SW_RTU1   Managed Ethernet switch (DIN rail)
=RTU.METER+RTU_PNL1.METERING-IED_PROT1    Protection IED interface (SEL, ABB)
=RTU.METER+RTU_PNL1.METERING-KWH_M1       Energy meter (Modbus RTU)
=RTU.COMM.WAN+RTU_PNL1.COMM.WAN-ANT_4G    4G antenna assembly
=RTU.COMM.WAN+RTU_PNL1.COMM.WAN-GPS1      GPS receiver (for time sync)
```

---

## Marshalling Cabinets (Automation-Focused)

> Interface layer between field cables and DCS/PLC/SIS systems

### Location Designations — Automation Marshalling
```
+MARSH_CAB_A             Marshalling cabinet A (I&C signals)
+MARSH_CAB_A.POWER       Power supply section
+MARSH_CAB_A.DI          Digital input marshalling section
+MARSH_CAB_A.DO          Digital output marshalling section
+MARSH_CAB_A.AI          Analog input marshalling section (HART signals)
+MARSH_CAB_A.AO          Analog output marshalling section
+MARSH_CAB_A.RTD         RTD / thermocouple marshalling section
+MARSH_CAB_A.BARRIER     Zener barrier / HART isolator section
+MARSH_CAB_A.RELAY       Output relay section (for DO isolation)
+MARSH_CAB_A.TERM.FIELD  Field cable terminations (left gland plate side)
+MARSH_CAB_A.TERM.SYSTEM System cable terminations (right, to DCS/PLC)

+MARSH_CAB_B             Marshalling cabinet B (safety signals)
+MARSH_CAB_B.DI_SAFE     Safety DI marshalling
+MARSH_CAB_B.DO_SAFE     Safety DO marshalling
+MARSH_CAB_B.BARRIER_S   Safety barriers (SIL-rated isolators)
+MARSH_CAB_B.TERM.FIELD  Safety field terminals
+MARSH_CAB_B.TERM.SIS    SIS system terminals

+TERM_CAB_01             Termination cabinet 01 (cable glanding only — no active devices)
+TERM_CAB_01.GLAND       Cable gland plate section
+TERM_CAB_01.TERM.DI     DI termination rail
+TERM_CAB_01.TERM.AI     AI termination rail
```

---

## Instrumentation Cabinets (Loop-Powered)

### Location Designations
```
+INST_CAB_01              Instrumentation cabinet 01
+INST_CAB_01.POWER        Loop power supply section
+INST_CAB_01.BARRIER      Intrinsic safety barriers (Zener / galvanic)
+INST_CAB_01.BARRIER.AI   Barriers for AI signals
+INST_CAB_01.BARRIER.DI   Barriers for DI signals
+INST_CAB_01.BARRIER.DO   Barriers for DO signals
+INST_CAB_01.ISOLATOR     HART galvanic isolators section
+INST_CAB_01.TEMP_TX      Temperature transmitter / head-mount TX section
+INST_CAB_01.TERM         Terminal section
+INST_CAB_01.TERM.SAFE    Safety terminals (blue — intrinsically safe)
+INST_CAB_01.TERM.NONEX   Non-IS terminals (grey — non-Ex)
+INST_CAB_01.SIGNAL_COND  Signal conditioner section
```

### Full Tag Examples — Instrumentation Cabinet
```
=PWR.24V+INST_CAB_01.POWER-PS_LOOP1      Loop power supply 24VDC (e.g. Phoenix mini POWER)
=INST+INST_CAB_01.BARRIER.AI-Z_AI01      Zener barrier channel 01 — AI (e.g. MTL 7787+)
=INST+INST_CAB_01.BARRIER.AI-Z_AI02      Zener barrier channel 02 — AI
=INST+INST_CAB_01.BARRIER.DI-Z_DI01      Zener barrier channel 01 — DI
=INST+INST_CAB_01.BARRIER.DO-Z_DO01      Zener barrier channel 01 — DO
=INST+INST_CAB_01.ISOLATOR-ISO_AI01      HART galvanic isolator channel 01
=INST+INST_CAB_01.SIGNAL_COND-SC_01      4-20mA signal conditioner / splitter
=INST+INST_CAB_01.TEMP_TX-TT_301         Head-mount temperature transmitter TT-301
```

---

## HMI Stations & Operator Consoles

### Location Designations
```
+OP_STN_1                 Operator station 1
+OP_STN_1.HMI             HMI panel (touchscreen or display)
+OP_STN_1.PC              PC / thin client
+OP_STN_1.CTRL            Control buttons, lamps, selectors
+OP_STN_1.ESTOP           Emergency stop section
+OP_STN_1.KEY             Key switches section
+OP_STN_1.PRINTER         Alarm / event printer

+OP_STN_2                 Operator station 2
+OP_CONSOLE_1             Operator console / desk 1 (large control room)
+OP_CONSOLE_1.MON1        Monitor 1 (left)
+OP_CONSOLE_1.MON2        Monitor 2 (centre)
+OP_CONSOLE_1.MON3        Monitor 3 (right)
+OP_CONSOLE_1.PC          Console PC / workstation
+OP_CONSOLE_1.KVM         KVM switch / extender
+OP_CONSOLE_1.CTRL        Operator controls (buttons, lamps)
+OP_CONSOLE_1.ESTOP       Console e-stop

+PANEL_VIEW_1             Standalone HMI panel (wall-mounted or machine-mounted)
+PENDANT_1                Operator pendant 1 (handheld, machine)
+PENDANT_1.HMI            Pendant HMI display
+PENDANT_1.CTRL           Pendant controls
+PENDANT_1.ESTOP          Pendant emergency stop

+MAIN_DISPLAY_WALL        Video wall / main display wall (control room)
+MAIN_DISPLAY_WALL.CTRL   Display wall controller
+MAIN_DISPLAY_WALL.PROC   Display wall processor
```

### Full Tag Examples — HMI / Operator Station
```
=CTRL.HMI+OP_STN_1.HMI-TP_700         Siemens TP700 or equivalent HMI panel
=CTRL.HMI+OP_STN_1.PC-WS_HMI_1        HMI workstation / thin client
=CTRL+OP_STN_1.CTRL-SS_MODE           Mode selector
=CTRL+OP_STN_1.CTRL-SB_RESET          Reset button
=CTRL+OP_STN_1.CTRL-HL_FAULT          Fault lamp
=CTRL+OP_STN_1.CTRL-HL_RUN            Running lamp
=SAFE.ESTOP+OP_STN_1.ESTOP-SB_ESTOP   E-stop push button
=SCADA.HMI+OP_CONSOLE_1.PC-WS_SCADA1  SCADA operator workstation
=SCADA.HMI+OP_CONSOLE_1.MON1-MON1     Monitor 1 (SCADA overview display)
=SCADA.HMI+OP_CONSOLE_1.MON2-MON2     Monitor 2 (process graphic)
=KVM+OP_CONSOLE_1.KVM-KVM_SW1         KVM switch at console 1
```

---

## Engineering Workstation Panels

```
+ENG_CAB1                  Engineering workstation cabinet
+ENG_CAB1.PC_ENG           Engineering PC / laptop docking
+ENG_CAB1.PROG_LAPTOP      Programming laptop connection
+ENG_CAB1.USB_HUB          USB hub for programming cables
+ENG_CAB1.USB_PN           PROFINET USB adapter (for S7 direct connect)
+ENG_CAB1.USB_PB           PROFIBUS USB adapter
+ENG_CAB1.SERIAL_485       RS485 programming port
+ENG_CAB1.NET_PORT         Ethernet port (isolated — programming only)
+ENG_CAB1.BREAKOUT         Breakout patch panel for comms connections
```

---

## Historian & Application Server Racks

> OSIsoft PI, Honeywell PHD, Aspen InfoPlus.21, Wonderware Historian, Ignition Historian

### Location Designations
```
+SERVER_RM                Server room
+SERVER_RM.RACK_HIST      Historian server rack
+SERVER_RM.RACK_HIST.SRV_HIST_PRI   Primary historian server
+SERVER_RM.RACK_HIST.SRV_HIST_STB   Standby historian server
+SERVER_RM.RACK_HIST.SRV_HIST_DR    DR historian server
+SERVER_RM.RACK_HIST.SRV_APP1       Application server 1 (asset framework, reports)
+SERVER_RM.RACK_HIST.SRV_APP2       Application server 2
+SERVER_RM.RACK_HIST.SRV_WEB        Web server (PI WebAPI, Tableau, etc.)
+SERVER_RM.RACK_HIST.NAS1           NAS / attached storage for historian data
+SERVER_RM.RACK_HIST.SW_MGT         Management network switch
+SERVER_RM.RACK_HIST.PDU_A          PDU A (A-side power)
+SERVER_RM.RACK_HIST.PDU_B          PDU B (B-side redundant power)
+SERVER_RM.RACK_HIST.PATCH          Patch panel section
+SERVER_RM.RACK_HIST.FIBER_DIST     Fibre distribution panel

+SERVER_RM.RACK_APP       Application server rack (SCADA, MES, reporting)
+SERVER_RM.RACK_APP.SRV_SCADA_PRI   Primary SCADA server
+SERVER_RM.RACK_APP.SRV_SCADA_STB   Standby SCADA server
+SERVER_RM.RACK_APP.SRV_OPC_UA      OPC UA server
+SERVER_RM.RACK_APP.SRV_MES         MES server
+SERVER_RM.RACK_APP.SRV_REPORT      Reporting server
+SERVER_RM.RACK_APP.SRV_DR          Disaster recovery server
+SERVER_RM.RACK_APP.VIRT_HOST       Virtualisation host (VMware / Hyper-V)
+SERVER_RM.RACK_APP.NAS2            SAN / NAS storage
```

### Full Tag Examples — Server Rack
```
=HIST+SERVER_RM.RACK_HIST.SRV_HIST_PRI-SRV_PI_PRI     PI historian primary server
=HIST+SERVER_RM.RACK_HIST.SRV_HIST_STB-SRV_PI_STB     PI historian standby
=SCADA.SERVER+SERVER_RM.RACK_APP.SRV_SCADA_PRI-SRV_SCADA_PRI   SCADA primary server
=SCADA.SERVER+SERVER_RM.RACK_APP.SRV_SCADA_STB-SRV_SCADA_STB   SCADA standby
=SCADA.OPC+SERVER_RM.RACK_APP.SRV_OPC_UA-SRV_OPC_UA   OPC UA server
=MES+SERVER_RM.RACK_APP.SRV_MES-SRV_MES1              MES server
=SERVER+SERVER_RM.RACK_APP.VIRT_HOST-ESXI_HOST1        VMware ESXi host
=STORAGE+SERVER_RM.RACK_HIST.NAS1-NAS_HIST1            NAS storage for historian
=PWR.IT+SERVER_RM.RACK_HIST.PDU_A-PDU_A1               Rack PDU A side
=PWR.IT+SERVER_RM.RACK_HIST.PDU_B-PDU_B1               Rack PDU B side (redundant)
```

---

## Network Infrastructure Cabinets

### Location Designations — OT Network
```
+NET_CAB_OT               OT network cabinet (control room)
+NET_CAB_OT.CORE_SW       Core OT switch section
+NET_CAB_OT.DIST_SW1      Distribution switch 1 section
+NET_CAB_OT.DIST_SW2      Distribution switch 2 section
+NET_CAB_OT.FIREWALL      OT firewall / DMZ appliance section
+NET_CAB_OT.ROUTER        WAN router section
+NET_CAB_OT.TIME_SRV      NTP / GPS time server section
+NET_CAB_OT.FIBER_DIST    Fibre distribution panel
+NET_CAB_OT.PATCH_ETH     Ethernet patch panel
+NET_CAB_OT.PDU           Rack PDU
+NET_CAB_OT.UPS           Rack UPS

+NET_CAB_FIELD_A          Field network cabinet area A
+NET_CAB_FIELD_A.SW1      Field switch 1 (access layer)
+NET_CAB_FIELD_A.MEDIA_CNV Fibre media converter section
+NET_CAB_FIELD_A.PATCH    Patch panel

+NET_CAB_FIELD_B          Field network cabinet area B
```

---

## Industrial Network Cabinets (OT Network)

> PROFINET, EtherNet/IP, Modbus TCP, PROFIBUS, DeviceNet, IO-Link, Foundation Fieldbus

### Function Designations — OT Network
```
=NETW.OT               OT network function (overall)
=NETW.OT.CORE          Core OT network function
=NETW.OT.DIST          Distribution layer function
=NETW.OT.ACCESS        Access layer (field switches) function
=NETW.OT.RING          Ring topology (MRP/RSTP) function
=NETW.OT.PN            PROFINET network function
=NETW.OT.EIP           EtherNet/IP network function
=NETW.OT.MODBUS        Modbus TCP network function
=NETW.OT.FIBER         Fibre backbone function
=NETW.OT.SERIAL        Serial / RS485 network function
=NETW.OT.HART          HART network function
=NETW.OT.FF            Foundation Fieldbus function
=NETW.OT.IOLINK        IO-Link network function
=NETW.OT.ASI           AS-Interface function
=NETW.OT.WIFI          Industrial WiFi function
=NETW.DMZ              DMZ function (OT/IT boundary)
=CYBER                 Cybersecurity function
```

### Location Designations — OT Network Equipment
```
+NET_CAB_OT.CORE_SW               Core OT switch (Layer 2/3 managed)
+NET_CAB_OT.DIST_SW1              Distribution switch 1
+NET_CAB_OT.DIST_SW2              Distribution switch 2
+NET_CAB_OT.FIREWALL              Firewall appliance (Fortinet, Cisco, Tofino)
+NET_CAB_OT.ROUTER                Router (for WAN / telemetry links)
+NET_CAB_OT.DMZ_CAB               DMZ cabinet (data diode, jump server)
+NET_CAB_OT.WIFI_AP               Industrial WiFi access point
+FLD_CAB_A1.COMM.SW_PN1           Field PROFINET switch area A1
+FLD_CAB_B1.COMM.SW_PN2           Field PROFINET switch area B1
+RIO_CAB_01.COMM.SW_PN3           Remote I/O cabinet switch 01
```

### Full Tag Examples — OT Network
```
=NETW.OT.CORE+NET_CAB_OT.CORE_SW-SW_CORE_OT      Core OT managed switch (e.g. Cisco IE4000)
=NETW.OT.DIST+NET_CAB_OT.DIST_SW1-SW_DIST_OT1    Distribution switch 1 (e.g. Hirschmann MACH)
=NETW.OT.DIST+NET_CAB_OT.DIST_SW2-SW_DIST_OT2    Distribution switch 2
=NETW.OT.PN+FLD_CAB_A1.COMM.SW_PN1-SW_PN_A1      PROFINET field switch area A1 (e.g. Scalance XC208)
=NETW.OT.FIBER+NET_CAB_OT.FIBER_DIST-FDP_OT1     Fibre distribution panel OT
=NETW.OT.ACCESS+FLD_CAB_B1.COMM.FC_1-FC_FIBER_B1  Fibre/copper media converter area B1
=NETW.DMZ+NET_CAB_OT.FIREWALL-FW_OT_IT            OT/IT firewall (Fortinet FortiGate, Tofino)
=CYBER+NET_CAB_OT.DMZ_CAB-DATA_DIODE1             Data diode (Owl, Waterfall — unidirectional)
=NETW.OT.WIFI+NET_CAB_OT.WIFI_AP-AP_INDUS1        Industrial WiFi AP (e.g. Cisco Catalyst IW6300)
=NETW.OT.SERIAL+RIO_CAB_01.COMM.CM_485_1-RS485_GW  RS485 Modbus serial gateway
=TIME+NET_CAB_OT.TIME_SRV-NTP_SRV1                NTP time server (GPS-disciplined)
```

---

## IT / Corporate Network Racks (IT Network)

### Function Designations — IT Network
```
=NETW.IT               IT / corporate network function
=NETW.IT.CORE          Core IT switch function
=NETW.IT.DIST          Distribution switch function
=NETW.IT.ACCESS        Access layer switch function
=NETW.IT.WIFI          Corporate WiFi function
=NETW.IT.VOIP          VoIP / telephony function
=NETW.IT.ROUTER        WAN / Internet router function
=NETW.IT.FIREWALL      IT perimeter firewall function
=NETW.IT.PROXY         Web proxy / content filter function
=NETW.IT.DNS_DHCP      DNS/DHCP server function
=NETW.IT.AD            Active Directory / identity function
=NETW.IT.EMAIL         Email server function
=NETW.IT.BACKUP        Backup / DR function
```

### Location Designations — IT Rack
```
+SERVER_RM.NET_RACK                IT network rack
+SERVER_RM.NET_RACK.CORE_SW_IT     Core IT switch
+SERVER_RM.NET_RACK.DIST_SW_IT1    Distribution switch 1
+SERVER_RM.NET_RACK.DIST_SW_IT2    Distribution switch 2
+SERVER_RM.NET_RACK.ROUTER_WAN     WAN router (ISP connection)
+SERVER_RM.NET_RACK.FIREWALL_IT    IT perimeter firewall
+SERVER_RM.NET_RACK.PROXY          Web proxy appliance
+SERVER_RM.NET_RACK.PATCH_IT1      Patch panel IT — Cat6 rack 1
+SERVER_RM.NET_RACK.PATCH_IT2      Patch panel IT — Cat6 rack 2
+SERVER_RM.NET_RACK.FDP_IT         Fibre distribution panel IT
+SERVER_RM.NET_RACK.PDU_IT         Rack PDU (IT power)
+SERVER_RM.NET_RACK.UPS_IT         Rack UPS IT
```

---

## Server Racks & Blade Centres

### Location Designations — Server Rack Detailed
```
+SERVER_RM.RACK_A                 Server rack A
+SERVER_RM.RACK_A.SRV1            Server / node 1 (1U, 2U, etc.)
+SERVER_RM.RACK_A.SRV2            Server / node 2
+SERVER_RM.RACK_A.SRV3            Server / node 3
+SERVER_RM.RACK_A.BLADE_CHASSIS   Blade chassis (e.g. Dell PowerEdge M1000e, HPE Synergy)
+SERVER_RM.RACK_A.BLADE1          Blade module 1
+SERVER_RM.RACK_A.BLADE2          Blade module 2
+SERVER_RM.RACK_A.BLADE3          Blade module 3
+SERVER_RM.RACK_A.SAN_SW          SAN switch (Fibre Channel)
+SERVER_RM.RACK_A.NAS             NAS appliance
+SERVER_RM.RACK_A.TAPE_LIB        Tape library (backup)
+SERVER_RM.RACK_A.KVM             KVM switch
+SERVER_RM.RACK_A.CONSOLE         Console port switch / IPMI aggregator
+SERVER_RM.RACK_A.PDU_A           Rack PDU A (left side, A-power)
+SERVER_RM.RACK_A.PDU_B           Rack PDU B (right side, B-power)
+SERVER_RM.RACK_A.PATCH           Patch panel (Cat6 / fibre)

+SERVER_RM.RACK_B                 Server rack B
+SERVER_RM.RACK_C                 Server rack C
```

### Full Tag Examples — Server Rack
```
=SERVER+SERVER_RM.RACK_A.SRV1-HP_PROLIANT1     Application server 1
=SERVER+SERVER_RM.RACK_A.SRV2-DELL_R750_2      Application server 2
=SERVER+SERVER_RM.RACK_A.BLADE_CHASSIS-CHASSIS1  Blade chassis
=STORAGE+SERVER_RM.RACK_A.NAS-NAS_NETAPP1      NAS storage
=KVM+SERVER_RM.RACK_A.KVM-KVM_RACK_A           Rack KVM switch
=NETW.IT.ACCESS+SERVER_RM.RACK_A.SW_MGMT-SW_MGMT_A  Out-of-band management switch
=PWR.IT+SERVER_RM.RACK_A.PDU_A-PDU_RACK_A_A   Rack PDU A (A-side)
=PWR.IT+SERVER_RM.RACK_A.PDU_B-PDU_RACK_A_B   Rack PDU B (B-side, redundant)
=PATCH+SERVER_RM.RACK_A.PATCH-PP_CAT6_A1       Cat6 patch panel rack A
```

---

## Storage & Backup Systems

```
+STORAGE_RM              Storage / backup room (or section of server room)
+STORAGE_RM.SAN_RACK     SAN rack
+STORAGE_RM.SAN_RACK.SAN_ARRAY1   SAN storage array 1
+STORAGE_RM.SAN_RACK.SAN_ARRAY2   SAN storage array 2
+STORAGE_RM.SAN_RACK.FC_SW1       Fibre Channel SAN switch 1
+STORAGE_RM.SAN_RACK.FC_SW2       Fibre Channel SAN switch 2
+STORAGE_RM.SAN_RACK.NAS1         NAS head 1
+STORAGE_RM.SAN_RACK.TAPE_LIB     Tape library / LTO drive
+STORAGE_RM.SAN_RACK.BACKUP_SRV   Backup server (Veeam, CommVault, etc.)
```

---

## KVM & Console Access Systems

```
+KVM_CAB                 KVM / console access cabinet
+KVM_CAB.KVM_MATRIX      KVM matrix switch (centralised)
+KVM_CAB.CAT_TX          KVM CAT extender — transmitter side
+KVM_CAB.IPKVM           IP KVM / IPMI aggregator (remote access)
+KVM_CAB.SERIAL_CON      Serial console server (Opengear, Digi, Lantronix)

+OP_CONSOLE_1.KVM        KVM receiver at operator console 1
+OP_CONSOLE_2.KVM        KVM receiver at operator console 2
+ENG_CAB1.KVM            KVM receiver at engineering workstation
```

### Full Tag Examples — KVM
```
=KVM+KVM_CAB.KVM_MATRIX-KVM_MATRIX1      KVM matrix switch (e.g. Guntermann, Raritan, Aten)
=KVM+KVM_CAB.CAT_TX-CAT_TX_SRV1          CAT6 KVM transmitter connected to server 1
=KVM+OP_CONSOLE_1.KVM-CAT_RX_CONS1       CAT6 KVM receiver at console 1
=KVM+KVM_CAB.IPKVM-IPKVM_AGGR1           IP KVM aggregator (Lantronix SLC)
=KVM+KVM_CAB.SERIAL_CON-SCS_CON1         Serial console server (Opengear CM7100)
```

---

## Patch Panels & Structured Cabling

```
+NET_CAB_OT.PATCH_ETH         Ethernet patch panel — OT (Cat6/6A)
+SERVER_RM.NET_RACK.PATCH_IT1 Ethernet patch panel — IT rack
+NET_CAB_OT.FIBER_DIST        Fibre distribution panel — OT
+SERVER_RM.RACK_A.PATCH       Patch panel — server rack A
+MDA.PATCH_MDA                Main distribution area patch (data centre)
+HDA1.PATCH_HDA               Horizontal distribution area patch
```

### Full Tag Examples — Patch
```
=PATCH+NET_CAB_OT.PATCH_ETH-PP_ETH_OT1      OT 24-port Cat6 patch panel
=FIBER+NET_CAB_OT.FIBER_DIST-FDP_OT1        OT fibre distribution panel (LC duplex)
=PATCH+SERVER_RM.NET_RACK.PATCH_IT1-PP_IT1  IT 48-port Cat6A patch panel
=FIBER+SERVER_RM.RACK_A.PATCH-FDP_SRV_A     Server rack A fibre patch panel
```

---

## UPS for Control & IT Systems

### Location Designations
```
+UPS_RM                   UPS room (or section within server room)
+UPS_RM.UPS_OT            OT / control system UPS
+UPS_RM.UPS_OT.UPS_UNIT   UPS main unit
+UPS_RM.UPS_OT.BATT1      Battery string 1
+UPS_RM.UPS_OT.BATT2      Battery string 2
+UPS_RM.UPS_OT.DIST_BD    UPS output distribution board

+UPS_RM.UPS_IT            IT system UPS
+UPS_RM.UPS_IT.UPS_UNIT   UPS main unit
+UPS_RM.UPS_IT.BATT1      Battery string 1
+UPS_RM.UPS_IT.DIST_BD    UPS output distribution board

+SERVER_RM.RACK_A.UPS_RACK  Rack-mount UPS for server rack A
+CTRL_RM.SCADA_CAB1.UPS     Cabinet-mount UPS for SCADA cabinet
+CP1.POWER.UPS_BUF          DIN-rail 24VDC UPS buffer module (inside PLC panel)
```

---

## PDU — Power Distribution Units (Rack Level)

```
+SERVER_RM.RACK_A.PDU_A     Vertical rack PDU A (A-side power, left)
+SERVER_RM.RACK_A.PDU_B     Vertical rack PDU B (B-side power, right)
+SERVER_RM.RACK_B.PDU_A     Rack B PDU A
+SERVER_RM.RACK_B.PDU_B     Rack B PDU B
+NET_CAB_OT.PDU             OT network cabinet PDU
+CTRL_RM.SCADA_CAB1.PDU     SCADA cabinet PDU
```

### Full Tag Examples — PDU
```
=PWR.IT+SERVER_RM.RACK_A.PDU_A-PDU_A_RACK_A   Rack PDU A — 32A IEC 60309 input, 24x C13 outlets
=PWR.IT+SERVER_RM.RACK_A.PDU_B-PDU_B_RACK_A   Rack PDU B — redundant B-side
=METER+SERVER_RM.RACK_A.PDU_A-METER_PDU_A      Metered PDU — per-outlet monitoring
```

---

## Fibre Optic Distribution Panels

```
+FDP_OT_MAIN              Main OT fibre distribution panel (core of star topology)
+FDP_OT_MAIN.LC_PANEL     LC duplex patch panel section
+FDP_OT_MAIN.SC_PANEL     SC duplex patch panel section
+FDP_OT_MAIN.SPLICE       Splice tray section (fusion splices)

+FDP_FIELD_A1             Field fibre distribution panel area A1
+FDP_FIELD_B1             Field fibre distribution panel area B1
+FDP_SERVER_RM            Server room fibre distribution panel
```

---

## Communications & Telecom Panels

```
+COMM_CAB1                Communications cabinet 1
+COMM_CAB1.ROUTER_WAN     WAN router (MPLS, leased line, cellular)
+COMM_CAB1.MODEM_4G       4G / 5G router / backup link
+COMM_CAB1.RADIO_MOD      Licensed radio modem (SCADA telemetry)
+COMM_CAB1.MEDIA_CNV      Fibre / copper media converters
+COMM_CAB1.SERIAL_MUX     Serial multiplexer / data concentrator
+COMM_CAB1.SW_WAN         WAN-side switch
+COMM_CAB1.VOIP_GW        VoIP gateway
+COMM_CAB1.PABX           PABX / telephone exchange (small)
+COMM_CAB1.PA_AMP         PA system amplifier
+COMM_CAB1.ANT_SPLIT      Antenna splitter / combiner

+COMM_CAB2                Communications cabinet 2 (satellite / microwave)
+COMM_CAB2.SAT_MODEM      Satellite modem (Ku-band, VSAT)
+COMM_CAB2.MW_MODEM       Microwave radio modem
+COMM_CAB2.IDU            Indoor unit (IDU) for microwave / satellite
```

---

## Cybersecurity & Demilitarized Zone (DMZ) Equipment

### Function Designations
```
=CYBER               Cybersecurity infrastructure function
=CYBER.FIREWALL      Firewall function
=CYBER.DMZ           DMZ function
=CYBER.DIODE         Data diode function (unidirectional security gateway)
=CYBER.JUMPSERVER    Jump server / bastion host function
=CYBER.SIEM          SIEM / log management function
=CYBER.IDS           Intrusion detection function
=CYBER.PAM           Privileged access management function
=NETW.DMZ            DMZ network function
```

### Location Designations — Cybersecurity
```
+DMZ_CAB                   DMZ cabinet
+DMZ_CAB.FW_OT_IT          OT/IT boundary firewall
+DMZ_CAB.FW_CORP           Corporate perimeter firewall
+DMZ_CAB.JUMP_SRV          Jump server / bastion host
+DMZ_CAB.DATA_DIODE        Data diode (unidirectional gateway)
+DMZ_CAB.SIEM_SRV          SIEM server (Splunk, IBM QRadar, AlienVault)
+DMZ_CAB.IDS_SENSOR        IDS / IPS sensor (Claroty, Dragos, Nozomi)
+DMZ_CAB.PAM_APPLIANCE     PAM appliance (CyberArk, Thycotic)
+DMZ_CAB.PATCH_MGT         Patch management server
+DMZ_CAB.AV_SRV            AV / endpoint protection update server
+DMZ_CAB.LOG_SRV           Centralised log / syslog server
```

### Full Tag Examples — Cybersecurity
```
=CYBER.FIREWALL+DMZ_CAB.FW_OT_IT-FW_OT_IT1      OT/IT firewall (Fortinet FortiGate 100F)
=CYBER.DIODE+DMZ_CAB.DATA_DIODE-DD1              Data diode (Owl Cyber Defense, Waterfall)
=CYBER.JUMPSERVER+DMZ_CAB.JUMP_SRV-SRV_JUMP1    Jump / bastion server
=CYBER.SIEM+DMZ_CAB.SIEM_SRV-SRV_SIEM1          SIEM server (Splunk Enterprise)
=CYBER.IDS+DMZ_CAB.IDS_SENSOR-IDS_SENSOR1        OT IDS sensor (Claroty / Dragos)
=CYBER.PAM+DMZ_CAB.PAM_APPLIANCE-PAM_APPLN1      PAM appliance (CyberArk)
```

---

## Time Synchronisation (GPS / NTP)

```
+NET_CAB_OT.TIME_SRV          NTP server location
+NET_CAB_OT.TIME_SRV.GPS_ANT  GPS antenna (roof-mounted, cabled to cabinet)
+RTU_PNL1.COMM.WAN.GPS1       GPS receiver in RTU panel
+SIS_CAB1.COMM.GPS_NTP        GPS NTP module in SIS cabinet
+PROT_PNL1.SCADA.GPS_NTP      GPS NTP for protection panel (IEC 61850 PTP)
```

### Full Tag Examples — Time Sync
```
=TIME+NET_CAB_OT.TIME_SRV-NTP_GPS_1         GPS-disciplined NTP server (e.g. Meinberg M300)
=TIME+NET_CAB_OT.TIME_SRV.GPS_ANT-ANT_GPS   Roof GPS antenna
=TIME+SIS_CAB1.COMM.GPS_NTP-GPS_NTP_SIS1    GPS NTP module in SIS (1ms accuracy)
=TIME+PROT_PNL1.SCADA.GPS_NTP-PTP_MASTER1   IEEE 1588 PTP grandmaster (for IED sync)
```

---

## Control Room Layout — Full Example

```
+CTRL_RM                              Control room (room boundary)

--- Control / PLC Cabinets ---
+CTRL_RM.CAB1                         PLC cabinet 1 (CPU A)
+CTRL_RM.CAB1.CPU_A                   CPU A rack
+CTRL_RM.CAB1.CPU_B                   CPU B rack (redundant)
+CTRL_RM.CAB1.IO_RACK                 I/O rack
+CTRL_RM.CAB1.POWER                   Power supplies
+CTRL_RM.CAB1.COMM                    Comms modules
+CTRL_RM.CAB1.TERM                    Terminals

+CTRL_RM.CAB2                         PLC cabinet 2 (I/O expansion)
+CTRL_RM.CAB2.IO_RACK1                I/O rack 1
+CTRL_RM.CAB2.IO_RACK2                I/O rack 2
+CTRL_RM.CAB2.TERM                    Terminals

--- SCADA / Server Cabinets ---
+CTRL_RM.SCADA_CAB                    SCADA server cabinet
+CTRL_RM.SCADA_CAB.SCADA_PRI          Primary SCADA server
+CTRL_RM.SCADA_CAB.SCADA_STB          Standby SCADA server
+CTRL_RM.SCADA_CAB.OPC_SRV            OPC server
+CTRL_RM.SCADA_CAB.UPS                SCADA cabinet UPS

--- Historian Cabinet ---
+CTRL_RM.HIST_CAB                     Historian cabinet
+CTRL_RM.HIST_CAB.HIST_SRV            Historian server
+CTRL_RM.HIST_CAB.APP_SRV             Application server

--- Network Cabinets ---
+CTRL_RM.NET_CAB_OT                   OT network cabinet
+CTRL_RM.NET_CAB_OT.CORE_SW           Core OT switch
+CTRL_RM.NET_CAB_OT.FIREWALL          OT/IT firewall
+CTRL_RM.NET_CAB_OT.TIME_SRV          NTP server
+CTRL_RM.NET_CAB_OT.FIBER_DIST        Fibre distribution panel

--- Safety Cabinet ---
+CTRL_RM.SIS_CAB                      SIS / safety cabinet
+CTRL_RM.SIS_CAB.LOGIC_A              SIS logic solver A
+CTRL_RM.SIS_CAB.LOGIC_B              SIS logic solver B
+CTRL_RM.SIS_CAB.IO_SAFE              Safety I/O rack
+CTRL_RM.SIS_CAB.POWER                Safety power supplies

--- UPS Cabinet ---
+CTRL_RM.UPS_CAB                      UPS cabinet (feeds all control room cabinets)
+CTRL_RM.UPS_CAB.UPS_UNIT             UPS main unit
+CTRL_RM.UPS_CAB.BATT1                Battery string 1
+CTRL_RM.UPS_CAB.DIST_BD              UPS distribution board

--- Operator Desks ---
+CTRL_RM.DESK1                        Operator desk 1
+CTRL_RM.DESK1.PC_HMI1                HMI workstation 1
+CTRL_RM.DESK1.MON1                   Monitor 1
+CTRL_RM.DESK1.MON2                   Monitor 2
+CTRL_RM.DESK1.ESTOP                  Desk-mounted e-stop

+CTRL_RM.DESK2                        Operator desk 2
+CTRL_RM.DESK2.PC_HMI2                HMI workstation 2
+CTRL_RM.DESK2.MON1                   Monitor 1
+CTRL_RM.DESK2.MON2                   Monitor 2

+CTRL_RM.ENG_DESK                     Engineering desk
+CTRL_RM.ENG_DESK.PC_ENG              Engineering workstation

--- Display Wall ---
+CTRL_RM.DISPLAY_WALL                 Video wall (6x panels)
+CTRL_RM.DISPLAY_WALL.CTRL_PROC       Display wall processor / controller
```

---

## DCS Control System — Full Example

```
Plant: Petrochemical Unit 30 — Reaction Area

=DCS+CTRL_RM.CAB1-FCS_A             DCS FCS A (Emerson DeltaV)
=DCS+CTRL_RM.CAB1-FCS_B             DCS FCS B (redundant)
=DCS.IO+CTRL_RM.CAB1.IO_RACK_A-AI01_A   AI card 01 side A (pressure / flow — 4-20mA HART)
=DCS.IO+CTRL_RM.CAB1.IO_RACK_B-AI01_B   AI card 01 side B (redundant)
=DCS.IO+CTRL_RM.CAB1.IO_RACK_A-AO01     AO card 01 (control valves)
=DCS.IO+CTRL_RM.CAB1.IO_RACK_A-DI01     DI card 01 (on/off status)
=DCS.IO+CTRL_RM.CAB1.IO_RACK_A-DO01     DO card 01 (on/off commands)
=DCS.IO+CTRL_RM.CAB1.IO_RACK_A-FF01     FF H1 card (Foundation Fieldbus devices)

=DCS.IO+FLD_CAB_A1.IO_RACK-IM1           Remote I/O interface module area A
=DCS.IO+FLD_CAB_A1.IO_RACK-AI01_R        Remote AI card (field-mounted, Ex rated)
=DCS.IO+FLD_CAB_A1.IO_RACK-HART_MUX1     HART multiplexer (field)

=MARSH+MARSH_CAB_A.AI-X_AI_01           AI marshalling terminals (HART loop)
=MARSH+MARSH_CAB_A.BARRIER.AI-Z_AI01    Zener barrier AI channel 01

=DCS.HMI+CTRL_RM.DESK1.PC_HMI1-WS_DCS1  DCS operator workstation 1
=DCS.ENG+CTRL_RM.ENG_DESK.PC_ENG-WS_ENG1 DCS engineering workstation
=DCS.HIST+CTRL_RM.HIST_CAB.HIST_SRV-SRV_HIST  Integrated historian server
=DCS.COMM+CTRL_RM.NET_CAB_OT.CORE_SW-SW_DCS_CORE  DCS control network switch
```

---

## SCADA / RTU Network — Full Example

```
SCADA Head End (Control Room):
=SCADA.SERVER+CTRL_RM.SCADA_CAB.SCADA_PRI-SRV_SCADA1   Primary SCADA server
=SCADA.SERVER+CTRL_RM.SCADA_CAB.SCADA_STB-SRV_SCADA2   Hot standby SCADA server
=SCADA.FRONT_END+CTRL_RM.SCADA_CAB.FEP-FEP1             Front-end processor
=SCADA.COMM+CTRL_RM.NET_CAB_OT.ROUTER-RTR_WAN1          WAN router (MPLS)
=HIST+CTRL_RM.HIST_CAB.HIST_SRV-SRV_PI1                PI historian
=SCADA.HMI+CTRL_RM.DESK1.PC_HMI1-WS_SCADA1             Operator HMI

Remote Sites (RTU panels, unmanned):
=RTU+RTU_PNL1.CPU-RTU1_CPU                RTU site 01 — pump station 1
=RTU.COMM.WAN+RTU_PNL1.COMM.WAN-MODEM1   RTU 01 4G modem
=RTU+RTU_PNL2.CPU-RTU2_CPU                RTU site 02 — pump station 2
=RTU.COMM.WAN+RTU_PNL2.COMM.WAN-RADIO1   RTU 02 radio modem (licensed UHF)
=RTU+RTU_PNL3.CPU-RTU3_CPU                RTU site 03 — reservoir
=RTU.COMM.WAN+RTU_PNL3.COMM.WAN-SAT1     RTU 03 satellite modem (remote site)
```

---

## IT / OT Convergence Architecture

```
LEVEL 4 (Enterprise / IT):
=NETW.IT+SERVER_RM.NET_RACK.CORE_SW_IT-SW_IT_CORE    IT core switch
=SERVER+SERVER_RM.RACK_A.SRV1-SRV_ERP                ERP server
=SERVER+SERVER_RM.RACK_A.SRV2-SRV_AD                 Active Directory server

LEVEL 3.5 (DMZ — OT/IT Boundary):
=CYBER.FIREWALL+DMZ_CAB.FW_OT_IT-FW_OT_IT1           OT/IT firewall (Purdue Model L3.5)
=CYBER.JUMPSERVER+DMZ_CAB.JUMP_SRV-SRV_JUMP1         Jump server (remote access)
=CYBER.DIODE+DMZ_CAB.DATA_DIODE-DD_HIST               Data diode — historian to IT

LEVEL 3 (Site Operations / SCADA):
=SCADA.SERVER+CTRL_RM.SCADA_CAB.SCADA_PRI-SRV_SCADA  SCADA server
=HIST+CTRL_RM.HIST_CAB.HIST_SRV-SRV_HIST             Historian server (PI / Ignition)
=SCADA.OPC+CTRL_RM.SCADA_CAB.OPC_SRV-SRV_OPC         OPC UA server

LEVEL 2 (Process Control / DCS):
=DCS+CTRL_RM.CAB1-FCS_A                               DCS controller
=CTRL.PLC+CP1.PLC-CPU1                                Standalone PLC
=NETW.OT.CORE+CTRL_RM.NET_CAB_OT.CORE_SW-SW_OT_CORE  OT core switch

LEVEL 1 (Field I/O / Remote I/O):
=CTRL.IO+FLD_CAB_A1.IO_RACK-IM1                       Remote I/O module
=RTU+RTU_PNL1.CPU-RTU1_CPU                            Remote RTU

LEVEL 0 (Field devices):
=INST+FIELD-FT101                                      Flow transmitter
=MOTOR.DOL+MCC1.M01-KM1                               Motor starter
```

---

## Common Device Tags Reference

### PLC / Controller Devices
```
CPU_A / CPU_B     PLC CPU (A = primary, B = standby)
PM1               PLC power module
IM1               Interface module (expansion rack)
DI01..n           Digital input modules
DO01..n           Digital output modules
AI01..n           Analog input modules
AO01..n           Analog output modules
RTD01             RTD/thermocouple module
CNT01             Counter/encoder module
SYNC_MOD          Redundancy sync module
CM_PN             PROFINET comms module
CM_PB             PROFIBUS comms module
CM_485            RS485/Modbus module
CM_ETH            Ethernet comms module
CM_IEC104         IEC 60870-5-104 comms module
```

### Server / IT Devices
```
SRV_SCADA_PRI     Primary SCADA server
SRV_SCADA_STB     Standby SCADA server
SRV_HIST          Historian server
SRV_OPC           OPC server
SRV_APP           Application server
SRV_WEB           Web server
SRV_DR            Disaster recovery server
SRV_ENG           Engineering server
ESXI_HOST         VMware ESXi hypervisor host
NAS1 / NAS2       Network attached storage
SAN_ARRAY         SAN storage array
TAPE_LIB          Tape library
```

### Network Devices
```
SW_CORE_OT        Core OT switch
SW_DIST_OT1       OT distribution switch
SW_PN_FIELD       PROFINET field switch
SW_CORE_IT        Core IT switch
SW_MGMT           Out-of-band management switch
RTR_WAN           WAN router
FW_OT_IT          OT/IT firewall
FW_CORP           Corporate perimeter firewall
FEP1              Front-end processor
FC_FIBER1         Fibre media converter
AP_INDUS1         Industrial WiFi access point
```

### Cybersecurity / Communications
```
FW_OT_IT          OT/IT boundary firewall
DD1               Data diode
SRV_JUMP          Jump / bastion server
SRV_SIEM          SIEM server
IDS_SENSOR        OT IDS/IPS sensor
PAM_APPLN         PAM appliance
NTP_GPS           GPS-disciplined NTP server
ANT_GPS           GPS antenna
MODEM_4G          4G/LTE modem
RADIO1            Licensed radio modem
SAT_MODEM         Satellite modem
```

---

## Common Mistakes

| ❌ Wrong | ✅ Correct | Reason |
|----------|------------|--------|
| `=SERVER_1` | `+SERVER_RM.RACK_A.SRV1` | Server 1 is a location/device, not a function |
| `+SCADA` | `=SCADA` and `+CTRL_RM.SCADA_CAB` | SCADA is a function; cabinet is the location |
| `+NETWORK` | `+NET_CAB_OT` or `+NET_CAB_IT` | Network is a function `=NETW`; the cabinet is the location |
| `=PLC1` | `+CP1.PLC` with `=CTRL.PLC` | PLC1 is a device `-CPU1`, not a function |
| Leaving `+` blank for servers | `+SERVER_RM.RACK_A.SRVn` | Blank location — server disappears from location-filtered reports |
| `+CONTROL_ROOM` for everything | Break down to cabinet level `+CTRL_RM.CAB1` | Too broad — entire control room merges in all reports |
| Mixing IT rack convention with PLC panel convention | Define rules upfront for automation vs IT sections | Inconsistency breaks rack layout drawings and cable reports |
| `+PLC_CAB` and `+PLCCAB` and `+PLC CAB` for same cabinet | `+PLC_CAB` — one convention, zero spaces | Three different names = three different locations in reports |
| `=CTRL+SERVER_RM` | `=SCADA.SERVER+SERVER_RM.RACK_A` | Function and location both need to be specific |
| Not distinguishing OT and IT network cabinets | `+NET_CAB_OT` / `+NET_CAB_IT` | OT and IT are different cybersecurity zones — must be separated |

---

## Expert Tips

### 1. Layer your `=` function by ISA/Purdue level
> Level 0 = field, Level 1 = I/O / RTU, Level 2 = PLC / DCS, Level 3 = SCADA / Historian, Level 3.5 = DMZ, Level 4 = IT / ERP. Use this as your `=` hierarchy. It maps directly to cybersecurity zone documentation.

### 2. Redundant systems need paired `+` locations
> `+CP1.CPU_A` and `+CP1.CPU_B` for redundant CPUs. `+UPS_RM.UPS_OT` and `+UPS_RM.UPS_IT` for separate UPS systems. Separate `+` locations = separate terminal diagrams = correct commissioning checklists.

### 3. Give every server its own `+` sub-location
> `+SERVER_RM.RACK_A.SRV1` not just `+SERVER_RM.RACK_A`. Rack-level granularity means your cable schedules, power circuits, and network port assignments all filter correctly.

### 4. Use `+FIELD` or `+FLD_CAB_XX` for all remote I/O drops
> Never leave remote I/O cabinets on the same `+` location as the main PLC cabinet. Each remote I/O drop is a physically separate enclosure and deserves its own `+` location.

### 5. Separate OT and IT `+` locations — always
> `+NET_CAB_OT` ≠ `+NET_CAB_IT`. Mixing them in EPLAN will mix your OT and IT cable schedules, which matters enormously for cybersecurity documentation (ISA/IEC 62443).

### 6. Safety system cabinets must have their own `+` location
> `+SIS_CAB1` separate from `+CTRL_RM.CAB1`. Safety I/O terminals, cable schedules, and wiring separation documents all depend on the SIS having its own distinct location.

### 7. Communications modules deserve their own `+` sub-section
> `+CP1.COMM` separate from `+CP1.PLC`. When commissioning a PROFINET ring or diagnosing a Modbus fault, having comms modules filtered separately saves hours.

### 8. Document WAN / telemetry links with their own `+` location
> `+RTU_PNL1.COMM.WAN` for the modem / radio section. Telecoms engineers who commission the WAN link need to find all WAN components in one place on the drawing.

### 9. Use `+CTRL_RM.DESK1` for operator workstations — not the server rack
> Operator PCs, monitors, and KVM receivers are physically at the desk, not in the server rack. Separate `+` for desk vs rack keeps installation drawings and cable schedules accurate.

### 10. Always tag GPS antennas, fibre runs, and battery backups
> `+NET_CAB_OT.TIME_SRV.GPS_ANT` for the GPS antenna. `+RTU_PNL1.BATT.BATT1` for the backup battery. These are real components with real cable connections that must appear in the cable schedule and BOM.

---

*Based on IEC 61131 | IEC 61512 | IEC 61511 | IEC 62443 | IEC 60870 | IEC 61968 | ISA-95 | ISA-99 / IEC 62443 | NIST SP 800-82 | Purdue Reference Model | IEC 61850 | IEEE 1588*
*Expert conventions for system integrators, automation engineers, DCS/SCADA designers, IT/OT convergence engineers, and cybersecurity-aware panel builders*
