# EPLAN Electric P8 2026 — Complete Property Categories & Most-Used Properties Reference

> **Software:** EPLAN Electric P8 / Eplan Platform 2026
> **Topic:** All placeholder property categories, most-used expert properties, and which forms they appear in
> **Level:** Intermediate — Expert Reference
> **Note:** EPLAN Platform 2026 introduced 400+ new properties. Categories marked 🆕 are new or significantly expanded in v2026.

---

## Overview

The **Placeholder texts browser** in the Form Editor groups all available properties into **categories**. Selecting a category filters the property list so you can quickly locate what you need. This document covers:

1. Every category available in EPLAN Platform 2026
2. What each category contains
3. The most commonly used properties per category
4. Which form types (`.f??`) each property is used in
5. When and why experts use each property

---

## Full Category List — EPLAN Platform 2026

```
All categories
├── Archive data
├── Cable data
├── Category
├── Certification
├── Connection
├── Customer
├── Data
├── Data for reports
├── Devices
├── Documents
├── Editing
├── End customer
├── Formats
├── Function data
├── General
├── Macro
├── Messages
├── Mounting data
├── Parts
├── PLC data
├── Pre-planning 1
├── Pre-planning 2
├── Pre-planning 3
├── Pre-planning 4
├── Pre-planning 5
├── Pre-planning 6
├── Pre-planning 7
├── Pre-planning 8
├── Prices
├── Pro Panel                    🆕 expanded in 2026
├── Revision                     🆕 enhanced in 2026
├── Safety                       🆕 new in 2026
├── Supplementary fields
├── Topology                     🆕 new in 2026
└── Wiring                       🆕 new in 2026
```

---

## Category Reference with Most-Used Properties

---

### 1. All Categories
**What it is:** Unfiltered view — shows every property from all categories in one list.

**When to use:** When you don't know which category a property belongs to, or when searching by keyword using the search box.

**Expert tip:** Never browse "All categories" without the search box — the list contains thousands of properties in EPLAN 2026.

---

### 2. Archive Data

**What it contains:** Document archiving metadata — DMS references, document numbers, archive status, storage locations.

**When to use:** Projects that integrate with a Document Management System (DMS) or require formal document control registration.

| Property | ID | Description | Used in Form |
|----------|----|-------------|-------------|
| Document number | `<10141>` | Formal drawing/document number | `.f00` `.f01` |
| Archive status | `<10161>` | DMS status (draft, released, archived) | `.f00` |
| Storage location | `<10171>` | DMS path or cabinet reference | `.f00` |
| External document number | `<10181>` | Client's own document reference number | `.f00` |

---

### 3. Cable Data ⭐ Most Used

**What it contains:** All properties related to cables — physical dimensions, electrical ratings, routing, shielding, reel data.

**When to use:** Cable diagram (`.f04`) and cable overview forms. Also used in connection lists where cable identity is needed.

| Property | ID | Description | Used in Form | Expert Usage |
|----------|----|-------------|-------------|-------------|
| Cable designation | `<32001>` | Cable ID (W1, W2…) | `.f04` `.f17` | Always the first column in cable tables |
| Cable type | `<32011>` | Cable type string (NYCWY 3×1.5mm²) | `.f04` | Procurement and installation reference |
| Cable length, max. | `<32021>` | Planned/manual length | `.f04` | Specified by engineer during design |
| Cable length, routed | `<32031>` | Actual routed length from routing engine | `.f04` | Compare with manual length for accuracy check |
| Cable: Cross-section | `<32071>` | Conductor cross-section (mm²) | `.f04` `.f17` | Used in procurement and voltage drop calc |
| Cable: Voltage level | `<32081>` | Rated voltage (e.g. 0.6/1 kV) | `.f04` | Safety and compliance documentation |
| Cable jacket: Color | `<32101>` | Outer jacket color | `.f04` | Cable identification on site |
| Cable outer diameter | `<32111>` | OD in mm | `.f04` | Cable gland and conduit sizing |
| Cables included | `<32061>` | Number of conductors | `.f04` | Harness / bundle documentation |
| Cable reel | `<32121>` | Reel/drum reference number | `.f04` | Warehouse and logistics |
| Shielded | `<32091>` | Yes/No shielding flag | `.f04` | Use with conditional area for ATEX/EMC notes |
| Blower available | `<32201>` | Forced cooling flag | `.f04` | High-power cable documentation |
| CO2 emission | `<32211>` | Environmental data | `.f04` | Sustainability reporting |
| Cable entry available | `<32221>` | Cable entry fitting assigned | `.f04` | Panel builder reference |
| ATEX identifier | `<32131>` | Explosion protection class | `.f04` | Hazardous area projects |

---

### 4. Category

