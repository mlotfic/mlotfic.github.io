## 11. Connector & Pin Elements

### `Pin`
An individual contact within a multi-pin connector. Has a pin number/designation, contact type (male/female), function assignment (signal name, potential), and connection assignment.

**Implementation notes:**
- Defined within a `Plug` object in the connector editor.
- Pin numbering follows the connector manufacturer's datasheet.
- Pins carry part references for individual contact elements (crimp contacts, solder cups, IDC contacts).

---

### `Plug`
A connector housing containing multiple pins, representing one-half of a mating connector pair. Identified by its designation (e.g., `-X10`, `-P1`) and part reference to the housing catalog item.

**Implementation notes:**
- Defined using the **Plug / Socket editor** or placed as a macro in schematics.
- Plug properties: housing part, contact count, coding/keying, IP rating.
- Associated with a counterpiece to form a complete connector pair.

---

### `Plug counterpiece`
The mating connector — the opposite gender half of a connector pair. The plug and its counterpiece together document both sides of a connector junction (e.g., cable-side plug + panel-mount receptacle).

**Implementation notes:**
- Counterpiece assignment is made in plug properties under **Counterpiece** tab.
- Both parts appear in connector BOMs.

---

### `Pin part`
Catalog part entry for an individual connector pin/contact element (e.g., crimp contact for 0.5–1.5 mm² wire, gold-plated socket contact).

---

### `Pin part reference`
Instance reference linking a placed pin to its contact catalog part. Used for crimp contact quantity calculation in connector assembly documentation.

---

### `Plug part`
Catalog part for the connector housing/body (the plastic or metal shell of the connector).

---

### `Plug part reference`
Instance reference for a placed connector housing.

---