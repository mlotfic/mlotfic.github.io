---
title: EPLAN Document Types Reference
date: 2024-03-16 14:20:00 +0000
categories: [EPLAN, Documentation, Reference]
tags: [document-types, electrical, standardization]
---

## Overview

Document Types (`&` symbol) in EPLAN P8 categorize different kinds of electrical documentation. They help organize and distinguish between schematics, diagrams, layouts, and specialized technical documents within a single electrical project.

## Standard Document Type Categories

### Schematic Documents

#### `SCH` - Schematic Diagram
- **Description:** Main electrical circuit schematic showing connections, components, and signal flow
- **Standards:** IEC 60617, IEEE 315
- **Used For:** Circuit logic, component interconnections, control circuit design
- **Example:** `PUMP_01+MCC_01&SCH`

#### `WIRING` - Wiring Diagram
- **Description:** Detailed point-to-point wiring connections with wire numbers and routing
- **Standards:** IEC 61346, IEEE 1346
- **Used For:** Installation guidance, wire identification, troubleshooting
- **Example:** `MOTOR_CTRL+PANEL_A&WIRING`

#### `LAYOUT` - Component Layout
- **Description:** Physical arrangement of components within a cabinet, panel, or enclosure
- **Standards:** IEC 60445, DIN 40719
- **Used For:** Physical placement, space planning, cabinet construction
- **Example:** `MCC_01+CABINET&LAYOUT`

#### `DETAIL` - Detail Drawing
- **Description:** Enlarged or zoomed view of a specific circuit section
- **Standards:** ISO 128, IEC 60617
- **Used For:** Complex circuit explanations, interconnect specifications
- **Example:** `HEATER_CTRL+PANEL_B&DETAIL`

---

### Terminal and Connection Documents

#### `TERMINAL` - Terminal Assignment
- **Description:** Lists all terminals with their assigned functions and connections
- **Standards:** IEC 61346, IEC 60445
- **Includes:** Terminal numbers, wire colors, signal names, voltage levels
- **Example:** `PUMP_01+MCC_01&TERMINAL`

#### `CONNECTOR` - Connector Assignment
- **Description:** Documentation of connectors and plug connections
- **Standards:** IEC 61076 series
- **Used For:** Multi-pin connector specifications, plug compatibility
- **Example:** `CONTROL_SYSTEM+PANEL&CONNECTOR`

---

### Electrical Characteristic Documents

#### `POWER` - Power Distribution
- **Description:** Shows power distribution paths and electrical loads
- **Standards:** IEC 60050, IEEE 100
- **Used For:** Load calculation, voltage drop analysis, power supply routing
- **Example:** `MAIN_DISTRIBUTION+SUBSTATION&POWER`

#### `GROUND` - Grounding / Earthing Diagram
- **Description:** Grounding and bonding connections throughout the system
- **Standards:** IEC 61936, IEEE 1100
- **Used For:** Lightning protection, safety grounding, EMC compliance
- **Example:** `SAFETY_SYSTEM+BUILDING&GROUND`

#### `SHIELDING` - Shielding / EMC
- **Description:** Electromagnetic shielding and interference mitigation
- **Standards:** IEC 61000, IEEE C95.1
- **Used For:** Cable shielding specifications, EMC design, noise reduction
- **Example:** `SIGNAL_PROCESSING+PANEL&SHIELDING`

---

### Control and Safety Documents

#### `LOGIC` - Logic Diagram
- **Description:** Boolean logic and function relationships (AND, OR, NOT gates)
- **Standards:** IEC 60617-2, IEC 61131-5
- **Used For:** Control logic visualization, Boolean expressions
- **Example:** `EMERGENCY_STOP+SAFETY_RELAY&LOGIC`

#### `STATE_DIAGRAM` - State Diagram
- **Description:** State transitions and operational sequences
- **Standards:** IEC 61131-3, UML
- **Used For:** Sequential control, mode transitions, timing relationships
- **Example:** `PRODUCTION_LINE+PLC&STATE_DIAGRAM`

#### `BLOCK_DIAGRAM` - Block Diagram
- **Description:** High-level system blocks and interactions
- **Standards:** IEC 61131-2, IEEE 1028
- **Used For:** System architecture overview, functional decomposition
- **Example:** `CONTROL_SYSTEM+LEVEL_1&BLOCK_DIAGRAM`

---

### Specialized Documents

#### `INSTALLATION` - Installation Drawing
- **Description:** Step-by-step installation instructions and procedures
- **Standards:** ISO 20171, IEC 62304
- **Used For:** On-site assembly, equipment mounting, commissioning
- **Example:** `COMPLETE_SYSTEM+SITE&INSTALLATION`

#### `TESTING` - Test Procedure
- **Description:** Functional testing and verification procedures
- **Standards:** IEC 61160, IEEE 1232
- **Used For:** Factory acceptance tests (FAT), site acceptance tests (SAT)
- **Example:** `MOTOR_SYSTEM+COMMISSIONING&TESTING`

#### `BOM` - Bill of Materials
- **Description:** Complete list of components with quantities and specifications
- **Standards:** IEC 61346, ISO 13584
- **Used For:** Procurement, inventory management, cost estimation
- **Example:** `PROJECT_CONTROL+MAIN&BOM`

