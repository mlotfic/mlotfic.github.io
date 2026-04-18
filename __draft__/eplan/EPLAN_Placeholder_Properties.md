# EPLAN Electric P8 — Placeholder Text Properties Reference

> **Software:** EPLAN Electric P8
> **Topic:** Placeholder text dialog — Properties, Elements, and Categories
> **Level:** Beginner Overview

---

## What is a Placeholder Text?

A **placeholder text** is a dynamic text element placed on a form (`.f??`) or schematic page that automatically fills in with real project or device data when EPLAN generates a report.

Instead of typing a fixed value like `"Siemens"`, you place a placeholder that reads the manufacturer property from the database — so the correct value appears automatically for every row or every project.

You configure placeholders through the **Properties (placeholder text)** dialog.

---

## The Properties Dialog

When you double-click a placeholder text element on a form canvas, the **Properties (placeholder text)** dialog opens. It has two tabs: **Placement** and **Format**.

```
┌──────────────────────────────────────────────┐
│         Properties (placeholder text)        │
├──────────────┬───────────────────────────────┤
│  Placement   │  Format                       │
└──────────────┴───────────────────────────────┘
```

---

## Placement Tab

The Placement tab defines **what data** the placeholder displays and **where it comes from**.

### Input Type — Three Options

| Option | What It Does |
|--------|-------------|
| **Property** | Displays a single property value from the project database (most common) |
| **Properties formatted / calculated** | Combines or calculates multiple properties (e.g., concatenate two fields, or compute a value) |
| **Action** | Triggers a special EPLAN function (e.g., insert page break, increment counter) |

> For most use cases, **Property** is the correct choice.

---

### Data Source Field

The **Data source** field defines which object the property is read from.

| Data Source | Meaning |
|-------------|---------|
| `Header object` | Data comes from the report header — project-level or page-level properties (same on every page) |
| `Data object` | Data comes from the repeating data records — one value per device, terminal, cable, or part |

```
Header object  →  Project name, date, revision, page number
Data object    →  Device tag, article number, description, cable type
```

---

### Element Tree

The **Element** panel (in the Placeholder texts browser on the right) shows the hierarchy of available data objects:

```
├── Header object
│   ├── Part (header object)
│   └── Part reference (header object)
└── Data object
    ├── Part
    ├── Part reference
    └── Record
```

| Element | Description |
|---------|-------------|
| **Header object** | Project or page-level data — applies once to the whole page |
| **Part (header object)** | Part data referenced in the page header context |
| **Part reference (header object)** | Part reference data in header context |
| **Data object** | The repeating record — one instance per row in a table report |
| **Part** | Part-level properties for the data row (e.g., article number, manufacturer) |
| **Part reference** | Part reference properties for the data row (e.g., quantity, mounting location) |
| **Record** | The base data record — device tag, description, connections |

> **Rule of thumb:** Use `Header object` for title block placeholders. Use `Data object` for table row placeholders.

---

### Summation Options

When the data source is a numeric property, the **Summation** section controls how values are handled across multiple rows:

| Option | Behaviour |
|--------|-----------|
| **Do not add up** | Each row shows its own value independently |
| **Add up in row** | Accumulates the value across rows (e.g., total quantity) |
| **Add up property in one row** | Checkbox — sums the property within a single combined row |

Additional checkboxes:

| Checkbox | Effect |
|----------|--------|
| **Replace identical text** | If the same value appears in consecutive rows, only show it once (suppresses repetition) |
| **Display all connections** | Shows every connection associated with the device, even if it spans multiple rows |

---

## The Placeholder Texts Browser

Clicking the `...` button next to the property field opens the **Placeholder texts** browser — a searchable library of every available property in EPLAN.

```
┌─────────────────────────┬──────────────────────────────┐
│  Element (tree)         │  Category (filter list)      │
├─────────────────────────┼──────────────────────────────┤
│  Header object          │  All categories              │
│    Part (header object) │  Archive data                │
│    Part reference       │  Cable data                  │
│  Data object            │  Category                    │
│    Part                 │  Certification               │
│    Part reference       │  Connection                  │
│    Record               │  Customer                    │
│                         │  Data                        │
│                         │  Data for reports            │
│                         │  Devices                     │
│                         │  Documents                   │
│                         │  Editing                     │
│                         │  End customer                │
│                         │  Formats                     │
│                         │  Function data               │
│                         │  General                     │
│                         │  Macro                       │
│                         │  Messages                    │
│                         │  Mounting data               │
│                         │  Parts                       │
│                         │  PLC data                    │
│                         │  Pre-planning 1–8            │
│                         │  Prices                      │
└─────────────────────────┴──────────────────────────────┘
```

---

## Property Categories

Categories are used to **filter the property list** so you can quickly find the placeholder you need. Each category groups related properties together.

