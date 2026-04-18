# EPLAN Electric P8 — Wire vs Cable in Schematic Drawing

> **Software:** EPLAN Electric P8
> **Topic:** The fundamental difference between wires and cables in schematics — definition, behavior, documentation, and form output
> **Level:** Beginner to Intermediate

---

## The Core Concept

In everyday speech, "wire" and "cable" are used interchangeably. In EPLAN P8, they are **two completely different engineering objects** with different data, different behavior in reports, and different purposes in the schematic.

```
┌─────────────────────────────────────────────────────────────┐
│                    EPLAN DEFINITION                         │
│                                                             │
│  WIRE   = a single conductor connection between two points  │
│           (one connection, one potential, drawn as a line)  │
│                                                             │
│  CABLE  = a physical multi-core cable that groups multiple  │
│           wires together inside one outer jacket/sheath     │
│           (a container object assigned to wires)            │
└─────────────────────────────────────────────────────────────┘
```

A **wire** is always a child of a connection.
A **cable** is always a parent that owns one or more wires/conductors.

---

## Wire — Full Definition

### What is a Wire?

A wire in EPLAN is the **graphical line** you draw between two device connection points on a schematic page. Every line you draw in a circuit diagram IS a wire. It represents a single electrical conductor.

### Wire Properties

| Property | Description | Example |
|----------|-------------|---------|
| Connection color | Wire conductor color | `BK` (Black), `BU` (Blue), `RD` (Red) |
| Cross-section | Conductor area in mm² | `1.5 mm²`, `2.5 mm²`, `0.75 mm²` |
| Potential | Electrical potential assigned | `L1`, `24VDC`, `GND`, `PE` |
| Signal name | Logical signal identifier | `Emergency_Stop`, `Motor_Run` |
| From (source) | Device:pin at start of wire | `=GB1+ET1-K1:13` |
| To (destination) | Device:pin at end of wire | `=GB1+ET1-K3:A1` |
| Wire number | Auto-generated or manual ID | `W001`, `001` |
| Connection type | Type of connection | `Conductor`, `Shield`, `PE` |

### How Wires Look in a Schematic

```
   -K1          -K3
  [13]──────────[A1]
        wire
   BK 1.5mm²
   Potential: 24VDC
```

A single horizontal or vertical line connecting two component pins. EPLAN automatically:
- Assigns potential from connected symbols
- Propagates color and cross-section from connection settings
- Generates a unique wire number

### Where Wires Appear in Reports

| Report | Form | What is shown |
|--------|------|---------------|
| Connection list | `.f17` | Every wire as one row — from, to, color, cross-section, potential |
| Terminal diagram | `.f11` | Wires arriving at terminals — internal connections |
| Terminal-strip overview | `.f10` | Wire color and cross-section at each terminal |
| PLC diagram | `.f22` | Wire from terminal to PLC I/O channel |

---

## Cable — Full Definition

### What is a Cable?

A cable in EPLAN is a **physical object** — a multi-core cable with an outer jacket that groups multiple conductors together. It is NOT drawn as a line. Instead, it is **assigned to existing wires** to tell EPLAN that those wires physically run inside the same cable.

A cable is a logical grouping and procurement object. It has a type (article number), length, and routing path — but it does not create connections by itself.

### Cable Properties

| Property | Description | Example |
|----------|-------------|---------|
| Cable designation | Unique cable ID | `W1`, `W2`, `C-101` |
| Cable type | Article/type string | `NYCWY 3×1.5mm²` |
| Number of conductors | How many cores inside | `3`, `5`, `7` |
| Cross-section | Core cross-section | `1.5 mm²` |
| Voltage level | Rated voltage | `0.6/1 kV`, `300/500 V` |
| Length (manual) | Planned cable length | `15 m` |
| Length (routed) | EPLAN topology-calculated | `16.2 m` |
| From | Source end location | `=GB1+ET1-X1:1` |
| To | Destination end location | `=GB2+MCC-X2:3` |
| Shielded | Shield flag | `Yes / No` |
| Jacket color | Outer jacket color | `Black`, `Grey` |
| Outer diameter | Physical OD in mm | `12.4 mm` |
| ATEX identifier | Explosion protection class | `Ex e IIC T4` |
| Reel reference | Cable drum/reel number | `Reel-07` |

### How a Cable Looks in a Schematic

A cable is represented by a **cable definition line** — a special symbol placed across the wires that belong to it:

