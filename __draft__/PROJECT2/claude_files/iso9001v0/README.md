# ISO 9001 Quality Management System

Production-ready implementation of ISO 9001:2015 Quality Management System with Statistical Process Control, process capability monitoring, CAPA tracking, and UNS publishing.

## Features

### ISO 9001:2015 Compliance
- **Clause 8.5**: Production and service provision (process control)
- **Clause 8.7**: Control of nonconforming outputs
- **Clause 9.1**: Monitoring, measurement, analysis and evaluation
- **Clause 9.2**: Internal audit
- **Clause 10.2**: Nonconformity and corrective action

### Core Capabilities
✅ **Multi-Source Data Collection**: Modbus TCP, OPC UA, file (CSV/JSON/XML), HTTP API, database queries  
✅ **Statistical Process Control (SPC)**: Western Electric & Nelson rules (8 rules)  
✅ **Process Capability**: Cp, Cpk, Pp, Ppk calculation and monitoring  
✅ **Nonconformance Lifecycle**: DETECTED → CONTAINED → INVESTIGATING → RESOLVED → CLOSED  
✅ **CAPA Management**: Corrective/Preventive actions with SLA enforcement  
✅ **Customer Complaints**: 8D problem solving integration  
✅ **Audit Management**: Internal/external audit findings with closure tracking  
✅ **Quality KPIs**: DPMO, PPM, FPY, RTY, Cpk, CAPA closure rate, OTD%  
✅ **UNS Publishing**: MQTT broker integration for plant-wide visibility  
✅ **PostgreSQL Storage**: Time-series optimized with optional TimescaleDB  

## Quick Start

### Prerequisites
- Docker & Docker Compose
- 4GB RAM minimum
- Network access to inspection equipment (if using Modbus/OPC UA)

### 1. Clone and Configure

```bash
cd quality_manager

# Edit configuration (optional - defaults work for demo)
nano config/config.yaml
```

### 2. Start Services

```bash
docker compose up -d --build
```

This starts:
- PostgreSQL database (port 5432)
- Mosquitto MQTT broker (port 1883)
- Quality Manager application
- pgAdmin web UI (port 5050)
- MQTT Explorer web UI (port 4000)

### 3. Import Reference Data

```bash
# Import products, processes, CQCs, SPC rules, etc.
docker compose exec quality-manager python /app/scripts/import_csv.py
```

### 4. Verify Operation

```bash
# Check logs
docker compose logs -f quality-manager

# Should see:
# INFO - QualityManager initialized successfully
# INFO - Connected to database: postgres:5432/quality_db
# INFO - Connected to MQTT broker successfully
# INFO - Entering main event loop...
```

### 5. Access Dashboards

- **pgAdmin** (Database): http://localhost:5050 (admin@quality.local / admin)
- **MQTT Explorer**: http://localhost:4000
- **Database** (Direct): localhost:5432 (quality_user / quality_pass)

## Architecture

### Three-Layer Pattern (Same as ISA-18.2 / ISO 50001 / ISO 27001)

```
┌────────────────────────────────────────────────────────────┐
│ DEVICE LAYER: Inspection Systems                          │
│ ├─ CMM (Coordinate Measuring Machine) - Modbus TCP        │
│ ├─ Hardness Tester - File export                          │
│ ├─ MES System - HTTP API                                  │
│ └─ PLC - OPC UA                                            │
└────────────────────────────────────────────────────────────┘
                            ↓
┌────────────────────────────────────────────────────────────┐
│ ISO 9001 LAYER: Quality Management                        │
│ ├─ Event Collection: Normalize measurements from sources  │
│ ├─ SPC Detection: Western Electric / Nelson rules         │
│ ├─ Process Monitor: Cp/Cpk calculation, capability status │
│ ├─ NC Manager: Nonconformance lifecycle                   │
│ ├─ CAPA Manager: Corrective/Preventive actions, SLA       │
│ ├─ Customer Manager: Complaint tracking                   │
│ ├─ Audit Manager: Finding resolution                      │
│ └─ KPI Calculator: DPMO, FPY, Cpk, etc.                   │
└────────────────────────────────────────────────────────────┘
                            ↓
┌────────────────────────────────────────────────────────────┐
│ HISTORIAN LAYER: PostgreSQL + UNS/MQTT                    │
│ ├─ PostgreSQL: Time-series optimized storage              │
│ └─ MQTT: Real-time pub/sub for plant-wide visibility      │
└────────────────────────────────────────────────────────────┘
```

### Data Flow

```
Measurement Source (CMM, Gauge, Test Equipment)
    ↓
Collector (Modbus/OPC UA/File/API)
    ↓
Normalize to standard Measurement dict
    ↓
Queue (50K capacity, 500 batch size)
    ↓
Database Batch Insert (execute_values)
    ↓
UNS Publish (QoS 0, high volume)
    ↓
SPC Detector Evaluates 8 Rules
    ↓
If Violation → Create NC → Link Measurement
    ↓
UNS Publish NC Event (QoS 1, important)
```

