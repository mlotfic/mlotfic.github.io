---

title: "EPLAN Electrical Panels Builder Examples"

description: >-
  A collection of practical examples and case studies demonstrating the application of EPLAN P8 for electrical panel builders, including real-world scenarios, design considerations, and best practices for panel layout, component selection, and documentation.
date: 2024-03-10 10:00:00 +0800
author: Mahmoud Lotfi
file_name: 2024-03-10-eplan-electrical-panels-builder-examples-1.md
categories: [EPLAN, Electrical Panels, Case Studies]
tags: [Eplan, electrical panels, case studies]
pin: False
math: true
mermaid: true
comments: true
toc: true
render_with_liquid: false

image:
  path: /assets/img/posts/eplan.jpg
  alt: EPLAN Electrical Panels Explained
  lqip: data:image/webp;base64,UklGRjoAAABXRUJQVlA4IC4AAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
---

# EPLAN P8 for Electrical Panel Builders: Installation Site vs Location Designation

## Real-World Panel Builder Scenarios

---

## **SCENARIO 1: Multi-Panel Industrial Control System**

### Project: Automotive Manufacturing Plant

**Installation Site (++):** Main Assembly Plant Building 3

```
++ Main Assembly Plant Building 3
   
   + Welding Station 1 - Control Cabinet (MCC-W1)
     ├─ Main Motor Starter (75 kW)
     ├─ Safety Relay Module
     ├─ PLC Controller
     └─ Emergency Stop Circuit
   
   + Welding Station 2 - Control Cabinet (MCC-W2)
     ├─ Main Motor Starter (75 kW)
     ├─ Cooling Fan Controller
     └─ Pressure Monitoring
   
   + Assembly Line 1 - Power Distribution Panel (PDP-A1)
     ├─ Incoming 63A Breaker
     ├─ 4× 32A Branch Breakers
     └─ RCD Protection 300mA
   
   + Assembly Line 2 - Power Distribution Panel (PDP-A2)
     ├─ Incoming 63A Breaker
     ├─ 4× 32A Branch Breakers
     └─ RCD Protection 300mA
   
   + Electrical Room B3-301 - Main MCC Panel
     ├─ Main 250A Breaker
     ├─ Transformer Secondary Disconnector
     ├─ Load Sharing Module
     └─ Power Factor Correction
   
   + Quality Control Room - Testing Panel (QC-TEST)
     ├─ Safety Interlock
     ├─ Test Circuit 1-6 (30A each)
     └─ Data Logger Interface
```

### EPLAN P8 Designations Generated
```
++Main Assembly Plant Building 3 + Welding Station 1 = Motor Starter 75kW & Schematic
++Main Assembly Plant Building 3 + Welding Station 1 = Safety Relay Module & Schematic
++Main Assembly Plant Building 3 + Assembly Line 1 = Main Breaker 63A & Single Line
++Main Assembly Plant Building 3 + Electrical Room B3-301 = MCC Distribution & Technical Data
```