**What it contains:** Device classification codes — ECLASS, product group, device category assignments from parts management.

**When to use:** BOM reports where classification codes (ECLASS) are required for ERP/SAP integration or procurement systems.

| Property | ID | Description | Used in Form |
|----------|----|-------------|-------------|
| Product group | `<20701>` | Product group from parts management | `.f05` `.f06` |
| ECLASS | `<20711>` | ECLASS code for ERP integration | `.f05` |
| Category (device) | `<20721>` | Internal EPLAN device category | `.f06` |

---

### 5. Certification ⭐ Commonly Used

**What it contains:** Compliance and certification data — ATEX, CE, VDE, UL, RoHS, REACH.

**When to use:** Projects with regulatory compliance requirements — hazardous areas, export to North America (UL), European CE marking.

| Property | ID | Description | Used in Form | Expert Usage |
|----------|----|-------------|-------------|-------------|
| Certification: ATEX identifier | `<20751>` | ATEX explosion protection class | `.f05` `.f06` | Mandatory for Zone 0/1/2 projects |
| Certification: CE | `<20761>` | CE conformity flag | `.f05` | EU machine directive compliance |
| Certification: VDE | `<20771>` | VDE standard compliance | `.f05` | German market projects |
| Certification: UL Category Control Number | `<20781>` | UL category listing number | `.f05` | North American projects |
| Certification: UL File Number | `<20791>` | UL file reference | `.f05` | North American projects |
| Certification: General | `<20741>` | Free text certification notes | `.f05` `.f06` | Custom compliance notes |

---

### 6. Connection ⭐ Most Used

**What it contains:** All wire and conductor properties — color, cross-section, potential, signal name, terminal references, topology routing.

**When to use:** Terminal diagrams (`.f11`), terminal-strip overviews (`.f10`), and connection lists (`.f17`). The most important category for wiring documentation.

| Property | ID | Description | Used in Form | Expert Usage |
|----------|----|-------------|-------------|-------------|
| Terminal designation | `<31001>` | Full terminal ID (X1:5) | `.f10` `.f11` | Primary key for all terminal tables |
| Terminal strip name | `<31011>` | Strip ID only (X1) | `.f10` `.f11` | Group headers in terminal forms |
| Terminal number | `<31021>` | Pin number only (5) | `.f10` `.f11` | Sequential ordering |
| Connection (internal) | `<31031>` | Source device:pin inside panel | `.f11` `.f17` | Full from-path for wiring |
| Connection (external) | `<31041>` | Destination device:pin outside panel | `.f11` `.f17` | Full to-path for wiring |
| Wire color | `<31051>` | Conductor color (BK, BU, RD…) | `.f10` `.f11` `.f17` | IEC 60757 color coding |
| Wire cross-section | `<31061>` | Cross-section in mm² | `.f10` `.f11` `.f17` | Safety and current rating |
| Potential / signal name | `<31071>` | Electrical potential (L1, 24VDC, GND) | `.f10` `.f11` `.f17` | Grouping by potential |
| Cable name (external) | `<31101>` | Cable identifier for external connection | `.f11` `.f17` | Links terminal to cable drawing |
| Conductor number | `<31111>` | Core/conductor number within cable | `.f11` | Termination reference |
| Connection direction | `<31121>` | Incoming or outgoing | `.f11` | Junction box wiring clarity |
| Jumper / bridge group | `<31091>` | Bridge group designation | `.f10` | Multi-wire bridges in terminal strips |
| Terminal type | `<31081>` | Article type of terminal | `.f10` | Panel builder parts reference |
| Topology: Routing track | `<31119>` 🆕 | Routing path specification | `.f17` `.f11` | Cable routing in EPLAN topology module |

---

### 7. Customer

**What it contains:** Customer-specific project fields — name, address, contact, project reference on customer side.

**When to use:** Title blocks and cover sheets that need customer identification data.

| Property | ID | Description | Used in Form |
|----------|----|-------------|-------------|
| Customer name | `<10021>` | Customer / client name | `.f00` `.f01` |
| Customer address | `<10022>` | Customer postal address | `.f00` |
| Customer contact | `<10023>` | Customer contact person | `.f00` |
| Customer order number | `<10031>` | Customer's own PO number | `.f00` |
| Customer project number | `<10032>` | Customer's internal project number | `.f00` |

---

### 8. Data

**What it contains:** General data fields that don't belong to a specific engineering category — free text fields, supplementary data, custom project fields.

**When to use:** When standard properties don't cover a specific data requirement. Common for custom fields in project templates.

| Property | ID | Description | Used in Form |
|----------|----|-------------|-------------|
| Supplementary field 1–10 | `<20901>`–`<20910>` | Free custom text fields | `.f05` `.f06` `.f11` |
| Project supplementary 1–5 | `<10901>`–`<10905>` | Free project-level custom fields | `.f00` `.f01` |

