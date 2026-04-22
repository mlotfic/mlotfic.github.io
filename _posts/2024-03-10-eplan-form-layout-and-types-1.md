---
layout: post
cover_color: #000000

keywords: EPLAN P8, Project Structure, Forms, Reports, Document Types, Electrical Design, Project Documentation, Standard Forms, Report Generation, EPLAN P8 Reference

title: "EPLAN Forms Reference Guide — Part 1: Report Structure"

description: >-
  A comprehensive reference guide to the standard report and form structure of an EPLAN Electric P8 project, including form types, purposes, examples, and applicable standards.

date: 2024-03-10 10:00:00 +0800
author: Mahmoud Lotfi
file_name: 2024-03-10-eplan-form-layout-and-types-1.md
categories: [EPLAN, Forms, Reports, Documentation]
tags: [Eplan, forms, reports]
pin: False
math: true
mermaid: true
comments: true
toc: true
render_with_liquid: false

image:
  path: /assets/img/posts/eplan.jpg
  alt: EPLAN Forms Explained
  lqip: data:image/webp;base64,UklGRjoAAABXRUJQVlA4IC4AAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
---

# EPLAN Electric P8 — Form Layout Areas & Form Types Reference

> **Software:** EPLAN Electric P8
> **Topic:** Form layout insert menu — area types, functions, and complete form type reference `.f00`–`.f34`
> **Level:** Beginner to Intermediate

---

## Overview

When building or editing a form in EPLAN P8, the **Insert** menu provides all the structural building blocks that define how a report page is laid out and how data flows through it. Understanding each area type — and knowing which form type to assign it to — is the foundation of professional form design in EPLAN.

---

## The Insert Menu — Form Layout Elements

Accessed via: **Insert → Forms** inside the Form Editor

```
Insert
└── Forms
    ├── Header
    ├── Data header area
    ├── Data area
    ├── Data footer area
    ├── Conditional area
    ├── Footer
    ├── Placeholder text
    ├── Insertion point of next form
    └── Conditional forms
```

Also available under **Insert**:
- **Text** — static text labels
- **Image file** — company logo or symbol graphics
- **Hyperlink** — clickable URL reference

---

## Form Layout Areas — Detailed Reference

### 1. Header

| Attribute | Detail |
|-----------|--------|
| **What it is** | The top section of a report page, rendered **once per page** |
| **Contains** | Title block frame, project name, page number, company logo, revision box |
| **Data source** | Header object properties only (project-level and page-level) |
| **Rendered** | Once at the top of every generated page |
| **Editable after generation** | No |

**Function:**
The Header area defines the static frame and metadata that appears at the top (or around the border) of every report page. It is the equivalent of a printed document's letterhead.

**When to use:**
Always. Every form must have a Header area. It is where you place the title block with project name, drawing number, revision history, date, and company logo.

**What goes inside:**
- Company name and logo (`Image file`)
- Project name placeholder `<10011>`
- Drawing number `<10141>`
- Revision `<10151>`
- Page number `<11021>` / Total pages `<11031>`
- Creator `<10081>`, Approved by `<10083>`
- Date `<10091>`

**Example output:**
```
┌─────────────────────────────────────────────────────┐
│  ACME Engineering  │ Project: MCC-01  │ Rev: 03     │
│  Drawing: E-001    │ Date: 11.03.2026 │ Page: 7/24  │
└─────────────────────────────────────────────────────┘
```

---

### 2. Data Header Area

| Attribute | Detail |
|-----------|--------|
| **What it is** | Column label row rendered **once per data table**, above the data rows |
| **Contains** | Fixed column heading labels — "Device Tag", "Description", "Article No." |
| **Data source** | Static text only — no placeholders |
| **Rendered** | Once per table block (not repeated per row) |
| **Editable after generation** | No |

**Function:**
Defines the column titles for the table that follows. It separates the header from the repeating data rows so the reader knows what each column means.