### Panel Builder Data Sheet Format
```
PROJECT: Automotive Assembly Line - Building 3
PANEL DESIGNATION: ++Main Assembly Plant Building 3

LOCATION-BY-LOCATION BREAKDOWN:
┌─────────────────────────────────────────────────────────────────┐
│ LOCATION: Welding Station 1 - Control Cabinet (MCC-W1)          │
├─────────────────────────────────────────────────────────────────┤
│ Cabinet Size: 2000×800×600 mm                                   │
│ Main Supply: 3Ph 400V, 63A, TN-S                                │
│ Load: 75 kW + auxiliary circuits                                │
│ Component Count:                                                │
│   - Main Contactor: 1× AF96 (75kW @ 400V)                       │
│   - Overload Relay: 1× NZM100 (63A setting)                     │
│   - Aux Relay: 1× CR420 (dual channel safety)                   │
│   - E-Stop: 1× AC23Z (mushroom head)                            │
│   - Terminal Blocks: 80-pin arrangement                         │
│ Wiring Gauge: 16mm² (main), 2.5mm² (control)                    │
│ Assembly Time: 16 hours                                         │
│ Test Point: TP1, TP2, TP3 (voltage, current, earth)             │
└─────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│ LOCATION: Assembly Line 1 - Power Distribution Panel (PDP-A1)   │
├─────────────────────────────────────────────────────────────────┤
│ Cabinet Size: 1200×800×400 mm                                   │
│ Main Supply: 3Ph 400V, 63A, TN-S                                │
│ Branch Circuits: 4 × 32A (industrial sockets)                   │
│ Component Count:                                                │
│   - Main Breaker: 1× C63 (63A curve)                            │
│   - Branch Breakers: 4× C32 (32A curve)                         │
│   - RCD Module: 1× A300/30 (dual channel)                       │
│   - DIN Rail: 90 mm × 3 sections                                │
│   - Cable Glands: 6 (metric M25, M20)                           │
│ Assembly Time: 8 hours                                          │
│ Field Installation: Wall-mounted, 1.5m height                   │
└─────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│ LOCATION: Electrical Room B3-301 - Main MCC Panel               │
├─────────────────────────────────────────────────────────────────┤
│ Cabinet Size: 2400×1200×800 mm (floor-standing)                 │
│ Main Supply: 3Ph 400V, 250A (from transformer secondary)        │
│ Total Outgoing: 6 × 125A circuits                               │
│ Load: 350 kW continuous + transient surges                      │
│ Component Count:                                                │
│   - Main Disconnect: 1× OT250D3 (250A isolator)                 │
│   - Main Breaker: 1× NM250H (250A selective)                    │
│   - Outgoing MCBs: 6× NM125H (125A each)                        │
│   - Transformer Secondary: 1× disconnect switch                 │
│   - Busbar: 160A × 3 sections (copper, 10mm²)                   │
│   - PFC Capacitor: 1× 25 kVAr (400V)                            │
│   - Temperature Monitor: 1× TMD23 (earth fault)                 │
│ Assembly Time: 24 hours                                         │
│ Testing: 3-phase voltage check, insulation test (500V DC)       │
└─────────────────────────────────────────────────────────────────┘
```

---

## **SCENARIO 2: Food & Beverage Processing Plant**

### Project: Bottling Line with Multiple Control Zones

**Installation Site (++):** Processing Plant South Wing

```
++ Processing Plant South Wing
   
   + Filling Machine Area - Motor Control Cabinet (MCC-FM)
     ├─ Main Pump Motor (45 kW, IE3)
     ├─ Secondary Pump Motor (22 kW, IE3)
     ├─ Conveyor Drive (11 kW)
     ├─ Temperature Controller
     ├─ Pressure Transducer Interface
     └─ Emergency Stop Interlocks
   
   + Labeling Station - Control Panel (CP-LABEL)
     ├─ Labeling Motor (7.5 kW)
     ├─ Pneumatic Solenoid Valves (6 circuits)
     ├─ Vision System Interface (24VDC)
     └─ Barcode Scanner Connection
   
   + Capping & Sealing - Combined Panel (CP-CAP-SEAL)
     ├─ Capping Motor (5.5 kW)
     ├─ Sealing Motor (3 kW)
     ├─ Heater Controller (9 kW resistive)
     └─ Position Sensors
   
   + Quality Control Inspection - Testing Panel (QC-INS)
     ├─ Optical Scanner PSU
     ├─ Weight Checker PSU
     ├─ Data Logger (24VDC powered)
     └─ Reject Gate Solenoid
   
   + Packaging Area - Power Distribution (PDP-PKG)
     ├─ Main Supply 125A
     ├─ 6× Branch Circuits 32A (to packaging machines)
     ├─ Pneumatic Compressor Contactor (15 kW)
     └─ Compressed Air Dryer (3 kW)
   
   + Cleanroom Interface - Isolation Transformer Panel (ISO-CLEAN)
     ├─ Isolation Transformer 63 kVA (1:1)
     ├─ Equipotential Bonding
     └─ 4× Segregated Circuits to clean area
   
   + Utility Room SR-101 - Transformer & Distribution
     ├─ Main Transformer 250 kVA (20kV/400V)
     ├─ Primary Switching (HV)
     ├─ Secondary Distribution (250A)
     └─ Metering & Monitoring Module
```

