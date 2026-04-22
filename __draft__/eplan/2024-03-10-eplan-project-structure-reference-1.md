---
layout: post
cover_color: #000000

keywords: EPLAN P8, Project Structure, Forms, Reports, Document Types, Electrical Design, Project Documentation, Standard Forms, Report Generation, EPLAN P8 Reference

title: "EPLAN Project Structure Reference Guide"

description: >-
  A comprehensive reference guide to the standard report and form structure of an EPLAN Electric P8 project, including form types, purposes, examples, and applicable standards.

date: 2024-03-10 10:00:00 +0800
author: Mahmoud Lotfi
file_name: 2024-03-10-eplan-project-structure-reference-1.md
categories: [EPLAN, Project Structure, Reference]
tags: [Eplan, project structure, reference]
pin: False
math: true
mermaid: true
comments: true
toc: true
render_with_liquid: false

image:
  path: /assets/img/posts/eplan.jpg
  alt: EPLAN Project Structure Reference Guide
  lqip: data:image/webp;base64,UklGRjoAAABXRUJQVlA4IC4AAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA

---

# EPLAN P8 — Project Structure Reference Guide
> How to organise the project tree | Structure identifiers | Page hierarchy | Naming conventions across machine building, process, power, panel building, and system integration industries

This one focuses entirely on the **project tree hierarchy** like what you saw in the image. Here's what's covered in **35 sections**:

**Foundation:**
- What the project tree actually is and why it matters for reports, filtering, and navigation
- The three axes (`=` function, `+` location, `&` installation)
- Structure depth recommendations (shallow vs deep)
- Page naming and **4 numbering strategies** (flat, block-by-structure, panel-coded, hierarchical dot)

**The sample project annotated** — every line in the image explained: why `K1 (PLC controller)` is a top-level node, why `HK1 (Paint workpiece)` contains its own P&IDs and sub-functions, why `GAA / GAB1 / GAB2` are separate power nodes

**Industry structures (all with full tree diagrams):**
- Machine building — single machine, multi-station transfer line, robotic cell
- Panel building — single panel, multi-panel project, MCC (with section-level nodes), MV switchgear
- Process & chemical plant — per-unit structure (`=U10` through `=U60`) with marshalling and DCS
- Oil & gas — LER rooms, ESD/SIS cabinet, F&G system
- Water & wastewater, Power substation, BAS/BMS, PLC/SCADA/DCS
- Solar PV, Wind, Marine, Rail, Data centre, Food & pharma, Mining
- Multi-site and multi-unit replication patterns

**Standards tables:**
- Complete **EPLAN page type → IEC 61355 document code mapping** table
- Mandatory admin pages list with exact content description per page

---

