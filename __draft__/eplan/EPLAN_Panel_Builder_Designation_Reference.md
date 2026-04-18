# EPLAN P8 — Panel Builder Designation Reference Guide
> Specialized for: MV Switchgear | LV Switchgear | MCC | Distribution Boards | Ring Main Units | Busbars | Transformers | UPS | Capacitor Banks | Soft Starters | VFD Panels | Control Panels | Marshalling Cabinets | Junction Boxes

---

## Table of Contents
1. [Fundamentals for Panel Builders](#fundamentals-for-panel-builders)
2. [Naming Philosophy](#naming-philosophy)
3. [MV Switchgear (Medium Voltage)](#mv-switchgear-medium-voltage)
4. [LV Main Switchboard (MSB)](#lv-main-switchboard-msb)
5. [Motor Control Centre (MCC)](#motor-control-centre-mcc)
6. [Distribution Boards (DB)](#distribution-boards-db)
7. [Ring Main Unit (RMU)](#ring-main-unit-rmu)
8. [Busbar Trunking System (BTS)](#busbar-trunking-system-bts)
9. [Power Transformers (Dry Type / Oil)](#power-transformers-dry-type--oil)
10. [UPS Systems](#ups-systems)
11. [Automatic Transfer Switch (ATS)](#automatic-transfer-switch-ats)
12. [Power Factor Correction / Capacitor Banks](#power-factor-correction--capacitor-banks)
13. [VFD / Drive Panels](#vfd--drive-panels)
14. [Soft Starter Panels](#soft-starter-panels)
15. [Control Panels (PLC / Relay Logic)](#control-panels-plc--relay-logic)
16. [Motor Control Panels (standalone)](#motor-control-panels-standalone)
17. [Marshalling Cabinets](#marshalling-cabinets)
18. [Instrumentation Cabinets](#instrumentation-cabinets)
19. [Protection & Metering Panels](#protection--metering-panels)
20. [Battery & DC Panels](#battery--dc-panels)
21. [Emergency & Essential Boards](#emergency--essential-boards)
22. [Junction Boxes & Field Enclosures](#junction-boxes--field-enclosures)
23. [Busbar Chambers & Interconnections](#busbar-chambers--interconnections)
24. [Operator Stations & HMI Panels](#operator-stations--hmi-panels)
25. [Complete Single-Line Examples](#complete-single-line-examples)
26. [IEC Standards Quick Reference](#iec-standards-quick-reference)
27. [Common Mistakes for Panel Builders](#common-mistakes-for-panel-builders)
28. [Expert Tips for Panel Builders](#expert-tips-for-panel-builders)

---

## Fundamentals for Panel Builders

### EPLAN Structure for Panel Work
```
=   Function      → What the panel/device does
+   Location      → The panel or enclosure itself
-   Device        → The component inside the panel
```

### The Panel Builder's Primary Focus
For panel builders, the `+` location IS the panel. Most work lives at:
```
+PANEL_NAME               The panel as a location
+PANEL_NAME.SECTION       A section within the panel
+PANEL_NAME.SECTION.COMP  A compartment within a section
```

### Typical Panel Builder Tag Structure
```
=PWR+MSB1-Q1              Main incomer breaker Q1 in MSB1
=CTRL+MCC1.SEC_A-K5       Control relay K5 in section A of MCC1
=METER+MSB1.METER-PQ1     Power analyser PQ1 in metering section of MSB1
=SAFE+MCC1-F3             Motor protection relay F3 in MCC1
```

---

## Naming Philosophy

### Option A — Descriptive (most common for panel shops)
```
+MSB1          Main switchboard 1
+MCC1          Motor control centre 1
+DB_L1         Distribution board level 1
+RMU1          Ring main unit 1
+VFD_PNL1      VFD panel 1
+CP1           Control panel 1
```

### Option B — Alphanumeric (common for large projects)
```
+SW01          Switchboard 01
+MC01          MCC 01
+DB01          Distribution board 01
+RM01          RMU 01
+CP01          Control panel 01
```

### Option C — Client Asset Code (matches client register)
```
+11KV-SW-01    Client's 11kV switchboard tag
+415V-MCC-01   Client's 415V MCC tag
+DB-B1-L01     Client's DB tag for building 1 level 1
```

> **Expert rule:** Always ask the client for their naming convention before starting. If none exists, use Option A with consistent abbreviations agreed at kick-off.

---

## MV Switchgear (Medium Voltage)

> Voltage range: typically 3.3kV, 6.6kV, 11kV, 22kV, 33kV
> Standards: IEC 62271-200, IEC 62271-100

### Function Designations
```
=MV            MV switchgear system (general)
=MV.INC        Incoming feeder function
=MV.BUS        Busbar function
=MV.TIE        Bus section / tie function
=MV.FDR        Outgoing feeder function
=MV.TX         Transformer feeder function
=MV.MOTOR      MV motor feeder function
=MV.CAP        Capacitor bank feeder function
=MV.GEN        Generator incomer function
=MV.METERING   Metering function
=MV.PROT       Protection function
=MV.EARTH      Earthing switch function
```

### Location Designations
```
+MV_SW1                    MV switchboard 1 (top level)
+MV_SW1.INC_1              Incoming panel 1
+MV_SW1.INC_2              Incoming panel 2 (dual incomer)
+MV_SW1.BUS_SEC            Bus section panel
+MV_SW1.TIE                Bus tie panel
+MV_SW1.FDR_1              Feeder panel 1
+MV_SW1.FDR_2              Feeder panel 2
+MV_SW1.FDR_3              Feeder panel 3
+MV_SW1.FDR_4              Feeder panel 4
+MV_SW1.TX_FDR1            Transformer feeder panel 1
+MV_SW1.TX_FDR2            Transformer feeder panel 2
+MV_SW1.MTR_FDR1           MV motor feeder panel 1
+MV_SW1.MTR_FDR2           MV motor feeder panel 2
+MV_SW1.CAP_FDR1           Capacitor bank feeder panel 1
+MV_SW1.METER              Metering panel / VT panel
+MV_SW1.PROT               Protection relay panel (if separate)
+MV_SW1.CABLE_BOX          Cable termination box (rear)
+MV_SW1.CTRL_WIRING        Control wiring duct / space
```

### Full Tag Examples — MV Switchgear
```
=MV.INC+MV_SW1.INC_1-QB1        VCB (vacuum circuit breaker) in incoming panel 1
=MV.INC+MV_SW1.INC_1-ES1        Earthing switch in incoming panel 1
=MV.INC+MV_SW1.INC_1-CT1        Current transformer in incoming panel 1
=MV.INC+MV_SW1.INC_1-VT1        Voltage transformer in incoming panel 1
=MV.INC+MV_SW1.INC_1-F1         Protection relay (overcurrent/earth fault)
=MV.INC+MV_SW1.INC_1-PQ1        Power analyser / metering relay
=MV.TIE+MV_SW1.BUS_SEC-QB_TIE   Bus section VCB
=MV.TIE+MV_SW1.BUS_SEC-ES_TIE   Bus section earthing switch
=MV.FDR+MV_SW1.FDR_1-QB1        Feeder VCB in feeder panel 1
=MV.FDR+MV_SW1.FDR_1-F1         Feeder protection relay
=MV.TX+MV_SW1.TX_FDR1-QB1       Transformer feeder VCB
=MV.TX+MV_SW1.TX_FDR1-F1        Transformer protection relay (REF, overcurrent)
=MV.MOTOR+MV_SW1.MTR_FDR1-QB1   MV motor starter VCB
=MV.MOTOR+MV_SW1.MTR_FDR1-F1    Motor protection relay
=MV.METER+MV_SW1.METER-VT1      Metering VT panel
=MV.METER+MV_SW1.METER-KWH1     kWh meter (fiscal / check metering)
```

### MV Switchgear Internal Device Naming (common)
```
QB          Vacuum/SF6 circuit breaker
QD          Disconnector / isolator
ES          Earthing switch
CT          Current transformer
VT          Voltage transformer (potential transformer)
F           Protection relay (general)
F_OC        Overcurrent relay
F_EF        Earth fault relay
F_DIFF      Differential relay
F_DIST      Distance relay
F_REF       Restricted earth fault relay
PQ          Power quality / power analyser
KWH         Energy meter
K           Auxiliary relay
X           Terminal block
HL          Indicating lamp
SB          Push button
SS          Selector switch
```

---

## LV Main Switchboard (MSB)

> Voltage: 400V / 415V / 690V AC
> Standards: IEC 61439-1, IEC 61439-2 (formerly IEC 60439)

### Function Designations
```
=PWR           Power distribution (general)
=PWR.INC       Incoming supply function
=PWR.BUS       Busbar function
=PWR.TIE       Bus tie / coupler function
=PWR.FDR       Outgoing feeder function
=PWR.EMERG     Emergency / essential supply
=METER         Metering and power quality
=PROT          Protection function
=CTRL          Control and interlocking
=SAFE          Safety and interlocking
```

### Location Designations — MSB Forms

#### Form 1 / Form 2 MSB (open busbars, simple)
```
+MSB1                     Main switchboard 1
+MSB1.INC                 Incoming section
+MSB1.BUS                 Busbar section
+MSB1.TIE                 Bus tie section
+MSB1.FDR                 Outgoing feeders section
+MSB1.METER               Metering section
```

#### Form 3b / Form 4b MSB (fully compartmentalised)
```
+MSB1                     Main switchboard 1
+MSB1.INC_A               Incomer A (left incomer)
+MSB1.INC_B               Incomer B (right incomer / generator)
+MSB1.BUS_A               Busbar chamber A
+MSB1.BUS_B               Busbar chamber B
+MSB1.TIE                 Bus coupler section
+MSB1.FDR_1               Feeder 1 compartment
+MSB1.FDR_2               Feeder 2 compartment
+MSB1.FDR_3               Feeder 3 compartment
+MSB1.FDR_4               Feeder 4 compartment
+MSB1.FDR_5               Feeder 5 compartment
+MSB1.FDR_6               Feeder 6 compartment
+MSB1.MCC_FDR1            MCC feeder compartment 1
+MSB1.MCC_FDR2            MCC feeder compartment 2
+MSB1.DB_FDR1             DB feeder compartment 1
+MSB1.DB_FDR2             DB feeder compartment 2
+MSB1.TRANS_FDR1          Transformer feeder (dry-type LV-LV)
+MSB1.UPS_FDR             UPS feeder compartment
+MSB1.GEN_FDR             Generator incomer compartment
+MSB1.ATS                 ATS / changeover section
+MSB1.METER               Metering compartment
+MSB1.CTRL                Control and indication compartment
+MSB1.BUSDUCT             Busduct / busbar trunking connection point
```

### Full Tag Examples — MSB
```
=PWR.INC+MSB1.INC_A-QF_INC_A     Main incomer MCCB/ACB incomer A
=PWR.INC+MSB1.INC_A-CT1          Incomer A current transformer
=PWR.INC+MSB1.INC_A-VT1          Incomer A voltage transformer
=METER+MSB1.INC_A-PQ1            Power analyser on incomer A
=PWR.TIE+MSB1.TIE-QF_TIE         Bus coupler ACB
=PWR.FDR+MSB1.FDR_1-QF1          Feeder 1 MCCB
=PWR.FDR+MSB1.FDR_1-CT1          Feeder 1 CT (if metered)
=CTRL+MSB1.CTRL-K_INC_A          Incomer A auxiliary relay
=CTRL+MSB1.CTRL-K_TIE            Bus tie interlock relay
=SAFE+MSB1.CTRL-K_ATS            ATS changeover relay
=METER+MSB1.METER-PQ_MAIN        Main power quality analyser
=METER+MSB1.METER-KWH_MAIN       Main energy meter
=CTRL+MSB1.INC_A-SS_LOCAL        Local/remote selector switch
=CTRL+MSB1.INC_A-HL_CLOSED       Breaker closed indicator lamp
=CTRL+MSB1.INC_A-HL_OPEN         Breaker open indicator lamp
=CTRL+MSB1.INC_A-HL_TRIP         Breaker trip indicator lamp
=CTRL+MSB1.INC_A-SB_CLOSE        Breaker close push button
=CTRL+MSB1.INC_A-SB_OPEN         Breaker open push button
=CTRL+MSB1.INC_A-SB_RESET        Breaker reset push button
```

### Two-Incomer + Bus Tie (2i+BT) MSB — common layout
```
+MSB1.INC_A       Incomer A (utility supply)
+MSB1.INC_B       Incomer B (generator / second utility)
+MSB1.TIE         Bus tie coupler
+MSB1.BUS_A       Busbar section A
+MSB1.BUS_B       Busbar section B
+MSB1.FDR_A1      Feeder on bus A — position 1
+MSB1.FDR_A2      Feeder on bus A — position 2
+MSB1.FDR_A3      Feeder on bus A — position 3
+MSB1.FDR_B1      Feeder on bus B — position 1
+MSB1.FDR_B2      Feeder on bus B — position 2
+MSB1.FDR_B3      Feeder on bus B — position 3
+MSB1.CTRL        Control and interlocking section
+MSB1.METER       Metering section
```

---

## Motor Control Centre (MCC)

> Standards: IEC 61439-1, IEC 61439-2, IEC 60947-4
> Draw-out or fixed type. Fixed plug-in (FPI) or withdrawable.

### Function Designations
```
=PWR           Power distribution through MCC
=PWR.INC       MCC incomer function
=PWR.BUS       MCC busbar function
=MOTOR         Motor feeder / starter function
=MOTOR.DOL     Direct-on-line starter function
=MOTOR.STAR_D  Star-delta starter function
=MOTOR.VFD     Variable frequency drive function
=MOTOR.SOFT    Soft starter function
=MOTOR.RDOL    Reversing DOL function
=CTRL          Control section function
=SAFE          Motor protection function
=METER         Motor / feeder metering
=HEAT          Enclosure heating function
=LIGHT         Panel lighting function
```

### Location Designations — MCC Structure

#### Vertical Section Based (most common)
```
+MCC1                     MCC 1 (top level)
+MCC1.INC                 Incoming section (usually leftmost)
+MCC1.SEC_1               Vertical section 1
+MCC1.SEC_2               Vertical section 2
+MCC1.SEC_3               Vertical section 3
+MCC1.SEC_4               Vertical section 4
+MCC1.SEC_5               Vertical section 5
+MCC1.CTRL_SEC            Control / PLC section (if integrated)
```

#### Within a Vertical Section — Compartment / Drawer Level
```
+MCC1.SEC_1.C01           Compartment 01 in section 1 (top)
+MCC1.SEC_1.C02           Compartment 02 in section 1
+MCC1.SEC_1.C03           Compartment 03 in section 1
+MCC1.SEC_1.C04           Compartment 04 in section 1
+MCC1.SEC_1.C05           Compartment 05 in section 1 (bottom)
+MCC1.SEC_1.CABLE_SPACE   Cable compartment in section 1
+MCC1.SEC_1.BUS           Busbar compartment in section 1
```

#### Feeder / Starter Named Approach (alternative — used when motor tags are known)
```
+MCC1                     MCC 1
+MCC1.INC                 Incoming section
+MCC1.M01                 Motor feeder 01 (for motor M01)
+MCC1.M02                 Motor feeder 02
+MCC1.M03                 Motor feeder 03
+MCC1.M04                 Motor feeder 04
+MCC1.M05                 VFD feeder for motor M05
+MCC1.M06                 Soft starter feeder for motor M06
+MCC1.P01                 Pump P01 feeder
+MCC1.P02                 Pump P02 feeder
+MCC1.FAN01               Fan 01 feeder
+MCC1.COMP01              Compressor 01 feeder
+MCC1.CTRL                PLC / controls drawer
+MCC1.DIST                24VDC distribution section
```

### Full Tag Examples — MCC (DOL Starter)
```
=PWR.INC+MCC1.INC-QF_INC         MCC incomer MCCB
=PWR.INC+MCC1.INC-CT1            Incomer CT
=METER+MCC1.INC-PQ1              Incomer power analyser
=MOTOR.DOL+MCC1.M01-QF1          Motor M01 feeder MCCB
=MOTOR.DOL+MCC1.M01-F1           Motor M01 protection relay (overload/phase loss)
=MOTOR.DOL+MCC1.M01-KM1          Motor M01 main contactor
=MOTOR.DOL+MCC1.M01-KM1_AUX      Motor M01 auxiliary contactor
=CTRL+MCC1.M01-SS_LOCAL          Motor M01 local/remote selector
=CTRL+MCC1.M01-SB_START          Motor M01 start push button
=CTRL+MCC1.M01-SB_STOP           Motor M01 stop push button
=CTRL+MCC1.M01-HL_RUN            Motor M01 run indication lamp
=CTRL+MCC1.M01-HL_TRIP           Motor M01 trip indication lamp
=CTRL+MCC1.M01-HL_READY          Motor M01 ready indication lamp
=SAFE+MCC1.M01-F1                Motor protection relay (thermal overload)
=METER+MCC1.M01-PQ1              Motor M01 individual power meter (if metered)
```

### Full Tag Examples — MCC (Star-Delta Starter)
```
=MOTOR.STAR_D+MCC1.M02-QF1       Star-delta feeder MCCB
=MOTOR.STAR_D+MCC1.M02-F1        Overload relay
=MOTOR.STAR_D+MCC1.M02-KM_MAIN   Main contactor (line)
=MOTOR.STAR_D+MCC1.M02-KM_STAR   Star contactor
=MOTOR.STAR_D+MCC1.M02-KM_DELTA  Delta contactor
=MOTOR.STAR_D+MCC1.M02-KT1       Star-delta timer relay
=CTRL+MCC1.M02-SS_LOCAL          Local/remote selector
=CTRL+MCC1.M02-SB_START          Start push button
=CTRL+MCC1.M02-SB_STOP           Stop push button
=CTRL+MCC1.M02-HL_STAR           Star mode indicator
=CTRL+MCC1.M02-HL_DELTA          Delta mode indicator
=CTRL+MCC1.M02-HL_TRIP           Trip indicator
```

### Full Tag Examples — MCC (VFD Drawer)
```
=MOTOR.VFD+MCC1.M03-QF1          VFD incomer MCCB
=MOTOR.VFD+MCC1.M03-F1           Motor protection relay
=MOTOR.VFD+MCC1.M03-VFD1         Variable frequency drive unit
=MOTOR.VFD+MCC1.M03-QF_BP        Bypass MCCB (if bypass fitted)
=MOTOR.VFD+MCC1.M03-KM_VFD       VFD output contactor
=MOTOR.VFD+MCC1.M03-KM_BP        Bypass contactor (if bypass fitted)
=MOTOR.VFD+MCC1.M03-EMC1         EMC filter / line reactor
=MOTOR.VFD+MCC1.M03-KS1          VFD/bypass interlock relay
=CTRL+MCC1.M03-SS_VFD_BP         VFD / bypass selector switch
=CTRL+MCC1.M03-SS_LOCAL          Local / remote selector
=CTRL+MCC1.M03-SB_START          Start push button (local)
=CTRL+MCC1.M03-SB_STOP           Stop push button (local)
=CTRL+MCC1.M03-HL_RUN            Run indicator
=CTRL+MCC1.M03-HL_FAULT          VFD fault indicator
```

### MCC with Integrated PLC Section
```
+MCC1.CTRL_SEC            Control/PLC section (rightmost)
+MCC1.CTRL_SEC.PLC        PLC mounting area
+MCC1.CTRL_SEC.DIST       24VDC distribution area
+MCC1.CTRL_SEC.IO         I/O modules area
+MCC1.CTRL_SEC.RELAY      Relay area
+MCC1.CTRL_SEC.TERM       Terminal area
+MCC1.CTRL_SEC.COMM       Communications / fieldbus modules
```

---

## Distribution Boards (DB)

> Standards: IEC 61439-3 (consumer DBs), IEC 61439-1/2 (industrial DBs)

### Function Designations
```
=PWR           Power distribution
=PWR.INC       Incomer function
=PWR.LIGHT     Lighting circuit function
=PWR.POWER     Power outlet circuit function
=PWR.HVAC      HVAC circuit function
=PWR.EMERG     Emergency circuit function
=PWR.SMALL_PWR Small power / data circuits
=METER         Sub-metering function
=SAFE          RCD / RCBO protection function
```

### Location Designations — Types of Distribution Boards

#### Main Distribution Board (MDB)
```
+MDB1                     Main distribution board 1
+MDB1.INC                 Incomer section
+MDB1.BUS                 Busbar section
+MDB1.LIGHT               Lighting circuits section
+MDB1.POWER               Power circuits section
+MDB1.HVAC                HVAC circuits section
+MDB1.EMERG               Emergency circuits section
+MDB1.SPARES              Spare ways section
+MDB1.METER               Sub-meter section
```

#### Sub-Distribution Board (SDB)
```
+SDB_L1                   Sub DB for Level 1
+SDB_L1.INC               Incomer (fed from MDB or riser)
+SDB_L1.LIGHT             Lighting circuits
+SDB_L1.GPO               General power outlets
+SDB_L1.HVAC              FCU / VAV circuits
+SDB_L1.CRIT              Critical / essential loads
+SDB_L2                   Sub DB for Level 2
+SDB_L2.INC               Incomer
+SDB_L2.LIGHT             Lighting circuits
+SDB_L2.GPO               General power outlets
```

#### Industrial / Process DB
```
+IDB1                     Industrial distribution board 1
+IDB1.INC                 Incomer MCCB / isolator
+IDB1.FDR_1               Feeder 1 (to panel CP1)
+IDB1.FDR_2               Feeder 2 (to panel CP2)
+IDB1.FDR_3               Feeder 3 (to JB1)
+IDB1.FDR_4               Feeder 4 (to field sockets)
+IDB1.FDR_5               Feeder 5 (to HVAC)
+IDB1.LIGHT               Panel lighting circuit
+IDB1.HEAT                Panel heating circuit
+IDB1.24VDC               24VDC SMPS and distribution
+IDB1.CTRL                Control MCBs (PLC, HMI power)
```

#### Essential Distribution Board (EDB)
```
+EDB1                     Essential distribution board 1
+EDB1.INC_NORM            Normal supply incomer (from MSB)
+EDB1.INC_EMERG           Emergency supply incomer (from ATS/UPS/generator)
+EDB1.ATS                 Automatic transfer switch section
+EDB1.FDR_1               Essential feeder 1
+EDB1.FDR_2               Essential feeder 2
+EDB1.FDR_3               Essential feeder 3
+EDB1.UPS_FDR             UPS-backed feeder
+EDB1.CRIT                Critical / life safety circuits
```

### Full Tag Examples — DB
```
=PWR.INC+MDB1.INC-QF_INC              Main incomer MCCB
=METER+MDB1.INC-KWH1                  Main energy meter
=SAFE+MDB1.INC-RCD_MAIN               Main RCD (if fitted)
=PWR.LIGHT+MDB1.LIGHT-MCB_L1          Lighting circuit 1 MCB
=PWR.LIGHT+MDB1.LIGHT-MCB_L2          Lighting circuit 2 MCB
=PWR.POWER+MDB1.POWER-MCB_P1          Power circuit 1 MCB
=PWR.POWER+MDB1.POWER-RCBO_P1         Power circuit 1 RCBO (RCD+MCB)
=PWR.HVAC+MDB1.HVAC-MCB_H1            HVAC circuit 1 MCB
=PWR.EMERG+MDB1.EMERG-MCB_E1          Emergency lighting circuit 1
=METER+MDB1.METER-KWH_LIGHT           Lighting sub-meter
=METER+MDB1.METER-KWH_POWER           Power sub-meter
```

---

## Ring Main Unit (RMU)

> Used for MV cable ring / radial distribution
> Standards: IEC 62271-200, IEC 62271-105
> Common types: 2-way, 3-way, 4-way (2 ring + 1 transformer feeder + 1 spare)

### Function Designations
```
=MV.RING       Ring circuit function
=MV.TX         Transformer feeder function
=MV.METER      Metering function
=MV.EARTH      Earthing function
```

### Location Designations — RMU
```
+RMU1                     Ring main unit 1
+RMU1.RING_IN             Ring incomer (from upstream)
+RMU1.RING_OUT            Ring outgoing (to next RMU)
+RMU1.TX_FDR              Transformer feeder (fuse/switch or VCB)
+RMU1.TX_FDR2             Second transformer feeder (if 4-way)
+RMU1.SPARE               Spare way
+RMU1.METER               Metering cubicle (if fitted)
+RMU1.CTRL                Control / protection (if numeric relay fitted)

+RMU2                     Ring main unit 2
+RMU2.RING_IN             Ring incomer
+RMU2.RING_OUT            Ring outgoing
+RMU2.TX_FDR              Transformer feeder

+RMU3                     Ring main unit 3 (end of ring / normally open point)
+RMU3.RING_IN_A           Ring incomer from circuit A
+RMU3.RING_IN_B           Ring incomer from circuit B (NOP)
+RMU3.TX_FDR              Transformer feeder
```

### Full Tag Examples — RMU
```
=MV.RING+RMU1.RING_IN-QS1        Ring incomer load break switch
=MV.RING+RMU1.RING_IN-ES1        Earthing switch on ring incomer
=MV.RING+RMU1.RING_OUT-QS2       Ring outgoing load break switch
=MV.RING+RMU1.RING_OUT-ES2       Earthing switch on ring outgoing
=MV.TX+RMU1.TX_FDR-QS3          TX feeder load break switch
=MV.TX+RMU1.TX_FDR-FU1          HRC fuse (if fused type)
=MV.TX+RMU1.TX_FDR-QB1          VCB (if VCB type with protection)
=MV.TX+RMU1.TX_FDR-F1           Protection relay (if VCB type)
=MV.TX+RMU1.TX_FDR-ES3          TX feeder earthing switch
=MV.METER+RMU1.METER-CT1        Metering CT
=MV.METER+RMU1.METER-VT1        Metering VT
=MV.METER+RMU1.METER-KWH1       kWh meter
=MV.EARTH+RMU1.RING_IN-ES1      Earthing switch (general)
```

### RMU Network Topology Example
```
Substation  →  +RMU1  →  +RMU2  →  +RMU3 (NOP)  ←  +RMU4  ←  Substation
                 ↓           ↓           ↓               ↓
               TX_A        TX_B        TX_C            TX_D
              +TX_A       +TX_B       +TX_C           +TX_D
              +MSB_A      +MSB_B      +MSB_C          +MSB_D
```

---

## Busbar Trunking System (BTS)

> Standards: IEC 61439-6
> Used for HV-to-LV transformer to MSB connections, riser systems, and high-current distribution

### Function Designations
```
=PWR.BTS       Busbar trunking function
=PWR.BTS.RISER Riser section function
=PWR.BTS.FDR   Tap-off / feeder function
```

### Location Designations
```
+BTS1                     Busbar trunking system 1
+BTS1.FEED_END            Feeding end (transformer or MSB connection)
+BTS1.RISER               Riser section (vertical run)
+BTS1.RISER.L1            Riser at level 1
+BTS1.RISER.L2            Riser at level 2
+BTS1.RISER.L3            Riser at level 3
+BTS1.RISER.L4            Riser at level 4
+BTS1.TAP_L1              Tap-off unit at level 1
+BTS1.TAP_L2              Tap-off unit at level 2
+BTS1.TAP_L3              Tap-off unit at level 3
+BTS1.DIST_RUN            Horizontal distribution run
+BTS1.TAP_A               Tap-off unit A (horizontal)
+BTS1.TAP_B               Tap-off unit B
+BTS1.END_CAP             End cap / termination
+BTS2                     Busbar trunking system 2 (parallel riser)
```

### Full Tag Examples — BTS
```
=PWR.BTS+BTS1.FEED_END-X1        Busbar feed-end connector/joint
=PWR.BTS.FDR+BTS1.TAP_L1-QF1    Tap-off MCB/MCCB at level 1
=PWR.BTS.FDR+BTS1.TAP_L2-QF1    Tap-off MCB/MCCB at level 2
=METER+BTS1.FEED_END-PQ1         Power analyser at feed end
=METER+BTS1.TAP_L1-KWH1         Sub-meter at level 1 tap-off
```

---

## Power Transformers (Dry Type / Oil)

> Standards: IEC 60076 (oil), IEC 60076-11 (dry type)
> Note: In EPLAN, transformer LV and HV panels/terminations are the focus

### Function Designations
```
=TX            Transformer function
=TX.HV         HV side function
=TX.LV         LV side function
=TX.COOL       Cooling system function
=TX.PROT       Protection function
=TX.EARTH      Earthing function
```

### Location Designations
```
+TX1                      Transformer 1 (the unit itself)
+TX1.HV_TERM              HV termination box / cable box
+TX1.LV_TERM              LV termination box / cable box
+TX1.MARSHALLING          Marshalling box (protection wiring)
+TX1.COOL                 Cooling fans / radiators (oil type)
+TX1.OLTC                 On-load tap changer (if fitted)
+TX1.OLTC.CTRL            OLTC controller
+TX1.BODY                 Transformer tank / enclosure
+TX1.BUND                 Bunding / oil containment area

+TX2                      Transformer 2
+TX2.HV_TERM              HV termination box
+TX2.LV_TERM              LV termination box
```

### Full Tag Examples — Transformer
```
=TX.HV+TX1.HV_TERM-X1            HV cable termination terminal
=TX.LV+TX1.LV_TERM-X1            LV cable termination terminal (busbar)
=TX.PROT+TX1.MARSHALLING-F_DIFF  Differential protection relay
=TX.PROT+TX1.MARSHALLING-F_BUCHH Buchholz relay (oil transformer)
=TX.PROT+TX1.MARSHALLING-F_WTI   Winding temperature indicator
=TX.PROT+TX1.MARSHALLING-F_OTI   Oil temperature indicator
=TX.PROT+TX1.MARSHALLING-F_OSL   Oil surge relay / PRV
=TX.PROT+TX1.MARSHALLING-F_PRD   Pressure relief device
=TX.COOL+TX1.COOL-KM1            Cooling fan contactor
=TX.COOL+TX1.COOL-F1             Fan overload protection
=TX.OLTC+TX1.OLTC.CTRL-AVR1      Automatic voltage regulator
=TX.EARTH+TX1.BODY-E1            Transformer body earthing
```

---

## UPS Systems

> Standards: IEC 62040 series
> Types: online double-conversion, line-interactive, static bypass, modular

### Function Designations
```
=PWR.UPS       UPS function (overall)
=PWR.UPS.RECT  Rectifier function
=PWR.UPS.BATT  Battery function
=PWR.UPS.INV   Inverter function
=PWR.UPS.BYP   Static bypass function
=PWR.UPS.MBP   Manual maintenance bypass function
=PWR.UPS.DIST  UPS distribution function
=BATT          Battery bank function
=CTRL          UPS monitoring and control
```

### Location Designations
```
+UPS1                     UPS system 1 (complete)
+UPS1.UPS_UNIT            UPS main unit enclosure
+UPS1.UPS_UNIT.RECT       Rectifier section
+UPS1.UPS_UNIT.INV        Inverter section
+UPS1.UPS_UNIT.STS        Static transfer switch section
+UPS1.UPS_UNIT.MBP        Maintenance bypass section
+UPS1.BATT_CAB1           Battery cabinet 1
+UPS1.BATT_CAB2           Battery cabinet 2
+UPS1.BATT_CAB3           Battery cabinet 3
+UPS1.DIST_BOARD          UPS output distribution board
+UPS1.DIST_BOARD.FDR_1    UPS feeder 1
+UPS1.DIST_BOARD.FDR_2    UPS feeder 2
+UPS1.DIST_BOARD.FDR_3    UPS feeder 3
+UPS1.DIST_BOARD.FDR_4    UPS feeder 4
+UPS1.INPUT_PANEL         UPS input isolation panel
+UPS1.BYPASS_PANEL        External bypass panel (if separate)
+UPS2                     UPS system 2 (parallel / redundant)
+UPS2.UPS_UNIT            UPS 2 main unit
+UPS2.BATT_CAB1           UPS 2 battery cabinet 1
```

### Full Tag Examples — UPS
```
=PWR.UPS+UPS1.INPUT_PANEL-QF_IN     UPS input MCCB / isolator
=PWR.UPS.RECT+UPS1.UPS_UNIT.RECT-F1 Rectifier protection
=PWR.UPS.INV+UPS1.UPS_UNIT.INV-F1   Inverter protection
=PWR.UPS.BYP+UPS1.UPS_UNIT.STS-QS1  Static bypass switch
=PWR.UPS.MBP+UPS1.UPS_UNIT.MBP-QS_MBP  Maintenance bypass switch
=BATT+UPS1.BATT_CAB1-F_BATT         Battery fuse / disconnect
=BATT+UPS1.BATT_CAB1-BMS1           Battery management system module
=CTRL+UPS1.UPS_UNIT-PLC_UPS         UPS controller / monitoring card
=CTRL+UPS1.UPS_UNIT-HL_NORMAL       Normal operation indicator
=CTRL+UPS1.UPS_UNIT-HL_BATT         On battery indicator
=CTRL+UPS1.UPS_UNIT-HL_FAULT        Fault indicator
=PWR.UPS.DIST+UPS1.DIST_BOARD.FDR_1-QF1  UPS feeder 1 MCB
=PWR.UPS.DIST+UPS1.DIST_BOARD.FDR_2-QF2  UPS feeder 2 MCB
=METER+UPS1.DIST_BOARD-PQ1          UPS output power analyser
```

---

## Automatic Transfer Switch (ATS)

> Standards: IEC 60947-6-1, IEC 62580
> Types: Open transition (break-before-make), closed transition (make-before-break)

### Function Designations
```
=PWR.ATS       ATS function (overall)
=PWR.ATS.NORM  Normal supply function
=PWR.ATS.ALT   Alternative supply function (generator/second utility)
=PWR.ATS.LOAD  Load side function
=CTRL.ATS      ATS control logic function
```

### Location Designations
```
+ATS1                     ATS panel 1
+ATS1.NORM_INC            Normal supply incomer section
+ATS1.ALT_INC             Alternative supply incomer section (generator)
+ATS1.TRANSFER            Transfer switch mechanism section
+ATS1.LOAD                Load side section
+ATS1.CTRL                Control logic section
+ATS1.METER               Metering section

+ATS2                     ATS panel 2 (if multiple)
```

### Full Tag Examples — ATS
```
=PWR.ATS.NORM+ATS1.NORM_INC-QF_NORM    Normal supply MCCB
=PWR.ATS.ALT+ATS1.ALT_INC-QF_ALT       Generator supply MCCB
=PWR.ATS+ATS1.TRANSFER-QS_NORM         Normal supply isolator/contactor
=PWR.ATS+ATS1.TRANSFER-QS_ALT          Alternative supply isolator/contactor
=PWR.ATS.LOAD+ATS1.LOAD-X_LOAD         Load output terminals
=CTRL.ATS+ATS1.CTRL-K_NORM             Normal supply sensing relay
=CTRL.ATS+ATS1.CTRL-K_ALT              Alternative supply sensing relay
=CTRL.ATS+ATS1.CTRL-KT1               Transfer timer (delay on transfer)
=CTRL.ATS+ATS1.CTRL-KT2               Retransfer timer (delay on retransfer)
=CTRL.ATS+ATS1.CTRL-SS_AUTO           Auto/manual selector
=CTRL.ATS+ATS1.CTRL-HL_NORM           Normal supply available indicator
=CTRL.ATS+ATS1.CTRL-HL_ALT            Generator supply available indicator
=CTRL.ATS+ATS1.CTRL-HL_ON_NORM        On normal supply indicator
=CTRL.ATS+ATS1.CTRL-HL_ON_ALT         On alternative supply indicator
=METER+ATS1.METER-PQ_NORM             Normal supply power analyser
=METER+ATS1.METER-PQ_ALT              Alternative supply power analyser
```

---

## Power Factor Correction / Capacitor Banks

> Standards: IEC 60831, IEC 61921
> Types: Fixed, automatic stepped (APFC), detuned (with reactors)

### Function Designations
```
=PWR.PFC       Power factor correction function
=PWR.PFC.INC   Incomer function
=PWR.PFC.STEP  Individual capacitor step function
=PWR.PFC.REACT Detuning reactor function
=PWR.PFC.CTRL  PFC controller function
```

### Location Designations
```
+PFC1                     PFC / capacitor bank panel 1
+PFC1.INC                 Incomer section
+PFC1.CTRL                Controller section
+PFC1.STEP_1              Capacitor step 1 (fixed or switched)
+PFC1.STEP_2              Capacitor step 2
+PFC1.STEP_3              Capacitor step 3
+PFC1.STEP_4              Capacitor step 4
+PFC1.STEP_5              Capacitor step 5
+PFC1.STEP_6              Capacitor step 6
+PFC1.REACT               Detuning reactor section (if detuned)
+PFC1.DISCHARGE           Discharge resistor section
+PFC1.FILTER              Harmonic filter section (if combined)
```

### Full Tag Examples — PFC
```
=PWR.PFC.INC+PFC1.INC-QF_INC         PFC incomer MCCB
=PWR.PFC.INC+PFC1.INC-CT1            Incomer CT (for PF measurement)
=PWR.PFC.CTRL+PFC1.CTRL-PFC_CTRL1    Power factor controller relay
=PWR.PFC.STEP+PFC1.STEP_1-QF1        Step 1 MCB/fuse
=PWR.PFC.STEP+PFC1.STEP_1-KM1        Step 1 contactor
=PWR.PFC.STEP+PFC1.STEP_1-C1         Capacitor bank step 1
=PWR.PFC.REACT+PFC1.STEP_1-L1        Step 1 detuning reactor
=PWR.PFC.STEP+PFC1.STEP_2-QF2        Step 2 MCB/fuse
=PWR.PFC.STEP+PFC1.STEP_2-KM2        Step 2 contactor
=PWR.PFC.STEP+PFC1.STEP_2-C2         Capacitor bank step 2
=METER+PFC1.INC-PQ1                  Power analyser (PF monitoring)
```

---

## VFD / Drive Panels

> Standards: IEC 61800 series
> Standalone VFD panels or multi-drive panels

### Function Designations
```
=DRIVE         Drive system function (overall)
=DRIVE.INC     Drive panel incomer function
=DRIVE.VFD     Individual VFD function
=DRIVE.BRAKE   Braking function
=DRIVE.FILTER  EMC filter / reactor function
=DRIVE.BYP     Bypass function
=CTRL          Drive control function
```

### Location Designations
```
+VFD_PNL1                 VFD panel 1 (standalone or multi-drive)
+VFD_PNL1.INC             Incomer section
+VFD_PNL1.VFD_1           VFD 1 section / drive 1
+VFD_PNL1.VFD_2           VFD 2 section / drive 2
+VFD_PNL1.VFD_3           VFD 3 section
+VFD_PNL1.BRAKE_1         Braking resistor section for VFD 1
+VFD_PNL1.FILTER_1        EMC filter / line reactor for VFD 1
+VFD_PNL1.BYP_1           Bypass section for VFD 1
+VFD_PNL1.CTRL            Control section (PLC, HMI, terminals)
+VFD_PNL1.DIST            24VDC distribution section
```

### Full Tag Examples — VFD Panel
```
=DRIVE.INC+VFD_PNL1.INC-QF_INC       Panel incomer MCCB
=DRIVE.VFD+VFD_PNL1.VFD_1-QF1        VFD 1 input MCCB
=DRIVE.FILTER+VFD_PNL1.FILTER_1-EMC1 EMC filter / line reactor
=DRIVE.VFD+VFD_PNL1.VFD_1-VFD1       VFD 1 unit (drive module)
=DRIVE.VFD+VFD_PNL1.VFD_1-KM_OUT1    VFD 1 output contactor
=DRIVE.BRAKE+VFD_PNL1.BRAKE_1-RB1    Braking resistor
=DRIVE.BYP+VFD_PNL1.BYP_1-QF_BP1     Bypass MCCB
=DRIVE.BYP+VFD_PNL1.BYP_1-KM_BP1     Bypass contactor
=CTRL+VFD_PNL1.CTRL-SS_VFD_BP1       VFD/bypass selector
=CTRL+VFD_PNL1.CTRL-HL_RUN1          VFD 1 run indicator
=CTRL+VFD_PNL1.CTRL-HL_FAULT1        VFD 1 fault indicator
=CTRL+VFD_PNL1.CTRL-SB_RESET1        VFD 1 fault reset button
=CTRL+VFD_PNL1.CTRL-PLC1             Panel PLC (for multi-drive coordination)
```

---

## Soft Starter Panels

> Standards: IEC 60947-4-2
> Inline or bypass type

### Function Designations
```
=MOTOR.SOFT    Soft starter function
=MOTOR.SOFT.INC  Incomer function
=MOTOR.SOFT.BYP  Bypass contactor function
=CTRL          Control function
```

### Location Designations
```
+SOFT_PNL1                Soft starter panel 1
+SOFT_PNL1.INC            Incomer section
+SOFT_PNL1.SOFT_1         Soft starter 1 section
+SOFT_PNL1.SOFT_2         Soft starter 2 section
+SOFT_PNL1.BYP_1          Bypass contactor section for starter 1
+SOFT_PNL1.CTRL           Control section
```

### Full Tag Examples — Soft Starter
```
=MOTOR.SOFT.INC+SOFT_PNL1.INC-QF_INC        Panel incomer MCCB
=MOTOR.SOFT+SOFT_PNL1.SOFT_1-QF1            Soft starter 1 input MCCB
=MOTOR.SOFT+SOFT_PNL1.SOFT_1-F1             Overload relay / motor protection
=MOTOR.SOFT+SOFT_PNL1.SOFT_1-SS1            Soft starter unit
=MOTOR.SOFT.BYP+SOFT_PNL1.BYP_1-KM_RUN1    Run bypass contactor
=MOTOR.SOFT.BYP+SOFT_PNL1.BYP_1-KM_BP1     Bypass / delta contactor (inline type)
=CTRL+SOFT_PNL1.CTRL-SS_LOCAL1              Local/remote selector starter 1
=CTRL+SOFT_PNL1.CTRL-SB_START1              Start push button starter 1
=CTRL+SOFT_PNL1.CTRL-SB_STOP1              Stop push button starter 1
=CTRL+SOFT_PNL1.CTRL-HL_RUN1               Run indicator starter 1
=CTRL+SOFT_PNL1.CTRL-HL_FAULT1             Fault indicator starter 1
```

---

## Control Panels (PLC / Relay Logic)

> The most common panel type for machine builders and system integrators

### Function Designations
```
=CTRL          Control system function
=CTRL.PLC      PLC function
=CTRL.IO       I/O function
=CTRL.HMI      HMI function
=CTRL.COMM     Communications function
=CTRL.RELAY    Relay logic function
=CTRL.TIMER    Timer function
=CTRL.SAFE     Safety controller function
=PWR.CTRL      Control power distribution
=PWR.24V       24VDC power function
=SAFE          Safety function
=SAFE.ESTOP    Emergency stop function
=SAFE.GUARD    Guard monitoring function
```

### Location Designations
```
+CP1                      Control panel 1
+CP1.POWER                Power supply section
+CP1.PLC                  PLC mounting section
+CP1.IO                   I/O modules section
+CP1.RELAY                Relay section
+CP1.SAFE                 Safety relay section
+CP1.COMM                 Communications / network section
+CP1.DIST_24V             24VDC distribution section
+CP1.TERM                 Terminal section (field wiring)
+CP1.TERM.DI              Digital input terminals
+CP1.TERM.DO              Digital output terminals
+CP1.TERM.AI              Analog input terminals
+CP1.TERM.AO              Analog output terminals
+CP1.TERM.SAFE            Safety terminal section
+CP1.TERM.COMM            Communications terminals
+CP1.DOOR                 Door-mounted devices
+CP1.DOOR.HMI             HMI touchscreen on door
+CP1.DOOR.OP              Operator devices (buttons, lamps, selectors)
```

### Full Tag Examples — Control Panel
```
=PWR.CTRL+CP1.POWER-QF_MAINS         Mains power MCB to panel
=PWR.CTRL+CP1.POWER-T1               Control transformer (230V→24VAC if needed)
=PWR.24V+CP1.POWER-PS1               24VDC SMPS power supply 1
=PWR.24V+CP1.POWER-PS2               24VDC SMPS power supply 2 (redundant)
=PWR.24V+CP1.POWER-UPS_MOD           24VDC UPS buffer module
=PWR.24V+CP1.DIST_24V-QF_PLC         24VDC MCB for PLC
=PWR.24V+CP1.DIST_24V-QF_IO          24VDC MCB for I/O modules
=PWR.24V+CP1.DIST_24V-QF_FIELD       24VDC MCB for field devices
=PWR.24V+CP1.DIST_24V-QF_SAFE        24VDC MCB for safety system
=CTRL.PLC+CP1.PLC-CPU1               PLC CPU module
=CTRL.IO+CP1.IO-DI01                 Digital input module 01
=CTRL.IO+CP1.IO-DI02                 Digital input module 02
=CTRL.IO+CP1.IO-DO01                 Digital output module 01
=CTRL.IO+CP1.IO-DO02                 Digital output module 02
=CTRL.IO+CP1.IO-AI01                 Analog input module 01
=CTRL.IO+CP1.IO-AO01                 Analog output module 01
=CTRL.COMM+CP1.COMM-CM_PN            PROFINET communications module
=CTRL.COMM+CP1.COMM-CM_ETH           Ethernet switch / module
=CTRL.COMM+CP1.COMM-CM_RS485         RS485 / Modbus module
=CTRL.HMI+CP1.DOOR.HMI-TP1          HMI touchpanel on door
=SAFE+CP1.SAFE-F3_SAFE               Safety relay module
=SAFE.ESTOP+CP1.SAFE-F3_ESTOP        Emergency stop safety relay
=SAFE.GUARD+CP1.SAFE-F3_GUARD        Guard door safety relay
=CTRL+CP1.DOOR.OP-SS_MODE            Mode selector switch
=CTRL+CP1.DOOR.OP-SB_RESET           Fault reset push button
=CTRL+CP1.DOOR.OP-HL_POWER          Power on indicator
=CTRL+CP1.DOOR.OP-HL_RUN            Machine running indicator
=CTRL+CP1.DOOR.OP-HL_FAULT          Fault indicator
=SAFE.ESTOP+CP1.DOOR.OP-SB_ESTOP    Emergency stop push button (door mounted)
```

---

## Motor Control Panels (standalone)

> Single motor, DOL, star-delta, or reversing — standalone enclosure

### Location Designations
```
+MCP_M01                  Motor control panel for motor M01
+MCP_M01.POWER            Power section
+MCP_M01.CTRL             Control section
+MCP_M01.TERM             Terminal section

+MCP_P01                  Motor control panel for pump P01
+MCP_P01.POWER            Power section
+MCP_P01.CTRL             Control section
```

### Full Tag Examples — Standalone Motor Control Panel
```
=PWR+MCP_M01.POWER-QF1              Incomer MCCB
=SAFE+MCP_M01.POWER-F1              Motor protection relay (overload + phase)
=MOTOR.DOL+MCP_M01.POWER-KM1        Main contactor
=CTRL+MCP_M01.CTRL-K_AUX1           Auxiliary relay
=CTRL+MCP_M01.CTRL-SS_LOCAL         Local/remote selector
=CTRL+MCP_M01.CTRL-SB_START         Start button
=CTRL+MCP_M01.CTRL-SB_STOP          Stop button
=CTRL+MCP_M01.CTRL-HL_RUN           Run indicator
=CTRL+MCP_M01.CTRL-HL_TRIP          Trip indicator
=CTRL+MCP_M01.TERM-X1               Terminal block (field wiring)
```

---

## Marshalling Cabinets

> Interface between field cables and control/instrument panels. Used heavily in process, oil & gas, and power projects.

### Function Designations
```
=MARSH         Marshalling function
=MARSH.DI      Digital input marshalling
=MARSH.DO      Digital output marshalling
=MARSH.AI      Analog input marshalling
=MARSH.AO      Analog output marshalling
=MARSH.SAFE    Safety I/O marshalling
=MARSH.COMM    Communications marshalling
```

### Location Designations
```
+MARSH_CAB1               Marshalling cabinet 1
+MARSH_CAB1.DI_RACK       Digital input terminal rack section
+MARSH_CAB1.DO_RACK       Digital output terminal rack section
+MARSH_CAB1.AI_RACK       Analog input terminal rack section
+MARSH_CAB1.AO_RACK       Analog output terminal rack section
+MARSH_CAB1.SAFE_RACK     Safety I/O terminal rack
+MARSH_CAB1.BARRIER_RACK  Zener barrier / isolator rack (hazardous area)
+MARSH_CAB1.POWER         24VDC power supply section
+MARSH_CAB1.TERM_FIELD    Field cable terminations (left side)
+MARSH_CAB1.TERM_CTRL     Control cable terminations (right side, to PLC)

+MARSH_CAB2               Marshalling cabinet 2
+MARSH_CAB3               Marshalling cabinet 3 (safety)
```

### Full Tag Examples — Marshalling Cabinet
```
=PWR.24V+MARSH_CAB1.POWER-PS1            24VDC power supply
=PWR.24V+MARSH_CAB1.POWER-QF1            24VDC MCB
=MARSH.DI+MARSH_CAB1.DI_RACK-X_DI01      DI terminal block row 01
=MARSH.DI+MARSH_CAB1.DI_RACK-X_DI02      DI terminal block row 02
=MARSH.DO+MARSH_CAB1.DO_RACK-X_DO01      DO terminal block row 01
=MARSH.AI+MARSH_CAB1.AI_RACK-X_AI01      AI terminal block row 01 (4-20mA)
=MARSH.AI+MARSH_CAB1.BARRIER_RACK-Z1     Zener barrier / isolator channel 1
=MARSH.AO+MARSH_CAB1.AO_RACK-X_AO01     AO terminal block row 01
=MARSH.SAFE+MARSH_CAB3.SAFE_RACK-X_S01  Safety terminal block row 01
```

---

## Instrumentation Cabinets

> For temperature, pressure, flow, and level instruments wiring termination

### Location Designations
```
+INST_CAB1                Instrumentation cabinet 1
+INST_CAB1.POWER          Power supply section
+INST_CAB1.LOOP_POWER     Loop power section (24VDC loops)
+INST_CAB1.TEMP           Temperature instrument terminals
+INST_CAB1.PRESS          Pressure instrument terminals
+INST_CAB1.FLOW           Flow instrument terminals
+INST_CAB1.LEVEL          Level instrument terminals
+INST_CAB1.ANAL           Analyser interface section
+INST_CAB1.BARRIER        Zener barrier / isolator section
+INST_CAB1.MTR            Instrument air / utilities interface
```

---

## Protection & Metering Panels

> Common in substations and large switchgear applications

### Function Designations
```
=PROT          Protection function
=PROT.OC       Overcurrent protection
=PROT.EF       Earth fault protection
=PROT.DIFF     Differential protection
=PROT.DIST     Distance protection
=PROT.BUSBAR   Busbar protection
=PROT.REF      Restricted earth fault
=METER         Metering function
=METER.ENERGY  Energy metering
=METER.PQ      Power quality metering
=SCADA         SCADA / RTU function
=DC            DC auxiliary supply function
```

### Location Designations
```
+PROT_PNL1                Protection and metering panel 1
+PROT_PNL1.INC_A          Incomer A protection section
+PROT_PNL1.INC_B          Incomer B protection section
+PROT_PNL1.TX1_PROT       Transformer 1 protection section
+PROT_PNL1.TX2_PROT       Transformer 2 protection section
+PROT_PNL1.FDR_PROT       Feeder protection section
+PROT_PNL1.BUSBAR         Busbar protection section
+PROT_PNL1.METER          Metering section
+PROT_PNL1.SCADA          SCADA / RTU section
+PROT_PNL1.DC_DIST        DC auxiliary distribution section
+PROT_PNL1.TERM           Terminal section
+PROT_PNL1.COMM           Communications section (IEC 61850 / GOOSE)
```

### Full Tag Examples — Protection Panel
```
=PROT.OC+PROT_PNL1.INC_A-F_OC_A       Overcurrent relay incomer A (e.g. SEL-751, REF615)
=PROT.EF+PROT_PNL1.INC_A-F_EF_A       Earth fault relay incomer A
=PROT.DIFF+PROT_PNL1.TX1_PROT-F_DIFF  Differential relay transformer 1 (e.g. REF630)
=PROT.REF+PROT_PNL1.TX1_PROT-F_REF    Restricted earth fault relay
=PROT.BUSBAR+PROT_PNL1.BUSBAR-F_BB    Busbar protection relay (e.g. REB670)
=METER.ENERGY+PROT_PNL1.METER-KWH1    Fiscal energy meter
=METER.PQ+PROT_PNL1.METER-PQ1         Power quality analyser
=SCADA+PROT_PNL1.SCADA-RTU1           RTU / IED gateway
=SCADA+PROT_PNL1.SCADA-IED1           Protection IED (IEC 61850)
=DC+PROT_PNL1.DC_DIST-QF_DC1          DC MCB distribution
=DC+PROT_PNL1.DC_DIST-QF_DC2          DC MCB protection
=COMM+PROT_PNL1.COMM-SW_FIBER         Managed fibre switch (IEC 61850 GOOSE)
```

---

## Battery & DC Panels

> For substation DC systems (110V DC / 48V DC / 24V DC)
> Standards: IEC 60896, IEC 62485

### Function Designations
```
=BATT          Battery bank function
=DC.CHRG       Battery charger function
=DC.DIST       DC distribution function
=DC.INC        DC incomer function
=DC.FDR        DC feeder function
```

### Location Designations
```
+BATT_RM                  Battery room (top level)
+BATT_RM.BATT_BANK1       Battery bank 1 (string of cells)
+BATT_RM.BATT_BANK2       Battery bank 2
+CHRG_CAB1                Battery charger cabinet 1
+CHRG_CAB1.CHRG_A         Charger A (main)
+CHRG_CAB1.CHRG_B         Charger B (standby)
+CHRG_CAB1.CTRL           Charger control section
+DC_DB1                   DC distribution board 1 (110V DC)
+DC_DB1.INC               DC incomer section
+DC_DB1.FDR               DC feeder section
+DC_DB1.FDR.PROT          Protection relay feeders
+DC_DB1.FDR.CTRL          Control relay feeders
+DC_DB1.FDR.SCADA         SCADA / RTU feeders
+DC_DB1.FDR.ALARM         Alarm / indication feeders
+DC_DB1.FDR.MOTOR         Motor trip coil feeders
+DC_DB1.DIODE             Diode coupling (parallel chargers)
+DC_DB2                   DC distribution board 2
```

### Full Tag Examples — Battery & DC
```
=BATT+BATT_RM.BATT_BANK1-FU_BATT1     Battery bank fuse / disconnect
=DC.CHRG+CHRG_CAB1.CHRG_A-CHRG_A      Charger A unit
=DC.CHRG+CHRG_CAB1.CHRG_B-CHRG_B      Charger B unit
=DC.INC+DC_DB1.INC-QF_DC_INC          DC incomer fuse / MCB
=DC.FDR+DC_DB1.FDR.PROT-QF_P1         Protection relay DC feeder 1
=DC.FDR+DC_DB1.FDR.PROT-QF_P2         Protection relay DC feeder 2
=DC.FDR+DC_DB1.FDR.CTRL-QF_C1         Control relay DC feeder 1
=DC.FDR+DC_DB1.FDR.MOTOR-QF_M1        Trip coil DC feeder motor 1
=CTRL+CHRG_CAB1.CTRL-HL_CHRG_A        Charger A on indicator
=CTRL+CHRG_CAB1.CTRL-HL_FAULT_A       Charger A fault indicator
```

---

## Emergency & Essential Boards

### Location Designations
```
+EMDB                     Emergency distribution board
+EMDB.INC_NORM            Normal supply incomer
+EMDB.INC_GEN             Generator supply incomer
+EMDB.ATS                 ATS section
+EMDB.BUS                 Essential busbar
+EMDB.FDR_1               Essential feeder 1 (fire alarm)
+EMDB.FDR_2               Essential feeder 2 (emergency lighting)
+EMDB.FDR_3               Essential feeder 3 (security)
+EMDB.FDR_4               Essential feeder 4 (comms / IT)
+EMDB.FDR_5               Essential feeder 5 (life safety)
+EMDB.UPS_FDR             UPS-backed critical feeder

+ESDB                     Essential services distribution board
+ESDB.INC                 Incomer (from EMDB or generator)
+ESDB.FDR_1               Essential services feeder 1
+ESDB.FDR_2               Essential services feeder 2
```

---

## Junction Boxes & Field Enclosures

> The "location" for field-mounted devices with no dedicated panel

### Location Designations
```
+JB1                      Junction box 1
+JB2                      Junction box 2
+JB_M01                   Junction box at motor M01
+JB_P01                   Junction box at pump P01
+JB_AREA_A                Junction box in area A
+JB_AREA_B                Junction box in area B
+JB_VALVE1                Junction box at valve station 1
+JB_ROOF                  Junction box on roof
+JB_FIELD_N               Junction box on north field area
+EX_JB1                   Explosion-proof junction box 1 (Ex zone)
+EX_JB2                   Explosion-proof junction box 2
+LS_BOX1                  Local isolator / switch box 1
+LS_BOX_M01               Local isolator box at motor M01
+FIELD                    General field (no enclosure)
+FIELD.AREA_A             Field area A
+FIELD.AREA_B             Field area B
```

### Full Tag Examples — Junction Box
```
=INST+JB_P01-X1           Terminal strip for pump P01 instruments
=CTRL+JB_P01-X2           Terminal strip for pump P01 control signals
=PWR+JB_P01-QS1           Local isolator for pump P01
=SAFE.ESTOP+JB_P01-SB_E   Local e-stop at pump P01
=CTRL+JB_P01-HL_RUN       Run indication lamp at pump P01
=INST+EX_JB1-X1           Terminals in Ex JB 1 (intrinsically safe)
=INST+EX_JB1-Z1           Zener barrier in Ex JB 1
```

---

## Busbar Chambers & Interconnections

### Location Designations
```
+BUSDUCT1                 Main busbar chamber / duct 1
+BUSDUCT1.FEED            Feed end (transformer LV terminals)
+BUSDUCT1.RUN             Busbar run section
+BUSDUCT1.MSB_END         MSB end connection

+INTER_CAB1               Interconnection / cable spreading chamber 1
+INTER_CAB1.MV_TERM       MV cable termination section
+INTER_CAB1.LV_TERM       LV cable termination section

+CABLE_VAULT1             Underground cable vault 1
+CABLE_VAULT1.JOINTS      Cable joints section
+CABLE_VAULT1.TERM        Cable terminations
```

---

## Operator Stations & HMI Panels

### Location Designations
```
+OP1                      Operator station 1
+OP1.HMI                  HMI touchscreen section
+OP1.CTRL                 Control buttons / lamps section
+OP1.ESTOP                Emergency stop section
+OP1.KEY_SW               Key switch section

+OP2                      Operator station 2
+OP_REMOTE1               Remote operator station 1

+DESK1                    Operator desk / console 1
+DESK1.MONITOR            Monitor section
+DESK1.KEYBOARD           Keyboard / peripherals
+DESK1.PC                 PC / workstation
+DESK1.KVM                KVM switch

+PENDANT1                 Operator pendant 1
+PENDANT1.CTRL            Pendant control buttons
+PENDANT1.ESTOP           Pendant emergency stop
```

---

## Complete Single-Line Examples

### Example 1 — Industrial Site: Utility to Motor
```
Grid supply
    ↓
+RMU1 (=MV.RING)  →  Ring main unit
    ↓ TX feeder
+TX1 (=TX)        →  11kV/415V transformer
    ↓ Busduct
+BTS1 (=PWR.BTS)  →  Busbar trunking to MSB
    ↓
+MSB1 (=PWR)      →  Main LV switchboard (ACB incomer)
    ↓ Feeder
+MCC1 (=MOTOR)    →  MCC (for motors up to 200kW)
    ↓ Drawer
+MCC1.M01         →  DOL starter for motor M01
    ↓
Field: +JB_M01    →  Junction box at motor M01
    ↓
Motor M01

Full device tag: =MOTOR.DOL+MCC1.M01-KM1   (main contactor)
```

### Example 2 — Data Centre Power Chain
```
+UTIL (=PWR.INC)       →  Utility incoming (2 feeds)
    ↓
+MSB1.INC_A (=PWR)     →  MSB incomer A (utility A)
+MSB1.INC_B (=PWR)     →  MSB incomer B (utility B or generator)
+MSB1.TIE (=PWR.TIE)   →  Bus tie
    ↓
+ATS1 (=PWR.ATS)       →  Automatic transfer switch (for generator)
    ↓
+UPS1 (=PWR.UPS)       →  UPS system (double conversion)
    ↓
+UPS1.DIST_BOARD       →  UPS output distribution
    ↓ feeders
+PDU_A1 (=PWR)         →  Power distribution unit A (critical load)
+PDU_B1 (=PWR)         →  Power distribution unit B (redundant)
```

### Example 3 — Substation: Grid to LV Bus
```
+MV_SW1.INC_1 (=MV.INC)    →  11kV incomer VCB
    ↓ busbar
+MV_SW1.BUS_SEC (=MV.TIE)  →  Bus section VCB
    ↓
+MV_SW1.TX_FDR1 (=MV.TX)   →  11kV transformer feeder VCB
    ↓
+TX1 (=TX)                 →  11kV/415V transformer (1600kVA)
    ↓
+MSB1.INC_A (=PWR.INC)     →  LV MSB ACB incomer
    ↓
+MSB1.FDR_1 (=PWR.FDR)     →  Feeder to MCC
+MSB1.FDR_2 (=PWR.FDR)     →  Feeder to DB1
+MSB1.FDR_3 (=PWR.FDR)     →  Feeder to PFC1
+MSB1.UPS_FDR (=PWR.UPS)   →  Feeder to UPS
    ↓
+PFC1 (=PWR.PFC)           →  Power factor correction bank
```

---

## IEC Standards Quick Reference

| Equipment | Relevant IEC Standard |
|-----------|----------------------|
| MV Switchgear (metal-enclosed) | IEC 62271-200 |
| MV Circuit Breakers | IEC 62271-100 |
| MV Load Break Switches | IEC 62271-103 |
| LV Switchgear & Controlgear Assemblies | IEC 61439-1 (general), IEC 61439-2 (power) |
| LV Consumer / Distribution boards | IEC 61439-3 |
| Motor Control Assemblies | IEC 61439-4 (also IEC 60947-4 for starters) |
| LV Circuit Breakers | IEC 60947-2 |
| Contactors | IEC 60947-4-1 |
| Soft Starters | IEC 60947-4-2 |
| VFDs | IEC 61800-2, IEC 61800-3 |
| Ring Main Units | IEC 62271-200, IEC 62271-105 |
| Transformers (oil) | IEC 60076 |
| Transformers (dry type) | IEC 60076-11 |
| Busbar Trunking | IEC 61439-6 |
| UPS Systems | IEC 62040-1, IEC 62040-3 |
| ATS / Transfer Switches | IEC 60947-6-1 |
| Capacitor Banks / PFC | IEC 60831, IEC 61921 |
| Battery Systems (VRLA) | IEC 60896-21/22 |
| Battery Chargers | IEC 62485-3 |
| Protection Relays | IEC 60255 series |
| Energy Meters | IEC 62053 series |
| Power Analysers | IEC 61000-4-30 |

---

## Common Mistakes for Panel Builders

| ❌ Wrong | ✅ Correct | Reason |
|----------|------------|--------|
| `=PANEL_A` | `+PANEL_A` | The panel is a location, not a function |
| `+MOTOR_1` | `+MCC1.M01` or `+JB_M01` | Motor is a device/field point, not a panel location |
| `+Q1` or `+KM1` | `+MCC1.M01-KM1` | Component is a device `-`, not a location `+` |
| Naming all sections `+SEC` | `+SEC_1`, `+SEC_2`, `+SEC_3` | Non-unique section names break report grouping |
| Leaving `+` blank on all pages | Use `+PANEL_NAME` at minimum | Blank location = useless terminal and cable reports |
| `+MCC 1` (with space) | `+MCC1` | Spaces break EPLAN structure identifiers |
| One location for entire project: `+SITE` | Break into panel-level locations | Too broad — all reports merge into one group |
| `+MCC1.DRAWER_FOR_MOTOR_1` | `+MCC1.M01` | Too long — truncated in reports and tables |
| Mixing `=` and `+` purpose | Function stays in `=`, physical location in `+` | Crossing them over destroys report filtering |
| Different engineers using `+CP`, `+CP1`, `+CTRL_PNL` for same panel | Standardise at project setup | Inconsistency means reports split the same panel |

---

## Expert Tips for Panel Builders

### 1. Set your location structure in the project settings first
> Before drawing page 1, define all `+` locations in *Project data → Structure identifiers*. This prevents inconsistent names and typos spreading through hundreds of pages.

### 2. One `+` per physical enclosure — always
> Every panel, cabinet, junction box, and operator station gets its own unique `+` location. This is what makes terminal diagrams, cable schedules, and BOMs filter correctly.

### 3. Use section-level `+` for large panels (MCC, MSB)
> `+MCC1.M01` for each motor drawer means your terminal diagram for drawer M01 prints cleanly, separately from M02. Without section-level `+`, all MCC terminals print as one massive list.

### 4. `+FIELD` is not just a placeholder — use it actively
> All instruments, sensors, solenoids, and actuators without their own enclosure should use `+FIELD` or `+JB_NEAREST`. This keeps your connection list and cable schedule complete.

### 5. Name drawers and compartments after the load, not the position
> `+MCC1.M01` (motor M01 feeder) is better than `+MCC1.SEC2.C04` (section 2, compartment 4). Load-named locations survive design changes when drawers are moved.

### 6. Keep `+` names consistent with the panel schedule and SLD
> If your single-line diagram calls a panel `MCC-1A`, your EPLAN location should be `+MCC_1A`. Never let EPLAN names and drawing names diverge.

### 7. Use `+PANEL.DOOR` for door-mounted devices
> Separating door devices (`+CP1.DOOR`) from internal devices (`+CP1.RELAY`) keeps your panel layout and door drilling drawings clean and auto-separable.

### 8. For multi-section MCCs, decide early: section-based or load-based naming
> Section-based (`+MCC1.SEC_1.C01`) suits shop drawings. Load-based (`+MCC1.M01`) suits field commissioning and maintenance. Load-based is usually preferred for complex projects.

### 9. DC and AC auxiliary supplies need their own `+` sub-location
> `+MSB1.CTRL` or `+MCC1.CTRL_SEC` keeps your 24VDC and 230VAC auxiliary wiring separated from the main power circuits in every report.

### 10. Validate with reports before issuing for manufacture
> Run a terminal diagram, cable list, and parts list before releasing drawings. If the report grouping looks wrong — too many or too few groups — your `+` structure is the first place to check.

---

*Based on IEC 61439 | IEC 62271 | IEC 60947 | IEC 61800 | IEC 62040 | IEC 60076 | IEC 60831 | IEC 60255 | IEC 62053*
*Expert conventions for panel builders, system integrators, switchgear manufacturers, and electrical engineering firms*