**When to use:**
Any form that outputs a table of records — parts lists, terminal lists, cable lists, connection lists, device tag lists. Without a Data header area, tables have no column labels.

**What goes inside:**
- Static text strings: `"Tag"`, `"Description"`, `"Article No."`, `"Qty"`, `"Manufacturer"`
- Vertical separator lines between columns
- Background fill or border lines for visual separation

**Example output:**
```
┌──────────────┬────────────────────┬───────────────┬─────┐
│ Device Tag   │ Description        │ Article No.   │ Qty │
├──────────────┼────────────────────┼───────────────┼─────┤
```

---

### 3. Data Area

| Attribute | Detail |
|-----------|--------|
| **What it is** | The **repeating row template** — the most important area in any report form |
| **Contains** | Placeholder properties that fill with real data — one copy per record |
| **Data source** | Data object properties (device, terminal, cable, part, PLC) |
| **Rendered** | Once per data record — repeated as many times as there are records |
| **Editable after generation** | No — change source data and regenerate |

**Function:**
This is the engine of the form. EPLAN reads this area once, then copies and fills it for every matching data record in the project. If your project has 50 terminals, the Data area is rendered 50 times — each time with the data for one terminal.

**When to use:**
Every report form that lists multiple records must have a Data area. This includes:
- Parts lists (one row per part)
- Terminal diagrams (one row per terminal)
- Cable overviews (one row per cable)
- Connection lists (one row per wire)
- Device tag lists (one row per device)
- PLC diagrams (one row per I/O channel)

**What goes inside:**
- Placeholder texts referencing Data object properties
- Separator lines matching the Data header area column widths
- Optional conditional formatting (bold for certain types, etc.)

**Example — Parts list Data area template:**
```
│ <20001>      │ <20631>            │ <20601>       │<20801>│
```
**Rendered output (5 rows for 5 devices):**
```
│ =GB1+ET1-K1  │ Main contactor 11kW│ 3RT2026-1AP00 │  5  │
│ =GB1+ET1-F1  │ Motor circuit bkr  │ 3RV2021-4AA10 │  1  │
│ =GB1+ET1-Q1  │ Main isolator      │ 3LD2203-0TK53 │  1  │
```

> ⚠️ **Critical rule:** Placeholders for device/cable/terminal data **only work inside the Data area**. Placing them outside produces blank or incorrect output.

---

### 4. Data Footer Area

| Attribute | Detail |
|-----------|--------|
| **What it is** | A summary row rendered **once after all data rows** on a page or table |
| **Contains** | Totals, sums, closing borders, page subtotals |
| **Data source** | Header object (for totals) or summation placeholders |
| **Rendered** | Once — after the last data row of the table block |
| **Editable after generation** | No |

**Function:**
Closes the data table and optionally displays calculated totals. Useful for showing total quantities, total cable length, total price, or simply drawing a closing border line under the last data row.

**When to use:**
- **Parts lists** — to show total item count or total cost
- **Cable overview** — to show total cable length
- **Terminal lists** — to show total terminal count per strip
- Any table where a summary row adds value

**What goes inside:**
- Static label `"Total:"` or `"Sum:"`
- Summation placeholder for quantity `<20801>` with **Add up** summation enabled
- Total price placeholder `<20831>`
- Closing horizontal border line

**Example output:**
```
├──────────────┼────────────────────┼───────────────┼─────┤
│              │                    │ TOTAL:        │  7  │
└──────────────┴────────────────────┴───────────────┴─────┘
```

---

### 5. Conditional Area

| Attribute | Detail |
|-----------|--------|
| **What it is** | A block that is **only rendered when a defined condition is true** |
| **Contains** | Any layout elements — text, placeholders, lines, images |
| **Data source** | Evaluated against a property value or condition expression |
| **Rendered** | Only when the condition evaluates to true for that record |
| **Editable after generation** | No |

**Function:**
Allows the form to show or hide content dynamically based on data. For example: show a warning symbol only if a device has an ATEX classification, or show a shielding note only if a cable is shielded.

