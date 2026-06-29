---
layout: post
cover_color: #000000

keywords: EPLAN P8, Project Structure, Forms, Reports, Document Types, Electrical Design, Project Documentation, Standard Forms, Report Generation, EPLAN P8 Reference

title: EPLAN P8 Document Types List

description: >-
  This guide provides a comprehensive reference to the standard document types used in EPLAN Electric P8 projects, including descriptions, examples, standards compliance, and best practices for selection and implementation.
  
date: 2024-03-10 10:00:00 +0800
author: Mahmoud Lotfi
file_name: 2024-03-10-eplan-document-types-list-1.md
categories: [EPLAN, Documentation]
tags: [EPLAN, document types]
pin: False
math: true
mermaid: true
comments: true
toc: true
render_with_liquid: false

image:
  path: /assets/img/posts/eplan.jpg
  alt: EPLAN P8 Document Types List
  lqip: data:image/webp;base64,UklGRjoAAABXRUJQVlA4IC4AAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
---

# EPLAN P8 Document Types List `&`

> **Software:** EPLAN Electric P8 / EPLAN Platform
> **Topic:** **All page types** — Automatic pages, Document type, Function designation, Interactive pages, Location designation
> **Level:** Beginner to Advanced

---

## Overview

Document Types (`&` symbol) in EPLAN P8 categorize different kinds of electrical documentation. They help organize and distinguish between schematics, diagrams, layouts, and specialized technical documents within a single electrical project.

---

## Post Covering:

- ✅ **25+ Standard Document Types** – From basic schematics to advanced P&ID diagrams  
- ✅ **Detailed Descriptions** – Purpose, standards, and use cases for each type  
- ✅ **Real Examples** – How document types appear in actual page names  
- ✅ **Common Combinations** – Typical document sets for industrial systems  
- ✅ **Selection Guide** – Choose by design, installation, operation, or system complexity  
- ✅ **Standards Compliance** – IEC, IEEE, and ISO references  
- ✅ **JSON Schema** – Structured data format for automation  
- ✅ **Quick Reference Table** – Fast lookup of all document types  

**Main Categories Covered:**

- Schematic Documents (SCH, WIRING, LAYOUT, DETAIL)
- Terminal & Connection (TERMINAL, CONNECTOR)
- Electrical Characteristics (POWER, GROUND, SHIELDING)
- Control & Safety (LOGIC, STATE_DIAGRAM, BLOCK_DIAGRAM)
- Specialized (INSTALLATION, TESTING, CALIBRATION, MANUAL)
- Documentation (BOM, CABLE_LIST, REVISION, INSTRUCTION)
- Advanced (LADDER_DIAGRAM, P&ID, SIGNAL_FLOW, TIMING)

---

## Standard EPLAN Document Types Overview

# EPLAN Page Type Codes Reference

## Core Schematic Pages

| Code       | Full Name              | Description                                                        |
|------------|------------------------|--------------------------------------------------------------------|
| **SCH**    | Schematic Diagram      | Core circuit design, signal flow, component interconnections       |
| **WIRING** | Wiring Diagram         | Detailed point-to-point connections, wire numbering, cable routing |
| **LAYOUT** | Layout / Panel Layout  | Physical arrangement of components within cabinets and enclosures  |
| **DETAIL** | Detail Drawing         | Enlarged or zoomed view of specific circuit sections               |

## Terminal & Connection Diagrams

| Code | Full Name | Description |
|------|-----------|-------------|
| **TERMINAL** | Terminal Diagram / Sheet | Lists all terminals with their assigned functions and connections    |
| **CONNECTOR** | Connector Diagram | Documentation of connectors and plug connections |

## Electrical Characteristic Pages

| Code | Full Name | Description |
|------|-----------|-------------|
| **POWER** | Power Distribution | Shows power distribution paths and electrical loads |
| **GROUND** | Grounding Diagram | Grounding and bonding connections throughout the system |
| **SHIELDING** | Shielding Diagram | Electromagnetic shielding and interference mitigation |