---

### 9. Data for Reports ⭐ Expert Category

**What it contains:** Properties specifically designed for use in generated reports — calculated values, formatted outputs, report-specific fields that are not used in schematics.

**When to use:** Advanced form design where calculated or formatted values are needed that differ from raw schematic properties.

| Property | ID | Description | Used in Form | Expert Usage |
|----------|----|-------------|-------------|-------------|
| Page count (report) | `<11031>` | Dynamically calculated total pages | `.f00` `.f01` | "Page X of Y" in title blocks |
| Item number | `<20851>` | Auto-incremented row number in report | `.f05` `.f06` | Sequential BOM numbering |
| Continuation text | `<11091>` | "Continued on next page" text | `.f01` `.f10` | Multi-page table management |
| Column header repeat | `<11101>` | Repeat column headers on each page | `.f05` `.f10` | Long multi-page reports |

---

### 10. Devices ⭐ Most Used

**What it contains:** Core device and component identification properties — the device tag system, function texts, cross-references.

**When to use:** Device tag lists (`.f06`), parts lists (`.f05`), table of contents (`.f01`), and any report that identifies individual devices.

| Property | ID | Description | Used in Form | Expert Usage |
|----------|----|-------------|-------------|-------------|
| Device tag (full) | `<20001>` | Complete tag: =GB1+ET1-K1 | `.f05` `.f06` `.f01` | Primary device identifier in all reports |
| Function text | `<20011>` | Device description text | `.f05` `.f06` `.f11` | What the device does |
| Higher-level assignment (=) | `<20031>` | Functional assignment block | `.f05` `.f06` `.f08` | Grouping and filtering in reports |
| Installation location (+) | `<20041>` | Physical location block | `.f05` `.f06` `.f10` | Cabinet/panel identification |
| Device tag (short) | `<20051>` | Short tag: -K1 | `.f06` `.f11` `.f10` | Space-saving in narrow columns |
| Cross-reference | `<20061>` | Page/column reference to schematic | `.f06` | Navigation back to source page |
| Type designation | `<20071>` | Device type code | `.f06` `.f05` | Technical type identification |
| Function definition | `<20021>` | IEC function definition | `.f06` | Standard function classification |
| Mounting location desc. | `<20042>` | Text description of location | `.f08` `.f06` | Human-readable location |
| Function assignment desc. | `<20032>` | Text description of function | `.f08` | Human-readable function |

---

### 11. Documents

**What it contains:** References to documents linked to devices or parts — datasheets, instruction manuals, CAD files, 3D models.

**When to use:** When output documentation should include hyperlinks or references to manufacturer datasheets or project documents.

| Property | ID | Description | Used in Form |
|----------|----|-------------|-------------|
| Document: Datasheet | `<20971>` | URL or path to datasheet | `.f05` `.f06` |
| Document: Manual | `<20972>` | URL or path to instruction manual | `.f05` |
| Document: 3D model | `<20973>` | Path to 3D model file | `.f05` |
| Document: Certification doc | `<20974>` | Path to certification document | `.f05` |

---

### 12. Editing

**What it contains:** Metadata about who created, modified, or approved data and when — audit trail properties.

**When to use:** Title blocks requiring creator/modifier information and formal revision control.

| Property | ID | Description | Used in Form | Expert Usage |
|----------|----|-------------|-------------|-------------|
| Created by | `<10081>` | Username who created the project | `.f00` `.f01` | Standard title block field |
| Creation date | `<10091>` | Date project was first created | `.f00` `.f01` | Formal document date |
| Last editor | `<10082>` | Username of last person to edit | `.f00` | Revision tracking |
| Modification date | `<10092>` | Date of last modification | `.f00` | Revision tracking |
| Approved by | `<10083>` | Approval authority name | `.f00` | Formal sign-off in title block |
| Approval date | `<10093>` | Date of formal approval | `.f00` | Document release control |

---

### 13. End Customer

**What it contains:** End-customer specific fields, separate from the direct customer (integrator/OEM distinction).

**When to use:** Projects delivered by a systems integrator to a final end client — two levels of customer data needed.

| Property | ID | Description | Used in Form |
|----------|----|-------------|-------------|
| End customer name | `<10041>` | Final end-user/operator name | `.f00` |
| End customer project no. | `<10042>` | End customer internal reference | `.f00` |
| End customer address | `<10043>` | End customer site address | `.f00` |
| Plant / site name | `<10044>` | Name of installation site/plant | `.f00` `.f01` |

---

### 14. Formats

**What it contains:** Number and date formatting settings, unit systems, decimal separators, display format rules.