### Panel Builder Electrical Analysis
```
INSTALLATION SITE: Processing Plant South Wing
TOTAL CONNECTED LOAD: 168.5 kW
DEMAND FACTOR: 0.75 (simultaneous operation unlikely)
DESIGN LOAD: 126.4 kW
REQUIRED SUPPLY: 250A @ 400V TN-S

LOCATION-BY-LOCATION LOAD BREAKDOWN:

┌──────────────────────────────────────────────────────────┐
│ LOCATION: Filling Machine Area (MCC-FM)                  │
├──────────────────────────────────────────────────────────┤
│ Connected Load: 45 + 22 + 11 = 78 kW                     │
│ Diversity Factor: 0.85 (motors rarely run simultaneously)│
│ Demand Load: 66.3 kW                                     │
│ Current @ 400V: I = 66300/(1.73×400×0.92) = 104.2A       │
│ Supply Circuit Breaker: 125A (Type C)                    │
│ Cable: 4×25mm² + 25mm² PE (voltage drop: 2.1%)           │
│ Installation Distance: 85m from main panel               │
│ Feeder Conduit: φ50mm PVC (underground)                  │
│ Soft Starter Required: YES (45 kW motor, soft start)     │
│ VFD Required: NO (fixed speed operations)                │
│ Harmonic Filters: YES (IE3 motors)                       │
└──────────────────────────────────────────────────────────┘

┌──────────────────────────────────────────────────────────┐
│ LOCATION: Labeling Station (CP-LABEL)                    │
├──────────────────────────────────────────────────────────┤
│ Connected Load: 7.5 + 0.5 (solenoids) = 8 kW             │
│ Demand Load: 8 kW (rarely simultaneous)                  │
│ Current @ 400V: I = 8000/(1.73×400×0.95) = 12.2A         │
│ Supply Circuit Breaker: 32A (Type C)                     │
│ Cable: 4×4mm² + 4mm² PE (voltage drop: 1.8%)             │
│ Installation Distance: 35m from main panel               │
│ 24VDC Auxiliary PSU: 480W (integrated)                   │
│ UPS Backup Required: NO                                  │
└──────────────────────────────────────────────────────────┘

┌──────────────────────────────────────────────────────────┐
│ LOCATION: Capping & Sealing (CP-CAP-SEAL)                │
├──────────────────────────────────────────────────────────┤
│ Connected Load: 5.5 + 3 + 9 = 17.5 kW                    │
│ Demand Load: 15.75 kW                                    │
│ Current @ 400V: I = 15750/(1.73×400×0.93) = 24.4A        │
│ Supply Circuit Breaker: 32A (Type B - shorter delay)     │
│ Cable: 4×6mm² + 6mm² PE (voltage drop: 2.3%)             │
│ Installation Distance: 42m from main panel               │
│ Special: Heater inrush monitored (9 kW resistive)        │
│ Contactor: AF38 dual main contactors                     │
└──────────────────────────────────────────────────────────┘

TOTAL SITE DEMAND: 126.4 kW → 250A Supply Adequate ✓
SPARE CAPACITY: ~25% for future expansion
SUPPLY TRANSFORMER: 250 kVA (typical for this load)
```

### Cable Routing Diagram (Electrical Engineering Data)
```
Main Transformer (Utility Room SR-101)
    ↓ (250A, 3Ph 400V TN-S)
    ├→ [Main MCC @ Electrical Room]
    │
    ├→ [MCC-FM @ Filling Machine] (125A, 85m, 4×25mm²+PE)
    │  ├─ Motor M1: 45 kW (soft start, contactor AF96)
    │  ├─ Motor M2: 22 kW (direct, contactor AF45)
    │  └─ Motor M3: 11 kW (direct, contactor AF30)
    │
    ├→ [CP-LABEL @ Labeling Station] (32A, 35m, 4×4mm²+PE)
    │  ├─ Motor M4: 7.5 kW (direct)
    │  └─ 24VDC PSU: 480W (for solenoids & vision)
    │
    ├→ [CP-CAP-SEAL] (32A, 42m, 4×6mm²+PE)
    │  ├─ Motor M5: 5.5 kW (direct)
    │  ├─ Motor M6: 3 kW (direct)
    │  └─ Heater: 9 kW resistive (dual contactors AF38)
    │
    ├→ [QC-INS @ Quality Control] (16A, 28m, 4×2.5mm²+PE)
    │  └─ All 24VDC PSU powered (optical scanner, weight check)
    │
    └→ [PDP-PKG @ Packaging] (63A, 52m, 4×16mm²+PE)
       ├─ Branch 1-6: 32A each (to packaging machines)
       ├─ Compressor: 15 kW (contactor AF46)
       └─ Air Dryer: 3 kW (direct)

TOTAL CABLE LENGTHS: ~282m of armored cable required
CONDUIT SYSTEM: φ50mm main, φ32mm branches
EARTHING: PME supplementary bonding at each panel location
```

---

## **SCENARIO 3: Data Center Power Distribution**

### Project: Enterprise Data Center Facility

**Installation Site (++):** Data Center Building West