```
  Panel A                            Panel B
  -X1:1 ──────────────────────────── -X2:1
  -X1:2 ──────────────────────────── -X2:2    ← individual wires
  -X1:3 ──────────────────────────── -X2:3
         ┌──────────────────────┐
         │   W1  NYCWY 3×1.5    │             ← cable definition line
         │   L=15m              │
         └──────────────────────┘
```

The cable definition line crosses the wires graphically and "owns" them. In EPLAN this is inserted via **Insert → Cable definition**.

---

## Side-by-Side Comparison

| Aspect | Wire | Cable |
|--------|------|-------|
| **What it is** | Single electrical conductor | Physical multi-core cable grouping |
| **Drawn as** | A line between two pins | A cable definition line across wires |
| **Creates a connection** | ✅ Yes | ❌ No — groups existing connections |
| **Has a potential** | ✅ Yes | ❌ No |
| **Has a length** | ❌ No | ✅ Yes (manual + routed) |
| **Has a type/article** | ❌ No | ✅ Yes (from parts management) |
| **Appears in connection list** | ✅ Yes — as a row | Referenced by name in rows |
| **Appears in cable diagram** | ❌ No | ✅ Yes — `.f04` |
| **Appears in BOM** | ❌ No | ✅ Yes — `.f05` (by meter) |
| **Has color** | ✅ Yes (conductor color) | ✅ Yes (jacket color — different property) |
| **Has cross-section** | ✅ Yes (conductor area) | ✅ Yes (individual core area) |
| **Can be shielded** | ❌ No | ✅ Yes |
| **Assigned to potential** | ✅ Yes | ❌ No |
| **EPLAN object type** | Connection | Cable |
| **Inserted via** | Drawing a line | Insert → Cable definition |

---

## The Relationship Between Wire and Cable

A cable **contains** wires. The wires define the electrical connections. The cable defines the physical routing object.

```
CABLE W1 — NYCWY 3×1.5mm², 15m
│
├── Conductor 1 (BN / Brown)  →  wire:  -X1:1 → -X2:1 (L1, 1.5mm²)
├── Conductor 2 (BK / Black)  →  wire:  -X1:2 → -X2:2 (L2, 1.5mm²)
└── Conductor 3 (GY / Grey)   →  wire:  -X1:3 → -X2:3 (L3, 1.5mm²)
```

- Each wire has its own **color**, **potential**, and **connection points**
- The cable has the **type**, **length**, **shielding**, and **article number**
- When you assign a cable to a wire, the wire gets a `Cable name` and `Conductor number` property

---

## Real-World Example

**Scenario:** Motor starter cabinet connected to a motor in the field.

```
Control Panel                           Motor Terminal Box
  -X1:1 (U1) ─────────────────────────── Motor U1
  -X1:2 (V1) ─────────────────────────── Motor V1
  -X1:3 (W1) ─────────────────────────── Motor W1
  -X1:PE (PE) ────────────────────────── Motor PE
              ┌──────────────────────┐
              │  W5  NYCWY 4×2.5+E   │
              │  L=22m  0.6/1kV      │
              └──────────────────────┘
```

**The wires are:**

| Wire | Color | Cross-section | Potential | From | To |
|------|-------|---------------|-----------|------|----|
| Conductor 1 | BN | 2.5 mm² | U1 | -X1:1 | Motor U1 |
| Conductor 2 | BK | 2.5 mm² | V1 | -X1:2 | Motor V1 |
| Conductor 3 | GY | 2.5 mm² | W1 | -X1:3 | Motor W1 |
| Conductor 4 | GN/YE | 2.5 mm² | PE | -X1:PE | Motor PE |

**The cable is:**

| Cable ID | Type | Conductors | Length | Voltage | Shielded | Article |
|----------|------|------------|--------|---------|----------|---------|
| W5 | NYCWY 4×2.5+E | 4 | 22 m | 0.6/1 kV | No | — |

---

## What Appears in Which Report

### Connection List (`.f17`) — Wire-driven

Shows the **wires** — one row per conductor connection.

```
From          │ To           │ Cable │ Cond │ Color │ mm²  │ Potential
─X1:1         │ Motor U1     │ W5    │  1   │ BN    │ 2.5  │ U1
-X1:2         │ Motor V1     │ W5    │  2   │ BK    │ 2.5  │ V1
-X1:3         │ Motor W1     │ W5    │  3   │ GY    │ 2.5  │ W1
-X1:PE        │ Motor PE     │ W5    │  4   │ GN/YE │ 2.5  │ PE
```