## Control & Safety Diagrams

| Code | Full Name | Description |
|------|-----------|-------------|
| **LOGIC** | Logic Diagram | Boolean logic, control sequences, state logic |
| **STATE_DIAGRAM** | State Diagram | System state transitions and control logic |
| **BLOCK_DIAGRAM** | Block Diagram | High-level system blocks and signal flow |

## Specialized Technical Documents

| Code | Full Name | Description |
|------|-----------|-------------|
| **INSTALLATION** | Installation Drawing | Physical installation guidance and component placement |
| **TESTING** | Test Procedure / Sheet | Step-by-step testing instructions and procedures |
| **CALIBRATION** | Calibration Sheet | Instrument calibration specifications and procedures |
| **MANUAL** | Manual / Operating Instructions | User manuals and operating instructions |
| **DATASHEET** | Datasheet | Technical datasheets for components |

## Documentation & Reporting Pages

| Code | Full Name | Description |
|------|-----------|-------------|
| **BOM** | Bill of Materials / Parts List | Complete list of all parts used in the project |
| **CABLE_LIST** | Cable List | Comprehensive cable schedule and specifications |
| **REVISION** | Revision History | Document revision history and change tracking |
| **INSTRUCTION** | Instructions / Notes | General project instructions and notes |

## Advanced & Specialized Page Types

| Code | Full Name | Description |
|------|-----------|-------------|
| **LADDER_DIAGRAM** | Ladder Diagram | PLC ladder logic representation |
| **P&ID** | Piping & Instrumentation Diagram | Process and instrumentation diagrams |
| **SIGNAL_FLOW** | Signal Flow Diagram | Signal flow through the entire system |
| **TIMING** | Timing Diagram | Signal timing and sequencing information |
| **SCHEMATIC_SYMBOL** | Schematic Symbol Sheet | Catalog of schematic symbols used in the project |

---

## Standard EPLAN Document Types in Detail

### Schematic Documents

#### 01. `SCH` - Schematic Diagram

**Description:** Main electrical circuit schematic showing connections, components, and signal flow
**Standards:** IEC 60617, IEEE 315
**Used For:**
- Circuit logic and operation
- Component interconnections
- Control circuit design
**Example Page:** `PUMP_01+MCC_01&SCH`

---

#### 02. `WIRING` - Wiring Diagram

**Description:** Detailed point-to-point wiring connections with wire numbers and routing
**Standards:** IEC 61346, IEEE 1346
**Used For:**
- Installation guidance
- Wire identification and routing
- Troubleshooting connections
**Example Page:** `MOTOR_CTRL+PANEL_A&WIRING`
**Includes:** Wire gauges, terminal numbers, color codes

---

#### 03. `LAYOUT` - Component Layout / Panel Layout

**Description:** Physical arrangement of components within a cabinet, panel, or enclosure
**Standards:** IEC 60445, DIN 40719
**Used For:**
- Physical placement of devices
- Space planning
- Cabinet construction
**Example Page:** `MCC_01+CABINET&LAYOUT`
**Includes:** Dimensions, mounting locations, thermal considerations

---

#### 04. `DETAIL` - Detail Drawing / Detail Sheet

**Description:** Enlarged or zoomed view of a specific circuit section with additional information
**Standards:** ISO 128, IEC 60617
**Used For:**
- Complex circuit explanations
- Interconnect specifications
- Specialized subsystem documentation
**Example Page:** `HEATER_CTRL+PANEL_B&DETAIL`

---

### Terminal and Connection Documents

#### 05. `TERMINAL` - Terminal Assignment / Terminal Sheet

**Description:** Lists all terminals with their assigned functions and connections
**Standards:** IEC 61346, IEC 60445
**Used For:**
- Terminal identification
- Cross-reference documentation
- Installation verification
**Example Page:** `PUMP_01+MCC_01&TERMINAL`
**Includes:** Terminal numbers, wire colors, signal names, voltage levels

---

#### 06. `CONNECTOR` - Connector Assignment