```
++ Data Center Building West
   
   + Server Room W-101 (Ground Floor) - PDU Bank 1
     ├─ Main Disconnect 250A
     ├─ 4× 63A Branch PDUs (each powers 24 rack units)
     ├─ Monitoring & Control Module
     └─ Emergency Shutdown Station
   
   + Server Room W-102 (Ground Floor) - PDU Bank 2
     ├─ Main Disconnect 250A
     ├─ 4× 63A Branch PDUs
     ├─ Temperature & Humidity Monitoring
     └─ Access Control Interface
   
   + Server Room W-201 (First Floor) - PDU Bank 3
     ├─ Main Disconnect 200A
     ├─ 3× 63A Branch PDUs
     └─ Network Tap Integration
   
   + Cooling Plant Room - Chiller & Pump Control
     ├─ Main Chiller Motor (45 kW, frequency controlled)
     ├─ Backup Chiller Motor (45 kW standby)
     ├─ Circulation Pumps (2× 11 kW)
     ├─ Temperature Sensor Interface (RTD/PT100)
     └─ Alarm & Shutdown Logic
   
   + UPS Battery Room - DC Distribution & Charging
     ├─ Main Battery Charger (24V, 2000A capable)
     ├─ Battery String Monitoring (cell-level voltage)
     ├─ DC-DC Converters (multiple redundant)
     └─ System Monitoring & Logging
   
   + Main Electrical Room - Utility Interface & Metering
     ├─ Transformer Secondary Disconnect (HV isolation)
     ├─ Main Metering Cabinet (revenue grade)
     ├─ Power Distribution Unit (PDU) main
     ├─ RCD & Surge Protection Module
     └─ Remote Monitoring Interface (SNMP/Modbus)
   
   + Generator Room - Backup Power System
     ├─ Diesel Generator Controller (400 kVA)
     ├─ Automatic Transfer Switch (ATS) 630A
     ├─ Fuel Level & Temperature Monitoring
     └─ Load Shedding Relay Logic
   
   + Security & Monitoring Room - Control Systems
     ├─ Access Control PSU (24VDC, 10A)
     ├─ CCTV System PSU (24VAC)
     ├─ Fire Alarm Panel Interface
     └─ Environmental Monitoring (24VDC)
```

