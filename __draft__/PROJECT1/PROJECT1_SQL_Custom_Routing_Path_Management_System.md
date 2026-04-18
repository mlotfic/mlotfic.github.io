# 🗺️ Custom Routing & Path Management System
> Design, database schema, and SQL queries for managing known paths between facility locations with waypoints, turns, and multi-stop trip optimization


---

## project

### core problem

i have a case where i have multiple known location like you may say plants, booster stations, administration budling distributed and additional know famous point in roads . when given a new location if we follow the google map it gave path that not unique and in some case gave not suitable roads for target , that why i want to store path with base location and famous point and turn in addition , we need to select three location close to each other for the same trip

### dev point of view

Architected comprehensive guide for location-based routing systemArchitected comprehensive guide for location-based routing systemThe user has an interesting spatial routing/navigation problem. Let me understand it:

They have known locations: plants, booster stations, admin buildings, plus famous/landmark points on roads
When someone needs to go to a new location, Google Maps gives paths that may not be suitable (maybe for heavy vehicles, restricted roads, etc.)
They want to store pre-defined paths between their known locations, including waypoints (famous points, turns)
They also need to select 3 locations close to each other for the same trip (optimize visits)

This is essentially a custom routing/navigation system with:

A graph of known locations and paths between them
Path segments with waypoints and turns
A clustering mechanism to find 3 nearby locations for combined trips

I'll design a comprehensive guide covering the database schema for locations, paths, and waypoints, then show how to query for specific routes and identify the nearest 3 locations for trip optimization using spatial analysis.

---


Here's your Custom Routing & Path Management System guide! Let me walk you through what was designed for your specific case:

---

**The Core Idea — 3-Layer Model:**
```
Layer 1 → LOCATIONS  (plants, boosters, admin buildings, road landmarks)
Layer 2 → PATH SEGMENTS  (approved roads with turn instructions between locations)
Layer 3 → ROUTES  (complete ordered sequences: A → LMK-001 → LMK-003 → B)
```

**The 9 Tables:**

| Table | What It Solves |
|-------|----------------|
| `locations` | All known points — facilities + road landmarks in one master table |
| `location_types` | PLANT, BOOSTER, ADMIN, LANDMARK, CHECKPOINT categories |
| `paths` | Named approved routes with total distance, duration, vehicle restrictions |
| `path_waypoints` | Turn-by-turn ordered stops with instructions like *"Stay on service road under overpass"* |
| `road_restrictions` | Weight limits, permits, daylight-only access |
| `location_proximity` | Pre-computed pairwise distances — makes "find 3 nearest" very fast |
| `trips` + `trip_stops` | Plan and record multi-stop visits |

**The 3 Key Queries:**
1. **Full turn-by-turn path** from origin to destination — with landmark tips per waypoint
2. **Best cluster of 3 destinations** — ranks all combinations by tightness (minimize pairwise spread + max detour from HQ)
3. **Optimal visiting order** — tests all 6 permutations of 3 stops and returns shortest total distance

**New Location Anchoring** — when a destination isn't in your system, it finds the nearest known landmark on a stored path and tells the driver: *"Follow PATH-HQ-PLT001 until LMK-003, then continue 2.1 km to your destination."*


---