**Description:** Documentation of connectors and plug connections
**Standards:** IEC 61076 series
**Used For:**
- Multi-pin connector specifications
- Plug compatibility
- Mating information
**Example Page:** `CONTROL_SYSTEM+PANEL&CONNECTOR`

---

### Electrical Characteristic Documents

#### 07. `POWER` - Power Distribution / Power Flow

**Description:** Shows power distribution paths and electrical loads
**Standards:** IEC 60050, IEEE 100
**Used For:**
- Load calculation
- Voltage drop analysis
- Power supply routing
**Example Page:** `MAIN_DISTRIBUTION+SUBSTATION&POWER`

---

#### 08. `GROUND` - Grounding / Earthing Diagram

**Description:** Grounding and bonding connections throughout the system
**Standards:** IEC 61936, IEEE 1100
**Used For:**
- Lightning protection
- Safety grounding
- EMC compliance
**Example Page:** `SAFETY_SYSTEM+BUILDING&GROUND`

---

#### 09. `SHIELDING` - Shielding / EMC

**Description:** Electromagnetic shielding and interference mitigation
**Standards:** IEC 61000, IEEE C95.1
**Used For:**
- Cable shielding specifications
- EMC design
- Noise reduction
**Example Page:** `SIGNAL_PROCESSING+PANEL&SHIELDING`

---

### Control and Safety Documents

#### 10. `LOGIC` - Logic Diagram / Function Chart

**Description:** Boolean logic and function relationships (AND, OR, NOT gates)
**Standards:** IEC 60617-2, IEC 61131-5
**Used For:**
- Control logic visualization
- Boolean expressions
- Sequential operations
**Example Page:** `EMERGENCY_STOP+SAFETY_RELAY&LOGIC`

---

#### 11. `STATE_DIAGRAM` - State Diagram / Sequence Diagram

**Description:** State transitions and operational sequences
**Standards:** IEC 61131-3, UML
**Used For:**
- Sequential control
- Mode transitions
- Timing relationships
**Example Page:** `PRODUCTION_LINE+PLC&STATE_DIAGRAM`

---

#### 12. `BLOCK_DIAGRAM` - Block Diagram / Functional Block

**Description:** High-level system blocks and interactions
**Standards:** IEC 61131-2, IEEE 1028
**Used For:**
- System architecture overview
- Functional decomposition
- System integration
**Example Page:** `CONTROL_SYSTEM+LEVEL_1&BLOCK_DIAGRAM`

---

### Specialized Documents

#### 13. `INSTALLATION` - Installation Drawing

**Description:** Step-by-step installation instructions and procedures
**Standards:** ISO 20171, IEC 62304
**Used For:**
- On-site assembly
- Equipment mounting
- Commissioning procedures
**Example Page:** `COMPLETE_SYSTEM+SITE&INSTALLATION`

---

#### 14. `TESTING` - Test Procedure / Test Protocol

**Description:** Functional testing and verification procedures
**Standards:** IEC 61160, IEEE 1232
**Used For:**
- Factory acceptance tests (FAT)
- Site acceptance tests (SAT)
- Validation procedures
**Example Page:** `MOTOR_SYSTEM+COMMISSIONING&TESTING`

---

#### 15. `CALIBRATION` - Calibration Sheet

**Description:** Instrument calibration settings and procedures
**Standards:** IEC 61566, NIST standards
**Used For:**
- Sensor calibration
- Measurement verification
- Accuracy documentation
**Example Page:** `SENSOR_ARRAY+PANEL&CALIBRATION`

---

#### 16. `MANUAL` - Manual / Operation Guide

**Description:** User instructions for operation and maintenance
**Standards:** IEC 62079, ISO 20607
**Used For:**
- User documentation
- Safety warnings
- Maintenance procedures
**Example Page:** `SYSTEM_CONTROL+OPERATOR&MANUAL`

---

#### 17. `DATASHEET` - Component Datasheet / Specification

**Description:** Technical specifications and performance data
**Standards:** Product-specific, ISO 11010
**Used For:**
- Component reference
- Performance characteristics
- Selection criteria
**Example Page:** `COMPONENT_REFERENCE+LIBRARY&DATASHEET`