### Critical Electrical Data for Panel Builder
```
INSTALLATION SITE: Data Center Building West
TOTAL INSTALLED CAPACITY: 1,600 kVA (transformer sized)
TYPICAL LOAD: 800 kW (50% utilization baseline)
PEAK LOAD: 1,200 kW (80% utilization maximum)
DESIGN REDUNDANCY: N+1 (dual supply feeders from utility)

LOCATION POWER BUDGETS:
┌──────────────────────────────────────────────────────────┐
│ LOCATION: Server Room W-101 (PDU Bank 1)                 │
├──────────────────────────────────────────────────────────┤
│ Capacity: 4 × 63A circuits = 252A @ 400V = 174.5 kW      │
│ Current Usage: ~120 kW (69% utilization)                 │
│ Monitored Power: Yes (metered at each PDU)               │
│ Redundancy: Dual-fed from separate MPD main breakers     │
│ Current @ rated load: 252A (split across 4 circuits)     │
│ Cable: 4 × (4×25mm² + 25mm² PE) per PDU                  │
│ Conditioning: Isolation transformer fed (backup power)   │
│ Next Expansion: Can upgrade to 315A (4×63A+spare)        │
└──────────────────────────────────────────────────────────┘

┌──────────────────────────────────────────────────────────┐
│ LOCATION: Cooling Plant Room                             │
├──────────────────────────────────────────────────────────┤
│ Connected Load: 45 + 45 + 11 + 11 = 112 kW               │
│ Demand Load: 90 kW (chiller + 1 pump running)            │
│ Current @ 400V: I = 90000/(1.73×400×0.92) = 141A         │
│ Supply Breaker: 160A (selective curve C)                 │
│ Cable: 4×35mm² + 35mm² PE (voltage drop: 1.2% @ 250m)    │
│ VFD Required: YES (main chiller, 45 kW, variable load)   │
│ Soft Starter: NO (fixed backup chiller)                  │
│ Motor Thermistors: All motors fitted (protection)        │
│ Special: Synchronous start between primary & backup      │
│ Load-Sharing: Intelligent control (HVAC system)          │
└──────────────────────────────────────────────────────────┘

┌──────────────────────────────────────────────────────────┐
│ LOCATION: Main Electrical Room (Central MPD)             │
├──────────────────────────────────────────────────────────┤
│ Incoming Supply: Dual 400A feeders from transformer      │
│ Main Metering: Revenue-grade (±0.5% accuracy)            │
│ Total Switchboard Capacity: 630A main bus                │
│ Outgoing Circuits:                                       │
│   - W-101 PDU: 250A (direct feeder)                      │
│   - W-102 PDU: 250A (direct feeder)                      │
│   - W-201 PDU: 200A (direct feeder)                      │
│   - Cooling: 160A (direct feeder)                        │
│   - Generator ATS: 630A (direct feeder)                  │
│   - UPS Charger: 125A (direct feeder)                    │
│   - Security: 32A (direct feeder)                        │
│ Total Switchboard Capacity: 630A (suitable at N+1 config)|
│ Protection: Selective coordination (TCC curves matching) │
│ Harmonic Filtering: Yes (VFD at cooling)                 │
│ Surge Protection: Type 1 (building entry) + Type 2 (PDU) │
│ Monitoring: Powermon 6000 (SNMP/Modbus/DNP3)             │
│ Component List (Switchboard):                            │
│   - Main Disconnect: 1× OT630D3 (630A isolator)          │
│   - Main Breaker: 1× NM630N (630A, selective)            │
│   - Metering Module: 1× MT600 (3-phase 600A)             │
│   - Outgoing MCBs: 8 × NM250-400H (250-400A range)       │
│   - RCD Module: 1× MA300 (300mA dual channel)            │
│   - Busbar: 400A × 4 vertical sections (copper)          │
│   - Terminal Blocks: 160-pin industrial grade            │
│   - Condition Monitoring: Thermal camera ports           │
│ Assembly Size: 2400×2000×1000 mm (floor-standing)        │
│ Assembly Time: 48 hours (critical infrastructure)        │
└──────────────────────────────────────────────────────────┘

┌──────────────────────────────────────────────────────────┐
│ LOCATION: Generator Room (Backup Power)                  │
├──────────────────────────────────────────────────────────┤
│ Generator Size: 400 kVA (standby), 1500 rpm              │
│ Fuel Type: Diesel (on-site storage)                      │
│ Current @ full load: 400000/692 = 578A @ 400V 3Ph        │
│ ATS (Automatic Transfer Switch): 630A                    │
│ ATS Type: STS-6300 (make-before-break, 3-phase)          │
│ Transfer Time: <100ms (UPS bridge load)                  │
│ ATS Contactors: 2× AF900 (dual-source changeover)        │
│ Utility Feed Disconnect: Main ATS isolation              │
│ Generator Control Panel:                                 │
│   - Engine Controller (AMF module)                       │
│   - Frequency Monitor: 48-52 Hz acceptable               │
│   - Voltage Monitor: 380-420V acceptable                 │
│   - Load Shedding Logic: 4-tier (non-critical first)     │
│   - Fuel Level Indicator & Gauge                         │
│   - Oil Temperature & Pressure Monitoring                │
│   - Exhaust Temperature Monitor                          │
│ Fuel Supply: 5000L on-site (16-hour runtime @ 75% load)  │
│ Emission: Meets Stage 3B regulations                     │
│ Testing: Monthly test-run (30 min no-load)               │
│ Documentation: Full maintenance log required             │
└──────────────────────────────────────────────────────────┘

LOAD PROFILE (24-HOUR):
Time        Load        Supply      Notes
06:00       600 kW      Grid        Morning startup
09:00       900 kW      Grid + UPS  Peak business hours
12:00       800 kW      Grid        Steady-state
18:00       950 kW      Grid        Evening peak
22:00       500 kW      Grid        Off-peak reduced
00:00       350 kW      Grid        Maintenance window

REDUNDANCY VERIFICATION:
✓ Dual feeder system (N+1 for main supply)
✓ Generator backup (8-hour autonomy with fuel load)
✓ UPS system (15-minute battery bridge)
✓ Cooling redundancy (dual chillers, one primary + one standby)
✓ PDU redundancy (each rack has dual-corded PSUs)
```

---

## **SCENARIO 4: Chemical Plant Process Control**

### Project: Reactant Dosing & Temperature Control System

**Installation Site (++):** Chemical Plant Building C (East Wing)

