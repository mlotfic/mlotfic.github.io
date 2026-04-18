---
title: EPLAN P8 Page Structure Guide
date: 2024-03-15 10:30:00 +0000
categories: [EPLAN, Documentation, Electrical]
tags: [page-structure, naming-convention, organization]
pin: true
---

## Overview

The **Page Structure** dialog in EPLAN P8 defines the naming and identification scheme for electrical schematic pages. It creates a hierarchical template that dictates how pages are organized, labeled, and referenced throughout your electrical project documentation.

## Page Structure Components

### 1. Functional Assignment (`==`)
**Purpose:** Groups related electrical circuits or functions together at a high level

**Status:** Not available (disabled)

**Example:**
- `POWER DISTRIBUTION`
- `MOTOR CONTROL`
- `SAFETY SYSTEMS`

---

### 2. Function Designation (`=`)
**Purpose:** Names individual circuit functions or subsystems

**Status:** Identifying (active)

**Example:**
- `PUMP_01` (pump circuit)
- `HEATER_CTRL` (heater control)
- `EMERGENCY_STOP` (E-stop circuit)

---

### 3. Installation Site (`++`)
**Purpose:** Specifies the physical location where equipment is installed

**Status:** Not available (disabled)

**Example:**
- `WAREHOUSE_A`
- `PRODUCTION_LINE_2`
- `EXTERNAL_SUBSTATION`

---

### 4. Location Designation (`+`)
**Purpose:** Identifies the specific cabinet, panel, or enclosure where electrical components reside

**Status:** Identifying (active)

**Example:**
- `MCC_01` (Motor Control Center 1)
- `PANEL_A` (Control Panel A)
- `BREAKER_BOX_MAIN` (Main breaker box)

---

### 5. Document Type (`&`)
**Purpose:** Categorizes the type of electrical page/document

**Status:** Identifying (active)

**Example:**
- `SCH` (Schematic)
- `WIRING` (Wiring diagram)
- `LAYOUT` (Component layout)
- `DETAIL` (Detail sheet)

---

### 6. User-Defined Structure (`#`)
**Purpose:** Custom fields for project-specific organizational needs

**Status:** Not available (disabled)

**Example:**
- `REV_A` (Revision)
- `VENDOR_SIEMENS` (Vendor identification)
- `COST_CENTER_123` (Accounting reference)

---

## Status Meanings

| Status | Definition | Impact |
|--------|-----------|--------|
| **Identifying** | Field is active and used to uniquely identify pages | Page names must include this field |
| **Not available** | Field is disabled in the current scheme | Field won't be used for page identification |

## Real-World Example

**Current Scheme:** Function designation, Location designation, Document type

**Generated Page Names:**
```
PUMP_01 + MCC_01 & SCH
PUMP_01 + MCC_01 & WIRING
MOTOR_CTRL + PANEL_A & SCH
MOTOR_CTRL + PANEL_A & DETAIL
HEATER_CTRL + PANEL_B & SCH
```

## Best Practices

### 1. **Naming Conventions**
```
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

---

## Troubleshooting

### Issue: Can't find pages by location
**Solution:** Ensure `Location designation` is marked as "Identifying"

### Issue: Pages with same function appear scattered
**Solution:** Add `Installation site` to identifying fields if managing multiple locations

### Issue: Naming becomes inconsistent
**Solution:** Create and enforce a naming standard document in your team

---

## Key Takeaways

✅ Use identifying fields strategically to balance organization with simplicity  
✅ Document your choices for team consistency  
✅ Design for scalability from the start  
✅ Establish naming standards before project begins  

---

For the complete detailed guide with JSON examples and automation tips, see our [full documentation](/posts/page-structure-complete-reference/).
