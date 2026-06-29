## 20. Topology & Routing Path Elements (EPLAN Pro Panel / Topology)

### `Routing path (topology)`
A defined physical path in EPLAN's **Topology** module representing the actual route a cable or wire harness follows through the plant or machine — through cable trays, conduits, floor ducts, and building structures.

**Implementation notes:**
- Defined as a network of routing path segments in the topology diagram.
- EPLAN calculates cable lengths automatically by summing routing path segment lengths.
- Critical for accurate cable length estimation and conduit fill calculations.
- Integrates with Pro Panel's 3D routing for automated wire length computation.

---

### `Routing path part (topology)`
A catalog part assigned to a routing path segment, defining the physical cable management product: cable tray, conduit, wire duct, cable ladder, or floor duct, with specific dimensions, material, and load capacity.

**Implementation notes:**
- Part assignment enables BOM generation for cable tray and conduit materials.
- Cross-section and fill-level properties support compliance with IEC 60364 installation rules.

---

### `Routing path part reference (topology)`
Instance reference linking a placed routing path segment to its catalog part. Enables length-based quantity calculation for cable tray orders (e.g., 3m sticks × required total length).