---

### Documentation and Control

#### 18. `BILL_OF_MATERIALS` / `BOM` - Parts List

**Description:** Complete list of components with quantities and specifications
**Standards:** IEC 61346, ISO 13584
**Used For:**
- Procurement
- Inventory management
- Cost estimation
**Example Page:** `PROJECT_CONTROL+MAIN&BOM`

---

#### 19. `CABLE_LIST` - Cable Schedule

**Description:** All cables with lengths, types, and routing information
**Standards:** IEC 60445, DIN 40719
**Used For:**
- Cable procurement
- Routing planning
- Installation verification
**Example Page:** `WIRING_CONTROL+SUBSTATION&CABLE_LIST`

---

#### 20. `REVISION` - Revision Drawing / Change Notice

**Description:** Mark changes and revisions from previous versions
**Standards:** ISO 1219-1, IEC 61346
**Used For:**
- Version control
- Change documentation
- Obsolescence notices
**Example Page:** `SYSTEM_UPDATE+REVISION_2&REVISION`

---

#### 21. `INSTRUCTION` - Instruction Sheet / Technical Note

**Description:** Special instructions or technical notes
**Standards:** Custom project standards
**Used For:**
- Design notes
- Special warnings
- Technical clarifications
**Example Page:** `SPECIAL_CIRCUIT+NOTES&INSTRUCTION`

---

### Advanced/Specialized Documents

#### 22. `LADDER_DIAGRAM` - Ladder Diagram / Relay Logic

**Description:** Relay logic represented in ladder format
**Standards:** IEC 61131-5, IEEE 991
**Used For:**
- PLC programming visualization
- Relay circuit logic
- Legacy system documentation
**Example Page:** `LOGIC_CONTROL+PLC&LADDER_DIAGRAM`

---

#### 23. `P&ID` - Piping & Instrumentation Diagram

**Description:** Fluid system with instrumentation and controls
**Standards:** ISA 5.1, ANSI Y32.11
**Used For:**
- Process automation
- Instrumentation integration
- System interactions
**Example Page:** `PROCESS_CONTROL+PLANT&P&ID`

---

#### 24. `SIGNAL_FLOW` - Signal Flow Diagram

**Description:** Signal paths and data flow through the system
**Standards:** IEC 61131, ISO 9545
**Used For:**
- Data routing
- Communication paths
- Signal processing
**Example Page:** `DATA_ACQUISITION+NETWORK&SIGNAL_FLOW`

---

#### 25. `TIMING` - Timing Diagram

**Description:** Time-based signal relationships and synchronization
**Standards:** IEC 61131-5, IEEE 1028
**Used For:**
- Signal timing analysis
- Synchronization requirements
- Operational sequencing
**Example Page:** `MOTOR_CONTROL+PLC&TIMING`

---

#### 26. `SCHEMATIC_SYMBOL` - Symbol Definition / Custom Symbol

**Description:** Custom electrical symbols and their definitions
**Standards:** IEC 60617, IEEE 315
**Used For:**
- Library creation
- Project-specific symbols
- Symbol standardization
**Example Page:** `SYMBOL_LIBRARY+STANDARDS&SCHEMATIC_SYMBOL`

---

## Document Type Selection Guide

### Choose By Purpose:

**For Design & Understanding:**
- SCH (schematic)
- LOGIC (logic)
- BLOCK_DIAGRAM (system architecture)

**For Installation:**
- WIRING (wire connections)
- LAYOUT (physical placement)
- INSTALLATION (step-by-step)
- CABLE_LIST (routing)

**For Operation & Maintenance:**
- MANUAL (user guide)
- TESTING (procedures)
- CALIBRATION (verification)
- INSTRUCTION (special notes)

**For Reference & Control:**
- TERMINAL (terminal assignments)
- BOM (parts list)
- DATASHEET (specifications)
- REVISION (change control)

