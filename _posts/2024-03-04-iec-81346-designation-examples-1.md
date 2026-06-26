## Full Tag Examples — Complete Projects

### Example 1 — DOL Motor Starter in MCC

```cs
=PWR.INC+MCC1.INC-QF_INC                
    =function: power Incoming, Section: incomer, 
    -Device: circuit breaker (switching/protection), suffix: incomer, 
    +Location: Motor Control Centre #1 incomer
=METER+MCC1.INC-CT_INC
    =function: meter, 
    -Device: current transformer (measurement), suffix: incomer
    +Location: Motor Control Centre #1, Section: incomer
=METER+MCC1.INC-PQ1
    =function: meter, 
    -Device: power quality analyser #1, 
    +Location: Motor Control Centre #1, Section: incomer
=MOTOR.DOL+MCC1.M01-QF1
    =function: motor, Section: DOL, 
    -Device: circuit breaker, suffix: M01, 
    +Location: Motor Control Centre #1, Section: M01
=MOTOR.DOL+MCC1.M01-F_MOTOR1
    =function: motor DOL, Section: MCC1, 
    -Device: protection relay, suffix: M01, 
    +Location: Motor Control Centre #1, Section: M01
=MOTOR.DOL+MCC1.M01-KM_MAIN
    =function: motor DOL, Section: MCC1, 
    -Device: motor contactor, suffix: M01, 
    +Location: Motor Control Centre #1, Section: M01
=CTRL+MCC1.M01-SS_LOCAL                 Local/remote selector
=CTRL+MCC1.M01-SB_START                 Start push button
=CTRL+MCC1.M01-SB_STOP                  Stop push button
=CTRL+MCC1.M01-HL_RUN                   Run indicator lamp
=CTRL+MCC1.M01-HL_TRIP                  Trip indicator lamp
=CTRL+MCC1.M01-X1                       Terminal block (field wiring)
=MOTOR+FIELD-M1                         Motor (in field)
```

### Example 2 — Star-Delta Starter

```cs
=MOTOR.STAR_D+MCC1.M02-QF1             Feeder MCCB
=MOTOR.STAR_D+MCC1.M02-F_MOTOR2        Motor protection relay
=MOTOR.STAR_D+MCC1.M02-KM_MAIN         Line contactor
=MOTOR.STAR_D+MCC1.M02-KM_STAR         Star contactor
=MOTOR.STAR_D+MCC1.M02-KM_DELTA        Delta contactor
=MOTOR.STAR_D+MCC1.M02-KT_SD           Star-delta timer
=CTRL+MCC1.M02-SB_START                Start button
=CTRL+MCC1.M02-SB_STOP                 Stop button
=CTRL+MCC1.M02-HL_STAR                 Star mode indicator
=CTRL+MCC1.M02-HL_DELTA                Delta mode indicator
=CTRL+MCC1.M02-HL_TRIP                 Trip indicator
=MOTOR+FIELD-M2                        Motor (in field)
```

### Example 3 — PLC Control Panel

```cs
=PWR.CTRL+CP1.POWER-QF_MAINS           Mains incoming MCB
=PWR.24V+CP1.POWER-PS1                 24VDC SMPS primary
=PWR.24V+CP1.POWER-PS2                 24VDC SMPS redundant
=PWR.UPS+CP1.POWER-UPS_BUF1            24VDC UPS buffer module
=PWR.24V+CP1.DIST_24V-FT1              PLC fused terminal block
=PWR.24V+CP1.DIST_24V-FT2              I/O fused terminal block
=PWR.24V+CP1.DIST_24V-FT3              Field sensor fused terminal
=CTRL.PLC+CP1.PLC-CPU1                 PLC CPU
=CTRL.IO+CP1.IO-DI01                   Digital input module 01
=CTRL.IO+CP1.IO-DO01                   Digital output module 01
=CTRL.IO+CP1.IO-AI01                   Analog input module 01
=CTRL.COMM+CP1.COMM-CM_PN1             PROFINET module
=CTRL.SAFE+CP1.SAFE-F3_ESTOP           E-stop safety relay
=CTRL.SAFE+CP1.SAFE-F3_GUARD           Guard door safety relay
=CTRL+CP1.RELAY-K_WD                   Watchdog relay
=CTRL.HMI+CP1.DOOR.HMI-TP_700         HMI touchpanel
=SAFE.ESTOP+CP1.DOOR.OP-SB_ESTOP       E-stop push button
=CTRL+CP1.DOOR.OP-SS_MODE              Mode selector
=CTRL+CP1.DOOR.OP-SB_RESET             Reset button
=CTRL+CP1.DOOR.OP-HL_POWER            Power indicator
=CTRL+CP1.DOOR.OP-HL_RUN              Run indicator
=CTRL+CP1.DOOR.OP-HL_FAULT            Fault indicator
=CTRL+CP1.TERM.DI-X_DI1               DI terminal block
=CTRL+CP1.TERM.AI-X_AI1               AI terminal block
=CTRL+CP1.TERM.SAFE-X_SAFE1           Safety terminal block
```