**When to use:** When properties need to be displayed in a specific format — e.g. dates as DD.MM.YYYY vs MM/DD/YYYY, numbers with/without units.

| Property | ID | Description | Used in Form |
|----------|----|-------------|-------------|
| Date format | `<18001>` | Date display format setting | `.f00` `.f01` |
| Decimal separator | `<18002>` | Period vs comma for decimals | `.f05` |
| Unit system | `<18003>` | Metric / Imperial switch | `.f04` `.f05` |

---

### 15. Function Data

**What it contains:** IEC function classification data — function definitions, function codes, subfunctions, hierarchical function structures.

**When to use:** P&ID forms, device tag lists, and any report requiring IEC 81346-based function classification.

| Property | ID | Description | Used in Form | Expert Usage |
|----------|----|-------------|-------------|-------------|
| Function definition | `<20021>` | IEC function category | `.f06` `.f30` | Standardized device classification |
| Function code | `<20022>` | IEC function short code | `.f06` | Compact classification in tables |
| Subfunction | `<20023>` | Sub-level function definition | `.f06` | Detailed IEC hierarchy |
| Symbol description | `<20024>` | Description of schematic symbol | `.f06` | Symbol library reference |

---

### 16. General ⭐ Most Used

**What it contains:** Core project and page metadata — the most fundamental properties used in every title block.

**When to use:** Header area of every form type. These are the baseline properties every form needs.

| Property | ID | Description | Used in Form | Expert Usage |
|----------|----|-------------|-------------|-------------|
| Project name | `<10011>` | Full project name | `.f00` `.f01` all | Always in title block |
| Project description | `<10013>` | Short project description | `.f00` `.f01` | Subtitle in cover sheet |
| Order number | `<10031>` | Internal order/job number | `.f00` | Project tracking |
| Revision index | `<10151>` | Current revision (Rev.03) | `.f00` `.f01` `.f02` | Version control |
| Drawing number | `<10141>` | Formal drawing number | `.f00` | Document control |
| Page name | `<11001>` | Full page designator | `.f01` `.f00` | TOC and navigation |
| Page description | `<11011>` | Human-readable page description | `.f01` `.f00` | TOC content |
| Page number | `<11021>` | Current page number | `.f00` `.f01` all | "Page X" in footer |
| Total page count | `<11031>` | Total pages in report set | `.f00` `.f01` | "of Y" in footer |
| Higher-level assignment | `<11061>` | Page-level = structure | `.f01` | TOC grouping |
| Installation location (page) | `<11071>` | Page-level + structure | `.f01` | TOC grouping |
| Scale | `<11081>` | Drawing scale | `.f00` | Standard title block field |
| Page type | `<11051>` | Page type string | `.f01` | TOC type column |

---

### 17. Macro

**What it contains:** Properties related to window macros and schematic macros — macro name, variant, description, application.

**When to use:** Forms that document macro usage in the project — macro overviews, template documentation.

| Property | ID | Description | Used in Form |
|----------|----|-------------|-------------|
| Macro name | `<21001>` | Name of the macro | `.f06` |
| Macro variant | `<21002>` | Variant letter/number | `.f06` |
| Macro description | `<21003>` | Description of macro function | `.f06` |
| Schematic macro path | `<21004>` | File path of macro | `.f06` |

---

### 18. Messages

**What it contains:** Check run validation message data — error codes, message classes, affected objects, status flags.

**When to use:** Internal quality reports and check run result forms. Rarely used in standard project documentation.

| Property | ID | Description | Used in Form |
|----------|----|-------------|-------------|
| Message class | `<25001>` | EPLAN check run class number | Internal |
| Message text | `<25002>` | Human-readable error description | Internal |
| Message status | `<25003>` | Open / resolved / ignored | Internal |

---

### 19. Mounting Data ⭐ Commonly Used

**What it contains:** Physical mounting and installation properties — mounting location, rail position, height in cabinet, DIN rail data.

**When to use:** Pro Panel 3D layout reports, device tag lists with physical location data, and assembly documentation.

| Property | ID | Description | Used in Form | Expert Usage |
|----------|----|-------------|-------------|-------------|
| Mounting location | `<20651>` | Where device is physically mounted | `.f05` `.f06` | Cross-reference to cabinet layout |
| Mounting position | `<20652>` | Slot/rail position number | `.f05` `.f06` | Assembly sequence |
| Clip-on height | `<20653>` | Height of clip-on component (mm) | `.f05` | Space planning |
| DIN rail name | `<20654>` | Name of mounting rail | `.f05` `.f06` | Cabinet assembly reference |
| Mounting panel | `<20655>` | Mounting panel designation | `.f05` `.f06` | Links to Pro Panel layout |
| Installation space | `<20656>` | Cabinet/enclosure reference | `.f05` `.f06` | Physical cabinet identification |

