---

title: "EPLAN Expert Properties Reference Guide"

description: >-
  A comprehensive reference guide to the most important and most frequently used properties in EPLAN P8, including their IDs, categories, data sources, form usage, output examples, and practical expert tips for effective use in electrical project documentation.
date: 2024-03-10 10:00:00 +0800
author: Mahmoud Lotfi
file_name: 2024-03-10-eplan-expert-properties-1.md
categories: [EPLAN, Properties, Reference]
tags: [Eplan, properties, reference]
pin: False
math: true
mermaid: true
comments: true
toc: true
render_with_liquid: false

image:
  path: /assets/img/posts/eplan.jpg
  alt: EPLAN Expert Properties Explained
  lqip: data:image/webp;base64,UklGRjoAAABXRUJQVlA4IC4AAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
---

# EPLAN Electric P8 — Essential Properties Reference for Experts

> **Software:** EPLAN Electric P8
> **Topic:** Most-used placeholder properties, their IDs, categories, and which forms they appear in
> **Level:** Intermediate / Expert Reference

---

## Overview

This reference documents the most important and most frequently used **properties** in EPLAN P8 — the ones expert engineers rely on when building and customizing forms. Each property entry includes:

- Internal property ID
- Category it belongs to
- What data it outputs
- Which form types (`.f??`) it is used in
- Practical usage notes

---

## How to Read This Document

```
Property Name       The readable name shown in the Placeholder texts browser
ID                  Internal EPLAN property number (e.g., <20001>)
Category            Filter group in the browser
Data Source         Header object (page/project level) or Data object (row level)
Form Used In        Which .f?? form types this property appears in
Output Example      What the generated report actually shows
```

---

## 1. General / Project Properties

These are the most used properties in **title blocks and cover sheets**. They pull data from the project properties dialog and are placed in the `Header object` context.

| Property Name | ID | Category | Data Source | Output Example | Form Used In |
|---------------|----|----------|-------------|----------------|--------------|
| Project name | `<10011>` | General | Header object | `EPLAN_Sample_Project_Education` | `.f00` `.f01` `.f10` `.f11` `.f05` |
| Creator | `<10081>` | General | Header object | `J. Smith` | `.f00` `.f01` |
| Creation date | `<10091>` | General | Header object | `01.03.2026` | `.f00` `.f01` |
| Last editor | `<10082>` | Editing | Header object | `M. Mueller` | `.f00` `.f01` |
| Modification date | `<10092>` | Editing | Header object | `11.03.2026` | `.f00` `.f01` |
| Approved by | `<10083>` | General | Header object | `T. Bauer` | `.f00` |
| Approval date | `<10093>` | General | Header object | `12.03.2026` | `.f00` |
| Customer | `<10021>` | Customer | Header object | `Acme Industries GmbH` | `.f00` `.f01` |
| Order number | `<10031>` | General | Header object | `PO-2026-0042` | `.f00` |
| Project description | `<10013>` | General | Header object | `Main control panel MCC-01` | `.f00` `.f01` |
| Revision index | `<10151>` | General | Header object | `Rev. 03` | `.f00` `.f01` |
| Drawing number | `<10141>` | General | Header object | `E-2026-001` | `.f00` |

> **Where to set these values:** Project properties dialog → `Project data` → `General` tab.
> Changes here automatically update all title blocks on every page.

---

## 2. Page Properties

Used inside **table of contents**, **title blocks**, and any form that needs page-level metadata.

| Property Name | ID | Category | Data Source | Output Example | Form Used In |
|---------------|----|----------|-------------|----------------|--------------|
| Page name | `<11001>` | General | Header object | `=GB1+ET1/7` | `.f01` `.f00` |
| Page description | `<11011>` | General | Header object | `Terminal diagram X1` | `.f01` `.f00` |
| Page number | `<11021>` | General | Header object | `7` | `.f00` `.f01` `.f10` `.f11` |
| Total page count | `<11031>` | General | Header object | `24` | `.f00` `.f01` |
| Page type | `<11051>` | General | Header object | `Circuit diagram` | `.f01` |
| Higher-level assignment | `<11061>` | General | Header object | `=GB1` | `.f01` `.f00` |
| Installation location | `<11071>` | General | Header object | `+ET1` | `.f01` `.f00` |
| Scale | `<11081>` | General | Header object | `1:1` | `.f00` |

---

## 3. Device / Function Properties

The most critical properties for **device tag lists**, **parts lists**, and **circuit documentation**. Always used in the `Data object` context inside the row template.

