---

layout: post
cover_color: #000000

keywords: 

title: "EPLAN - Intro"

description: >- 
  EPLAN is a software suite for electrical engineering and automation design. It provides tools for creating electrical schematics, panel layouts, and other documentation required for electrical systems. It is used by electrical engineers, automation engineers, and other professionals to design, document, and manage electrical systems. It is used in a variety of industries, including manufacturing, automation, and energy. It is a powerful tool that can be used to create complex electrical systems.

date: 2024-01-01 10:00:00 +0800
author: Mahmoud Lotfi
file_name: 2024-01-01-eplan-intro.md
categories: [EPLAN, Intro]
tags: [EPLAN, Intro]
pin: False
math: true
mermaid: true
comments: true
toc: true
render_with_liquid: false

image:
  path: /assets/img/posts/eplan.jpg
  alt: Eplan Intro
  lqip: data:image/webp;base64,UklGRjoAAABXRUJQVlA4IC4AAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA

---

# Eplan - Intro

- EPLAN is a software suite for electrical engineering and automation design.
- It provides tools for creating electrical schematics, panel layouts, and other documentation required for electrical systems.
- It is used by electrical engineers, automation engineers, and other professionals to design, document, and manage electrical systems.
- It is used in a variety of industries, including manufacturing, automation, and energy.
- It is a powerful tool that can be used to create complex electrical systems.

---

## About Eplan Electric P8

- If you come to EPLAN Electric P8 from AutoCAD or Visio, you will spend the first few weeks fighting it.
- The software feels rigid, opinionated, and oddly connected — change a wire color on one page and something updates three pages away.
- That is not a bug. That is the point.

> The mental shift: **EPLAN is a database that happens to have a drawing front-end.** Every symbol you place, every wire you draw, every terminal you assign — all of it is a record in a project database. The schematic is just one view of that data.

Once that clicks, everything else follows.

---

## The paradigm shift in one sentence

> In AutoCAD, you draw lines that look like wires.  
> In EPLAN, you define connections — the drawing is just how you see them.

This is why EPLAN feels rigid at first: it enforces the data model. A wire must connect two defined pins. A device must have a part assigned before it appears in the BOM. A terminal must belong to a strip. The constraints are the feature.

---

## Summary

| Layer             | Mental model                                       |
| :---------------- | :------------------------------------------------- |
| Master data       | Shared library — symbols, parts, macros, forms     |
| Project           | The engineering database for one job               |
| Pages             | Visual interface to the database                   |
| Engineering model | Devices, connections, potentials — the actual data |
| Auto reports      | Queries formatted as documents                     |
| Output            | XML, CSV, PDF, API — downstream consumption        |

EPLAN rewards engineers who understand its data model. The learning curve is not about learning where buttons are — it is about accepting that you are doing structured data entry, and the schematic is the UI for that entry.

---

# Eplan Architecture

- EPLAN is a software suite for electrical engineering and automation design.
- It is a database-driven system that allows users to create, manage, and document electrical designs.
- It has 4 main components:
    1. **Project Container** - holds everything
    2. **Master Data** - symbols, parts, macros, forms
    3. **Reports** - auto-generated from data
    4. **Settings** - project settings, numbering, standards

---

## The building blocks of an EPLAN project

> The key mental model insight is: EPLAN is database-first, not drawing-first. The schematic IS the database.

the major pillars of an EPLAN P8 project.

- `Project Container` - holds everything
  - `Pages` - drawing sheets (schematic, SLD, terminal, report).
  - `Devices` - the engineering objects (DT-based).
  - `Connections` - wires, cables, potentials.
- `Master Data` - symbols, parts, macros, forms.
- `Reports` - auto-generated from data.
- `Settings/Properties` - project settings, numbering, standards

![Eplan has four layers](/assets/img/posts/eplan-architecture.png)

A P8 project has four conceptual layers, stacked from foundation to output:

EPLAN P8 Project Structure

```cs

├── Master Data (global libraries)
│   ├── Symbols
│   ├── Parts Database
│   ├── Macros
│   └── Forms
│
├── Project (local to this job)
│   ├── Pages (schematic, overview, terminal, report)
│   │
│   ├── Engineering Model (the real database)
│   │   ├── Devices (DT-tagged components)
│   │   ├── Functions (coil, contacts, PLC I/O)
│   │   ├── Connections (wires, cables, potentials)
│   │   └── Terminals (strip assignment, numbering)
│   │
│   └── Reports (auto-generated)
│       ├── BOM / Parts List
│       ├── Wire List
│       ├── Terminal Diagram
│       └── Cable Schedule
│
└── Settings
    ├── Standards
    └── Numbering Schemes
```

---

### Layer 1 — Master data (the library)

Master data lives outside any single project and is shared across all of them. It is the reference layer.

| Component             | What it is                                                                         |
| ----------------------|------------------------------------------------------------------------------------|
| **Symbols**           | Graphical representations per IEC 60617 or NFPA 79 — coils, contacts, motors, PLCs |
| **Parts database**    | Manufacturer articles with technical data, macros, order numbers                   |
| **Macros**            | Reusable window, symbol, or page blocks — a DOL starter circuit, a fuse group      |
| **Forms / templates** | Report layouts, title block templates, page frame definitions                      |

Good master data discipline pays compound interest. A part entered correctly once means every BOM, every terminal list, and every cross-reference is correct automatically.

---

### Layer 2 — The project container

The project file (`.elk`) holds everything specific to one engineering job. Its internal structure follows a tag-based identifier system:

