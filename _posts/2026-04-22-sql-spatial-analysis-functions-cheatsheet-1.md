---

title: SQL Spatial Analysis Functions Cheatsheet

description: >-
  A comprehensive cheatsheet covering all SQL spatial analysis functions, including Spatial Data Types, Geometry Constructors, Input / Output (WKT & WKB), Geometry Properties, Measurement Functions, Spatial Relationship Functions, Spatial Set Operations, Coordinate & Projection, GeoJSON & Geohash, Spatial Indexes, Window & Aggregate Spatial Functions, Cross-Engine Master Table, and Common Patterns & Examples. Includes inline and table-level syntax, add/drop/modify examples, cross-engine compatibility.
date: 2026-04-22 10:00:00 +0800
author: Mahmoud Lotfi
file_name: 2026-04-22-sql-spatial-analysis-functions-cheatsheet-1.md
categories: [SQL, Spatial Analysis, cheatsheet]
tags: [SQL, Spatial Analysis, cheatsheet]
pin: False
math: true
mermaid: true
comments: true
toc: true
render_with_liquid: false

image:
  path: /assets/img/posts/sql.jpg
  alt: SQL Spatial Analysis Functions Cheatsheet
  lqip: data:image/webp;base64,UklGRjoAAABXRUJQVlA4IC4AAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
---

# 🗺️ SQL Spatial Analysis Functions Cheatsheet

> Geometry types · Construction · Measurement · Relationships · Cross-engine compatibility

---

## Legend

| Symbol | Meaning |
|--------|---------|
| ✅ | Supported (same or very similar syntax) |
| ⚠️ | Supported with different syntax or behavior |
| ❌ | Not supported / no direct equivalent |


---

# In Article 

Here's your SQL Spatial Analysis Functions Cheatsheet! It covers **13 sections**:

| # | Section | What's Inside |
|---|---------|---------------|
| 1 | **Spatial Data Types** | POINT, LINESTRING, POLYGON, GEOMETRY, GEOGRAPHY, SRID table |
| 2 | **Geometry Constructors** | Build POINT, LINESTRING, POLYGON, MULTI*, GEOMETRYCOLLECTION |
| 3 | **Input / Output (WKT & WKB)** | ST_AsText, ST_AsBinary, ST_GeomFromText, ST_Envelope |
| 4 | **Geometry Properties** | Type, validity, coordinates, rings, collections |
| 5 | **Measurement Functions** | Distance (flat & spherical), Area, Length, Hausdorff |
| 6 | **Spatial Relationship Functions** | ST_Contains, ST_Within, ST_Intersects, ST_Touches + all MBR predicates |
| 7 | **Spatial Set Operations** | Intersection, Union, Difference, Buffer, ConvexHull, Simplify, Centroid |
| 8 | **Coordinate & Projection** | ST_Transform, ST_SwapXY, ST_LineInterpolatePoint, Geohash |
| 9 | **GeoJSON & Geohash** | Import/export GeoJSON, build FeatureCollection |
| 10 | **Spatial Indexes** | R-Tree (MySQL), GiST/BRIN (PostGIS), Grid (SQL Server), Oracle setup |
| 11 | **Aggregate Spatial Functions** | ST_Collect, ST_Union, ST_Extent, KNN nearest-neighbor |
| 12 | **Cross-Engine Master Table** | All features × all engines at a glance |
| 13 | **Common Patterns** | GPS storage, radius search, geofencing, route length, spatial join, buffer zones |

A few important gotchas are highlighted: **GEOMETRY vs GEOGRAPHY** accuracy tradeoff, **SQLite/SpatiaLite requiring a PRAGMA**, and the **MBR pre-filter + precise function** performance pattern for large datasets.

---

