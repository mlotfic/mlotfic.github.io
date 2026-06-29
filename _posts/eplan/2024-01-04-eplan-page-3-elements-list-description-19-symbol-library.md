## 19. Symbol Library

### `Symbol`
A graphical representation of an electrical, fluid, or mechanical function in the EPLAN symbol library. Defines the visual appearance (lines, shapes, text fields) and the connection point layout (number, position, type) of a schematic element.

**Implementation notes:**
- Symbols are stored in symbol libraries (`.slk` files).
- Each symbol has: symbol name, variant number, logic (function definition assignment), and connection point definitions.
- IEC and NFPA symbol sets are included; custom libraries are created in the **Symbol editor**.
- Symbol properties (dynamic texts) bind to device/function properties at placement.

---

### `Symbol library`
A collection of EPLAN symbols organized by standard and discipline. Standard libraries: `IEC_symbol`, `IEC_single_symbol`, `NFPA_symbol`, `GB_symbol`, `SPECIAL`, `FLUID`, `P&ID_ISO`.

**Implementation notes:**
- Assigned to projects in **Settings → Projects → Graphical editing → Symbol library**.
- Custom symbol libraries are best practice for company-standard symbol sets.
- Library synchronization tool checks for symbol version mismatches.

---

### `Variants (all variants)`
A report display element that renders all defined project variants simultaneously side-by-side for comparison output. Used in variant summary documentation.