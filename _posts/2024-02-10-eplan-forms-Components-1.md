---
title: EPLAN Form Components Reference
description: >-
  A beginner-friendly overview of the structure and components of EPLAN form files (`.f??`), including the anatomy of a form page and the meaning of common property placeholders.
author: Mahmoud Lotfi
file_name: 2024-06-15-eplan-form-Components-1.md
date: 2024-06-01 10:00:00 +0800
categories: [EPLAN, Forms, Report Pages, Placeholders]
tags: [Eplan, forms, placeholders]
pin: False
math: false
mermaid: false
comments: true
toc: true
render_with_liquid: false
image:
  path: /assets/img/posts/eplan.jpg
  alt: EPLAN Form Components
  lqip: data:image/webp;base64,UklGRjoAAABXRUJQVlA4IC4AAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA

---

# EPLAN Electric P8 — Form Components Reference

> **Software:** EPLAN Electric P8
> **Topic:** Form file structure, anatomy, and property placeholders
> **Level:** Beginner Overview

---

## What is a Form in EPLAN P8?

A **form** in EPLAN P8 is a template file that defines how an auto-generated report page looks and what data it displays. Think of it as a **page layout blueprint** — it tells EPLAN where to put data, how to format it, and which properties to pull from the project database.

```
Project Data  +  Form Template  =  Generated Report Page
(your devices,    (.f?? file)       (terminal list, BOM,
 terminals,                          cable diagram, etc.)
 cables, etc.)
```

Forms are separate from your schematic data. You can change a form without touching your project, and the next time you generate reports, the output will look different — but the underlying engineering data stays the same.

---

## Form File Naming Convention

EPLAN form files use the `.f??` extension where the number indicates the **report type**:

| Extension | Report Type |
|-----------|-------------|
| `.f00` | Title page / Cover sheet |
| `.f01` | Table of contents |
| `.f04` | Cable diagram / Cable overview |
| `.f05` | Summarized parts list |
| `.f06` | Device tag list |
| `.f08` | Structure identifier overview |
| `.f10` | Terminal-strip overview |
| `.f11` | Terminal diagram |
| `.f17` | Connection list |
| `.f22` | PLC diagram |
| `.f30` | P&ID / Piping overview |
| `.f31` | Pre-planning: Pipe class overview |
| `.f32` | Pre-planning: Planning object overview |
| `.f33` | Pre-planning: Loop diagram |
| `.f34` | Pre-planning: Substance overview |

> The number in the extension is fixed by EPLAN — it determines which type of data the form can access. A `.f11` form can only be used for terminal diagrams; it cannot be assigned to a parts list report.

### File Location

```
%APPDATA%\EPLAN\Electric P8\{version}\Forms\
```

Form files are part of the **EPLAN master data**, not the project itself. They can be shared across multiple projects.

---

## Form File Anatomy

A form file is made up of several visual and logical components arranged on a page canvas inside the Form Editor.

```
┌──────────────────────────────────────────────────────┐
│                    FORM PAGE                         │
│  ┌────────────────────────────────────────────────┐  │
│  │              HEADER / TITLE BLOCK              │  │
│  │  Project name | Drawing number | Revision      │  │
│  └────────────────────────────────────────────────┘  │
│  ┌────────────────────────────────────────────────┐  │
│  │                TABLE HEADER ROW                │  │
│  │  Tag | Description | Article No. | Qty         │  │
│  └────────────────────────────────────────────────┘  │
│  ┌────────────────────────────────────────────────┐  │
│  │              ROW TEMPLATE (repeating)          │  │
│  │  %D  |  %T        |  %BN          |  %MC       │  │
│  └────────────────────────────────────────────────┘  │
│  ┌────────────────────────────────────────────────┐  │
│  │                   FOOTER                       │  │
│  │  Page %P of %PT  |  Date %DA  |  Scale         │  │
│  └────────────────────────────────────────────────┘  │
└──────────────────────────────────────────────────────┘
```

### The Four Main Areas

**1. Title Block (Header)**
The border frame around the page containing project metadata. Usually appears at the bottom or right edge of the page. Contains static labels (text you type) and dynamic placeholders (variables that fill in automatically).

**2. Table Header Row**
A static row of column labels — e.g., "Device Tag", "Description", "Article Number". This text is fixed and does not change between projects.

**3. Row Template (Data Row)**
The most important part of a report form. This is the **repeating row** that EPLAN copies once for each data record (each terminal, each cable, each device). It contains **property placeholders** that are replaced with real values when the report is generated.

**4. Footer**
Optional area at the bottom of the page for page numbers, dates, revision marks, and company information.

---

## Form Components in Detail

### Static Text
Plain text labels you type directly onto the form canvas. These never change — they are the same on every generated page.

```
Example:  "Device Tag"   "Description"   "Article No."
```

### Lines and Borders
Graphical elements (horizontal lines, boxes, frames) used to create the table structure and title block border. Drawn using the line tools in the Form Editor.

### Property Placeholders
The dynamic elements of a form. These are special codes written as `%XX` or `<property name>` that EPLAN replaces with real data from the project when generating the report. See the full reference in the next section.

### Special Areas
Defined regions on the form that tell EPLAN where to place the repeating data rows, where the header ends, and where the footer begins. These boundaries are set using **area markers** in the Form Editor.

| Area Marker | Purpose |
|-------------|---------|
| Row area | Defines the repeating data row template |
| Header area | Content above the data rows |
| Footer area | Content below the data rows |
| Title block area | The page border frame |

---

## Property Placeholders (Variables)

Property placeholders are codes embedded in the form that EPLAN replaces with real project or device data during report generation. They are the core of what makes a form dynamic.

### How They Look in the Form Editor

