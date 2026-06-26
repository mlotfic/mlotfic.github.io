## 10. Terminal Elements

### `Terminal`
An individual terminal block unit within a terminal strip assembly. Has a terminal number/designation, a defined function (feed-through, fuse, disconnect, PE, data), and connection points on both internal and external sides.

**Implementation notes:**
- Placed via **Terminal strip editor** (Utilities → Terminal strips).
- Terminal properties: mark, cross-section, voltage rating, color coding.
- Terminals are automatically numbered by the terminal strip editor.
- Jumper assignments and bridge definitions managed within the terminal strip.

---

### `Terminal strip`
An organized row/assembly of terminal blocks sharing a common rail (DIN rail). Identified by its designation (e.g., `-X1`, `-XT-MCC`). Contains terminals, accessories (end brackets, jumpers, labels, dividers), and the rail itself.

**Implementation notes:**
- Managed in the **Terminal strip editor**.
- Terminal strip reports: terminal diagram, wiring list, parts list.
- Strip width and rail length calculated automatically from part dimensions.
- Supports mixed terminal types (feed-through + PE + fuse + disconnect) within one strip.

---

### `Terminal strip part reference`
Part reference for the terminal strip assembly or its accessories (end brackets, partition plates, labels, cover cap, etc.).

---

### `Terminal strip parts`
Catalog parts data associated with a terminal strip, including all accessories and the rail.

---

### `Terminal part reference`
Instance reference linking a specific placed terminal to its catalog part entry.

---

### `Terminal parts`
Catalog parts data for terminal components.

---

### `Main terminal`
The primary terminal in a terminal strip performing the main feed-through or power distribution function, as distinguished from auxiliary, PE, or data terminals. Has its own part assignment.

---

### `Main terminal part`
Catalog part for the main terminal type.

---

### `Main terminal part reference`
Part reference instance for a main terminal.

---

### `Terminal connection point external`
The external (field wiring) side of a terminal's connection point, where field cables connect. This side faces outside the panel toward field instruments and motors.

---

### `Terminal connection point internal`
The internal (panel wiring) side of a terminal, connecting to internal panel devices. This side faces into the panel interior.

---

### `Terminal part reference by product subgroups`
Terminal part references grouped and reported by manufacturer product subgroup (e.g., Phoenix Contact → PT series vs. PTFIX series). Enables structured procurement by product family.

---

### `Terminal parts by product subgroups`
Terminal parts organized by manufacturer product subgroups.

---

### `Terminal strip part reference by product subgroups`
Strip-level accessories grouped by product subgroup.

---

### `Terminal strip parts by product subgroups`
Strip parts data organized by product subgroup categories.
