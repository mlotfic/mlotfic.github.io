# EPLAN P8 Document Types Reference

## Overview

Document Types (`&` symbol) in EPLAN P8 categorize different kinds of electrical documentation. They help organize and distinguish between schematics, diagrams, layouts, and specialized technical documents within a single electrical project.

---

## Standard EPLAN Document Types

### Schematic Documents

#### `SCH` - Schematic Diagram
**Description:** Main electrical circuit schematic showing connections, components, and signal flow
**Standards:** IEC 60617, IEEE 315
**Used For:**
- Circuit logic and operation
- Component interconnections
- Control circuit design
**Example Page:** `PUMP_01+MCC_01&SCH`

---

#### `WIRING` - Wiring Diagram
**Description:** Detailed point-to-point wiring connections with wire numbers and routing
**Standards:** IEC 61346, IEEE 1346
**Used For:**
- Installation guidance
- Wire identification and routing
- Troubleshooting connections
**Example Page:** `MOTOR_CTRL+PANEL_A&WIRING`
**Includes:** Wire gauges, terminal numbers, color codes

---

#### `LAYOUT` - Component Layout / Panel Layout
**Description:** Physical arrangement of components within a cabinet, panel, or enclosure
**Standards:** IEC 60445, DIN 40719
**Used For:**
- Physical placement of devices
- Space planning
- Cabinet construction
**Example Page:** `MCC_01+CABINET&LAYOUT`
**Includes:** Dimensions, mounting locations, thermal considerations

---

#### `DETAIL` - Detail Drawing / Detail Sheet
**Description:** Enlarged or zoomed view of a specific circuit section with additional information
**Standards:** ISO 128, IEC 60617
**Used For:**
- Complex circuit explanations
- Interconnect specifications
- Specialized subsystem documentation
**Example Page:** `HEATER_CTRL+PANEL_B&DETAIL`

---

### Terminal and Connection Documents

#### `TERMINAL` - Terminal Assignment / Terminal Sheet
**Description:** Lists all terminals with their assigned functions and connections
**Standards:** IEC 61346, IEC 60445
**Used For:**
- Terminal identification
- Cross-reference documentation
- Installation verification
**Example Page:** `PUMP_01+MCC_01&TERMINAL`
**Includes:** Terminal numbers, wire colors, signal names, voltage levels

---

#### `CONNECTOR` - Connector Assignment
**Description:** Documentation of connectors and plug connections
**Standards:** IEC 61076 series
**Used For:**
- Multi-pin connector specifications
- Plug compatibility
- Mating information
**Example Page:** `CONTROL_SYSTEM+PANEL&CONNECTOR`

---

### Electrical Characteristic Documents

#### `POWER` - Power Distribution / Power Flow
**Description:** Shows power distribution paths and electrical loads
**Standards:** IEC 60050, IEEE 100
**Used For:**
- Load calculation
- Voltage drop analysis
- Power supply routing
**Example Page:** `MAIN_DISTRIBUTION+SUBSTATION&POWER`

---

#### `GROUND` - Grounding / Earthing Diagram
**Description:** Grounding and bonding connections throughout the system
**Standards:** IEC 61936, IEEE 1100
**Used For:**
- Lightning protection
- Safety grounding
- EMC compliance
**Example Page:** `SAFETY_SYSTEM+BUILDING&GROUND`

---

#### `SHIELDING` - Shielding / EMC
**Description:** Electromagnetic shielding and interference mitigation
**Standards:** IEC 61000, IEEE C95.1
**Used For:**
- Cable shielding specifications
- EMC design
- Noise reduction
**Example Page:** `SIGNAL_PROCESSING+PANEL&SHIELDING`

---

### Control and Safety Documents

#### `LOGIC` - Logic Diagram / Function Chart
**Description:** Boolean logic and function relationships (AND, OR, NOT gates)
**Standards:** IEC 60617-2, IEC 61131-5
**Used For:**
- Control logic visualization
- Boolean expressions
- Sequential operations
**Example Page:** `EMERGENCY_STOP+SAFETY_RELAY&LOGIC`

---

#### `STATE_DIAGRAM` - State Diagram / Sequence Diagram
**Description:** State transitions and operational sequences
**Standards:** IEC 61131-3, UML
**Used For:**
- Sequential control
- Mode transitions
- Timing relationships
**Example Page:** `PRODUCTION_LINE+PLC&STATE_DIAGRAM`

