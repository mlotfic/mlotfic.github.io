## 16. Potential

### `Potential`

An electrical equipotential network designation assigned to all conductors carrying the same voltage. Defines what signal/voltage level a Connection, cable core, or terminal connection carries.

**Implementation notes:**
- Potential names are assigned in **Potential definition** objects or inherited from potential rails/bus bars.
- Standard potentials in IEC projects: `L1`, `L2`, `L3`, `N`, `PE`, `24VDC`, `0VDC`, `GND`, `EARTH`.
- EPLAN uses potentials for short-circuit detection (same potential connected via conductor → OK; different potentials bridged without a device → DRC error).
- Potential tracking propagates through connections, terminals, and cable cores.
- Custom potential definitions carry additional properties (color, cross-section defaults).