The cable name `W5` is a **reference** — it appears in the wire's row to show which cable the conductor belongs to.

---

### Cable Diagram / Overview (`.f04`) — Cable-driven

Shows the **cable** as the primary object, with its conductors listed below.

```
Cable: W5
Type:  NYCWY 4×2.5+E
Length: 22m
From: =GB1+ET1-X1    To: Motor terminal box

  Cond │ Color  │ mm²  │ From pin │ To pin    │ Potential
  1    │ BN     │ 2.5  │ X1:1     │ Motor U1  │ U1
  2    │ BK     │ 2.5  │ X1:2     │ Motor V1  │ V1
  3    │ GY     │ 2.5  │ X1:3     │ Motor W1  │ W1
  4    │ GN/YE  │ 2.5  │ X1:PE    │ Motor PE  │ PE
```

---

### Summarized Parts List (`.f05`) — Cable as a part

The cable appears **once as a purchased item** with quantity in meters.

```
Article: NYCWY 4×2.5+E   │ Manufacturer: Lapp   │ Unit: m   │ Qty: 22
```

The individual wires do NOT appear in the BOM — only the cable as a product.

---

### Terminal Diagram (`.f11`) — Wire at terminal

Shows where each conductor lands on a terminal, including which cable it belongs to.

```
Terminal │ Internal from    │ Cable │ Cond │ Color │ mm²
X1:1     │ -K3:2            │ W5    │  1   │ BN    │ 2.5
X1:2     │ -K3:4            │ W5    │  2   │ BK    │ 2.5
X1:3     │ -K3:6            │ W5    │  3   │ GY    │ 2.5
X1:PE    │ PE busbar        │ W5    │  4   │ GN/YE │ 2.5
```

---

## Common Beginner Mistakes

| Mistake | Problem | Correct Approach |
|---------|---------|-----------------|
| Drawing a cable as lines between panels | No cable object exists — no cable report | Draw wires, then insert cable definition across them |
| Assigning wrong number of conductors to cable | Cable type says 3-core but 4 wires assigned | Match cable type to actual wires assigned |
| Forgetting to assign cable to wires | Wires exist but no cable report generated | Open cable dialog, assign each wire to a conductor |
| Using wire color for cable jacket color | Color properties are different objects | `Wire color` = conductor; `Cable jacket color` = outer sheath |
| Expecting cable to appear in connection list | Connection list shows wires, not cables | Check cable diagram (`.f04`) for cable documentation |
| Not setting cable length | Cable BOM shows 0m | Enter manual length in cable properties dialog |
| Confusing cross-section | Cable shows 3×1.5 but wires set to 2.5mm² | Cross-section on wire = conductor; on cable = type description — must match |

---

## How to Insert a Wire (Connection)

Wires are created automatically when you:
1. Draw a line between two component pins in the schematic editor
2. Use **Insert → Connection** to draw a conductor line
3. Drag from one pin connection point to another

EPLAN automatically assigns the potential from the connected symbols.

---

## How to Insert a Cable Definition

1. Draw all wires that will belong to the cable first
2. Go to **Insert → Cable definition**
3. Click and drag a cable definition line **across all wires** that belong to this cable
4. The Cable properties dialog opens — enter:
   - Cable designation (W1, W2…)
   - Cable type (from parts management or free text)
   - Length
   - Number of conductors
5. In the cable dialog, **assign each conductor to a wire**
6. Click OK

Alternatively, use the **Cable Navigator** (`Project data → Cables`) to manage all cables in one place.

---

## Summary

```
WIRE                              CABLE
────────────────────────────      ────────────────────────────
= electrical connection           = physical routing object
= drawn as a schematic line       = inserted as cable definition
= has potential & signal          = has type, length & article
= has conductor color             = has jacket color
= drives connection list          = drives cable diagram & BOM
= one wire = one connection       = one cable = many wires
= child of the circuit            = parent container of wires
```

---

## Related Files

| File | Description |
|------|-------------|
| `eplan_p8_project_structure.json` | Full metadata for all 16 project report folders |
| `README.md` | General project structure reference |
| `README_Expert_Properties.md` | Expert property reference — cable & connection properties |
| `README_All_Categories_2026.md` | All property categories including Cable data & Connection |
| `README_Form_Layout_and_Types.md` | Form layout and `.f04`, `.f17`, `.f11` type reference |
| `README_Wire_vs_Cable.md` | This file |

---

*EPLAN Electric P8 — Engineering Reference Documentation*
