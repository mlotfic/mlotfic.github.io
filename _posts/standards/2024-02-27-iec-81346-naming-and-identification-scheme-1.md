---
layout: post
cover_color: #000000

keywords: EPLAN P8, Project Structure, Page Structure, Page Labeling, Page Identification, Page Naming, Document Structure, Electrical Design, Project Documentation, EPLAN P8 Reference

title: "EPLAN P8 Page Naming and Identification Scheme"

description: >-
  The **Page Structure** dialog in EPLAN P8 defines the naming and identification scheme for electrical schematic pages. It creates a hierarchical template that dictates how pages are organized, labeled, and referenced throughout your electrical project documentation.
  based on IEC 81346 and IEC 61355 standards

date: 2024-03-10 10:00:00 +0800
author: Mahmoud Lotfi
file_name: 2024-03-10-eplan-pages-labeling-1.md
categories: [EPLAN, Page, labeling]
tags: [EPLAN, pages, labeling]
pin: False
math: true
mermaid: true
comments: true
toc: true
render_with_liquid: false

image:
  path: /assets/img/posts/eplan.jpg
  alt: EPLAN Pages labeling based on IEC 81346 and IEC 61355 standards
  lqip: data:image/webp;base64,UklGRjoAAABXRUJQVlA4IC4AAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
---

# EPLAN P8 Page naming and identification scheme

> **Topic:** The **Page Structure** dialog in EPLAN P8 defines the naming and identification scheme for electrical schematic pages. It creates a hierarchical template that dictates how pages are organized, labeled, and referenced throughout your electrical project documentation.
> Based on IEC 81346 and IEC 61355 standards
> **Level:** Beginner to Advanced

---

## The Structure Components Explained

| Component                  | Symbol | Purpose                                             | Status |
|----------------------------|--------|-----------------------------------------------------|--------|
| **Functional assignment**  | `==`   | Groups related circuits/functions together          |        |
| **Function designation**   | `=`    | Names individual circuit functions                  |        |
| **Installation site**      | `++`   | Specifies physical location of equipment            |        |
| **Location designation**   | `+`    | Identifies the cabinet/panel location               |        |
| **Document type**          | `&`    | Categorizes page type (schematic, layout, etc.)     |        |
| **User-defined structure** | `#`    | Custom fields for project-specific data             |        |

---

## Overview

The **Page Structure** dialog in EPLAN P8 defines the naming and identification scheme for electrical schematic pages. It creates a hierarchical template that dictates how pages are organized, labeled, and referenced throughout your electrical project documentation.

---

## Page Structure Components

### 1. Functional Assignment (`==`)

**Purpose:** Groups related electrical circuits or functions together at a high level

**Example:**

- `POWER DISTRIBUTION`
- `MOTOR CONTROL`
- `SAFETY SYSTEMS`

**Use Case:** When you want to organize pages by major system categories

---

### 2. Function Designation (`=`)

**Purpose:** Names individual circuit functions or subsystems

**Example:**

- `PUMP_01` (pump circuit)
- `HEATER_CTRL` (heater control)
- `EMERGENCY_STOP` (E-stop circuit)

**Use Case:** Each unique function gets its own designation for clear identification

---

### 3. Installation Site (`++`)

**Purpose:** Specifies the physical location where equipment is installed

**Example:**

- `WAREHOUSE_A`
- `PRODUCTION_LINE_2`
- `EXTERNAL_SUBSTATION`

**Use Case:** When the same circuit design is replicated across multiple physical locations

---

### 4. Location Designation (`+`)

**Purpose:** Identifies the specific cabinet, panel, or enclosure where electrical components reside

**Example:**

- `MCC_01` (Motor Control Center 1)
- `PANEL_A` (Control Panel A)
- `BREAKER_BOX_MAIN` (Main breaker box)

**Use Case:** Essential for linking documentation to physical equipment locations

---

### 5. Document Type (`&`)

**Purpose:** Categorizes the type of electrical page/document

**Example:**

- `SCH` (Schematic)
- `WIRING` (Wiring diagram)
- `LAYOUT` (Component layout)
- `DETAIL` (Detail sheet)

**Use Case:** Distinguishes between different documentation types for the same system

---

### 6. User-Defined Structure (`#`)

**Purpose:** Custom fields for project-specific organizational needs

**Example:**

- `REV_A` (Revision)
- `VENDOR_SIEMENS` (Vendor identification)
- `COST_CENTER_123` (Accounting reference)

**Use Case:** Flexible custom metadata when standard fields don't fit

---

## Real-World Examples

### Example 1: Industrial Control System

**Current Scheme:** Function designation, Location designation, Document type

**Page Names Generated:**