**For Complex Systems:**
- STATE_DIAGRAM (sequencing)
- SIGNAL_FLOW (data paths)
- TIMING (synchronization)
- P&ID (process integration)

---

## Regulatory & Standards Compliance

| Document Type | IEC Standard  | IEEE Standard | ISO Standard |
|---------------|---------------|---------------|--------------|
| SCH           | IEC 60617     | IEEE 315      | ISO 1219-1   |
| WIRING        | IEC 61346     | IEEE 1346     | ISO 9545     |
| LAYOUT        | IEC 60445     | IEEE 1135     | ISO 128      |
| P&ID          | ISA 5.1       | IEEE 1028     | ISO 9545     |
| LOGIC         | IEC 61131-5   | IEEE 91       | ISO 1219-2   |
| TESTING       | IEC 61160     | IEEE 1232     | ISO 16100    |
| INSTALLATION  | IEC 62304     | IEEE 1175     | ISO 20171    |

---

## Quick Reference Table

| Abbreviation  | Full Name             | Category        | Primary Use         | Eplan Page Type                     |
|---------------|-----------------------|-----------------|---------------------| ------------------------------------|
| SCH           | Schematic Diagram     | Circuit         | Design              | Schematic multi-line / single-line  |
| WIRING        | Wiring Diagram        | Circuit         | Installation        | Schematic multi-line / single-line  |
| LAYOUT        | Component Layout      | Physical        | Installation        | Panel layout                        |
| DETAIL        | Detail Drawing        | Circuit         | Clarification       | Detail drawing                      |
| TERMINAL      | Terminal Assignment   | Reference       | Verification        | Terminal diagram                    |
| CONNECTOR     | Connector Assignment  | Reference       | Compatibility       | Connector diagram                   |
| LOGIC         | Logic Diagram         | Control         | Design              | Logic diagram                       |
| BOM           | Bill of Materials     | Control         | Procurement         | Bill of materials                   |
| CABLE_LIST    | Cable Schedule        | Control         | Installation        | Cable schedule                      |
| INSTALLATION  | Installation Guide    | Instructions    | Assembly            | Installation guide                  |
| TESTING       | Test Procedure        | Instructions    | Verification        | Test procedure                      |
| MANUAL        | Operation Guide       | Instructions    | Operation           | Operation guide                     |
| BLOCK_DIAGRAM | Block Diagram         | Overview        | Architecture        | Block/overview diagram              |
| P&ID          | P&ID Diagram          | Process         | Integration         | P&I diagram/ Fluid power schematic  |



---
## inteactive pages (I)

| Page Type | Abbreviation|Description |
|-----------|-------------|-------------|
| External document | EXT | Reference or link to external documentation or files |
| Fluid power schematic | FLUID | Schematic diagram for hydraulic or pneumatic systems |
| Function overview (fluid power) | FUNCTION_FLUID | Overview of functions within fluid power systems |
| Graphic | GRAPHIC | Page for graphical illustrations or visual elements |
| Model view | MODEL | 3D or model-based view of system components |
| Overview | OVERVIEW | General overview page summarizing system or project |
| P&I diagram | P&I | Process and instrumentation diagram for process systems |
| Panel layout | PANEL_LAYOUT | Layout drawing of electrical panels and components |
| Pre-planning | PRE_PLANNING | Page for early-stage planning and design documentation |
| Schematic multi-line | SCH | Detailed multi-line electrical schematic for complex circuits |
| Schematic single-line | SCH_SL | Simplified single-line schematic for power distribution |
| Topology | TOPOLOGY | Topology diagram showing network or system connections |

---

## Automatic pages (A)




