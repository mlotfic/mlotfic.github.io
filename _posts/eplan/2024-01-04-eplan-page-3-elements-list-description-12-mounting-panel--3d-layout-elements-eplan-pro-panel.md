## 12. Mounting Panel & 3D Layout Elements (EPLAN Pro Panel)

### `Mounting panel`
The physical flat surface (back plate, mounting plate) inside an enclosure on which devices are mounted. Defined by dimensions, material, thickness, and enclosure assignment.

**Implementation notes:**
- Defined in Pro Panel under **Project → Mounting layout editor**.
- Serves as the coordinate reference plane for all device placements in the 2D layout view.
- Cut-outs are placed on or around the mounting panel.

---

### `Mounting panel part`
Catalog part for the mounting panel component (e.g., a specific back-plate for an RITTAL TS8 enclosure).

---

### `Mounting panel part reference`
Instance reference for the mounting panel, enabling BOMs to include the panel plate as an ordered component.

---

### `Part placement`
The 2D or 3D physical placement record of a device or component on a mounting panel or in an enclosure. Carries X/Y/Z coordinates, orientation, and the reference to the placed device.

**Implementation notes:**
- Created when a device is dragged onto the mounting layout in Pro Panel.
- Drives interference/clearance checks between placed components.
- Required for generating assembly drawings and picking lists.

---

### `Part placement (header object)`
Header record grouping multiple part placements belonging to the same device or assembly group.

---

### `3D part placement (source)`
The 3D physical placement record of the source device in a Pro Panel layout. Links the 2D schematic source device to its 3D panel position for wiring path calculation.

---

### `3D part placement (target)`
3D placement record for the target device.

---

### `Cut-out`
A defined aperture/opening in a mounting plate, enclosure door, or gland plate for device installation or cable entry. Characterized by shape (circular, rectangular, D-sub), dimensions, and position coordinates.

**Implementation notes:**
- Generated automatically when placing devices with defined cut-out macros in Pro Panel.
- Cut-out data is exported to CNC machining files (DXF) for automated panel fabrication.
- Clearance violations between adjacent cut-outs are flagged by DRC.