```
++ Chemical Plant Building C (East Wing)
   
   + Reactor Control Room 1 - Main Process Panel (CP-REACT-1)
     ├─ Reactor Heater Circuit 1 (36 kW resistive)
     ├─ Reactor Heater Circuit 2 (36 kW resistive)
     ├─ Chiller Motor (22 kW)
     ├─ Agitator Motor (15 kW)
     ├─ Dosing Pump Motor (7.5 kW)
     ├─ Temperature Sensor Interface (PT100 RTD)
     ├─ Pressure Transducer Circuit (4-20mA)
     └─ Safety Interlocks & E-Stop
   
   + Reactor Control Room 2 - Process Panel (CP-REACT-2)
     ├─ Reactor Heater Circuit 1 (36 kW resistive)
     ├─ Reactor Heater Circuit 2 (36 kW resistive)
     ├─ Chiller Motor (22 kW)
     ├─ Agitator Motor (15 kW)
     ├─ Dosing Pump Motor (7.5 kW)
     └─ Control Interface & Monitoring
   
   + Auxiliary Equipment Room - Support Panel (SP-AUX)
     ├─ Vacuum Pump Motor (11 kW)
     ├─ Inert Gas Supply Compressor (7.5 kW)
     ├─ Ventilation Exhaust Fan (5.5 kW)
     ├─ Fume Hood Supply Fan (3 kW)
     └─ Chemical Supply Chiller (5.5 kW)
   
   + Utility Room C-201 - Main MCC & Distribution
     ├─ Main Transformer Secondary 400A
     ├─ Main Distribution Breaker
     ├─ Outgoing Breakers (to each control area)
     ├─ Harmonic Filter Module (THD control)
     └─ Power Quality Monitor
```