## SPC Rules (Western Electric / Nelson)

| Rule | Description | Severity | Detection |
|------|-------------|----------|-----------|
| 1 | 1 point > 3σ from center | CRITICAL | Special cause variation |
| 2 | 9 points on same side of center | WARNING | Process shift |
| 3 | 6 points trending up or down | WARNING | Process drift |
| 4 | 14 points alternating up/down | WARNING | Over-adjustment |
| 5 | 2 of 3 points > 2σ | WARNING | Unusual variation |
| 6 | 4 of 5 points > 1σ | INFO | Process change |
| 7 | 15 points within 1σ | INFO | Over-control |
| 8 | 8 points beyond 1σ | WARNING | Stratification |

## Process Capability Interpretation

### Cpk Values
- **Cpk ≥ 1.33**: CAPABLE (6σ quality)
- **1.0 ≤ Cpk < 1.33**: WARNING (marginally capable)
- **Cpk < 1.0**: CRITICAL (incapable, auto-create CAPA)

### Cp vs Cpk
- **High Cp, Low Cpk**: Process is precise but off-center → Adjust mean
- **Low Cp, High Cpk**: Process is on-target but imprecise → Reduce variation
- **High Cp, High Cpk**: Process is capable and centered → Ideal state

## Quality KPIs

### Defect Metrics
- **DPMO** = (Defects / Opportunities) × 1,000,000
- **PPM** = (Defects / Total) × 1,000,000
- **FPY** = (Passed / Total) × 100
- **RTY** = FPY₁ × FPY₂ × ... × FPYₙ

### Process Metrics
- **Rework Rate** = (Reworked / Total) × 100
- **Scrap Rate** = (Scrapped / Total) × 100
- **Average Cpk**: Mean Cpk across all CQCs

### Corrective Action Metrics
- **Open NCs**: Count of non-closed nonconformances
- **Open CAPAs**: Count of non-closed CAPAs
- **Overdue CAPAs**: Count past SLA deadline
- **CAPA Closure Rate** = (Closed / Total) × 100

### Customer Metrics
- **Customer Complaints**: Open complaint count
- **Complaint Age**: Average days open

### Audit Metrics
- **Open Findings**: Count of non-closed findings
- **Finding Closure Rate** = (Closed / Total) × 100

### Delivery Metrics
- **OTD%** = (On-time Shipments / Total) × 100

## UNS Topic Structure

```
UNS/PlantAlpha/quality/
├── measurements/
│   ├── CQC_SHAFT_DIA/live        (QoS 0, measurements)
│   ├── CQC_HOUSING_THICK/live
│   └── ...
├── spc/
│   └── events                     (QoS 1, violations)
├── capability/
│   └── events                     (QoS 1, Cpk results)
├── nonconformances/
│   ├── events                     (QoS 1, lifecycle)
│   └── state                      (QoS 0, retained)
├── capas/
│   ├── events                     (QoS 1, lifecycle)
│   └── state                      (QoS 0, retained)
├── complaints/
│   ├── events                     (QoS 1, lifecycle)
│   └── state                      (QoS 0, retained)
├── audits/
│   ├── events                     (QoS 1, findings)
│   └── state                      (QoS 0, retained)
└── kpis/
    └── current                    (QoS 0, retained)
```

## Configuration

### Add Modbus Inspection Source

Edit `config/config.yaml`:

```yaml
inspection_sources:
  - source_id: my_cmm_01
    source_type: modbus_tcp
    enabled: true
    poll_interval_seconds: 60
    modbus_host: 192.168.1.100
    modbus_port: 502
    modbus_registers:
      - address: 40001
        cqc_id: CQC_SHAFT_DIA
        scale: 0.01  # Convert raw value to mm
```

Restart: `docker compose restart quality-manager`

### Add New CQC (Critical Quality Characteristic)

Edit `templates/cqcs.csv`:

```csv
CQC_NEW_01,Piston Diameter,PROD_PISTON_001,PROC_CNC_TURN_001,DIMENSION,mm,49.90,50.00,49.95,1.33,1.0,0.67,30,SPC,true
```

Import: `docker compose exec quality-manager python /app/scripts/import_csv.py`

### Adjust Cpk Thresholds

Edit `config/config.yaml`:

```yaml
capability:
  target_cpk: 1.67   # More stringent
  warning_cpk: 1.33
  critical_cpk: 1.0
```

Restart: `docker compose restart quality-manager`

### Change CAPA SLA by Severity

Edit `config/config.yaml`:

```yaml
capa:
  sla_by_severity:
    CRITICAL: 3   # 3 days
    MAJOR: 7      # 7 days
    MINOR: 21     # 21 days
```

## CSV Templates

Located in `templates/` directory:

1. **products.csv** - Product master data (12 entries)
2. **processes.csv** - Process definitions (10 entries)
3. **cqcs.csv** - Critical Quality Characteristics (18 entries)
4. **spc_rules.csv** - Western Electric rules (8 rules)
5. **capa_sla.csv** - CAPA SLA by severity (4 entries)
6. **nc_types.csv** - Nonconformance types (4 types)
7. **audit_clauses.csv** - ISO 9001 clause references (10 clauses)

## Maintenance

### View Logs

```bash
# All services
docker compose logs -f

# Quality manager only
docker compose logs -f quality-manager

# Database only
docker compose logs -f postgres
```

### Database Queries

```sql
-- Check quality dashboard
SELECT * FROM quality_dashboard;

-- Active nonconformances
SELECT * FROM active_nonconformances;

-- CAPA status
SELECT * FROM capa_status WHERE overdue = true;

-- Latest capability per CQC
SELECT * FROM capability_summary WHERE capability_status = 'CRITICAL';

-- Measurements in last hour
SELECT COUNT(*) FROM quality_measurements 
WHERE ts_utc >= NOW() - INTERVAL '1 hour';
```

### Backup Database

```bash
# Backup
docker compose exec postgres pg_dump -U quality_user quality_db > backup.sql

# Restore
docker compose exec -T postgres psql -U quality_user quality_db < backup.sql
```

## Production Deployment

### Security Checklist

- [ ] Change default passwords (postgres, pgadmin)
- [ ] Enable MQTT authentication (edit mosquitto.conf, create passwd file)
- [ ] Use SSL/TLS for MQTT (port 8883)
- [ ] Restrict firewall rules (close unused ports)
- [ ] Configure database backups (pg_dump daily, offsite retention)
- [ ] Enable audit logging
- [ ] Use secrets management (Docker secrets, Vault)

### Performance Tuning

**Single Inspection Source** (~50,000 measurements/day):
- Default config works fine
- ~50 MB/month storage

**10+ Inspection Sources** (~500,000 measurements/day):
- Enable TimescaleDB: uncomment hypertable commands in migration SQL
- Compression policies: 7-day uncompressed, 1-year compressed
- Read replicas for reporting
- Increase batch size: 1000 measurements per batch
- Partition measurements table by month

**TimescaleDB Setup**:
```sql
-- Convert to hypertable
SELECT create_hypertable('quality_measurements', 'ts_utc', 
    chunk_time_interval => INTERVAL '1 month');

-- Compression policy
ALTER TABLE quality_measurements SET (
    timescaledb.compress,
    timescaledb.compress_segmentby = 'cqc_id'
);

SELECT add_compression_policy('quality_measurements', INTERVAL '7 days');

-- Retention policy (optional)
SELECT add_retention_policy('quality_measurements', INTERVAL '5 years');
```

### Monitoring

**Critical Alerts**:
- Database connection loss → Check postgres health
- MQTT disconnect → Check mosquitto status
- Measurement queue overflow → Increase batch size or poll interval
- SPC detection errors → Check control limits validity

**Grafana Dashboards** (recommended):
- Defect rate trend (DPMO over time)
- Cpk by CQC (heatmap, color by capability status)
- CAPA closure rate (target: >90%)
- FPY by product (target: >99%)
- SPC violations per day
- Top 10 products by defect count
- NC aging (open time histogram)

## Troubleshooting

### No Measurements Received

```bash
# Check collector status
docker compose logs quality-manager | grep -i collector

# Test Modbus connectivity
docker compose exec quality-manager ping <modbus_host>

# Check Modbus registers manually
# (requires pymodbus tools)
```

### SPC Violations Not Creating NCs

```bash
# Check SPC detection is enabled
docker compose exec quality-manager cat /app/config/config.yaml | grep spc_detection

# Check cooldown settings (may prevent duplicate NCs)
# View SPC violations table
docker compose exec postgres psql -U quality_user quality_db -c \
  "SELECT * FROM spc_violations ORDER BY ts_utc DESC LIMIT 10;"
```

### Capability Shows INSUFFICIENT_DATA

- Requires minimum 30 samples (configurable: `capability.min_samples`)
- Check: `SELECT COUNT(*) FROM quality_measurements WHERE cqc_id = 'CQC_XXX';`
- Wait for more measurements to accumulate

### CAPA Not Auto-Created for CRITICAL Capability

- Check feature flag: `features.capability_monitoring = true`
- Check threshold: `capability.critical_cpk` (default 0.67)
- Verify Cpk < 0.67: `SELECT * FROM capability_summary WHERE cqc_id = 'CQC_XXX';`

## License

Production-ready module for industrial quality management. 

## Series

Part of the three-layer architecture series:
1. ISA-18.2 Alarm Management
2. ISO 50001 Energy Management
3. ISO 27001 Information Security Management
4. **ISO 9001 Quality Management** (this module)

Version: 1.0  
Date: 2026-02-04
