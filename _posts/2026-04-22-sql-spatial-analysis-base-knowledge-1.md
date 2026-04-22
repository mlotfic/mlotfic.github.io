---

title: SQL Spatial Analysis Base Knowledge Guide

description: >-
  A comprehensive guide to spatial analysis, covering geometry types, coordinate systems, spatial functions, and real-world use cases. Includes inline and table-level syntax, add/drop/modify examples, cross-engine compatibility, naming best practices, and common patterns.

date: 2026-04-22 10:00:00 +0800
author: Mahmoud Lotfi
file_name: 2026-04-22-sql-spatial-analysis-base-knowledge-1.md
categories: [SQL, Spatial Analysis, base-knowledge]
tags: [SQL, Spatial Analysis, base-knowledge]
pin: False
math: true
mermaid: true
comments: true
toc: true
render_with_liquid: false

image:
  path: /assets/img/posts/sql.jpg
  alt: SQL Spatial Analysis Base Knowledge Guide
  lqip: data:image/webp;base64,UklGRjoAAABXRUJQVlA4IC4AAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
---

# 🌍 Spatial Analysis — Base Knowledge Guide

> Everything you need to understand and work with spatial data, geometry types, coordinate systems, and spatial functions

---

## in article

Here's your Spatial Analysis Base Knowledge guide! It's structured as a **learning path** from fundamentals to advanced patterns across **13 sections**:

| # | Section | What You'll Learn |
|---|---------|------------------|
| 1 | **What is Spatial Analysis?** | Core questions spatial data answers, vector vs raster |
| 2 | **How Computers Represent Space** | X/Y axes, lat/lng axis order, coordinate plane |
| 3 | **Coordinate Systems & SRID** | WGS84, Web Mercator, UTM, flat vs spherical math — the most critical concept |
| 4 | **Geometry Types** | POINT, LINESTRING, POLYGON, MULTI*, GEOMETRYCOLLECTION — visuals + SQL examples |
| 5 | **Spatial Relationships (DE-9IM)** | Visual guide to all 8 predicates (Contains, Within, Intersects, Touches…) + decision table |
| 6 | **Measurement Concepts** | Distance formulas, area units, azimuth/bearing |
| 7 | **Spatial Indexes** | How R-Tree / GiST work, when indexes are used vs skipped, two-pass query strategy |
| 8 | **Data Formats** | WKT, WKB, GeoJSON — when to use each, axis order in GeoJSON |
| 9 | **Spatial Operations Explained** | Buffer, Intersection, Union, Difference, Centroid, Convex Hull, Simplify — all with ASCII visuals |
| 10 | **Real-World Use Cases** | Store locator, geofencing, reverse geocoding, density heatmap, infrastructure alerts |
| 11 | **Common Mistakes & Gotchas** | 10 traps with wrong vs correct SQL — lat/lng swap, SRID mixing, unclosed rings, area in degrees |
| 12 | **Choosing the Right Tool** | MySQL vs PostGIS vs SpatiaLite vs SQL Server vs GIS software — decision table |
| 13 | **Glossary** | 40+ spatial terms defined |

The guide uses **ASCII diagrams** throughout to visualize abstract geometry concepts without needing external images.


---

