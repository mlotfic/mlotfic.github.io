
# 2. Cable Elements

## `Cable`

- The logical schematic object representing a multi-conductor cable run between two points or across multiple devices.
- Acts as a container for individual cable cores/conductors.
- Carries properties:
  - cable designation,
  - routing path,
  - cable type part number,
  - cross-reference positions.

**Implementation notes:**

- Placed via the **Cable** symbol in schematics or defined in the cable navigator.
- Each conductor within the cable is represented as a separate `Connection` assigned to the cable.
- The cable designation follows project naming conventions (e.g., `W001`, `C-MCC-01`).
- Cross-references to source/target pages are auto-generated.

---

## `Cable part`

- The parts-catalog entry for the physical cable product
  - specifying manufacturer,
  - catalog number,
  - outer diameter,
  - conductor count,
  - cross-section (mm²),
  - insulation material,
  - and voltage rating.

**Implementation notes:**

- Assigned to the Cable object via **Cable properties → Parts**.
- EPLAN uses the cable part to validate conductor assignments against the part's defined conductor count.
- Required for generating cable schedules with part-level detail.

---

## `Cable part (assignment: source)`

- The cable part assignment at the originating/source end of the cable run.
- Specifies which catalog part applies from the source device's perspective when a cable changes type along its route.

**Implementation notes:**

- Relevant when a cable is split across assembly boundaries (e.g., armoured section from field to junction box, unarmoured section within panel).
- Used in structured cable documentation where both ends carry explicit part assignments.

---

## `Cable part (assignment: target)`

- Mirror of the source assignment — defines the cable part at the destination (target) end of the run.

---

## `Cable part reference`

- Instance-level reference linking a cable placement to its parts-catalog entry.
- Carries the actual part number resolved for this specific cable instance, including quantity calculations for length-based ordering.

**Implementation notes:**

- Cable length × factor = ordered quantity, automatically calculated if length property is populated.
- Appears in BOM and procurement reports.

---

## `Cable part reference (assignment: source)`

- Part reference resolved at the source end of a cable.
- Used when reporting requires end-specific part identification (e.g., source connector kit vs. field connection kit).

---

## `Cable part reference (assignment: target)`

- Part reference resolved at the target end of a cable.

---

### `Cable / connection`
A unified report element that handles both cable and direct-wire connections in the same report context. Eliminates the need for separate cable and connection report variants in mixed-wiring documentation.

**Implementation notes:**
- Used in reports where some connections are cabled and others are direct wires.
- The report engine determines whether to apply cable or connection formatting based on the actual object type.

---

### `Cable / Connection part`
Combined part element applicable to either a cable or a connection component within the unified `Cable / connection` element.

---

### `Cable / Connection part (assignment: source)` / `(assignment: target)`
Source/target-specific part assignments within the combined cable/connection element.

---

### `Cable / Connection part reference` / `(assignment: source)` / `(assignment: target)`
Part reference instances for the combined element at source and target ends respectively.

---

## 3. Cable Units & Wire Harnesses

### `Cable unit`
A logical sub-grouping within a multi-core cable that bundles a set of conductors into a functional unit. Used for complex cable types such as multi-pair data cables (where each twisted pair is a unit), screened sub-cables, or composite instrumentation cables (power + signal in one sheath).

**Implementation notes:**
- Defined in the **Cable navigator** under the parent Cable object.
- Each Cable unit can have its own part assignment (e.g., individual screened pair specification).
- Essential for IEC 60079 intrinsic safety documentation where each pair needs separate documentation.

---

### `Cable unit part`
Catalog part for the cable unit component — typically a sub-cable or sub-assembly within a larger cable structure.

---

### `Cable unit part reference`
Instance reference linking a cable unit to its catalog part.

---

### `Wire harness`
A logical assembly grouping multiple wires, cables, and connections that are physically bundled and routed together (e.g., a control cabinet harness, a machine tool wiring harness). Central element in **EPLAN Harness proD** integration workflows.

**Implementation notes:**
- Defined in Harness proD and synchronized back to EPLAN Electric P8 via the integration interface.
- Carries harness geometry data (branch lengths, diameter, bend radius) used in manufacturing.
- Generates harness drawings, nail board layouts, and cutting lists.

---

### `Wire harness part`
The catalog part for the wire harness assembly as a finished product (applicable for pre-made harnesses supplied by a vendor).

---

### `Wire harness part reference`
Instance reference linking a harness placement to its catalog part.

---