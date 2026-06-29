---



---

## 7. PCT Loop & Instrumentation (EPLAN Instrumentation)

### `PCT loop`
A **Process Control Technology** loop object representing a complete instrumentation loop — e.g., a flow control loop `FIC-101` containing a flow transmitter, controller, and control valve. The PCT loop is the organizational unit for all instruments sharing a common process variable.

**Implementation notes:**
- Defined in the **Loop navigator** (EPLAN Instrumentation module).
- Each loop has a Loop ID (tag number), loop function (measurement type: F=flow, T=temp, P=pressure, L=level), and modifier (I=indicator, C=controller, etc.).
- Loop diagrams (instrument loop drawings per ISA 5.4) are generated from PCT loop data.
- Connected to PCT loop functions representing individual instruments.

---

### `PCT loop (header object)`
The master header record for a PCT loop, aggregating all loop functions, instruments, and wiring under one loop designation. Header properties include loop number, process area, and revision data.

---

### `PCT loop function`
A specific instrument or logical function within a PCT loop — e.g., the flow transmitter (FT-101) or the control valve (FCV-101). Each PCT loop function maps to an EPLAN device with a function definition corresponding to the instrument type.

**Implementation notes:**
- Assigned instrument tag numbers following ISA 5.1 conventions.
- PCT loop functions carry connection data (4-20 mA, HART, Foundation Fieldbus, Profibus PA) used in wiring documentation.
- Linked to PLC connection points via signal assignments.

---

### `PCT loop function (header object)`
Header record for a PCT loop function, used in reports requiring one entry per function regardless of multi-variant placements.

---

### `Connected sensor / actuator`
A field device (sensor or actuator) associated with either a PLC I/O channel or a PCT loop function. Represents the physical process instrument in the overall signal chain documentation.

**Implementation notes:**
- Links the PLC's I/O address to the field tag number.
- Appears in I/O lists, instrument index, and loop sheets.

---

### `Connected sensor / actuator per connection point`
The field device linked to a specific individual PLC connection point (I/O channel). More granular than the general `Connected sensor / actuator` — scoped to a single channel.

---