### Example 4 — Process Instrumentation Loop (Flow)

```cs
=INST+FIELD-FE101                      Flow element (orifice plate)
=INST+FIELD-FT101                      Flow transmitter (HART 4-20mA)
=INST+INST_CAB_01.BARRIER.AI-Z_FT101   Zener barrier for FT101
=INST+MARSH_CAB_A.AI-X_AI_FT101       Marshalling terminal block
=DCS.IO+DCS_CAB1.IO_RACK_A-AI01       DCS AI card (receives FT101 signal)
=DCS+CTRL_RM.DESK1.PC_HMI1-WS_DCS1   DCS HMI workstation
=PWR+MCC1.M01-KM_MAIN                 Pump contactor (flow control output)
```

### Example 5 — MV Switchgear Feeder Panel

```cs
=MV.FDR+MV_SW1.FDR_1-QB1             
    =function: Medium Voltage, sub-function: Feeder, 
    -Device: VCB (switching/protection), 
    +Location: MV Switchgear 1, section : Feeder 1
=MV.FDR+MV_SW1.FDR_1-QD1             
    =function: Medium Voltage, sub-function: Feeder, 
    -Device: Line disconnector (switching), 
    +Location: MV Switchgear 1, section : Feeder 1
=MV.FDR+MV_SW1.FDR_1-QE1             
    =function: Medium Voltage, sub-function: Feeder, 
    -Device: Earth switch, 
    +Location: MV Switchgear 1, section : Feeder 1
=MV.FDR+MV_SW1.FDR_1-CT1             
    =function: Medium Voltage, sub-function: Feeder, 
    -Device: Protection CT phase A, 
    +Location: MV Switchgear 1, section : Feeder 1
=MV.FDR+MV_SW1.FDR_1-CT2             
    =function: Medium Voltage, sub-function: Feeder, 
    -Device: Protection CT phase B, 
    +Location: MV Switchgear 1, section : Feeder 1
=MV.FDR+MV_SW1.FDR_1-CT3             
    =function: Medium Voltage, sub-function: Feeder, 
    -Device: Protection CT phase C, 
    +Location: MV Switchgear 1, section : Feeder 1
=PROT.OC+MV_SW1.FDR_1-F_OC1          
    =function: protection, sub-function: overcurrent, 
    -Device: overcurrent protection device, 
    +Location: MV Switchgear 1, section : Feeder 1
=PROT.EF+MV_SW1.FDR_1-F_EF1          
    =function: protection, sub-function: earth fault, 
    -Device: earth fault protection device, 
    +Location: MV Switchgear 1, section : Feeder 1
=METER+MV_SW1.FDR_1-PQ1              
    =function: Medium Voltage, sub-function: Feeder, 
    -Device: Power quality analyser, 
    +Location: MV Switchgear 1, section : Feeder 1
=CTRL+MV_SW1.FDR_1-CLOSING_COIL1     
    =function: Medium Voltage, sub-function: Feeder, 
    -Device: VCB closing coil, 
    +Location: MV Switchgear 1, section : Feeder 1
=CTRL+MV_SW1.FDR_1-TRIP_COIL1        
    =function: Medium Voltage, sub-function: Feeder, 
    -Device: VCB trip coil 1, 
    +Location: MV Switchgear 1, section : Feeder 1
=CTRL+MV_SW1.FDR_1-TRIP_COIL2        
    =function: Medium Voltage, sub-function: Feeder, 
    -Device: VCB trip coil 2 (backup), 
    +Location: MV Switchgear 1, section : Feeder 1
=CTRL+MV_SW1.FDR_1-ANTI_PUMP_K1      
    =function: Medium Voltage, sub-function: Feeder, 
    -Device: Anti-pump relay, 
    +Location: MV Switchgear 1, section : Feeder 1
=CTRL+MV_SW1.FDR_1-HL_CLOSED         
    =function: Medium Voltage, sub-function: Feeder, 
    -Device: Breaker closed indicator (red), 
    +Location: MV Switchgear 1, section : Feeder 1
=CTRL+MV_SW1.FDR_1-HL_OPEN
    =function: Medium Voltage, sub-function: Feeder, 
    -Device: Breaker open indicator (green), 
    +Location: MV Switchgear 1, section : Feeder 1
=CTRL+MV_SW1.FDR_1-SB_CLOSE          
    =function: Medium Voltage, sub-function: Feeder, 
    -Device: Close push button, 
    +Location: MV Switchgear 1, section : Feeder 1
=CTRL+MV_SW1.FDR_1-SB_OPEN           
    =function: Medium Voltage, sub-function: Feeder, 
    -Device: Open push button, 
    +Location: MV Switchgear 1, section : Feeder 1
=CTRL+MV_SW1.FDR_1-SS_LOCAL          
    =function: Medium Voltage, sub-function: Feeder, 
    -Device: Local/remote selector, 
    +Location: MV Switchgear 1, section : Feeder 1
=CTRL+MV_SW1.FDR_1-X1                
    =function: Medium Voltage, sub-function: Feeder, 
    -Device: Control wiring terminal strip, 
    +Location: MV Switchgear 1, section : Feeder 1
=DC+MV_SW1.FDR_1-QF_DC1              
    =function: Medium Voltage, sub-function: Feeder, 
    -Device: DC MCB for trip circuit, 
    +Location: MV Switchgear 1, section : Feeder 1
```