In the Form Editor, placeholders appear as text elements with a special code:

```
%D          →  becomes  →  =GB1+ET1-K1     (device tag)
%T          →  becomes  →  Main contactor  (description)
%P          →  becomes  →  5               (page number)
```

---

## Common Placeholder Reference

### Project-Level Placeholders
These pull data from the **project properties** (same value on every page).

| Placeholder | Property | Example Output |
|-------------|----------|----------------|
| `%PN` | Project name | `EPLAN_Sample_Project_Education` |
| `%CN` | Company name | `Acme Engineering GmbH` |
| `%DA` | Current date | `11.03.2026` |
| `%CR` | Created by | `J. Smith` |
| `%AP` | Approved by | `M. Mueller` |
| `%RE` | Revision | `Rev. 03` |

---

### Page-Level Placeholders
These pull data specific to the **current page**.

| Placeholder | Property | Example Output |
|-------------|----------|----------------|
| `%P` | Current page number | `7` |
| `%PT` | Total page count | `24` |
| `%PD` | Page description | `Terminal diagram X1` |
| `%PP` | Page name / designator | `=GB1+ET1/7` |
| `%SC` | Drawing scale | `1:1` |

---

### Device / Component Placeholders
Used in the **row template** of device lists, parts lists, and tag lists. Repeated once per device.

| Placeholder | Property | Example Output |
|-------------|----------|----------------|
| `%D` | Device tag (full) | `=GB1+ET1-K1` |
| `%T` | Description / function text | `Main contactor 11kW` |
| `%BN` | Article / part number | `3RT2026-1AP00` |
| `%BH` | Manufacturer | `Siemens` |
| `%MC` | Quantity | `5` |
| `%FT` | Device type | `Contactor` |

---

### Terminal Placeholders
Used in terminal diagram and terminal-strip overview forms (`.f10`, `.f11`).

| Placeholder | Property | Example Output |
|-------------|----------|----------------|
| `%TN` | Terminal designation | `X1:5` |
| `%TC` | Terminal type | `CLIPLINE 2.5` |
| `%TT` | Target (connection to) | `=GB1+ET1-K3:14` |
| `%TW` | Wire color | `BK` (Black) |
| `%TCS` | Wire cross-section | `1.5 mm²` |
| `%TCN` | Cable name | `W5` |

---

### Cable Placeholders
Used in cable diagram and cable overview forms (`.f04`).

| Placeholder | Property | Example Output |
|-------------|----------|----------------|
| `%CN` | Cable designation | `W1` |
| `%CT` | Cable type | `NYCWY 3×1.5mm²` |
| `%CL` | Cable length | `15 m` |
| `%CF` | Cable from (source) | `=GB1+ET1-X1:1` |
| `%CTO` | Cable to (destination) | `=GB2+MCC-X2:3` |
| `%CSH` | Shielded | `Yes` |

---

### PLC Placeholders
Used in PLC connection diagram forms (`.f22`).

| Placeholder | Property | Example Output |
|-------------|----------|----------------|
| `%PA` | PLC address | `I0.0` |
| `%PS` | Signal name | `Emergency_Stop_S1` |
| `%PC` | Card designation | `DI 32×24VDC` |
| `%PSL` | Slot number | `2` |
| `%PCH` | Channel number | `0` |

---

## Placeholder Syntax Rules

1. **Case sensitive** — `%D` and `%d` may behave differently depending on context
2. **Must be inside a text element** — placeholders only work when placed as text on the form canvas, not in graphical elements
3. **Row template context** — device/terminal/cable placeholders only work inside the defined row area of the form
4. **Project placeholders** — work anywhere on the form including the title block
5. **Unresolved placeholders** — if a placeholder has no matching data, EPLAN leaves it blank or shows a `?` depending on settings

---

## Simple Example: Parts List Row

A row template in a summarized parts list form (`.f05`) might look like this in the Form Editor:

```
| %D          | %T                  | %BN           | %BH      | %MC  |
```

When EPLAN generates the report, each device becomes one row:

```
| =GB1+ET1-K1 | Main contactor 11kW | 3RT2026-1AP00 | Siemens  |  5   |
| =GB1+ET1-F1 | Motor circuit breaker| 3RV2021-4AA10 | Siemens  |  1   |
| =GB1+ET1-Q1 | Main isolator       | 3LD2203-0TK53 | Siemens  |  1   |
```

---

## How to View and Edit a Form

1. In EPLAN P8, go to **Utilities → Forms → Open**
2. Browse to `%APPDATA%\EPLAN\Electric P8\{version}\Forms\`
3. Select the `.f??` file you want to inspect
4. The **Form Editor** opens — a graphical canvas where you can see all text elements, placeholders, lines, and area markers
5. Double-click any text element to see or edit its placeholder code
6. Save and close, then regenerate reports to see the effect

> ⚠️ Always keep a backup copy of the original form before making changes.

---

## Summary

| Concept | What It Is |
|---------|-----------|
| Form file (`.f??`) | Template that defines a report page layout |
| File extension number | Determines which report type the form belongs to |
| Static text | Fixed labels that never change |
| Property placeholder | `%XX` code replaced with real data on generation |
| Row template | Repeating area — one copy per data record |
| Title block | Page border with project metadata |
| Form Editor | EPLAN tool used to view and modify form files |

---

## Related Files

| File | Description |
|------|-------------|
| `eplan_p8_project_structure.json` | Full metadata for all 16 project report folders |
| `README.md` | General project structure reference |
| `README_Interactive_vs_AutoGenerated.md` | Interactive vs. auto-generated page types |
| `README_Form_Components.md` | This file |

---

*EPLAN Electric P8 — Engineering Reference Documentation*
