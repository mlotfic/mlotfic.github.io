# 1. Part & Component Management

## `Part`

- The fundamental catalog record in EPLAN Parts Management (EPM).
- Stores :
  - manufacturer data,
  - catalog number,
  - technical specifications (voltage, current, IP rating, weight, dimensions),
  - property assignments.
- Every device placed in a schematic references a Part to generate BOMs and procurement data.

**Implementation notes:**

- Stored in the EPLAN parts database (`.edb` or SQL backend).
- Synchronized across projects via master parts database.
- A Part may have multiple variants (A-variant, B-variant) for order options.
- Linked to `Record` for structured access via reports.

---

## `Part (header object)`

- The parent-level record that aggregates sub-parts under a common catalog number when a component consists of multiple physical items (e.g., a motor starter kit: contactor + overload relay + accessories).
- Acts as the umbrella record in multi-part assemblies.

**Implementation notes:**

- Used in `PARTSM` report context.
- Header object properties (e.g., manufacturer, catalog number) cascade to child Part entries.
- Essential for multi-article ordering where a single function number maps to multiple physical parts.

---

## `Part reference`

- An instance reference created when a device function in the schematic is linked to a specific Part in the catalog.
- The Part reference carries properties inherited from the Part catalog entry, overridden at the instance level if needed.

**Implementation notes:**

- Created automatically when you assign a part number to a device using **Device properties → Parts**.
- Multiple Part references can exist under one device (e.g., coil part + contact part + accessories).
- Referenced in BOM reports, terminal diagrams, and wiring lists.

---

## `Part reference (header object)`

- Header record grouping multiple Part reference instances under a single device or function.
- When a device has both a main part and accessory parts, the header object provides the aggregation point for total-cost and total-quantity calculations in procurement reports.

**Implementation notes:**

- Appears in reports that use `PART_REF_HEADER` sort key.
- Required when generating hierarchical BOM structures (assembly → sub-components).

---

## `Record`

- A top-level data record in the parts management database representing a complete dataset for one catalog item.
- The Record contains all sub-entries:
  - technical data fields
  - accessories
  - macro assignments
  - revision history
  - mounting data

**Implementation notes:**

- Accessible via **Utilities → Parts → Management**.
- Records can be imported/exported via `.edz` or directly from manufacturer portals (e.g., Siemens TIA Portal integration, Eaton xPole catalog).
- Record integrity validation checks for mandatory fields before use in projects.

---

## `Manufacturer / supplier`

- Master data record for a manufacturer or supplier organization in EPM.
- Stores contact data, web links, and serves as the parent entity for all Part entries from that source.

**Implementation notes:**

- Assigned to each Part under **Manufacturer/supplier** property tab.
- Used in procurement reports to filter and sort by supplier.
- Distinguishing `Manufacturer` from `Supplier` allows separate tracking of OEM vs. distributor sourcing.

---

## `Part reference manufacturer`

- A Part reference specifically linked to a manufacturer's catalog entry, as opposed to a generic or supplier-defined reference.
- Used when the design calls out a specific OEM product.

**Implementation notes:**

- Selected when the `Source = Manufacturer` field is populated in the Part reference properties.
- Generates manufacturer-specific procurement documents.

---

## `Part reference supplier`

- A Part reference tied to a specific distributor/supplier, enabling generation of supplier-specific purchase orders.
- Often used alongside a manufacturer reference when procurement channels differ.

**Implementation notes:**

- Allows cost comparison between multiple suppliers for the same manufacturer part.
- Selected via **Part reference → Supplier** tab in device properties.

---

## `Part (source)`

- The physical catalog part at the source-side of a cable or connection.
- Distinct from `Device (source)` — this refers to the connector/termination part, not the device itself.

---

## `Part (target)`

- The catalog part at the target side of the connection.

---

## `Part reference (source)`

- Instance reference for the source-side connection part,
- enabling BOM line items for connectors, ferrules, or cable glands at the source end.

---

## `Part reference (target)`

- Instance reference for the target-side connection part.

---