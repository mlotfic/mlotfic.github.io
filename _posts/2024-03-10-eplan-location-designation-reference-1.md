---

title: "EPLAN Location Designation (`+`) Reference Guide"

description: >-
  A comprehensive reference guide to the location designation (`+`) scheme in EPLAN Electric P8, including its definition, characteristics, examples, hierarchical structure, practical use cases, and expert tips for effective implementation in electrical project documentation.
date: 2024-03-10 10:00:00 +0800
author: Mahmoud Lotfi
file_name: 2024-03-10-eplan-location-designation-reference-1.md
categories: [EPLAN, Location Designation, Reference]
tags: [Eplan, location designation, reference]
pin: False
math: true
mermaid: true
comments: true
toc: true
render_with_liquid: false

image:
  path: /assets/img/posts/eplan.jpg
  alt: EPLAN Location Designation Explained
  lqip: data:image/webp;base64,UklGRjoAAABXRUJQVlA4IC4AAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
---

# EPLAN P8 — Location Designation (`+`) Reference Guide
> Based on IEC 81346 | Expert conventions from machine building, process, energy, and infrastructure industries

---

## Table of Contents
1. [Fundamentals](#fundamentals)
2. [IEC 81346 Location Hierarchy Principles](#iec-81346-location-hierarchy-principles)
3. [Machine Building](#machine-building)
4. [Panel Building & OEM](#panel-building--oem)
5. [Process & Chemical Industry](#process--chemical-industry)
6. [Oil & Gas](#oil--gas)
7. [Water & Wastewater Treatment](#water--wastewater-treatment)
8. [Power Distribution & Energy](#power-distribution--energy)
9. [Building Automation (BAS/BMS)](#building-automation-basbms)
10. [Automotive Manufacturing](#automotive-manufacturing)
11. [Food & Beverage](#food--beverage)
12. [Pharmaceutical & Cleanroom](#pharmaceutical--cleanroom)
13. [Renewable Energy — Solar PV](#renewable-energy--solar-pv)
14. [Renewable Energy — Wind](#renewable-energy--wind)
15. [Marine & Shipbuilding](#marine--shipbuilding)
16. [Rail & Transportation](#rail--transportation)
17. [Data Centre & IT Infrastructure](#data-centre--it-infrastructure)
18. [Mining & Heavy Industry](#mining--heavy-industry)
19. [HVAC Systems](#hvac-systems)
20. [Safety & SIL Systems](#safety--sil-systems)
21. [Full Structure Examples](#full-structure-examples)
22. [Location vs Function — Side by Side](#location-vs-function--side-by-side)
23. [Common Mistakes](#common-mistakes)
24. [Expert Tips](#expert-tips)

---

## Fundamentals

### The Three Pillars of EPLAN Referencing (IEC 81346)
```
=   Function designation     → WHAT it does
+   Location designation     → WHERE it is
-   Device designation       → WHAT it is (component tag)
```

### What Location Designation Represents
Location designation describes the **physical place** where a component, panel, or cable is installed. It answers the question:
> *"If I walked into the facility, where would I physically find this item?"*

### Location Hierarchy — Three Typical Levels
```
+SITE                        Level 1 — Site / facility
+SITE.BUILDING               Level 2 — Building / structure
+SITE.BUILDING.ROOM          Level 3 — Room / area
+SITE.BUILDING.ROOM.PANEL    Level 4 — Panel / enclosure (common deepest level)
```

### Full Tag Syntax
```
=FUNCTION+LOCATION-DEVICE

Examples:
=CTRL+SITE1.BLDG_A.CR1.PLC_CAB-CPU01     PLC CPU in cabinet, control room, building A, site 1
=PWR+PLANT.MCC_ROOM.MCC1-Q3              Contactor in MCC1, MCC room, plant
=SAFE+MACHINE.CP1-F3_SAFE                Safety relay in control panel CP1 on machine
```

### Separator Rules
```
.   Sub-level separator        +SITE.BUILDING.ROOM
-   Device tag follows         +PANEL1-K1
```

---

## IEC 81346 Location Hierarchy Principles

IEC 81346 does not prescribe fixed letter codes for location the same way it does for function classes. Instead it defines a **structural hierarchy** — engineers apply their own naming within that hierarchy. Common expert interpretations:

### Geographic / Spatial Levels
| Level | Typical Scope | Example |
|-------|--------------|---------|
| 1 | Site / campus / facility | `+SITE_A`, `+PLANT1`, `+OFFSHORE_A` |
| 2 | Building / structure / area | `+BLDG_1`, `+PROCESS_AREA`, `+PLATFORM` |
| 3 | Room / zone / floor | `+MCC_ROOM`, `+CTRL_ROOM`, `+L01` |
| 4 | Panel / enclosure / cabinet | `+MCC1`, `+PLC_CAB`, `+JB1` |
| 5 | Device mounting location | Typically becomes the `-` device tag |

### Naming Styles Used by Experts
```
Descriptive:    +CONTROL_ROOM.PLC_CABINET
Alphanumeric:   +CR1.CAB01
Code-based:     +CR.C01
Short:          +CR.PLC1
```

---

## Machine Building

> Convention: Machine sections and control panels. Simple — usually 1 to 2 levels. Common in European and Australian machine builders.

### Single Machine
```
+MACHINE           The machine itself (top level)
+MACHINE.CP1       Control panel 1 (main electrical enclosure)
+MACHINE.CP2       Control panel 2 (secondary or remote panel)
+MACHINE.OP1       Operator station 1
+MACHINE.OP2       Operator station 2
+MACHINE.JB1       Junction box 1
+MACHINE.JB2       Junction box 2
+MACHINE.FIELD     Field-mounted devices (sensors, actuators)
+MACHINE.BED       Machine bed / base
+MACHINE.HEAD      Machine head / upper section
+MACHINE.DOOR      Machine guarding / door area
```

### Multi-Section Machine (e.g. transfer line)
```
+LINE              Production line (top level)
+LINE.SEC_A        Section A
+LINE.SEC_B        Section B
+LINE.SEC_C        Section C
+LINE.SEC_A.CP1    Control panel in section A
+LINE.SEC_B.CP1    Control panel in section B
+LINE.SEC_C.CP1    Control panel in section C
+LINE.SEC_A.OP1    Operator station in section A
+LINE.CONV         Conveyor area
+LINE.LOAD         Loading station
+LINE.UNLOAD       Unloading station
+LINE.INFEED       Infeed conveyor area
+LINE.OUTFEED      Outfeed conveyor area
```

### CNC Machine
```
+CNC               CNC machine
+CNC.ELEC_CAB      Electrical cabinet (rear of machine)
+CNC.CTRL_CAB      CNC controller cabinet
+CNC.OP_PANEL      Operator panel (front)
+CNC.JB1           Junction box 1
+CNC.SPINDLE       Spindle area
+CNC.TABLE         Machine table area
+CNC.COOLANT       Coolant system area
+CNC.CHIP          Chip conveyor area
+CNC.TOOL_CHGR     Tool changer area
```

### Robotic Cell
```
+CELL              Robot cell (top level)
+CELL.CP1          Main control panel
+CELL.CP_R1        Robot 1 controller cabinet
+CELL.CP_R2        Robot 2 controller cabinet
+CELL.OP1          Operator station
+CELL.SAFETY_POST  Safety monitoring post
+CELL.FENCE        Perimeter fence area
+CELL.INFEED       Infeed station
+CELL.OUTFEED      Outfeed station
+CELL.JB1          Junction box 1
+CELL.JB2          Junction box 2
+CELL.WELD_AREA    Welding area
+CELL.FIXTURE      Fixture / tooling area
```

---

## Panel Building & OEM

> Convention: Panel or enclosure as the primary location. Often the only level used. Suitable for standalone panel projects.

### Single Panel Project
```
+PANEL             Panel (if only one)
+MCC               Motor control centre
+DB                Distribution board
+CP                Control panel
+JB                Junction box
+OP                Operator panel / station
```

### Multi-Panel Project
```
+MCC1              MCC 1
+MCC2              MCC 2
+MCC3              MCC 3
+PLC_CAB           PLC cabinet
+DB1               Distribution board 1
+DB2               Distribution board 2
+DB3               Distribution board 3
+EDB               Essential distribution board
+JB1               Junction box 1
+JB2               Junction box 2
+JB3               Junction box 3
+OP1               Operator station 1
+OP2               Operator station 2
+FIELD             Field devices (no enclosure)
```

### MCC Internal Sections
```
+MCC1              MCC 1 (top level)
+MCC1.INC          Incoming section
+MCC1.BUS          Busbar section
+MCC1.SEC_A        Section A — motor feeders
+MCC1.SEC_B        Section B — VFD feeders
+MCC1.SOFT         Softstarter section
+MCC1.CTRL         Control section / PLC drawer
+MCC1.METER        Metering section
```

---

## Process & Chemical Industry

> Convention: Plant → area → room → panel. Mirrors the plant layout and P&ID area breakdown.

### Plant Hierarchy
```
+PLANT             Entire plant site
+PLANT.AREA_10     Process area 10 (raw material intake)
+PLANT.AREA_20     Process area 20 (pre-treatment)
+PLANT.AREA_30     Process area 30 (reaction)
+PLANT.AREA_40     Process area 40 (separation)
+PLANT.AREA_50     Process area 50 (purification)
+PLANT.AREA_60     Process area 60 (product storage)
+PLANT.UTIL        Utilities area
+PLANT.CTRL_ROOM   Central control room
+PLANT.SUBST       Electrical substation
+PLANT.WORKSHOP    Maintenance workshop
```

### Within a Process Area
```
+PLANT.AREA_30                  Reaction area (top level)
+PLANT.AREA_30.MCC1             MCC for area 30
+PLANT.AREA_30.PLC_CAB          PLC cabinet for area 30
+PLANT.AREA_30.JB_R01           Junction box at reactor R01
+PLANT.AREA_30.JB_R02           Junction box at reactor R02
+PLANT.AREA_30.OP1              Local operator station
+PLANT.AREA_30.FIELD            Field instruments and devices
```

### Control Room
```
+CTRL_ROOM                      Central control room
+CTRL_ROOM.DCS_CAB1             DCS cabinet 1
+CTRL_ROOM.DCS_CAB2             DCS cabinet 2
+CTRL_ROOM.HIST_CAB             Historian server cabinet
+CTRL_ROOM.UPS_CAB              UPS cabinet
+CTRL_ROOM.PATCH                Patch panel / comms cabinet
+CTRL_ROOM.DESK1                Operator workstation 1
+CTRL_ROOM.DESK2                Operator workstation 2
+CTRL_ROOM.ENG_DESK             Engineering workstation
```

### Utilities Area
```
+UTIL                           Utilities area
+UTIL.COMPRESS_RM               Compressor room
+UTIL.BOILER_RM                 Boiler room
+UTIL.COOL_TOWER                Cooling tower area
+UTIL.WATER_TREAT               Water treatment area
+UTIL.SUBST                     Electrical substation
+UTIL.GEN_RM                    Generator room
+UTIL.BATT_RM                   Battery room
```

---

## Oil & Gas

> Convention: Platform / facility → module → area → panel. Follows ISO 10628 and discipline-specific layouts.

### Offshore Platform / FPSO
```
+PLATFORM          Offshore platform / FPSO (top level)
+PLATFORM.CELLAR   Cellar deck
+PLATFORM.MAIN     Main deck
+PLATFORM.UPPER    Upper deck
+PLATFORM.MEZZANINE Mezzanine deck
+PLATFORM.CCR      Central control room
+PLATFORM.LER      Local equipment room (per area)
+PLATFORM.LER_A    LER area A
+PLATFORM.LER_B    LER area B
+PLATFORM.LER_C    LER area C
+PLATFORM.ER       Main electrical room
+PLATFORM.BATT_RM  Battery room
+PLATFORM.WELLBAY  Wellbay area
+PLATFORM.PROC_A   Process module A
+PLATFORM.PROC_B   Process module B
+PLATFORM.COMP     Compression module
+PLATFORM.UTIL     Utilities module
+PLATFORM.ACCOM    Accommodation block
+PLATFORM.LIFEBOAT Lifeboat station
+PLATFORM.HELIDECK Helideck
```

### Onshore Gas Plant / Refinery
```
+FACILITY          Plant facility (top level)
+FACILITY.PROCESS  Process area
+FACILITY.COMPRESS Compression area
+FACILITY.STORAGE  Storage area
+FACILITY.LOADING  Truck / rail loading area
+FACILITY.FLARE    Flare area
+FACILITY.SUBST    Main substation
+FACILITY.CTRL_BLDG Control building
+FACILITY.CTRL_BLDG.CCR    Central control room
+FACILITY.CTRL_BLDG.ENG    Engineering room
+FACILITY.CTRL_BLDG.UPS    UPS room
+FACILITY.CTRL_BLDG.COMMS  Communications room
+FACILITY.MAINT_BLDG       Maintenance building
+FACILITY.FIRE_STN         Fire station
+FACILITY.WAREHSE          Warehouse
```

### Local Equipment Rooms (LER)
```
+LER_A             Local equipment room A
+LER_A.MCC1        MCC 1
+LER_A.PLC_CAB     PLC / ESD cabinet
+LER_A.JB1         Junction box 1
+LER_A.SAFE_CAB    Safety system cabinet
+LER_A.COMM_CAB    Communications cabinet
+LER_A.UPS_CAB     UPS cabinet
```

---

## Water & Wastewater Treatment

> Convention: Site → structure / building → room → panel. Follows asset register and site layout.

### Water Treatment Plant
```
+SITE              Treatment plant site
+SITE.INTAKE       Intake structure
+SITE.INTAKE.CP1   Control panel at intake
+SITE.INTAKE.JB1   Junction box at intake
+SITE.FLOC         Flocculation building
+SITE.FLOC.CP1     Control panel in floc building
+SITE.FILT         Filter building
+SITE.FILT.CP1     Control panel in filter building
+SITE.FILT.JB1     Junction box at filter 1
+SITE.FILT.JB2     Junction box at filter 2
+SITE.DOSE         Dosing building
+SITE.DOSE.CP1     Chemical dosing panel
+SITE.PUMP_STN     Pump station
+SITE.PUMP_STN.MCC1 MCC at pump station
+SITE.CTRL_BLDG    Central control building
+SITE.CTRL_BLDG.CR Control room
+SITE.CTRL_BLDG.CR.SCADA_CAB  SCADA cabinet
+SITE.CTRL_BLDG.CR.UPS_CAB    UPS cabinet
+SITE.CTRL_BLDG.SUBST Switchroom / substation
+SITE.SLUDGE       Sludge handling area
+SITE.SLUDGE.CP1   Sludge control panel
+SITE.RESERVOIR    Clear water reservoir
+SITE.RESERVOIR.CP1 Reservoir control panel
```

### Remote Pump Station (Telemetry)
```
+PS_01             Pump station 01
+PS_01.CP1         Main control panel
+PS_01.MCC1        Motor control centre
+PS_01.JB1         Junction box 1
+PS_01.VALVE_PIT   Valve pit
+PS_01.WELL        Wet well
+PS_02             Pump station 02
+PS_02.CP1         Main control panel
```

---

## Power Distribution & Energy

> Convention: Site → substation → room → panel. Used by utilities, EPC, and substation designers. Often follows network naming conventions.

### HV/MV Substation
```
+SUBST             Substation (top level)
+SUBST.YARD        Switchyard (outdoor HV equipment)
+SUBST.YARD.GANTRY HV gantry / structure
+SUBST.CTRL_BLDG   Control building
+SUBST.CTRL_BLDG.RELAY_RM   Relay / protection room
+SUBST.CTRL_BLDG.BATT_RM    Battery room
+SUBST.CTRL_BLDG.HVAC_RM    HVAC plant room
+SUBST.CTRL_BLDG.CABLE_BSMT Cable basement
+SUBST.GIS_BLDG    GIS building (indoor switchgear)
+SUBST.TRANS_YARD  Transformer yard
+SUBST.TRANS_YARD.TX1  Transformer 1 bay
+SUBST.TRANS_YARD.TX2  Transformer 2 bay
+SUBST.CTRL_BLDG.RELAY_RM.PNL_A  Protection panel A
+SUBST.CTRL_BLDG.RELAY_RM.PNL_B  Protection panel B
+SUBST.CTRL_BLDG.RELAY_RM.DC_DB  DC distribution board
+SUBST.CTRL_BLDG.RELAY_RM.SCADA  SCADA/RTU cabinet
+SUBST.CTRL_BLDG.RELAY_RM.COMMS  Communications cabinet
```

### Industrial Power Distribution
```
+SITE              Plant site
+SITE.MAIN_SUBST   Main substation
+SITE.MAIN_SUBST.HV_ROOM   HV switchgear room
+SITE.MAIN_SUBST.MV_ROOM   MV switchgear room
+SITE.MAIN_SUBST.LV_ROOM   LV switchgear room
+SITE.MAIN_SUBST.BATT_RM   Battery room
+AREA_A            Production area A
+AREA_A.SS_A       Area A substation
+AREA_A.SS_A.MCC1  MCC 1
+AREA_A.SS_A.MCC2  MCC 2
+AREA_A.SS_A.DB1   Distribution board 1
+AREA_B            Production area B
+AREA_B.SS_B       Area B substation
+AREA_B.SS_B.MCC3  MCC 3
+UTIL              Utilities area
+UTIL.GEN_RM       Generator room
+UTIL.GEN_RM.GEN1  Generator 1 enclosure
+UTIL.GEN_RM.GEN2  Generator 2 enclosure
+UTIL.UPS_RM       UPS room
+UTIL.UPS_RM.UPS1  UPS 1 cabinet
+UTIL.UPS_RM.DIST  UPS distribution board
```

---

## Building Automation (BAS/BMS)

> Convention: Building → floor / zone → room → panel. Mirrors building layout and services zones.

```
+BLDG              Building (top level)
+BLDG.B1           Basement level 1
+BLDG.GF           Ground floor
+BLDG.L1           Level 1
+BLDG.L2           Level 2
+BLDG.L3           Level 3
+BLDG.ROOF         Roof level
+BLDG.PLANT_RM     Main plant room (typically basement or roof)
+BLDG.PLANT_RM.AHU_1   AHU 1 location
+BLDG.PLANT_RM.AHU_2   AHU 2 location
+BLDG.PLANT_RM.CHILLER  Chiller location
+BLDG.PLANT_RM.BOILER   Boiler location
+BLDG.PLANT_RM.MCC1     MCC 1
+BLDG.PLANT_RM.BMS_CAB  BMS controller cabinet
+BLDG.ELEC_RM      Main electrical room
+BLDG.ELEC_RM.MSB  Main switchboard
+BLDG.ELEC_RM.DB_MAIN  Main DB
+BLDG.ELEC_RM.UPS  UPS
+BLDG.L1.ELEC_RISER  Level 1 electrical riser
+BLDG.L1.ELEC_RISER.DB_L1  Level 1 distribution board
+BLDG.L2.ELEC_RISER.DB_L2  Level 2 distribution board
+BLDG.ROOF.COOL_TOWER   Cooling tower location
+BLDG.CARPARK      Carpark area
+BLDG.CARPARK.DB_CP  Carpark distribution board
+BLDG.LOBBY        Lobby area
+BLDG.LOBBY.OP1    Lobby operator / reception panel
```

### Multi-Building Campus
```
+CAMPUS            Campus (top level)
+CAMPUS.BLDG_A     Building A
+CAMPUS.BLDG_B     Building B
+CAMPUS.BLDG_C     Building C
+CAMPUS.CENTRAL    Central plant building
+CAMPUS.CENTRAL.CHILLER_RM  Chiller room
+CAMPUS.CENTRAL.BOILER_RM   Boiler room
+CAMPUS.CENTRAL.SUBST       Electrical substation
+CAMPUS.BLDG_A.PLANT_RM     Building A plant room
+CAMPUS.BLDG_A.L1           Building A level 1
```

---

## Automotive Manufacturing

> Convention: Plant → shop → line / zone → panel. Follows production layout and area numbering.

```
+PLANT             Manufacturing plant (top level)
+PLANT.BODY        Body shop
+PLANT.BODY.STAMP  Stamping area
+PLANT.BODY.STAMP.CP1   Stamping control panel 1
+PLANT.BODY.WELD   Welding area
+PLANT.BODY.WELD.CP_W1  Welding CP zone 1
+PLANT.BODY.WELD.CP_W2  Welding CP zone 2
+PLANT.BODY.GEO    Geometry station
+PLANT.PAINT       Paint shop
+PLANT.PAINT.PREP  Pre-treatment area
+PLANT.PAINT.ED    ED primer area
+PLANT.PAINT.BASE  Basecoat booth
+PLANT.PAINT.CLEAR Clearcoat booth
+PLANT.PAINT.OVEN  Paint oven area
+PLANT.PAINT.CP1   Paint shop main CP
+PLANT.TRIM        Trim assembly
+PLANT.TRIM.T1     Trim line 1
+PLANT.TRIM.T1.CP1 Trim line 1 CP
+PLANT.TRIM.T2     Trim line 2
+PLANT.CHASSIS     Chassis and drivetrain
+PLANT.FINAL       Final assembly
+PLANT.FINAL.EOL   End of line test area
+PLANT.UTIL        Plant utilities area
+PLANT.UTIL.SUBST  Electrical substation
+PLANT.UTIL.COMPRESS  Compressor room
+PLANT.UTIL.WATER  Water treatment room
+PLANT.CTRL_RM     Central control room
```

---

## Food & Beverage

> Convention: Site → production area → room → panel. Zoning often follows food safety hygiene zones (raw / ready-to-eat separation).

```
+SITE              Production site
+SITE.RAW          Raw material area (low care zone)
+SITE.RAW.RECV     Receiving dock
+SITE.RAW.STORE    Raw material store
+SITE.RAW.CP1      Raw area control panel
+SITE.PROC         Processing area (medium care zone)
+SITE.PROC.PREP    Preparation room
+SITE.PROC.COOK    Cooking area
+SITE.PROC.COOL    Cooling area
+SITE.PROC.CP1     Processing control panel
+SITE.PROC.JB1     Junction box 1
+SITE.PROC.JB2     Junction box 2
+SITE.HIGH_CARE    High care area (ready-to-eat)
+SITE.HIGH_CARE.FILL   Filling room
+SITE.HIGH_CARE.PACK   Packing room
+SITE.HIGH_CARE.CP1    High care control panel
+SITE.PACK         Secondary packaging (low care)
+SITE.PACK.CART    Cartoning area
+SITE.PACK.PALLETISE  Palletising area
+SITE.PACK.CP1     Packing control panel
+SITE.REFRIG       Refrigeration plant room
+SITE.REFRIG.CP1   Refrigeration panel
+SITE.STEAM        Boiler / steam room
+SITE.STEAM.CP1    Steam control panel
+SITE.CIP          CIP room
+SITE.CIP.CP1      CIP control panel
+SITE.SUBST        Electrical substation
+SITE.SUBST.MDB    Main distribution board
+SITE.CTRL_RM      Control room
+SITE.CTRL_RM.SCADA_CAB  SCADA cabinet
```

---

## Pharmaceutical & Cleanroom

> Convention: Building → cleanroom grade zone → room → panel. Strictly follows GMP zoning (Grade A/B/C/D).

```
+BLDG              Manufacturing building
+BLDG.UNCLASS      Unclassified / general area
+BLDG.GRADE_D      Grade D cleanroom corridor
+BLDG.GRADE_C      Grade C cleanroom
+BLDG.GRADE_B      Grade B cleanroom
+BLDG.GRADE_A      Grade A (isolator / RABS)
+BLDG.GRADE_D.WEIGH    Weighing room (Grade D)
+BLDG.GRADE_D.GOWN     Gowning room
+BLDG.GRADE_C.FORM     Formulation suite
+BLDG.GRADE_C.BLEND    Blending room
+BLDG.GRADE_C.GRANUL   Granulation room
+BLDG.GRADE_B.FILL     Filling room
+BLDG.GRADE_B.LYOPHIL  Lyophiliser room
+BLDG.GRADE_A.ISOLATOR Isolator (Grade A microenvironment)
+BLDG.UNCLASS.WFI_RM   WFI plant room
+BLDG.UNCLASS.PW_RM    Purified water plant room
+BLDG.UNCLASS.HVAC_RM  HVAC plant room
+BLDG.UNCLASS.ELEC_RM  Electrical room
+BLDG.UNCLASS.ELEC_RM.MDB   Main distribution board
+BLDG.UNCLASS.ELEC_RM.UPS   UPS cabinet
+BLDG.UNCLASS.CTRL_RM  Control room
+BLDG.UNCLASS.CTRL_RM.DCS_CAB1  DCS cabinet 1
+BLDG.UNCLASS.CTRL_RM.DCS_CAB2  DCS cabinet 2
+BLDG.UNCLASS.CTRL_RM.SAFE_CAB  Safety / ESD cabinet
+BLDG.UNCLASS.CTRL_RM.BMS_CAB   BMS cabinet
+BLDG.FORM.CP1     Formulation local panel
+BLDG.FILL.CP1     Filling local panel
```

---

## Renewable Energy — Solar PV

> Convention: Site → inverter station / block → combiner level → field. Based on electrical single-line topology.

```
+SITE              Solar farm site
+SITE.POC          Point of connection (grid interface)
+SITE.MAIN_SUBST   Main grid-side substation
+SITE.MAIN_SUBST.HV_SW  HV switchgear
+SITE.MAIN_SUBST.TX1    Export transformer 1
+SITE.MAIN_SUBST.TX2    Export transformer 2
+SITE.CTRL_BLDG    Site control building
+SITE.CTRL_BLDG.SCADA_CAB  SCADA / monitoring cabinet
+SITE.CTRL_BLDG.COMM_CAB   Communications cabinet
+SITE.CTRL_BLDG.MET_STN    Meteorological station (if co-located)
+SITE.BESS         Battery energy storage area
+SITE.BESS.BATT_CAB1  Battery cabinet 1
+SITE.BESS.BATT_CAB2  Battery cabinet 2
+SITE.BESS.PCS_CAB    PCS cabinet
+SITE.INV_STN_1    Inverter station 1
+SITE.INV_STN_1.INV1   Inverter 1 enclosure
+SITE.INV_STN_1.INV2   Inverter 2 enclosure
+SITE.INV_STN_1.TX_1   LV/MV step-up transformer
+SITE.INV_STN_2    Inverter station 2
+SITE.INV_STN_2.INV3   Inverter 3 enclosure
+SITE.INV_STN_2.INV4   Inverter 4 enclosure
+SITE.INV_STN_2.TX_2   LV/MV step-up transformer
+SITE.FIELD_A      PV field area A (string arrays)
+SITE.FIELD_A.SCB1 String combiner box 1
+SITE.FIELD_A.SCB2 String combiner box 2
+SITE.FIELD_B      PV field area B
+SITE.FIELD_B.SCB3 String combiner box 3
+SITE.FIELD_B.SCB4 String combiner box 4
+SITE.MET_MAST     Meteorological mast
```

---

## Renewable Energy — Wind

> Convention: Site → turbine (WTG number) → internal turbine area. Site infrastructure separate.

```
+SITE              Wind farm site
+SITE.ONSHORE_SS   Onshore substation
+SITE.ONSHORE_SS.CTRL_BLDG  Control building
+SITE.ONSHORE_SS.YARD       Switchyard
+SITE.OSS          Offshore substation (offshore projects)
+SITE.OSS.HV_RM    HV room
+SITE.OSS.MV_RM    MV room
+SITE.OSS.AUX_RM   Auxiliary room
+SITE.OSS.CTRL_RM  Control room
+WTG_01            Wind turbine 01
+WTG_01.TOWER_BTM  Tower base (bottom)
+WTG_01.TOWER_MID  Tower mid-section
+WTG_01.NACELLE    Nacelle
+WTG_01.NACELLE.CONV_CAB  Converter cabinet
+WTG_01.NACELLE.CTRL_CAB  Control cabinet
+WTG_01.NACELLE.TRANS     Nacelle transformer
+WTG_01.HUB        Hub
+WTG_01.TOWER_BTM.MV_SW   MV switchgear at base
+WTG_02            Wind turbine 02
+WTG_02.TOWER_BTM  Tower base
+WTG_02.NACELLE    Nacelle
+WTG_02.HUB        Hub
+ARRAY             Array cable route (shared)
+ARRAY.JB1         Offshore junction box 1
+ARRAY.JB2         Offshore junction box 2
+METMAST           Meteorological mast
```

---

## Marine & Shipbuilding

> Convention: Vessel → deck → compartment / space. Follows ship block and compartment numbering. Common in naval architecture documentation.

```
+VESSEL            The vessel (top level)
+VESSEL.KEEL       Keel / bilge
+VESSEL.D1         Deck 1 (lowest)
+VESSEL.D2         Deck 2
+VESSEL.D3         Deck 3
+VESSEL.D4         Deck 4 (main deck)
+VESSEL.D5         Deck 5 (upper)
+VESSEL.BRIDGE     Bridge deck
+VESSEL.D1.ER      Engine room (typically lower decks)
+VESSEL.D1.ER.MAIN_SW   Main switchboard
+VESSEL.D1.ER.EMERG_SW  Emergency switchboard
+VESSEL.D1.ER.CTRL_PANEL Engine room control panel
+VESSEL.D1.ER.BATT_RM   Battery room
+VESSEL.D1.CARGO   Cargo hold
+VESSEL.D2.PUMP_RM Pump room
+VESSEL.D2.PUMP_RM.CP1   Pump room control panel
+VESSEL.D2.ELEC_RM Electrical equipment room
+VESSEL.D3.ACCOM   Accommodation deck
+VESSEL.D3.ACCOM.DB1  Accommodation DB 1
+VESSEL.D4.MAST    Mast
+VESSEL.D4.MAST.NAV_LIGHTS Navigation lights
+VESSEL.BRIDGE.HELM   Helm station
+VESSEL.BRIDGE.DP     Dynamic positioning console
+VESSEL.BRIDGE.NAV    Navigation console
+VESSEL.BRIDGE.FIRE   Fire and safety console
+VESSEL.FWD         Forward section
+VESSEL.AFT         Aft section
+VESSEL.AMIDSHIPS   Midship section
```

---

## Rail & Transportation

> Convention: Line → station / section → room → panel. Follows infrastructure asset hierarchy.

### Metro / Light Rail Line
```
+LINE_1            Rail line 1 (top level)
+LINE_1.DEPOT      Depot
+LINE_1.DEPOT.CTRL_BLDG  Depot control building
+LINE_1.DEPOT.MAINT_BLDG Maintenance building
+LINE_1.DEPOT.SUBST      Depot substation
+LINE_1.STN_A      Station A
+LINE_1.STN_A.CTRL_RM    Station control room
+LINE_1.STN_A.SUBST      Station substation
+LINE_1.STN_A.SUBST.MV_SW    MV switchgear
+LINE_1.STN_A.SUBST.DB_MAIN  Station main DB
+LINE_1.STN_A.L1         Station level 1 (concourse)
+LINE_1.STN_A.L1.DB_L1   Level 1 distribution board
+LINE_1.STN_A.L1.PA_CAB  PA/communications cabinet
+LINE_1.STN_A.L1.CCTV    CCTV equipment
+LINE_1.STN_A.PLATFORM   Platform level
+LINE_1.STN_A.PLATFORM.DB_PLT  Platform DB
+LINE_1.STN_A.PLATFORM.PSD_CP  PSD control panel
+LINE_1.STN_B      Station B
+LINE_1.TUNNEL_A   Tunnel section A
+LINE_1.TUNNEL_A.VENT_A  Tunnel ventilation A
+LINE_1.TUNNEL_A.JB1     Tunnel junction box 1
+LINE_1.TRAC_SS_1  Traction substation 1
+LINE_1.TRAC_SS_1.RECT   Rectifier
+LINE_1.TRAC_SS_1.CTRL_PANEL  Control panel
```

---

## Data Centre & IT Infrastructure

> Convention: Campus → data hall / room → row → rack. Follows TIA-942 / EN 50600 space hierarchy.

```
+DC                Data centre facility
+DC.MDA            Main distribution area
+DC.MDA.MSB        Main switchboard
+DC.MDA.GENSET_RM  Generator room
+DC.MDA.GENSET_RM.GEN1  Generator 1
+DC.MDA.GENSET_RM.GEN2  Generator 2
+DC.MDA.GENSET_RM.ATS1  ATS 1
+DC.MDA.UPS_RM     UPS room
+DC.MDA.UPS_RM.UPS_A  UPS system A
+DC.MDA.UPS_RM.UPS_B  UPS system B
+DC.MDA.BATT_RM    Battery room
+DC.COOL_PLANT     Cooling plant room
+DC.COOL_PLANT.CHILLER1  Chiller 1
+DC.COOL_PLANT.CHILLER2  Chiller 2
+DC.COOL_PLANT.CT1 Cooling tower 1
+DC.COOL_PLANT.CT2 Cooling tower 2
+DC.HALL_A         Data hall A
+DC.HALL_A.HDA1    Horizontal distribution area 1
+DC.HALL_A.HDA1.PDU_A1  PDU A1
+DC.HALL_A.HDA1.PDU_B1  PDU B1
+DC.HALL_A.ROW_1   Row 1
+DC.HALL_A.ROW_1.RACK_A01  Rack A01
+DC.HALL_A.ROW_1.RACK_A02  Rack A02
+DC.HALL_A.ROW_1.CRAC1     CRAC unit 1
+DC.HALL_B         Data hall B
+DC.HALL_B.ROW_1   Row 1 in hall B
+DC.NETWORK_RM     Network / telecoms room
+DC.NOC            Network operations centre
+DC.SECURITY_RM    Security control room
+DC.LOADING_DOCK   Loading dock
```

---

## Mining & Heavy Industry

> Convention: Site → area → structure → panel. Area codes often match mine plan grid or plant area numbering.

```
+MINE_SITE         Mine site (top level)
+MINE_SITE.PIT     Open pit area
+MINE_SITE.ROM     Run-of-mine stockpile
+MINE_SITE.CRUSH   Crushing plant
+MINE_SITE.CRUSH.CP_PRI    Primary crusher control panel
+MINE_SITE.CRUSH.CP_SEC    Secondary crusher control panel
+MINE_SITE.CRUSH.MCC1      Crushing MCC 1
+MINE_SITE.CRUSH.SUBST     Crushing substation
+MINE_SITE.GRIND   Grinding circuit
+MINE_SITE.GRIND.CP1       Grinding control panel
+MINE_SITE.GRIND.MCC2      Grinding MCC 2
+MINE_SITE.FLOAT   Flotation circuit
+MINE_SITE.FLOAT.CP1       Flotation control panel
+MINE_SITE.TAILING Tailings area
+MINE_SITE.TAILING.CP1     Tailings control panel
+MINE_SITE.PROCESS_CTRL    Process control building
+MINE_SITE.PROCESS_CTRL.DCS_CAB1  DCS cabinet 1
+MINE_SITE.PROCESS_CTRL.DCS_CAB2  DCS cabinet 2
+MINE_SITE.PROCESS_CTRL.UPS_CAB   UPS cabinet
+MINE_SITE.MAIN_SUBST  Main substation
+MINE_SITE.MAIN_SUBST.HV_SW   HV switchgear
+MINE_SITE.MAIN_SUBST.TX1     Main transformer 1
+MINE_SITE.MAIN_SUBST.MV_SW   MV switchgear
+MINE_SITE.SS_CRUSH    Crushing area substation
+MINE_SITE.SS_GRIND    Grinding area substation
+MINE_SITE.WORKSHOP    Maintenance workshop
+MINE_SITE.WORKSHOP.MCC_WS   Workshop MCC
+MINE_SITE.ADMIN   Administration building
+MINE_SITE.WAREHOUSE   Warehouse
+MINE_SITE.CONVEY  Conveyor transfer stations
+MINE_SITE.CONVEY.TS1  Transfer station 1
+MINE_SITE.CONVEY.TS2  Transfer station 2
+MINE_SITE.CONVEY.OLC  Overland conveyor route
```

---

## HVAC Systems

> Convention: Building → plant room / floor → equipment room → enclosure. Mirrors mechanical services layout.

```
+BLDG              Building
+BLDG.PLANT_RM     Main plant room
+BLDG.PLANT_RM.AHU_1      AHU 1 location
+BLDG.PLANT_RM.AHU_2      AHU 2 location
+BLDG.PLANT_RM.FCU_RM     Fan coil unit plant room
+BLDG.PLANT_RM.CHILLER_1  Chiller 1 location
+BLDG.PLANT_RM.CHILLER_2  Chiller 2 location
+BLDG.PLANT_RM.BOILER_1   Boiler 1 location
+BLDG.PLANT_RM.BOILER_2   Boiler 2 location
+BLDG.PLANT_RM.PUMP_SET   Pump set location
+BLDG.PLANT_RM.MCC1       HVAC MCC 1
+BLDG.PLANT_RM.BMS_CAB    BMS controller cabinet
+BLDG.ROOF         Roof
+BLDG.ROOF.CT1     Cooling tower 1
+BLDG.ROOF.CT2     Cooling tower 2
+BLDG.ROOF.ERV     Energy recovery unit
+BLDG.ROOF.EAH     Exhaust air hood
+BLDG.L1           Level 1
+BLDG.L1.ELEC_RISER.DB_L1  Level 1 HVAC DB
+BLDG.L1.FCU_1     FCU at level 1, position 1
+BLDG.L1.FCU_2     FCU at level 1, position 2
+BLDG.L2           Level 2
+BLDG.L2.AHU_3     AHU 3 at level 2 (roof of level 2)
+BLDG.CARPARK.CP1  Carpark ventilation panel
+BLDG.FIRE_RM      Fire pump room
+BLDG.FIRE_RM.CP1  Fire pump control panel
```

---

## Safety & SIL Systems

> Convention: Mirrors the primary plant location structure. Safety equipment co-located with process, so `+` follows process areas. SIL-rated cabinets often in segregated safety rooms.

```
+SAFE_RM           Dedicated safety equipment room (where segregated)
+SAFE_RM.SIS_CAB1  SIS logic solver cabinet 1
+SAFE_RM.SIS_CAB2  SIS logic solver cabinet 2
+SAFE_RM.ESD_CAB   ESD cabinet
+SAFE_RM.F&G_CAB   F&G controller cabinet
+SAFE_RM.UPS_CAB   Safety UPS cabinet
+CTRL_RM           Control room (where safety is co-located)
+CTRL_RM.SIS_CAB   SIS cabinet in control room
+AREA_A            Process area A (field safety devices)
+AREA_A.JB_SAFE1   Safety junction box 1 (segregated from process JBs)
+AREA_A.JB_SAFE2   Safety junction box 2
+AREA_A.ESTOP_1    E-stop post 1
+AREA_A.ESTOP_2    E-stop post 2
+PLANT.SAFE_RM     Plant-level safety room
+PLANT.SAFE_RM.SIS_CAB   SIS cabinet
+PLANT.SAFE_RM.FIRE_CAB  Fire panel
+PLATFORM.SAFE_RM  Offshore platform safety room
+PLATFORM.SAFE_RM.ESD_CAB  ESD cabinet
+PLATFORM.SAFE_RM.F&G_CAB  F&G cabinet
```

---

## Full Structure Examples

### Example 1 — Pump Station (simple project)
```
Full tag:   =CTRL+CP1-K1
Meaning:    Control relay K1, located in control panel CP1

Full tag:   =PWR+MCC1-Q3
Meaning:    Contactor Q3, located in MCC 1

Full tag:   =INST+FIELD-FT101
Meaning:    Flow transmitter FT101, in field (no enclosure)

Full tag:   =SCADA+CTRL_RM.SCADA_CAB-CPU
Meaning:    SCADA CPU, in SCADA cabinet, in control room

Full tag:   =SAFE+MCC1-F1_SAFE
Meaning:    Motor protection relay, in MCC 1, safety function
```

### Example 2 — Process Plant (multi-level)
```
=U30+PLANT.AREA_30.MCC1-Q5        Contactor Q5, MCC1, area 30
=CTRL+PLANT.CTRL_BLDG.CR.DCS1-CPU DCS CPU, cabinet DCS1, control room
=INST+PLANT.AREA_30.FIELD-PT301    Pressure xmtr PT301, field, area 30
=SAFE+PLANT.AREA_30.JB_SAFE1-F3    Safety relay, safe JB1, area 30
=UTIL+PLANT.UTIL.UPS_RM.UPS1-CB1   Circuit breaker, UPS 1, UPS room
```

### Example 3 — Substation (IEC 81346 aligned)
```
=Q1+SUBST.YARD.TX1-Q1      Main transformer incomer isolator in TX1 bay
=F1.PROT+SUBST.CTRL_BLDG.RELAY_RM.PNL_A-K21   Overcurrent relay in relay panel A
=G1+SUBST.CTRL_BLDG.BATT_RM-G1                 Battery bank in battery room
=D1+SUBST.CTRL_BLDG.RELAY_RM.SCADA-CPU         RTU/SCADA CPU in relay room
```

### Example 4 — Machine with Multiple Panels
```
=CTRL.PLC+MACHINE.CP1-CPU         PLC CPU in main control panel
=CTRL.IO+MACHINE.CP1-DI01         DI module in main control panel
=DRIVE.X+MACHINE.CP1-VFD_X        X-axis VFD in main control panel
=CTRL.HMI+MACHINE.OP1-TP700       HMI at operator station 1
=SENS.POS+MACHINE.FIELD-B1        Proximity sensor on machine field
=SAFE.GUARD+MACHINE.CP1-F3_SAFE   Safety relay in main control panel
=ACT.PNEU+MACHINE.FIELD-YV1       Solenoid valve in machine field
```

---

## Location vs Function — Side by Side

| Aspect | Function `=` | Location `+` |
|--------|-------------|--------------|
| Answers | *What does it do?* | *Where is it?* |
| Example | `=CTRL` (control function) | `+CP1` (control panel 1) |
| Hierarchy | Functional decomposition | Physical/spatial hierarchy |
| Standard | IEC 81346 function classes | IEC 81346 spatial hierarchy |
| Driven by | System architecture / P&ID | Site layout / drawings |
| Changes when | System design changes | Physical installation changes |
| Used for | Filtering by system | Filtering by panel / area |
| Typical depth | 1–3 levels | 2–4 levels |

### Common Pairings
```
=CTRL    +CP1           Control relay in control panel 1
=PWR     +MCC1          Power contactor in MCC 1
=DRIVE   +CP1           VFD in control panel
=SAFE    +MCC1          Safety relay in MCC 1
=INST    +FIELD         Field instrument (no panel)
=SCADA   +CTRL_RM.CAB1  PLC in control room cabinet 1
=UTIL    +UPS_RM.UPS1   Circuit breaker in UPS system 1
```

---

## Common Mistakes

| ❌ Wrong | ✅ Correct | Reason |
|----------|------------|--------|
| `+CONTROL_SYSTEM` | `=CTRL` | Control system is a function, not a location |
| `+MOTOR_CTRL` | `=CTRL` with `+MCC1` | Motor control is function; MCC1 is location |
| `+PUMP_1` | `+FIELD` or `+JB1` | Pump 1 is a device (`-P1`), not a location |
| Leaving `+` blank for field devices | `+FIELD` or `+JB1` | Blank location breaks cable and terminal reports |
| `+MAIN_SWITCHBOARD_ROOM` | `+MSB_RM` | Too long — truncated in reports |
| Different naming per engineer | Agree on convention at project start | Inconsistency ruins report filtering |
| `+PANEL A` (with space) | `+PANEL_A` | Spaces break EPLAN structure |
| Starting with number: `+1MCC` | `+MCC1` | Numbers should not lead in most naming conventions |
| Mixing depth: some `+MCC`, some `+SITE.PLANT.MCC` | Consistent depth throughout | Mixed depth makes report filtering unreliable |
| Putting instrument tag in location: `+FT101` | `+FIELD-FT101` | FT101 is a device tag `-FT101`, not a location |

---

## Expert Tips

### 1. Define your location hierarchy before page 1
> Sketch the physical layout: site → building → room → panel. Lock this down before drawing starts. Changing location structure mid-project is painful.

### 2. Match `+` to your panel schedule and single-line diagram
> If your SLD calls it `MCC-1A`, your EPLAN location should be `+MCC_1A`. Consistency across documents saves hours during FAT and installation.

### 3. Always give field devices a location
> Even if a device is just bolted to a machine, use `+MACHINE.FIELD` or `+FIELD`. A blank `+` location causes missing entries in cable schedules and terminal reports.

### 4. Keep location names short but recognisable
> `+CTRL_RM` is better than `+CENTRAL_CONTROL_ROOM`. Names appear in report column headers — long names truncate.

### 5. Use location to drive cable routing logic
> In EPLAN Topology, `+` locations become nodes on your routing network. A clean `+` structure = automatic cable length estimation that actually works.

### 6. Reserve `+FIELD` as a catch-all for unenclosed devices
> Any sensor, actuator, or instrument without a dedicated enclosure should land on `+FIELD` or `+AREA_XX.FIELD`. This keeps terminal and connection reports clean.

### 7. Align with the client's asset register
> Many clients have existing asset hierarchies (SAP, Maximo, IBM Maximo). If their asset register calls the room `CR-01`, your `+` designation should match: `+CR_01`.

### 8. Create a location structure page early
> Use a `Structure identifier overview` page type in EPLAN to document and display your full `+` hierarchy. It acts as a quick reference for the whole team.

### 9. Consider maintenance access zones
> Group locations logically by who maintains them. A panel maintained by the client's electrical team should have a different location than one maintained by an automation vendor — this makes filtering maintenance documentation far easier.

### 10. Test your location structure with one report before full build-out
> Run a terminal diagram or cable schedule early with just a few pages. If the location filtering, grouping, and sorting all look correct, proceed. If not, fix the structure before it's replicated across hundreds of pages.

---

*Based on IEC 81346 | IEC 61355 | TIA-942 | EN 50600 | ISO 10628 | IACS Rules*
*Expert conventions compiled from machine building, process, energy, infrastructure, maritime, and data centre industries*
