# EPLAN P8 Page Structure Guide

## Overview

The **Page Structure** dialog in EPLAN P8 defines the naming and identification scheme for electrical schematic pages. It creates a hierarchical template that dictates how pages are organized, labeled, and referenced throughout your electrical project documentation.

---

## Page Structure Components

### 1. Functional Assignment (`==`)
**Purpose:** Groups related electrical circuits or functions together at a high level

**Status:** Not available (disabled)

**Example:**
- `POWER DISTRIBUTION`
- `MOTOR CONTROL`
- `SAFETY SYSTEMS`

**Use Case:** When you want to organize pages by major system categories

---

### 2. Function Designation (`=`)
**Purpose:** Names individual circuit functions or subsystems

**Status:** Identifying (active)

**Example:**
- `PUMP_01` (pump circuit)
- `HEATER_CTRL` (heater control)
- `EMERGENCY_STOP` (E-stop circuit)

**Use Case:** Each unique function gets its own designation for clear identification

---

### 3. Installation Site (`++`)
**Purpose:** Specifies the physical location where equipment is installed

**Status:** Not available (disabled)

**Example:**
- `WAREHOUSE_A`
- `PRODUCTION_LINE_2`
- `EXTERNAL_SUBSTATION`

**Use Case:** When the same circuit design is replicated across multiple physical locations

---

### 4. Location Designation (`+`)
**Purpose:** Identifies the specific cabinet, panel, or enclosure where electrical components reside

**Status:** Identifying (active)

**Example:**
- `MCC_01` (Motor Control Center 1)
- `PANEL_A` (Control Panel A)
- `BREAKER_BOX_MAIN` (Main breaker box)

**Use Case:** Essential for linking documentation to physical equipment locations

---

### 5. Document Type (`&`)
**Purpose:** Categorizes the type of electrical page/document

**Status:** Identifying (active)

**Example:**
- `SCH` (Schematic)
- `WIRING` (Wiring diagram)
- `LAYOUT` (Component layout)
- `DETAIL` (Detail sheet)

**Use Case:** Distinguishes between different documentation types for the same system

---

### 6. User-Defined Structure (`#`)
**Purpose:** Custom fields for project-specific organizational needs

**Status:** Not available (disabled)

**Example:**
- `REV_A` (Revision)
- `VENDOR_SIEMENS` (Vendor identification)
- `COST_CENTER_123` (Accounting reference)

**Use Case:** Flexible custom metadata when standard fields don't fit

---

### 7. Higher-Level Function Number
**Purpose:** References parent functions in a hierarchical structure

**Status:** Not available (disabled)

**Example:**
- Links `PUMP_01_MOTOR_CTRL` back to parent `PUMP_01`

**Use Case:** Creating multi-level functional hierarchies

---

## Status Meanings

| Status | Definition | Impact |
|--------|-----------|--------|
| **Identifying** | Field is active and used to uniquely identify pages | Page names must include this field |
| **Not available** | Field is disabled in the current scheme | Field won't be used for page identification |

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

## JSON Format Export

When exporting or automating EPLAN projects, the page structure can be represented as JSON:

### Basic Structure
```json
{
  "pageStructure": {
    "scheme": "Function designation, location designation and document type",
    "description": "Function designation, location designation and document type identifying",
    "identifyingFields": [
      {
        "name": "Function designation",
        "symbol": "=",
        "status": "Identifying"
      },
      {
        "name": "Location designation",
        "symbol": "+",
        "status": "Identifying"
      },
      {
        "name": "Document type",
        "symbol": "&",
        "status": "Identifying"
      }
    ],
    "nonIdentifyingFields": [
      {
        "name": "Functional assignment",
        "symbol": "==",
        "status": "Not available"
      },
      {
        "name": "Installation site",
        "symbol": "++",
        "status": "Not available"
      }
    ]
  }
}
```

### Page Instance Example
```json
{
  "pages": [
    {
      "pageId": "PUMP_01+MCC_01&SCH",
      "functionDesignation": "PUMP_01",
      "locationDesignation": "MCC_01",
      "documentType": "SCH",
      "description": "Pump 01 schematic in Motor Control Center 01"
    },
    {
      "pageId": "MOTOR_CTRL+PANEL_A&WIRING",
      "functionDesignation": "MOTOR_CTRL",
      "locationDesignation": "PANEL_A",
      "documentType": "WIRING",
      "description": "Motor control wiring diagram in Panel A"
    }
  ]
}
```

---

## When to Modify Page Structure

### Modify When:
- ✅ Adding new physical locations to your facility
- ✅ Implementing new equipment categories
- ✅ Need to track additional metadata (revisions, vendors, cost centers)
- ✅ Expanding from single-site to multi-site operations
- ✅ Standardizing naming across multiple EPLAN projects

### Don't Modify When:
- ❌ Project is already in production documentation phase
- ❌ Changing structure would break existing page references
- ❌ Team hasn't agreed on new standards

---

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

### 4. **Documentation**
```
Example Project Structure:
├── Function Designations (PUMP_xx, MOTOR_xx, CTRL_xx)
├── Locations (MCC_01-03, PANEL_A-C, BREAKER_MAIN)
└── Document Types (SCH, WIRING, LAYOUT, DETAIL)
```

---

## Troubleshooting

### Issue: Can't find pages by location
**Solution:** Ensure `Location designation` is marked as "Identifying"

### Issue: Pages with same function appear scattered
**Solution:** Add `Installation site` to identifying fields if managing multiple locations

### Issue: Naming becomes inconsistent
**Solution:** Create and enforce a naming standard document in your team

### Issue: Schema is too complex
**Solution:** Simplify to only truly identifying fields; use comments for metadata

---

## Integration with Automation

### Python Example: Parse EPLAN Page Structure
```python
import json

# Load page structure from JSON export
with open('page_structure.json', 'r') as f:
    structure = json.load(f)

# Extract identifying fields
identifying = [field for field in structure['pageStructure']['identifyingFields']]

# Generate page ID from components
def generate_page_id(function, location, doctype):
    return f"{function}+{location}&{doctype}"

# Example
page_id = generate_page_id("PUMP_01", "MCC_01", "SCH")
print(page_id)  # Output: PUMP_01+MCC_01&SCH
```

### Excel Template for Page Planning
| Function | Location | Document Type | Page ID |
|----------|----------|----------------|---------|
| PUMP_01 | MCC_01 | SCH | PUMP_01+MCC_01&SCH |
| PUMP_01 | MCC_01 | WIRING | PUMP_01+MCC_01&WIRING |
| MOTOR_CTRL | PANEL_A | SCH | MOTOR_CTRL+PANEL_A&SCH |

---

## Summary

The Page Structure in EPLAN P8 is a powerful organization tool that:
- **Identifies** pages uniquely using consistent naming schemes
- **Organizes** electrical documentation hierarchically
- **Scales** across single and multi-site projects
- **Integrates** with automation and data management workflows

Use identifying fields strategically to balance organization with simplicity, and document your choices for team consistency.

---

## References

- EPLAN P8 Documentation: Page Structure Configuration
- IEEE 1346: Standard for Interconnecting Distributed Resources with Electric Power Systems
- IEC 61346-1: Industrial systems, machines and devices - Structuring principles and reference designations