**When to use:**
- Show `"ATEX"` label only for explosion-protected devices
- Show shielding note on cable forms only when `Shielded = Yes`
- Show a spare terminal marker only when terminal type = `"Spare"`
- Display different row formatting for PE terminals vs signal terminals

**Condition logic examples:**
```
Property: Cable: Shielded  =  "Yes"   → show shielding note block
Property: ATEX identifier  ≠  ""      → show ATEX warning row
Property: Terminal type    =  "PE"    → show green/yellow color marker
```

**Expert tip:** Conditional areas are one of the most powerful but underused features in EPLAN form design. They eliminate the need for separate form variants for similar report types.

---

### 6. Footer

| Attribute | Detail |
|-----------|--------|
| **What it is** | The bottom section of a report page, rendered **once per page** |
| **Contains** | Page number, revision notes, legal text, continuation markers |
| **Data source** | Header object properties (page-level) |
| **Rendered** | Once at the bottom of every generated page |
| **Editable after generation** | No |

**Function:**
Mirrors the Header in purpose but appears at the bottom of the page. Used for page numbering, "continued on next page" markers, and legal/copyright text.

**When to use:**
- When your title block is at the bottom of the page (common in European engineering drawing standards)
- When you need "Page X of Y" at the bottom
- When regulatory documentation requires a footer disclaimer

**What goes inside:**
- Page number `<11021>` and total pages `<11031>`
- Revision index `<10151>`
- "Sheet continues" text (static)
- Company legal text

---

### 7. Placeholder Text

| Attribute | Detail |
|-----------|--------|
| **What it is** | An individual dynamic text element that resolves to a property value |
| **Contains** | A single property reference (one placeholder per text element) |
| **Data source** | Header object or Data object depending on placement |
| **Rendered** | Replaced with real data value on report generation |

**Function:**
The atomic unit of dynamic content in a form. Every dynamic value on a form — whether a device tag, a page number, or a manufacturer name — is a placeholder text element linked to a specific property.

**When to use:**
Whenever you need to display a value that comes from the project database rather than typed manually. Use inside any of the areas above.

**How to insert:**
`Insert → Forms → Placeholder text` then configure in the Properties dialog (see `README_Placeholder_Properties.md`).

---

### 8. Insertion Point of Next Form

| Attribute | Detail |
|-----------|--------|
| **What it is** | A marker that defines where the **next chained form begins** on a multi-form page |
| **Contains** | A positional anchor point only — no visible content |
| **Rendered** | Not visible in output — used by EPLAN engine only |

**Function:**
When a report requires more than one form type on the same page (e.g., a terminal diagram followed immediately by a parts list for that strip), the insertion point marker tells EPLAN where the second form should start.

**When to use:**
- Combined report pages with two table types stacked vertically
- Terminal-strip overview followed by a cable entry table on the same page
- Any form that chains into a secondary form (`Conditional forms`)

---

### 9. Conditional Forms

| Attribute | Detail |
|-----------|--------|
| **What it is** | A form block that is **only inserted when a condition is met** — at the form level, not the row level |
| **Contains** | A complete secondary form reference |
| **Rendered** | Only when the triggering condition is satisfied for the current record set |

**Function:**
Similar to Conditional area but operates at the whole-form level. Allows a completely different form layout to be used depending on the data context — for example, using a different terminal form layout for power terminals vs signal terminals.

**When to use:**
- Different layout needed for different terminal strip types
- Special form for ATEX-rated cable entries vs standard cables
- Alternate BOM format for fluid components vs electrical components

---

## Area Rendering Order on a Generated Page

```
┌──────────────────────────────────┐
│           HEADER                 │  ← Rendered once per page
├──────────────────────────────────┤
│        DATA HEADER AREA          │  ← Rendered once per table block
├──────────────────────────────────┤
│          DATA AREA               │  ← Repeated once per record
│          DATA AREA               │
│          DATA AREA               │
│          DATA AREA               │
│    [CONDITIONAL AREA if true]    │  ← Only when condition met
│          DATA AREA               │
├──────────────────────────────────┤
│        DATA FOOTER AREA          │  ← Rendered once after last row
├──────────────────────────────────┤
│           FOOTER                 │  ← Rendered once per page
└──────────────────────────────────┘
```