---

#### `BLOCK_DIAGRAM` - Block Diagram / Functional Block
**Description:** High-level system blocks and interactions
**Standards:** IEC 61131-2, IEEE 1028
**Used For:**
- System architecture overview
- Functional decomposition
- System integration
**Example Page:** `CONTROL_SYSTEM+LEVEL_1&BLOCK_DIAGRAM`

---

### Specialized Documents

#### `INSTALLATION` - Installation Drawing
**Description:** Step-by-step installation instructions and procedures
**Standards:** ISO 20171, IEC 62304
**Used For:**
- On-site assembly
- Equipment mounting
- Commissioning procedures
**Example Page:** `COMPLETE_SYSTEM+SITE&INSTALLATION`

---

#### `TESTING` - Test Procedure / Test Protocol
**Description:** Functional testing and verification procedures
**Standards:** IEC 61160, IEEE 1232
**Used For:**
- Factory acceptance tests (FAT)
- Site acceptance tests (SAT)
- Validation procedures
**Example Page:** `MOTOR_SYSTEM+COMMISSIONING&TESTING`

---

#### `CALIBRATION` - Calibration Sheet
**Description:** Instrument calibration settings and procedures
**Standards:** IEC 61566, NIST standards
**Used For:**
- Sensor calibration
- Measurement verification
- Accuracy documentation
**Example Page:** `SENSOR_ARRAY+PANEL&CALIBRATION`

---

#### `MANUAL` - Manual / Operation Guide
**Description:** User instructions for operation and maintenance
**Standards:** IEC 62079, ISO 20607
**Used For:**
- User documentation
- Safety warnings
- Maintenance procedures
**Example Page:** `SYSTEM_CONTROL+OPERATOR&MANUAL`

---

#### `DATASHEET` - Component Datasheet / Specification
**Description:** Technical specifications and performance data
**Standards:** Product-specific, ISO 11010
**Used For:**
- Component reference
- Performance characteristics
- Selection criteria
**Example Page:** `COMPONENT_REFERENCE+LIBRARY&DATASHEET`

---

### Documentation and Control

#### `BILL_OF_MATERIALS` / `BOM` - Parts List
**Description:** Complete list of components with quantities and specifications
**Standards:** IEC 61346, ISO 13584
**Used For:**
- Procurement
- Inventory management
- Cost estimation
**Example Page:** `PROJECT_CONTROL+MAIN&BOM`

---

#### `CABLE_LIST` - Cable Schedule
**Description:** All cables with lengths, types, and routing information
**Standards:** IEC 60445, DIN 40719
**Used For:**
- Cable procurement
- Routing planning
- Installation verification
**Example Page:** `WIRING_CONTROL+SUBSTATION&CABLE_LIST`

---

#### `REVISION` - Revision Drawing / Change Notice
**Description:** Mark changes and revisions from previous versions
**Standards:** ISO 1219-1, IEC 61346
**Used For:**
- Version control
- Change documentation
- Obsolescence notices
**Example Page:** `SYSTEM_UPDATE+REVISION_2&REVISION`

---

#### `INSTRUCTION` - Instruction Sheet / Technical Note
**Description:** Special instructions or technical notes
**Standards:** Custom project standards
**Used For:**
- Design notes
- Special warnings
- Technical clarifications
**Example Page:** `SPECIAL_CIRCUIT+NOTES&INSTRUCTION`

---

### Advanced/Specialized Documents

#### `LADDER_DIAGRAM` - Ladder Diagram / Relay Logic
**Description:** Relay logic represented in ladder format
**Standards:** IEC 61131-5, IEEE 991
**Used For:**
- PLC programming visualization
- Relay circuit logic
- Legacy system documentation
**Example Page:** `LOGIC_CONTROL+PLC&LADDER_DIAGRAM`

---

#### `P&ID` - Piping & Instrumentation Diagram
**Description:** Fluid system with instrumentation and controls
**Standards:** ISA 5.1, ANSI Y32.11
**Used For:**
- Process automation
- Instrumentation integration
- System interactions
**Example Page:** `PROCESS_CONTROL+PLANT&P&ID`

---

#### `SIGNAL_FLOW` - Signal Flow Diagram
**Description:** Signal paths and data flow through the system
**Standards:** IEC 61131, ISO 9545
**Used For:**
- Data routing
- Communication paths
- Signal processing
**Example Page:** `DATA_ACQUISITION+NETWORK&SIGNAL_FLOW`