## Table of Contents
1. [What is Spatial Analysis?](#1--what-is-spatial-analysis)
2. [How Computers Represent Space](#2--how-computers-represent-space)
3. [Coordinate Systems & SRID](#3--coordinate-systems--srid)
4. [Geometry Types](#4--geometry-types)
5. [Spatial Relationships — The DE-9IM Model](#5--spatial-relationships--the-de-9im-model)
6. [Measurement Concepts](#6--measurement-concepts)
7. [Spatial Indexes — How They Work](#7--spatial-indexes--how-they-work)
8. [Data Formats (WKT, WKB, GeoJSON)](#8--data-formats-wkt-wkb-geojson)
9. [Common Spatial Operations Explained](#9--common-spatial-operations-explained)
10. [Real-World Use Cases](#10--real-world-use-cases)
11. [Common Mistakes & Gotchas](#11--common-mistakes--gotchas)
12. [Choosing the Right Tool / Engine](#12--choosing-the-right-tool--engine)
13. [Glossary](#13--glossary)

---

## 1. 🔭 What is Spatial Analysis?

**Spatial analysis** is the process of examining the locations, attributes, and relationships of features in geographic or geometric space to answer questions like:

- Where is the nearest hospital to this patient?
- Which houses are inside a flood zone?
- How much area does this city cover?
- Which delivery routes cross restricted zones?
- How many customers live within 10 km of our store?

Spatial analysis extends regular data analysis with a **location dimension** — it adds the concept of *where* things are and *how they relate* to each other in space.

### Two Domains of Spatial Data

| Domain | Description | Examples |
|--------|-------------|---------|
| **Geographic** | Real-world Earth locations using lat/lng | GPS tracks, city boundaries, rivers |
| **Geometric** | Abstract 2D/3D space, any coordinate system | Floor plans, circuit boards, game maps |

SQL databases handle both using the same functions — the difference lies in the **coordinate system** you choose (see Section 3).

---

## 2. 💻 How Computers Represent Space

### The Fundamental Building Blocks

Everything in spatial analysis is built from three primitive concepts:

```
Point  →  A location (x, y)
Line   →  Two or more connected points
Area   →  A closed line (ring) that encloses space
```

A **Point** is the simplest. It has exactly two values:
- `X` = horizontal position (longitude on Earth)
- `Y` = vertical position (latitude on Earth)

```
Point(31.2357, 30.0444)
        │         │
      X/lng     Y/lat
      (Cairo)
```

> ⚠️ **Important axis order**: In mathematics and most spatial functions, the order is `(X, Y)` which maps to `(longitude, latitude)`. This is the **opposite** of how humans say it ("lat, lng"). This is one of the most common sources of confusion in spatial work.

### The Coordinate Plane

```
        Y (North / Latitude)
        │
   90°  │
        │
    0°  │──────────────────── X (East / Longitude)
        │         0°      180°
  -90°  │
```

On Earth:
- **Longitude** (X): −180° (West) to +180° (East), 0° = Greenwich
- **Latitude** (Y): −90° (South Pole) to +90° (North Pole), 0° = Equator

### Vector vs Raster

SQL databases use **vector** spatial data — shapes defined by coordinates:

| Model | Description | SQL support |
|-------|-------------|-------------|
| **Vector** | Shapes as points, lines, polygons | ✅ Full support |
| **Raster** | Grid of pixels (satellite images, elevation) | ⚠️ Limited (PostGIS Raster) |

---

## 3. 🗺️ Coordinate Systems & SRID

This is the most critical concept to understand before doing any spatial work.

### Why Coordinate Systems Matter

The Earth is a **3D sphere** but your screen (and your database) is **flat**. Every coordinate system is a mathematical recipe for projecting the round Earth onto a flat surface — like peeling an orange and pressing it flat. Every projection distorts something: shape, area, distance, or direction.

```
       Real Earth              Flat Map
      (sphere/ellipsoid)      (projection)
           ○                    ──────────
        /     \                |          |
       |  🌍   |    →→→      |   🗺️    |
        \     /                |          |
           ○                    ──────────
                           (some distortion added)
```

### SRID — Spatial Reference System Identifier

An **SRID** (Spatial Reference System Identifier) is a number that uniquely identifies a coordinate system. Think of it as a "language code" for coordinates — you must know what coordinate system data is in before you can correctly measure or compare it.

```sql
-- SRID is embedded in the geometry
SELECT ST_SRID(position) FROM locations;   -- returns e.g. 4326

-- Create geometry with SRID
ST_PointFromText('POINT(31.2357 30.0444)', 4326)
                                            ↑
                              This says: "these coords are WGS84 GPS"
```

### The Most Important SRIDs

#### SRID 4326 — WGS 84 (GPS Standard)
- **What it is**: The global GPS standard used by all modern GPS devices, Google Maps, smartphones
- **Units**: Degrees of latitude and longitude
- **Range**: X = −180 to 180, Y = −90 to 90
- **Best for**: Storing GPS coordinates, global data, interchange format
- **Problem**: Degrees are not equal in meters — 1° latitude ≠ 1° longitude in meters

```sql
-- Cairo in WGS84
POINT(31.2357 30.0444)   -- X=longitude, Y=latitude
```

#### SRID 3857 — Web Mercator (Google Maps / OpenStreetMap)
- **What it is**: The projection used by all web mapping services
- **Units**: Meters (approximately)
- **Best for**: Displaying maps on screen, tile-based web maps
- **Problem**: Severe area distortion near the poles (Greenland looks the size of Africa)

```sql
-- Cairo in Web Mercator (same real location, different numbers)
POINT(3477088 3507280)   -- X and Y in meters
```

#### SRID 32636 — UTM Zone 36N (Egypt / Middle East)
- **What it is**: A local projection accurate for Egypt and nearby regions
- **Units**: True meters
- **Best for**: Accurate distance and area calculations in Egypt/Levant
- **Problem**: Only works for a specific geographic band

```sql
-- Cairo in UTM 36N
POINT(322262 3322078)   -- X=easting meters, Y=northing meters
```

### Flat (Cartesian) vs Spherical (Geographic) Math

This is the second most important concept:

```
Flat Math (GEOMETRY type):
  Treats the Earth as a flat piece of paper.
  Fast to compute.
  Accurate for small areas (< ~50 km).
  Inaccurate for long distances (e.g., intercontinental).

Spherical Math (GEOGRAPHY type — PostGIS/SQL Server):
  Treats the Earth as a curved sphere.
  Slower to compute.
  Accurate everywhere on Earth.
  Always returns meters for distances and m² for areas.
```

**Rule of thumb:**
- For data within a **city or country**: flat math with a local SRID (e.g., UTM) is fine
- For **global or intercontinental** data: use `GEOGRAPHY` type (PostGIS/SQL Server) or `ST_Distance_Sphere()` (MySQL)

```sql
-- MySQL: flat distance in degrees (not meters!) — WRONG for real distances
SELECT ST_Distance(point_a, point_b);

-- MySQL: accurate spherical distance in meters — CORRECT
SELECT ST_Distance_Sphere(point_a, point_b);

-- PostGIS: cast to geography for spherical accuracy
SELECT ST_Distance(point_a::geography, point_b::geography);
```

### How to Choose Your SRID

```
Q: Is your data global (whole world)?
   YES → Use SRID 4326 for storage
         Use ST_Distance_Sphere() or geography type for measurements

Q: Is your data regional (one country / city)?
   YES → Use a local UTM projection for that region
         This gives you true meter/km measurements

Q: Are you displaying data on a web map (Google Maps, Leaflet)?
   YES → Store as 4326, display as 3857 (or let the mapping library handle it)

Q: Do you need pixel-accurate display on screen?
   YES → Use 3857 (Web Mercator)
```

---

## 4. 📐 Geometry Types

### The Type Hierarchy

```
GEOMETRY (abstract base — any type)
├── POINT
├── CURVE (abstract)
│   └── LINESTRING
├── SURFACE (abstract)
│   └── POLYGON
└── GEOMETRYCOLLECTION
    ├── MULTIPOINT
    ├── MULTICURVE
    │   └── MULTILINESTRING
    ├── MULTISURFACE
    │   └── MULTIPOLYGON
    └── GEOMETRYCOLLECTION (mixed)
```

---

### POINT — Zero dimensions

A single location. The most fundamental type.

```
 •  ← A point

Coordinates: (X, Y)
```

```sql
-- A restaurant location in Cairo
POINT(31.2357 30.0444)

-- In SQL
SELECT ST_PointFromText('POINT(31.2357 30.0444)', 4326);
SELECT ST_X(position) AS longitude, ST_Y(position) AS latitude FROM stores;
```

**Real-world uses**: Store locations, GPS waypoints, events, IP locations, user check-ins

---

### LINESTRING — One dimension

An ordered sequence of two or more points connected by straight segments.

```
  •─────•─────•─────•
  start              end
```

```sql
-- A road with 4 waypoints
LINESTRING(31.20 30.00, 31.25 30.05, 31.30 30.10, 31.35 30.15)

-- Properties
ST_Length(route)          -- total length
ST_NumPoints(route)       -- number of vertices
ST_StartPoint(route)      -- first point
ST_EndPoint(route)        -- last point
ST_PointN(route, 3)       -- 3rd vertex
```

**Real-world uses**: Roads, rivers, pipelines, flight paths, hiking trails, transmission lines

**Closed LineString** (first point = last point):
```sql
LINESTRING(0 0, 1 0, 1 1, 0 1, 0 0)   -- a square outline (but NOT a polygon)
```

---

### POLYGON — Two dimensions

A closed ring defining an area. The first and last coordinate must be identical to close the ring.

```
  •────────•
  │        │
  │  area  │    ← filled area
  │        │
  •────────•  (closing point = starting point)
```

```sql
-- A city block (must close: last = first)
POLYGON((31.20 30.00, 31.25 30.00, 31.25 30.05, 31.20 30.05, 31.20 30.00))
         └─ start ─┘                                           └─ close ─┘

-- Properties
ST_Area(boundary)            -- area (in SRID units)
ST_Perimeter(boundary)       -- perimeter length
ST_Centroid(boundary)        -- geometric center point
ST_ExteriorRing(boundary)    -- outer ring as LINESTRING
```

**Polygon with a hole (donut shape)**:
```sql
-- Outer ring first, then inner ring(s) — each must also close
POLYGON(
  (31.00 29.90, 31.50 29.90, 31.50 30.50, 31.00 30.50, 31.00 29.90),  -- outer ring
  (31.10 30.00, 31.20 30.00, 31.20 30.10, 31.10 30.10, 31.10 30.00)   -- hole
)
```

**Winding rule**: Outer rings go **counter-clockwise**, holes go **clockwise** in most systems. If your polygon behaves unexpectedly, reversed winding may be the cause.

**Real-world uses**: City/country boundaries, land parcels, flood zones, building footprints, delivery zones, lake/forest outlines

---

### MULTIPOINT — Collection of Points

```
  •     •        •
     •       •
```

```sql
MULTIPOINT(31.20 30.00, 31.25 30.05, 31.30 30.10)

-- Extract individual points
ST_NumGeometries(mp)       -- count
ST_GeometryN(mp, 1)        -- first point
```

**Real-world uses**: ATM network, store chain locations, sensor array, tree survey

---

### MULTILINESTRING — Collection of LineStrings

```
  •────•────•          •──────•
                  •───•
```

```sql
MULTILINESTRING((31.00 30.00, 31.10 30.10),(31.20 30.00, 31.30 30.05))
```

**Real-world uses**: Disconnected road segments, river system with tributaries, power line network

---

### MULTIPOLYGON — Collection of Polygons

```
  ┌──────┐     ┌───┐
  │  A   │     │ B │
  └──────┘     └───┘
```

```sql
MULTIPOLYGON(
  ((31.00 30.00, 31.10 30.00, 31.10 30.10, 31.00 30.10, 31.00 30.00)),
  ((31.20 30.00, 31.30 30.00, 31.30 30.10, 31.20 30.10, 31.20 30.00))
)
```

**Real-world uses**: Countries with islands (Greece, Indonesia), fragmented land ownership, city with exclave zones

---

### GEOMETRYCOLLECTION — Mixed Types

```
  •     •────•────•     ┌──────┐
               point +  line  + polygon
```

```sql
GEOMETRYCOLLECTION(
  POINT(31.20 30.00),
  LINESTRING(31.00 30.00, 31.10 30.10),
  POLYGON((31.20 30.00, 31.30 30.00, 31.30 30.10, 31.20 30.00))
)
```

**Real-world uses**: Mixed dataset exports, GeoJSON FeatureCollections, heterogeneous spatial queries

---

### GEOMETRY — Generic Column Type

In SQL, you can declare a column as `GEOMETRY` to accept any geometry type:

```sql
CREATE TABLE map_features (
  id      INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
  name    VARCHAR(100),
  geom    GEOMETRY NOT NULL SRID 4326    -- accepts POINT, POLYGON, etc.
);

-- Check what type is stored
SELECT ST_GeometryType(geom) FROM map_features;
-- Returns: 'ST_Point', 'ST_Polygon', 'ST_LineString', etc.
```

---

## 5. 🔗 Spatial Relationships — The DE-9IM Model

The **DE-9IM (Dimensionally Extended 9-Intersection Model)** is the mathematical framework behind all spatial relationship functions. Understanding it helps you choose the right predicate.

### The Concept

Every geometry has three parts: **Interior (I)**, **Boundary (B)**, and **Exterior (E)**.

```
For a POLYGON:
  ┌──────────────────────────────────────────┐
  │                 Exterior (E)              │
  │                                           │
  │    ╔══════════════╗                       │
  │    ║              ║  ← Boundary (B)       │
  │    ║  Interior    ║                       │
  │    ║    (I)       ║                       │
  │    ╚══════════════╝                       │
  └──────────────────────────────────────────┘

For a POINT:
  The point itself = Interior
  No boundary (dimension -1)
  Everything else = Exterior
```

The DE-9IM checks all 9 combinations of intersections between the parts of geometry A and geometry B. Each spatial predicate function (ST_Contains, ST_Within, etc.) is a specific pattern of these 9 checks.

### Visual Guide to All Predicates

---

#### ST_Equals — Geometrically identical
```
  A: ┌──────┐
     │      │    A and B occupy exactly the same space
  B: └──────┘    (could have different vertex counts but same shape)

SELECT ST_Equals(geom_a, geom_b);   → 1 (true)
```

---

#### ST_Disjoint — No shared space at all
```
  ┌──────┐        ┌──────┐
  │  A   │        │  B   │    A and B are completely separate
  └──────┘        └──────┘

SELECT ST_Disjoint(geom_a, geom_b);  → 1
Note: ST_Disjoint = NOT ST_Intersects
```

---

#### ST_Intersects — Any shared space (most common check)
```
  ┌──────┐
  │  A ┌─┼────┐
  └────┼─┘  B │    Any overlap at all (interior, boundary, or both)
       └──────┘

SELECT ST_Intersects(geom_a, geom_b);  → 1
This is the OPPOSITE of ST_Disjoint.
Use this for: "Do these geometries touch or overlap at all?"
```

---

#### ST_Touches — Share only boundary (no interior overlap)
```
  ┌──────┐┌──────┐
  │  A   ││  B   │    They share an edge or point but do NOT overlap inside
  └──────┘└──────┘
           ↑
     shared boundary only

SELECT ST_Touches(geom_a, geom_b);  → 1
Use this for: adjacent polygons, roads that meet at a point
```

---

#### ST_Crosses — Interiors intersect, one goes through the other
```
  ──────•──────
        │         A line crosses through a polygon or another line
  ┌─────┼─────┐
  │     │  B  │
  └─────┼─────┘
        │

SELECT ST_Crosses(line, polygon);  → 1
Use this for: roads crossing zone boundaries, pipes crossing property lines
```

---

#### ST_Overlaps — Partial overlap of same-dimension geometries
```
  ┌──────┐
  │  A ┌─┼────┐
  │    │░│  B │    The shaded (░) area is shared — partial, not full
  └────┼─┘    │
       └──────┘

SELECT ST_Overlaps(poly_a, poly_b);  → 1
Use this for: overlapping land parcels, intersecting service areas
```

---

#### ST_Contains — A completely contains B (B inside A)
```
  ┌──────────────┐
  │      A       │
  │  ┌──────┐   │    B is fully inside A — no part of B touches A's exterior
  │  │  B   │   │
  │  └──────┘   │
  └──────────────┘

SELECT ST_Contains(A, B);  → 1
Note: boundary of B CAN touch boundary of A in MySQL
Use this for: points inside a zone, building inside a city
```

---

#### ST_Within — A is completely inside B (inverse of Contains)
```
  ┌──────────────┐
  │      B       │
  │  ┌──────┐   │
  │  │  A   │   │    A is inside B
  │  └──────┘   │
  └──────────────┘

SELECT ST_Within(A, B);    → 1    (same as ST_Contains(B, A))
Use this for: "Is this store within city limits?"
```

---

### Choosing the Right Predicate — Decision Table

| Question | Function |
|----------|----------|
| Do these two shapes share ANY space? | `ST_Intersects()` |
| Is point/shape fully INSIDE a polygon? | `ST_Contains(polygon, point)` |
| Is this polygon fully INSIDE another? | `ST_Within(inner, outer)` |
| Do they share a border but NOT interiors? | `ST_Touches()` |
| Do they partially overlap (same dimension)? | `ST_Overlaps()` |
| Does a line cross through a polygon? | `ST_Crosses()` |
| Are they completely separate? | `ST_Disjoint()` |
| Are they geometrically identical? | `ST_Equals()` |

---

### MBR Predicates — Fast Approximations

**MBR (Minimum Bounding Rectangle)** is a rectangle that fully encloses a geometry. MBR checks are much faster than exact checks because they use the spatial index directly.

```
  Complex polygon:         Its MBR (bounding box):
  ╱╲                       ┌────────┐
 ╱  ╲                      │  ╱╲   │
│    │         →→→         │ ╱  ╲  │
 ╲  ╱                      ││    │ │
  ╲╱                        │ ╲  ╱ │
                            │  ╲╱  │
                            └────────┘
  Exact shape               Simple rectangle
  (slow to test)            (fast to test, uses index)
```

**Strategy — two-pass spatial query:**
1. **Pass 1 (fast)**: Use MBR/bounding box to eliminate obviously non-matching rows using the spatial index
2. **Pass 2 (exact)**: Apply precise ST_Contains / ST_Intersects on remaining candidates

```sql
-- Efficient: bounding box first, then exact check
SELECT name
FROM stores
WHERE MBRContains(
        ST_Buffer(ST_PointFromText('POINT(31.2357 30.0444)', 4326), 0.05),
        position
      )                                       -- fast: uses index
  AND ST_Distance_Sphere(
        position,
        ST_PointFromText('POINT(31.2357 30.0444)', 4326)
      ) <= 5000;                              -- exact: meters
```

---

## 6. 📏 Measurement Concepts

### Distance

**Flat / Cartesian distance** (Pythagorean theorem on the coordinate plane):
```
distance = √((x₂−x₁)² + (y₂−y₁)²)
```
- Fast, but units depend on SRID
- With SRID 4326 → result is in **degrees** (not useful as meters)
- With a projected SRID (UTM, 3857) → result is in **meters**

**Spherical / Great-circle distance** (accounts for Earth's curvature):
```
Uses the Haversine formula or Vincenty formula
Result is always in meters
Accurate anywhere on Earth
```

```sql
-- MySQL: flat distance (degrees if using 4326 — not meters!)
SELECT ST_Distance(pt_cairo, pt_alex);            -- returns ~2.8 (degrees)

-- MySQL: spherical distance (always meters)
SELECT ST_Distance_Sphere(pt_cairo, pt_alex);     -- returns ~183,000 (meters)

-- PostGIS: cast to geography → spherical meters
SELECT ST_Distance(pt_cairo::geography, pt_alex::geography);  -- meters
```

### Area

Area is a **two-dimensional measurement**. Its unit is the square of the SRID unit:

| SRID | Distance unit | Area unit |
|------|--------------|-----------|
| 4326 | Degrees | Square degrees (useless!) |
| 3857 | Meters | m² (but distorted at lat/lng extremes) |
| 32636 UTM | Meters | m² (accurate for Egypt) |
| PostGIS geography | Meters | m² (accurate globally) |

```sql
-- Always divide by 1,000,000 to get km²
SELECT ST_Area(boundary) / 1000000 AS area_km2 FROM regions;

-- PostGIS: accurate area using geography
SELECT ST_Area(boundary::geography) / 1000000 AS area_km2 FROM regions;
```

### Length

The same rules as distance — the SRID determines units:

```sql
-- Route length
SELECT ST_Length(route) FROM routes;                        -- in SRID units
SELECT ST_Length(route::geography) / 1000 AS km FROM routes;  -- PostGIS: km
```

### Azimuth / Bearing

Direction from point A to point B, measured clockwise from north in radians (PostGIS):

```sql
-- PostGIS: bearing from Cairo to Alexandria
SELECT DEGREES(ST_Azimuth(
  ST_PointFromText('POINT(31.2357 30.0444)', 4326)::geography,
  ST_PointFromText('POINT(29.9553 31.2001)', 4326)::geography
)) AS bearing_degrees;
-- 0° = North, 90° = East, 180° = South, 270° = West
```

---

## 7. 📇 Spatial Indexes — How They Work

Without a spatial index, every spatial query reads **every row** in the table (full table scan). For 1 million locations, that means testing all 1 million rows for `ST_Contains`, `ST_Distance`, etc. A spatial index reduces this to only a handful of candidates.

### R-Tree Index (Used by MySQL, Oracle, SpatiaLite)

An **R-Tree** organizes geometries into nested bounding rectangles:

```
Level 0 (root):   one big bounding box covering all data
                  ┌──────────────────────────────────────┐
                  │                                      │
Level 1:      ┌───┼────────┐       ┌────────────┐       │
              │   │  Box A │       │   Box B    │       │
              └───┼────────┘       └────────────┘       │
                  │                                      │
Level 2:     ┌────┼──┐  ┌────┐  ┌────┐  ┌──────┐       │
             │ a1 │  │  │ a2 │  │ b1 │  │  b2  │       │
             └────┘  └──┘    └──┘    └──┘      └───────┘

Actual points/polygons sit in the leaf nodes.
```

**How a query uses the R-Tree**:
```
Query: "Find all stores within this polygon"

1. Check root bounding box → does it overlap my polygon? YES → go deeper
2. Check Level 1 boxes     → Box A overlaps? YES | Box B overlaps? NO → skip B
3. Check Level 2 boxes     → a1 overlaps? YES, a2 overlaps? NO
4. Check actual rows in a1 → run exact ST_Contains on ~3 rows

Result: Instead of testing 10,000 rows, only 3 rows were exactly tested.
```

### GiST Index (Used by PostGIS)

**GiST (Generalized Search Tree)** is a flexible index framework. For spatial data it behaves similarly to R-Tree but supports more operators and geometry types including `GEOGRAPHY`.

### Key Rules for Spatial Indexes

```sql
-- MySQL: column must be NOT NULL for a SPATIAL INDEX
ALTER TABLE locations ADD SPATIAL INDEX idx_pos (position);   -- ✅
-- position column must be declared NOT NULL

-- PostGIS: no NOT NULL requirement
CREATE INDEX idx_pos ON locations USING GIST (position);     -- ✅

-- The index is used automatically by the query planner when you use spatial operators
-- You do NOT need to hint the index manually in most cases
```

### When the Index Is Used vs Skipped

| Situation | Index used? |
|-----------|-------------|
| `ST_Contains(indexed_col, ?)` | ✅ |
| `ST_Intersects(indexed_col, ?)` | ✅ |
| `ST_Within(indexed_col, ?)` | ✅ |
| `ST_Distance(col, ?) < 5000` | ❌ (MySQL) — distance calc ignores index |
| `ST_Distance_Sphere(col, ?) < 5000` | ❌ — use bounding box pre-filter |
| PostGIS `col::geography <-> point` (KNN) | ✅ |
| `ST_DWithin(col, point, dist)` | ✅ (PostGIS — uses index!) |

**Best practice for distance queries:**
```sql
-- Step 1: narrow candidates with a bounding box (uses index)
-- Step 2: apply exact distance filter
SELECT name, ST_Distance_Sphere(position, @center) AS dist
FROM stores
WHERE ST_Contains(
  ST_Buffer(@center, 0.05),   -- rough bounding box — uses index
  position
)
AND ST_Distance_Sphere(position, @center) <= 5000;   -- exact filter
```

---

## 8. 📄 Data Formats (WKT, WKB, GeoJSON)

### WKT — Well-Known Text

**Human-readable** text format. Use for debugging, SQL queries, and display.

```
POINT(31.2357 30.0444)
LINESTRING(31.00 30.00, 31.10 30.05, 31.20 30.10)
POLYGON((31.00 30.00, 31.10 30.00, 31.10 30.10, 31.00 30.10, 31.00 30.00))
MULTIPOINT(31.00 30.00, 31.10 30.05)
GEOMETRYCOLLECTION(POINT(31.0 30.0), LINESTRING(31.0 30.0, 31.1 30.1))
```

```sql
-- Convert geometry to WKT (for reading)
SELECT ST_AsText(position) FROM locations;

-- Parse WKT to geometry (for input)
SELECT ST_GeomFromText('POINT(31.2357 30.0444)', 4326);
```

### WKB — Well-Known Binary

**Binary encoding** of geometry. Compact, efficient for storage and transfer. Not human-readable.

```
Example WKB (hex): 0101000020E6100000F8A0A7D17D523F40713D0AD7A3F03E40
                   └─ type ──┘└── SRID ──────┘└── X coord ────┘└── Y coord ───┘
```

```sql
-- Convert geometry to binary (for transfer/storage efficiency)
SELECT ST_AsBinary(position) FROM locations;

-- Parse binary to geometry
SELECT ST_GeomFromWKB(wkb_column, 4326);
```

### GeoJSON

**JSON format** for spatial data. The standard for web mapping APIs (Google Maps, Leaflet, Mapbox). Human-readable and widely supported.

```json
Point:
{ "type": "Point", "coordinates": [31.2357, 30.0444] }
                                    └─lng─┘  └─lat─┘

LineString:
{ "type": "LineString", "coordinates": [[31.0,30.0],[31.1,30.1],[31.2,30.2]] }

Polygon:
{ "type": "Polygon", "coordinates": [[[31.0,30.0],[31.1,30.0],[31.1,30.1],[31.0,30.0]]] }

Feature (geometry + properties):
{
  "type": "Feature",
  "geometry": { "type": "Point", "coordinates": [31.2357, 30.0444] },
  "properties": { "name": "Cairo", "population": 20000000 }
}

FeatureCollection (multiple features):
{
  "type": "FeatureCollection",
  "features": [
    { "type": "Feature", "geometry": {...}, "properties": {...} },
    { "type": "Feature", "geometry": {...}, "properties": {...} }
  ]
}
```

> ⚠️ **GeoJSON coordinate order**: GeoJSON always uses `[longitude, latitude]` (X, Y) order — not `[latitude, longitude]`. This matches WKT and SQL spatial functions.

```sql
-- SQL → GeoJSON (for sending to web APIs / maps)
SELECT ST_AsGeoJSON(position) FROM locations;
-- → '{"type":"Point","coordinates":[31.2357,30.0444]}'

-- GeoJSON → SQL geometry
SELECT ST_GeomFromGeoJSON('{"type":"Point","coordinates":[31.2357,30.0444]}');
```

### Format Comparison

| Format | Human-readable | Compact | Web-friendly | SQL input | SQL output |
|--------|---------------|---------|-------------|-----------|------------|
| WKT | ✅ | ❌ verbose | ❌ | ✅ | ✅ |
| WKB | ❌ binary | ✅ | ❌ | ✅ | ✅ |
| GeoJSON | ✅ | ❌ verbose | ✅ | ✅ | ✅ |

---

## 9. ⚙️ Common Spatial Operations Explained

### Buffer — Creating a Zone Around a Geometry

A **buffer** expands a geometry outward by a specified distance, creating an area:

```
 Point + buffer:        Line + buffer:       Polygon + buffer:
      ╭───╮            ╭──────────╮          ╭──────────────╮
   ╭──┼───┼──╮         │  ═══════ │          │  ┌────────┐  │
   │  │ • │  │   →     │  ─────── │    →     │  │        │  │
   ╰──┼───┼──╯         │  ═══════ │          │  └────────┘  │
      ╰───╯            ╰──────────╯          ╰──────────────╯
   Circle around        Corridor around       Expanded polygon
   the point            the line
```

```sql
-- Buffer a store (creates a circle for SRID 4326 in degrees — not useful)
SELECT ST_Buffer(position, 0.01) FROM stores;

-- Buffer in meters using projected SRID (PostGIS — best practice)
SELECT ST_Buffer(
  ST_Transform(position, 32636),   -- project to UTM (meters)
  500                               -- 500 meters
) FROM stores;

-- Buffer a road to create a 200m corridor
SELECT ST_Buffer(route, 0.002) FROM roads;
```

**Real uses**: Delivery zones, noise pollution areas, flood risk buffers, proximity analysis

---

### Intersection — Shared Area

What area do two shapes share?

```
  ┌──────┐
  │  A   │
  │    ┌─┼─────┐
  │    │▓│  B  │     ▓ = ST_Intersection(A, B)
  └────┼─┘     │
       └───────┘
```

```sql
SELECT ST_AsText(ST_Intersection(zone_a, zone_b)) FROM zones;
-- Returns the shared geometry (could be empty, a point, line, or polygon)

-- Check if intersection is empty
SELECT ST_IsEmpty(ST_Intersection(zone_a, zone_b)) FROM zones;
```

---

### Union — Combine Shapes

Merge two or more geometries into one, removing internal boundaries:

```
  ┌──────┐
  │  A   │
  │    ┌─┼─────┐        ┌────────────┐
  │    │ │  B  │   →    │    A + B   │
  └────┼─┘     │        └────────────┘
       └───────┘
```

```sql
-- Merge two districts
SELECT ST_AsText(ST_Union(district_a, district_b));

-- Aggregate union: merge all districts in a city
SELECT city_id, ST_Union(boundary) AS city_outline
FROM districts GROUP BY city_id;
```

---

### Difference — Subtract Shape B from A

```
  ┌──────┐
  │  A   │
  │    ┌─┼─────┐        ┌──────┐
  │    │ │  B  │   →    │A    │     (the part of A not covered by B)
  └────┼─┘     │        └─────┘
       └───────┘
```

```sql
-- City boundary minus a restricted military zone
SELECT ST_AsText(ST_Difference(city_boundary, restricted_zone));
```

---

### Centroid — Geometric Center

The **centroid** is the arithmetic mean of all coordinates — the "center of gravity":

```
  ┌──────────────┐
  │              │
  │       •      │   ← centroid (may NOT be inside for concave shapes)
  │              │
  └──────────────┘
```

```sql
SELECT ST_AsText(ST_Centroid(boundary)) FROM regions;

-- ⚠️ For concave polygons, centroid may fall OUTSIDE the shape
-- PostGIS: use ST_PointOnSurface() to guarantee an interior point
SELECT ST_AsText(ST_PointOnSurface(boundary)) FROM regions;
```

---

### Convex Hull — Tightest Convex Wrapper

The smallest convex shape that contains all input geometries — like stretching a rubber band around all points:

```
Raw points:                  Convex Hull:
 •  •                         •──────•
    • •                      ╱ •  •  ╲
  •   •    →→→              ╱    •    ╲
     •                     •  •   •    •
  •                          ╲  •     ╱
                               •──────•
```

```sql
SELECT ST_AsText(ST_ConvexHull(ST_Collect(position))) FROM delivery_points;
```

**Uses**: Estimating service area from a cluster of locations, bounding area for a point cloud

---

### Simplify — Reduce Complexity

Reduce the number of vertices in a geometry while preserving its shape (Douglas-Peucker algorithm):

```
Original (100 vertices):     Simplified (12 vertices):
╭─────────────────────╮      ╭───────────────────╮
│ ╭──────────────── ╮ │  →   │ ╭───────────────╮ │
│ │ ~~~~~~~~~~~~~~~~ │ │      │ │               │ │
│ ╰──────────────── ╯ │      │ ╰───────────────╯ │
╰─────────────────────╯      ╰───────────────────╯
  detailed coastline          simplified for display
```

```sql
-- tolerance: larger = more simplification
SELECT ST_AsText(ST_Simplify(boundary, 0.001)) FROM regions;  -- gentle
SELECT ST_AsText(ST_Simplify(boundary, 0.01))  FROM regions;  -- aggressive
```

**Uses**: Displaying boundaries at low zoom levels, reducing storage size, faster rendering

---

### ST_Validate / Repair Invalid Geometries

Geometries can become invalid (self-intersecting polygons, unclosed rings, etc.):

```
Valid polygon:      Invalid polygon (self-intersecting):
┌──────────┐           ╱╲
│          │          ╱  ╲   ← The ring crosses itself
│          │         ╱    ╲
└──────────┘        ╱──────╲
                    ╲      ╱
                     ╲    ╱ ← figure-8 shape — INVALID
```

```sql
-- Check validity
SELECT ST_IsValid(boundary) FROM regions;    -- returns 1 or 0

-- Find invalid geometries
SELECT id, name FROM regions WHERE NOT ST_IsValid(boundary);

-- Repair (PostGIS)
UPDATE regions SET boundary = ST_MakeValid(boundary) WHERE NOT ST_IsValid(boundary);
```

---

## 10. 🏙️ Real-World Use Cases

### Use Case 1 — Store Locator (Nearest Stores)
```sql
-- User's GPS location
SET @user_lat = 30.0444;
SET @user_lng = 31.2357;
SET @user_pos = ST_PointFromText(CONCAT('POINT(', @user_lng, ' ', @user_lat, ')'), 4326);

-- Find 5 nearest open stores, with distance
SELECT
  name,
  address,
  ROUND(ST_Distance_Sphere(position, @user_pos)) AS distance_m,
  opening_hours
FROM stores
WHERE is_open = 1
ORDER BY ST_Distance_Sphere(position, @user_pos) ASC
LIMIT 5;
```

---

### Use Case 2 — Geofencing (Is the Driver Inside the Zone?)
```sql
-- Check if a delivery driver's GPS ping is inside their assigned zone
SELECT
  d.driver_name,
  z.zone_name,
  CASE
    WHEN ST_Contains(z.boundary, d.current_position) THEN 'IN ZONE ✅'
    ELSE 'OUT OF ZONE ❌'
  END AS status
FROM drivers d
JOIN delivery_zones z ON d.assigned_zone_id = z.id;
```

---

### Use Case 3 — Reverse Geocoding (Which City Is This Point In?)
```sql
-- Find which administrative region a GPS coordinate belongs to
SELECT
  country,
  governorate,
  district
FROM admin_boundaries
WHERE ST_Contains(
  boundary,
  ST_PointFromText('POINT(31.2357 30.0444)', 4326)
)
ORDER BY ST_Area(boundary) ASC   -- get the most specific (smallest) boundary
LIMIT 1;
```

---

### Use Case 4 — Delivery Zone Optimization (Spatial Join)
```sql
-- Count customers per delivery zone, and flag overfull zones
SELECT
  z.zone_name,
  COUNT(c.id)                    AS customer_count,
  ROUND(ST_Area(z.boundary::geography) / 1000000, 2) AS area_km2,
  ROUND(COUNT(c.id) / (ST_Area(z.boundary::geography) / 1000000), 1) AS density_per_km2,
  CASE WHEN COUNT(c.id) > 500 THEN 'OVERFULL' ELSE 'OK' END AS status
FROM delivery_zones z
LEFT JOIN customers c ON ST_Contains(z.boundary, c.location)
GROUP BY z.id, z.zone_name, z.boundary
ORDER BY customer_count DESC;
```

---

### Use Case 5 — Infrastructure Proximity Alert
```sql
-- Find all construction projects within 100m of a water pipeline
SELECT
  p.project_name,
  p.start_date,
  ROUND(ST_Distance_Sphere(p.location, w.path)) AS dist_to_pipe_m
FROM construction_projects p
JOIN water_pipelines w
  ON ST_Distance_Sphere(p.location, w.path) <= 100
ORDER BY dist_to_pipe_m;
```

---

### Use Case 6 — Land Use Overlap Analysis
```sql
-- Find areas where industrial zones overlap with residential zones (conflict detection)
SELECT
  i.zone_id AS industrial_zone,
  r.zone_id AS residential_zone,
  ST_AsGeoJSON(ST_Intersection(i.boundary, r.boundary)) AS overlap_area,
  ROUND(ST_Area(ST_Intersection(i.boundary, r.boundary)::geography) / 10000, 2) AS overlap_hectares
FROM industrial_zones i
JOIN residential_zones r
  ON ST_Intersects(i.boundary, r.boundary)       -- only check intersecting pairs
 AND NOT ST_Touches(i.boundary, r.boundary)      -- exclude adjacent (only touching)
WHERE ST_Area(ST_Intersection(i.boundary, r.boundary)) > 0;
```

---

### Use Case 7 — Route Analysis (Is the Road Inside City Limits?)
```sql
-- What percentage of each road is inside the city?
SELECT
  r.road_name,
  ROUND(
    ST_Length(ST_Intersection(r.route, c.boundary)::geography)
    / ST_Length(r.route::geography) * 100
  , 1) AS pct_inside_city
FROM roads r
JOIN cities c ON c.name = 'Cairo'
WHERE ST_Intersects(r.route, c.boundary);
```

---

### Use Case 8 — Heat Map Data (Density per Grid Cell)
```sql
-- PostGIS: count incidents per 0.1° × 0.1° grid cell (for heat map)
SELECT
  FLOOR(ST_X(location) / 0.1) * 0.1 AS grid_lng,
  FLOOR(ST_Y(location) / 0.1) * 0.1 AS grid_lat,
  COUNT(*) AS incident_count
FROM incidents
WHERE ST_Within(
  location,
  ST_PolygonFromText('POLYGON((29.0 22.0, 37.0 22.0, 37.0 32.0, 29.0 32.0, 29.0 22.0))', 4326)
)
GROUP BY grid_lng, grid_lat
ORDER BY incident_count DESC;
```

---

## 11. ⚠️ Common Mistakes & Gotchas

### Mistake 1 — Swapping Latitude and Longitude
```sql
-- ❌ WRONG — lat/lng swapped (puts Cairo in the ocean near Africa's west coast)
ST_PointFromText('POINT(30.0444 31.2357)', 4326)
                        └─lat─┘  └─lng─┘

-- ✅ CORRECT — X is longitude, Y is latitude
ST_PointFromText('POINT(31.2357 30.0444)', 4326)
                        └─lng─┘  └─lat─┘

-- Rule: POINT(longitude  latitude) = POINT(X  Y) = POINT(east-west  north-south)
```

---

### Mistake 2 — Forgetting SRID or Mixing SRIDs
```sql
-- ❌ WRONG — no SRID, or mismatched SRIDs
SELECT ST_Distance(
  ST_PointFromText('POINT(31.2357 30.0444)'),       -- no SRID
  ST_PointFromText('POINT(29.9553 31.2001)', 4326)  -- has SRID 4326
);
-- Error or wrong result — geometries are in different systems!

-- ✅ CORRECT — same SRID on both
SELECT ST_Distance_Sphere(
  ST_PointFromText('POINT(31.2357 30.0444)', 4326),
  ST_PointFromText('POINT(29.9553 31.2001)', 4326)
);
```

---

### Mistake 3 — Using ST_Distance Instead of ST_Distance_Sphere for Real Distances
```sql
-- ❌ WRONG — returns degrees, not meters
SELECT ST_Distance(position, ST_PointFromText('POINT(31.2357 30.0444)', 4326))
FROM stores;
-- Result: 0.0023 (degrees — meaningless for physical distance)

-- ✅ CORRECT — returns meters
SELECT ST_Distance_Sphere(position, ST_PointFromText('POINT(31.2357 30.0444)', 4326))
FROM stores;
-- Result: 250 (meters)
```

---

### Mistake 4 — Unclosed Polygon Ring
```sql
-- ❌ WRONG — last point doesn't match first
POLYGON((31.00 30.00, 31.10 30.00, 31.10 30.10, 31.00 30.10))
         └─start─┘                               └─≠start─┘

-- ✅ CORRECT — first = last to close the ring
POLYGON((31.00 30.00, 31.10 30.00, 31.10 30.10, 31.00 30.10, 31.00 30.00))
         └─start─┘                                            └─= start─┘
```

---

### Mistake 5 — No Spatial Index on Large Tables
```sql
-- ❌ SLOW — no spatial index, full table scan on 1M rows
SELECT name FROM stores WHERE ST_Contains(delivery_zone, position);

-- ✅ FAST — ensure spatial index exists
SHOW INDEX FROM stores;  -- check for SPATIAL type
-- If missing:
ALTER TABLE stores ADD SPATIAL INDEX idx_position (position);
```

---

### Mistake 6 — MySQL SPATIAL INDEX Requires NOT NULL
```sql
-- ❌ Will fail — column allows NULL
ALTER TABLE locations ADD SPATIAL INDEX idx_pos (position);
-- ERROR: All parts of a SPATIAL index must be NOT NULL

-- ✅ Fix: declare column NOT NULL first
ALTER TABLE locations MODIFY COLUMN position POINT NOT NULL SRID 4326;
ALTER TABLE locations ADD SPATIAL INDEX idx_pos (position);
```

---

### Mistake 7 — SQLite Ignores Foreign Keys AND Spatial Checks Without PRAGMA
```sql
-- ❌ In SQLite, spatial functions are NOT built-in
-- You must load the SpatiaLite extension first:
SELECT load_extension('mod_spatialite');

-- Without this, ST_Contains, ST_Distance etc. don't exist in SQLite
```

---

### Mistake 8 — Area in Square Degrees (Using SRID 4326)
```sql
-- ❌ WRONG — area in square degrees, not km²
SELECT ST_Area(boundary) AS area FROM regions;   -- SRID 4326 → degrees²

-- ✅ CORRECT — reproject to a metric SRID first (MySQL)
SELECT ST_Area(ST_Transform(boundary, 32636)) / 1000000 AS area_km2 FROM regions;

-- ✅ CORRECT — PostGIS with geography type
SELECT ST_Area(boundary::geography) / 1000000 AS area_km2 FROM regions;
```

---

### Mistake 9 — ST_Contains vs ST_Within Confusion
```sql
-- These are equivalent — choose based on which argument you have handy:
SELECT ST_Contains(polygon, point);   -- "Does polygon contain the point?"
SELECT ST_Within(point, polygon);     -- "Is the point within the polygon?"

-- Both return the same result.
-- Argument order is reversed between Contains and Within!
```

---

### Mistake 10 — Centroid Outside the Polygon
```sql
-- For a crescent or concave polygon, centroid can fall outside:
--  ╭────────────────────╮
--  │  ╭──────╮          │
--  │  │ HOLE │   •      │  ← centroid is in the hole area — OUTSIDE polygon!
--  │  ╰──────╯          │
--  ╰────────────────────╯

-- ✅ PostGIS: use ST_PointOnSurface() for a guaranteed interior point
SELECT ST_AsText(ST_PointOnSurface(boundary)) FROM regions;
```

---

## 12. 🛠️ Choosing the Right Tool / Engine

| Need | Best Choice |
|------|-------------|
| General-purpose, web apps, basic spatial | **MySQL 8.0+** — good enough for most use cases |
| Advanced analysis, accurate measurements, GIS work | **PostGIS (PostgreSQL)** — the gold standard |
| Embedded / mobile / lightweight | **SpatiaLite (SQLite)** |
| Microsoft ecosystem, .NET apps | **SQL Server** with `geometry` / `geography` types |
| Enterprise Oracle stack | **Oracle Spatial / SDO_GEOMETRY** |
| Dedicated GIS software | **QGIS** (open-source) or **ArcGIS** (commercial) |
| Web mapping / visualization | **Mapbox**, **Leaflet.js**, **Google Maps API** |
| Big data spatial | **PostGIS + TimescaleDB**, **BigQuery GIS**, **Snowflake** |

### When to Use SQL Spatial vs Dedicated GIS

| Task | SQL Spatial | Dedicated GIS (QGIS/ArcGIS) |
|------|-------------|------------------------------|
| Query and filter locations | ✅ Ideal | ✅ But slower to set up |
| Calculate distances/areas | ✅ | ✅ |
| Spatial joins | ✅ Ideal | ✅ |
| Network routing (shortest path) | ⚠️ Limited (pgRouting for PostGIS) | ✅ Built-in |
| Raster/satellite image analysis | ❌ | ✅ Core feature |
| Map rendering / visualization | ❌ | ✅ Core feature |
| Topology validation | ⚠️ Basic | ✅ Advanced |
| Geostatistics (Kriging, IDW) | ❌ | ✅ |

---

## 13. 📖 Glossary

| Term | Definition |
|------|-----------|
| **Azimuth** | Direction from one point to another, measured clockwise from north in degrees |
| **Bounding Box (MBR)** | The smallest rectangle that fully encloses a geometry, aligned with the X/Y axes |
| **Buffer** | A zone created by expanding a geometry outward by a specified distance |
| **Cartesian** | Flat, Euclidean coordinate system — X and Y axes at right angles, infinite flat plane |
| **Centroid** | The geometric center point (mean of all coordinates) of a geometry |
| **Convex Hull** | The smallest convex polygon that encloses a set of geometries |
| **CRS** | Coordinate Reference System — the full specification of how coordinates map to real-world locations |
| **DE-9IM** | Dimensionally Extended 9-Intersection Model — the standard framework for spatial predicates |
| **Datum** | The reference ellipsoid used to model the Earth's shape (e.g., WGS 84) |
| **Envelope** | Synonym for Bounding Box / MBR |
| **EPSG** | European Petroleum Survey Group — maintains the registry of SRID codes |
| **Geodesic** | The shortest path between two points on the Earth's curved surface |
| **Geofence** | A virtual boundary defined as a polygon used to trigger events when something enters/exits |
| **GeoJSON** | A JSON-based format for encoding geographic data structures |
| **Geography** | Spherical/ellipsoidal spatial type — accounts for Earth's curvature |
| **Geometry** | Flat/Cartesian spatial type — treats coordinates as on a flat plane |
| **GIS** | Geographic Information System — software for capturing, storing, and analyzing spatial data |
| **GiST** | Generalized Search Tree — the index type used by PostGIS |
| **GPS** | Global Positioning System — uses WGS 84 (SRID 4326) |
| **Great Circle** | The shortest path between two points on a sphere |
| **Haversine** | Formula to calculate the great-circle distance between two lat/lng points |
| **KNN** | K-Nearest Neighbors — finding the K closest geometries to a query point |
| **Latitude** | Angular distance north/south of the Equator — the Y axis on a map |
| **Longitude** | Angular distance east/west of the Prime Meridian — the X axis on a map |
| **MBR** | Minimum Bounding Rectangle — see Bounding Box |
| **Meridian** | A line of constant longitude running from pole to pole |
| **PostGIS** | The spatial extension for PostgreSQL — the most feature-rich SQL spatial system |
| **Predicate** | A spatial function that returns TRUE/FALSE about a relationship |
| **Projection** | A mathematical method for representing the curved Earth on a flat surface |
| **R-Tree** | A tree data structure used for spatial indexing (used in MySQL, Oracle, SpatiaLite) |
| **Raster** | Spatial data stored as a grid of pixels (satellite imagery, elevation models) |
| **Ring** | A closed LineString where the first and last coordinate are identical |
| **SRID** | Spatial Reference Identifier — a number identifying a specific coordinate system |
| **Topology** | The study of spatial relationships that are preserved under continuous deformation |
| **UTM** | Universal Transverse Mercator — a family of metric projected coordinate systems |
| **Vector** | Spatial data stored as geometric shapes (points, lines, polygons) |
| **Vincenty** | A more accurate (but slower) formula for geodesic distance calculations |
| **WGS 84** | World Geodetic System 1984 — the standard datum used by GPS (SRID 4326) |
| **WKB** | Well-Known Binary — compact binary representation of geometry |
| **WKT** | Well-Known Text — human-readable text representation of geometry |
| **Z coordinate** | Elevation or altitude — a third dimension added to 2D geometries (POINT Z) |

---

## Quick Decision Guide

```
I have GPS coordinates (lat, lng) from a phone/device
  → Use SRID 4326. Store as POINT(longitude latitude).

I want to measure real distance in meters between two GPS points
  → Use ST_Distance_Sphere() (MySQL) or cast to geography (PostGIS).

I want to check if a GPS point is inside a region
  → Use ST_Contains(region_polygon, point).

I want to find all rows within N kilometers
  → Use ST_Distance_Sphere() <= N * 1000, with a bounding box pre-filter.

I want accurate area of a polygon in km²
  → PostGIS: ST_Area(geom::geography) / 1e6
  → MySQL: ST_Area(ST_Transform(geom, local_utm)) / 1e6

I want to merge multiple polygons into one
  → Use ST_Union() — individual or as GROUP BY aggregate.

My geometry is invalid / broken
  → Use ST_IsValid() to detect, ST_MakeValid() (PostGIS) to repair.

My spatial queries are slow
  → Create a SPATIAL INDEX on the geometry column.
  → Make sure the indexed column is NOT NULL (MySQL requirement).
  → Use MBR/bounding box pre-filter before exact spatial functions.
```

---

*Written for MySQL 8.x with PostGIS / PostgreSQL alternatives noted throughout. Concepts apply universally to all spatial-capable SQL engines.*