---

### 20. Parts ⭐ Most Used

**What it contains:** Parts management data — the article database fields for BOM generation and procurement.

**When to use:** Summarized parts list (`.f05`), device tag list (`.f06`). The most critical category for procurement output.

| Property | ID | Description | Used in Form | Expert Usage |
|----------|----|-------------|-------------|-------------|
| Part number (article) | `<20601>` | Manufacturer part/article number | `.f05` `.f06` | Primary BOM identifier |
| Manufacturer | `<20611>` | Manufacturer name | `.f05` `.f06` | Procurement contact |
| Order number | `<20621>` | Ordering/catalog number | `.f05` | Purchasing reference |
| Description 1 | `<20631>` | Short description line 1 | `.f05` `.f06` | Main BOM description |
| Description 2 | `<20632>` | Detail description line 2 | `.f05` `.f06` | Variant/option detail |
| Quantity | `<20801>` | Total count of identical parts | `.f05` | Core BOM column |
| Unit | `<20811>` | Unit of measure (pcs, m, kg) | `.f05` | BOM unit column |
| EAN / barcode | `<20641>` | European Article Number | `.f05` | Warehouse scanning |
| Supplier | `<20612>` | Preferred supplier name | `.f05` | Procurement workflow |
| Supplier part number | `<20613>` | Supplier catalog number | `.f05` | Alternative ordering reference |
| Supplementary field: Text | `<20501>` | Free additional text field | `.f05` `.f06` | Custom BOM field |
| Weight | `<20661>` | Part weight (kg) | `.f05` | Shipping/logistics |
| Technical characteristics | `<20671>` | Free tech spec text | `.f05` `.f06` | Detailed spec in BOM |

---

### 21. PLC Data ⭐ Most Used

**What it contains:** All PLC hardware and software assignment properties — addresses, signal names, card data, CPU assignments, symbolic names.

**When to use:** PLC connection diagrams (`.f22`) exclusively. Also referenced in connection lists for signal documentation.

| Property | ID | Description | Used in Form | Expert Usage |
|----------|----|-------------|-------------|-------------|
| PLC address | `<40001>` | Hardware address (I0.0, Q1.3) | `.f22` `.f17` | Primary PLC identifier |
| Signal name | `<40011>` | Process signal name | `.f22` `.f17` | Control narrative reference |
| I/O type | `<40021>` | DI / DO / AI / AO | `.f22` | Signal type column |
| Card designation | `<40031>` | I/O card type string | `.f22` | Hardware configuration |
| Slot number | `<40041>` | Rack slot number | `.f22` | Hardware config reference |
| Channel number | `<40051>` | Channel on card | `.f22` | Wiring pin reference |
| CPU designation | `<40061>` | CPU type/name | `.f22` | System identification |
| Rack number | `<40071>` | Rack/chassis number | `.f22` | Multi-rack systems |
| Symbolic address | `<40091>` | TIA Portal / STEP 7 tag | `.f22` | PLC programming reference |
| Data type | `<40101>` | BOOL, INT, REAL, WORD… | `.f22` | Programming data type |
| Comment | `<40111>` | Engineer's note on signal | `.f22` | Context for programmer |
| Bus address | `<40081>` | PROFIBUS/PROFINET address | `.f22` | Network configuration |
| UDT name | `<40121>` 🆕 | User Defined Type name for TIA | `.f22` | Advanced TIA Portal export |
| Assignment list | `<40131>` 🆕 | Tag table name for export | `.f22` | TIA Portal TagTable export |

---

### 22. Pre-planning 1 — 8

**What it contains:** Eight levels of pre-planning properties supporting top-down engineering in EPLAN Preplanning. Each level corresponds to a planning hierarchy tier.

**When to use:** Process automation projects using EPLAN Preplanning module — loop diagrams, PCT objects, substance documentation, pipe classes.

| Level | Typical Use | Key Forms |
|-------|-------------|-----------|
| Pre-planning 1 | PCT loops, instrument tags, signal types | `.f33` `.f32` |
| Pre-planning 2 | Pipe classes, fluid specifications | `.f31` |
| Pre-planning 3 | Substances/media, ATEX zones, P&T data | `.f34` |
| Pre-planning 4 | Cable planning objects, cable placeholders | `.f32` |
| Pre-planning 5 | Planning structure assignments | `.f32` |
| Pre-planning 6 | Function group planning | `.f32` |
| Pre-planning 7 | Vendor/package unit planning | `.f32` |
| Pre-planning 8 | Custom project-specific planning level | `.f32` |

**Most used Pre-planning properties:**

