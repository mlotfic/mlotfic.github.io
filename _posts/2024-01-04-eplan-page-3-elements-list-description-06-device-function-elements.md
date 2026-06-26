
---

## 6. Device & Function Elements

### `Device`
The core engineering object in EPLAN representing one physical component installed in the project. A Device has a unique device tag (reference designation), one or more Functions, and one or more Part references.

**Structure of a Device:**
```
Device [-K1]
├── Function: Main contact (NO)
├── Function: Auxiliary contact (NC)
├── Function: Coil
└── Part reference: 3RT2023-1BB40
```

**Implementation notes:**
- Device tags follow IEC 81346: `=Function+Location-Product` (e.g., `=MCC+Panel01-K1`).
- Devices without matching Part references generate BOM warnings.
- Device navigator provides a tree view of all devices in the project.

---

### `Device (header object)`
The top-level container record aggregating all functions of a multi-function device. Provides summary properties (device tag, description) accessible at the header level without drilling into individual functions.

**Implementation notes:**
- Used in device-level reports where header properties must appear once per device regardless of function count.
- Header properties cascade to child function records unless overridden.

---

### `Function`
Represents one specific electrical function of a device as placed in the schematic — e.g., the main contact of a contactor, the coil symbol, or one auxiliary contact. Functions are placed as schematic symbols and cross-referenced back to the parent device.

**Implementation notes:**
- Functions are defined by their **Function definition** (from the function definition library), which specifies connection point count, function type, and representation in different symbol standards.
- A device's complete set of functions must be "closed" — all defined functions of the device type must be placed for schematic completeness checks to pass.
- Use **View → Device navigator** to verify all function placements.

---

### `Function (header object)`
Header record for a function entry, aggregating variants of the same function across the project.

---

### `Device group (further functions)`
A grouping element used to collect auxiliary or supplementary functions of a device (e.g., position feedback contacts, mechanical interlocks, LED indicators) that are listed separately from the main function group.

**Implementation notes:**
- Declared in device properties under the **Further functions** tab.
- Ensures auxiliary functions are cross-referenced to the correct device without being treated as separate devices.

---

### `Device tag`
The alphanumeric label uniquely identifying a device in the project, composed according to the project's reference designation scheme. Follows IEC 81346 with structure: `=<function designation>+<location>-<product code><number>`.

**Implementation notes:**
- Device tags must be unique within their structure level.
- Generated automatically by incrementing counters or manually assigned.
- Changing a device tag propagates across all cross-references and reports.
- Tag format is configured in **Project settings → Device → Device tag**.

---

### `3D model view`
A view representation of a 3D component model within EPLAN Pro Panel. Displays the geometric 3D body of a placed device, used for enclosure layout visualization and interference checking.

**Implementation notes:**
- 3D models are stored as `.3ds`, `.step`, or `.dxf` files referenced by part records.
- Required for accurate cut-out and mounting clearance checks in panel layouts.
- Exported to Pro Panel for photorealistic assembly documentation.


## `Device (source)`

- The originating device of a cable connection as shown in cable documentation and wiring lists.
- Represents the "FROM" device with its full reference designation (e.g., `=A1+MCC-K1:A1`).

**Implementation notes:**

- Populated automatically from the cable's schematic source connection point.
- Used as the primary sort key in cable schedules and wiring lists.

---

## `Device (target)`

- The destination device of a cable connection — the "TO" device in wiring documentation.
- Paired with `Device (source)` in every cable schedule row.

---