
## 4. Connection Elements

### `Connection`
The fundamental schematic element representing a single electrical conductor (wire) between two connection points. The Connection is the building block of all electrical schematics — every line drawn between symbols creates a Connection object.

**Properties carried by a Connection:**
- Wire type / color
- Cross-section (mm² or AWG)
- Potential assignment
- Wire number / mark
- Connection part assignments (ferrules, end sleeves)

**Implementation notes:**
- In EPLAN's data model, Connections are the edges of the netlist graph; devices are nodes.
- Connection properties can be inherited from potential definitions or set explicitly.
- Connections aggregate into nets across schematic pages via cross-references.

---

### `Cable connection`
A connection established by — and associated with — a specific Cable object. Distinguished from a bare wire connection by its parent Cable assignment. Carries routing reference back to the cable designation.

**Implementation notes:**
- In reports, cable connections show the cable designation alongside the connection data.
- Used in the cable navigator to show which physical conductors carry which signals.

---

### `Connection part`
A physical accessory component used to prepare/terminate a wire end (e.g., wire ferrule, ring lug, butt splice, heat-shrink end sleeve). Assigned to a Connection object at its source and/or target end.

**Implementation notes:**
- Assigned via **Connection properties → Parts** or via **Connections navigator**.
- Drives ferrule/end-treatment BOMs in manufacturing documentation.
- Automatically quantified: one per wire end.

---

### `Connection part (assignment: source)`
The connection part assigned specifically to the source end of a wire. Example: a wire-end ferrule (DIN 46228) crimped onto the wire before insertion into a terminal.

---

### `Connection part (assignment: target)`
The connection part at the target end of the wire. May differ from the source part (e.g., ferrule at source, ring lug at target device screw terminal).

---

### `Connection part reference`
Instance reference linking a connection to its source/target part in the catalog. Enables BOM generation for all ferrules and termination accessories.

---

### `Connection part reference (assignment: source)`
Part reference resolved at the source end of a connection.

---

### `Connection part reference (assignment: target)`
Part reference resolved at the target end.

---

### `Conduit / line`
A physical cable management element (conduit, cable tray, cable duct, wire duct) represented in the wiring topology or panel layout. Defines the physical path through which cables and wires are routed.

**Implementation notes:**
- Used in EPLAN Pro Panel for 3D cable routing paths.
- Also used in topology diagrams (P8) to represent cable trays and conduit runs.
- Carries fill-level calculations for conduit sizing and compliance checks.

---

### `Connection point, external`
A connection point on a device that interfaces with external field wiring — the outward-facing terminal/pin. Mapped to terminal strip entries or cable entry points.

**Implementation notes:**
- Determines which connections appear in external wiring documentation.
- Distinguished from internal connection points in terminal strip reports.

---

### `Connection point, internal`
A connection point facing inward toward the panel's internal wiring — connecting devices within the same enclosure.

**Implementation notes:**
- Internal connection points drive the internal wiring list.
- Used to separate field wiring from panel wiring in documentation.