```cs
PUMP_01 + MCC_01 & SCH
PUMP_01 + MCC_01 & WIRING
MOTOR_CTRL + PANEL_A & SCH
MOTOR_CTRL + PANEL_A & DETAIL
HEATER_CTRL + PANEL_B & SCH
```

**Breakdown:**

- `PUMP_01` = function (identifying)
- `MCC_01` = location/cabinet (identifying)
- `SCH` = schematic document type (identifying)
- `+` and `&` = connectors showing structure

---

### Example 2: Manufacturing Plant with Multiple Sites

**Enhanced Scheme (if enabled):**

```cs
WAREHOUSE_A ++ PUMP_01 + MCC_01 & SCH
WAREHOUSE_B ++ PUMP_01 + MCC_01 & SCH
WAREHOUSE_A ++ HEATER + PANEL_A & WIRING
```

**Breakdown:**

- `WAREHOUSE_A` = installation site (physical location)
- `PUMP_01` = function
- `MCC_01` = cabinet
- `SCH` = document type

---

### Example 3: Safety System Documentation

```cs
EMERGENCY_STOP + SAFETY_RELAY & SCH
EMERGENCY_STOP + SAFETY_RELAY & DETAIL
EMERGENCY_STOP + CONTROL_PANEL & WIRING
```

**Benefit:** All E-stop pages are grouped together and easily searchable by function

---

## Best Practices

### 1. **Naming Conventions**

```cs
FUNCTION:     Use descriptive, uppercase names
              ✓ PUMP_01, MOTOR_CTRL, HEATER_BLOCK_1
              ✗ P, M, HB (too vague)

LOCATION:     Use cabinet/panel identifiers
              ✓ MCC_01, PANEL_CTRL, BREAKER_MAIN
              ✗ ROOM_A, FLOOR_2 (too vague)

DOCUMENT:     Use standardized abbreviations
              ✓ SCH, WIRING, LAYOUT, DETAIL
              ✗ DIAG, DRAWING, DOC (inconsistent)
```

### 2. **Consistency**

- Establish and document your naming standard before starting
- Use the same delimiters throughout (+, =, &)
- Avoid special characters that complicate searching

### 3. **Scalability**

- Design structure to accommodate future expansion
- Consider multi-site/multi-panel scenarios early
- Leave room for additional functions

### 4. **Documentation**

```cs
Example Project Structure:
├── Function Designations (PUMP_xx, MOTOR_xx, CTRL_xx)
├── Locations (MCC_01-03, PANEL_A-C, BREAKER_MAIN)
└── Document Types (SCH, WIRING, LAYOUT, DETAIL)
```

---

## Real-World Examples

### Example 1: Industrial Control System

**Current Scheme:** Function designation, Location designation, Document type

**Page Names Generated:**
```
PUMP_01 + MCC_01 & SCH
PUMP_01 + MCC_01 & WIRING
MOTOR_CTRL + PANEL_A & SCH
MOTOR_CTRL + PANEL_A & DETAIL
HEATER_CTRL + PANEL_B & SCH
```

**Breakdown:**
- `PUMP_01` = function (identifying)
- `MCC_01` = location/cabinet (identifying)
- `SCH` = schematic document type (identifying)
- `+` and `&` = connectors showing structure

---

### Example 2: Manufacturing Plant with Multiple Sites

**Enhanced Scheme (if enabled):**
```
WAREHOUSE_A ++ PUMP_01 + MCC_01 & SCH
WAREHOUSE_B ++ PUMP_01 + MCC_01 & SCH
WAREHOUSE_A ++ HEATER + PANEL_A & WIRING
```

**Breakdown:**
- `WAREHOUSE_A` = installation site (physical location)
- `PUMP_01` = function
- `MCC_01` = cabinet
- `SCH` = document type

---

### Example 3: Safety System Documentation

```
EMERGENCY_STOP + SAFETY_RELAY & SCH
EMERGENCY_STOP + SAFETY_RELAY & DETAIL
EMERGENCY_STOP + CONTROL_PANEL & WIRING
```

**Benefit:** All E-stop pages are grouped together and easily searchable by function

---

### Excel Template for Page Planning

| Function    | Location    | Document Type | Page ID                  |
|-------------|-------------|---------------|--------------------------|
| PUMP_01     | MCC_01      | SCH           | PUMP_01+MCC_01&SCH       |
| PUMP_01     | MCC_01      | WIRING        | PUMP_01+MCC_01&WIRING    |
| MOTOR_CTRL  | PANEL_A     | SCH           | MOTOR_CTRL+PANEL_A&SCH   |

---

## References

- EPLAN P8 Documentation: Page Structure Configuration
- IEEE 1346: Standard for Interconnecting Distributed Resources with Electric Power Systems
- IEC 61346-1: Industrial systems, machines and devices - Structuring principles and reference designations