## Categories
1. [Spatial Data Types](#1--spatial-data-types)
2. [Geometry Constructors](#2--geometry-constructors)
3. [Input / Output (WKT & WKB)](#3--input--output-wkt--wkb)
4. [Geometry Properties](#4--geometry-properties)
5. [Measurement Functions](#5--measurement-functions)
6. [Spatial Relationship Functions](#6--spatial-relationship-functions)
7. [Spatial Set Operations](#7--spatial-set-operations)
8. [Coordinate & Projection Functions](#8--coordinate--projection-functions)
9. [GeoJSON & Geohash](#9--geojson--geohash)
10. [Spatial Indexes](#10--spatial-indexes)
11. [Window & Aggregate Spatial Functions](#11--window--aggregate-spatial-functions)
12. [Cross-Engine Master Table](#12--cross-engine-master-table)
13. [Common Patterns & Examples](#13--common-patterns--examples)

---

## 1. 📐 Spatial Data Types

> Column types that store geometric/geographic objects.

### MySQL Spatial Types

| Type | Description | Example |
|------|-------------|---------|
| `POINT` | Single X,Y coordinate | A shop location |
| `LINESTRING` | Ordered sequence of points | A road, river |
| `POLYGON` | Closed ring(s) — area with holes | A city boundary |
| `MULTIPOINT` | Collection of Points | Multiple ATMs |
| `MULTILINESTRING` | Collection of LineStrings | Multiple roads |
| `MULTIPOLYGON` | Collection of Polygons | Country with islands |
| `GEOMETRYCOLLECTION` | Mix of any geometry types | Mixed dataset |
| `GEOMETRY` | Generic — accepts any type | Flexible column |

### Declaring Spatial Columns
```sql
CREATE TABLE locations (
  id          INT            NOT NULL AUTO_INCREMENT PRIMARY KEY,
  name        VARCHAR(100)   NOT NULL,
  position    POINT          NOT NULL SRID 4326,   -- WGS84 lat/lng
  region      POLYGON,
  route       LINESTRING,
  geom        GEOMETRY                             -- accepts any type
);
```

### SRID — Spatial Reference System Identifier

| SRID | System | Unit | Use |
|------|--------|------|-----|
| `4326` | WGS 84 (GPS) | Degrees lat/lng | Global GPS coordinates |
| `3857` | Web Mercator | Meters | Google Maps, OpenStreetMap tiles |
| `32636` | UTM Zone 36N | Meters | Egypt / Middle East |
| `2263` | NY State Plane | Feet | Local US surveys |

```sql
-- Create column with enforced SRID
position POINT NOT NULL SRID 4326

-- Check SRID of a geometry
SELECT ST_SRID(position) FROM locations;

-- Change SRID
SELECT ST_SRID(position, 4326) FROM locations;   -- MySQL 8.0+
```

### Cross-Engine — Spatial Types

| Type | MySQL | SQLite + SpatiaLite | PostgreSQL + PostGIS | SQL Server | Oracle Spatial |
|------|-------|---------------------|----------------------|------------|----------------|
| `POINT` | ✅ | ✅ | ✅ | ✅ `geometry` | ✅ `SDO_GEOMETRY` |
| `LINESTRING` | ✅ | ✅ | ✅ | ✅ | ✅ |
| `POLYGON` | ✅ | ✅ | ✅ | ✅ | ✅ |
| `GEOMETRY` (generic) | ✅ | ✅ | ✅ | ✅ | ✅ |
| `GEOGRAPHY` (spherical) | ❌ | ❌ | ✅ | ✅ | ✅ |
| SRID enforcement | ✅ 8.0+ | ✅ | ✅ | ✅ | ✅ |

> 💡 **GEOMETRY vs GEOGRAPHY**: `GEOMETRY` uses flat (Euclidean) math — fast but inaccurate over long distances. `GEOGRAPHY` uses spherical (ellipsoidal) math — slower but accurate for real-world GPS distances. Use `GEOGRAPHY` in PostGIS / SQL Server for distances > ~100 km.

---

## 2. 🏗️ Geometry Constructors {: 2--geometry-constructors}

> Build geometry objects from coordinates.

### POINT
```sql
-- ST_Point(longitude, latitude)  ← note X=lng, Y=lat order
SELECT ST_Point(31.2357, 30.0444);                         -- Cairo
SELECT ST_PointFromText('POINT(31.2357 30.0444)', 4326);
SELECT Point(31.2357, 30.0444);                            -- MySQL shorthand (no SRID)

-- Store a point
INSERT INTO locations (name, position)
VALUES ('Cairo Center', ST_PointFromText('POINT(31.2357 30.0444)', 4326));
```

### LINESTRING
```sql
-- Road from point A to point B to point C
SELECT ST_LineStringFromText('LINESTRING(31.2 30.0, 31.3 30.1, 31.4 30.2)', 4326);

SELECT LineString(
  Point(31.2, 30.0),
  Point(31.3, 30.1),
  Point(31.4, 30.2)
);
```

### POLYGON
```sql
-- Closing ring: first point = last point
SELECT ST_PolygonFromText(
  'POLYGON((31.0 29.9, 31.5 29.9, 31.5 30.5, 31.0 30.5, 31.0 29.9))',
  4326
);

-- Polygon with a hole (donut shape)
SELECT ST_PolygonFromText(
  'POLYGON(
    (31.0 29.9, 31.5 29.9, 31.5 30.5, 31.0 30.5, 31.0 29.9),
    (31.1 30.0, 31.2 30.0, 31.2 30.1, 31.1 30.1, 31.1 30.0)
  )',
  4326
);
```

### MULTIPOINT / MULTILINESTRING / MULTIPOLYGON
```sql
SELECT ST_MultiPointFromText('MULTIPOINT(31.2 30.0, 31.5 30.3, 31.8 30.6)', 4326);
SELECT ST_MultiLineStringFromText('MULTILINESTRING((31.0 30.0, 31.1 30.1),(31.2 30.2, 31.3 30.3))', 4326);
SELECT ST_MultiPolygonFromText('MULTIPOLYGON(((31.0 30.0,31.1 30.0,31.1 30.1,31.0 30.0)),((31.2 30.2,31.3 30.2,31.3 30.3,31.2 30.2)))', 4326);
```

### GEOMETRYCOLLECTION
```sql
SELECT ST_GeomCollFromText(
  'GEOMETRYCOLLECTION(POINT(31.2 30.0), LINESTRING(31.0 30.0, 31.5 30.5))',
  4326
);
```

### Cross-Engine — Constructors

| Function | MySQL | SpatiaLite | PostGIS | SQL Server | Oracle |
|----------|-------|------------|---------|------------|--------|
| `ST_PointFromText()` | ✅ | ✅ | ✅ | ⚠️ `geometry::STPointFromText()` | ⚠️ `SDO_GEOMETRY(2001,...)` |
| `ST_LineStringFromText()` | ✅ | ✅ | ✅ | ⚠️ `geometry::STLineFromText()` | ✅ |
| `ST_PolygonFromText()` | ✅ | ✅ | ✅ | ⚠️ `geometry::STPolyFromText()` | ✅ |
| `ST_GeomFromGeoJSON()` | ✅ 8.0+ | ✅ | ✅ | ⚠️ `geometry::Parse()` | ✅ |
| `ST_Point(x,y)` | ✅ | ✅ | ✅ | ⚠️ `geometry::Point(x,y,srid)` | ❌ |

---

## 3. 📤 Input / Output (WKT & WKB)

> Convert geometries to/from standard text and binary formats.

### WKT — Well-Known Text

```sql
-- Geometry → WKT string
SELECT ST_AsText(position)    FROM locations;     -- 'POINT(31.2357 30.0444)'
SELECT ST_AsWKT(position)     FROM locations;     -- synonym

-- WKT string → Geometry
SELECT ST_GeomFromText('POINT(31.2357 30.0444)', 4326);
SELECT ST_PointFromText('POINT(31.2357 30.0444)', 4326);
SELECT ST_LineFromText('LINESTRING(0 0, 1 1, 2 2)', 4326);
SELECT ST_PolyFromText('POLYGON((0 0,1 0,1 1,0 1,0 0))', 4326);
```

### WKB — Well-Known Binary

```sql
-- Geometry → WKB (binary — used for storage/transfer)
SELECT ST_AsBinary(position)  FROM locations;
SELECT ST_AsWKB(position)     FROM locations;     -- synonym

-- WKB → Geometry
SELECT ST_GeomFromWKB(wkb_column, 4326);
```

### Bounding Box (MBR / Envelope)
```sql
-- Minimum Bounding Rectangle
SELECT ST_Envelope(geom)      FROM regions;
SELECT ST_AsText(ST_Envelope(geom)) FROM regions;
-- → POLYGON((minX minY, maxX minY, maxX maxY, minX maxY, minX minY))
```

### Cross-Engine — Input / Output

| Function | MySQL | SpatiaLite | PostGIS | SQL Server | Oracle |
|----------|-------|------------|---------|------------|--------|
| `ST_AsText()` | ✅ | ✅ | ✅ | ⚠️ `.STAsText()` method | ✅ |
| `ST_AsBinary()` | ✅ | ✅ | ✅ | ⚠️ `.STAsBinary()` | ✅ |
| `ST_GeomFromText()` | ✅ | ✅ | ✅ | ⚠️ `geometry::STGeomFromText()` | ✅ |
| `ST_GeomFromWKB()` | ✅ | ✅ | ✅ | ⚠️ `geometry::STGeomFromWKB()` | ✅ |
| `ST_AsGeoJSON()` | ✅ 8.0+ | ✅ | ✅ | ⚠️ manual or `FOR JSON` | ✅ 12c+ |
| `ST_Envelope()` | ✅ | ✅ | ✅ | ⚠️ `.STEnvelope()` | ⚠️ `SDO_GEOM.SDO_MBR()` |

---

## 4. 📏 Geometry Properties

> Inspect and decompose geometry objects.

### Type & Validity
```sql
SELECT ST_GeometryType(geom)  FROM locations;   -- 'ST_Point', 'ST_Polygon' …
SELECT ST_IsValid(geom)       FROM regions;     -- 1 = valid, 0 = invalid
SELECT ST_IsEmpty(geom)       FROM regions;     -- 1 if empty geometry
SELECT ST_IsSimple(geom)      FROM routes;      -- 1 if no self-intersections
SELECT ST_IsClosed(geom)      FROM routes;      -- 1 if LineString start = end
SELECT ST_Dimension(geom)     FROM shapes;      -- 0=point, 1=line, 2=polygon
SELECT ST_SRID(position)      FROM locations;   -- spatial reference system ID
```

### Points & Coordinates
```sql
SELECT ST_X(position)         FROM locations;   -- longitude (X)
SELECT ST_Y(position)         FROM locations;   -- latitude  (Y)
SELECT ST_Latitude(position)  FROM locations;   -- MySQL 8.0+ — latitude
SELECT ST_Longitude(position) FROM locations;   -- MySQL 8.0+ — longitude

-- Extract start/end of a linestring
SELECT ST_StartPoint(route)   FROM routes;
SELECT ST_EndPoint(route)     FROM routes;
SELECT ST_NumPoints(route)    FROM routes;      -- total points in linestring
SELECT ST_PointN(route, 2)    FROM routes;      -- 2nd point (1-indexed)
```

### Polygon Rings
```sql
SELECT ST_ExteriorRing(boundary)     FROM regions;    -- outer ring as LINESTRING
SELECT ST_NumInteriorRings(boundary) FROM regions;    -- count of holes
SELECT ST_InteriorRingN(boundary, 1) FROM regions;    -- 1st hole as LINESTRING
```

### Collections
```sql
SELECT ST_NumGeometries(collection)  FROM multi_shapes;    -- count of sub-geometries
SELECT ST_GeometryN(collection, 1)   FROM multi_shapes;    -- extract 1st geometry
```

### Cross-Engine — Properties

| Function | MySQL | SpatiaLite | PostGIS | SQL Server | Oracle |
|----------|-------|------------|---------|------------|--------|
| `ST_GeometryType()` | ✅ | ✅ | ✅ | ⚠️ `.STGeometryType()` | ⚠️ `.Get_GType()` |
| `ST_X()` / `ST_Y()` | ✅ | ✅ | ✅ | ⚠️ `.STX` / `.STY` properties | ⚠️ `SDO_UTIL.GETVERTICES()` |
| `ST_IsValid()` | ✅ | ✅ | ✅ | ⚠️ `.STIsValid()` | ⚠️ `SDO_GEOM.VALIDATE_GEOMETRY()` |
| `ST_StartPoint()` | ✅ | ✅ | ✅ | ⚠️ `.STStartPoint()` | ✅ |
| `ST_NumPoints()` | ✅ | ✅ | ✅ | ⚠️ `.STNumPoints()` | ✅ |
| `ST_ExteriorRing()` | ✅ | ✅ | ✅ | ⚠️ `.STExteriorRing()` | ✅ |

---

## 5. 📐 Measurement Functions

> Calculate distances, areas, and lengths.

### Distance
```sql
-- Cartesian (flat) distance — fast, less accurate over long distances
SELECT ST_Distance(
  ST_PointFromText('POINT(31.2357 30.0444)', 4326),   -- Cairo
  ST_PointFromText('POINT(29.9553 31.1342)', 4326)    -- Giza
) AS dist_degrees;

-- Spherical distance — accurate real-world distance in meters
SELECT ST_Distance_Sphere(
  ST_PointFromText('POINT(31.2357 30.0444)', 4326),
  ST_PointFromText('POINT(29.9553 31.1342)', 4326)
) AS dist_meters;

-- PostGIS — use GEOGRAPHY type for accurate sphere distance
SELECT ST_Distance(
  'SRID=4326;POINT(31.2357 30.0444)'::geography,
  'SRID=4326;POINT(29.9553 31.1342)'::geography
) AS dist_meters;
```

### Area
```sql
-- ST_Area returns area in the unit of the SRID
-- SRID 4326 → square degrees (not useful); use projected SRID (e.g. 3857) for m²
SELECT ST_Area(boundary)         FROM regions;

-- PostGIS with geography for m²
SELECT ST_Area(boundary::geography) / 1000000 AS area_km2  FROM regions;
```

### Length / Perimeter
```sql
SELECT ST_Length(route)          FROM routes;    -- length of linestring
SELECT ST_Perimeter(boundary)    FROM regions;   -- perimeter of polygon

-- PostGIS — accurate length in meters using geography
SELECT ST_Length(route::geography) AS length_m   FROM routes;
```

### Hausdorff & Fréchet Distance (shape similarity)
```sql
-- How similar are two line shapes? (lower = more similar)
SELECT ST_HausdorffDistance(route_a, route_b)  FROM route_pairs;
SELECT ST_FrechetDistance(route_a, route_b)    FROM route_pairs;   -- MySQL 8.0.37+
```

### Cross-Engine — Measurement

| Function | MySQL | SpatiaLite | PostGIS | SQL Server | Oracle |
|----------|-------|------------|---------|------------|--------|
| `ST_Distance()` (flat) | ✅ | ✅ | ✅ | ⚠️ `.STDistance()` | ⚠️ `SDO_GEOM.SDO_DISTANCE()` |
| `ST_Distance_Sphere()` | ✅ | ✅ `SphereDistance()` | ⚠️ Use `geography` type | ⚠️ Use `geography` type | ⚠️ `SDO_GEOM.SDO_DISTANCE()` with tolerance |
| `ST_Area()` | ✅ | ✅ | ✅ | ⚠️ `.STArea()` | ⚠️ `SDO_GEOM.SDO_AREA()` |
| `ST_Length()` | ✅ | ✅ | ✅ | ⚠️ `.STLength()` | ⚠️ `SDO_GEOM.SDO_LENGTH()` |
| `ST_Perimeter()` | ✅ | ✅ | ✅ | ❌ use `.STLength()` on ring | ✅ |
| `ST_HausdorffDistance()` | ✅ | ✅ | ✅ | ❌ | ❌ |

---

## 6. 🤝 Spatial Relationship Functions

> Test topological and geometric relationships between two geometries.

### DE-9IM Predicates (Standard)

```sql
-- Contains: does A completely contain B?
SELECT ST_Contains(region, point)    FROM areas, locations;     -- 1 or 0

-- Within: is A completely inside B?
SELECT ST_Within(point, region)      FROM locations, areas;     -- inverse of Contains

-- Intersects: do A and B share any space?
SELECT ST_Intersects(geom_a, geom_b) FROM shapes;

-- Overlaps: do A and B partially overlap (same dimension)?
SELECT ST_Overlaps(poly_a, poly_b)   FROM polygons;

-- Touches: do A and B share only a boundary point?
SELECT ST_Touches(geom_a, geom_b)    FROM shapes;

-- Crosses: do A and B cross each other (different dimensions)?
SELECT ST_Crosses(linestring, poly)  FROM routes, areas;

-- Disjoint: do A and B share NO space at all?
SELECT ST_Disjoint(geom_a, geom_b)   FROM shapes;

-- Equals: are A and B geometrically identical?
SELECT ST_Equals(geom_a, geom_b)     FROM shapes;
```

### MBR (Minimum Bounding Rectangle) Predicates — Faster but less precise
```sql
-- Use MBR checks for large dataset filtering (index-friendly)
SELECT ST_MBRContains(mbr_a, mbr_b)  FROM shapes;
SELECT ST_MBRWithin(mbr_a, mbr_b)    FROM shapes;
SELECT ST_MBRIntersects(mbr_a, mbr_b)FROM shapes;
SELECT ST_MBROverlaps(mbr_a, mbr_b)  FROM shapes;
SELECT ST_MBREquals(mbr_a, mbr_b)    FROM shapes;
SELECT ST_MBRDisjoint(mbr_a, mbr_b)  FROM shapes;
SELECT ST_MBRTouches(mbr_a, mbr_b)   FROM shapes;
SELECT ST_MBRCoveredBy(mbr_a, mbr_b) FROM shapes;
SELECT ST_MBRCovers(mbr_a, mbr_b)    FROM shapes;
```

### Practical: Find all points inside a polygon
```sql
-- Find all stores inside a city boundary
SELECT s.name, ST_AsText(s.position)
FROM stores s
JOIN cities c ON c.name = 'Cairo'
WHERE ST_Contains(c.boundary, s.position);
```

### Practical: Find points within a radius
```sql
-- All restaurants within 2 km of a given point (flat distance)
SELECT name
FROM restaurants
WHERE ST_Distance_Sphere(
  position,
  ST_PointFromText('POINT(31.2357 30.0444)', 4326)
) <= 2000;

-- Better: use bounding box first (uses spatial index), then refine
SELECT name
FROM restaurants
WHERE MBRContains(
  ST_Buffer(ST_PointFromText('POINT(31.2357 30.0444)', 4326), 0.02),
  position
)
AND ST_Distance_Sphere(position, ST_PointFromText('POINT(31.2357 30.0444)', 4326)) <= 2000;
```

### Cross-Engine — Relationships

| Function | MySQL | SpatiaLite | PostGIS | SQL Server | Oracle |
|----------|-------|------------|---------|------------|--------|
| `ST_Contains()` | ✅ | ✅ | ✅ | ⚠️ `.STContains()` | ⚠️ `SDO_CONTAINS()` |
| `ST_Within()` | ✅ | ✅ | ✅ | ⚠️ `.STWithin()` | ⚠️ `SDO_WITHIN_DISTANCE()` |
| `ST_Intersects()` | ✅ | ✅ | ✅ | ⚠️ `.STIntersects()` | ⚠️ `SDO_ANYINTERACT()` |
| `ST_Overlaps()` | ✅ | ✅ | ✅ | ⚠️ `.STOverlaps()` | ⚠️ `SDO_OVERLAPS()` |
| `ST_Touches()` | ✅ | ✅ | ✅ | ⚠️ `.STTouches()` | ⚠️ `SDO_TOUCH()` |
| `ST_Crosses()` | ✅ | ✅ | ✅ | ⚠️ `.STCrosses()` | ⚠️ `SDO_CROSSES()` |
| `ST_Disjoint()` | ✅ | ✅ | ✅ | ⚠️ `.STDisjoint()` | ⚠️ `SDO_DISJOINT()` |
| `ST_Equals()` | ✅ | ✅ | ✅ | ⚠️ `.STEquals()` | ⚠️ `SDO_EQUAL()` |
| MBR predicates | ✅ | ✅ | ⚠️ `&&` operator | ❌ | ❌ |

---

## 7. ✂️ Spatial Set Operations {: 7--spatial-set-operations}

> Compute new geometries from the intersection, union, or difference of two geometries.

### Intersection — shared area
```sql
SELECT ST_AsText(ST_Intersection(poly_a, poly_b)) FROM region_pairs;
-- Returns the geometry that both inputs share
```

### Union — combined area
```sql
SELECT ST_AsText(ST_Union(poly_a, poly_b)) FROM region_pairs;
-- Returns one geometry covering both inputs (no duplicates)
```

### Difference — subtract B from A
```sql
SELECT ST_AsText(ST_Difference(city_boundary, restricted_zone)) FROM areas;
-- Returns the part of A that is NOT in B
```

### Symmetric Difference — XOR of geometries
```sql
SELECT ST_AsText(ST_SymDifference(poly_a, poly_b)) FROM region_pairs;
-- Returns area in A or B but NOT in both (like XOR)
```

### Buffer — expand geometry by distance
```sql
-- Buffer a point (creates a circle in flat/Cartesian space)
SELECT ST_AsText(ST_Buffer(ST_PointFromText('POINT(31.2357 30.0444)', 4326), 0.01));

-- Buffer a road corridor
SELECT ST_AsText(ST_Buffer(route, 0.001)) FROM routes;

-- PostGIS — buffer with projected SRID (meters)
SELECT ST_AsText(
  ST_Buffer(
    ST_Transform(ST_PointFromText('POINT(31.2357 30.0444)', 4326), 32636),
    500   -- 500 meters in UTM Zone 36N
  )
);
```

### Convex Hull — smallest convex shape enclosing geometry
```sql
SELECT ST_AsText(ST_ConvexHull(geom)) FROM point_clouds;
-- Returns the tightest convex polygon around all input points
```

### Simplify — reduce vertex count (generalize shape)
```sql
-- Reduce complexity of a detailed polygon (Douglas-Peucker algorithm)
SELECT ST_AsText(ST_Simplify(boundary, 0.001)) FROM regions;
-- Tolerance: larger = more simplification, less detail
```

### Centroid — geometric center point
```sql
SELECT ST_AsText(ST_Centroid(boundary)) FROM regions;
-- Note: centroid may fall OUTSIDE a concave polygon
-- Use ST_PointOnSurface() for a guaranteed-inside point (PostGIS)
```

### Cross-Engine — Set Operations

| Function | MySQL | SpatiaLite | PostGIS | SQL Server | Oracle |
|----------|-------|------------|---------|------------|--------|
| `ST_Intersection()` | ✅ | ✅ | ✅ | ⚠️ `.STIntersection()` | ⚠️ `SDO_GEOM.SDO_INTERSECTION()` |
| `ST_Union()` | ✅ | ✅ | ✅ | ⚠️ `.STUnion()` | ⚠️ `SDO_GEOM.SDO_UNION()` |
| `ST_Difference()` | ✅ | ✅ | ✅ | ⚠️ `.STDifference()` | ⚠️ `SDO_GEOM.SDO_DIFFERENCE()` |
| `ST_SymDifference()` | ✅ | ✅ | ✅ | ⚠️ `.STSymDifference()` | ⚠️ `SDO_GEOM.SDO_XOR()` |
| `ST_Buffer()` | ✅ | ✅ | ✅ | ⚠️ `.STBuffer()` | ⚠️ `SDO_GEOM.SDO_BUFFER()` |
| `ST_ConvexHull()` | ✅ | ✅ | ✅ | ⚠️ `.STConvexHull()` | ⚠️ `SDO_GEOM.SDO_CONVEXHULL()` |
| `ST_Simplify()` | ✅ | ✅ | ✅ | ❌ | ⚠️ `SDO_UTIL.SIMPLIFY()` |
| `ST_Centroid()` | ✅ | ✅ | ✅ | ❌ use `.STCentroid()` MSSQL extension | ✅ |

---

## 8. 🌐 Coordinate & Projection Functions

> Transform coordinates between spatial reference systems.

### Transform (Reproject)
```sql
-- PostGIS — transform from WGS84 (4326) to UTM (32636)
SELECT ST_AsText(
  ST_Transform(
    ST_PointFromText('POINT(31.2357 30.0444)', 4326),
    32636
  )
);

-- MySQL 8.0+
SELECT ST_Transform(position, 32636) FROM locations;
```

### Swap X/Y coordinates
```sql
-- Fix geometries where lat/lng are accidentally reversed
SELECT ST_SwapXY(position) FROM locations;
```

### Line Interpolation (point along a line)
```sql
-- Point 50% along a route
SELECT ST_AsText(ST_LineInterpolatePoint(route, 0.5)) FROM routes;

-- Multiple points at regular intervals along a route
SELECT ST_AsText(ST_LineInterpolatePoints(route, 0.25)) FROM routes;  -- every 25%

-- Point at specific distance from start
SELECT ST_AsText(ST_PointAtDistance(route, 1000)) FROM routes;  -- 1000 map units from start
```

### Geohash (encode coordinates as string)
```sql
-- Encode point as geohash (shorter = lower precision)
SELECT ST_GeoHash(position, 10) FROM locations;       -- 10-char precision
SELECT ST_GeoHash(ST_PointFromText('POINT(31.2357 30.0444)',4326), 8);
-- → 'svhwsq3w'

-- Decode geohash back to point
SELECT ST_AsText(ST_PointFromGeoHash('svhwsq3w', 0));

-- Extract lat/lng from geohash
SELECT ST_LatFromGeoHash('svhwsq3w');
SELECT ST_LongFromGeoHash('svhwsq3w');
```

### Cross-Engine — Projections

| Function | MySQL | SpatiaLite | PostGIS | SQL Server | Oracle |
|----------|-------|------------|---------|------------|--------|
| `ST_Transform()` | ✅ 8.0+ | ✅ | ✅ | ⚠️ manual via CLR | ⚠️ `SDO_CS.TRANSFORM()` |
| `ST_SwapXY()` | ✅ | ✅ | ✅ | ❌ | ❌ |
| `ST_LineInterpolatePoint()` | ✅ | ✅ | ✅ | ❌ | ❌ |
| `ST_GeoHash()` | ✅ | ✅ | ✅ | ❌ | ❌ |
| `ST_PointFromGeoHash()` | ✅ | ✅ | ⚠️ `ST_GeomFromGeoHash()` | ❌ | ❌ |

---

## 9. 🌍 GeoJSON & Geohash

> Exchange spatial data in standard web-friendly formats.

### GeoJSON Input / Output
```sql
-- Geometry → GeoJSON string
SELECT ST_AsGeoJSON(position) FROM locations;
-- → '{"type":"Point","coordinates":[31.2357,30.0444]}'

SELECT ST_AsGeoJSON(boundary) FROM regions;
-- → '{"type":"Polygon","coordinates":[[[31.0,29.9],...]]}'

-- GeoJSON string → Geometry
SELECT ST_GeomFromGeoJSON(
  '{"type":"Point","coordinates":[31.2357,30.0444]}'
);

-- Insert from GeoJSON
INSERT INTO locations (name, position)
VALUES (
  'Cairo',
  ST_GeomFromGeoJSON('{"type":"Point","coordinates":[31.2357,30.0444]}')
);

-- Full feature with metadata (MySQL 8.0+)
SELECT ST_AsGeoJSON(
  ST_GeomFromText('POINT(31.2357 30.0444)', 4326),
  4,      -- max decimal digits
  2       -- options flag: include SRID
);
```

### PostGIS — Build GeoJSON FeatureCollection
```sql
SELECT json_build_object(
  'type', 'FeatureCollection',
  'features', json_agg(
    json_build_object(
      'type',       'Feature',
      'geometry',   ST_AsGeoJSON(position)::json,
      'properties', json_build_object('name', name, 'category', category)
    )
  )
)
FROM locations;
```

### Cross-Engine — GeoJSON

| Function | MySQL | SpatiaLite | PostGIS | SQL Server | Oracle |
|----------|-------|------------|---------|------------|--------|
| `ST_AsGeoJSON()` | ✅ 8.0+ | ✅ | ✅ | ⚠️ manual JSON build | ✅ 12c+ |
| `ST_GeomFromGeoJSON()` | ✅ 8.0+ | ✅ | ✅ `ST_GeomFromGeoJSON()` | ⚠️ `geometry::Parse()` | ✅ 12c+ |

---

## 10. 📇 Spatial Indexes

> Critical for performance — without a spatial index, every spatial query does a full table scan.

### MySQL — SPATIAL INDEX
```sql
-- Require NOT NULL + no SRID on older MySQL, or SRID on 8.0+
CREATE TABLE locations (
  id        INT   NOT NULL AUTO_INCREMENT PRIMARY KEY,
  name      VARCHAR(100) NOT NULL,
  position  POINT NOT NULL SRID 4326,
  SPATIAL INDEX idx_position (position)   -- inline at creation
);

-- Add spatial index later
ALTER TABLE locations ADD SPATIAL INDEX idx_position (position);
CREATE SPATIAL INDEX idx_position ON locations(position);

-- Drop spatial index
DROP INDEX idx_position ON locations;
ALTER TABLE locations DROP INDEX idx_position;
```

### PostgreSQL (PostGIS) — GiST / SP-GiST / BRIN
```sql
-- GiST index — most common, supports all operators
CREATE INDEX idx_position ON locations USING GIST (position);

-- SP-GiST — better for non-overlapping data (points, quadtrees)
CREATE INDEX idx_position ON locations USING SPGIST (position);

-- BRIN — very small, good for large append-only tables
CREATE INDEX idx_position ON locations USING BRIN (position);

-- Partial spatial index (only index active records)
CREATE INDEX idx_active_pos ON locations USING GIST (position) WHERE active = TRUE;
```

### SQL Server — Spatial Index
```sql
CREATE SPATIAL INDEX idx_position
ON locations(position)
USING GEOMETRY_AUTO_GRID
WITH (BOUNDING_BOX = (29.0, 22.0, 37.0, 32.0));   -- xmin,ymin,xmax,ymax for Egypt
```

### Oracle — Spatial Index (R-Tree)
```sql
CREATE INDEX idx_position ON locations(position)
INDEXTYPE IS MDSYS.SPATIAL_INDEX_V2;

-- Required: insert metadata first
INSERT INTO user_sdo_geom_metadata VALUES (
  'LOCATIONS', 'POSITION',
  MDSYS.SDO_DIM_ARRAY(
    MDSYS.SDO_DIM_ELEMENT('X', 29.0, 37.0, 0.005),
    MDSYS.SDO_DIM_ELEMENT('Y', 22.0, 32.0, 0.005)
  ),
  4326
);
```

### Cross-Engine — Spatial Indexes

| Feature | MySQL | SpatiaLite | PostGIS | SQL Server | Oracle |
|---------|-------|------------|---------|------------|--------|
| Spatial index type | R-Tree | R-Tree | GiST / SP-GiST / BRIN | Grid-based | R-Tree |
| Syntax | `SPATIAL INDEX` | `CREATE SPATIAL INDEX` | `USING GIST` | `CREATE SPATIAL INDEX` | `INDEXTYPE IS MDSYS.SPATIAL_INDEX` |
| Column must be `NOT NULL` | ✅ required | ✅ | ❌ optional | ❌ | ❌ |
| Partial / filtered index | ❌ | ❌ | ✅ | ✅ | ❌ |
| Automatic SRID enforcement | ✅ 8.0+ | ❌ | ✅ | ✅ | ✅ |

> ⚠️ **Performance tip**: Always use a spatial index + a bounding box pre-filter (MBR/envelope check) before applying precise spatial functions like `ST_Contains` or `ST_Distance`. This dramatically reduces the number of rows that need exact computation.

---

## 11. 🪟 Window & Aggregate Spatial Functions

> Aggregate geometries across groups or windows.

### ST_Collect — aggregate into a collection (no merge)
```sql
-- PostGIS: collect all points per city into a MULTIPOINT
SELECT city, ST_Collect(position) AS all_positions
FROM locations
GROUP BY city;
```

### ST_Union — aggregate and merge (dissolve boundaries)
```sql
-- PostGIS: merge all district polygons into a single city polygon
SELECT city_id, ST_Union(district_boundary) AS city_boundary
FROM districts
GROUP BY city_id;
```

### ST_Extent — bounding box of a group
```sql
-- PostGIS: bounding box of all stores in a region
SELECT region, ST_Extent(position) AS bbox
FROM stores
GROUP BY region;
-- → BOX(minX minY, maxX maxY)
```

### ST_ConvexHull on group
```sql
-- Convex hull enclosing all delivery points per route
SELECT route_id, ST_AsText(ST_ConvexHull(ST_Collect(position))) AS hull
FROM deliveries
GROUP BY route_id;
```

### Nearest Neighbor (PostGIS KNN)
```sql
-- 5 nearest locations to a target point using <-> distance operator
SELECT name, ST_Distance(position, target.pt) AS dist
FROM locations,
     (SELECT ST_PointFromText('POINT(31.2357 30.0444)', 4326) AS pt) target
ORDER BY position <-> target.pt
LIMIT 5;
```

### Cross-Engine — Aggregate Spatial

| Function | MySQL | SpatiaLite | PostGIS | SQL Server | Oracle |
|----------|-------|------------|---------|------------|--------|
| `ST_Collect()` aggregate | ✅ | ✅ | ✅ | ❌ | ❌ |
| `ST_Union()` aggregate | ❌ | ✅ | ✅ | ❌ | ⚠️ `SDO_AGGR_UNION()` |
| `ST_Extent()` aggregate | ❌ | ✅ | ✅ | ❌ | ⚠️ `SDO_AGGR_MBR()` |
| KNN `<->` operator | ❌ | ❌ | ✅ | ❌ | ❌ |

---

## 12. 📊 Cross-Engine Master Table

| Category | MySQL | SpatiaLite | PostGIS | SQL Server | Oracle Spatial |
|----------|-------|------------|---------|------------|----------------|
| Spatial types | ✅ | ✅ | ✅ + `GEOGRAPHY` | ✅ + `GEOGRAPHY` | ✅ `SDO_GEOMETRY` |
| WKT / WKB I/O | ✅ | ✅ | ✅ | ✅ | ✅ |
| GeoJSON I/O | ✅ 8.0+ | ✅ | ✅ | ⚠️ | ✅ 12c+ |
| Geohash | ✅ | ✅ | ✅ | ❌ | ❌ |
| Measurement (flat) | ✅ | ✅ | ✅ | ✅ | ✅ |
| Measurement (spherical) | ✅ `ST_Distance_Sphere` | ✅ | ✅ `GEOGRAPHY` type | ✅ `GEOGRAPHY` type | ✅ with tolerance |
| Relationship predicates | ✅ full DE-9IM | ✅ | ✅ | ✅ | ✅ |
| MBR predicates | ✅ | ✅ | ⚠️ `&&` operator | ❌ | ❌ |
| Set operations (buffer, union…) | ✅ | ✅ | ✅ | ✅ | ✅ |
| Coordinate transform | ✅ 8.0+ | ✅ | ✅ | ⚠️ limited | ✅ |
| Spatial indexes | ✅ R-Tree | ✅ R-Tree | ✅ GiST/BRIN | ✅ Grid | ✅ R-Tree |
| Aggregate spatial functions | ⚠️ ST_Collect only | ✅ | ✅ full | ❌ | ⚠️ limited |
| KNN nearest-neighbor index | ❌ | ❌ | ✅ | ✅ | ✅ |
| Deferrable constraint / FK on geom | ❌ | ❌ | ✅ | ❌ | ✅ |

---

## 13. 🛠️ Common Patterns & Examples {: 13--common-patterns--examples}

---

### Pattern 1 — Store and query GPS locations
```sql
-- Table setup
CREATE TABLE stores (
  id       INT   NOT NULL AUTO_INCREMENT PRIMARY KEY,
  name     VARCHAR(100) NOT NULL,
  position POINT NOT NULL SRID 4326,
  SPATIAL INDEX idx_pos (position)
);

-- Insert using lat/lng
INSERT INTO stores (name, position) VALUES
  ('Cairo Downtown', ST_PointFromText('POINT(31.2357 30.0444)', 4326)),
  ('Giza',           ST_PointFromText('POINT(31.2089 30.0131)', 4326)),
  ('Alexandria',     ST_PointFromText('POINT(29.9187 31.2001)', 4326));

-- Retrieve lat/lng
SELECT name,
  ST_Y(position) AS latitude,
  ST_X(position) AS longitude
FROM stores;
```

---

### Pattern 2 — Find all points within N km of a location
```sql
-- All stores within 5 km of a given point
SET @center = ST_PointFromText('POINT(31.2357 30.0444)', 4326);
SET @radius_m = 5000;

SELECT
  name,
  ROUND(ST_Distance_Sphere(position, @center)) AS distance_m
FROM stores
WHERE ST_Distance_Sphere(position, @center) <= @radius_m
ORDER BY distance_m;
```

---

### Pattern 3 — Find points inside a polygon (geofencing)
```sql
-- Define a delivery zone polygon
SET @zone = ST_GeomFromText(
  'POLYGON((31.1 29.9, 31.4 29.9, 31.4 30.2, 31.1 30.2, 31.1 29.9))',
  4326
);

-- Find all orders inside the delivery zone
SELECT o.id, o.customer_name
FROM orders o
WHERE ST_Contains(@zone, o.delivery_point);
```

---

### Pattern 4 — Calculate area of a region (PostGIS)
```sql
-- Area in km² using geography type for accuracy
SELECT
  name,
  ROUND(ST_Area(boundary::geography) / 1000000, 2) AS area_km2
FROM regions
ORDER BY area_km2 DESC;
```

---

### Pattern 5 — Route length in kilometers
```sql
-- MySQL (flat approximation)
SELECT name, ST_Length(route) AS length_degrees FROM routes;

-- PostGIS (accurate using geography)
SELECT name,
  ROUND(ST_Length(route::geography) / 1000, 2) AS length_km
FROM routes;
```

---

### Pattern 6 — Nearest neighbor search (PostGIS KNN)
```sql
-- 10 nearest hospitals to a patient location
SELECT h.name, ST_Distance(h.position::geography, p.location::geography) AS dist_m
FROM hospitals h,
     (SELECT ST_SetSRID(ST_Point(31.2357, 30.0444), 4326)::geography AS location) p
ORDER BY h.position::geography <-> p.location
LIMIT 10;
```

---

### Pattern 7 — Dissolve district boundaries into city boundary
```sql
-- PostGIS aggregate union
SELECT
  city_id,
  ST_AsText(ST_Union(boundary)) AS city_boundary,
  ROUND(ST_Area(ST_Union(boundary)::geography)/1000000, 2) AS total_km2
FROM districts
GROUP BY city_id;
```

---

### Pattern 8 — Generate a buffer zone (PostGIS with reprojection)
```sql
-- 500m buffer around a hospital in UTM (accurate meters)
SELECT
  name,
  ST_AsGeoJSON(
    ST_Transform(
      ST_Buffer(ST_Transform(position, 32636), 500),   -- buffer 500m in UTM
      4326                                              -- back to WGS84
    )
  ) AS buffer_geojson
FROM hospitals;
```

---

### Pattern 9 — Track which admin region a GPS point falls in
```sql
-- Reverse geocode: find which city a point belongs to
SELECT c.name AS city, c.country
FROM cities c
WHERE ST_Contains(
  c.boundary,
  ST_PointFromText('POINT(31.2357 30.0444)', 4326)
)
LIMIT 1;
```

---

### Pattern 10 — Spatial join: count points per polygon
```sql
-- Count stores per district
SELECT
  d.name AS district,
  COUNT(s.id) AS store_count
FROM districts d
LEFT JOIN stores s ON ST_Contains(d.boundary, s.position)
GROUP BY d.id, d.name
ORDER BY store_count DESC;
```

---

## Quick Reference Card

| Task | Function(s) |
|------|-------------|
| Create point from lng/lat | `ST_PointFromText('POINT(lng lat)', 4326)` |
| Get coordinates | `ST_X(pt)` → lng, `ST_Y(pt)` → lat |
| Distance (spherical) | `ST_Distance_Sphere(pt_a, pt_b)` → meters |
| Point inside polygon | `ST_Contains(polygon, point)` |
| Points in radius | `ST_Distance_Sphere(pt, center) <= radius` |
| Overlap check | `ST_Intersects(geom_a, geom_b)` |
| Merge polygons | `ST_Union(poly_a, poly_b)` |
| Expand shape | `ST_Buffer(geom, distance)` |
| Shape center | `ST_Centroid(geom)` |
| Bounding box | `ST_Envelope(geom)` |
| Convert to GeoJSON | `ST_AsGeoJSON(geom)` |
| Convert to WKT | `ST_AsText(geom)` |
| Reproject | `ST_Transform(geom, target_srid)` |
| Validate geometry | `ST_IsValid(geom)` |

---

*Syntax primarily shown for MySQL 8.x. PostGIS (PostgreSQL), SQL Server, Oracle, and SpatiaLite (SQLite) alternatives noted throughout.*
