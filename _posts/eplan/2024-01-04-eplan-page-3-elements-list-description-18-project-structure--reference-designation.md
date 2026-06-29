## 18. Project Structure & Reference Designation

### `Project`
The top-level container for all EPLAN project data — pages, devices, parts assignments, settings, and reports. Stored as a `.elk` / `.edb` project directory or compressed `.zw1` archive.

**Implementation notes:**
- Project settings include: reference designation structure, display standards (IEC, NFPA, GB, AS), page numbering, DRC rules, and report forms.
- Project properties auto-fill plot frame title block fields.
- Multiple engineers can work simultaneously using EPLAN's multi-user infrastructure.

---

### `Document type`
A classification applied to project pages that determines how the page is processed, reported, and displayed. Standard document types include:

| Document type | Use |
|---|---|
| Schematic multi-line | Main circuit diagrams |
| Schematic single-line | One-line / riser diagrams |
| Terminal diagram | Auto-generated terminal charts |
| P&ID | Process & Instrumentation Diagram |
| Panel layout | 2D mounting panel layout |
| 3D mounting layout | Pro Panel 3D view |
| Cover sheet | Title page |
| Table of contents | Auto-generated index |
| PLC diagram | PLC rack/card layout |

---

### `Function designation`
The functional component of the reference designation system (IEC 81346 aspect `=`). Identifies what a device does (e.g., `=DRIVE`, `=CONTROL`, `=LIGHTING`). Used as the first level of the full device tag.

---

### `Functional assignment`
The assignment of a device or function to a defined functional area in the project structure, linking the device to its role in the overall system.

---

### `Installation site`
A physical location identifier in IEC 81346 using the installation aspect (`++`). Represents the geographical or spatial location: building, floor, room (e.g., `++SITE-A`, `++PUMP-HOUSE`).

---

### `Location designation`
Physical location prefix in the reference designation (`+`) identifying an enclosure, room, or cabinet (e.g., `+MCC-01`, `+JB-FIELD-03`).

---

### `Product`
The product/component identifier component of the reference designation (`-`) distinguishing the individual item (e.g., `-K1`, `-Q3`, `-T1`).

---

### `Structure identifier`
The complete hierarchical reference designation combining function designation (`=`), installation site (`++`), location (`+`), and product (`-`) to form the full unique identifier for a device or page.

---

### `User-defined structure`
A custom structure level defined beyond the standard IEC 81346 hierarchy. Used when project-specific organizational requirements exceed the standard three-level system.

---

### `Higher-level function number`
A numeric element for defining hierarchical function numbering, used in complex multi-level functional hierarchies.

---

### `Project option`
A variant configuration within a project, enabling multiple equipment variants to coexist in one project file. When option A is active, only option-A pages and devices are visible/exported; option B pages are suppressed.

**Implementation notes:**
- Configured under **Project options navigator**.
- Used for product variants (e.g., standard vs. extended I/O configuration).
- Project option sections group the pages belonging to each variant.

---

### `Project option section`
A named group of pages and elements belonging to a specific project option variant. Acts as the container for all content associated with one configuration.

---

### `Value set table`
A lookup table defining the allowable values for properties and parameters in EPLAN. Used to create consistent dropdown selections across the project (e.g., insulation color codes, cross-section standards, mounting types).

---

### `Placeholder object`
A variable placeholder in forms and report templates that resolves to a real project data field at report generation time. Examples: `<PROJECT.CUSTOMER>`, `<DATE>`, `<PAGE.NAME>`.

**Implementation notes:**
- Defined in the form editor as special text objects.
- Supports formatting (date format, number format, text truncation).
- Custom placeholder types can reference any project, page, or device property.

---

### `Page`
A drawing sheet within an EPLAN project. Has a page type, page name (full designation), page properties (description, revision, approval), and is assigned a plot frame and structure identifier.

**Implementation notes:**
- Pages are numbered and named according to project settings.
- Page cross-references are generated automatically by EPLAN for off-page connections.
- Page types determine which symbols and report forms apply.