| Property Name | ID | Category | Data Source | Output Example | Form Used In |
|---------------|----|----------|-------------|----------------|--------------|
| Device tag (full) | `<20001>` | Devices | Data object | `=GB1+ET1-K1` | `.f06` `.f05` `.f01` |
| Function text | `<20011>` | Devices | Data object | `Main contactor 11kW` | `.f06` `.f05` `.f11` `.f10` |
| Function definition | `<20021>` | Function data | Data object | `Contactor, normally open` | `.f06` |
| Higher-level assignment | `<20031>` | Devices | Data object | `=GB1` | `.f06` `.f05` |
| Installation location | `<20041>` | Devices | Data object | `+ET1` | `.f06` `.f05` `.f10` |
| Device tag (short) | `<20051>` | Devices | Data object | `-K1` | `.f06` `.f11` `.f10` |
| Cross-reference | `<20061>` | Devices | Data object | `Page 5 / Col. 3` | `.f06` |
| Type designation | `<20071>` | Devices | Data object | `3RT2026` | `.f06` `.f05` |
| Supplementary field 1 | `<20901>` | Data | Data object | `Free custom text` | `.f06` `.f05` |

---

## 4. Parts / BOM Properties

Essential for **summarized parts lists** and **device tag lists**. These read from the parts management database.

| Property Name | ID | Category | Data Source | Output Example | Form Used In |
|---------------|----|----------|-------------|----------------|--------------|
| Part number (article) | `<20601>` | Parts | Data object | `3RT2026-1AP00` | `.f05` `.f06` |
| Manufacturer | `<20611>` | Parts | Data object | `Siemens` | `.f05` `.f06` |
| Order number | `<20621>` | Parts | Data object | `3RT2026-1AP00` | `.f05` |
| Description 1 | `<20631>` | Parts | Data object | `Contactor 11kW 230VAC` | `.f05` `.f06` |
| Description 2 | `<20632>` | Parts | Data object | `3-pole, screw terminals` | `.f05` `.f06` |
| Quantity (count) | `<20801>` | Parts | Data object | `5` | `.f05` `.f06` |
| Unit | `<20811>` | Parts | Data object | `pcs` | `.f05` |
| Price (unit) | `<20821>` | Prices | Data object | `45.00 €` | `.f05` |
| Price (total) | `<20831>` | Prices | Data object | `225.00 €` | `.f05` |
| EAN / barcode | `<20641>` | Parts | Data object | `4011209262856` | `.f05` |
| Mounting location | `<20651>` | Mounting data | Data object | `DIN rail, slot 4` | `.f05` `.f06` |
| Supplementary field: Text | `<20501>` | Parts | Data object | `Free additional field` | `.f05` `.f06` |

> **Expert tip:** Use `Description 1` + `Description 2` together in BOM forms — Description 1 for the short type name, Description 2 for variant/option details.

---

## 5. Terminal Properties

Used exclusively in **terminal-strip overview** (`.f10`) and **terminal diagram** (`.f11`) forms.

| Property Name | ID | Category | Data Source | Output Example | Form Used In |
|---------------|----|----------|-------------|----------------|--------------|
| Terminal designation | `<31001>` | Connection | Data object | `X1:5` | `.f10` `.f11` |
| Terminal strip name | `<31011>` | Connection | Data object | `X1` | `.f10` `.f11` |
| Terminal number | `<31021>` | Connection | Data object | `5` | `.f10` `.f11` |
| Connection designation (internal) | `<31031>` | Connection | Data object | `=GB1+ET1-K3:14` | `.f11` |
| Connection designation (external) | `<31041>` | Connection | Data object | `=GB1+FIELD-Y1:A1` | `.f11` |
| Wire color | `<31051>` | Connection | Data object | `BK` (Black) | `.f10` `.f11` |
| Wire cross-section | `<31061>` | Connection | Data object | `1.5 mm²` | `.f10` `.f11` |
| Potential / signal name | `<31071>` | Connection | Data object | `L1` | `.f10` `.f11` |
| Terminal type | `<31081>` | Parts | Data object | `CLIPLINE 2.5 BU` | `.f10` |
| Jumper / bridge group | `<31091>` | Connection | Data object | `Bridge group 1` | `.f10` |
| Cable name (external) | `<31101>` | Cable data | Data object | `W5` | `.f11` |
| Conductor number | `<31111>` | Cable data | Data object | `3` | `.f11` |
| Connection direction | `<31121>` | Connection | Data object | `Incoming / Outgoing` | `.f11` |