```cs
=Function (system/process)
  +Location (physical cabinet, room, building)
    -Device (individual component, e.g. -Q1, -K3)
```

This three-level hierarchy — function, location, device — is the addressing scheme EPLAN uses to uniquely identify every object in the project.

It maps cleanly onto ISA-88 and ISO 14224 equipment taxonomies if you are feeding data downstream into an asset management system.

---

### Layer 3 — The three columns inside the project

Inside the project, three things coexist and stay permanently synchronized:

**Pages — the visual layer**

Pages are drawing sheets. Types include:

- Schematic pages (multi-line circuit diagrams)
- SLD / overview pages (single-line, topology)
- Terminal diagrams (auto-generated or manual)
- Cable overview pages
- PLC I/O pages
- Report pages (BOM, wire list, cross-reference)

Pages are how engineers *interact* with the data. They are not the data itself.

**Engineering model — the real database**

The engineering model is what actually matters. Every action on a page writes to it:

| Object           | What it represents                                                                       |
| ---------------- | ---------------------------------------------------------------------------------------- |
| **Device (DT)**  | A physical component, uniquely addressed                                                 |
| **Function**     | One role of a device — main contact, coil, aux contact — potentially spread across pages |
| **Connection**   | A wire or conductor between two pins                                                     |
| **Potential**    | A named net — `+24VDC`, `L1`, `PE`, `GND`                                                |
| **Cable**        | A multi-core conductor with shield, cross-references auto-maintained                     |
| **Terminal**     | A connection point with auto-numbering and strip assignment                              |

The key insight: placing a symbol on a schematic page **creates or updates a device record**. Deleting a symbol does not delete a wire if the wire still connects two other pins — EPLAN tracks the connection independently of its graphical representation.

**Auto reports — derived output**

Reports are not documents you write. They are queries against the engineering model, formatted via a template (form). EPLAN regenerates them every time you update the project.

Standard auto-reports:

- Parts list / BOM
- Terminal strip diagram (per strip, per location)
- Wire list — from-pin to-pin with wire number, cross-section, color
- Cable schedule — cores, length, routing
- PLC I/O list — address, function, tag
- Cross-reference index — every device, every page it appears on

Because reports are derived, they are always consistent with the schematic. There is no "export then update the spreadsheet" step.

---

### Layer 4 — Output and export

When the project is complete, EPLAN exports to:

| Format                        | Use                                                                      |
| ----------------------------- | ------------------------------------------------------------------------ |
| **XML**                       | Full project data tree — suitable for ETL into EAM or CMMS               |
| **CSV / XLSX**                | Device list, BOM, terminal list for procurement or commissioning         |
| **PDF**                       | Drawing packages for site, client, or authority                          |
| **EPLAN API (COM/.NET)**      | Programmatic access — read devices, modify properties, run reports       |

The XML export is the most powerful for data engineering purposes. It exposes the full device-function-connection graph and maps well onto ISA-95 equipment hierarchy schemas.

---

## Some product information stored in path variable

|Path variable	              | Meaning                                                                                                         |
| :-------------------------- | :-------------------------------------------------------------------------------------------------------------- |
|$(BIN)	                      | A program directory generated on installation contains the program libraries (*.dll) of the individual modules. |
|$(CFG)	                      | A configuration directory generated on installation containing the xml files of the individual modules.         |
|$(CFG_COMPANY)	              | Configuration directory generated on installation, contains the company settings.                               |
|$(CFG_STATION)	              | Configuration directory generated on installation, contains the station settings.                               |
|$(CFG_USER)	                | Configuration directory generated on installation, contains the user settings.                                  |
|$(DOC)	                      | Project-specific directory for documents.                                                                       |
|$(EPLAN)	                    | An upper-level main directory generated on installation.                                                        |
|$(EPLAN_DATA)	              | A superior directory for master data, generated on installation.                                                |
|$(EPLAN_EXECUTABLE)	        | The directory to Eplan.exe.                                                                                     |
|$(ENVVAR_<Variable_Name>)    | OS environment variable.                                                                                        |
|$(EPLAN_VARIANT)             | Name of the started product variant.                                                                            |
|$(EPLAN_VERSION)             | Version number of the used Eplan.                                                                               |
|$(EPLAN_VERSION_SHORT)       | Main version number of the used Eplan.                                                                          |

---

## **Company name** (Company organization)

path : `C:\Users\Public\EPLAN\Settings\Education\2026.0.3\x64\Cfg`

- A company organization is a company-specific, protected Eplan Cloud workspace.
- In this workspace only invited members receive access and user rights for programs and data.
- The company organization is connected with your Eplan ID, your serial number and customer number.
- This company organization allows you to launch products such as Eplan Electric P8 starting at version 2022.

Settings
You can perform a number of different settings to configure the program to suit your personal requirements and needs:

- You can define the properties of a project, e.g. the graphical representation of electronic functions or the default format for device tags.
- You can set the working environment on a user-specific basis and thus adapt the program functionality to match the working methods of each user.
- You can define workstation-specific settings, such as the file path for the management of system messages.
- You can define company-specific settings, in order to define defaults and company conventions for all workstations used.

---

## user data and settings

Project data that you frequently use and project settings and configurations that you frequently use in your daily work can be managed in the user data and settings. You can specify the storage location for the user data and settings and you can set whether this user data and settings are to be loaded for each project or not.

---

#### ➲ **Next post:** [Eplan_Projects](https://mlotfic.github.io/posts/eplan-project-container)

> ⛓️‍💥 Mahmoud Lotfi