---

## Complete Form Type Reference — `.f00` through `.f34`

### `.f00` — Title Page / Cover Sheet

| Attribute | Detail |
|-----------|--------|
| **Report type** | Title page, cover sheet, front matter |
| **Areas used** | Header, Footer, Placeholder text |
| **Key properties** | Project name, customer, revision, creator, approver, date |
| **Interactive or generated** | 🔀 Mixed — cover sheet interactive; material regs / safety auto-generated |
| **When to use** | Always — mandatory for every documentation package |
| **Typical content** | Company logo, project metadata, revision table, compliance declarations, safety instructions |

---

### `.f01` — Table of Contents

| Attribute | Detail |
|-----------|--------|
| **Report type** | Document index / TOC |
| **Areas used** | Header, Data header area, Data area, Footer |
| **Key properties** | Page name `<11001>`, page description `<11011>`, page number `<11021>`, page type `<11051>` |
| **Interactive or generated** | ⚙️ Auto-generated |
| **When to use** | Always — include in every formal documentation deliverable |
| **Typical content** | One row per page: page designator, description, page type, page number |

---

### `.f02` — Revision Overview

| Attribute | Detail |
|-----------|--------|
| **Report type** | Revision history list |
| **Areas used** | Header, Data header area, Data area, Footer |
| **Key properties** | Revision index, description, date, editor, approver |
| **Interactive or generated** | ⚙️ Auto-generated |
| **When to use** | Projects with formal revision control — client deliverables, regulated industries |
| **Typical content** | Revision table with date, change description, drawn/approved columns |

---

### `.f03` — Parts List (Page-based)

| Attribute | Detail |
|-----------|--------|
| **Report type** | Parts list per schematic page |
| **Areas used** | Header, Data header area, Data area, Data footer area, Footer |
| **Key properties** | Device tag, article number, description, quantity, manufacturer |
| **Interactive or generated** | ⚙️ Auto-generated |
| **When to use** | When BOM per schematic page is required (less common than `.f05`) |
| **Typical content** | All components on one page listed with part numbers |

---

### `.f04` — Cable Diagram / Cable Overview

| Attribute | Detail |
|-----------|--------|
| **Report type** | Cable documentation |
| **Areas used** | Header, Data header area, Data area, Conditional area, Footer |
| **Key properties** | Cable designation, type, length, from/to terminals, cross-section, shielded |
| **Interactive or generated** | ⚙️ Auto-generated |
| **When to use** | Any project with routed cables between devices or panels |
| **Typical content** | Individual: one cable per page with conductor table. Total: all cables in one summary |

---

### `.f05` — Summarized Parts List (BOM)

| Attribute | Detail |
|-----------|--------|
| **Report type** | Consolidated Bill of Materials |
| **Areas used** | Header, Data header area, Data area, Data footer area, Footer |
| **Key properties** | Article number, description, manufacturer, quantity, unit, price |
| **Interactive or generated** | ⚙️ Auto-generated |
| **When to use** | End of engineering — procurement BOM for purchasing department |
| **Typical content** | All identical parts summed: Qty 5 × Siemens 3RT2026-1AP00 @ €45 = €225 |

---

### `.f06` — Device Tag List

| Attribute | Detail |
|-----------|--------|
| **Report type** | Complete list of all device tags |
| **Areas used** | Header, Data header area, Data area, Footer |
| **Key properties** | Full device tag, function text, type, article number, installation location |
| **Interactive or generated** | ⚙️ Auto-generated |
| **When to use** | Design review, asset register, cross-reference checking |
| **Typical content** | Every tagged device with its full designation and associated part data |

---

### `.f07` — Plug / Connector Overview

