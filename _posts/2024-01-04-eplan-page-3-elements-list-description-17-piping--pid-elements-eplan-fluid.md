## 17. Piping & P&ID Elements (EPLAN Fluid)

### `Piping`
A pipe run or flow line in an P&ID / hydraulic / pneumatic diagram. Represents the physical pipeline connecting instruments, vessels, and equipment. Carries process medium assignment and pipe class reference.

**Implementation notes:**
- Placed as schematic lines in EPLAN Fluid diagrams.
- Pipeline properties: medium, pipe class, nominal diameter, insulation.
- Generates piping line lists and material take-offs.

---

### `Pipe class`
A specification class defining a set of compatible piping components (fittings, flanges, valves) for a given service condition (pressure, temperature, material compatibility, corrosion allowance). Examples: `150# CS RF`, `300# SS BW`.

**Implementation notes:**
- Defined in the Fluid parts database.
- Assigned to pipe runs to enforce material/rating consistency.
- Drives automated pipe component selection in BOMs.

---

### `Pipe class (header object)`
Header record for pipe class specifications.

---

### `Piping definition`
The formal record defining a specific piping segment including medium, design pressure/temperature, material, insulation class, and painting specification.

---

### `Piping definition (header object)`
Header record for piping definitions.

---

### `Piping planning object`
A logical planning element representing a piping system or segment in pre-planning. Defines high-level piping intent before detailed P&ID work begins.

---

### `Piping planning object (header object)`
Header for piping planning objects.

---

### `Substance`
The process medium (fluid, gas, steam, slurry) flowing through a piping system. Carries chemical properties (name, CAS number, phase, hazard classification) used for safety documentation and insulation selection.

**Implementation notes:**
- Assigned to pipe runs in EPLAN Fluid.
- Substance data feeds into hazardous area documentation and ATEX classification.

---

### `Substance (header object)`
Header record for process substance definitions.

---

### `Placement P&I diagram`
The placed representation of an instrument or equipment item on a P&ID diagram page in EPLAN Fluid. Contains position coordinates and links the diagram symbol to the underlying device/planning object.

---

### `Placement P&I diagram (header object)`
Header record for P&ID placements.