---

title: EPLAN Pages - Interactive vs. Auto-Generated Pages
description: >-
  A clear explanation of the difference between interactive pages (manually drawn) and auto-generated report pages (form-based) in EPLAN P8, with examples and best practices.
date: 2024-03-19 10:00:00 +0800
author: Mahmoud Lotfi
file_name: 2024-03-19-eplan-pages-interactive-pages-auto-generated-pages-1.md

categories: [EPLAN, Pages, Files Structures, Interactive, Auto-generated, Reports]
tags: [EPLAN, pages]

pin: False
math: true
mermaid: true
comments: true
toc: true
render_with_liquid: false

image:
  path: /assets/img/posts/eplan.jpg
  alt: EPLAN Pages - Interactive vs. Auto-Generated Pages
  lqip: data:image/webp;base64,UklGRjoAAABXRUJQVlA4IC4AAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
---

# Pages in Eplan

> Interactive Pages vs. Auto-Generated Report Pages in EPLAN P8



---

## 🖊️ Interactive Pages

These are pages you **manually create and draw** in the schematic editor. You place symbols, draw connections, enter data yourself.

| Property   | Detail                                                        |
| ---------- | ------------------------------------------------------------- |
| Created by | Engineer manually                                             |
| Page types | Circuit diagram, Single-line, P&ID, PLC overview, Fluid power |
| Stored as  | `.eds` project data                                           |
| Examples   | Motor starter circuit, PLC I/O schematic, P&ID flow diagram   |
| Editable   | Yes — full graphical editing                                  |

These are your **source data**. Everything else flows from them.

### list of Interactive Pages

| Interactive Pages (I)               | Description                                                    |
| ------------------------------------| -------------------------------------------------------------- |
| External document (I)               | Reference or link to external documentation or files           |
| Fluid power schematic (I)           | Schematic diagram for hydraulic or pneumatic systems           |
| Function overview (fluid power) (I) | Overview of functions within fluid power systems               |
| Graphic (I)                         | Page for graphical illustrations or visual elements            |
| Model view (I)                      | 3D or model-based view of system components                    |
| Overview (I)                        | General overview page summarizing system or project            |
| P&I diagram (I)                     | Process and instrumentation diagram for process systems        |
| Panel layout (I)                    | Layout drawing of electrical panels and components             |
| Pre-planning (I)                    | Page for early-stage planning and design documentation         |
| Schematic multi-line (I)            | Detailed multi-line electrical schematic for complex circuits  |
| Schematic single-line (I)           | Simplified single-line schematic for power distribution        |
| Topology (I)                        | Topology diagram showing network or system connections         |

---

## ⚙️ Auto-Generated Pages (Form-Based Reports)

These are pages EPLAN **generates automatically** by reading data from interactive pages and rendering it through a `.f??` form template.

| Property   | Detail                                                                   |
| ---------- | ------------------------------------------------------------------------ |
| Created by | EPLAN engine (Utilities → Reports → Generate)                            |
| Driven by  | Form files (`.f00`–`.f51`)                                               |
| Source     | Device data, connections, terminals, cables entered on interactive pages |
| Examples   | Terminal diagrams, Parts list, Cable overview, Connection list, TOC      |
| Editable   | ❌ Not directly — changes must be made on the source interactive page    |

### list of Auto-generated Pages