## Table of Contents
1. [Problem Statement & Goals](#1--problem-statement--goals)
2. [System Design Overview](#2--system-design-overview)
3. [Database Schema](#3--database-schema)
4. [Entity Relationship Diagram](#4--entity-relationship-diagram)
5. [Inserting Data — Examples](#5--inserting-data--examples)
6. [Core Queries — Path Lookup](#6--core-queries--path-lookup)
7. [Finding 3 Nearest Locations for One Trip](#7--finding-3-nearest-locations-for-one-trip)
8. [Trip Optimization — Visiting Order](#8--trip-optimization--visiting-order)
9. [Finding the Best Starting Waypoint for a New Location](#9--finding-the-best-starting-waypoint-for-a-new-location)
10. [Maintenance & Data Quality Queries](#10--maintenance--data-quality-queries)
11. [Full Working Example — End to End](#11--full-working-example--end-to-end)
12. [Indexing Strategy](#12--indexing-strategy)
13. [Extension Ideas](#13--extension-ideas)

---

## 1. 🎯 Problem Statement & Goals

### The Problem

Google Maps and standard navigation tools:
- ❌ Suggest roads that are unsuitable (low bridges, weight restrictions, unpaved)
- ❌ Give non-unique paths — different every time the query runs
- ❌ Don't know about internal facility rules (entry gates, checkpoints)
- ❌ Can't optimize visits to multiple nearby sites in one trip
- ❌ Don't leverage your organization's institutional knowledge of the road network

### Your Assets

You already have:
- **Known facility locations**: plants, booster stations, administration buildings
- **Landmark points**: well-known road junctions, bridges, roundabouts, landmarks
- **Institutional knowledge**: the right roads to use, turns to make, checkpoints to pass

### What We're Building

A **custom routing database** that:

1. **Stores approved paths** between your known locations, including all waypoints and turn-by-turn instructions
2. **Anchors new destinations** to the nearest known landmark point on an approved road, then follows the stored path
3. **Groups nearby locations** intelligently so a driver can visit 3 sites in one efficient trip

---

## 2. 🏗️ System Design Overview

### Core Concept — The Graph Model

Think of your road network as a **graph**:

```
                    [Admin HQ]
                        │
                   (approved road)
                        │
[Plant A] ──────── [Junction X] ──────── [Plant B]
                        │
                   [Booster St. 1]
                        │
              [Famous Roundabout Y]
                        │
                   [Booster St. 2]
```

- **Nodes** = your known locations + landmark points (everything with coordinates)
- **Edges** = approved path segments between nodes, with turn instructions
- **Paths** = sequences of connected edges forming a complete route

### Three-Layer Architecture

```
Layer 1 — LOCATIONS
  All named points: facilities, landmarks, checkpoints
  (Plants, Booster Stations, Admin Buildings, Road Junctions, Roundabouts)

Layer 2 — PATH SEGMENTS
  Approved road segments between pairs of locations
  Each segment stores: geometry, distance, duration, road restrictions

Layer 3 — ROUTES (complete paths)
  An ordered sequence of segments forming a complete A→B route
  Includes waypoints and turn-by-turn instructions at each junction
```

### Path Lookup Flow for a NEW Location

```
New destination arrives (GPS point)
         │
         ▼
Find nearest known LANDMARK POINT on an approved road
         │
         ▼
Locate the ROUTE that passes through or near that landmark
         │
         ▼
Return the stored PATH from origin to that landmark
         +
Return the short "last mile" segment from landmark to destination
         │
         ▼
Driver gets: approved path + simple final instruction
```

---

## 3. 🗄️ Database Schema

### Table 1 — `location_types`
Defines what category a location belongs to.

```sql
CREATE TABLE location_types (
  id          TINYINT      NOT NULL AUTO_INCREMENT PRIMARY KEY,
  code        VARCHAR(20)  NOT NULL UNIQUE,   -- 'PLANT', 'BOOSTER', 'ADMIN', 'LANDMARK', 'CHECKPOINT'
  label       VARCHAR(50)  NOT NULL,
  description TEXT,
  icon        VARCHAR(50)                     -- optional: icon name for map display
);

INSERT INTO location_types (code, label, description) VALUES
  ('PLANT',      'Plant',                'Production or processing plant'),
  ('BOOSTER',    'Booster Station',      'Pipeline or power booster station'),
  ('ADMIN',      'Administration',       'Administrative or office building'),
  ('LANDMARK',   'Road Landmark',        'Well-known road point: roundabout, bridge, junction'),
  ('CHECKPOINT', 'Checkpoint / Gate',    'Security gate or access checkpoint'),
  ('DEPOT',      'Depot / Warehouse',    'Storage or maintenance depot');
```

---

### Table 2 — `locations`
The master table of all known points in your network.

```sql
CREATE TABLE locations (
  id              INT            NOT NULL AUTO_INCREMENT PRIMARY KEY,
  code            VARCHAR(20)    NOT NULL UNIQUE,           -- e.g. 'PLT-001', 'BST-012', 'LMK-045'
  name            VARCHAR(150)   NOT NULL,
  name_ar         VARCHAR(150),                             -- Arabic name if needed
  type_id         TINYINT        NOT NULL,
  position        POINT          NOT NULL SRID 4326,        -- GPS coordinates
  address         TEXT,
  notes           TEXT,                                     -- access notes, restrictions, contact
  is_destination  BOOLEAN        NOT NULL DEFAULT TRUE,     -- can be a trip destination?
  is_waypoint     BOOLEAN        NOT NULL DEFAULT TRUE,     -- can be used as a path waypoint?
  is_active       BOOLEAN        NOT NULL DEFAULT TRUE,
  created_at      DATETIME       NOT NULL DEFAULT CURRENT_TIMESTAMP,
  updated_at      DATETIME       NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,

  CONSTRAINT fk_loc_type FOREIGN KEY (type_id) REFERENCES location_types(id),
  SPATIAL INDEX idx_location_pos (position)
);
```

---

### Table 3 — `road_restrictions`
Stores restrictions that apply to path segments or locations.

```sql
CREATE TABLE road_restrictions (
  id              INT           NOT NULL AUTO_INCREMENT PRIMARY KEY,
  code            VARCHAR(20)   NOT NULL UNIQUE,
  description     VARCHAR(100)  NOT NULL
);

INSERT INTO road_restrictions (code, description) VALUES
  ('MAX_WEIGHT_7T',   'Max vehicle weight 7 tonnes'),
  ('MAX_WEIGHT_15T',  'Max vehicle weight 15 tonnes'),
  ('NO_HAZMAT',       'No hazardous materials'),
  ('NO_TRUCKS',       'No trucks or heavy vehicles'),
  ('4WD_ONLY',        'Four-wheel drive vehicles only'),
  ('PERMIT_REQUIRED', 'Access permit required'),
  ('DAYLIGHT_ONLY',   'Daylight access only');
```

---

### Table 4 — `paths`
A named, approved route between an origin and a destination.

```sql
CREATE TABLE paths (
  id              INT            NOT NULL AUTO_INCREMENT PRIMARY KEY,
  code            VARCHAR(30)    NOT NULL UNIQUE,           -- e.g. 'PATH-HQ-PLT001'
  name            VARCHAR(150)   NOT NULL,
  origin_id       INT            NOT NULL,                  -- starting location
  destination_id  INT            NOT NULL,
  is_bidirectional BOOLEAN       NOT NULL DEFAULT FALSE,    -- can be traversed both ways?
  total_distance_m INT,                                     -- total meters
  total_duration_min SMALLINT,                              -- estimated minutes
  geometry        LINESTRING     SRID 4326,                 -- full path geometry for map display
  notes           TEXT,
  vehicle_types   VARCHAR(200),                             -- 'SEDAN,SUV,TRUCK' — allowed vehicles
  is_active       BOOLEAN        NOT NULL DEFAULT TRUE,
  created_at      DATETIME       NOT NULL DEFAULT CURRENT_TIMESTAMP,
  updated_at      DATETIME       NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,

  CONSTRAINT fk_path_origin      FOREIGN KEY (origin_id)      REFERENCES locations(id),
  CONSTRAINT fk_path_destination FOREIGN KEY (destination_id) REFERENCES locations(id),
  CONSTRAINT chk_path_different  CHECK (origin_id <> destination_id),
  SPATIAL INDEX idx_path_geom (geometry)
);
```

---

### Table 5 — `path_waypoints`
Ordered sequence of locations that make up a path, with turn instructions.

```sql
CREATE TABLE path_waypoints (
  id              INT            NOT NULL AUTO_INCREMENT PRIMARY KEY,
  path_id         INT            NOT NULL,
  sequence        SMALLINT       NOT NULL,                  -- 1, 2, 3 … order along the path
  location_id     INT            NOT NULL,                  -- the waypoint location
  instruction     TEXT,                                     -- turn instruction: "Turn RIGHT at the roundabout"
  instruction_ar  TEXT,                                     -- Arabic version
  distance_from_prev_m INT,                                 -- meters from previous waypoint
  duration_from_prev_min SMALLINT,                          -- minutes from previous waypoint
  landmark_note   TEXT,                                     -- "After the blue water tower, turn left"
  segment_geom    LINESTRING     SRID 4326,                 -- geometry of this segment only

  CONSTRAINT fk_pw_path     FOREIGN KEY (path_id)     REFERENCES paths(id) ON DELETE CASCADE,
  CONSTRAINT fk_pw_location FOREIGN KEY (location_id) REFERENCES locations(id),
  CONSTRAINT uq_path_seq    UNIQUE (path_id, sequence),
  SPATIAL INDEX idx_pw_segment (segment_geom)
);
```

---

### Table 6 — `path_restrictions`
Links a path to its applicable restrictions.

```sql
CREATE TABLE path_restrictions (
  path_id        INT NOT NULL,
  restriction_id INT NOT NULL,
  PRIMARY KEY (path_id, restriction_id),
  CONSTRAINT fk_pr_path        FOREIGN KEY (path_id)        REFERENCES paths(id) ON DELETE CASCADE,
  CONSTRAINT fk_pr_restriction FOREIGN KEY (restriction_id) REFERENCES road_restrictions(id)
);
```

---

### Table 7 — `location_proximity`
Pre-computed distances between all location pairs (materialized for speed).
Update this table whenever locations are added or changed.

```sql
CREATE TABLE location_proximity (
  location_a_id  INT            NOT NULL,
  location_b_id  INT            NOT NULL,
  distance_m     INT            NOT NULL,                   -- straight-line meters
  has_direct_path BOOLEAN       NOT NULL DEFAULT FALSE,     -- is there a stored path?
  path_id        INT,                                       -- if yes, which path
  updated_at     DATETIME       NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,

  PRIMARY KEY (location_a_id, location_b_id),
  CONSTRAINT fk_lp_a    FOREIGN KEY (location_a_id) REFERENCES locations(id),
  CONSTRAINT fk_lp_b    FOREIGN KEY (location_b_id) REFERENCES locations(id),
  CONSTRAINT fk_lp_path FOREIGN KEY (path_id)       REFERENCES paths(id),
  INDEX idx_lp_a_dist (location_a_id, distance_m),
  INDEX idx_lp_b_dist (location_b_id, distance_m)
);
```

---

### Table 8 — `trips`
Records planned or completed multi-stop trips.

```sql
CREATE TABLE trips (
  id              INT            NOT NULL AUTO_INCREMENT PRIMARY KEY,
  trip_code       VARCHAR(30)    NOT NULL UNIQUE,
  origin_id       INT            NOT NULL,                  -- trip starting point
  planned_date    DATE,
  vehicle_type    VARCHAR(30),
  driver_notes    TEXT,
  status          VARCHAR(20)    NOT NULL DEFAULT 'PLANNED',  -- PLANNED, IN_PROGRESS, COMPLETED
  created_at      DATETIME       NOT NULL DEFAULT CURRENT_TIMESTAMP,

  CONSTRAINT fk_trip_origin FOREIGN KEY (origin_id) REFERENCES locations(id),
  CONSTRAINT chk_trip_status CHECK (status IN ('PLANNED','IN_PROGRESS','COMPLETED','CANCELLED'))
);
```

---

### Table 9 — `trip_stops`
The ordered list of destinations for a trip.

```sql
CREATE TABLE trip_stops (
  id              INT            NOT NULL AUTO_INCREMENT PRIMARY KEY,
  trip_id         INT            NOT NULL,
  stop_sequence   TINYINT        NOT NULL,                  -- 1 = first stop
  location_id     INT            NOT NULL,
  path_id         INT,                                      -- which path to take to reach this stop
  estimated_arrival_min INT,                                -- cumulative minutes from trip start
  notes           TEXT,

  CONSTRAINT fk_ts_trip     FOREIGN KEY (trip_id)     REFERENCES trips(id) ON DELETE CASCADE,
  CONSTRAINT fk_ts_location FOREIGN KEY (location_id) REFERENCES locations(id),
  CONSTRAINT fk_ts_path     FOREIGN KEY (path_id)     REFERENCES paths(id),
  CONSTRAINT uq_trip_stop   UNIQUE (trip_id, stop_sequence)
);
```

---

## 4. 📊 Entity Relationship Diagram

```
┌──────────────────┐
│  location_types  │
│──────────────────│
│ id (PK)          │
│ code             │
│ label            │
└────────┬─────────┘
         │ 1
         │
         │ N
┌────────▼──────────────────────────────┐
│              locations                 │
│───────────────────────────────────────│
│ id (PK)                               │
│ code (UNIQUE)                         │
│ name                                  │
│ type_id (FK → location_types)        │
│ position  POINT SRID 4326  [SPATIAL]  │
│ is_destination                        │
│ is_waypoint                           │
└───────┬──────────────┬────────────────┘
        │              │
        │ origin/dest  │ waypoint
        │              │
        ▼              ▼
┌───────────────────────────────────────┐       ┌──────────────────────┐
│               paths                   │──────▶│  path_restrictions   │
│───────────────────────────────────────│       │──────────────────────│
│ id (PK)                               │       │ path_id (FK)         │
│ code (UNIQUE)                         │       │ restriction_id (FK)  │
│ origin_id (FK → locations)           │       └──────────────────────┘
│ destination_id (FK → locations)      │
│ is_bidirectional                      │
│ total_distance_m                      │
│ total_duration_min                    │
│ geometry  LINESTRING  [SPATIAL]       │
└──────────────┬────────────────────────┘
               │ 1
               │
               │ N
┌──────────────▼────────────────────────┐
│           path_waypoints              │
│───────────────────────────────────────│
│ id (PK)                               │
│ path_id (FK → paths)                 │
│ sequence                              │
│ location_id (FK → locations)         │
│ instruction                           │
│ distance_from_prev_m                  │
│ segment_geom  LINESTRING  [SPATIAL]  │
└───────────────────────────────────────┘

┌──────────────────────────────────────┐
│          location_proximity          │
│──────────────────────────────────────│
│ location_a_id (FK)                   │     pre-computed pairwise distances
│ location_b_id (FK)                   │     for fast "nearest 3" queries
│ distance_m                           │
│ has_direct_path                      │
│ path_id (FK)                         │
└──────────────────────────────────────┘

┌──────────────────┐      ┌──────────────────────┐
│      trips       │─────▶│     trip_stops        │
│──────────────────│      │──────────────────────│
│ id (PK)          │      │ trip_id (FK)          │
│ trip_code        │      │ stop_sequence         │
│ origin_id (FK)   │      │ location_id (FK)      │
│ status           │      │ path_id (FK)          │
└──────────────────┘      └──────────────────────┘
```

---

## 5. 📝 Inserting Data — Examples

### Step 1 — Insert Locations

```sql
-- Administration Building (HQ — main starting point)
INSERT INTO locations (code, name, type_id, position, notes, is_destination, is_waypoint)
VALUES (
  'ADMIN-HQ',
  'Main Administration Building',
  (SELECT id FROM location_types WHERE code = 'ADMIN'),
  ST_PointFromText('POINT(31.2357 30.0444)', 4326),
  'Main gate — report to security. Open 07:00–17:00.',
  TRUE, TRUE
);

-- Plant A
INSERT INTO locations (code, name, type_id, position, notes)
VALUES (
  'PLT-001',
  'Plant Alpha — North Zone',
  (SELECT id FROM location_types WHERE code = 'PLANT'),
  ST_PointFromText('POINT(31.3012 30.1205)', 4326),
  'Use Gate C for trucks. Max weight 15T on access road.'
);

-- Plant B
INSERT INTO locations (code, name, type_id, position, notes)
VALUES (
  'PLT-002',
  'Plant Beta — East Zone',
  (SELECT id FROM location_types WHERE code = 'PLANT'),
  ST_PointFromText('POINT(31.4203 30.0891)', 4326),
  'Call ahead: +20-xxx. Access road not suitable for articulated trucks.'
);

-- Booster Station 1
INSERT INTO locations (code, name, type_id, position, notes)
VALUES (
  'BST-001',
  'Booster Station North-1',
  (SELECT id FROM location_types WHERE code = 'BOOSTER'),
  ST_PointFromText('POINT(31.2890 30.1550)', 4326),
  'Always check-in with station supervisor on arrival.'
);

-- Booster Station 2
INSERT INTO locations (code, name, type_id, position, notes)
VALUES (
  'BST-002',
  'Booster Station East-2',
  (SELECT id FROM location_types WHERE code = 'BOOSTER'),
  ST_PointFromText('POINT(31.3780 30.1102)', 4326),
  NULL
);

-- Landmark Points (road reference points — is_destination = FALSE)
INSERT INTO locations (code, name, type_id, position, is_destination, is_waypoint, notes) VALUES
  ('LMK-001', 'Al Nozha Roundabout',     (SELECT id FROM location_types WHERE code='LANDMARK'), ST_PointFromText('POINT(31.2612 30.0812)', 4326), FALSE, TRUE, 'Large roundabout — take 3rd exit heading north'),
  ('LMK-002', 'Blue Water Tower Junction',(SELECT id FROM location_types WHERE code='LANDMARK'), ST_PointFromText('POINT(31.2890 30.1100)', 4326), FALSE, TRUE, 'Turn right after the blue water tower'),
  ('LMK-003', 'Ring Road Overpass',       (SELECT id FROM location_types WHERE code='LANDMARK'), ST_PointFromText('POINT(31.3200 30.0950)', 4326), FALSE, TRUE, 'Do NOT use Ring Road — use service road below'),
  ('LMK-004', 'East Industrial Gate',     (SELECT id FROM location_types WHERE code='LANDMARK'), ST_PointFromText('POINT(31.4100 30.0870)', 4326), FALSE, TRUE, 'Company permit required at this gate'),
  ('LMK-005', 'Main Canal Bridge',        (SELECT id FROM location_types WHERE code='LANDMARK'), ST_PointFromText('POINT(31.3500 30.1200)', 4326), FALSE, TRUE, 'Weight limit 15T — check bridge sign');
```

---

### Step 2 — Insert a Path (HQ → Plant A)

```sql
-- Create the path header
INSERT INTO paths (code, name, origin_id, destination_id, is_bidirectional, total_distance_m, total_duration_min, vehicle_types, notes)
VALUES (
  'PATH-HQ-PLT001',
  'HQ to Plant Alpha (North Zone)',
  (SELECT id FROM locations WHERE code = 'ADMIN-HQ'),
  (SELECT id FROM locations WHERE code = 'PLT-001'),
  FALSE,         -- return path must be stored separately if different
  18500,         -- 18.5 km
  35,            -- ~35 minutes
  'SEDAN,SUV,VAN,TRUCK',
  'Approved route. Avoid Ring Road section — use service road at LMK-003.'
);

-- Link restrictions
INSERT INTO path_restrictions (path_id, restriction_id)
VALUES (
  (SELECT id FROM paths WHERE code = 'PATH-HQ-PLT001'),
  (SELECT id FROM road_restrictions WHERE code = 'MAX_WEIGHT_15T')
);

-- Insert the ordered waypoints (turn-by-turn)
-- Waypoint 1: Starting point (sequence 1 = origin itself)
INSERT INTO path_waypoints (path_id, sequence, location_id, instruction, distance_from_prev_m, duration_from_prev_min, landmark_note)
VALUES (
  (SELECT id FROM paths WHERE code = 'PATH-HQ-PLT001'),
  1,
  (SELECT id FROM locations WHERE code = 'ADMIN-HQ'),
  'Depart from Main Administration Building. Head NORTH on the main access road.',
  0, 0,
  'Exit via the main gate, security check-in required.'
);

-- Waypoint 2: Al Nozha Roundabout
INSERT INTO path_waypoints (path_id, sequence, location_id, instruction, distance_from_prev_m, duration_from_prev_min, landmark_note)
VALUES (
  (SELECT id FROM paths WHERE code = 'PATH-HQ-PLT001'),
  2,
  (SELECT id FROM locations WHERE code = 'LMK-001'),
  'At Al Nozha Roundabout, take the 3rd exit heading NORTH-EAST.',
  4200, 8,
  'The roundabout has a large fountain in the center. Take exit 3, not exit 2.'
);

-- Waypoint 3: Blue Water Tower Junction
INSERT INTO path_waypoints (path_id, sequence, location_id, instruction, distance_from_prev_m, duration_from_prev_min, landmark_note)
VALUES (
  (SELECT id FROM paths WHERE code = 'PATH-HQ-PLT001'),
  3,
  (SELECT id FROM locations WHERE code = 'LMK-002'),
  'Turn RIGHT at the Blue Water Tower Junction.',
  5800, 11,
  'You will see a large blue painted water tower on your left — turn RIGHT immediately after it.'
);

-- Waypoint 4: Ring Road Overpass (important — avoid Ring Road!)
INSERT INTO path_waypoints (path_id, sequence, location_id, instruction, distance_from_prev_m, duration_from_prev_min, landmark_note)
VALUES (
  (SELECT id FROM paths WHERE code = 'PATH-HQ-PLT001'),
  4,
  (SELECT id FROM locations WHERE code = 'LMK-003'),
  'IMPORTANT: Do NOT go up the Ring Road overpass. Stay on the SERVICE ROAD beneath it.',
  4100, 8,
  'The ramp up to Ring Road is on your right — ignore it. Continue straight on the lower service road.'
);

-- Waypoint 5: Destination — Plant Alpha
INSERT INTO path_waypoints (path_id, sequence, location_id, instruction, distance_from_prev_m, duration_from_prev_min, landmark_note)
VALUES (
  (SELECT id FROM paths WHERE code = 'PATH-HQ-PLT001'),
  5,
  (SELECT id FROM locations WHERE code = 'PLT-001'),
  'Arrive at Plant Alpha — North Zone. Enter via Gate C.',
  4400, 8,
  'Gate C is on the east side of the facility. Report to the guard station with your work order.'
);
```

---

### Step 3 — Populate the Proximity Matrix

Run this after all locations are inserted to pre-compute distances:

```sql
-- Insert/update all pairwise distances (both directions)
INSERT INTO location_proximity (location_a_id, location_b_id, distance_m, has_direct_path, path_id)
SELECT
  a.id AS location_a_id,
  b.id AS location_b_id,
  ROUND(ST_Distance_Sphere(a.position, b.position)) AS distance_m,
  CASE WHEN p.id IS NOT NULL THEN TRUE ELSE FALSE END AS has_direct_path,
  p.id AS path_id
FROM locations a
JOIN locations b ON a.id < b.id         -- avoid duplicates, store A<B only
LEFT JOIN paths p ON (
  (p.origin_id = a.id AND p.destination_id = b.id)
  OR
  (p.origin_id = b.id AND p.destination_id = a.id AND p.is_bidirectional = TRUE)
)
WHERE a.is_active = TRUE AND b.is_active = TRUE
ON DUPLICATE KEY UPDATE
  distance_m = VALUES(distance_m),
  has_direct_path = VALUES(has_direct_path),
  path_id = VALUES(path_id),
  updated_at = NOW();
```

---

## 6. 🔍 Core Queries — Path Lookup

### Query 1 — Get Full Path with All Waypoints from A to B

```sql
-- Get the complete turn-by-turn path from HQ to Plant Alpha
SELECT
  p.code          AS path_code,
  p.name          AS path_name,
  p.total_distance_m,
  p.total_duration_min,
  p.vehicle_types,
  p.notes         AS path_notes,
  -- waypoints
  pw.sequence,
  l.code          AS waypoint_code,
  l.name          AS waypoint_name,
  lt.label        AS waypoint_type,
  pw.instruction,
  pw.landmark_note,
  pw.distance_from_prev_m,
  pw.duration_from_prev_min,
  ST_X(l.position) AS longitude,
  ST_Y(l.position) AS latitude
FROM paths p
JOIN path_waypoints pw ON pw.path_id = p.id
JOIN locations      l  ON l.id = pw.location_id
JOIN location_types lt ON lt.id = l.type_id
WHERE p.origin_id      = (SELECT id FROM locations WHERE code = 'ADMIN-HQ')
  AND p.destination_id = (SELECT id FROM locations WHERE code = 'PLT-001')
  AND p.is_active = TRUE
ORDER BY pw.sequence;
```

**Result:**
```
seq | waypoint      | type        | instruction                          | dist_m | min
----|---------------|-------------|--------------------------------------|--------|----
 1  | ADMIN-HQ      | Admin       | Depart heading NORTH                 |      0 |   0
 2  | LMK-001       | Landmark    | At roundabout take 3rd exit NE       |   4200 |   8
 3  | LMK-002       | Landmark    | Turn RIGHT at Blue Water Tower        |   5800 |  11
 4  | LMK-003       | Landmark    | Stay on SERVICE ROAD under overpass   |   4100 |   8
 5  | PLT-001       | Plant       | Arrive Plant Alpha — enter Gate C    |   4400 |   8
```

---

### Query 2 — List All Available Paths from a Given Origin

```sql
-- What paths are available departing from HQ?
SELECT
  p.code,
  p.name,
  lo.name                     AS origin,
  ld.name                     AS destination,
  p.total_distance_m / 1000   AS distance_km,
  p.total_duration_min        AS duration_min,
  p.vehicle_types,
  COUNT(pw.id)                AS num_waypoints,
  GROUP_CONCAT(
    r.description
    ORDER BY r.code
    SEPARATOR ' | '
  )                           AS restrictions
FROM paths p
JOIN locations      lo ON lo.id = p.origin_id
JOIN locations      ld ON ld.id = p.destination_id
JOIN path_waypoints pw ON pw.path_id = p.id
LEFT JOIN path_restrictions pr ON pr.path_id = p.id
LEFT JOIN road_restrictions  r  ON r.id = pr.restriction_id
WHERE p.origin_id = (SELECT id FROM locations WHERE code = 'ADMIN-HQ')
  AND p.is_active = TRUE
GROUP BY p.id
ORDER BY p.total_distance_m;
```

---

### Query 3 — Find Path Between Any Two Points (Including Bidirectional)

```sql
-- Find path regardless of direction
SELECT
  p.id,
  p.code,
  p.name,
  CASE
    WHEN p.origin_id = src.id THEN 'FORWARD'
    ELSE 'REVERSE (bidirectional)'
  END AS direction,
  p.total_distance_m,
  p.total_duration_min
FROM paths p
JOIN locations src ON src.code = 'PLT-001'
JOIN locations dst ON dst.code = 'ADMIN-HQ'
WHERE p.is_active = TRUE
  AND (
    (p.origin_id = src.id AND p.destination_id = dst.id)
    OR
    (p.origin_id = dst.id AND p.destination_id = src.id AND p.is_bidirectional = TRUE)
  );
```

---

### Query 4 — Get Formatted Turn-by-Turn Instructions (Driver View)

```sql
-- Clean driver-friendly output
SELECT
  CONCAT(LPAD(pw.sequence, 2, '0'), '. ', pw.instruction)   AS step,
  CONCAT('(', pw.distance_from_prev_m, 'm / ',
              pw.duration_from_prev_min, ' min)')             AS segment,
  COALESCE(pw.landmark_note, '')                              AS landmark_tip
FROM paths p
JOIN path_waypoints pw ON pw.path_id = p.id
WHERE p.code = 'PATH-HQ-PLT001'
ORDER BY pw.sequence;
```

**Output:**
```
step                                           | segment         | landmark_tip
-----------------------------------------------|-----------------|------------------------------------------
01. Depart from HQ. Head NORTH                 | (0m / 0min)     | Exit via main gate, security check-in
02. At Nozha Roundabout take 3rd exit NE       | (4200m / 8min)  | Large fountain — exit 3, NOT exit 2
03. Turn RIGHT at Blue Water Tower             | (5800m / 11min) | Blue tower on left — turn RIGHT after it
04. STAY on service road — NO Ring Road        | (4100m / 8min)  | Ramp on right — ignore, go straight below
05. Arrive Plant Alpha — enter Gate C          | (4400m / 8min)  | Gate C on east side — report to guard
```

---

## 7. 📍 Finding 3 Nearest Locations for One Trip

### The Problem

Given a starting point, find the **3 destination locations** that are:
1. Close to each other (tight geographic cluster)
2. All reasonably close to the starting point
3. Can all be visited in a single efficient trip

### Strategy

Use **cluster scoring**: find groups of 3 locations where:
- The sum of distances between all three is minimized (tight cluster)
- The furthest one from origin is acceptable
- Each pair in the group has a stored path (or at least one hub path through a shared waypoint)

---

### Query 5 — Top 3 Nearest Destinations to Origin (Simple Version)

```sql
-- Simplest: just the 3 destinations physically closest to origin
SELECT
  l.code,
  l.name,
  lt.label AS type,
  ROUND(ST_Distance_Sphere(l.position, origin.position) / 1000, 2) AS km_from_origin,
  lp.has_direct_path,
  p.code AS path_code
FROM locations l
JOIN location_types lt ON lt.id = l.type_id
JOIN locations origin  ON origin.code = 'ADMIN-HQ'
LEFT JOIN location_proximity lp
  ON (lp.location_a_id = origin.id AND lp.location_b_id = l.id)
  OR (lp.location_a_id = l.id      AND lp.location_b_id = origin.id)
LEFT JOIN paths p ON p.id = lp.path_id
WHERE l.is_destination = TRUE
  AND l.is_active = TRUE
  AND l.code <> 'ADMIN-HQ'
ORDER BY ST_Distance_Sphere(l.position, origin.position) ASC
LIMIT 3;
```

---

### Query 6 — Best Cluster of 3 Destinations (Optimized Version)

Find the **tightest cluster of 3 destinations** — minimizing total pairwise distance within the group AND total distance from origin.

```sql
-- Find all combinations of 3 destinations, score by cluster tightness
-- Variables: set your origin code and max acceptable one-way distance
SET @origin_code = 'ADMIN-HQ';
SET @max_km      = 50;    -- only consider destinations within 50 km

WITH
-- Step 1: Pre-filter destinations within acceptable range
candidates AS (
  SELECT
    l.id,
    l.code,
    l.name,
    lt.label AS type,
    ROUND(ST_Distance_Sphere(l.position, o.position) / 1000, 2) AS km_from_origin,
    l.position
  FROM locations l
  JOIN location_types lt ON lt.id = l.type_id
  JOIN locations o ON o.code = @origin_code
  WHERE l.is_destination = TRUE
    AND l.is_active       = TRUE
    AND l.code <> @origin_code
    AND ST_Distance_Sphere(l.position, o.position) / 1000 <= @max_km
),

-- Step 2: Generate all combinations of 3 from candidates
combos AS (
  SELECT
    a.id   AS loc_a_id,   a.code AS loc_a_code,   a.name AS loc_a_name,   a.type AS type_a,
    b.id   AS loc_b_id,   b.code AS loc_b_code,   b.name AS loc_b_name,   b.type AS type_b,
    c.id   AS loc_c_id,   c.code AS loc_c_code,   c.name AS loc_c_name,   c.type AS type_c,
    a.km_from_origin   AS km_a,
    b.km_from_origin   AS km_b,
    c.km_from_origin   AS km_c,
    -- pairwise distances within the cluster (meters)
    ROUND(ST_Distance_Sphere(a.position, b.position) / 1000, 2) AS km_ab,
    ROUND(ST_Distance_Sphere(b.position, c.position) / 1000, 2) AS km_bc,
    ROUND(ST_Distance_Sphere(a.position, c.position) / 1000, 2) AS km_ac,
    -- cluster score: sum of all pairwise distances (lower = tighter cluster)
    ROUND((
      ST_Distance_Sphere(a.position, b.position) +
      ST_Distance_Sphere(b.position, c.position) +
      ST_Distance_Sphere(a.position, c.position)
    ) / 1000, 2) AS cluster_spread_km,
    -- trip score: max single leg from origin (longest detour in the trip)
    GREATEST(a.km_from_origin, b.km_from_origin, c.km_from_origin) AS max_km_from_origin
  FROM candidates a
  JOIN candidates b ON b.id > a.id   -- avoid duplicate combinations
  JOIN candidates c ON c.id > b.id   -- a < b < c ensures each combo is unique
)

-- Step 3: Rank combinations by composite score
SELECT
  loc_a_code, loc_a_name, type_a, km_a,
  loc_b_code, loc_b_name, type_b, km_b,
  loc_c_code, loc_c_name, type_c, km_c,
  km_ab, km_bc, km_ac,
  cluster_spread_km,
  max_km_from_origin,
  -- composite trip score: cluster tightness (70%) + max detour (30%)
  ROUND(cluster_spread_km * 0.7 + max_km_from_origin * 0.3, 2) AS trip_score
FROM combos
ORDER BY trip_score ASC
LIMIT 10;       -- show top 10 best cluster options
```

**Example output:**
```
loc_a        | loc_b        | loc_c        | km_ab | km_bc | km_ac | cluster | max_km | score
-------------|--------------|--------------|-------|-------|-------|---------|--------|-------
PLT-001      | BST-001      | BST-002      |  8.2  |  6.5  |  9.1  |  23.8   |  22.1  | 23.3
PLT-001      | PLT-002      | BST-002      | 12.3  |  7.8  | 11.2  |  31.3   |  24.5  | 29.3
ADMIN-HQ(2) | BST-001      | PLT-001      |  9.5  | 10.1  |  8.8  |  28.4   |  20.6  | 26.1
```
→ **Best trip cluster**: PLT-001 + BST-001 + BST-002 (tightest, lowest score = most efficient)

---

### Query 7 — Best 3 Locations with Preference for Type Diversity

Sometimes you want to ensure the trip covers different types of facilities:

```sql
-- Best 3-stop trip with at least one PLANT, one BOOSTER, and one of any type
WITH ranked AS (
  SELECT
    l.id, l.code, l.name,
    lt.code AS type_code,
    ROUND(ST_Distance_Sphere(l.position, o.position) / 1000, 2) AS km_from_origin
  FROM locations l
  JOIN location_types lt ON lt.id = l.type_id
  JOIN locations o ON o.code = 'ADMIN-HQ'
  WHERE l.is_destination = TRUE AND l.is_active = TRUE AND l.code <> 'ADMIN-HQ'
)
SELECT
  p.code AS plant, p.km_from_origin AS plant_km,
  b.code AS booster, b.km_from_origin AS booster_km,
  x.code AS third, x.km_from_origin AS third_km,
  ROUND((
    ST_Distance_Sphere(
      (SELECT position FROM locations WHERE code = p.code),
      (SELECT position FROM locations WHERE code = b.code)
    ) +
    ST_Distance_Sphere(
      (SELECT position FROM locations WHERE code = b.code),
      (SELECT position FROM locations WHERE code = x.code)
    ) +
    ST_Distance_Sphere(
      (SELECT position FROM locations WHERE code = p.code),
      (SELECT position FROM locations WHERE code = x.code)
    )
  ) / 1000, 1) AS cluster_km
FROM ranked p
JOIN ranked b ON b.type_code = 'BOOSTER' AND b.id <> p.id
JOIN ranked x ON x.id <> p.id AND x.id <> b.id
WHERE p.type_code = 'PLANT'
ORDER BY cluster_km ASC
LIMIT 5;
```

---

## 8. 🔄 Trip Optimization — Visiting Order

Once you've selected 3 locations, find the most efficient **visiting order** (nearest-neighbor heuristic for 3 stops — all 6 permutations):

```sql
-- Given 3 locations, find the best visiting order (all permutations of 3 stops)
SET @origin = 'ADMIN-HQ';
SET @stop1  = 'PLT-001';
SET @stop2  = 'BST-001';
SET @stop3  = 'BST-002';

WITH stops AS (
  SELECT code, position FROM locations WHERE code IN (@stop1, @stop2, @stop3)
),
origin_pos AS (
  SELECT position FROM locations WHERE code = @origin
)
SELECT
  CONCAT(@origin, ' → ', a.code, ' → ', b.code, ' → ', c.code) AS route,
  ROUND((
    ST_Distance_Sphere((SELECT position FROM origin_pos), a.position) +
    ST_Distance_Sphere(a.position, b.position) +
    ST_Distance_Sphere(b.position, c.position)
  ) / 1000, 2) AS total_km
FROM stops a
JOIN stops b ON b.code > a.code
JOIN stops c ON c.code <> a.code AND c.code <> b.code
-- Generate all 6 permutations manually for 3 stops:
UNION ALL
SELECT CONCAT(@origin,' → ',@stop1,' → ',@stop2,' → ',@stop3),
  ROUND((ST_Distance_Sphere((SELECT position FROM locations WHERE code=@origin),(SELECT position FROM locations WHERE code=@stop1))
       + ST_Distance_Sphere((SELECT position FROM locations WHERE code=@stop1),(SELECT position FROM locations WHERE code=@stop2))
       + ST_Distance_Sphere((SELECT position FROM locations WHERE code=@stop2),(SELECT position FROM locations WHERE code=@stop3)))/1000,2)
UNION ALL
SELECT CONCAT(@origin,' → ',@stop1,' → ',@stop3,' → ',@stop2),
  ROUND((ST_Distance_Sphere((SELECT position FROM locations WHERE code=@origin),(SELECT position FROM locations WHERE code=@stop1))
       + ST_Distance_Sphere((SELECT position FROM locations WHERE code=@stop1),(SELECT position FROM locations WHERE code=@stop3))
       + ST_Distance_Sphere((SELECT position FROM locations WHERE code=@stop3),(SELECT position FROM locations WHERE code=@stop2)))/1000,2)
UNION ALL
SELECT CONCAT(@origin,' → ',@stop2,' → ',@stop1,' → ',@stop3),
  ROUND((ST_Distance_Sphere((SELECT position FROM locations WHERE code=@origin),(SELECT position FROM locations WHERE code=@stop2))
       + ST_Distance_Sphere((SELECT position FROM locations WHERE code=@stop2),(SELECT position FROM locations WHERE code=@stop1))
       + ST_Distance_Sphere((SELECT position FROM locations WHERE code=@stop1),(SELECT position FROM locations WHERE code=@stop3)))/1000,2)
UNION ALL
SELECT CONCAT(@origin,' → ',@stop2,' → ',@stop3,' → ',@stop1),
  ROUND((ST_Distance_Sphere((SELECT position FROM locations WHERE code=@origin),(SELECT position FROM locations WHERE code=@stop2))
       + ST_Distance_Sphere((SELECT position FROM locations WHERE code=@stop2),(SELECT position FROM locations WHERE code=@stop3))
       + ST_Distance_Sphere((SELECT position FROM locations WHERE code=@stop3),(SELECT position FROM locations WHERE code=@stop1)))/1000,2)
UNION ALL
SELECT CONCAT(@origin,' → ',@stop3,' → ',@stop1,' → ',@stop2),
  ROUND((ST_Distance_Sphere((SELECT position FROM locations WHERE code=@origin),(SELECT position FROM locations WHERE code=@stop3))
       + ST_Distance_Sphere((SELECT position FROM locations WHERE code=@stop3),(SELECT position FROM locations WHERE code=@stop1))
       + ST_Distance_Sphere((SELECT position FROM locations WHERE code=@stop1),(SELECT position FROM locations WHERE code=@stop2)))/1000,2)
UNION ALL
SELECT CONCAT(@origin,' → ',@stop3,' → ',@stop2,' → ',@stop1),
  ROUND((ST_Distance_Sphere((SELECT position FROM locations WHERE code=@origin),(SELECT position FROM locations WHERE code=@stop3))
       + ST_Distance_Sphere((SELECT position FROM locations WHERE code=@stop3),(SELECT position FROM locations WHERE code=@stop2))
       + ST_Distance_Sphere((SELECT position FROM locations WHERE code=@stop2),(SELECT position FROM locations WHERE code=@stop1)))/1000,2)
ORDER BY total_km ASC
LIMIT 1;   -- best order
```

### Simpler — Stored Procedure for Trip Optimization

```sql
DELIMITER //

CREATE PROCEDURE optimize_trip(
  IN p_origin  VARCHAR(20),
  IN p_stop1   VARCHAR(20),
  IN p_stop2   VARCHAR(20),
  IN p_stop3   VARCHAR(20)
)
BEGIN
  -- Calculate total distance for all 6 orderings, return the best one
  SELECT route, total_km, visit_order
  FROM (
    SELECT '1-2-3' AS visit_order,
           CONCAT(p_origin,' → ',p_stop1,' → ',p_stop2,' → ',p_stop3) AS route,
           ROUND((
             ST_Distance_Sphere((SELECT position FROM locations WHERE code=p_origin),
                                (SELECT position FROM locations WHERE code=p_stop1)) +
             ST_Distance_Sphere((SELECT position FROM locations WHERE code=p_stop1),
                                (SELECT position FROM locations WHERE code=p_stop2)) +
             ST_Distance_Sphere((SELECT position FROM locations WHERE code=p_stop2),
                                (SELECT position FROM locations WHERE code=p_stop3))
           ) / 1000, 2) AS total_km
    UNION ALL
    SELECT '1-3-2', CONCAT(p_origin,' → ',p_stop1,' → ',p_stop3,' → ',p_stop2),
           ROUND((ST_Distance_Sphere((SELECT position FROM locations WHERE code=p_origin),(SELECT position FROM locations WHERE code=p_stop1))
                + ST_Distance_Sphere((SELECT position FROM locations WHERE code=p_stop1),(SELECT position FROM locations WHERE code=p_stop3))
                + ST_Distance_Sphere((SELECT position FROM locations WHERE code=p_stop3),(SELECT position FROM locations WHERE code=p_stop2)))/1000,2)
    UNION ALL
    SELECT '2-1-3', CONCAT(p_origin,' → ',p_stop2,' → ',p_stop1,' → ',p_stop3),
           ROUND((ST_Distance_Sphere((SELECT position FROM locations WHERE code=p_origin),(SELECT position FROM locations WHERE code=p_stop2))
                + ST_Distance_Sphere((SELECT position FROM locations WHERE code=p_stop2),(SELECT position FROM locations WHERE code=p_stop1))
                + ST_Distance_Sphere((SELECT position FROM locations WHERE code=p_stop1),(SELECT position FROM locations WHERE code=p_stop3)))/1000,2)
    UNION ALL
    SELECT '2-3-1', CONCAT(p_origin,' → ',p_stop2,' → ',p_stop3,' → ',p_stop1),
           ROUND((ST_Distance_Sphere((SELECT position FROM locations WHERE code=p_origin),(SELECT position FROM locations WHERE code=p_stop2))
                + ST_Distance_Sphere((SELECT position FROM locations WHERE code=p_stop2),(SELECT position FROM locations WHERE code=p_stop3))
                + ST_Distance_Sphere((SELECT position FROM locations WHERE code=p_stop3),(SELECT position FROM locations WHERE code=p_stop1)))/1000,2)
    UNION ALL
    SELECT '3-1-2', CONCAT(p_origin,' → ',p_stop3,' → ',p_stop1,' → ',p_stop2),
           ROUND((ST_Distance_Sphere((SELECT position FROM locations WHERE code=p_origin),(SELECT position FROM locations WHERE code=p_stop3))
                + ST_Distance_Sphere((SELECT position FROM locations WHERE code=p_stop3),(SELECT position FROM locations WHERE code=p_stop1))
                + ST_Distance_Sphere((SELECT position FROM locations WHERE code=p_stop1),(SELECT position FROM locations WHERE code=p_stop2)))/1000,2)
    UNION ALL
    SELECT '3-2-1', CONCAT(p_origin,' → ',p_stop3,' → ',p_stop2,' → ',p_stop1),
           ROUND((ST_Distance_Sphere((SELECT position FROM locations WHERE code=p_origin),(SELECT position FROM locations WHERE code=p_stop3))
                + ST_Distance_Sphere((SELECT position FROM locations WHERE code=p_stop3),(SELECT position FROM locations WHERE code=p_stop2))
                + ST_Distance_Sphere((SELECT position FROM locations WHERE code=p_stop2),(SELECT position FROM locations WHERE code=p_stop1)))/1000,2)
  ) orderings
  ORDER BY total_km ASC
  LIMIT 1;
END //

DELIMITER ;

-- Usage
CALL optimize_trip('ADMIN-HQ', 'PLT-001', 'BST-001', 'BST-002');
```

---

## 9. 🧭 Finding the Best Starting Waypoint for a New Location

When a driver needs to go to an **unknown new location** (GPS point not in your system), find the nearest known landmark on an approved path, then guide from there.

```sql
-- Given a new destination GPS point, find which known landmark is nearest
-- and which path passes closest to that new point

SET @new_lat = 30.1450;
SET @new_lng = 31.3350;
SET @new_point = ST_PointFromText(CONCAT('POINT(', @new_lng, ' ', @new_lat, ')'), 4326);

-- Step 1: Find the 3 closest known landmarks to the new destination
SELECT
  l.code,
  l.name,
  lt.label AS type,
  ROUND(ST_Distance_Sphere(l.position, @new_point)) AS meters_to_dest,
  l.notes AS access_notes,
  ST_X(l.position) AS lng,
  ST_Y(l.position) AS lat
FROM locations l
JOIN location_types lt ON lt.id = l.type_id
WHERE l.is_waypoint = TRUE
  AND l.is_active   = TRUE
ORDER BY ST_Distance_Sphere(l.position, @new_point) ASC
LIMIT 3;
```

```sql
-- Step 2: Find which stored PATH passes closest to the new point
-- (useful to identify which route the driver should branch off from)
SELECT
  p.code              AS path_code,
  p.name              AS path_name,
  lo.name             AS from_location,
  ld.name             AS to_location,
  p.total_distance_m,
  -- How close does this path's geometry come to the new point?
  ROUND(ST_Distance_Sphere(
    ST_ClosestPoint(p.geometry, @new_point),   -- PostGIS syntax
    @new_point
  )) AS meters_path_to_dest
FROM paths p
JOIN locations lo ON lo.id = p.origin_id
JOIN locations ld ON ld.id = p.destination_id
WHERE p.is_active = TRUE
ORDER BY ST_Distance(p.geometry, @new_point) ASC
LIMIT 3;
```

```sql
-- Step 3: Combined — nearest landmark that is also on a stored path
-- This gives the driver: "Follow PATH-HQ-PLT001 until LMK-003,
-- then continue 2.1 km to your new destination"
SELECT
  pw.path_id,
  p.code              AS path_code,
  p.name              AS path_name,
  l.code              AS branch_point_code,
  l.name              AS branch_point_name,
  pw.sequence         AS sequence_in_path,
  pw.instruction      AS instruction_at_branch,
  ROUND(ST_Distance_Sphere(l.position, @new_point) / 1000, 2) AS km_to_new_dest,
  -- cumulative time to reach this waypoint
  (
    SELECT SUM(pw2.duration_from_prev_min)
    FROM path_waypoints pw2
    WHERE pw2.path_id = pw.path_id
      AND pw2.sequence <= pw.sequence
  ) AS mins_to_branch_point
FROM path_waypoints pw
JOIN paths      p ON p.id = pw.path_id
JOIN locations  l ON l.id = pw.location_id
WHERE p.is_active = TRUE
ORDER BY ST_Distance_Sphere(l.position, @new_point) ASC
LIMIT 5;
```

---

## 10. 🛠️ Maintenance & Data Quality Queries

### Find Locations with No Stored Paths

```sql
SELECT
  l.code, l.name, lt.label AS type
FROM locations l
JOIN location_types lt ON lt.id = l.type_id
WHERE l.is_destination = TRUE
  AND l.is_active = TRUE
  AND l.id NOT IN (
    SELECT origin_id      FROM paths WHERE is_active = TRUE
    UNION
    SELECT destination_id FROM paths WHERE is_active = TRUE
  )
ORDER BY lt.code, l.name;
```

---

### Find Paths with Missing Waypoints or Broken Sequences

```sql
-- Paths that have no waypoints at all
SELECT p.code, p.name
FROM paths p
WHERE p.is_active = TRUE
  AND NOT EXISTS (
    SELECT 1 FROM path_waypoints pw WHERE pw.path_id = p.id
  );

-- Paths where sequence numbers are not continuous
SELECT
  p.code,
  p.name,
  COUNT(pw.id) AS waypoint_count,
  MAX(pw.sequence) AS max_sequence,
  CASE WHEN COUNT(pw.id) = MAX(pw.sequence) THEN 'OK' ELSE '⚠️ GAP IN SEQUENCE' END AS status
FROM paths p
JOIN path_waypoints pw ON pw.path_id = p.id
GROUP BY p.id
HAVING MAX(pw.sequence) <> COUNT(pw.id);
```

---

### Refresh Proximity Matrix (Run After Adding/Moving Locations)

```sql
-- Delete stale entries, recompute all pairs
DELETE FROM location_proximity;

INSERT INTO location_proximity (location_a_id, location_b_id, distance_m, has_direct_path, path_id)
SELECT
  LEAST(a.id, b.id)    AS location_a_id,
  GREATEST(a.id, b.id) AS location_b_id,
  ROUND(ST_Distance_Sphere(a.position, b.position)) AS distance_m,
  CASE WHEN p.id IS NOT NULL THEN TRUE ELSE FALSE END,
  p.id
FROM locations a
JOIN locations b ON a.id <> b.id
LEFT JOIN paths p ON (
  (p.origin_id = a.id AND p.destination_id = b.id) OR
  (p.origin_id = b.id AND p.destination_id = a.id AND p.is_bidirectional = TRUE)
)
WHERE a.is_active = TRUE AND b.is_active = TRUE AND a.id < b.id
ON DUPLICATE KEY UPDATE
  distance_m = VALUES(distance_m),
  has_direct_path = VALUES(has_direct_path),
  path_id = VALUES(path_id),
  updated_at = NOW();
```

---

### Validate All Polygon Geometries and Point SRIDs

```sql
-- Find any locations with wrong or missing SRID
SELECT code, name, ST_SRID(position) AS srid
FROM locations
WHERE ST_SRID(position) <> 4326;

-- Find invalid path geometries
SELECT p.code, p.name
FROM paths p
WHERE p.geometry IS NOT NULL
  AND NOT ST_IsValid(p.geometry);
```

---

## 11. 🔁 Full Working Example — End to End

### Scenario
> "I am at HQ. I need to visit 3 locations today — pick the best cluster of destinations, tell me the optimal order to visit them, and give me the turn-by-turn path to the first stop."

```sql
-- ============================================================
-- STEP 1: Find best 3-stop cluster within 40 km of HQ
-- ============================================================
SET @origin = 'ADMIN-HQ';
SET @max_km = 40;

SELECT
  CONCAT(a.code, ' + ', b.code, ' + ', c.code)   AS cluster,
  a.name AS stop_1, ROUND(a.km,1) AS km_1,
  b.name AS stop_2, ROUND(b.km,1) AS km_2,
  c.name AS stop_3, ROUND(c.km,1) AS km_3,
  ROUND((
    ST_Distance_Sphere((SELECT position FROM locations WHERE code=a.code),
                       (SELECT position FROM locations WHERE code=b.code)) +
    ST_Distance_Sphere((SELECT position FROM locations WHERE code=b.code),
                       (SELECT position FROM locations WHERE code=c.code)) +
    ST_Distance_Sphere((SELECT position FROM locations WHERE code=a.code),
                       (SELECT position FROM locations WHERE code=c.code))
  ) / 1000, 1) AS cluster_spread_km
FROM (
  SELECT l.code, l.name,
         ST_Distance_Sphere(l.position, o.position)/1000 AS km
  FROM locations l
  JOIN locations o ON o.code = @origin
  WHERE l.is_destination=TRUE AND l.is_active=TRUE AND l.code<>@origin
    AND ST_Distance_Sphere(l.position, o.position)/1000 <= @max_km
) a
JOIN (SELECT l.code, l.name, ST_Distance_Sphere(l.position, o.position)/1000 AS km
      FROM locations l JOIN locations o ON o.code=@origin
      WHERE l.is_destination=TRUE AND l.is_active=TRUE AND l.code<>@origin
        AND ST_Distance_Sphere(l.position,o.position)/1000 <= @max_km) b ON b.code > a.code
JOIN (SELECT l.code, l.name, ST_Distance_Sphere(l.position, o.position)/1000 AS km
      FROM locations l JOIN locations o ON o.code=@origin
      WHERE l.is_destination=TRUE AND l.is_active=TRUE AND l.code<>@origin
        AND ST_Distance_Sphere(l.position,o.position)/1000 <= @max_km) c ON c.code > b.code
ORDER BY cluster_spread_km ASC
LIMIT 1;
-- Result: PLT-001 + BST-001 + BST-002 (spread = 23.8 km)

-- ============================================================
-- STEP 2: Best visiting order for the selected 3 stops
-- ============================================================
CALL optimize_trip('ADMIN-HQ', 'PLT-001', 'BST-001', 'BST-002');
-- Result: HQ → BST-001 → PLT-001 → BST-002 (38.2 km total)

-- ============================================================
-- STEP 3: Get turn-by-turn path HQ → BST-001 (first stop)
-- ============================================================
SELECT
  pw.sequence,
  l.name          AS waypoint,
  pw.instruction,
  pw.landmark_note,
  CONCAT(pw.distance_from_prev_m, 'm')  AS distance,
  CONCAT(pw.duration_from_prev_min, ' min') AS time
FROM paths p
JOIN path_waypoints pw ON pw.path_id = p.id
JOIN locations l ON l.id = pw.location_id
WHERE p.origin_id      = (SELECT id FROM locations WHERE code='ADMIN-HQ')
  AND p.destination_id = (SELECT id FROM locations WHERE code='BST-001')
  AND p.is_active = TRUE
ORDER BY pw.sequence;
```

---

## 12. 📇 Indexing Strategy

```sql
-- Core spatial indexes (already defined in schema)
-- locations.position         → SPATIAL INDEX idx_location_pos
-- paths.geometry             → SPATIAL INDEX idx_path_geom
-- path_waypoints.segment_geom → SPATIAL INDEX idx_pw_segment

-- Additional performance indexes
CREATE INDEX idx_loc_type_active  ON locations     (type_id, is_active, is_destination);
CREATE INDEX idx_loc_active_dest  ON locations     (is_active, is_destination);
CREATE INDEX idx_path_origin      ON paths         (origin_id, is_active);
CREATE INDEX idx_path_dest        ON paths         (destination_id, is_active);
CREATE INDEX idx_path_both        ON paths         (origin_id, destination_id, is_active);
CREATE INDEX idx_pw_path_seq      ON path_waypoints(path_id, sequence);
CREATE INDEX idx_lp_dist_a        ON location_proximity (location_a_id, distance_m);
CREATE INDEX idx_lp_dist_b        ON location_proximity (location_b_id, distance_m);
CREATE INDEX idx_trip_status      ON trips         (status, planned_date);
```

---

## 13. 💡 Extension Ideas

### A — Path Versioning
Track changes to paths over time (road closures, new roads):
```sql
ALTER TABLE paths ADD COLUMN version       TINYINT NOT NULL DEFAULT 1;
ALTER TABLE paths ADD COLUMN valid_from    DATE;
ALTER TABLE paths ADD COLUMN valid_to      DATE;
ALTER TABLE paths ADD COLUMN replaced_by   INT REFERENCES paths(id);
```

### B — Real-Time Driver Position Tracking
```sql
CREATE TABLE driver_positions (
  id          INT      NOT NULL AUTO_INCREMENT PRIMARY KEY,
  driver_id   INT      NOT NULL,
  trip_id     INT,
  position    POINT    NOT NULL SRID 4326,
  recorded_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  speed_kmh   DECIMAL(5,1),
  SPATIAL INDEX idx_drv_pos (position)
);
-- Query: Is driver still on the approved path?
-- Compare driver.position against path.geometry using ST_Distance
```

### C — Automatic Path Suggestion Score
```sql
-- Score existing paths by how close they pass to a new destination
CREATE VIEW path_relevance AS
SELECT
  p.id, p.code, p.name,
  ST_Distance_Sphere(p.geometry, l.position) AS min_dist_to_dest
FROM paths p
CROSS JOIN locations l
WHERE l.is_active = TRUE;
```

### D — Heat Map of Most-Used Waypoints
```sql
-- Which waypoints appear in the most paths?
SELECT
  l.code, l.name,
  COUNT(DISTINCT pw.path_id) AS used_in_paths,
  lt.label AS type
FROM path_waypoints pw
JOIN locations l ON l.id = pw.location_id
JOIN location_types lt ON lt.id = l.type_id
GROUP BY l.id
ORDER BY used_in_paths DESC;
```

### E — pgRouting (PostgreSQL Advanced Routing)
For true shortest-path routing on your road graph using Dijkstra's algorithm:
```sql
-- Requires pgRouting extension
SELECT * FROM pgr_dijkstra(
  'SELECT id, source, target, cost FROM path_segments',
  start_node_id,
  end_node_id,
  directed := FALSE
);
```

---

## Summary — What Each Table Stores

| Table | Purpose |
|-------|---------|
| `location_types` | Categories: Plant, Booster, Admin, Landmark, Checkpoint |
| `locations` | All known GPS points — facilities AND road landmarks |
| `road_restrictions` | Weight limits, permit requirements, access rules |
| `paths` | Named approved routes between two locations |
| `path_waypoints` | Ordered turn-by-turn stops within each path |
| `path_restrictions` | Which restrictions apply to which path |
| `location_proximity` | Pre-computed pairwise distances (fast cluster queries) |
| `trips` | Planned or completed multi-stop visits |
| `trip_stops` | The ordered stops within each trip |

---

*Designed for MySQL 8.0+. PostGIS equivalents available for ST_ClosestPoint, ST_DWithin, and pgRouting for advanced graph routing.*
