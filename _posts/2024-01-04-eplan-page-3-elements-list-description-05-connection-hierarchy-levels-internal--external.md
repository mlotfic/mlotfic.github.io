## 5. Connection Hierarchy Levels (Internal / External)

EPLAN's connection traversal engine resolves multi-hop connections across terminal strips and junction boxes. "Level" (1–3) denotes how many intermediate connection points (terminals, plugs) the wire passes through before reaching its ultimate endpoint.

---

### `Cable, external 'level (1-3)'`
A cable segment that crosses an external boundary (panel boundary, system boundary) at the specified traversal depth. Level 1 = direct external cable; Level 2 = cable after passing through one intermediate terminal; Level 3 = two intermediate terminals crossed.

**Implementation notes:**
- Drives cable schedule entries for cables leaving the local panel.
- Traversal depth is configured per project in **Settings → Projects → Connection → Cross-references**.

---

### `Cable, internal 'level (1-3)'`
A cable segment within the same enclosure/assembly at the specified traversal depth.

---

### `Connection, external 'level (1-3)'`
A direct wire (non-cable) connection that exits the local enclosure boundary at the given level. Typically appears in terminal strip diagrams showing field wiring.

---

### `Connection, internal 'level (1-3)'`
A direct wire connection within the same enclosure at the given level.

---

### `Last external target`
The ultimate external destination of a connection chain, regardless of how many intermediate terminals it passes through. Reported as the final "TO" endpoint in multi-hop wiring documentation.

**Implementation notes:**
- Critical for long wiring runs passing through multiple junction boxes.
- Used in cable schedules where the full end-to-end routing must be documented.

---

### `Last internal target`
The final internal endpoint in a multi-hop internal connection chain.

---

### `Target, external 'level (1-3)'`
An external connection endpoint at the specified traversal level. Used in terminal diagrams to show where external wires terminate.

---

### `Target, external, connection point 'level (1-3)'`
The specific connection point (terminal number, pin) at the external target at the given traversal level.

---

### `Target, external, counter-connection 'level (1-3)'`
The mating/opposite connection point at the external target — i.e., what's connected on the other side of the referenced connection point.

**Implementation notes:**
- Used in terminal strip reports to show both the terminal connection and its counter-connection for each wire.

---

### `Target, internal 'level (1-3)'`
Internal connection endpoint at the given level.

---

### `Target, internal, connection point 'level (1-3)'`
Specific connection point at the internal target.

---

### `Target, internal, counter-connection 'level (1-3)'`
Mating connection point at the internal target.