> **Expert tip:** In `.f11` always use both `Connection designation (internal)` and `Connection designation (external)` side by side — this gives technicians the full from/to picture on a single row without needing to read the schematic.

---

## 6. Cable Properties

Used in **cable diagram** and **cable overview** forms (`.f04`).

| Property Name | ID | Category | Data Source | Output Example | Form Used In |
|---------------|----|----------|-------------|----------------|--------------|
| Cable designation | `<32001>` | Cable data | Data object | `W1` | `.f04` |
| Cable type | `<32011>` | Cable data | Data object | `NYCWY 3×1.5mm²` | `.f04` |
| Cable length (manual) | `<32021>` | Cable data | Data object | `15 m` | `.f04` |
| Cable length (routed) | `<32031>` | Cable data | Data object | `16.2 m` | `.f04` |
| Cable from (source terminal) | `<32041>` | Cable data | Data object | `=GB1+ET1-X1:1` | `.f04` |
| Cable to (destination terminal) | `<32051>` | Cable data | Data object | `=GB2+MCC-X2:3` | `.f04` |
| Number of conductors | `<32061>` | Cable data | Data object | `3` | `.f04` |
| Cross-section | `<32071>` | Cable data | Data object | `1.5 mm²` | `.f04` |
| Voltage level | `<32081>` | Cable data | Data object | `0.6/1 kV` | `.f04` |
| Shielded | `<32091>` | Cable data | Data object | `Yes` | `.f04` |
| Cable jacket color | `<32101>` | Cable data | Data object | `Black` | `.f04` |
| Cable outer diameter | `<32111>` | Cable data | Data object | `12.4 mm` | `.f04` |
| Cable reel | `<32121>` | Cable data | Data object | `Reel-07` | `.f04` |
| ATEX identifier | `<32131>` | Certification | Data object | `Ex e IIC T4` | `.f04` |

> **Expert tip:** Always include both `Cable length (manual)` and `Cable length (routed)` on cable overview forms — the difference between the two flags discrepancies between planned and actual routed lengths.

---

## 7. PLC Properties

Used in **PLC connection diagram** forms (`.f22`).

| Property Name | ID | Category | Data Source | Output Example | Form Used In |
|---------------|----|----------|-------------|----------------|--------------|
| PLC address | `<40001>` | PLC data | Data object | `I0.0` | `.f22` |
| Signal name | `<40011>` | PLC data | Data object | `Emergency_Stop_S1` | `.f22` |
| I/O type | `<40021>` | PLC data | Data object | `DI` (Digital Input) | `.f22` |
| Card designation | `<40031>` | PLC data | Data object | `DI 32×24VDC` | `.f22` |
| Slot number | `<40041>` | PLC data | Data object | `2` | `.f22` |
| Channel number | `<40051>` | PLC data | Data object | `0` | `.f22` |
| CPU designation | `<40061>` | PLC data | Data object | `CPU 1516-3 PN/DP` | `.f22` |
| Rack number | `<40071>` | PLC data | Data object | `0` | `.f22` |
| Bus address | `<40081>` | PLC data | Data object | `3` | `.f22` |
| Symbolic address | `<40091>` | PLC data | Data object | `"E_Stop_S1"` | `.f22` |
| Data type | `<40101>` | PLC data | Data object | `BOOL` | `.f22` |
| Comment | `<40111>` | PLC data | Data object | `NC contact, hardwired safety` | `.f22` |

---

## 8. Pre-planning Properties

Used in **pre-planning loop diagrams** and **PCT overview** forms (`.f31`–`.f34`).

| Property Name | ID | Category | Data Source | Output Example | Form Used In |
|---------------|----|----------|-------------|----------------|--------------|
| Planning object designation | `<50001>` | Pre-planning 1 | Data object | `TIC-101` | `.f32` `.f33` |
| Planning object description | `<50011>` | Pre-planning 1 | Data object | `Temperature control loop` | `.f32` `.f33` |
| Loop number | `<50021>` | Pre-planning 1 | Data object | `Loop-042` | `.f33` |
| Instrument tag | `<50031>` | Pre-planning 1 | Data object | `TT-101` | `.f33` |
| Pipe class | `<50041>` | Pre-planning 2 | Data object | `A1B` | `.f31` |
| Substance / medium | `<50051>` | Pre-planning 3 | Data object | `Natural Gas` | `.f34` |
| Operating pressure | `<50061>` | Pre-planning 3 | Data object | `10 bar` | `.f34` |
| Operating temperature | `<50071>` | Pre-planning 3 | Data object | `+50°C` | `.f34` |
| ATEX zone | `<50081>` | Pre-planning 3 | Data object | `Zone 1` | `.f34` |
| Signal type | `<50091>` | Pre-planning 1 | Data object | `4–20 mA HART` | `.f33` |