| Attribute | Detail |
|-----------|--------|
| **Report type** | Connector and plug pin assignment overview |
| **Areas used** | Header, Data header area, Data area, Footer |
| **Key properties** | Connector designation, pin number, signal name, wire color, cross-section |
| **Interactive or generated** | ⚙️ Auto-generated |
| **When to use** | Projects with multi-pin connectors, harnesses, or equipment interfaces |
| **Typical content** | Pin-by-pin wiring table for each connector in the project |

---

### `.f08` — Structure Identifier Overview

| Attribute | Detail |
|-----------|--------|
| **Report type** | Reference designation structure summary |
| **Areas used** | Header, Data header area, Data area, Footer |
| **Key properties** | Higher-level assignment `=`, installation location `+`, descriptions |
| **Interactive or generated** | ⚙️ Auto-generated |
| **When to use** | Project setup review, tag convention documentation, client handover |
| **Standard** | IEC 81346 |
| **Typical content** | Tree of all `=`, `+`, `-` identifiers used with their descriptions |

---

### `.f09` — Terminal Connection Diagram

| Attribute | Detail |
|-----------|--------|
| **Report type** | Graphical terminal wiring connection diagram |
| **Areas used** | Header, Data area, Conditional area, Footer |
| **Key properties** | Terminal designation, internal/external connections, wire, cable |
| **Interactive or generated** | ⚙️ Auto-generated |
| **When to use** | Detailed graphical wiring documentation for complex terminal assemblies |
| **Typical content** | Graphical representation of terminal with wires shown as lines |

---

### `.f10` — Terminal-Strip Overview

| Attribute | Detail |
|-----------|--------|
| **Report type** | Terminal strip layout and wiring overview |
| **Areas used** | Header, Data header area, Data area, Conditional area, Data footer area, Footer |
| **Key properties** | Strip name, terminal designation, wire color, cross-section, bridge groups |
| **Interactive or generated** | ⚙️ Auto-generated |
| **When to use** | Mandatory for all projects with terminal blocks — used by panel builders |
| **Typical content** | Strip X1: ordered list of terminals with connections, colors, cross-sections |

---

### `.f11` — Terminal Diagram

| Attribute | Detail |
|-----------|--------|
| **Report type** | Detailed per-terminal wiring diagram |
| **Areas used** | Header, Data header area, Data area, Conditional area, Footer |
| **Key properties** | Terminal designation, internal connection, external connection, cable, conductor, wire color |
| **Interactive or generated** | ⚙️ Auto-generated |
| **When to use** | Complex marshalling panels, junction boxes, field instrument wiring |
| **Typical content** | Each terminal row shows full from/to path including cable and conductor reference |

---

### `.f12` — PLC Card Overview

| Attribute | Detail |
|-----------|--------|
| **Report type** | PLC hardware card layout overview |
| **Areas used** | Header, Data header area, Data area, Footer |
| **Key properties** | Card designation, slot, article number, rack |
| **Interactive or generated** | ⚙️ Auto-generated |
| **When to use** | Projects with PLC systems where hardware layout documentation is required |
| **Typical content** | Rack/slot table listing each card with its type and address range |

---

### `.f13` — Bus System Overview

| Attribute | Detail |
|-----------|--------|
| **Report type** | Fieldbus / network topology overview |
| **Areas used** | Header, Data header area, Data area, Footer |
| **Key properties** | Bus name, device address, device type, cable type |
| **Interactive or generated** | ⚙️ Auto-generated |
| **When to use** | Projects with PROFIBUS, PROFINET, DeviceNet, or other fieldbus systems |
| **Typical content** | All bus nodes listed with addresses and device types |

---

### `.f14` — Fluid Power / Pneumatic Parts List

| Attribute | Detail |
|-----------|--------|
| **Report type** | Parts list specific to fluid power components |
| **Areas used** | Header, Data header area, Data area, Data footer area, Footer |
| **Key properties** | Device tag (fluid), description, article number, quantity |
| **Interactive or generated** | ⚙️ Auto-generated |
| **When to use** | Projects with pneumatic or hydraulic circuits documented in EPLAN Fluid |
| **Typical content** | Valves, cylinders, fittings, regulators with part numbers |