## Table of Contents
- [EPLAN P8 — Project Structure Reference Guide](#eplan-p8--project-structure-reference-guide)
  - [Table of Contents](#table-of-contents)
  - [Fundamentals — What Is the Project Structure?](#fundamentals--what-is-the-project-structure)
    - [Why It Matters](#why-it-matters)
    - [The Three Axes of Structure](#the-three-axes-of-structure)
  - [Structure Identifier Types in EPLAN](#structure-identifier-types-in-eplan)
    - [How EPLAN Displays the Tree](#how-eplan-displays-the-tree)
    - [Structure Depth — Recommendations](#structure-depth--recommendations)
  - [Page Naming \& Numbering Conventions](#page-naming--numbering-conventions)
    - [Page Number Strategies](#page-number-strategies)
    - [Page Description Conventions](#page-description-conventions)
  - [The Sample Project Explained (from image)](#the-sample-project-explained-from-image)
    - [Annotated Tree from Image](#annotated-tree-from-image)
    - [Key Observations from Sample](#key-observations-from-sample)
  - [Machine Building — Project Structure](#machine-building--project-structure)
    - [Single Machine (simple)](#single-machine-simple)
    - [Multi-Station Machine / Transfer Line](#multi-station-machine--transfer-line)
    - [Robotic Cell](#robotic-cell)
  - [Panel Building — Project Structure](#panel-building--project-structure)
    - [Single Panel (standalone)](#single-panel-standalone)
    - [Multi-Panel Project (typical)](#multi-panel-project-typical)
  - [MCC / Switchgear Project Structure](#mcc--switchgear-project-structure)
    - [Large MCC (multi-section, many feeders)](#large-mcc-multi-section-many-feeders)
    - [MV Switchgear Project](#mv-switchgear-project)
  - [Process \& Chemical Plant](#process--chemical-plant)
  - [Oil \& Gas Project Structure](#oil--gas-project-structure)
  - [Water \& Wastewater Treatment](#water--wastewater-treatment)
  - [Power Distribution \& Substation](#power-distribution--substation)
  - [Building Automation (BAS/BMS)](#building-automation-basbms)
  - [PLC / SCADA / DCS Project Structure](#plc--scada--dcs-project-structure)
  - [Renewable Energy — Solar PV](#renewable-energy--solar-pv)
  - [Renewable Energy — Wind](#renewable-energy--wind)
  - [Marine \& Shipbuilding](#marine--shipbuilding)
  - [Rail \& Transportation](#rail--transportation)
  - [Data Centre \& IT Infrastructure](#data-centre--it-infrastructure)
  - [Food \& Beverage / Pharmaceutical](#food--beverage--pharmaceutical)
  - [Mining \& Heavy Industry](#mining--heavy-industry)
  - [Multi-Site / Multi-Unit Project Structure](#multi-site--multi-unit-project-structure)
    - [Multi-Site SCADA Project](#multi-site-scada-project)
    - [Multi-Unit Identical Process (replication)](#multi-unit-identical-process-replication)
  - [Standard Cover Pages \& Admin Pages](#standard-cover-pages--admin-pages)
    - [Mandatory Admin Pages](#mandatory-admin-pages)
    - [Optional Admin Pages](#optional-admin-pages)
  - [Page Type to Document Type Mapping](#page-type-to-document-type-mapping)
  - [Numbering Strategies](#numbering-strategies)
    - [Strategy 1 — Flat Sequential (small projects, \<50 pages)](#strategy-1--flat-sequential-small-projects-50-pages)
    - [Strategy 2 — Block-by-Structure (recommended for medium projects)](#strategy-2--block-by-structure-recommended-for-medium-projects)
    - [Strategy 3 — Panel-Coded (panel building standard)](#strategy-3--panel-coded-panel-building-standard)
    - [Strategy 4 — Hierarchical Dot (large plant / DCS)](#strategy-4--hierarchical-dot-large-plant--dcs)
    - [Page Counter Reset Options](#page-counter-reset-options)
  - [Common Mistakes](#common-mistakes)
  - [Expert Tips](#expert-tips)
    - [1. Plan the structure before creating page 1](#1-plan-the-structure-before-creating-page-1)
    - [2. Match the project structure to the client's asset hierarchy](#2-match-the-project-structure-to-the-clients-asset-hierarchy)
    - [3. Admin pages always come first — no exceptions](#3-admin-pages-always-come-first--no-exceptions)
    - [4. Keep report pages separate and at the end](#4-keep-report-pages-separate-and-at-the-end)
    - [5. Use descriptive page descriptions — not just page numbers](#5-use-descriptive-page-descriptions--not-just-page-numbers)
    - [6. Give field device pages their own `+FIELD` or `+JB_XX` location](#6-give-field-device-pages-their-own-field-or-jb_xx-location)
    - [7. Sub-systems get sub-nodes — don't flatten everything](#7-sub-systems-get-sub-nodes--dont-flatten-everything)
    - [8. Use the same page structure for repeated units](#8-use-the-same-page-structure-for-repeated-units)
    - [9. Overview and architecture pages belong at the top of each major section](#9-overview-and-architecture-pages-belong-at-the-top-of-each-major-section)
    - [10. Document your structure in page EAC (Structure description)](#10-document-your-structure-in-page-eac-structure-description)

---

## Fundamentals — What Is the Project Structure?

The project structure in EPLAN is the **tree hierarchy** visible in the Pages navigator. It organises every page into a logical, navigable structure using **structure identifiers** as folder nodes.

### Why It Matters
```
✔ Determines how reports are filtered and grouped
✔ Controls how terminal diagrams, cable lists, and BOMs are sorted
✔ Defines the page numbering and cross-reference logic
✔ Makes the documentation navigable for engineers, clients, and maintenance
✔ Affects how EPLAN auto-generates interconnection and connection lists
```

### The Three Axes of Structure
EPLAN allows structuring the page tree using any combination of:
```
=   Function (what system / subsystem)
+   Location (where physically)
&   Installation (which installation / unit — less commonly used)
#   Document type / higher-level grouping
```

In practice most projects use one or two axes:
```
Common combinations:
=FUNCTION only          → Machine builders (group by system)
+LOCATION only          → Panel builders (group by panel)
=FUNCTION+LOCATION      → Process and large projects (group by system then panel)
+LOCATION=FUNCTION      → Alternative ordering (group by location then system)
```

---

## Structure Identifier Types in EPLAN

### How EPLAN Displays the Tree
Each node in the project tree is a **unique combination of structure identifiers**. EPLAN creates a folder automatically when a page is assigned those identifiers.

```
Project root
  └─ =CTRL                          Function node
       └─ +CP1                       Location node
            ├─ Page 1 (Cover)
            ├─ Page 2 (PLC schematic)
            └─ Page 3 (I/O list)
  └─ =PWR
       └─ +MCC1
            ├─ Page 1 (Incomer)
            ├─ Page 2 (Feeder 1)
            └─ Page 3 (Terminal diagram)
```

### Structure Depth — Recommendations
```
Shallow (1 level):    Good for small single-panel projects
  +MCC1 → pages

Medium (2 levels):    Good for most projects
  =CTRL+CP1 → pages
  =PWR+MCC1 → pages

Deep (3 levels):      Good for large multi-site projects
  =UNIT_30+AREA_A.MCC1 → pages
  =CTRL+PLANT.CTRL_RM.CAB1 → pages
```

---

## Page Naming & Numbering Conventions

### Page Number Strategies
```
Strategy 1 — Sequential flat numbers (simple projects)
  1, 2, 3, 4 ... 100, 101, 102

Strategy 2 — Structure-coded numbers (recommended)
  Each structure node gets a number block:
  AAA pages  →  0001 - 0099  (admin / cover)
  =CTRL       →  1000 - 1099
  =PWR        →  2000 - 2099
  =DRIVE      →  3000 - 3099
  =SAFE       →  4000 - 4099

Strategy 3 — Hierarchical dot notation
  1.1, 1.2, 1.3  (section 1)
  2.1, 2.2, 2.3  (section 2)
  3.1.1, 3.1.2   (sub-section)

Strategy 4 — Structure prefix + number
  CTRL-001, CTRL-002
  PWR-001, PWR-002
  MCC1-001, MCC1-002
```

### Page Description Conventions
```
Format: [Panel/System Tag] [Circuit description]
Examples:
  MCC1 — Incomer and bus section
  MCC1 / M01 — DOL starter pump P-101
  CP1 — PLC CPU and power supply
  CP1 — Digital inputs 1-32
  DB1 — Lighting circuits L1-L12
  TX1 — Transformer protection
```

---

## The Sample Project Explained (from image)

> The image shows `EPLAN_Sample_Project_Education` — a training/demonstration project showing best-practice structure for an automated manufacturing/paint workstation system.

### Annotated Tree from Image
```
EPLAN_Sample_Project_Education          ← Project root
│
├── AAA1  Title page / cover sheet      ← EAA — Admin, cover sheet
├── AAB1  Table of contents             ← EAB — Lists regarding documents
├── ADB1  Structure description         ← EAC — Explanatory documents
├── EFA2  Overview "PROFINET"           ← EFA — Functional overview (network topology)
├── EMA3  Connection list               ← EMA — Connection documents
│
├── A1    Enclosure 1                   ← Location A1 — first cabinet
├── A2    Enclosure 2                   ← Location A2 — second cabinet
│
├── B1    Station "Feed"                ← Functional area / station B1
├── B2    Station "Work"                ← Functional area / station B2
├── B3    Station "Provide"             ← Functional area / station B3
│
├── C2    Control panel                 ← Location C2 — control panel
│
├── B4    Field                         ← Location B4 — field devices (no enclosure)
│
├── GAA   400V power supply             ← Power supply section (=PWR / +MSB)
├── GAB1  24V device power supply       ← 24VDC device supply
├── GAB2  24V supply PLC signals        ← 24VDC PLC signal supply
│
├── EA    Lighting                      ← Lighting circuits (=LIGHT)
│
├── F     Emergency-stop control        ← Safety / E-stop system (=SAFE.ESTOP)
│
├── K1    PLC controller ← (selected)   ← PLC system (=CTRL.PLC)
│
├── S1    Machine operation enclosure   ← Operator enclosure (=CTRL.HMI / +OP_ENCL)
├── S2    Machine operation control panel ← Operator control panel (=CTRL / +OP_PANEL)
│
├── GL1   Feed workpiece: Transport     ← Process function — feed transport
│
├── TM1   Work workpiece: Grind         ← Process function — grinding station
│    ├── A1  Enclosure 1               ← Sub-location inside TM1
│    └── A2  Enclosure 2               ← Sub-location inside TM1
│
├── HK1   Paint workpiece              ← Process function — paint station
│    ├── PFB   P&I diagrams            ← EFB — Flow diagrams / P&ID
│    ├── EDB   Explanatory documents   ← EDB — Explanatory docs for paint station
│    ├── HW1   Prepare basic color red ← Sub-function — colour preparation
│    └── HW2   Mix paint color red     ← Sub-function — paint mixing
```

### Key Observations from Sample
```
1. Admin pages come first (AAA, AAB, ADB) — always
2. System overview pages come after admin (EFA, EMA)
3. Physical enclosures (A1, A2, C2) are used as structure nodes
4. Functional stations (B1, B2, B3) represent machine work areas
5. Power supplies (GAA, GAB) are separated from control
6. Safety system (F) is a separate top-level node
7. PLC (K1) is its own top-level node
8. Operator interfaces (S1, S2) are separate from PLC
9. Process functions (GL1, TM1, HK1) use descriptive names
10. Sub-stations (TM1) have their own enclosure sub-nodes (A1, A2)
11. The paint workstation (HK1) contains its own P&ID, docs, and sub-functions
```

---

## Machine Building — Project Structure

> Convention: Admin first → overview → power → control → safety → per-station / per-axis → operator → field → reports

### Single Machine (simple)
```
PROJECT_NAME
│
├── 0_ADMIN
│    ├── 0001  Cover sheet / title page
│    ├── 0002  Table of contents
│    ├── 0003  Revision history
│    ├── 0004  Symbol legend / abbreviations
│    └── 0005  Structure description
│
├── =PWR / +CP1     Power distribution
│    ├── PWR-001    Mains incoming, isolation, transformer
│    ├── PWR-002    24VDC power supplies (SMPS, UPS buffer)
│    ├── PWR-003    24VDC distribution (fused terminal blocks)
│    └── PWR-004    Panel lighting and heating circuits
│
├── =CTRL / +CP1    PLC and control system
│    ├── CTRL-001   PLC CPU, power module, interface module
│    ├── CTRL-002   Digital inputs 1–16 (DI01)
│    ├── CTRL-003   Digital inputs 17–32 (DI02)
│    ├── CTRL-004   Digital outputs 1–16 (DO01)
│    ├── CTRL-005   Digital outputs 17–32 (DO02)
│    ├── CTRL-006   Analog inputs (AI01)
│    ├── CTRL-007   Analog outputs (AO01)
│    └── CTRL-008   Communications module (PROFINET, Modbus)
│
├── =SAFE / +CP1    Safety system
│    ├── SAFE-001   Safety relay wiring (E-stop, guards)
│    ├── SAFE-002   Light curtain / area scanner circuits
│    ├── SAFE-003   Safety I/O modules
│    └── SAFE-004   Safety circuit overview
│
├── =DRIVE / +CP1   Drive system
│    ├── DRIVE-001  X-axis VFD wiring
│    ├── DRIVE-002  Y-axis VFD wiring
│    ├── DRIVE-003  Z-axis VFD wiring
│    └── DRIVE-004  Spindle drive wiring
│
├── =MOTOR / +FIELD  Motor and actuator circuits
│    ├── MOTOR-001  Motor M1 DOL starter
│    ├── MOTOR-002  Motor M2 star-delta starter
│    ├── MOTOR-003  Solenoid valves (pneumatic)
│    └── MOTOR-004  Servo actuators
│
├── =CTRL.HMI / +OP1  Operator station
│    ├── HMI-001    HMI panel wiring
│    ├── HMI-002    Door-mounted push buttons and lamps
│    └── HMI-003    Operator pendant
│
├── =FIELD / +FIELD  Field devices (sensors, limit switches)
│    ├── FIELD-001  Position sensors — section A
│    ├── FIELD-002  Position sensors — section B
│    ├── FIELD-003  Temperature sensors
│    └── FIELD-004  Pressure / flow sensors
│
└── REPORTS
     ├── RPT-001    Terminal diagram
     ├── RPT-002    Cable list
     ├── RPT-003    Parts list / BOM
     ├── RPT-004    Device tag list
     └── RPT-005    Connection list
```

### Multi-Station Machine / Transfer Line
```
PROJECT_NAME
│
├── 0_ADMIN            Cover, TOC, revision, legend
├── OVERVIEW           System architecture, PROFINET topology
│
├── =PWR               Power distribution (main panel)
│    ├── +MSB          Main switchboard
│    └── +MCC1         MCC
│
├── =CTRL              Central PLC system
│    └── +CP_MAIN      Main control cabinet
│
├── =SAFE              Safety system
│    └── +CP_MAIN.SAFE Safety section
│
├── =STN_A             Station A (loading)
│    ├── +STN_A.CP1    Station A control panel
│    ├── +STN_A.FIELD  Station A field devices
│    └── +STN_A.OP1    Station A operator station
│
├── =STN_B             Station B (processing)
│    ├── +STN_B.CP1    Station B control panel
│    ├── +STN_B.FIELD  Station B field devices
│    └── +STN_B.OP1    Station B operator station
│
├── =STN_C             Station C (unloading)
│    ├── +STN_C.CP1    Station C panel
│    └── +STN_C.FIELD  Station C field
│
├── =CONV              Conveyor system
│    ├── +CONV.CP1     Conveyor control panel
│    └── +CONV.FIELD   Conveyor field devices
│
└── REPORTS
```

### Robotic Cell
```
PROJECT_NAME
│
├── 0_ADMIN
├── OVERVIEW           Cell layout, safety zone diagram
│
├── =PWR / +CP_MAIN    Power distribution
├── =CTRL / +CP_MAIN   Cell PLC system
├── =SAFE / +CP_MAIN   Safety system (perimeter, e-stop)
│
├── =ROB.R1 / +CP_R1   Robot 1 controller cabinet
│    ├── ROB1-001      Robot 1 power wiring
│    ├── ROB1-002      Robot 1 I/O interface
│    └── ROB1-003      Robot 1 fieldbus / PROFINET
│
├── =ROB.R2 / +CP_R2   Robot 2 controller cabinet
│
├── =VISION / +CP_MAIN.VISION  Vision system
│    ├── VIS-001       Camera power and trigger wiring
│    └── VIS-002       Vision controller I/O
│
├── =GRIP / +FIELD     End-of-arm tooling
│    ├── GRIP-001      Gripper solenoids
│    └── GRIP-002      Gripper sensors
│
├── =CONV / +FIELD     Infeed / outfeed conveyors
│
└── REPORTS
```

---

## Panel Building — Project Structure

> Convention: Admin → overview → panel by panel → field (if any) → reports
> Focus: Each panel is its own top-level structure node

### Single Panel (standalone)
```
PROJECT_NAME
│
├── ADMIN
│    ├── Cover sheet
│    ├── Table of contents
│    └── Symbol legend
│
├── +MCC1              Motor Control Centre 1
│    ├── MCC1-001      Single-line diagram
│    ├── MCC1-002      Incomer and bus section
│    ├── MCC1-003      Motor feeder M01 — DOL
│    ├── MCC1-004      Motor feeder M02 — DOL
│    ├── MCC1-005      Motor feeder M03 — Star-delta
│    ├── MCC1-006      Motor feeder M04 — VFD
│    ├── MCC1-007      Motor feeder M05 — VFD
│    ├── MCC1-008      Control power supply (24VDC)
│    ├── MCC1-009      Auxiliary relay circuits
│    ├── MCC1-010      PLC integration (if integrated)
│    └── MCC1-011      Panel lighting and heating
│
└── REPORTS
     ├── Terminal diagram — MCC1
     ├── Parts list — MCC1
     └── Cable list
```

### Multi-Panel Project (typical)
```
PROJECT_NAME
│
├── ADMIN
│    ├── Cover sheet
│    ├── Table of contents
│    ├── Revision list
│    ├── Symbol legend
│    └── Single-line diagram (SLD overview)
│
├── +MSB1              Main Switchboard 1
│    ├── MSB1-001      SLD — MSB1 single line
│    ├── MSB1-002      Incomer A (ACB, CT, metering)
│    ├── MSB1-003      Incomer B (ACB, CT, metering)
│    ├── MSB1-004      Bus tie (ACB)
│    ├── MSB1-005      Feeder 1 — to MCC1
│    ├── MSB1-006      Feeder 2 — to MCC2
│    ├── MSB1-007      Feeder 3 — to DB1
│    ├── MSB1-008      Feeder 4 — to UPS
│    ├── MSB1-009      ATS / changeover circuits
│    ├── MSB1-010      Control power and metering
│    └── MSB1-011      Interlocking and indication
│
├── +MCC1              Motor Control Centre 1
│    ├── MCC1-001      SLD — MCC1
│    ├── MCC1-002      Incomer
│    ├── MCC1-003      M01 — Pump P-101 (DOL)
│    ├── MCC1-004      M02 — Pump P-102 (DOL)
│    ├── MCC1-005      M03 — Fan F-101 (VFD)
│    ├── MCC1-006      M04 — Agitator AG-101 (Soft starter)
│    ├── MCC1-007      M05 — Conveyor CV-101 (DOL reversing)
│    ├── MCC1-008      Control power 24VDC
│    └── MCC1-009      Auxiliary relay wiring
│
├── +MCC2              Motor Control Centre 2
│    ├── MCC2-001      SLD — MCC2
│    ├── MCC2-002      Incomer
│    ├── MCC2-003..n   Individual motor feeders
│    └── MCC2-xxx      Control and interlocking
│
├── +DB1               Distribution Board 1
│    ├── DB1-001       Incomer
│    ├── DB1-002       Lighting circuits
│    ├── DB1-003       Power outlet circuits
│    ├── DB1-004       HVAC circuits
│    └── DB1-005       Sub-metering
│
├── +UPS1              UPS System
│    ├── UPS1-001      UPS input / output wiring
│    ├── UPS1-002      Battery cabinet connections
│    └── UPS1-003      UPS distribution board
│
├── +CP1               Control Panel 1
│    ├── CP1-001       PLC power supply
│    ├── CP1-002       PLC CPU and I/O
│    ├── CP1-003       24VDC distribution
│    ├── CP1-004       Relay wiring
│    └── CP1-005       Terminal connections
│
└── REPORTS
     ├── Terminal diagrams (per panel)
     ├── Cable list
     ├── Parts list (per panel and summary)
     └── Device tag list
```

---

## MCC / Switchgear Project Structure

### Large MCC (multi-section, many feeders)
```
PROJECT_NAME_MCC
│
├── ADMIN
│    ├── Cover / title
│    ├── Table of contents
│    ├── Revision list
│    ├── Applicable standards (IEC 61439, etc.)
│    ├── General arrangement drawing
│    └── SLD overview
│
├── +MCC1.INC          Incoming section
│    ├── 001  Incomer ACB / MCCB
│    ├── 002  Current transformers
│    ├── 003  Power quality analyser
│    └── 004  Control power and metering
│
├── +MCC1.BUS          Busbar section
│    └── 001  Busbar arrangement
│
├── +MCC1.SEC_1        Section 1 — motors 1–4
│    ├── S1-001  M01 DOL starter — Pump P-101
│    ├── S1-002  M02 DOL starter — Pump P-102
│    ├── S1-003  M03 Star-delta — Compressor C-101
│    └── S1-004  M04 VFD — Fan F-101
│
├── +MCC1.SEC_2        Section 2 — motors 5–8
│    ├── S2-001  M05 DOL starter
│    ├── S2-002  M06 DOL starter
│    ├── S2-003  M07 VFD
│    └── S2-004  M08 Soft starter
│
├── +MCC1.SEC_3        Section 3 — motors 9–12
│
├── +MCC1.CTRL_SEC     Control section (PLC / MCC intelligence)
│    ├── C-001   PLC CPU and power
│    ├── C-002   Digital I/O modules
│    ├── C-003   Analog I/O modules
│    ├── C-004   Communications (PROFINET/Modbus)
│    ├── C-005   24VDC distribution
│    ├── C-006   Auxiliary relay circuits
│    └── C-007   HMI connection
│
└── REPORTS
     ├── Terminal diagram — per section
     ├── Cable list
     ├── Parts list — per section and summary
     └── Motor feeder schedule
```

### MV Switchgear Project
```
MV_SWITCHGEAR_PROJECT
│
├── ADMIN
│    ├── Cover
│    ├── Table of contents
│    ├── Standards reference (IEC 62271-200)
│    └── Single-line diagram
│
├── +MV_SW1.INC_1      Incomer panel 1
│    ├── 001  VCB and CT/VT wiring
│    ├── 002  Protection relay wiring (REF615 / SEL-751)
│    ├── 003  Trip/close coil circuits
│    └── 004  Local control and indication
│
├── +MV_SW1.INC_2      Incomer panel 2
│
├── +MV_SW1.BUS_SEC    Bus section panel
│    ├── 001  Bus tie VCB
│    └── 002  Bus section protection
│
├── +MV_SW1.FDR_1      Feeder panel 1
│    ├── 001  VCB wiring
│    ├── 002  Protection relay
│    └── 003  Control and indication
│
├── +MV_SW1.FDR_2      Feeder panel 2
├── +MV_SW1.FDR_3      Feeder panel 3
├── +MV_SW1.TX_FDR1    Transformer feeder 1
├── +MV_SW1.MTR_FDR1   MV motor feeder 1
│
├── +MV_SW1.METER      Metering panel
│    ├── 001  VT and metering wiring
│    └── 002  Energy meter and PQ analyser
│
└── REPORTS
     ├── Terminal diagrams
     ├── Cable list (DC auxiliary cables)
     └── Protection relay setting schedule
```

---

## Process & Chemical Plant

> Convention: Admin → P&IDs → per functional area → utilities → control room → reports
> Structure: `=UNIT_XX` as primary nodes, `+AREA` as secondary

```
PROCESS_PLANT_PROJECT
│
├── ADMIN
│    ├── Cover sheet
│    ├── Table of contents
│    ├── Revision history
│    ├── Project basis of design
│    ├── Symbol legend / abbreviations
│    ├── Applicable standards
│    └── Site layout plan
│
├── OVERVIEW
│    ├── OV-001   Electrical SLD (high level)
│    ├── OV-002   Control system architecture
│    ├── OV-003   Network topology (PROFINET / DCS)
│    └── OV-004   Safety system overview (SIL)
│
├── =U10  Raw material intake
│    ├── +U10.MCC1
│    │    ├── U10-MCC1-001   Incomer
│    │    ├── U10-MCC1-002   Conveyor M-1001 DOL
│    │    ├── U10-MCC1-003   Conveyor M-1002 DOL
│    │    └── U10-MCC1-004   Control 24VDC
│    ├── +U10.CP1
│    │    ├── U10-CP1-001    PLC I/O for area 10
│    │    └── U10-CP1-002    Field junction box wiring
│    └── +U10.FIELD
│         ├── U10-FIELD-001  Instruments FT-1001, PT-1001
│         └── U10-FIELD-002  Instruments LT-1001, TT-1001
│
├── =U20  Pre-treatment
│    ├── +U20.MCC1
│    ├── +U20.CP1
│    └── +U20.FIELD
│
├── =U30  Reaction
│    ├── +U30.MCC1          Reactor area MCC
│    │    ├── U30-MCC1-001  Incomer
│    │    ├── U30-MCC1-002  Agitator M-3001 (VFD)
│    │    ├── U30-MCC1-003  Circulation pump M-3002 (soft starter)
│    │    └── U30-MCC1-004  Cooling water pump M-3003 (DOL)
│    ├── +U30.PLC_CAB       Remote PLC / DCS I/O
│    │    ├── U30-PLC-001   DCS field control station
│    │    ├── U30-PLC-002   AI modules (flow, pressure)
│    │    ├── U30-PLC-003   AO modules (control valves)
│    │    ├── U30-PLC-004   DI modules (switches)
│    │    └── U30-PLC-005   DO modules (on/off)
│    ├── +U30.JB_R01        Junction box at reactor R-301
│    │    └── JB-R01-001    Instruments at R-301
│    └── +U30.FIELD
│         ├── U30-FIELD-001 FT-3001, PT-3001, TT-3001
│         └── U30-FIELD-002 Control valves FCV-3001, PCV-3001
│
├── =U40  Separation
├── =U50  Purification
├── =U60  Product storage
│
├── =UTIL  Utilities
│    ├── +UTIL.COMPRESS_RM  Compressor room
│    ├── +UTIL.BOILER_RM    Boiler room
│    ├── +UTIL.WATER        Water treatment
│    └── +UTIL.SUBST        Electrical substation
│
├── =CTRL_SYS  Central control system
│    ├── +CTRL_RM.DCS_CAB1  DCS cabinet 1
│    │    ├── DCS-001        FCS A (primary controller)
│    │    ├── DCS-002        FCS B (redundant)
│    │    ├── DCS-003        AI modules — rack A
│    │    ├── DCS-004        AO modules
│    │    ├── DCS-005        DI modules
│    │    └── DCS-006        DO modules
│    ├── +CTRL_RM.DCS_CAB2  DCS cabinet 2 (expansion I/O)
│    ├── +CTRL_RM.HIST_CAB  Historian server cabinet
│    └── +CTRL_RM.NET_CAB   Network cabinet
│
├── =SIS  Safety instrumented system
│    ├── +CTRL_RM.SIS_CAB1  SIS cabinet
│    │    ├── SIS-001        Logic solver A
│    │    ├── SIS-002        Logic solver B
│    │    ├── SIS-003        Safety I/O rack A
│    │    └── SIS-004        Safety I/O rack B
│    └── MARSH_SAFE         Safety marshalling
│
└── REPORTS
     ├── Terminal diagrams (per cabinet / JB)
     ├── Cable list
     ├── I/O list
     ├── Instrument index
     └── Parts list / BOM
```

---

## Oil & Gas Project Structure

```
OIL_GAS_PROJECT
│
├── ADMIN
│    ├── Cover, TOC, revision
│    ├── Applicable codes (IEC 60079, IEC 61511, API RP 14C)
│    ├── Area classification drawing
│    └── Electrical SLD
│
├── OVERVIEW
│    ├── Electrical power SLD
│    ├── ICSS architecture
│    ├── Network topology
│    ├── Safety system overview
│    └── Area classification summary
│
├── =WELLHEAD / +WELLHEAD    Wellhead control panel
├── =SEP / +LER_A            Separator area
│    ├── +LER_A.MCC1         Separator MCC
│    ├── +LER_A.PLC_CAB      PLC cabinet
│    └── +LER_A.JB_S01       Junction box at separator S-101
│
├── =COMPRESS / +LER_B       Compression area
│    ├── +LER_B.MCC2         Compressor MCC
│    ├── +LER_B.PLC_CAB      Remote I/O cabinet
│    └── +LER_B.JB_K01       Junction box at compressor K-101
│
├── =EXPORT / +LER_C         Export area
│
├── =UTIL / +UTIL_RM         Utilities
│    ├── +UTIL_RM.GEN_RM     Generator room
│    └── +UTIL_RM.UPS_RM     UPS room
│
├── =ESD / +CTRL_RM.SIS_CAB  ESD / Safety system
│    ├── ESD-001   Logic solver A (Triconex / HIMA)
│    ├── ESD-002   Logic solver B
│    ├── ESD-003   Logic solver C (TMR)
│    ├── ESD-004   Safety I/O rack
│    ├── ESD-005   ESD relay cabinet
│    └── ESD-006   Safety marshalling cabinet
│
├── =F_G / +CTRL_RM.F_G_CAB  Fire and gas system
│    ├── FG-001    F&G controller
│    ├── FG-002    Fire detectors zone A
│    ├── FG-003    Fire detectors zone B
│    ├── FG-004    Gas detectors zone A
│    └── FG-005    Gas detectors zone B
│
├── =ICSS / +CTRL_RM         Integrated control and safety system
│    ├── +CTRL_RM.DCS_CAB    DCS cabinets
│    ├── +CTRL_RM.HIST_CAB   Historian
│    └── +CTRL_RM.NET_CAB    Network
│
└── REPORTS
```

---

## Water & Wastewater Treatment

```
WATER_TREATMENT_PLANT
│
├── ADMIN
│    ├── Cover, TOC, revision
│    └── Site overview / layout
│
├── OVERVIEW
│    ├── Electrical SLD
│    ├── Process overview / PFD
│    └── SCADA architecture
│
├── =INTAKE / +INTAKE.CP1    Intake structure
│    ├── 001  Screen drive motor
│    ├── 002  Intake pump M-101 (VFD)
│    ├── 003  Intake pump M-102 (VFD)
│    └── 004  Level and flow instruments
│
├── =FLOC / +FLOC.CP1        Flocculation area
│    ├── 001  Mixer motors
│    └── 002  Dosing pump motors
│
├── =FILT / +FILT.CP1        Filter building
│    ├── 001  Filter 1 backwash pump
│    ├── 002  Filter 2 backwash pump
│    ├── 003  Air scour blowers
│    └── 004  Filter instruments
│
├── =DOSE / +DOSE.CP1        Chemical dosing building
│    ├── 001  Chlorine dosing pump
│    ├── 002  Lime dosing pump
│    └── 003  Fluoride dosing pump
│
├── =PUMP_STN / +PUMP_STN.MCC1  Pump station
│    ├── 001  Incomer
│    ├── 002  High-lift pump 1 (VFD)
│    ├── 003  High-lift pump 2 (VFD)
│    ├── 004  High-lift pump 3 (standby)
│    └── 005  Panel control 24VDC
│
├── =SUBST / +SUBST          Electrical substation
│    ├── +SUBST.MV_SW        MV switchgear
│    ├── +SUBST.TX1          Transformer 1
│    ├── +SUBST.MSB1         LV main switchboard
│    └── +SUBST.DB1          Sub-distribution board
│
├── =SCADA / +CTRL_BLDG.CR   Control room / SCADA
│    ├── +CTRL_BLDG.CR.SCADA_CAB   SCADA server cabinet
│    ├── +CTRL_BLDG.CR.PLC_CAB    PLC cabinet (if combined)
│    └── +CTRL_BLDG.CR.DESK1      Operator desk
│
├── =RTU  Remote pump stations (telemetry)
│    ├── +PS_01.CP1          Pump station 01 RTU panel
│    ├── +PS_02.CP1          Pump station 02 RTU panel
│    └── +PS_03.CP1          Pump station 03 RTU panel
│
└── REPORTS
```

---

## Power Distribution & Substation

```
SUBSTATION_PROJECT
│
├── ADMIN
│    ├── Cover, TOC, revision
│    ├── Standards (IEC 62271, IEC 61850)
│    └── Site layout
│
├── OVERVIEW
│    ├── HV SLD (132kV / 66kV)
│    ├── MV SLD (11kV / 6.6kV)
│    ├── LV SLD (415V)
│    ├── DC SLD (110VDC)
│    ├── Protection and metering overview
│    └── IEC 61850 network architecture
│
├── =HV / +SUBST.YARD        HV yard / outdoor switchgear
│    ├── HV-001   Incomer gantry / surge arresters
│    ├── HV-002   Line 1 disconnector and earth switch
│    ├── HV-003   Line 2 disconnector and earth switch
│    └── HV-004   HV busbar connections
│
├── =MV / +SUBST.GIS_BLDG    MV switchgear
│    ├── +MV_SW1.INC_1       Incomer panel 1 (from TX1)
│    ├── +MV_SW1.INC_2       Incomer panel 2 (from TX2)
│    ├── +MV_SW1.BUS_SEC     Bus section
│    ├── +MV_SW1.FDR_1..n    Feeder panels
│    └── +MV_SW1.METER       Metering panel
│
├── =TX / +SUBST.TRANS_YARD  Transformers
│    ├── +TX1                Transformer 1
│    │    ├── TX1-001  HV cable termination
│    │    ├── TX1-002  LV busbar / busduct connection
│    │    ├── TX1-003  Protection relay wiring
│    │    ├── TX1-004  OLTC control (if fitted)
│    │    └── TX1-005  Cooling and auxiliaries
│    └── +TX2                Transformer 2
│
├── =LV / +SUBST.CTRL_BLDG   LV switchboard
│    ├── +MSB1.INC_A         Incomer A (from TX1)
│    ├── +MSB1.INC_B         Incomer B (from TX2)
│    ├── +MSB1.TIE           Bus coupler
│    ├── +MSB1.FDR_1..n      Feeder compartments
│    └── +MSB1.CTRL          Control and interlocking
│
├── =PROT / +SUBST.CTRL_BLDG.RELAY_RM   Protection and metering
│    ├── +PROT_PNL1.INC_A    Incomer A protection panel
│    ├── +PROT_PNL1.INC_B    Incomer B protection panel
│    ├── +PROT_PNL1.TX1_PROT TX1 differential protection
│    ├── +PROT_PNL1.TX2_PROT TX2 protection
│    ├── +PROT_PNL1.BUSBAR   Busbar protection
│    ├── +PROT_PNL1.METER    Energy and PQ metering
│    └── +PROT_PNL1.SCADA    RTU / SCADA panel
│
├── =DC / +SUBST.CTRL_BLDG.BATT_RM   DC battery and distribution
│    ├── +BATT_RM.BATT_BANK1 Battery bank 1
│    ├── +CHRG_CAB1          Charger cabinet
│    └── +DC_DB1             110VDC distribution board
│
├── =SCADA / +SUBST.CTRL_BLDG.RELAY_RM   SCADA / IEC 61850
│    ├── RTU-001  RTU hardware and communications
│    ├── RTU-002  IED interface (IEC 61850 GOOSE)
│    └── RTU-003  GPS time server
│
└── REPORTS
     ├── Terminal diagrams
     ├── DC cable list
     ├── CT/VT schedule
     └── Protection relay schedule
```

---

## Building Automation (BAS/BMS)

```
BMS_PROJECT
│
├── ADMIN
├── OVERVIEW
│    ├── System architecture
│    └── Network topology
│
├── =BMS / +BLDG.PLANT_RM.BMS_CAB   BMS system
│    ├── BMS-001  BMS server / supervisor
│    ├── BMS-002  System controller (DDC)
│    ├── BMS-003  Field controllers — level 1
│    ├── BMS-004  Field controllers — level 2
│    └── BMS-005  Communications network
│
├── =HVAC / +BLDG.PLANT_RM   HVAC plant
│    ├── +AHU_1               AHU 1
│    │    ├── AHU1-001  Supply fan motor (VFD)
│    │    ├── AHU1-002  Return fan motor (VFD)
│    │    ├── AHU1-003  Heating / cooling coil valves
│    │    ├── AHU1-004  Damper actuators
│    │    └── AHU1-005  Sensors (T, RH, CO2, DP)
│    ├── +CHILLER_1           Chiller 1
│    ├── +BOILER_1            Boiler 1
│    └── +PUMP_SET            Pump set
│
├── =HVAC / +BLDG.L1         Level 1 FCUs / VAV
│    ├── L1-001  FCU 1-01 wiring
│    ├── L1-002  FCU 1-02 wiring
│    └── L1-003  VAV zone controls
│
├── =HVAC / +BLDG.L2         Level 2 FCUs / VAV
├── =HVAC / +BLDG.ROOF       Roof plant
│    ├── +CT1                 Cooling tower 1
│    └── +ERV                 Energy recovery unit
│
├── =LIGHTING / +BLDG        Lighting control
│    ├── +BLDG.DALI_CAB       DALI controller cabinet
│    └── +BLDG.EMERG_CAB     Emergency lighting panel
│
├── =PWR / +BLDG.ELEC_RM     Electrical distribution
│    ├── +MSB                 Main switchboard
│    ├── +DB_L1               Level 1 DB
│    └── +DB_L2               Level 2 DB
│
└── REPORTS
```

---

## PLC / SCADA / DCS Project Structure

```
AUTOMATION_PROJECT
│
├── ADMIN
│    ├── Cover, TOC, revision
│    ├── I/O list / instrument index
│    ├── Network architecture
│    └── Software version record
│
├── OVERVIEW
│    ├── System architecture (Purdue model)
│    ├── Network topology diagram
│    ├── Power distribution overview
│    └── Safety architecture overview
│
├── =PWR / +CTRL_RM.UPS_CAB  Control room power
│    ├── PWR-001  UPS system
│    ├── PWR-002  UPS distribution board
│    └── PWR-003  Rack power distribution
│
├── =CTRL.PLC / +CTRL_RM.CAB1   Main PLC cabinet
│    ├── PLC-001  Power supply and 24VDC distribution
│    ├── PLC-002  CPU and rack A
│    ├── PLC-003  CPU and rack B (redundant)
│    ├── PLC-004  Digital inputs — rack A
│    ├── PLC-005  Digital inputs — rack B
│    ├── PLC-006  Digital outputs — rack A
│    ├── PLC-007  Analog inputs — rack A
│    ├── PLC-008  Analog outputs
│    ├── PLC-009  RTD / thermocouple modules
│    ├── PLC-010  Communications — PROFINET
│    ├── PLC-011  Communications — Modbus / serial
│    └── PLC-012  Auxiliary relay wiring
│
├── =CTRL.IO / +FLD_CAB_A1   Remote I/O cabinet A1
│    ├── RIO-A1-001  Power supply
│    ├── RIO-A1-002  Interface module
│    ├── RIO-A1-003  DI modules
│    ├── RIO-A1-004  DO modules
│    ├── RIO-A1-005  AI modules
│    └── RIO-A1-006  Field terminals
│
├── =CTRL.IO / +FLD_CAB_A2   Remote I/O cabinet A2
├── =CTRL.IO / +FLD_CAB_B1   Remote I/O cabinet B1
│
├── =SIS / +CTRL_RM.SIS_CAB  Safety system
│    ├── SIS-001  Safety PLC CPU A
│    ├── SIS-002  Safety PLC CPU B
│    ├── SIS-003  Safety I/O rack A
│    ├── SIS-004  Safety I/O rack B
│    ├── SIS-005  Safety power supply A/B
│    └── SIS-006  Safety terminals
│
├── =SCADA / +CTRL_RM.SCADA_CAB   SCADA system
│    ├── SCADA-001  Primary SCADA server
│    ├── SCADA-002  Standby SCADA server
│    ├── SCADA-003  OPC server
│    ├── SCADA-004  UPS for SCADA cabinet
│    └── SCADA-005  PDU and power management
│
├── =HIST / +CTRL_RM.HIST_CAB   Historian
│    ├── HIST-001   Primary historian server
│    └── HIST-002   Standby historian
│
├── =NETW.OT / +CTRL_RM.NET_CAB   OT network
│    ├── NET-001  Core OT switch
│    ├── NET-002  Distribution switches
│    ├── NET-003  OT/IT firewall
│    ├── NET-004  NTP time server
│    └── NET-005  Fibre distribution panel
│
├── =CTRL.HMI / +CTRL_RM.DESK1   Operator stations
│    ├── HMI-001  Workstation 1 (primary)
│    ├── HMI-002  Workstation 2
│    └── HMI-003  Engineering workstation
│
├── =MARSH / +MARSH_CAB_A   Marshalling cabinet A
│    ├── MARSH-A-001  DI marshalling terminals
│    ├── MARSH-A-002  DO marshalling terminals
│    ├── MARSH-A-003  AI marshalling terminals
│    ├── MARSH-A-004  HART barriers / isolators
│    └── MARSH-A-005  AO marshalling terminals
│
├── =INST / +FIELD   Field instruments
│    ├── FIELD-001  Flow instruments (FT-xxx)
│    ├── FIELD-002  Pressure instruments (PT-xxx)
│    ├── FIELD-003  Temperature instruments (TT-xxx)
│    ├── FIELD-004  Level instruments (LT-xxx)
│    └── FIELD-005  Analytical instruments (AT-xxx)
│
└── REPORTS
     ├── I/O schedule
     ├── Terminal diagrams
     ├── Cable list
     ├── Instrument index
     └── Network cable schedule
```

---

## Renewable Energy — Solar PV

```
SOLAR_FARM_PROJECT
│
├── ADMIN
│    ├── Cover, TOC, revision
│    └── Site layout
│
├── OVERVIEW
│    ├── Electrical SLD (string → combiner → inverter → grid)
│    ├── Protection coordination study
│    └── SCADA architecture
│
├── =PV / +SITE.FIELD_A     PV array — Field A
│    ├── +SITE.FIELD_A.SCB1  String combiner 1
│    ├── +SITE.FIELD_A.SCB2  String combiner 2
│    └── +SITE.FIELD_A.SCB3  String combiner 3
│
├── =INV / +SITE.INV_STN_1   Inverter station 1
│    ├── INV1-001  Inverter 1 DC input and AC output
│    ├── INV1-002  Inverter 2 DC input and AC output
│    ├── INV1-003  LV/MV step-up transformer T1
│    └── INV1-004  Station auxiliary power
│
├── =INV / +SITE.INV_STN_2   Inverter station 2
│
├── =BESS / +SITE.BESS       Battery energy storage
│    ├── BESS-001  Battery cabinets
│    ├── BESS-002  PCS cabinet
│    └── BESS-003  BMS and HVAC
│
├── =GRID / +SITE.MAIN_SUBST  Grid connection substation
│    ├── +MV_SW               MV switchgear
│    ├── +TX_EXPORT           Export transformer
│    └── +PROT_PNL            Protection panel
│
├── =SCADA / +SITE.CTRL_BLDG  Site monitoring and SCADA
│    ├── SCADA-001  SCADA server
│    ├── SCADA-002  Communications gateway
│    ├── SCADA-003  Network cabinet
│    └── SCADA-004  Meteorological station
│
└── REPORTS
```

---

## Renewable Energy — Wind

```
WIND_FARM_PROJECT
│
├── ADMIN
├── OVERVIEW
│    ├── Site SLD
│    ├── Array cable schematic
│    └── SCADA architecture
│
├── =WTG / +WTG_01           Turbine 01
│    ├── WTG01-001  Tower base MV switchgear
│    ├── WTG01-002  Nacelle power converter
│    ├── WTG01-003  Nacelle control cabinet
│    ├── WTG01-004  Pitch system (hub)
│    ├── WTG01-005  Yaw system
│    └── WTG01-006  Condition monitoring
│
├── =WTG / +WTG_02           Turbine 02
├── =WTG / +WTG_03           Turbine 03
│   (repeat per turbine)
│
├── =SUBST / +ONSHORE_SS     Onshore substation
│    ├── +ONSHORE_SS.HV_SW   HV switchgear
│    ├── +ONSHORE_SS.TX      Export transformer
│    └── +ONSHORE_SS.CTRL    Control building
│
├── =SCADA / +SITE           Wind farm SCADA
│    └── +SITE.CTRL_BLDG     Control building
│
└── REPORTS
```

---

## Marine & Shipbuilding

```
VESSEL_PROJECT
│
├── ADMIN
│    ├── Cover (vessel name, IMO number, flag state)
│    ├── Applicable rules (IACS, classification society)
│    └── General arrangement
│
├── OVERVIEW
│    ├── Single-line diagram (main switchboard to loads)
│    ├── Power management system overview
│    └── Fire & safety overview
│
├── =ELECT / +VESSEL.D1.ER   Engine room — main electrical
│    ├── +VESSEL.D1.ER.MAIN_SW   Main switchboard
│    │    ├── MSB-001  DG1 incomer
│    │    ├── MSB-002  DG2 incomer
│    │    ├── MSB-003  Shore power incomer
│    │    ├── MSB-004  Bus coupler
│    │    ├── MSB-005  Thruster feeder
│    │    ├── MSB-006  Distribution feeders
│    │    └── MSB-007  Power management system (PMS)
│    ├── +VESSEL.D1.ER.EMERG_SW  Emergency switchboard
│    └── +VESSEL.D1.ER.BATT_RM  Battery room
│
├── =PROPUL / +VESSEL.D1     Propulsion
│    ├── +VESSEL.D1.ER       Main engines
│    ├── +VESSEL.D2.PUMP_RM  Pump room
│    └── Thruster systems
│
├── =BRIDGE / +VESSEL.BRIDGE Navigation and bridge
│    ├── BRIDGE-001  Helm / navigation console
│    ├── BRIDGE-002  DP system
│    ├── BRIDGE-003  Comms (GMDSS, AIS)
│    └── BRIDGE-004  Fire and safety console
│
├── =FIRE / +VESSEL          Fire detection system
│    ├── +VESSEL.D1.ER       ER fire detection
│    ├── +VESSEL.D3.ACCOM    Accommodation detection
│    └── +VESSEL.BRIDGE      Bridge fire panel
│
├── =CARGO / +VESSEL         Cargo system
│
└── REPORTS
```

---

## Rail & Transportation

```
METRO_LINE_PROJECT
│
├── ADMIN
├── OVERVIEW
│    ├── Line SLD
│    ├── Traction power overview
│    └── SCADA / TIMS architecture
│
├── =TRAC / +LINE_1          Traction power system
│    ├── +TRAC_SS_1          Traction substation 1
│    │    ├── TSS1-001  Rectifier
│    │    ├── TSS1-002  DC switchgear
│    │    └── TSS1-003  Control panel
│    └── +TRAC_SS_2          Traction substation 2
│
├── =SIGNAL / +LINE_1        Signalling system
│    ├── +LINE_1.STN_A.SIGNAL  Station A signal equipment
│    └── +LINE_1.INTLK1      Interlocking room
│
├── =STN_A / +LINE_1.STN_A  Station A
│    ├── +LINE_1.STN_A.SUBST  Station substation
│    │    ├── STN_A-ELEC-001  MV switchgear
│    │    ├── STN_A-ELEC-002  LV distribution
│    │    └── STN_A-ELEC-003  UPS
│    ├── +LINE_1.STN_A.PLATFORM  Platform
│    │    ├── STN_A-PLAT-001  PSD control panel
│    │    ├── STN_A-PLAT-002  Lighting
│    │    └── STN_A-PLAT-003  PA and CCTV
│    └── +LINE_1.STN_A.CTRL_RM  Station control room
│         └── SCADA cabinet
│
├── =STN_B / +LINE_1.STN_B  Station B
│
├── =TUNNEL / +LINE_1.TUNNEL_A  Tunnel section A
│    ├── TUN-001  Ventilation fans
│    ├── TUN-002  Emergency lighting
│    └── TUN-003  Fire detection
│
└── REPORTS
```

---

## Data Centre & IT Infrastructure

```
DATA_CENTRE_PROJECT
│
├── ADMIN
│    ├── Cover (Tier rating, certification)
│    └── Standards (TIA-942, EN 50600)
│
├── OVERVIEW
│    ├── Power chain SLD (utility → ATS → UPS → PDU → rack)
│    ├── Cooling system overview
│    └── Network topology
│
├── =POWER / +DC.MDA         Main distribution area
│    ├── +DC.MDA.GENSET_RM   Generator room
│    │    ├── GEN-001  Generator 1
│    │    ├── GEN-002  Generator 2
│    │    └── GEN-003  ATS panels
│    ├── +DC.MDA.UPS_RM      UPS room
│    │    ├── UPS-001  UPS system A
│    │    ├── UPS-002  UPS system B
│    │    └── UPS-003  UPS distribution boards
│    └── +DC.MDA.MSB         Main switchboard
│
├── =COOL / +DC.COOL_PLANT   Cooling plant
│    ├── COOL-001  Chiller 1 — motor and control
│    ├── COOL-002  Chiller 2 — motor and control
│    ├── COOL-003  Cooling tower fans
│    └── COOL-004  Pump motors
│
├── =POWER / +DC.HALL_A      Data hall A
│    ├── +DC.HALL_A.HDA1     HDA — PDU area
│    │    ├── HALL_A-PDU-001  PDU A1
│    │    ├── HALL_A-PDU-002  PDU B1
│    │    └── HALL_A-PDU-003  PDU A2
│    └── +DC.HALL_A.CRAC1    CRAC units
│         └── CRAC-001  CRAC motor and controls
│
├── =NETW / +DC.NETWORK_RM   Network room
│    ├── NET-001  Core switches
│    ├── NET-002  Distribution switches
│    ├── NET-003  Firewalls
│    ├── NET-004  Patch panels
│    └── NET-005  Fibre distribution
│
├── =DCIM / +DC               DCIM system
│    ├── DCIM-001  Environmental monitoring
│    └── DCIM-002  Power monitoring
│
└── REPORTS
```

---

## Food & Beverage / Pharmaceutical

```
FOOD_BEVERAGE_PROJECT
│
├── ADMIN
│    ├── Cover, TOC, revision
│    └── Hygienic zone layout
│
├── OVERVIEW
│    ├── SLD
│    ├── Process flow diagram (PFD)
│    └── Control system architecture
│
├── =RECV / +SITE.RAW.CP1    Receiving (low care)
├── =PROC / +SITE.PROC.CP1   Processing area
│    ├── PROC-001  Prep and mixing motors
│    ├── PROC-002  Cooking system
│    ├── PROC-003  Cooling system
│    └── PROC-004  CIP system
│
├── =FILL / +SITE.HIGH_CARE.CP1  High care filling
│    ├── FILL-001  Filler motor and controls
│    ├── FILL-002  Sealing and labelling
│    └── FILL-003  Cleanroom instruments
│
├── =PACK / +SITE.PACK.CP1   Packaging
├── =REFRIG / +SITE.REFRIG.CP1  Refrigeration
│    ├── REFRIG-001  Compressor rack
│    ├── REFRIG-002  Evaporators
│    └── REFRIG-003  Cold store controls
│
├── =UTIL / +SITE.STEAM.CP1  Steam and utilities
├── =SUBST / +SITE.SUBST     Electrical substation
│
├── =CTRL / +SITE.CTRL_RM    Control room / MES
│    ├── +CTRL_RM.PLC_CAB    PLC cabinets
│    ├── +CTRL_RM.SCADA_CAB  SCADA server
│    └── +CTRL_RM.DESK1      Operator desk
│
└── REPORTS
     ├── Terminal diagrams
     ├── Instrument index
     ├── Motor schedule
     └── I/O list
```

---

## Mining & Heavy Industry

```
MINING_PROJECT
│
├── ADMIN
├── OVERVIEW
│    ├── Site electrical SLD
│    └── Process overview
│
├── =CRUSH / +MINE_SITE.CRUSH     Crushing plant
│    ├── +MINE_SITE.CRUSH.SUBST   Crushing substation
│    ├── +MINE_SITE.CRUSH.MCC1    Crushing MCC
│    │    ├── CRUSH-MCC1-001  Incomer
│    │    ├── CRUSH-MCC1-002  Primary crusher motor (VFD)
│    │    ├── CRUSH-MCC1-003  Secondary crusher motor
│    │    ├── CRUSH-MCC1-004  Screen motors
│    │    └── CRUSH-MCC1-005  Conveyor motors
│    └── +MINE_SITE.CRUSH.CP_PRI  Primary crusher control panel
│
├── =GRIND / +MINE_SITE.GRIND     Grinding circuit
│    ├── +MINE_SITE.GRIND.SUBST   Grinding substation
│    ├── +MINE_SITE.GRIND.MCC2    Grinding MCC (large drives)
│    └── +MINE_SITE.GRIND.CP1     Grinding control panel
│
├── =FLOAT / +MINE_SITE.FLOAT     Flotation circuit
├── =THICKEN / +MINE_SITE.TAILING  Tailings and thickening
│
├── =CONVEYOR / +MINE_SITE.CONVEY  Conveyor system
│    ├── +MINE_SITE.CONVEY.TS1    Transfer station 1
│    └── +MINE_SITE.CONVEY.TS2    Transfer station 2
│
├── =POWER / +MINE_SITE.MAIN_SUBST  Main substation
│    ├── +MINE_SITE.MAIN_SUBST.HV_SW  HV switchgear
│    ├── +MINE_SITE.MAIN_SUBST.TX1    Main transformer
│    └── +MINE_SITE.MAIN_SUBST.MV_SW  MV switchgear
│
├── =CTRL / +MINE_SITE.PROCESS_CTRL  Process control
│    ├── +MINE_SITE.PROCESS_CTRL.DCS_CAB1  DCS cabinet 1
│    └── +MINE_SITE.PROCESS_CTRL.DCS_CAB2  DCS cabinet 2
│
└── REPORTS
```

---

## Multi-Site / Multi-Unit Project Structure

> For projects spanning multiple physical sites, or multiple identical production units

### Multi-Site SCADA Project
```
MULTI_SITE_PROJECT
│
├── ADMIN (project-level)
├── OVERVIEW (project-level SLD, network map)
│
├── =SCADA / +HEAD_END        SCADA head end (master)
│    └── +HEAD_END.SCADA_CAB  SCADA server cabinet
│
├── =SITE_A                   Site A (e.g. Treatment plant A)
│    ├── +SITE_A.SUBST        Substation
│    ├── +SITE_A.MCC1         MCC 1
│    └── +SITE_A.RTU_PNL      RTU panel
│
├── =SITE_B                   Site B
│    ├── +SITE_B.SUBST
│    ├── +SITE_B.MCC1
│    └── +SITE_B.RTU_PNL
│
└── =SITE_C                   Site C
```

### Multi-Unit Identical Process (replication)
```
MULTI_UNIT_PROJECT
│
├── ADMIN
├── OVERVIEW
├── COMMON    Common / shared equipment
│    ├── +COMMON.SUBST     Main substation
│    ├── +COMMON.UTIL      Utilities
│    └── +COMMON.CTRL_RM   Central control room
│
├── =UNIT_1                Production unit 1
│    ├── +UNIT_1.MCC1
│    ├── +UNIT_1.CP1
│    └── +UNIT_1.FIELD
│
├── =UNIT_2                Production unit 2
│    ├── +UNIT_2.MCC1
│    ├── +UNIT_2.CP1
│    └── +UNIT_2.FIELD
│
└── =UNIT_3                Production unit 3
```

---

## Standard Cover Pages & Admin Pages

> Every project starts with these pages regardless of industry.
> Document type: EAA (Administrative), EAB (Lists), EAC (Explanatory)

### Mandatory Admin Pages
```
Page  Type        Content
001   EAA   Cover sheet / title page
      Contents: Project name, client name, project number,
                revision, date, approvals, company logo,
                applicable standards, voltage levels,
                degree of protection (IP rating),
                drawing set description

002   EAB   Table of contents (auto-generated from EPLAN)
      Contents: All page numbers, page descriptions,
                structure identifiers, page types

003   EAA   Revision history
      Contents: Rev number, date, description, drawn by,
                checked by, approved by

004   EAC   Symbol legend / graphical symbols
      Contents: All symbols used in the project with
                description and standard reference (IEC 60617)

005   EAC   Abbreviations list
      Contents: All abbreviations used (MCC, VFD, PLC, etc.)

006   EAC   Structure description
      Contents: Explanation of all = and + identifiers used,
                what each one represents

007   EAC   General notes
      Contents: Design basis, voltage levels, cable standards,
                protection philosophy, earthing philosophy

008   EAA   Applicable documents / standards list
      Contents: IEC standards, client specs, codes of practice
```

### Optional Admin Pages
```
009   EAA   Project contacts list
010   EAA   Drawing office notes (for internal use)
011   EAB   Document register / transmittal list
012   EAC   Area classification drawing (reference)
013   EAC   Site layout plan (reference)
014   EFA   Electrical SLD (high-level overview)
015   EFA   Control system architecture overview
016   EFA   Network topology diagram
017   EFA   Safety system overview
018   EFB   P&ID (or reference link to P&IDs)
```

---

## Page Type to Document Type Mapping

> When assigning IEC 61355 document types to EPLAN page types

| EPLAN Page Type | IEC 61355 Code | Description |
|----------------|---------------|-------------|
| Title page / cover sheet | EAA | Administrative documents |
| Table of contents | EAB | Lists regarding documents |
| Symbol overview / legend | EAC | Explanatory documents |
| Structure identifier overview | EAC | Explanatory documents |
| Revision overview | EBH | Documents regarding changes |
| Schematic multi-line | EFS | Circuitry documents |
| Schematic single-line | EFS | Circuitry documents |
| Overview (functional) | EFA | Functional overview documents |
| P&I diagram | EFB | Flow diagrams |
| Function descriptions | EFE | Function descriptions |
| PLC diagram | EFF | Function diagrams |
| Signal descriptions / I/O list | EFP | Signal descriptions |
| Setting value documents | EFQ | Setting value documents |
| Panel layout | ELU | In/on-equipment location documents |
| Terminal diagram | EMA | Connection documents |
| Terminal-connection diagram | EMA | Connection documents |
| Cable diagram | EMB | Cabling documents |
| Connection list | EMA | Connection documents |
| Cable overview | EMB | Cabling documents |
| Parts list | EPB | Parts lists |
| Summarised parts list | EPA | Material lists |
| Device tag list | EPB | Parts lists |
| Terminal-strip overview | EMA | Connection documents |
| PLC card overview | EFF | Function diagrams |
| PLC address overview | EFP | Signal descriptions |
| Manufacturer / supplier list | EPD | Product lists |
| Mounting list | ETL | Arrangement documents |
| Plot frame documentation | EAA | Administrative documents |

---

## Numbering Strategies

### Strategy 1 — Flat Sequential (small projects, <50 pages)
```
0001  Cover sheet
0002  Table of contents
0003  Symbol legend
0010  SLD overview
0020  MCC1 — incomer
0021  MCC1 — feeder M01
0022  MCC1 — feeder M02
0030  CP1 — PLC power
0031  CP1 — PLC CPU and I/O
0099  Terminal diagram
0100  Cable list
0101  Parts list
```

### Strategy 2 — Block-by-Structure (recommended for medium projects)
```
Admin block:     0001 - 0099
=PWR block:      1000 - 1099
=CTRL block:     2000 - 2099
=SAFE block:     3000 - 3099
=DRIVE block:    4000 - 4099
=MOTOR block:    5000 - 5099
=FIELD block:    6000 - 6099
Reports:         9000 - 9999
```

### Strategy 3 — Panel-Coded (panel building standard)
```
ADMIN:    0001 - 0099
MSB1:     1001 - 1099
MCC1:     2001 - 2099
MCC2:     3001 - 3099
DB1:      4001 - 4049
DB2:      4050 - 4099
CP1:      5001 - 5099
JB pages: 6001 - 6099
Reports:  9001 - 9099
```

### Strategy 4 — Hierarchical Dot (large plant / DCS)
```
1       System overview
1.1     Electrical SLD
1.2     Control architecture
2       Unit 10 — Raw material intake
2.1     MCC1 incomer
2.2     M-1001 DOL starter
2.3     M-1002 DOL starter
3       Unit 20 — Pre-treatment
3.1     MCC2 incomer
...
9       Reports
9.1     Terminal diagrams
9.2     Cable list
```

### Page Counter Reset Options
```
Option A — Continuous: pages never reset, always unique
  Pros: No ambiguity ever
  Cons: Large gaps between sections

Option B — Reset per structure node
  Each = or + block starts from 001
  Pros: Neat numbers within each section
  Cons: Same page number appears in different sections
  Requires: Full identifier prefix to be unique (e.g. MCC1/001, MCC2/001)
```

---

## Common Mistakes

| ❌ Wrong | ✅ Correct | Reason |
|----------|------------|--------|
| No admin / cover pages | Always start with cover, TOC, legend | Client standard — missing these fails document review |
| All pages at project root (no structure) | Group into `=` or `+` nodes | Flat structure → all reports merged → unusable |
| Inconsistent capitalisation: `=ctrl`, `=CTRL`, `=Ctrl` | Pick one — use `=CTRL` | Three different nodes in the tree |
| Spaces in structure names: `=MOTOR CTRL` | `=MOTOR_CTRL` | Spaces break EPLAN identifiers |
| One structure node for everything: `=SYSTEM` | Break into functional sub-nodes | Too broad → all reports merge into one |
| Mixing `=` and `+` roles | Function goes in `=`, location goes in `+` | Mixing them breaks report filtering |
| Reports scattered through project | Group all reports in one block at end | Makes issuing, printing, and reviewing much cleaner |
| No page description on schematic pages | Always fill in the page description | Page description appears in TOC and on drawing title block |
| Starting page numbering at 1 without a gap | Start admin at 1, first section at 100 or 1000 | Leaves room to insert pages without renumbering |
| Different engineers using different structure names for same panel | Agree structure at project kick-off | `+MCC1`, `+MCC_1`, `+MCC-1` are three different locations |
| Putting overview pages inside a structure node | Put overviews at project root or admin group | Overviews should be accessible without navigating into a subsystem |
| Single structure depth for large projects | Use two or three levels for large projects | `=U30+AREA_A.MCC1` is navigable; `=ALL` is not |

---

## Expert Tips

### 1. Plan the structure before creating page 1
> Sketch the full tree on paper first. Define all `=` and `+` identifiers, agree the numbering strategy, and set up the structure in EPLAN project settings before any drawing starts. Restructuring mid-project is expensive.

### 2. Match the project structure to the client's asset hierarchy
> If the client uses SAP Plant Maintenance with locations like `PLANT-AREA10-MCC1`, your EPLAN `+` structure should match exactly: `+PLANT.AREA10.MCC1`. This makes commissioning, handover, and maintenance spares ordering seamless.

### 3. Admin pages always come first — no exceptions
> Cover sheet, table of contents, revision history, symbol legend, and structure description are the first things a client engineer, auditor, or maintenance person looks for. Put them at the very top of the tree, unnested.

### 4. Keep report pages separate and at the end
> Terminal diagrams, cable lists, BOMs, and device tag lists should live in their own block at the end of the project. Never mix report pages with schematic pages — it makes document control a nightmare.

### 5. Use descriptive page descriptions — not just page numbers
> `MCC1 — M03 Star-delta starter — Agitator AG-101` is infinitely better than `Page 0043`. The page description appears in the table of contents, the drawing title block, and in report headers.

### 6. Give field device pages their own `+FIELD` or `+JB_XX` location
> Instruments, sensors, and actuators that are not inside an enclosure need a location. `+FIELD` or `+JB_P01` keeps their connections out of the panel terminal diagrams and in the correct field wiring documents.

### 7. Sub-systems get sub-nodes — don't flatten everything
> A paint workstation (like HK1 in the sample) should have its own P&ID sub-pages, its own enclosure nodes, and its own sub-functions. EPLAN supports this naturally — use it. Navigating into `HK1 → PFB → P&ID` is much cleaner than hunting through 200 flat pages.

### 8. Use the same page structure for repeated units
> If you have 6 identical motor starters, create one template structure and replicate it. `MCC1.M01`, `MCC1.M02`, ... `MCC1.M06` with identical internal page structure means changes to one propagate cleanly, and reports sort logically.

### 9. Overview and architecture pages belong at the top of each major section
> Each major `=` function node should start with an overview or SLD page for that system. Engineers navigating to `=PWR` should immediately see the power SLD before diving into individual panel pages.

### 10. Document your structure in page EAC (Structure description)
> Create a dedicated page in your admin section that lists every `=` and `+` identifier used, with a plain-English description of what each one means. This page is often the first thing a new engineer reads and saves hours of confusion on large projects.

---

*Based on IEC 61355 | IEC 81346 | IEC 60617 | ISA-5.1 | TIA-942 | IEC 62271 | IEC 61439*
*Expert conventions compiled from machine building, panel building, process, power, automation, marine, rail, and data centre engineering*