| Category | What It Contains |
|----------|-----------------|
| **All categories** | Shows every available property (unfiltered) |
| **Archive data** | Document archiving and revision metadata |
| **Cable data** | Cable properties — type, length, diameter, cross-section, voltage level, shielding |
| **Category** | Device classification and category assignments |
| **Certification** | Compliance data — ATEX identifier, CE marking, VDE, UL category/file numbers |
| **Connection** | Wire/conductor properties — color, cross-section, potential, signal name |
| **Customer** | Customer-specific project fields |
| **Data** | General data fields for devices and parts |
| **Data for reports** | Properties specifically intended for use in generated reports |
| **Devices** | Core device properties — tag, description, function text, type |
| **Documents** | Document references linked to devices or parts |
| **Editing** | Internal EPLAN editing metadata (created by, modified date) |
| **End customer** | End-customer specific project information |
| **Formats** | Number and text format settings |
| **Function data** | Function-level properties and assignments |
| **General** | General-purpose project and page properties |
| **Macro** | Properties linked to macro objects and schematic macros |
| **Messages** | Check-run messages and validation flags |
| **Mounting data** | Physical mounting properties — clip height, mounting rail, position |
| **Parts** | Parts management data — article number, order number, manufacturer, stock |
| **PLC data** | PLC-specific properties — address, signal name, card, channel, slot |
| **Pre-planning 1–8** | Properties for pre-planning objects across 8 planning levels |
| **Prices** | Cost and pricing data from parts management |

---

## Cable Data Properties (Example List)

When the **Cable data** category is selected, the property list includes:

| Property | Description |
|----------|-------------|
| Blower available | Whether a blower is associated with the cable |
| CO2 emission | Environmental data field |
| Cable data | General cable data reference |
| Cable diameter | Physical outer diameter of the cable |
| Cable entry available | Whether a cable entry fitting is defined |
| Cable entry into device | Entry point designation on the device |
| Cable jacket: Color | Outer jacket colour |
| Cable length, max. | Maximum permitted cable length |
| Cable length, routed | Actual routed length from routing engine |
| Cable outer diameter | Outer diameter value |
| Cable outer diameter, max. | Maximum outer diameter tolerance |
| Cable outer diameter, min. | Minimum outer diameter tolerance |
| Cable reel | Reel or drum reference |
| Cable reel available | Whether reel data is assigned |
| Cable: Cross-section | Conductor cross-sectional area (mm²) |
| Cable: Voltage level | Rated voltage of the cable |
| Cables included | Number of individual cables in a bundle |
| Calibration approval | Calibration certification status |
| Capacitive load | Electrical capacitive load value |
| Center mismatch | Physical alignment offset |
| Certification: ATEX identifier | ATEX explosion protection classification |
| Certification: CE | CE conformity marking |
| Certification: General | General certification notes |
| Certification: UL Category Control Number | UL listing category number |
| Certification: UL File Number | UL file reference number |
| Certification: VDE | VDE standard compliance |
| Characteristic curve | Performance/characteristic curve reference |
| Circuit type | Electrical circuit classification |
| Climate class | Environmental climate class rating |
| Clip-on height | Physical clip height for mounting |
| Closing pressure | Mechanical closing pressure value |

---

## Property ID Numbers

Every property in EPLAN has an internal **ID number** shown in the description panel at the bottom of the browser (e.g., `<20501> Suppl. field: Text`).

These IDs are used when referencing properties in scripts, macros, or API integrations.

```
Example:
<20501> Suppl. field: Text
→ Supplementary field for part reference data.
→ Serves as a free additional property field.
→ Outputs the value of "Supplementary field text" (ID 20915) per part reference.
```

> When building custom forms, note the ID of the property you need — it ensures you are referencing the exact correct field, especially when multiple similarly-named properties exist.

---

## Step-by-Step: Inserting a Placeholder on a Form

1. Open a form file via **Utilities → Forms → Open**
2. Select **Insert → Text** (or use the text tool) on the form canvas
3. In the text properties dialog, switch the type to **Placeholder text**
4. Click the `...` button next to the property field — the **Placeholder texts browser** opens
5. Select the appropriate **Element** (Header object or Data object)
6. Use the **Category** filter to narrow down the property list
7. Select the property you need from the list
8. Click **OK** — the placeholder code is inserted into the text element
9. Position the text element on the form canvas
10. Save the form and regenerate reports to verify the output

---

## Common Mistakes to Avoid

| Mistake | Result | Fix |
|---------|--------|-----|
| Using a `Data object` property in the title block | Blank or repeated value | Use `Header object` properties in the title block |
| Using a `Header object` property inside the row template | Same value on every row | Use `Data object` properties in the row area |
| Placing placeholder outside the row area | Property not repeated per record | Move the text element inside the defined row area |
| Wrong category selected | Can't find the right property | Try **All categories** then search by keyword |

---

## Summary

| Concept | Description |
|---------|-------------|
| Placeholder text | Dynamic text element that auto-fills with project/device data |
| Property | The most common input type — reads a single data field |
| Header object | Source for page-level or project-level data |
| Data object | Source for repeating row data (devices, cables, terminals) |
| Category | Filter group used to find properties in the browser |
| Property ID | Internal EPLAN number uniquely identifying each property |
| Summation | Controls how numeric values accumulate across rows |

---

## Related Files

| File | Description |
|------|-------------|
| `eplan_p8_project_structure.json` | Full metadata for all 16 project report folders |
| `README.md` | General project structure reference |
| `README_Interactive_vs_AutoGenerated.md` | Interactive vs. auto-generated page types |
| `README_Form_Components.md` | Form file anatomy and placeholder syntax overview |
| `README_Placeholder_Properties.md` | This file |

---

*EPLAN Electric P8 — Engineering Reference Documentation*
