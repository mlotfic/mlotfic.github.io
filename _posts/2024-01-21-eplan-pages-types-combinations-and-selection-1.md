---

title: "EPLAN P8 Common Document Type Combinations and Selection Guide"

description: >-
  This guide provides practical examples of common document type combinations in EPLAN P8 for different industrial applications, helping you select the right document types for your projects.
date: 2024-03-10 10:00:00 +0800
author: Mahmoud Lotfi
file_name: 2024-03-10-eplan-document-types-combinations-and-selection-guide-1.md
categories: [EPLAN, Documentation, Reference]
tags: [Eplan, document types, reference]
pin: False
math: true
mermaid: true
comments: true
toc: true
render_with_liquid: false

image:
  path: /assets/img/posts/eplan.jpg
  alt: EPLAN P8 Common Document Type Combinations and Selection Guide
  lqip: data:image/webp;base64,UklGRjoAAABXRUJQVlA4IC4AAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
---

# EPLAN P8 Common Document Type Combinations and Selection Guide

## Industrial Control System
```
PUMP_01 + MCC_01 & SCH              (Main circuit schematic)
PUMP_01 + MCC_01 & WIRING           (Detailed wiring)
PUMP_01 + MCC_01 & LAYOUT           (Cabinet layout)
PUMP_01 + MCC_01 & TERMINAL         (Terminal assignments)
PUMP_01 + MCC_01 & TESTING          (Test procedures)
```

## Safety System
```
EMERGENCY_STOP + SAFETY_PANEL & SCH          (Schematic)
EMERGENCY_STOP + SAFETY_PANEL & LOGIC        (Logic diagram)
EMERGENCY_STOP + SAFETY_PANEL & DETAIL       (Detailed circuit)
EMERGENCY_STOP + SAFETY_PANEL & INSTALLATION (Installation guide)
```

## Complete Project Package
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

## Tips for Implementation

1. **Define Your Standard:** Establish which document types your project will use
2. **Document Selection Criteria:** Create guidelines for when to use each type
3. **Template Creation:** Build templates for frequently used document types
4. **Consistency Check:** Periodically audit projects for proper document type usage
5. **Version Control:** Track document type changes as the project evolves

---

## Common Mistakes to Avoid

❌ Using inconsistent abbreviations (SCHEM vs SCH)  
❌ Creating too many custom document types  
❌ Not distinguishing between document types (same info, different pages)  
❌ Forgetting to update document type labels during revisions  
❌ Using vague or overlapping document type names  
❌ Not training team members on document type standards  