### Electrical Load & Cable Sizing Analysis
```
INSTALLATION SITE: Chemical Plant Building C (East Wing)
TOTAL PROCESS LOAD: 246 kW
DUTY CYCLE: Continuous (24/5 operation)
DESIGN SAFETY MARGIN: 25%
REQUIRED SUPPLY: 315A @ 400V TN-S

LOCATION 1: Reactor Control Room 1 (CP-REACT-1)
────────────────────────────────────────────────
Connected Load: (36+36+22+15+7.5) = 116.5 kW
Diversified Load: 110 kW (heaters 100%, motors 75%)
Current Required: I = 110000/(1.73×400×0.92) = 172A
Supply Breaker: 200A (Curve D for inrush resistance)
Cable Specification: 4×35mm² + 35mm² PE
Distance from Main: 120m (underground conduit)
Voltage Drop Calc: Vd = (2×L×I×R)/1000 = 2×120×172×0.00163/1000 = 0.067V = 0.016% ✓
  [Note: 35mm² Cu = 0.00163 Ω/m]
Installation Method: 4-core armored cable in buried conduit φ50mm
Earth Fault Loop: Tested <0.5Ω (measured at site)
Protection: Bi-metal thermal overload + MCB discrimination curve
Temperature Compensation: Heater thermostat ±2°C accuracy

HEATER CIRCUITS (Critical Load Segment):
├─ Heater 1: 36 kW @ 400V = 52A → CB C63 (3-pole)
├─ Heater 2: 36 kW @ 400V = 52A → CB C63 (3-pole)
├─ Cable: 2×6mm² per heater (single phase distributed)
├─ Control: Contactor AF45 + thermal overload NZM45
├─ Contactor coil: 24VDC (from dedicated PSU)
└─ Interlock: Safety relay prevents both heaters ON simultaneously

MOTOR CIRCUITS:
├─ Chiller Motor 22kW: CB C32, Cable 4×10mm²+PE, DOL starting
├─ Agitator Motor 15kW: CB C32, Cable 4×6mm²+PE, DOL starting
├─ Dosing Pump 7.5kW: CB C20, Cable 4×4mm²+PE, DOL starting

MONITORING CIRCUITS (Instrumentation):
├─ PT100 Temperature Sensor: 3-wire, 1.5mm² shielded pair
│  Signal Range: -20 to +150°C (RTD output)
│  Transmitter: DIN-rail mounted, 4-20mA output
│  Cable: Armored shielded pair (EMI immunity)
│  Distance: 35m to sensor (compensation wiring)
│
├─ Pressure Transducer: 0-10 bar → 4-20mA output
│  Mounting: Vessel flange-mounted (IP67 connector)
│  Signal Conditioning: Isolator module (galvanic isolation)
│  Cable: 2-conductor 0.75mm² shielded (50m run)
│
└─ E-Stop Circuit: 24VDC dual-channel safety relay
   Safety Rating: PNEU SIL2 Category 3
   Relay Type: CR420 (redundant contacts)
   Response Time: <10ms

LOCATION 2: Reactor Control Room 2 (CP-REACT-2)
────────────────────────────────────────────────
Configuration: IDENTICAL to CP-REACT-1
Connected Load: 116.5 kW (parallel installation)
Supply Breaker: 200A (independent feed)
Cable: Separate 4×35mm² run (parallel to Reactor 1)
Distance from Main: 115m (separate underground route)
Cross-connection: None (safety-critical separation)

LOCATION 3: Auxiliary Equipment Room (SP-AUX)
────────────────────────────────────────────────
Connected Load: (11+7.5+5.5+3+5.5) = 32.5 kW
Diversified Load: 30 kW (motors 75%, fan 100%, chiller 100%)
Current Required: I = 30000/(1.73×400×0.92) = 47A
Supply Breaker: 63A (Curve C, general purpose)
Cable: 4×10mm² + 10mm² PE
Distance from Main: 85m
Voltage Drop: 0.041V = 0.010% ✓
Installation: Above-ground conduit (machine room area)
Motors: All DOL starting (low-inertia machines)
Fans: Soft-start recommended (reduce stress on building ventilation)

LOCATION 4: Main Utility Room (MCC @ Utility C-201)
────────────────────────────────────────────────────
Incoming Supply: 400A dual feeders from 630kVA transformer
Main Distribution Architecture:
┌─────────────────────────────────────┐
│ Main Transformer Secondary 630kVA   │
│ 20kV:400V, 1000A nominal            │
└──────────────────┬──────────────────┘
                   ↓
        ┌──────────────────────┐
        │  HV Disconnect (OT80)│ ← 20kV side isolation
        │  LV Main Breaker NM1000 (1000A)
        └──────────────────────┘
                   ↓
    ┌──────────────┼──────────────┐
    ↓              ↓              ↓
 [CB-1]        [CB-2]         [CB-3]
 315A Feed    [Harmonic      [Metering]
 to Reactor   Filter]
 Room 1
    ↓              ↓              ↓
 [CP-REACT-1] [THD <5%]     [kWh Meter]
    ↓          Protection      [Power Analyzer]
 [200A Outlet]

MAIN SWITCHBOARD COMPONENTS:
├─ Main Isolator: OT630D3 (630A knife switch, HV side)
├─ Main Breaker: NM630H (630A, selective curve)
├─ Metering: MD500 (3-phase, 600A capacity)
├─ Outgoing MCBs:
│  ├─ CB1: NM315H (315A) → CP-REACT-1
│  ├─ CB2: NM315H (315A) → CP-REACT-2
│  ├─ CB3: NM100H (100A) → SP-AUX
│  ├─ CB4: NM63H (63A) → Utility Loads
│  └─ Spare: 2 breakers available
├─ RCD Protection: MA300 (300mA, dual channel)
├─ Harmonic Filter: FLW-25-7-400 (25 kVAr, 7th harmonic)
├─ Power Quality Monitor: Powermon 8000 (web interface)
└─ Busbar: 400A copper × 4 compartments

HARMONIC MITIGATION (Critical):
┌────────────────────────────────────┐
│ THD Source Analysis:                │
│ ├─ Heater coils: Minimal (resistive)│
│ ├─ Motors (DOL): 20-30% THD         │
│ ├─ Motor soft-starters: 40% THD     │
│ └─ Cumulative @ 200A: ~25% THD      │
└────────────────────────────────────┘
Mitigation: Fixed harmonic filter (25 kVAr, tuned to 7th harmonic)
Result: THD reduced to <5% (compliance with EN 61000-2-2)
Benefit: Reduced cable heating, longer equipment life

PROTECTION COORDINATION:
Time (ms)  Event                  Action
0          Short circuit occurs   All breakers see fault current
1-5        Instantaneous zone     Main breaker sees 400A+, trips instantly
5-50       Short delay zone       Outgoing breakers see current surge
50-100     Long delay zone        Thermal overload elements activate
>100       Thermal overload       Motor protection operates (12-16s @ 130%)

TCC (Time-Current Curves) verified for:
✓ Main breaker faster than outgoing breakers
✓ Motor overload slower than branch breaker
✓ All curves coordinated for selective operation
```

---

## **Panel Builder Design Checklist for EPLAN P8**

### For Each Location, Verify:

