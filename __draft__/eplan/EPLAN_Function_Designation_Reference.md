# EPLAN P8 — Function Designation (`=`) Reference Guide
> Based on IEC 81346 | Expert conventions from machine building, process, energy, and infrastructure industries

---

## Table of Contents
1. [Fundamentals](#fundamentals)
2. [IEC 81346 Standard Letter Codes](#iec-81346-standard-letter-codes)
3. [Machine Building](#machine-building)
4. [Panel Building & OEM](#panel-building--oem)
5. [Process & Chemical Industry](#process--chemical-industry)
6. [Oil & Gas](#oil--gas)
7. [Water & Wastewater Treatment](#water--wastewater-treatment)
8. [Power Distribution & Energy](#power-distribution--energy)
9. [Building Automation (BAS/BMS)](#building-automation-basbms)
10. [Automotive Manufacturing](#automotive-manufacturing)
11. [Food & Beverage](#food--beverage)
12. [Pharmaceutical & Cleanroom](#pharmaceutical--cleanroom)
13. [Renewable Energy — Solar PV](#renewable-energy--solar-pv)
14. [Renewable Energy — Wind](#renewable-energy--wind)
15. [Marine & Shipbuilding](#marine--shipbuilding)
16. [Rail & Transportation](#rail--transportation)
17. [Data Centre & IT Infrastructure](#data-centre--it-infrastructure)
18. [Mining & Heavy Industry](#mining--heavy-industry)
19. [HVAC Systems](#hvac-systems)
20. [Safety & SIL Systems](#safety--sil-systems)
21. [Full Structure Examples](#full-structure-examples)
22. [Common Mistakes](#common-mistakes)
23. [Expert Tips](#expert-tips)

---

## Fundamentals

### The Three Pillars of EPLAN Referencing (IEC 81346)
```
=   Function designation     → WHAT it does
+   Location designation     → WHERE it is
-   Device designation       → WHAT it is (component tag)
```

### Structure Syntax
```
=FUNCTION+LOCATION-DEVICE

Examples:
=CTRL+MCC1-Q1        Contactor Q1, in MCC1, performing control function
=PWR+PANEL_A-F1      Fuse F1, in Panel A, in power distribution
=SAFE+DB1-K1         Relay K1, in distribution board 1, safety function
```

### Hierarchy Separator
Use `.` to add sub-levels:
```
=CTRL.PLC            PLC sub-function within control
=PWR.UPS             UPS sub-function within power
=DRIVE.AXIS1         Axis 1 sub-function within drive system
```

---

## IEC 81346 Standard Letter Codes

> Used on large infrastructure, energy, and authority-submitted projects. Required by many European utilities and EPC contractors.

| Code | Function Class | Typical Use |
|------|---------------|-------------|
| `=A` | Processing / converting energy (non-electrical to electrical) | Generators, PV inverters, fuel cells |
| `=B` | Converting physical variable to signal | Sensors, transducers, encoders |
| `=C` | Storing energy or material | Capacitors, tanks, batteries, accumulators |
| `=D` | Processing or storing information | PLCs, computers, HMIs, recorders |
| `=E` | Providing radiation or thermal energy | Heaters, lamps, UV sources |
| `=F` | Protecting against dangerous conditions | Fuses, circuit breakers, safety relays |
| `=G` | Providing electrical energy from a primary source | Batteries, UPS, power supplies |
| `=H` | Signalling or indicating | Indicator lights, alarms, buzzers, displays |
| `=K` | Processing signals or information for control | Relays, timers, logic modules |
| `=M` | Providing mechanical energy (prime movers) | Motors, actuators, cylinders |
| `=N` | Regulating or controlling a process variable | PID controllers, regulators, VFDs |
| `=P` | Measuring or testing | Meters, analyzers, test equipment |
| `=Q` | Switching or varying electrical circuits | Contactors, switches, isolators |
| `=R` | Restricting or stabilising movement or flow | Resistors, throttle valves, dampers |
| `=S` | Converting manual action to signals | Push buttons, selector switches, keyboards |
| `=T` | Converting electrical quantities | Transformers, converters, transducers |
| `=U` | Keeping objects in defined position | Clamps, brakes, locks |
| `=V` | Processing materials or products | Mixers, reactors, conveyors |
| `=W` | Conducting, transmitting or distributing energy/signals | Cables, busbars, waveguides |
| `=X` | Connecting or terminating | Terminal blocks, connectors, junction boxes |
| `=Y` | Positioning or guiding | Positioners, guides, actuators |

### IEC 81346 Example Set — Pump Station
```
=A01          Generator / energy conversion
=B01          Flow sensors
=B02          Pressure sensors
=B03          Level sensors
=C01          Battery bank / energy storage
=D01          PLC main controller
=D02          HMI panel
=F01          Motor protection
=F02          Short circuit protection
=G01          24VDC SMPS power supply
=H01          Alarm and indication
=K01          Control relays
=M01          Pump motor 1
=M02          Pump motor 2
=M03          Agitator motor
=N01          VFD for pump 1
=N02          VFD for pump 2
=P01          Flow measurement
=P02          Energy meter
=Q01          Main incoming isolator
=Q02          MCC feeders
=T01          Power transformer
=X01          Terminal junction boxes
```

---

## Machine Building

> Convention: Short descriptive English tags, 3–6 characters. Most common in European and Australian machine builders.

### General Machine
```
=CTRL          Main machine control system
=CTRL.PLC      PLC and I/O subsystem
=CTRL.HMI      Operator interface
=CTRL.SAFE     Safety logic (within control)
=PWR           Power distribution
=PWR.MAIN      Main incoming power
=PWR.UPS       Uninterruptible power supply
=PWR.24V       24VDC control power rail
=PWR.48V       48VDC power rail
=DRIVE         Drive and motion system
=DRIVE.X       X-axis servo
=DRIVE.Y       Y-axis servo
=DRIVE.Z       Z-axis servo
=DRIVE.SP      Spindle drive
=DRIVE.CONV    Conveyor drive
=SAFE          Safety system
=SAFE.ESTOP    Emergency stop circuit
=SAFE.GUARD    Guard door monitoring
=SAFE.LIGHT    Light curtain system
=SAFE.TWO      Two-hand control
=SENS          Sensing and detection
=SENS.POS      Position sensing
=SENS.PROX     Proximity detection
=SENS.TEMP     Temperature sensing
=SENS.PRESS    Pressure sensing
=ACT           Actuators
=ACT.PNEU     Pneumatic actuators
=ACT.HYD      Hydraulic actuators
=ACT.SERVO    Servo actuators
=IO            I/O expansion
=IO.DI         Digital input modules
=IO.DO         Digital output modules
=IO.AI         Analog input modules
=IO.AO         Analog output modules
=COMM          Communications
=COMM.PNET     PROFINET network
=COMM.PBUS     PROFIBUS network
=COMM.ETH      Ethernet network
=COMM.IO       IO-Link system
=LIGHT         Machine lighting
=HEAT          Enclosure heating
=FAN           Enclosure cooling / fans
```

### CNC Machine Specific
```
=CNC           CNC controller system
=CNC.AXIS      Axis control
=CNC.SPIN      Spindle control
=CNC.TOOL      Tool changer
=CNC.COOL      Coolant system
=CNC.CHIP      Chip conveyor
=CNC.PROBE     Touch probe system
=CNC.MIST      Mist extraction
=HYD           Hydraulic system
=HYD.UNIT      Hydraulic power unit
=HYD.CLAMP     Hydraulic clamping
=PNEU          Pneumatic system
=PNEU.UNIT     Pneumatic supply unit
=PNEU.CLAMP    Pneumatic clamping
=LUBE          Lubrication system
```

### Robotic Cell
```
=ROB           Robot system
=ROB.R1        Robot 1
=ROB.R2        Robot 2
=ROB.CTRL      Robot controller
=ROB.TOOL      End effector / tooling
=ROB.CONV      Infeed/outfeed conveyor
=ROB.WELD      Welding equipment
=ROB.GRIP      Gripper system
=SAFE          Cell safety system
=SAFE.FENCE    Perimeter fence monitoring
=SAFE.SCAN     Safety laser scanners
=SAFE.MUTE     Safety muting
=VISION        Vision system
=VISION.CAM    Cameras
=VISION.CTRL   Vision controller
```

---

## Panel Building & OEM

> Convention: Often minimal or single-level. Focus on what is inside the panel.

```
=               (blank — acceptable for single-panel projects)
=MAIN          Main distribution
=CTRL          Control section
=PWR           Power section
=IO            I/O section
=COMM          Communications section
=METER         Metering section
=AUX           Auxiliary circuits
=LIGHT         Lighting circuits
=HEAT          Heating circuits
```

### MCC (Motor Control Centre) Panel
```
=MCC           Motor control centre
=MCC.INC       Incoming section
=MCC.BUS       Busbar section
=MCC.FDR1      Feeder 1
=MCC.FDR2      Feeder 2
=MCC.SOFT      Softstarter section
=MCC.VFD       VFD section
=MCC.DIST      Distribution section
=AUX           Auxiliary control
=METER         Power metering
```

### Distribution Board
```
=DB            Distribution board
=DB.MAIN       Main incomer
=DB.LT         Lighting circuits
=DB.PWR        Power socket circuits
=DB.HVAC       HVAC circuits
=DB.EMERG      Emergency circuits
=DB.EDB        Essential distribution board
```

---

## Process & Chemical Industry

> Convention: Functional areas aligned to P&ID. Numbers used to distinguish parallel trains or units.

```
=U10           Unit 10 — Raw material intake
=U20           Unit 20 — Pre-treatment
=U30           Unit 30 — Reaction
=U40           Unit 40 — Separation
=U50           Unit 50 — Purification
=U60           Unit 60 — Product storage
=U70           Unit 70 — Utilities
=U80           Unit 80 — Waste treatment
=U90           Unit 90 — Packaging and dispatch
```

### Within a Unit (e.g. Reaction Unit =U30)
```
=U30.HEAT      Heating subsystem
=U30.MIX       Mixing subsystem
=U30.PRESS     Pressure control
=U30.VENT      Venting system
=U30.SAFE      Safety interlock system
=U30.SAMPLE    Sampling system
```

### Utilities
```
=UTIL          Utilities general
=UTIL.STEAM    Steam system
=UTIL.CW       Cooling water
=UTIL.CDA      Compressed dry air
=UTIL.N2       Nitrogen system
=UTIL.ELEC     Electrical utilities
=UTIL.INST     Instrument air
=UTIL.WATER    Process water
=UTIL.WASTE    Waste collection
```

### DCS / Instrumentation Split
```
=DCS           Distributed control system
=DCS.CTRL      Controllers and I/O
=DCS.HIST      Historian
=DCS.HMI       Operator workstations
=ESD           Emergency shutdown system
=F&G           Fire and gas system
=INST          Field instrumentation
=INST.FLOW     Flow instruments
=INST.PRESS    Pressure instruments
=INST.TEMP     Temperature instruments
=INST.LEVEL    Level instruments
=INST.ANAL     Analysers
```

---

## Oil & Gas

> Convention: Follows ISA / IEC 81346 hybrid. Functional groupings align to process units and safety systems.

```
=WELLHEAD      Wellhead control
=MANIFOLD      Manifold control
=SEP           Separation train
=SEP.1ST       First stage separator
=SEP.2ND       Second stage separator
=SEP.3RD       Third stage separator
=SEP.TEST      Test separator
=COMPRESS      Compression system
=COMPRESS.K1   Compressor train 1
=COMPRESS.K2   Compressor train 2
=COMPRESS.FLARE Flare knockout
=EXPORT        Export system
=EXPORT.PUMP   Export pumps
=EXPORT.METER  Fiscal metering
=EXPORT.PIPE   Pipeline interface
=UTIL          Utilities
=UTIL.FUEL     Fuel gas system
=UTIL.INST     Instrument air
=UTIL.FIRE     Firewater system
=UTIL.HVAC     HVAC and pressurisation
=UTIL.POWER    Power generation
=UTIL.UPS      UPS system
=ESD           Emergency shutdown system
=ESD.L1        ESD level 1 — process shutdown
=ESD.L2        ESD level 2 — process unit shutdown
=ESD.L3        ESD level 3 — emergency shutdown
=F&G           Fire and gas detection
=F&G.FLAME     Flame detectors
=F&G.GAS       Gas detectors
=F&G.HEAT      Heat detectors
=F&G.SMOKE     Smoke detectors
=PSD           Process safety devices (PSVs, BDVs)
=ICSS          Integrated control and safety system
=ICSS.DCS      DCS portion
=ICSS.SIS      Safety instrumented system
=ICSS.F&G      F&G controller
=TURRET        Turret system (FPSO)
=MOORING       Mooring system
=OFFL          Offloading system
```

---

## Water & Wastewater Treatment

> Convention: Process stages as function designations. Common in council, utility, and infrastructure projects.

### Water Treatment Plant
```
=INTAKE        Raw water intake
=INTAKE.SCREEN Intake screening
=INTAKE.PUMP   Intake pumping
=COAG          Coagulation dosing
=FLOC          Flocculation
=CLARI         Clarification / sedimentation
=FILT          Filtration
=FILT.RAPID    Rapid sand filtration
=FILT.SLOW     Slow sand filtration
=FILT.MEMB     Membrane filtration
=FILT.BW       Filter backwash system
=DOSE          Chemical dosing
=DOSE.CL2      Chlorine dosing
=DOSE.FLUOR    Fluoride dosing
=DOSE.LIME     Lime dosing
=DOSE.ACID     Acid dosing
=STOR          Clear water storage
=DIST          Distribution pumping
=SLUDGE        Sludge handling
=SLUDGE.THCK   Sludge thickening
=SLUDGE.DISP   Sludge disposal
=SCADA         SCADA and telemetry
=SCADA.RTU     Remote terminal units
=SCADA.COMM    Communications network
```

### Wastewater Treatment Plant
```
=INFLOW        Inlet works
=INFLOW.SCREEN Inlet screening
=INFLOW.GRIT   Grit removal
=PRIM          Primary treatment
=PRIM.SETT     Primary settlement
=PRIM.SCUM     Scum removal
=BIO           Biological treatment
=BIO.ASP       Activated sludge process
=BIO.MBR       Membrane bioreactor
=BIO.AIRLIFT   Aeration / air lift
=BIO.AIR       Aeration blowers
=SEC           Secondary settlement
=TER           Tertiary treatment
=TER.UV        UV disinfection
=TER.FILT      Sand filtration
=RETURN        Return activated sludge
=WASTE         Waste activated sludge
=SLUDGE        Sludge processing
=SLUDGE.THICK  Sludge thickening
=SLUDGE.DIGEST Anaerobic digestion
=SLUDGE.DEWATER Sludge dewatering
=SLUDGE.INCINR Sludge incineration
=BIOGAS        Biogas handling
=BIOGAS.STORE  Biogas storage
=BIOGAS.GEN    Gas to energy (CHP)
=ODOUR         Odour control
=UTIL          Site utilities
=SCADA         SCADA system
```

---

## Power Distribution & Energy

> Convention: Based on voltage levels, switchgear designations, and IEC standards. Used by utilities, EPC, and substation designers.

### HV/MV Substation
```
=GEN           Generation (if applicable)
=GEN.G1        Generator 1
=GEN.G2        Generator 2
=HV            High voltage system (e.g. 132kV, 66kV)
=HV.BUS_A      HV busbar A
=HV.BUS_B      HV busbar B
=HV.INC1       HV incoming feeder 1
=HV.INC2       HV incoming feeder 2
=HV.TIE        HV bus tie
=TX            Transformer
=TX.T1         Transformer 1
=TX.T2         Transformer 2
=TX.COOL       Transformer cooling
=TX.PROT       Transformer protection
=MV            Medium voltage system (e.g. 11kV, 6.6kV, 3.3kV)
=MV.BUS_A      MV busbar A
=MV.BUS_B      MV busbar B
=MV.TIE        MV bus tie
=MV.FDR1       MV feeder 1
=MV.FDR2       MV feeder 2
=MV.MOTOR      MV motor feeders
=LV            Low voltage system (415V / 400V)
=LV.MDB        Main distribution board
=LV.EMDB       Essential MDB
=LV.UPS        UPS system
=LV.DB1        Distribution board 1
=LV.DB2        Distribution board 2
=PROT          Protection and metering
=PROT.DIFF     Differential protection
=PROT.OVERCUR  Overcurrent protection
=PROT.EARTH    Earth fault protection
=PROT.DIST     Distance protection
=PROT.BUSBAR   Busbar protection
=SCADA         Substation automation system (SAS)
=SCADA.RTU     RTU / IED gateway
=SCADA.IED     Individual IEDs (IEC 61850)
=SCADA.HMI     Local HMI
=COMM          Protection communications
=COMM.FIBER    Fibre optic network
=COMM.PLC      Power line carrier
=EARTH         Earthing system
=LIGHTING      Substation lighting
=BATT          DC battery and charger system
=BATT.CHRG     Battery charger
=BATT.BANK     Battery bank
=BATT.DIST     DC distribution board
=HVAC          Control room HVAC
=FIRE          Fire detection and suppression
```

### UPS System
```
=UPS           UPS system
=UPS.RECT      Rectifier
=UPS.INV       Inverter
=UPS.BATT      Battery bank
=UPS.BYPASS    Static bypass
=UPS.MBP       Manual maintenance bypass
=UPS.DIST      UPS distribution board
```

---

## Building Automation (BAS/BMS)

> Convention: System type + zone or floor number. Follows ASHRAE and building services standards.

```
=BMS           Building management system (head end)
=BMS.SERVER    BMS server
=BMS.CTRL      System controllers
=BMS.FIELD     Field controllers (DDC, BCU)
=HVAC          HVAC systems
=HVAC.AHU1     Air handling unit 1
=HVAC.AHU2     Air handling unit 2
=HVAC.FCU      Fan coil units
=HVAC.CHILLER  Chiller plant
=HVAC.BOILER   Boiler plant
=HVAC.PUMP     Pumping systems
=HVAC.CT       Cooling towers
=HVAC.VAV      VAV boxes
=HVAC.ERV      Energy recovery ventilation
=LIGHTING      Lighting control
=LIGHTING.DALI DALI network
=LIGHTING.EMERG Emergency lighting
=ACCESS        Access control
=CCTV          CCTV system
=FIRE          Fire detection
=LIFT          Lift / elevator system
=POWER         Power monitoring
=POWER.METER   Smart metering
=POWER.PV      Solar PV monitoring
=SECUR         Security system
=CARPARK       Car park management
=IRRIG         Irrigation system
=WATER         Water metering
```

---

## Automotive Manufacturing

> Convention: Production line segments and process stations. Used by Tier 1 suppliers and OEMs.

```
=BODY          Body shop
=BODY.STAMP    Stamping press line
=BODY.WELD     Welding line
=BODY.WELD.R1  Welding robot group 1
=BODY.WELD.R2  Welding robot group 2
=BODY.GEO      Geometry station
=PAINT         Paint shop
=PAINT.PREP    Surface preparation
=PAINT.ED      Electro-deposition primer
=PAINT.SEAL    Sealing and underbody
=PAINT.BASE    Basecoat
=PAINT.CLEAR   Clearcoat
=PAINT.OVEN    Paint ovens
=PAINT.CONV    Conveyors
=TRIM          Trim and final assembly
=TRIM.T1       Trim line 1
=TRIM.T2       Trim line 2
=TRIM.GLASS    Glass installation
=TRIM.ELEC     Electrical installation
=CHASSIS       Chassis and drivetrain
=CHASSIS.ENG   Engine installation
=CHASSIS.TRANS Transmission
=CHASSIS.AXL   Axle and wheel
=FINAL         Final quality and test
=FINAL.ALIGN   Wheel alignment
=FINAL.TEST    End of line test
=FINAL.AUDIT   Quality audit
=CONV          Material handling conveyors
=CONV.OVERHEAD Overhead conveyor
=CONV.SKID     Skid conveyor
=CONV.AGV      AGV system
=UTIL          Plant utilities
=UTIL.COMPRESS Compressed air
=UTIL.WELD_GAS Welding gases
=UTIL.PAINT_AIR Paint supply air
```

---

## Food & Beverage

> Convention: Process stages from intake to packaging. Often follows FSSC 22000 / GMP documentation structure.

```
=RECV          Raw material receiving
=RECV.WEIGH    Weighing and intake
=RECV.STORE    Raw material storage
=CLEAN         CIP / SIP cleaning system
=CLEAN.CIP1    CIP circuit 1
=CLEAN.CIP2    CIP circuit 2
=CLEAN.SIP     Steam-in-place
=PREP          Ingredient preparation
=PREP.SIFT     Sifting and screening
=PREP.BLEND    Dry blending
=PREP.HYDRATE  Hydration / mixing
=COOK          Cooking process
=COOK.BATCH    Batch cookers
=COOK.CONT     Continuous cooker
=COOK.STEAM    Steam injection
=COOL          Cooling process
=COOL.PLATE    Plate heat exchanger
=COOL.FLASH    Flash cooling
=COOL.CHILL    Chill tunnel
=FILL          Filling and packaging
=FILL.DOSING   Dosing system
=FILL.FILL1    Filler line 1
=FILL.FILL2    Filler line 2
=FILL.SEAL     Sealing
=FILL.LABEL    Labelling
=PACK          Secondary packaging
=PACK.CART     Cartoning
=PACK.WRAP     Shrink wrap
=PACK.PALLETISE Palletising
=REFRIG        Refrigeration system
=REFRIG.COMP   Compressor rack
=REFRIG.COLD   Cold store
=REFRIG.FREEZE Freezer
=STEAM         Steam generation
=STEAM.BOILER  Boiler
=STEAM.DIST    Steam distribution
=WASTE         Waste management
=WASTE.EFFLUENT Effluent treatment
=UTIL          Site utilities
=UTIL.CDA      Compressed dry air
=UTIL.CO2      CO2 system
=UTIL.N2       Nitrogen system
=UTIL.WATER    Water treatment
```

---

## Pharmaceutical & Cleanroom

> Convention: Strict GMP documentation alignment. Function designations often mirror validation documents (URS/DQ/IQ/OQ/PQ).

```
=HVAC          HVAC / cleanroom conditioning
=HVAC.AHU1     Air handling unit 1 (Grade A/B)
=HVAC.AHU2     Air handling unit 2 (Grade C/D)
=HVAC.HEPA     HEPA filtration
=HVAC.LAF      Laminar air flow units
=HVAC.PRESS    Room pressurisation control
=HVAC.TEMP     Temperature and humidity
=WFI           Water for injection system
=WFI.STILL     WFI still / distillation
=WFI.STORE     WFI storage
=WFI.DIST      WFI distribution loop
=PW            Purified water system
=PW.RO         Reverse osmosis
=PW.EDI        Electrodeionisation
=PW.STORE      PW storage
=PW.DIST       PW distribution loop
=CIP           Clean-in-place system
=SIP           Steam-in-place system
=AUTOCLAVE     Autoclave sterilisation
=FORM          Formulation
=FORM.WEIGH    Weighing isolator
=FORM.BLEND    Blending
=FORM.GRANUL   Granulation
=FORM.COAT     Tablet coating
=FILL.VIAL     Vial filling line
=FILL.AMPUL    Ampoule filling
=FILL.SYRINGE  Syringe filling
=LYOPHIL       Lyophilisation (freeze drying)
=INSPECT       Visual inspection
=PACK          Packaging
=PACK.BLISTER  Blister packing
=PACK.LABEL    Labelling
=COLD          Cold chain
=COLD.REFRIG   Refrigerated storage
=COLD.FREEZE   Frozen storage
=BMS           Building management system
=ELOG          Electronic batch record / MES interface
=SAFE          Safety system
=SAFE.ESD      Emergency shutdown
=SAFE.ALARM    Alarm management system
```

---

## Renewable Energy — Solar PV

> Convention: Based on string configuration and inverter groupings.

```
=PV            Photovoltaic generation
=PV.STR_A      String group A
=PV.STR_B      String group B
=PV.STR_C      String group C
=SCB           String combiner boxes
=SCB.1         SCB 1
=SCB.2         SCB 2
=INV           Inverter system
=INV.1         Inverter 1
=INV.2         Inverter 2
=INV.3         Inverter 3
=XFMR          Step-up transformer(s)
=XFMR.T1       Transformer 1
=XFMR.T2       Transformer 2
=GRID          Grid connection
=GRID.POC      Point of connection
=GRID.METER    Export metering
=GRID.PROT     Grid protection relay
=BESS          Battery energy storage system
=BESS.BATT     Battery modules
=BESS.PCS      Power conversion system
=BESS.BMS      Battery management system
=BESS.HVAC     BESS HVAC
=SCADA         Plant SCADA / monitoring
=SCADA.MET     Meteorological station
=SCADA.COMM    SCADA communications
=CTRL          Site plant controller
=FIRE          Fire detection
=CCTV          CCTV and security
=UTIL          Site auxiliary power
=UTIL.TXAUX    Auxiliary transformer
=UTIL.DB       Auxiliary distribution board
```

---

## Renewable Energy — Wind

> Convention: Turbine-based with site level groupings.

```
=WTG           Wind turbine generator
=WTG.T01       Turbine 01
=WTG.T02       Turbine 02
=WTG.T03       Turbine 03
=WTG.NACELLE   Nacelle systems
=WTG.TOWER     Tower systems
=WTG.BLADE     Blade pitch system
=WTG.YAW       Yaw system
=WTG.GEAR      Gearbox and drivetrain
=WTG.GEN       Generator
=WTG.CONV      Power converter
=ARRAY         Array cable system
=ARRAY.C1      Array circuit 1
=ARRAY.C2      Array circuit 2
=OSS           Offshore substation (offshore)
=OSS.MV        MV switchgear
=OSS.HV        HV switchgear
=OSS.TX        Offshore transformer
=OSS.AUX       Auxiliary systems
=ONSHORE       Onshore substation
=ONSHORE.TX    Onshore transformer
=ONSHORE.GRID  Grid connection
=SCADA         Wind farm SCADA
=SCADA.MET     Metmast
=SCADA.COMM    Comms network
=SAFE          Safety and ice detection
```

---

## Marine & Shipbuilding

> Convention: Follows IACS / classification society standards. Ship systems and compartments used.

```
=PROPUL        Propulsion system
=PROPUL.ME1    Main engine 1
=PROPUL.ME2    Main engine 2
=PROPUL.GEAR   Gearbox
=PROPUL.PROP   Propeller / shaft
=PROPUL.BOW    Bow thruster
=PROPUL.STERN  Stern thruster
=ELECT         Electrical power generation
=ELECT.DG1     Diesel generator 1
=ELECT.DG2     Diesel generator 2
=ELECT.DG3     Emergency generator
=ELECT.SW      Main switchboard
=ELECT.ESW     Emergency switchboard
=ELECT.DIST    Distribution switchboards
=BRIDGE        Bridge systems
=BRIDGE.NAV    Navigation systems
=BRIDGE.COMM   Communications
=BRIDGE.DP     Dynamic positioning
=BRIDGE.AIS    AIS / GMDSS
=CARGO         Cargo systems
=CARGO.PUMP    Cargo pumps
=CARGO.TANK    Tank monitoring
=CARGO.INERT   Inert gas system
=STAB          Stability systems
=STAB.BALLAST  Ballast system
=STAB.HEEL     Heel correction
=FIRE          Fire detection and suppression
=FIRE.CO2      CO2 flooding
=FIRE.SPRINK   Sprinkler system
=BILGE         Bilge system
=HVAC          HVAC and ventilation
=SAFE          Safety management system
=HULL          Hull monitoring
=ENGINE_RM     Engine room monitoring
=SCADA         Integrated automation system (IAS)
```

---

## Rail & Transportation

> Convention: Aligned to subsystem codes used in rail projects (EN 50128, EN 50129). RAMS-driven.

```
=TRAC          Traction power system
=TRAC.OCS      Overhead contact system
=TRAC.SS       Traction substations
=TRAC.RETURN   Return current system
=SIGNAL        Signalling system
=SIGNAL.ATP    Automatic train protection
=SIGNAL.ATO    Automatic train operation
=SIGNAL.ATS    Automatic train supervision
=SIGNAL.INTLK  Interlocking
=COMMS         Communications
=COMMS.RADIO   Radio system
=COMMS.SCADA   SCADA / TIMS
=COMMS.PA      Passenger announcement
=COMMS.CCTV    CCTV
=PLATFORM      Platform systems
=PLATFORM.PSD  Platform screen doors
=PLATFORM.LIFT Lifts and escalators
=PLATFORM.DISP Passenger displays
=DEPOT         Depot systems
=DEPOT.WASH    Train wash
=DEPOT.FUEL    Fuelling / charging
=DEPOT.MAINT   Maintenance equipment
=TUNNEL        Tunnel systems
=TUNNEL.VENT   Tunnel ventilation
=TUNNEL.FIRE   Tunnel fire and life safety
=TUNNEL.DRAIN  Drainage and pump sumps
=TRACK         Track equipment
=TRACK.SWITCH  Track switches and points
=TRACK.HEAT    Track heating
=SAFE          Safety and SIL systems
=POWER         Auxiliary power
=POWER.LV      Station LV distribution
=POWER.UPS     UPS systems
=LIGHTING      Station and tunnel lighting
=LIGHTING.EMERG Emergency lighting
```

---

## Data Centre & IT Infrastructure

> Convention: Tier classification aligned. Follows TIA-942 / EN 50600.

```
=POWER         Power distribution
=POWER.UTIL    Utility incoming
=POWER.GENSET  Generator sets
=POWER.ATS     Automatic transfer switches
=POWER.UPS_A   UPS system A
=POWER.UPS_B   UPS system B
=POWER.PDU_A   PDU A side
=POWER.PDU_B   PDU B side
=POWER.RPP     Remote power panels
=POWER.FLOOR   Floor PDUs
=POWER.METER   Power metering
=COOL          Cooling system
=COOL.CHILLER  Chiller plant
=COOL.CRAC     Computer room air conditioners
=COOL.CRAH     Computer room air handlers
=COOL.RDHx     Row/rack cooling
=COOL.CT       Cooling towers
=COOL.PUMP     Chilled water pumps
=COOL.ECON     Economiser / free cooling
=NETW          Network infrastructure
=NETW.CORE     Core switches
=NETW.DIST     Distribution switches
=NETW.ACCESS   Access layer
=NETW.OOB      Out-of-band management
=NETW.FIBER    Fibre backbone
=FIRE          Fire detection and suppression
=FIRE.VESDA    VESDA early warning
=FIRE.SUPPRS   Suppression system (FM200, Novec)
=DCIM          Data centre infrastructure management
=DCIM.ENV      Environmental monitoring
=DCIM.POWER    Power chain monitoring
=DCIM.ASSET    Asset management
=ACCESS        Physical access control
=CCTV          CCTV system
=SAFE          Safety and emergency
=SAFE.ESD      Emergency power off (EPO)
=STRUCT        Structured cabling
=STRUCT.MDA    Main distribution area
=STRUCT.HDA    Horizontal distribution area
=STRUCT.ZDA    Zone distribution area
```

---

## Mining & Heavy Industry

> Convention: Mining process stages and areas. Common in APAC and African mining projects.

```
=MINE          Mining operation
=MINE.DRILL    Drilling system
=MINE.BLAST    Blast management
=MINE.HAUL     Haul road and truck dispatch
=MINE.DWATER   Dewatering
=CRUSH         Crushing plant
=CRUSH.PRI     Primary crusher
=CRUSH.SEC     Secondary crusher
=CRUSH.TERT    Tertiary crusher
=CRUSH.SCRN    Screening
=GRIND         Grinding circuit
=GRIND.SAG     SAG mill
=GRIND.BALL    Ball mill
=GRIND.CYCL    Cyclones
=FLOAT         Flotation circuit
=FLOAT.ROUGH   Rougher cells
=FLOAT.CLEAN   Cleaner cells
=FLOAT.SCAV    Scavenger cells
=REAGENT       Reagent dosing
=REAGENT.LIME  Lime dosing
=REAGENT.COLL  Collector
=REAGENT.FROTH Frother
=THICKEN       Thickening
=THICKEN.CONC  Concentrate thickener
=THICKEN.TAIL  Tailings thickener
=FILTER        Filtration
=FILTER.DISC   Disc filter
=FILTER.PRESS  Filter press
=CONVEYOR      Conveyor systems
=CONVEYOR.C1   Conveyor 1
=CONVEYOR.C2   Conveyor 2
=CONVEYOR.OLC  Overland conveyor
=WATER         Water circuit
=WATER.FRESH   Fresh water
=WATER.PROC    Process water
=WATER.RECLAIM Reclaim water
=TAILS         Tailings management
=TAILS.PIPE    Tailings pipeline
=TAILS.DAM     Tailings storage facility
=POWER         Site power distribution
=POWER.GRID    Grid connection / bulk supply
=POWER.SS1     Substation 1
=POWER.SS2     Substation 2
=COMM          Site communications
=SAFE          Safety systems
```

---

## HVAC Systems

> Convention: Equipment type with zone or air handling unit number.

```
=AHU           Air handling units
=AHU.AHU01     AHU 01
=AHU.AHU02     AHU 02
=AHU.AHU03     AHU 03 (fresh air)
=FCU           Fan coil units
=FCU.L1        Level 1 FCUs
=FCU.L2        Level 2 FCUs
=VAV           VAV system
=VAV.ZONE_A    Zone A VAV
=VAV.ZONE_B    Zone B VAV
=CHILLER       Chiller plant
=CHILLER.CH1   Chiller 1
=CHILLER.CH2   Chiller 2
=CHILLER.CH3   Standby chiller
=BOILER        Boiler plant
=BOILER.B1     Boiler 1
=BOILER.B2     Boiler 2
=PUMP          Pumping systems
=PUMP.CHW      Chilled water pumps
=PUMP.HW       Heating water pumps
=PUMP.CW       Condenser water pumps
=CT            Cooling towers
=CT.CT1        Cooling tower 1
=CT.CT2        Cooling tower 2
=VENT          Mechanical ventilation
=VENT.SUPPLY   Supply air
=VENT.EXHAUST  Exhaust air
=VENT.SMOKE    Smoke exhaust
=VENT.CARPARK  Carpark ventilation
=CTRL          BMS / controls
=REFRIG        Refrigerant system
=HEX           Heat exchangers
=BMS           Building management interface
```

---

## Safety & SIL Systems

> Convention: Safety layers and safety functions. Aligned to IEC 61508 / IEC 61511.

```
=SIS           Safety instrumented system (overall)
=SIS.SIL1      SIL 1 functions
=SIS.SIL2      SIL 2 functions
=SIS.SIL3      SIL 3 functions
=SIF           Safety instrumented functions
=SIF.SF001     Safety function 001 (e.g. high pressure shutdown)
=SIF.SF002     Safety function 002 (e.g. high temperature shutdown)
=SIF.SF003     Safety function 003 (e.g. high level shutdown)
=ESD           Emergency shutdown system
=ESD.L1        Process shutdown (PSD)
=ESD.L2        Emergency shutdown (ESD)
=ESD.L3        Abandon platform (APS — offshore)
=BPCS          Basic process control system
=F&G           Fire and gas system
=F&G.ZONE_A    Fire zone A
=F&G.ZONE_B    Fire zone B
=SAFE.ESTOP    Emergency stop system
=SAFE.GUARD    Guarding / access interlock
=SAFE.SAFE_IO  Safety I/O modules
=SAFE.LOGIC    Safety PLC / logic solver
=SAFE.VALVE    Safety valves (SDV, BDV, XV)
=RELIEF        Pressure relief system
=RELIEF.PSV    Pressure safety valves
=RELIEF.FLARE  Flare / vent system
=GROUNDING     Earthing and bonding
=GROUNDING.LPS Lightning protection
=GROUNDING.STAT Static bonding
```

---

## Full Structure Examples

### Example 1 — Water Pump Station (small project)
```
Full tag:   =CTRL+DB1-K1
Meaning:    Control relay K1, located in distribution board DB1, performing control function

Full tag:   =PWR+MCC1-Q3
Meaning:    Contactor Q3, in MCC1, power distribution function

Full tag:   =SAFE+MCC1-F1
Meaning:    Motor protection relay F1, in MCC1, safety function

Full tag:   =INST+FIELD-FT101
Meaning:    Flow transmitter FT101, in field, instrumentation function

Full tag:   =SCADA+CTRL_ROOM-PLC1
Meaning:    PLC1, in control room panel, SCADA function
```

### Example 2 — Manufacturing Cell (multi-level)
```
=CTRL.PLC+CP1-CPU         PLC CPU in control panel CP1
=CTRL.IO+CP1-DI01         Digital input module in CP1
=DRIVE.X+CP1-VFD_X        X-axis VFD in CP1
=SAFE.GUARD+CP1-F3_SAFE   Safety relay for guarding in CP1
=CTRL.HMI+OP1-TP700       HMI touchpanel at operator station OP1
=ACT.PNEU+MACHINE-CYL1    Pneumatic cylinder 1 on machine
=SENS.POS+MACHINE-B1      Proximity sensor B1 on machine
```

### Example 3 — Substation (IEC 81346 strict)
```
=T1+PAN_1-F1              Transformer T1 protection, panel 1, fuse F1
=Q1.PROT+PAN_1-K21        Feeder Q1 overcurrent relay in panel 1
=G1+BATT_RM-G1            DC battery bank G1 in battery room
=D1+CTRL_RM-PLC           RTU/PLC D1 in control room
=H1+PAN_1-HL1             Alarm indicator H1 in panel 1
```

---

## Common Mistakes

| ❌ Wrong | ✅ Correct | Reason |
|----------|------------|--------|
| `=PANEL_A` | `+PANEL_A` | Panel A is a location, not a function |
| `=MOTOR_1` | `-M1` or `+LOC-M1` | Motor 1 is a device, not a function |
| `=CABINET_3` | `+CAB3` | Cabinet is a location |
| `=ELECTRICAL` | `=PWR` or `=CTRL` | Too vague — what function? |
| `=PLANT` | `+PLANT` | Plant is a location |
| Mixing conventions mid-project | Pick one and stick to it | Consistency is critical |
| Over-nesting: `=A.B.C.D.E` | Max 2–3 levels | Deep nesting causes report issues |
| Using spaces: `=CTRL PWR` | `=CTRL.PWR` | Spaces break EPLAN structure |
| Starting with number: `=1CTRL` | `=CTRL1` | Numbers must not lead in IEC 81346 |

---

## Expert Tips

### 1. Agree with the client before starting
> Ask: *"How do you mentally divide your system?"* Use their language.

### 2. Match your `=` structure to the P&ID or SLD
> If the P&ID has units U10–U90, your EPLAN `=` should mirror that.

### 3. Keep it short
> `=CTRL` is better than `=MAIN_CONTROL_SYSTEM`. Tags appear in reports — long names truncate.

### 4. Reserve `=Z` or `=MISC` for exceptions
> Always have a catch-all so unclassified circuits have somewhere to go without breaking the structure.

### 5. Create a designation key page
> Use page type `EAC` (Explanatory documents) to document what each `=` designation means. Future engineers will thank you.

### 6. Don't create too many top-level designations
> 5–15 top-level `=` entries is ideal. More than 20 and the project becomes hard to navigate.

### 7. Consider report filtering from day one
> Every `=` designation becomes a filter in EPLAN reports. Good designations = useful, filterable BOMs and connection lists.

### 8. Validate with a test page early
> Create one page per `=` designation at the start. Check that your filter logic, page numbering, and report output all work as expected before building out the full project.

---

*Based on IEC 81346 | IEC 61355 | IEC 61511 | ISA-5.1 | TIA-942 | EN 50600 | IACS*
*Expert conventions compiled from machine building, process, energy, infrastructure, and maritime industries*
