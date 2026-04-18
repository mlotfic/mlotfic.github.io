---
title: EPLAN Pages Explained - Interactive vs. Auto-Generated Report Pages
description: >-
  A clear explanation of the difference between interactive pages (manually drawn) and auto-generated report pages (form-based) in EPLAN P8, with examples and best practices.

author: Mahmoud Lotfi
date: 2024-03-19 10:00:00 +0800

categories: [EPLAN, Pages, Files Structures, Interactive, Auto-generated, Reports]
tags: [Eplan, pages]

pin: False
math: true
mermaid: true
comments: true
toc: true
render_with_liquid: false

image:
  path: /assets/img/posts/eplan.jpg
  alt: EPLAN Pages Explained
  lqip: data:image/webp;base64,UklGRjoAAABXRUJQVlA4IC4AAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
---

# Interactive Pages vs. Auto-Generated Report Pages in EPLAN P8

### 🖊️ Interactive Pages
These are pages you **manually create and draw** in the schematic editor. You place symbols, draw connections, enter data yourself.

| Property   | Detail                                                        |
| ---------- | ------------------------------------------------------------- |
| Created by | Engineer manually                                             |
| Page types | Circuit diagram, Single-line, P&ID, PLC overview, Fluid power |
| Stored as  | `.eds` project data                                           |
| Examples   | Motor starter circuit, PLC I/O schematic, P&ID flow diagram   |
| Editable   | Yes — full graphical editing                                  |

These are your **source data**. Everything else flows from them.

---

### ⚙️ Auto-Generated Pages (Form-Based Reports)
These are pages EPLAN **generates automatically** by reading data from interactive pages and rendering it through a `.f??` form template.

| Property   | Detail                                                                   |
| ---------- | ------------------------------------------------------------------------ |
| Created by | EPLAN engine (Utilities → Reports → Generate)                            |
| Driven by  | Form files (`.f00`–`.f34`)                                               |
| Source     | Device data, connections, terminals, cables entered on interactive pages |
| Examples   | Terminal diagrams, Parts list, Cable overview, Connection list, TOC      |
| Editable   | ❌ Not directly — changes must be made on the source interactive page     |

---

### The Relationship

```
Interactive Pages  →  EPLAN Database  →  Form Template (.f??)  →  Auto-Generated Report Page
 (you draw this)       (data extracted)    (defines layout)         (EPLAN renders this)
```

So for example:
- You draw a **circuit diagram** (interactive) placing terminal -X1:1
- EPLAN extracts all terminal data into its database
- The **Terminal Diagram form** (`.f11`) reads that data and renders the terminal wiring page automatically

---

### Key Rule
> **Never edit a generated report page directly.** If you change something there, it gets overwritten the next time reports are regenerated. Always go back to the **source interactive page** to make corrections.

---

### Which folders in your project are which?

| Folder                            | Type                                              |
| --------------------------------- | ------------------------------------------------- |
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