---

### `.f17` — Connection List

| Attribute | Detail |
|-----------|--------|
| **Report type** | Point-to-point wiring list |
| **Areas used** | Header, Data header area, Data area, Footer |
| **Key properties** | From terminal, to terminal, wire color, cross-section, potential, cable name |
| **Interactive or generated** | ⚙️ Auto-generated |
| **When to use** | Panel wiring and commissioning — replaces reading schematics on the shop floor |
| **Typical content** | Every wire: X1:1 → K1:A1, BK, 1.5mm², L1 |

---

### `.f18` — Potential Overview

| Attribute | Detail |
|-----------|--------|
| **Report type** | List of all electrical potentials in the project |
| **Areas used** | Header, Data header area, Data area, Footer |
| **Key properties** | Potential name, voltage level, frequency, signal type |
| **Interactive or generated** | ⚙️ Auto-generated |
| **When to use** | Verifying potential definitions and checking for naming conflicts |
| **Typical content** | 24VDC, 230VAC, L1, L2, L3, PE, GND — all potentials listed |

---

### `.f19` — Signal Overview

| Attribute | Detail |
|-----------|--------|
| **Report type** | List of all defined signals and their properties |
| **Areas used** | Header, Data header area, Data area, Footer |
| **Key properties** | Signal name, type, source device, target device |
| **Interactive or generated** | ⚙️ Auto-generated |
| **When to use** | I&C projects — cross-referencing signal names to physical connections |
| **Typical content** | All signal names with source and destination devices |

---

### `.f22` — PLC Diagram (SPS Connection)

| Attribute | Detail |
|-----------|--------|
| **Report type** | PLC I/O wiring connection diagrams |
| **Areas used** | Header, Data header area, Data area, Conditional area, Footer |
| **Key properties** | PLC address, signal name, I/O type, card, slot, channel, symbolic address |
| **Interactive or generated** | ⚙️ Auto-generated |
| **When to use** | All automation projects with a PLC — links field wiring to I/O cards |
| **Typical content** | I0.0 = Emergency_Stop_S1 → Terminal X10:1 → Card DI slot 2 channel 0 |
| **Note** | "SPS" = German abbreviation for PLC |

---

### `.f30` — P&ID / Piping Overview

| Attribute | Detail |
|-----------|--------|
| **Report type** | Piping and Instrumentation Diagram overview page |
| **Areas used** | Header, Footer (diagram content is interactive) |
| **Key properties** | Process equipment tags, instrument tags, pipe designations |
| **Interactive or generated** | ✏️ Interactive (drawn manually in P&ID editor) |
| **When to use** | Process plants, HVAC, water treatment, any fluid system with instrumentation |
| **Standard** | IEC 10628 / ISA 5.1 |
| **Typical content** | Pumps, vessels, heat exchangers, valves, instruments with signal lines |

---

### `.f31` — Pre-planning: Pipe Class Overview

| Attribute | Detail |
|-----------|--------|
| **Report type** | Pipe specification class documentation |
| **Areas used** | Header, Data header area, Data area, Footer |
| **Key properties** | Pipe class name, material, pressure rating, temperature range, standard |
| **Interactive or generated** | ✏️ Interactive (Pre-planning Navigator) |
| **When to use** | FEED phase — define pipe classes before detailed P&ID work begins |
| **Typical content** | Class A1B: Carbon steel, PN40, −20 to +300°C, for steam/utility systems |

---

### `.f32` — Pre-planning: Planning Object Overview

| Attribute | Detail |
|-----------|--------|
| **Report type** | High-level functional planning object summary |
| **Areas used** | Header, Data header area, Data area, Footer |
| **Key properties** | Planning object tag, description, loop number, assigned devices |
| **Interactive or generated** | ✏️ Interactive (Pre-planning Navigator) |
| **When to use** | Early project phases — scope definition before detailed engineering |
| **Typical content** | PCT loops, cable placeholders, functional unit assignments |