#### `CABLE_LIST` - Cable Schedule
- **Description:** All cables with lengths, types, and routing information
- **Standards:** IEC 60445, DIN 40719
- **Used For:** Cable procurement, routing planning, installation verification
- **Example:** `WIRING_CONTROL+SUBSTATION&CABLE_LIST`

---

## Document Type Selection Guide

### For Design & Understanding:
- **SCH** (schematic)
- **LOGIC** (logic)
- **BLOCK_DIAGRAM** (system architecture)

### For Installation:
- **WIRING** (wire connections)
- **LAYOUT** (physical placement)
- **INSTALLATION** (step-by-step)
- **CABLE_LIST** (routing)

### For Operation & Maintenance:
- **MANUAL** (user guide)
- **TESTING** (procedures)
- **CALIBRATION** (verification)
- **INSTRUCTION** (special notes)

### For Reference & Control:
- **TERMINAL** (terminal assignments)
- **BOM** (parts list)
- **DATASHEET** (specifications)
- **REVISION** (change control)

---

## Common Document Type Combinations

### Industrial Control System
```
PUMP_01 + MCC_01 & SCH              (Main circuit schematic)
PUMP_01 + MCC_01 & WIRING           (Detailed wiring)
PUMP_01 + MCC_01 & LAYOUT           (Cabinet layout)
PUMP_01 + MCC_01 & TERMINAL         (Terminal assignments)
PUMP_01 + MCC_01 & TESTING          (Test procedures)
```

### Safety System
```
EMERGENCY_STOP + SAFETY_PANEL & SCH          (Schematic)
EMERGENCY_STOP + SAFETY_PANEL & LOGIC        (Logic diagram)
EMERGENCY_STOP + SAFETY_PANEL & DETAIL       (Detailed circuit)
EMERGENCY_STOP + SAFETY_PANEL & INSTALLATION (Installation guide)
```

---

## Quick Reference Table

| Abbreviation | Full Name | Category | Primary Use |
|------------|-----------|----------|------------|
| SCH | Schematic Diagram | Circuit | Design |
| WIRING | Wiring Diagram | Circuit | Installation |
| LAYOUT | Component Layout | Physical | Installation |
| DETAIL | Detail Drawing | Circuit | Clarification |
| TERMINAL | Terminal Assignment | Reference | Verification |
| LOGIC | Logic Diagram | Control | Design |
| BOM | Bill of Materials | Control | Procurement |
| CABLE_LIST | Cable Schedule | Control | Installation |
| INSTALLATION | Installation Guide | Instructions | Assembly |
| TESTING | Test Procedure | Instructions | Verification |

---

## Best Practices

### ✓ Clear Document Type Abbreviations
```
GOOD:   PUMP_01+MCC_01&SCH
        PUMP_01+MCC_01&WIRING
        PUMP_01+MCC_01&DETAIL

POOR:   PUMP_01+MCC_01&SCHEMATIC
        PUMP_01+MCC_01&WIRE_DIA
        PUMP_01+MCC_01&DTL
```

### ✓ Consistent Naming Across Project
Use standard abbreviations consistently:
- SCH, WIRING, LAYOUT, TERMINAL, DETAIL
- NOT: SCHEMATIC, WIRE_DIAGRAM, PANEL_LAYOUT, etc.

### ✓ Avoid Ambiguity
```
CLEAR:   PUMP_01+MCC_01&SCH
         PUMP_01+MCC_01&WIRING

VAGUE:   PUMP_01+MCC_01&MAIN
         PUMP_01+MCC_01&DOCUMENT
```

---

## Regulatory & Standards Compliance

| Document Type | IEC Standard | IEEE Standard |
|--------------|-------------|---------------|
| SCH | IEC 60617 | IEEE 315 |
| WIRING | IEC 61346 | IEEE 1346 |
| LAYOUT | IEC 60445 | IEEE 1135 |
| LOGIC | IEC 61131-5 | IEEE 91 |
| TESTING | IEC 61160 | IEEE 1232 |

---

## Tips for Implementation

1. **Define Your Standard** - Establish which document types your project will use
2. **Document Selection Criteria** - Create guidelines for when to use each type
3. **Template Creation** - Build templates for frequently used document types
4. **Team Training** - Ensure all team members understand the scheme
5. **Consistency Check** - Periodically audit projects for proper usage

---

## Common Mistakes to Avoid

❌ Using inconsistent abbreviations (SCHEM vs SCH)  
❌ Creating too many custom document types  
❌ Not distinguishing between document types  
❌ Forgetting to update labels during revisions  
❌ Not training team members on standards  

---

## Summary

EPLAN P8 Document Types provide a standardized way to categorize electrical documentation. Proper selection ensures:

✅ Clear organization and navigation  
✅ Consistent team communication  
✅ Compliance with industry standards  
✅ Easy maintenance and updates  
✅ Professional project documentation  

---

**Related Articles:**
- [Page Structure Guide](/posts/page-structure-guide/)
- [Function Designation Basics](/posts/function-designation/)
- [Location Designation Guide](/posts/location-designation/)