| Property | ID | Category | Description | Used in Form |
|----------|----|----------|-------------|-------------|
| Planning object designation | `<50001>` | Pre-planning 1 | Loop/object tag (TIC-101) | `.f32` `.f33` |
| Planning object description | `<50011>` | Pre-planning 1 | Loop description | `.f32` `.f33` |
| Loop number | `<50021>` | Pre-planning 1 | Instrument loop number | `.f33` |
| Instrument tag | `<50031>` | Pre-planning 1 | Field device tag (TT-101) | `.f33` |
| Signal type | `<50091>` | Pre-planning 1 | 4-20mA, HART, 24VDC | `.f33` |
| Pipe class | `<50041>` | Pre-planning 2 | Pipe spec class (A1B) | `.f31` |
| Pipe material | `<50042>` | Pre-planning 2 | Carbon steel, SS316 | `.f31` |
| Pressure rating | `<50043>` | Pre-planning 2 | PN40, Class 300 | `.f31` |
| Substance name | `<50051>` | Pre-planning 3 | Process medium name | `.f34` |
| Operating pressure | `<50061>` | Pre-planning 3 | Bar / psi | `.f34` |
| Operating temperature | `<50071>` | Pre-planning 3 | °C / °F range | `.f34` |
| ATEX zone | `<50081>` | Pre-planning 3 | Zone 0/1/2, Zone 20/21/22 | `.f34` |
| Hazard class | `<50082>` | Pre-planning 3 | II A/B/C, T1-T6 | `.f34` |

---

### 23. Prices

**What it contains:** Cost and pricing data from the parts management database — unit prices, total prices, currency, discount information.

**When to use:** Cost estimation reports and BOM forms where financial data is required.

| Property | ID | Description | Used in Form | Expert Usage |
|----------|----|-------------|-------------|-------------|
| Price (unit) | `<20821>` | Unit price from parts management | `.f05` | Cost estimation |
| Price (total) | `<20831>` | Quantity × unit price | `.f05` | BOM cost rollup |
| Currency | `<20841>` | Currency code (EUR, USD…) | `.f05` | Multi-currency projects |
| Discount % | `<20851>` | Applied discount percentage | `.f05` | Negotiated pricing |
| Net price | `<20861>` | Price after discount | `.f05` | Final procurement cost |

---

### 24. Pro Panel 🆕 Expanded in 2026

**What it contains:** 3D cabinet layout properties from EPLAN Pro Panel — enclosure dimensions, mounting panel references, rail positions, layout space data.

**When to use:** Projects using EPLAN Pro Panel for 3D cabinet design. Links schematic devices to their physical 3D placement.

| Property | ID | Description | Used in Form | Expert Usage |
|----------|----|-------------|-------------|-------------|
| Enclosure designation | `<26001>` | Cabinet/enclosure ID | `.f05` `.f06` | Links BOM to 3D layout |
| Layout space | `<26011>` | 3D layout space name | `.f05` `.f06` | Pro Panel space reference |
| Mounting panel designation | `<26021>` | Mounting panel ID | `.f05` `.f06` | Panel assembly reference |
| X/Y/Z position | `<26031>` | 3D coordinates in cabinet | `.f06` | Assembly positioning |
| Enclosure width/height/depth | `<26041>` | Cabinet external dimensions | `.f05` | Logistics/installation |
| Rail designation | `<26051>` | DIN rail ID in layout | `.f05` `.f06` | Assembly sequence |
| View (front/rear/side) | `<26061>` 🆕 | Which view the device appears in | `.f06` | Multi-view Pro Panel 2026 feature |

---

### 25. Revision 🆕 Enhanced in 2026

**What it contains:** Full revision tracking data — revision index, change descriptions, dates, authors across all revision levels.

**When to use:** Formal revision history tables on cover sheets and title blocks. Especially important for regulated industries (machinery directive, ATEX).

| Property | ID | Description | Used in Form | Expert Usage |
|----------|----|-------------|-------------|-------------|
| Revision index | `<10151>` | Current revision (A, B, 01…) | `.f00` `.f01` `.f02` | Title block revision field |
| Revision: Description | `<10152>` | What changed in this revision | `.f00` `.f02` | Change description column |
| Revision: Date | `<10153>` | Date of this revision | `.f00` `.f02` | Revision history date column |
| Revision: Author | `<10154>` | Who made this revision | `.f00` `.f02` | Accountability tracking |
| Revision: Approval | `<10155>` | Who approved this revision | `.f00` `.f02` | Formal sign-off |
| Revision: Status | `<10156>` 🆕 | Draft / For review / Released | `.f00` `.f02` | Document lifecycle state |

---

### 26. Safety 🆕 New in 2026