### Example 6 — Safety PLC SIL2 Shutdown Loop

#### Field sensing
```sql
=SIS.IO+FIELD-PT201A
    =function: safety shutdown System, sub-function: Input/Output 
    -Device: Pressure transmitter A (SIL2 — 2oo3),
    +Location: Field
=SIS.IO+FIELD-PT201B
    =function: safety shutdown System, sub-function: Input/Output 
    -Device: Pressure transmitter B (SIL2 — 2oo3),
    +Location: Field
=SIS.IO+FIELD-PT201C
    =function: safety shutdown System, sub-function: Input/Output 
    -Device: Pressure transmitter C (SIL2 — 2oo3),
    +Location: Field
```
#### Marshalling

```sql
=SIS.IO+MARSH_CAB_B.DI_SAFE-X_PT201
    =function: safety shutdown System, Section: Input/Output 
    -Device: Safety PT terminal (2oo3 wiring),
    +Location: Marshalling cabinet
=SIS.IO+MARSH_CAB_B.BARRIER_S-Z_PT201A
    =function: safety shutdown System, Section: Input/Output 
    -Device: Safety barrier for PT201A,
    +Location: Marshalling cabinet
```
#### SIS Logic Solver

```sql
=SIS.IO+SIS_CAB1.IO_A-DI_S01_A
    =function: safety shutdown System, Section: Input/Output 
    -Device: Safety DI module (1oo2D architecture),
    +Location: SIS Logic Solver
=SIS.IO+SIS_CAB1.IO_B-DI_S01_B
    =function: safety shutdown System, Section: Input/Output 
    -Device: Safety DI module B,
    +Location: SIS Logic Solver
=SIS.LOGIC+SIS_CAB1.LOGIC_A-CPU_S_A
    =function: safety shutdown System, Section: Logic 
    -Device: SIS logic solver A,
    +Location: SIS Logic Solver
=SIS.LOGIC+SIS_CAB1.LOGIC_B-CPU_S_B
    =function: safety shutdown System, Section: Logic 
    -Device: SIS logic solver B,
    +Location: SIS Logic Solver
=SIS.POWER+SIS_CAB1.POWER_A-PS_S_A
    =function: safety shutdown System, Section: Power 
    -Device: SIS power supply A,
    +Location: SIS Logic Solver
=SIS.POWER+SIS_CAB1.POWER_B-PS_S_B
    =function: safety shutdown System, Section: Power 
    -Device: SIS power supply B,
    +Location: SIS Logic Solver
```
#### Final Element
```sql
=SIS.IO+SIS_CAB1.IO_A-DO_S01_A
    =function: safety shutdown System, Section: Input/Output 
    -Device: Safety DO module A,
    +Location: SIS Logic Solver
=ESD.L2+FIELD-SDV201
    =function: safety shutdown System, Section: Output 
    -Device: Shutdown valve (solenoid — de-energise to close),
    +Location: Field
=ESD.L2+FIELD-YV_SDV201
    =function: safety shutdown System, Section: Output 
    -Device: Solenoid valve coil on SDV201,
    +Location: Field
=ESD.L2+FIELD-ZS_SDV201_O
    =function: safety shutdown System, Section: Output 
    -Device: Position switch — open,
    +Location: Field
=ESD.L2+FIELD-ZS_SDV201_C
    =function: safety shutdown System, Section: Output 
    -Device: Position switch — closed,
    +Location: Field
```

---
