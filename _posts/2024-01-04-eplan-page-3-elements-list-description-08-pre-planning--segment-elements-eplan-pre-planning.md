## 8. Pre-planning & Segment Elements (EPLAN Pre-planning)

Pre-planning elements belong to the **EPLAN Pre-planning** module (formerly EPLAN Cogineer) used for early-stage engineering before full schematic design.

---

### `Pre-planning segment`
A logical engineering unit in the pre-planning phase representing a functional process segment (e.g., a pump station, a drive system, a heating circuit). Contains preliminary device lists, function requirements, and connection definitions that will later be elaborated into full schematics.

**Implementation notes:**
- Defined in the **Segment navigator**.
- Segments have a type (mechanical, electrical, instrumentation) and hierarchy level.
- Can be instantiated from **Segment templates** for repetitive engineering.

---

### `Pre-planning segment (header object)`
Header record for a pre-planning segment, used in summary reports.

---

### `Planning object`
A generic element in the pre-planning module representing any device, function, or system component that has been identified but not yet fully specified in schematics. Carries preliminary tag, function type, and process data.

**Implementation notes:**
- Planning objects are the pre-engineering equivalents of Devices.
- They are "promoted" to full devices as engineering progresses.
- Connected to `Source segments` and `Target segments` via connections.

---

### `Planning object (header object)`
Header record for planning objects.

---

### `Segment template`
A reusable pre-engineering template defining the standard structure of a process segment — including expected devices, connections, and property defaults. Applied to new segments for consistency and speed.

**Implementation notes:**
- Stored in the segment template library.
- When instantiated, all devices and connections from the template are copied into the new segment.
- Modifications to the template do not retroactively update existing instances.

---

### `Structure segment`
A structural definition within the pre-planning hierarchy that organizes segments by engineering discipline or system structure (e.g., Mechanical / Electrical / Instrumentation layers of the same process unit).

---

### `Structure segment (header object)`
Header record for structure segments.

---

### `Structure segment hierarchical`
A structure segment that carries a hierarchical parent–child relationship, defining the top-down breakdown from plant → unit → section → segment level.

---

### `Structure segment / Planning object`
A combined element serving dual roles — acting as both a structural container and a planning object. Used at transition boundaries in the hierarchy where a segment is itself a plannable unit.

---

### `Source segment`
The originating segment in a pre-planning connection, representing the "from" side of a planned process route or signal path.

---

### `Source segment (header object)`
Header record for source segments.

---

### `Target segment`
The destination segment in a planned connection.

---

### `Target segment (header object)`
Header record for target segments.

---

### `Superior segment`
A parent segment in the hierarchy that contains and supervises one or more subordinate segments.

---

### `Superior segment (header object)`
Header record for superior segments.

---

### `Superior structure segment`
The highest-level structural segment in the pre-planning hierarchy, representing plant or system level.

---

### `Subordinate segment`
A child segment under a `Superior segment` in the hierarchy.

---

### `Linked segments`
Pre-planning segments that have been explicitly linked to indicate a process flow, signal path, or functional relationship between them.

---

### `Linked with superior segments`
A segment that maintains a link to its parent segments — used in hierarchical traversal when generating top-down documentation.

---

### `Cable planning object`
A planning-level cable object defined in pre-planning before routing details are established. Carries preliminary data: start/end points, estimated cable type, and process area.

---

### `Placement pre-planning`
The visual/positional placement of a planning object on a pre-planning diagram page. Represents where the component appears in the process topology.

---

### `Placement pre-planning (header object)`
Header record for pre-planning placements.