{
  "PageTypes": [
    { "name": "Cable assignment diagram", "description": "Diagram showing cable assignments to devices or terminals" },
    { "name": "Terminal diagram", "description": "Diagram showing terminal connections" },
    { "name": "Terminal-connection diagram", "description": "Detailed terminal-to-device connection diagram" },
    { "name": "Cable diagram", "description": "Detailed representation of cable connections" },
    { "name": "Terminal line-up diagram", "description": "Diagram showing terminal arrangement" },
    { "name": "Device tag list", "description": "List of device identifiers used in the project" },
    { "name": "Table of contents", "description": "Index of project documentation" },
    { "name": "Terminal-strip overview", "description": "Overview of terminal strips used" },
    { "name": "PLC card overview", "description": "Overview of PLC cards/modules" },
    { "name": "Title page / cover sheet", "description": "Front page of the project documentation" },
    { "name": "Symbol overview", "description": "Overview of symbols used in diagrams" },
    { "name": "Connection list", "description": "Tabular list of all electrical connections" },
    { "name": "Potential overview", "description": "Overview of electrical potentials" },
    { "name": "Cable overview", "description": "Summary of all cables used in the project" },
    { "name": "Parts list", "description": "Comprehensive list of project parts" },
    { "name": "Plug overview", "description": "Overview of plug types and usage" },
    { "name": "PLC diagram", "description": "Detailed PLC wiring and logic diagram" },
    { "name": "Device-connection diagram", "description": "Diagram showing device interconnections" },
    { "name": "Cable-connection diagram", "description": "Illustrates specific cable-to-device connections" },
    { "name": "Pin-connection diagram", "description": "Diagram showing pin-level connections" },
    { "name": "Plug diagram", "description": "Diagram of plug connections" },
    { "name": "Enclosure legend", "description": "Legend for enclosure components" },
    { "name": "Summarized parts list", "description": "Condensed list of project parts" },
    { "name": "Structure identifier overview", "description": "Overview of structure identifiers" },
    { "name": "Forms documentation", "description": "Documentation forms for project reporting" },
    { "name": "Plot frame documentation", "description": "Documentation of plot frames used" },
    { "name": "Revision overview", "description": "Overview of project revisions" },
    { "name": "Project options overview", "description": "Overview of project options and settings" },
    { "name": "Placeholder object overview", "description": "Overview of placeholder objects in design" },
    { "name": "Manufacturer / supplier list", "description": "List of manufacturers and suppliers" },
    { "name": "Model view", "description": "Graphical model view of system components" },
    { "name": "Mounting list", "description": "List of mounting components and positions" },
    { "name": "PCT loop legend", "description": "Legend for PCT loops" },
    { "name": "Topology", "description": "General topology documentation" },
    { "name": "Topology: Topology path list", "description": "List of topology paths" },
    { "name": "Topology: Routing path diagram", "description": "Diagram of routing paths" },
    { "name": "Topology: Routed cables / connections", "description": "Topology of routed cables and connections" },
    { "name": "P&I diagram: Piping overview", "description": "Overview of piping in process diagrams" },
    { "name": "Pre-planning: Structure segment overview", "description": "Overview of structure segments in pre-planning" },
    { "name": "Pre-planning: Structure segment plan", "description": "Plan of structure segments in pre-planning" },
    { "name": "Pre-planning: Planning object overview", "description": "Overview of planning objects" },
    { "name": "Pre-planning: Planning object plan", "description": "Plan of planning objects" },
    { "name": "Pre-planning: Segment template overview", "description": "Overview of segment templates" },
    { "name": "Pre-planning: Segment template plan", "description": "Plan of segment templates" },
    { "name": "Pre-planning", "description": "General pre-planning documentation" },
    { "name": "Assembly/Module overview", "description": "Overview of assemblies or modules in the project" },
    { "name": "Distributed device list", "description": "List of devices distributed across locations" },
    { "name": "Conduit / line plan", "description": "Plan for conduits and line routing" },
    { "name": "Cut-out legend", "description": "Legend for cut-outs in panels or enclosures" },
    { "name": "PLC address overview", "description": "Overview of PLC addresses used" },
    { "name": "Pre-planning: Pipe class overview", "description": "Overview of pipe classes in pre-planning" },
    { "name": "Pre-planning: Substance overview", "description": "Overview of substances in pre-planning" },
    { "name": "Function overview (fluid power)", "description": "Overview of functions in fluid power systems" }
  ]
}