---

### `.f33` — Pre-planning: Loop Diagram

| Attribute | Detail |
|-----------|--------|
| **Report type** | Instrumentation loop diagram |
| **Areas used** | Header, Data area, Conditional area, Footer |
| **Key properties** | Loop number, instrument tag, signal type, cable, terminal, DCS address |
| **Interactive or generated** | 🔀 Mixed — loop defined in Pre-planning Navigator, diagram auto-rendered |
| **When to use** | All process instrumentation loops — mandatory for FAT/SAT |
| **Standard** | ISA 5.4 |
| **Typical content** | TT-101 (4-20mA HART) → JB terminal → Marshalling → AI card → DCS tag |

---

### `.f34` — Pre-planning: Substance Overview

| Attribute | Detail |
|-----------|--------|
| **Report type** | Process medium / substance documentation |
| **Areas used** | Header, Data header area, Data area, Footer |
| **Key properties** | Substance name, phase, temperature, pressure, ATEX zone, hazard class |
| **Interactive or generated** | ✏️ Interactive (Pre-planning Navigator) |
| **When to use** | Chemical, oil & gas, or any process project with regulated media |
| **Typical content** | Natural Gas: Gas phase, 10 bar, ATEX Zone 1, Hazard class II B T3 |

---

## Area × Form Type Matrix

Which areas are typically used in each form type:

| Form | Header | Data Header | Data Area | Data Footer | Conditional | Footer |
|------|:------:|:-----------:|:---------:|:-----------:|:-----------:|:------:|
| `.f00` Title page | ✅ | — | — | — | — | ✅ |
| `.f01` TOC | ✅ | ✅ | ✅ | — | — | ✅ |
| `.f04` Cable | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `.f05` Parts list | ✅ | ✅ | ✅ | ✅ | — | ✅ |
| `.f06` Device list | ✅ | ✅ | ✅ | — | ✅ | ✅ |
| `.f08` Structure | ✅ | ✅ | ✅ | — | — | ✅ |
| `.f10` Terminal strip | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `.f11` Terminal diagram | ✅ | ✅ | ✅ | — | ✅ | ✅ |
| `.f17` Connection list | ✅ | ✅ | ✅ | — | — | ✅ |
| `.f22` PLC diagram | ✅ | ✅ | ✅ | — | ✅ | ✅ |
| `.f30` P&ID | ✅ | — | — | — | — | ✅ |
| `.f33` Loop diagram | ✅ | — | ✅ | — | ✅ | ✅ |

---

## Summary

| Area | Rendered | Data Source | Core Purpose |
|------|----------|-------------|-------------|
| **Header** | Once per page | Header object | Title block, project metadata |
| **Data header area** | Once per table | Static text | Column labels |
| **Data area** | Once per record | Data object | Repeating data rows |
| **Data footer area** | Once after last row | Header object / sum | Totals, closing border |
| **Conditional area** | Only if condition true | Data object | Dynamic show/hide content |
| **Footer** | Once per page | Header object | Page number, legal text |
| **Placeholder text** | Per placement | Header or Data object | Single dynamic value |
| **Insertion point** | Engine only | — | Chain multiple forms |
| **Conditional forms** | Only if condition true | — | Alternate form layout |

---

## Related Files

| File | Description |
|------|-------------|
| `eplan_p8_project_structure.json` | Full metadata for all 16 project report folders |
| `README.md` | General project structure reference |
| `README_Interactive_vs_AutoGenerated.md` | Interactive vs. auto-generated page types |
| `README_Form_Components.md` | Form file anatomy and placeholder syntax overview |
| `README_Placeholder_Properties.md` | Placeholder text dialog — elements and categories |
| `README_Expert_Properties.md` | Expert property reference with form mapping |
| `README_Form_Layout_and_Types.md` | This file |

---

*EPLAN Electric P8 — Engineering Reference Documentation*