**What it contains:** Safety-related properties supporting functional safety documentation — SIL levels, safety function descriptions, ATEX references, safety integrity data.

**When to use:** Machinery safety projects (ISO 13849, IEC 62061), SIL-rated systems (IEC 61511), ATEX documentation.

| Property | ID | Description | Used in Form | Expert Usage |
|----------|----|-------------|-------------|-------------|
| Safety function | `<27001>` 🆕 | Safety function description | `.f06` `.f22` | Functional safety documentation |
| SIL level | `<27002>` 🆕 | Safety Integrity Level (SIL 1-4) | `.f06` `.f22` | IEC 61508/61511 compliance |
| Performance level | `<27003>` 🆕 | PL a-e (ISO 13849) | `.f06` | Machinery safety compliance |
| Safety category | `<27004>` 🆕 | Category B/1/2/3/4 (ISO 13849) | `.f06` | Safety architecture |
| ATEX category | `<27005>` 🆕 | Equipment category 1G/2G/3G/1D/2D/3D | `.f06` `.f04` | Hazardous area classification |
| Safe state | `<27006>` 🆕 | Defined safe state of device | `.f06` | SIL documentation |

---

### 27. Supplementary Fields

**What it contains:** Free-text and numeric user-definable fields at both project and device level — up to 10 slots at device level, 5 at project level.

**When to use:** Any project-specific data that doesn't fit into standard EPLAN properties. Commonly used for custom client fields, internal tracking codes, asset tags.

| Property | ID | Description | Used in Form | Expert Usage |
|----------|----|-------------|-------------|-------------|
| Device supplementary 1–10 | `<20901>`–`<20910>` | Free device-level text | `.f05` `.f06` `.f11` | Custom BOM columns |
| Project supplementary 1–5 | `<10901>`–`<10905>` | Free project-level text | `.f00` `.f01` | Custom title block fields |
| Part supp. field: Text | `<20501>` | Free part reference text | `.f05` `.f06` | Part-level custom field |

---

### 28. Topology 🆕 New in 2026

**What it contains:** Cable routing topology properties — routing paths, routing tracks, topology network data for automated cable routing.

**When to use:** Projects using EPLAN's Topology module for automated cable length calculation and routing path documentation.

| Property | ID | Description | Used in Form | Expert Usage |
|----------|----|-------------|-------------|-------------|
| Routing track specification | `<31119>` 🆕 | Assigned routing track name | `.f17` `.f04` | Topology routing reference |
| Routing path name | `<31120>` 🆕 | Named routing path designation | `.f04` | Cable routing documentation |
| Topology: Network | `<31121>` 🆕 | Topology network assignment | `.f04` | Network-based routing |
| Routed cable length | `<32031>` | Calculated routed length | `.f04` | Compare vs manual length |

---

### 29. Wiring 🆕 New in 2026

**What it contains:** Properties from the new EPLAN Wiring Manager — wiring sequences, wire assignments, automated wiring data for smart wiring machines.

**When to use:** Projects connected to EPLAN Smart Wiring or automated wiring machine export (Rittal Wire Terminal WT, Komax, Schleuniger).

| Property | ID | Description | Used in Form | Expert Usage |
|----------|----|-------------|-------------|-------------|
| Wiring sequence | `<35001>` 🆕 | Order of wiring operations | `.f17` | Manufacturing sequence |
| Wire bundle | `<35002>` 🆕 | Bundle/harness assignment | `.f17` `.f04` | Smart wiring machine data |
| Wiring side | `<35003>` 🆕 | Front / rear panel wiring side | `.f17` | Panel assembly instruction |
| Wire cut length | `<35004>` 🆕 | Pre-cut wire length for machine | `.f17` | Automated wire prep |
| Wiring machine export status | `<35005>` 🆕 | Ready / exported / confirmed | `.f17` | Manufacturing workflow |

---

## Category × Form Type Quick Matrix

Which categories are relevant to which form types:

