---

## 9. PLC Elements

### `PLC addresses`
The I/O address mapping table for a PLC, assigning logical tag addresses to physical I/O channels. Defines the complete address space for a PLC CPU/rack in the project.

**Implementation notes:**
- Populated in the **PLC navigator** (View → Navigators → PLC).
- Address formats depend on PLC manufacturer (e.g., Siemens: `I0.0`–`I127.7`, `Q0.0`–`Q127.7`; Allen-Bradley: `I:0/0`; IEC 61131: `%IX0.0`).
- EPLAN can import PLC programs (TIA Portal, Studio 5000) to pre-populate addresses.
- Address overlaps trigger DRC errors.

---

### `PLC addresses (header object)`
Header record aggregating all address entries for a PLC unit.

---

### `PLC connection point`
An individual I/O channel terminal on a PLC I/O module, representing a single digital input, digital output, analog input, or analog output point.

**Implementation notes:**
- Placed in schematics as symbols with connection points matching the module's pin layout.
- Carries: channel address, signal type (DI/DO/AI/AO), signal description, and engineering unit.
- Linked to `Connected sensor / actuator` for full signal chain documentation.

---

### `Connected PLC connection point`
A PLC I/O connection point that has an active signal connection routed to a field device. Differentiates used channels from spare/unassigned channels in I/O lists.

**Implementation notes:**
- Only connected PLC connection points appear in active I/O lists.
- Unconnected points generate DRC warnings about unused I/O.

---

### `PLC card`
A PLC I/O module (card/blade) with a defined number of channels. Has a rack slot assignment, address range, and part reference pointing to the specific module catalog item.

**Implementation notes:**
- Defined in the PLC navigator with slot/rack position.
- Module type determines available connection points (DI 16×24VDC, AO 8×4-20mA, etc.).
- Part reference drives BOM entries for PLC hardware.

---

### `PLC card communication unit`
The communication interface module of a PLC (e.g., Profibus DP master, Profinet IO controller, EtherNet/IP adapter). Handles data exchange with field devices, drives, and HMI systems.

**Implementation notes:**
- Defined as a separate card type with communication-specific properties (network address, baud rate, DP/IO configuration).
- In EPLAN, communication units are placed as part of the PLC rack definition.