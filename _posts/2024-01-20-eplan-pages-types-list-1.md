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
tags: [Eplan, document types]
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

### Schematic Documents
1. Schematic Diagrams `SCH`
2. Wiring Diagrams `WIRING`
3. Layouts `LAYOUT`
4. Details `DETAIL`

### Terminal and Connection Documents
5. Terminal Diagrams `TERMINAL`
6. Connector Diagrams `CONNECTOR`

### Electrical Characteristic Documents
7. Power Diagrams `POWER`
8. Grounding Diagrams `GROUND`
9. Shielding Diagrams `SHIELDING`

### Control and Safety Documents
10. Logic Diagrams `LOGIC`
11. State Diagrams `STATE_DIAGRAM`
12. Block Diagrams `BLOCK_DIAGRAM`

### Specialized Documents
13. Installation Drawings `INSTALLATION`
14. Test Procedures `TESTING`
15. Calibration Sheets `CALIBRATION`
16. Manuals `MANUAL`
17. Datasheets `DATASHEET`
18. Bill of Materials `BOM`
19. Cable Lists `CABLE_LIST`
20. Revision History `REVISION`
21. Instructions `INSTRUCTION`

### Advanced/Specialized Documents
22. Ladder Diagrams `LADDER_DIAGRAM`
23. Piping & Instrumentation Diagrams `P&ID`
24. Signal Flow Diagrams `SIGNAL_FLOW`
25. Timing Diagrams `TIMING`
26. Schematic Symbols `SCHEMATIC_SYMBOL`

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

| Document Type | IEC Standard | IEEE Standard | ISO Standard |
|--------------|-------------|---------------|-------------|
| SCH | IEC 60617 | IEEE 315 | ISO 1219-1 |
| WIRING | IEC 61346 | IEEE 1346 | ISO 9545 |
| LAYOUT | IEC 60445 | IEEE 1135 | ISO 128 |
| P&ID | ISA 5.1 | IEEE 1028 | ISO 9545 |
| LOGIC | IEC 61131-5 | IEEE 91 | ISO 1219-2 |
| TESTING | IEC 61160 | IEEE 1232 | ISO 16100 |
| INSTALLATION | IEC 62304 | IEEE 1175 | ISO 20171 |

---

## Quick Reference Table

| Abbreviation | Full Name | Category | Primary Use |
|------------|-----------|----------|------------|
| SCH | Schematic Diagram | Circuit | Design |
| WIRING | Wiring Diagram | Circuit | Installation |
| LAYOUT | Component Layout | Physical | Installation |
| DETAIL | Detail Drawing | Circuit | Clarification |
| TERMINAL | Terminal Assignment | Reference | Verification |
| CONNECTOR | Connector Assignment | Reference | Compatibility |
| LOGIC | Logic Diagram | Control | Design |
| BOM | Bill of Materials | Control | Procurement |
| CABLE_LIST | Cable Schedule | Control | Installation |
| INSTALLATION | Installation Guide | Instructions | Assembly |
| TESTING | Test Procedure | Instructions | Verification |
| MANUAL | Operation Guide | Instructions | Operation |
| BLOCK_DIAGRAM | Block Diagram | Overview | Architecture |
| P&ID | P&ID Diagram | Process | Integration |