| Category | `.f00` | `.f01` | `.f04` | `.f05` | `.f06` | `.f10` | `.f11` | `.f17` | `.f22` | `.f31`–`.f34` |
|----------|:------:|:------:|:------:|:------:|:------:|:------:|:------:|:------:|:------:|:-------------:|
| General | ✅ | ✅ | — | — | ✅ | — | — | — | — | — |
| Editing | ✅ | ✅ | — | — | — | — | — | — | — | — |
| Customer | ✅ | — | — | — | — | — | — | — | — | — |
| End customer | ✅ | — | — | — | — | — | — | — | — | — |
| Archive data | ✅ | ✅ | — | — | — | — | — | — | — | — |
| Revision | ✅ | ✅ | — | — | — | — | — | — | — | — |
| Devices | — | ✅ | — | ✅ | ✅ | ✅ | ✅ | — | — | — |
| Function data | — | — | — | — | ✅ | — | — | — | — | ✅ |
| Parts | — | — | — | ✅ | ✅ | ✅ | — | — | — | — |
| Prices | — | — | — | ✅ | — | — | — | — | — | — |
| Certification | — | — | ✅ | ✅ | ✅ | — | — | — | — | ✅ |
| Connection | — | — | — | — | — | ✅ | ✅ | ✅ | — | — |
| Cable data | — | — | ✅ | — | — | — | ✅ | ✅ | — | — |
| PLC data | — | — | — | — | — | — | — | ✅ | ✅ | — |
| Mounting data | — | — | — | ✅ | ✅ | — | — | — | — | — |
| Pro Panel | — | — | — | ✅ | ✅ | — | — | — | — | — |
| Pre-planning 1–3 | — | — | — | — | — | — | — | — | — | ✅ |
| Topology 🆕 | — | — | ✅ | — | — | — | — | ✅ | — | — |
| Wiring 🆕 | — | — | — | — | — | — | — | ✅ | — | — |
| Safety 🆕 | — | — | — | — | ✅ | — | — | — | ✅ | — |
| Data for reports | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Supplementary fields | ✅ | — | — | ✅ | ✅ | — | ✅ | — | — | — |

---

## Top 20 Properties Every EPLAN Expert Uses

Regardless of project type, these properties appear in virtually every professional EPLAN project:

| # | Property | ID | Category | Why Every Expert Uses It | Form |
|---|----------|----|----------|--------------------------|------|
| 1 | Project name | `<10011>` | General | Title block — mandatory on every page | All |
| 2 | Page number | `<11021>` | General | "Page X of Y" — always in footer | All |
| 3 | Total page count | `<11031>` | General | "of Y" complement to page number | All |
| 4 | Device tag (full) | `<20001>` | Devices | Primary device identifier in all reports | `.f05` `.f06` |
| 5 | Function text | `<20011>` | Devices | What the device does — most readable field | `.f05` `.f06` `.f11` |
| 6 | Part number | `<20601>` | Parts | BOM article number — procurement core | `.f05` `.f06` |
| 7 | Manufacturer | `<20611>` | Parts | Supplier identification — procurement core | `.f05` `.f06` |
| 8 | Quantity | `<20801>` | Parts | BOM count — procurement core | `.f05` |
| 9 | Description 1 | `<20631>` | Parts | Human-readable part description | `.f05` `.f06` |
| 10 | Wire color | `<31051>` | Connection | IEC color coding — wiring technician essential | `.f10` `.f11` `.f17` |
| 11 | Wire cross-section | `<31061>` | Connection | Safety-critical wiring spec | `.f10` `.f11` `.f17` |
| 12 | Terminal designation | `<31001>` | Connection | Primary terminal identifier | `.f10` `.f11` |
| 13 | Connection (internal) | `<31031>` | Connection | Full from-path for technician | `.f11` `.f17` |
| 14 | Connection (external) | `<31041>` | Connection | Full to-path for technician | `.f11` `.f17` |
| 15 | Cable designation | `<32001>` | Cable data | Cable ID in all cable reports | `.f04` `.f17` |
| 16 | Cable type | `<32011>` | Cable data | Procurement and installation spec | `.f04` |
| 17 | PLC address | `<40001>` | PLC data | Hardware I/O address | `.f22` `.f17` |
| 18 | Signal name | `<40011>` | PLC data | Process signal identity | `.f22` `.f17` |
| 19 | Revision index | `<10151>` | Revision | Document version control | `.f00` `.f01` |
| 20 | Mounting location | `<20651>` | Mounting data | Physical location in cabinet | `.f05` `.f06` |

---

## Related Files

| File | Description |
|------|-------------|
| `eplan_p8_project_structure.json` | Full metadata for all 16 project report folders |
| `README.md` | General project structure reference |
| `README_Interactive_vs_AutoGenerated.md` | Interactive vs. auto-generated page types |
| `README_Form_Components.md` | Form file anatomy and placeholder syntax |
| `README_Placeholder_Properties.md` | Placeholder text dialog — elements and categories |
| `README_Expert_Properties.md` | Expert property reference with form mapping |
| `README_Form_Layout_and_Types.md` | Form layout areas and `.f00`–`.f34` types |
| `README_All_Categories_2026.md` | This file |

---

*EPLAN Electric P8 / Eplan Platform 2026 — Engineering Reference Documentation*
*Property IDs shown are standard EPLAN IDs. IDs marked 🆕 are new or significantly changed in Platform 2026.*
*Always verify IDs in the Placeholder texts browser for your specific installation version.*