---

#### `TIMING` - Timing Diagram
**Description:** Time-based signal relationships and synchronization
**Standards:** IEC 61131-5, IEEE 1028
**Used For:**
- Signal timing analysis
- Synchronization requirements
- Operational sequencing
**Example Page:** `MOTOR_CONTROL+PLC&TIMING`

---

#### `SCHEMATIC_SYMBOL` - Symbol Definition / Custom Symbol
**Description:** Custom electrical symbols and their definitions
**Standards:** IEC 60617, IEEE 315
**Used For:**
- Library creation
- Project-specific symbols
- Symbol standardization
**Example Page:** `SYMBOL_LIBRARY+STANDARDS&SCHEMATIC_SYMBOL`

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

### Complete Project Package
```
MAIN_SYSTEM + LEVEL_1 & BLOCK_DIAGRAM        (Overview)
SUBSYSTEM_A + PANEL_A & SCH                  (Design)
SUBSYSTEM_A + PANEL_A & WIRING               (Installation)
SUBSYSTEM_A + PANEL_A & BOM                  (Parts list)
SUBSYSTEM_A + PANEL_A & CABLE_LIST           (Cables)
SUBSYSTEM_A + PANEL_A & TESTING              (FAT procedure)
```

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

## Naming Best Practices

### Clear Document Type Abbreviations
```
✓ GOOD:  PUMP_01+MCC_01&SCH
         PUMP_01+MCC_01&WIRING
         PUMP_01+MCC_01&DETAIL

✗ POOR:  PUMP_01+MCC_01&SCHEMATIC
         PUMP_01+MCC_01&WIRE_DIA
         PUMP_01+MCC_01&DTL
```

### Consistent Naming Across Project
```
Use standard abbreviations:
SCH, WIRING, LAYOUT, TERMINAL, DETAIL
NOT: SCHEMATIC, WIRE_DIAGRAM, PANEL_LAYOUT, etc.
```

### Avoid Ambiguity
```
✓ CLEAR:   PUMP_01+MCC_01&SCH
           PUMP_01+MCC_01&WIRING

✗ VAGUE:   PUMP_01+MCC_01&MAIN
           PUMP_01+MCC_01&DOCUMENT
```

---

## JSON Schema for Document Types

```json
{
  "documentTypes": [
    {
      "symbol": "&",
      "abbreviation": "SCH",
      "fullName": "Schematic Diagram",
      "category": "Schematic Documents",
      "description": "Main electrical circuit schematic",
      "standards": ["IEC 60617", "IEEE 315"],
      "usedFor": [
        "Circuit logic and operation",
        "Component interconnections"
      ],
      "includes": [
        "Component symbols",
        "Wire connections",
        "Signal paths"
      ]
    },
    {
      "symbol": "&",
      "abbreviation": "WIRING",
      "fullName": "Wiring Diagram",
      "category": "Schematic Documents",
      "description": "Detailed point-to-point wiring",
      "standards": ["IEC 61346", "IEEE 1346"],
      "usedFor": [
        "Installation guidance",
        "Wire identification"
      ],
      "includes": [
        "Wire numbers",
        "Terminal assignments",
        "Color codes"
      ]
    }
  ]
}
```

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

---

## Tips for Implementation

1. **Define Your Standard:** Establish which document types your project will use
2. **Document Selection Criteria:** Create guidelines for when to use each type
3. **Template Creation:** Build templates for frequently used document types
4. **Team Training:** Ensure all team members understand the document type scheme
5. **Consistency Check:** Periodically audit projects for proper document type usage
6. **Version Control:** Track document type changes as the project evolves

---

## Common Mistakes to Avoid

❌ Using inconsistent abbreviations (SCHEM vs SCH)  
❌ Creating too many custom document types  
❌ Not distinguishing between document types (same info, different pages)  
❌ Forgetting to update document type labels during revisions  
❌ Using vague or overlapping document type names  
❌ Not training team members on document type standards  

---

## Summary

EPLAN P8 Document Types provide a standardized way to categorize electrical documentation. Proper selection ensures:
- Clear organization and navigation
- Consistent team communication
- Compliance with industry standards
- Easy maintenance and updates
- Professional project documentation

Choose document types that best fit your project structure and maintain consistency throughout the electrical documentation lifecycle.