| Auto-generated pages (A)                     | Form template | Description                                               |
| -------------------------------------------- | ------------- | --------------------------------------------------------- |
| Assembly/Module overview (A)                 | f44           | Overview of assemblies or modules in the project          |
| Cable assignment diagram (A)                 | f08           | Diagram showing cable assignments to devices or terminals |
| Cable diagram (A)                            | f09           | Detailed representation of cable connections              |
| Cable overview (A)                           | f10           | Summary of all cables used in the project                 |
| Cable-connection diagram (A)                 | f07           | Illustrates specific cable-to-device connections          |
| Conduit / line plan (A)                      | f46           | Plan for conduits and line routing                        |
| Connection list (A)                          | f27           | Tabular list of all electrical connections                |
| Cut-out legend (A)                           | f47           | Legend for cut-outs in panels or enclosures               |
| Device tag list (A)                          | f03           | List of device identifiers used in the project            |
| Device-connection diagram (A)                | f05           | Diagram showing device interconnections                   |
| Distributed device list (A)                  | f45           | List of devices distributed across locations              |
| Enclosure legend (A)                         | f18           | Legend for enclosure components                           |
| Forms documentation (A)                      | f04           | Documentation forms for project reporting                 |
| Manufacturer / supplier list (A)             | f31           | List of manufacturers and suppliers                       |
| Mounting list (A)                            | f32           | List of mounting components and positions                 |
| P&I diagram: Piping overview (A)             | f37           | Process and instrumentation piping overview               |
| PLC address overview (A)                     | f48           | Overview of PLC addresses used                            |
| PLC card overview (A)                        | f20           | Overview of PLC cards/modules                             |
| PLC diagram (A)                              | f19           | Detailed PLC wiring and logic diagram                     |
| Parts list (A)                               | f01           | Comprehensive list of project parts                       |
| Pin-connection diagram (A)                   | f21           | Diagram showing pin-level connections                     |
| Placeholder object overview (A)              | f30           | Overview of placeholder objects in design                 |
| Plot frame documentation (A)                 | f15           | Documentation of plot frames used                         |
| Plug diagram (A)                             | f22           | Diagram of plug connections                               |
| Plug overview (A)                            | f23           | Overview of plug types and usage                          |
| Potential overview (A)                       | f16           | Overview of electrical potentials                         |
| Pre-planning: Pipe class overview (A)        | f49           | Overview of pipe classes in pre-planning                  |
| Pre-planning: Planning object overview (A)   | f40           | Overview of planning objects                              |
| Pre-planning: Planning object plan (A)       | f41           | Plan of planning objects                                  |
| Pre-planning: Segment template overview (A)  | f42           | Overview of segment templates                             |
| Pre-planning: Segment template plan (A)      | f43           | Plan of segment templates                                 |
| Pre-planning: Structure segment overview (A) | f38           | Overview of structure segments                            |
| Pre-planning: Structure segment plan (A)     | f39           | Plan of structure segments                                |
| Pre-planning: Substance overview (A)         | f51           | Overview of substances in pre-planning                    |
| Project options overview (A)                 | f29           | Overview of project options and settings                  |
| Revision overview (A)                        | f17           | Overview of project revisions                             |
| Structure identifier overview (A)            | f24           | Overview of structure identifiers                         |
| Summarized parts list (A)                    | f02           | Condensed list of project parts                           |
| Symbol overview (A)                          | f25           | Overview of symbols used in diagrams                      |
| Table of contents (A)                        | f06           | Table of contents for documentation                       |
| Terminal diagram (A)                         | f13           | Diagram of terminal connections                           |
| Terminal line-up diagram (A)                 | f12           | Diagram showing terminal arrangement                      |
| Terminal-connection diagram (A)              | f11           | Diagram showing terminal-to-device connections            |
| Terminal-strip overview (A)                  | f14           | Overview of terminal strips                               |
| Title page / cover sheet (A)                 | f04           | Title or cover sheet for documentation                    |
| Topology: Routed cables / connections (A)    | f36           | Topology of routed cables and connections                 |
| Topology: Routing path diagram (A)           | f35           | Diagram of routing paths                                  |
| Topology: Routing path list (A)              | f34           | List of routing paths                                     |

---

## The Relationship

```cs
Interactive Pages  →  EPLAN Database    →  Form Template (.f??)  →  Auto-Generated Report Page
 (you draw this)     (data extracted)        (defines layout)         (EPLAN renders this)
```

So for example:

- You draw a **circuit diagram** (interactive) placing terminal -X1:1
- EPLAN extracts all terminal data into its database
- The **Terminal Diagram form** (`.f11`) reads that data and renders the terminal wiring page automatically

---

## Key Rule

> **Never edit a generated report page directly.** If you change something there, it gets overwritten the next time reports are regenerated. Always go back to the **source interactive page** to make corrections.

---

## Which folders in your project are which?

| Folder                            | Type                                               |
| --------------------------------- | -------------------------------------------------- |
| P&I diagram: Piping overview      | ✏️ Interactive                                     |
| PLC diagram (SPS Connection)      | ⚙️ Auto-generated                                  |
| Pre-planning diagrams             | ✏️ Interactive (pre-planning editor)               |
| Cable diagram                     | ⚙️ Auto-generated                                  |
| Connection list                   | ⚙️ Auto-generated                                  |
| Terminal diagram / strip overview | ⚙️ Auto-generated                                  |
| Summarized parts list             | ⚙️ Auto-generated                                  |
| Table of contents                 | ⚙️ Auto-generated                                  |
| Title page / cover sheet          | 🔀 Mixed — cover sheet is interactive, others auto |

The **pre-planning pages** are a special case — they are interactive in their own editor (the Pre-planning Navigator), but they also drive auto-generated outputs like loop diagrams and PCT overviews.