```
LOCATION DESIGNATION SETUP:
□ Unique location code assigned (e.g., "CP-REACT-1", "MCC-FM")
□ Physical address documented (building, room, coordinates)
□ Distance to main supply calculated
□ Environmental conditions noted (temp, humidity, hazardous area)

ELECTRICAL LOAD ANALYSIS:
□ Connected load calculated (sum of all devices)
□ Demand load estimated (diversity factors applied)
□ Peak inrush current identified (motor soft-start required?)
□ Voltage drop verified (<3% branch, <5% total)
□ Cable gauge selected & confirmed
□ Protective device ratings calculated

COMPONENT SELECTION:
□ Main breaker rated for full load + margin
□ Branch breakers coordinated for selective operation
□ Cable glands, shrouds, terminal blocks specified
□ Mounting hardware selected (DIN rail vs. busbar)
□ Heatsinks/cooling provisions assessed

DOCUMENTATION GENERATION:
□ Schematic diagram created (functional symbols per IEC 60617)
□ Single-line diagram for distribution (power flow)
□ Cable routing diagram (with conduit sizes)
□ Control circuit details (24VDC PSU, interlocks)
□ BOM (Bill of Materials) extracted from EPLAN database

SAFETY & COMPLIANCE:
□ Earth fault protection (RCD/FI) specified
□ Surge protection (Type 1, 2, 3) installed
□ Harmonic filtering assessed (if VFDs present)
□ Temperature monitoring provisions (thermistor/PT100)
□ Emergency stop circuits interlocked
□ Access to live parts restricted (IP54 minimum)
□ Heat dissipation adequate (thermal load calculation)

TESTING & COMMISSIONING:
□ Insulation test performed (500V DC, >10MΩ)
□ Continuity test on all circuits
□ Phase rotation verified (3-phase systems)
□ Load test at 80% rated current
□ Temperature rise verified (no component >40°C rise)
□ Final sign-off & labeling complete
```

---

## **JSON Data Format for Panel Documentation**

```json
{
  "installationSite": "Chemical Plant Building C (East Wing)",
  "designCode": "++CP-BldgC-East",
  "locations": [
    {
      "locationDesignation": "Reactor Control Room 1",
      "locationCode": "CP-REACT-1",
      "distanceFromMain": {
        "value": 120,
        "unit": "meters"
      },
      "connectedLoad": {
        "value": 116.5,
        "unit": "kW"
      },
      "diversifiedLoad": {
        "value": 110,
        "unit": "kW"
      },
      "supplyBreaker": {
        "type": "NM315H",
        "ratedCurrent": {
          "value": 200,
          "unit": "A"
        },
        "curve": "Type D"
      },
      "cableSpecification": {
        "cores": 4,
        "crossSection": {
          "value": 35,
          "unit": "mm²"
        },
        "earthing": {
          "value": 35,
          "unit": "mm²"
        },
        "voltageDrop": {
          "value": 0.016,
          "unit": "%"
        }
      },
      "components": [
        {
          "functionDesignation": "Reactor Heater 1",
          "type": "Resistive Heater",
          "power": {
            "value": 36,
            "unit": "kW"
          },
          "breaker": "C63",
          "cable": "2×6mm²"
        },
        {
          "functionDesignation": "Chiller Motor",
          "type": "Three-phase Asynchronous Motor",
          "power": {
            "value": 22,
            "unit": "kW"
          },
          "breaker": "C32",
          "cable": "4×10mm²+PE",
          "protection": "Direct-On-Line"
        },
        {
          "functionDesignation": "Temperature Sensor Interface",
          "type": "PT100 RTD Transmitter",
          "signal": "4-20mA",
          "cable": "1.5mm² armored shielded pair",
          "distance": {
            "value": 35,
            "unit": "meters"
          }
        }
      ]
    }
  ],
  "documentGeneration": {
    "schematic": "CP-REACT-1-Schematic.pdf",
    "singleLine": "CP-REACT-1-SingleLine.pdf",
    "cableRouting": "CP-REACT-1-Cabling.dwg",
    "bom": "CP-REACT-1-BOM.xlsx"
  }
}
```

---

## **Key Takeaways for Panel Builders**

1. **++ (Installation Site)** = Where your panel is located (building, facility)
2. **+ (Location Designation)** = Specific room/area (control room, electrical room)
3. **= (Function Designation)** = What the panel does (motor control, power distribution)
4. **Use this hierarchy** to generate documentation, BOMs, and cable lists automatically
5. **EPLAN P8 exports** this structure into Excel, CAD, and electrical reports
6. **Data-driven design** ensures consistency across multi-location projects