---

## 9. Structure Identifier Properties

Used in **structure identifier overview** (`.f08`) and **table of contents** (`.f01`).

| Property Name | ID | Category | Data Source | Output Example | Form Used In |
|---------------|----|----------|-------------|----------------|--------------|
| Full device tag | `<20001>` | Devices | Data object | `=GB1+ET1-K1` | `.f08` `.f01` |
| Higher-level assignment (=) | `<20031>` | Devices | Data object | `=GB1` | `.f08` `.f01` |
| Installation location (+) | `<20041>` | Devices | Data object | `+ET1` | `.f08` `.f01` |
| Mounting location description | `<20042>` | Devices | Data object | `Control cabinet 1` | `.f08` |
| Function assignment description | `<20032>` | Devices | Data object | `Drive system` | `.f08` |

---

## Form ↔ Property Mapping Summary

Quick reference — which forms use which property groups most heavily:

| Form | Extension | Primary Property Categories |
|------|-----------|----------------------------|
| Title page / Cover sheet | `.f00` | General, Customer, Editing, General (page) |
| Table of contents | `.f01` | General (page), Devices |
| Cable diagram / overview | `.f04` | Cable data, Certification |
| Summarized parts list | `.f05` | Parts, Prices, Mounting data |
| Device tag list | `.f06` | Devices, Parts, Function data |
| Structure identifier overview | `.f08` | Devices, General |
| Terminal-strip overview | `.f10` | Connection, Parts |
| Terminal diagram | `.f11` | Connection, Cable data |
| Connection list | `.f17` | Connection, Cable data, Devices |
| PLC diagram | `.f22` | PLC data |
| P&ID piping overview | `.f30` | Function data, Pre-planning 1 |
| Pre-planning: Pipe class | `.f31` | Pre-planning 2 |
| Pre-planning: Planning object | `.f32` | Pre-planning 1 |
| Pre-planning: Loop diagram | `.f33` | Pre-planning 1, Connection |
| Pre-planning: Substance | `.f34` | Pre-planning 3 |

---

## Expert Tips Summary

| Tip | Detail |
|-----|--------|
| Always show both description lines | Use `Description 1` + `Description 2` together in parts lists for full part clarity |
| Manual vs routed cable length | Include both `<32021>` and `<32031>` to catch routing discrepancies |
| Internal + external connection | Show both `<31031>` and `<31041>` on terminal diagrams for complete wiring info |
| Use property IDs in scripts | When scripting or using the EPLAN API, always reference properties by their numeric ID, not name — names can vary by language setting |
| Supplementary fields for custom data | Use `<20501>`–`<20510>` (Supplementary field 1–10) for project-specific data not covered by standard properties |
| Symbolic PLC addresses | Add `<40091>` (Symbolic address) alongside `<40001>` (PLC address) — required for TIA Portal / STEP 7 integration |
| Replace identical text | Enable this option on `Higher-level assignment` and `Installation location` columns to suppress repeated values and improve readability |

---

## Property ID Quick Lookup

| ID Range | Category |
|----------|----------|
| `10001`–`10999` | Project and page general properties |
| `11001`–`11999` | Page-specific properties |
| `20001`–`20099` | Device / function properties |
| `20501`–`20599` | Supplementary / free fields |
| `20601`–`20699` | Parts management — article data |
| `20801`–`20899` | Quantity and unit |
| `20821`–`20899` | Pricing |
| `31001`–`31999` | Terminal and connection properties |
| `32001`–`32999` | Cable properties |
| `40001`–`40999` | PLC data |
| `50001`–`59999` | Pre-planning properties (levels 1–8) |

---

## Related Files

| File | Description |
|------|-------------|
| `eplan_p8_project_structure.json` | Full metadata for all 16 project report folders |
| `README.md` | General project structure reference |
| `README_Interactive_vs_AutoGenerated.md` | Interactive vs. auto-generated page types |
| `README_Form_Components.md` | Form file anatomy and placeholder syntax overview |
| `README_Placeholder_Properties.md` | Placeholder text dialog — elements and categories |
| `README_Expert_Properties.md` | This file — expert property reference with form mapping |

---

*EPLAN Electric P8 — Engineering Reference Documentation*
