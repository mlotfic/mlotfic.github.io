---
layout: post
cover_color: #000000

keywords: EPLAN P8, Project Structure, Forms, Reports, Document Types, Electrical Design, Project Documentation, Standard Forms, Report Generation, EPLAN P8 Reference

title: SQL Constraints Cheatsheet

description: >-
  A comprehensive cheatsheet covering all SQL constraint types, including PRIMARY KEY, FOREIGN KEY, UNIQUE, NOT NULL, CHECK, DEFAULT, AUTO_INCREMENT, and more. Includes inline and table-level syntax, add/drop/modify examples, cross-engine compatibility, naming best practices, and common patterns.
date: 2026-04-22 10:00:00 +0800
author: Mahmoud Lotfi
file_name: 2026-04-22-sql-constraints-cheatsheet.md
categories: [SQL, Constraints, cheatsheet]
tags: [SQL, Constraints, cheatsheet]
pin: False
math: true
mermaid: true
comments: true
toc: true
render_with_liquid: false

image:
  path: /assets/img/posts/sql.jpg
  alt: SQL Constraints Cheatsheet
  lqip: data:image/webp;base64,UklGRjoAAABXRUJQVlA4IC4AAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA

---

# 🔒 SQL Constraints Cheatsheet

> All constraint types · Inline & table-level syntax · Add/Drop/Modify · Cross-engine compatibility

---

## Legend
| Symbol | Meaning |
|--------|---------|
| ✅ | Supported (same or very similar syntax) |
| ⚠️ | Supported with different syntax or behavior |
| ❌ | Not supported / no direct equivalent |

---
## IN Article

Here's your SQL Constraints Cheatsheet! It covers **14 sections**:

| # | Section | What's Inside |
|---|---------|---------------|
| 1 | **PRIMARY KEY** | Inline, table-level, composite PKs |
| 2 | **FOREIGN KEY** | Referential actions (CASCADE, SET NULL, RESTRICT…), composite FK, disable/enable |
| 3 | **UNIQUE** | Inline, named, composite, NULL behavior per engine |
| 4 | **NOT NULL** | Column defaults, adding/removing NOT NULL |
| 5 | **CHECK** | Inline, named, multi-column, expression checks |
| 6 | **DEFAULT** | Literals, timestamps, expressions, ON UPDATE |
| 7 | **AUTO_INCREMENT / Identity** | Full syntax comparison across all 6 engines |
| 8 | **Adding Constraints** | ALTER TABLE ADD for every constraint type |
| 9 | **Dropping Constraints** | DROP PK, FK, UNIQUE, CHECK, DEFAULT, NOT NULL |
| 10 | **Inspecting Constraints** | Query system tables in MySQL, PostgreSQL, SQL Server, Oracle, SQLite |
| 11 | **Deferrable Constraints** | DEFERRED, NOCHECK, DISABLE/ENABLE |
| 12 | **Naming Best Practices** | `pk_`, `fk_`, `uq_`, `chk_`, `df_` conventions + full example |
| 13 | **Cross-Engine Master Table** | All constraints × all engines at a glance |
| 14 | **Common Patterns** | Cascade delete, CHECK validation, soft delete, tree/hierarchy, SQLite workaround |

Two particularly useful gotchas are highlighted: **SQLite silently ignores FKs** unless you enable them with a PRAGMA, and **MySQL < 8.0.16 silently ignores CHECK** constraints.

---

## Categories
1. [PRIMARY KEY](#1--primary-key)
2. [FOREIGN KEY](#2--foreign-key)
3. [UNIQUE](#3--unique)
4. [NOT NULL](#4--not-null)
5. [CHECK](#5--check)
6. [DEFAULT](#6--default)
7. [AUTO_INCREMENT / Identity](#7--auto_increment--identity)
8. [Adding Constraints to Existing Tables](#8--adding-constraints-to-existing-tables)
9. [Dropping Constraints](#9--dropping-constraints)
10. [Viewing & Inspecting Constraints](#10--viewing--inspecting-constraints)
11. [Deferrable Constraints](#11--deferrable-constraints)
12. [Constraint Naming Best Practices](#12--constraint-naming-best-practices)
13. [Cross-Engine Master Table](#13--cross-engine-master-table)
14. [Common Patterns & Examples](#14--common-patterns--examples)

---

## 1. 🗝️ PRIMARY KEY {: #1--primary-key}

> Uniquely identifies each row. Cannot be NULL. Only one per table.

### Inline (single column)
```sql
CREATE TABLE employees (
  id    INT         NOT NULL AUTO_INCREMENT PRIMARY KEY,
  name  VARCHAR(100) NOT NULL
);
```

### Table-level (recommended — allows naming)
```sql
CREATE TABLE employees (
  id    INT          NOT NULL AUTO_INCREMENT,
  name  VARCHAR(100) NOT NULL,
  CONSTRAINT pk_employees PRIMARY KEY (id)
);
```

### Composite Primary Key (multiple columns)
```sql
CREATE TABLE order_items (
  order_id    INT  NOT NULL,
  product_id  INT  NOT NULL,
  qty         INT  NOT NULL DEFAULT 1,
  CONSTRAINT pk_order_items PRIMARY KEY (order_id, product_id)
);
```

### Cross-Engine — PRIMARY KEY

| Feature | MySQL | SQLite | PostgreSQL | SQL Server | Oracle | MS Access |
|---------|-------|--------|------------|------------|--------|-----------|
| Single-column PK | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Composite PK | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Named PK constraint | ✅ | ⚠️ ignored internally | ✅ | ✅ | ✅ | ❌ |
| PK auto-creates index | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |

---

## 2. 🔗 FOREIGN KEY

> Enforces referential integrity between two tables.

### Basic Foreign Key
```sql
CREATE TABLE orders (
  id          INT  NOT NULL AUTO_INCREMENT,
  customer_id INT  NOT NULL,
  CONSTRAINT pk_orders     PRIMARY KEY (id),
  CONSTRAINT fk_orders_cust FOREIGN KEY (customer_id)
    REFERENCES customers(id)
);
```

### With Referential Actions
```sql
CREATE TABLE orders (
  id          INT  NOT NULL AUTO_INCREMENT,
  customer_id INT,
  CONSTRAINT pk_orders      PRIMARY KEY (id),
  CONSTRAINT fk_orders_cust FOREIGN KEY (customer_id)
    REFERENCES customers(id)
    ON DELETE SET NULL      -- set to NULL if parent deleted
    ON UPDATE CASCADE       -- follow parent PK if it changes
);
```

### ON DELETE / ON UPDATE Actions

| Action | Behavior |
|--------|----------|
| `CASCADE` | Delete/update child rows automatically when parent changes |
| `SET NULL` | Set FK column to NULL when parent is deleted/updated |
| `SET DEFAULT` | Set FK column to its DEFAULT value |
| `RESTRICT` | Prevent parent delete/update if children exist (checked immediately) |
| `NO ACTION` | Same as RESTRICT but checked at end of transaction (default) |

### Composite Foreign Key
```sql
CREATE TABLE shipment_items (
  shipment_id INT NOT NULL,
  product_id  INT NOT NULL,
  qty         INT NOT NULL,
  CONSTRAINT fk_shipment_item
    FOREIGN KEY (shipment_id, product_id)
    REFERENCES order_items (order_id, product_id)
    ON DELETE CASCADE
);
```

### Disable / Enable FK Checks (MySQL)
```sql
SET FOREIGN_KEY_CHECKS = 0;   -- disable (e.g., during bulk load)
-- ... load data ...
SET FOREIGN_KEY_CHECKS = 1;   -- re-enable
```

### Cross-Engine — FOREIGN KEY

| Feature | MySQL | SQLite | PostgreSQL | SQL Server | Oracle | MS Access |
|---------|-------|--------|------------|------------|--------|-----------|
| Basic FK | ✅ InnoDB only | ⚠️ parsed but NOT enforced by default | ✅ | ✅ | ✅ | ✅ |
| `ON DELETE CASCADE` | ✅ | ⚠️ `PRAGMA foreign_keys = ON` required | ✅ | ✅ | ✅ | ✅ |
| `ON DELETE SET NULL` | ✅ | ✅ (with pragma) | ✅ | ✅ | ✅ | ✅ |
| `ON DELETE SET DEFAULT` | ❌ | ✅ (with pragma) | ✅ | ✅ | ❌ | ❌ |
| `ON UPDATE CASCADE` | ✅ | ✅ (with pragma) | ✅ | ✅ | ❌ | ✅ |
| Composite FK | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Disable FK checks | ✅ `SET FOREIGN_KEY_CHECKS=0` | ⚠️ `PRAGMA foreign_keys=OFF` | ⚠️ `SET session_replication_role='replica'` | ⚠️ `ALTER TABLE NOCHECK CONSTRAINT ALL` | ⚠️ `DISABLE CONSTRAINT` | ❌ |

> ⚠️ **SQLite**: Foreign keys are **parsed but silently ignored** unless you run `PRAGMA foreign_keys = ON` at the start of each connection.

---

## 3. 🔑 UNIQUE

> Ensures all values in a column (or combination) are distinct. Allows NULL (multiple NULLs allowed in most engines).

### Inline
```sql
CREATE TABLE users (
  id    INT          NOT NULL AUTO_INCREMENT PRIMARY KEY,
  email VARCHAR(150) NOT NULL UNIQUE
);
```

### Table-level (named)
```sql
CREATE TABLE users (
  id       INT          NOT NULL AUTO_INCREMENT,
  email    VARCHAR(150) NOT NULL,
  username VARCHAR(50)  NOT NULL,
  CONSTRAINT pk_users       PRIMARY KEY (id),
  CONSTRAINT uq_users_email UNIQUE (email),
  CONSTRAINT uq_users_uname UNIQUE (username)
);
```

### Composite UNIQUE (combination must be unique)
```sql
CREATE TABLE team_members (
  team_id INT NOT NULL,
  user_id INT NOT NULL,
  CONSTRAINT uq_team_member UNIQUE (team_id, user_id)
);
```

### NULL behavior in UNIQUE columns

| Engine | Multiple NULLs allowed in UNIQUE column? |
|--------|------------------------------------------|
| MySQL | ✅ Yes (NULLs are not considered equal) |
| SQLite | ✅ Yes |
| PostgreSQL | ✅ Yes |
| SQL Server | ✅ Yes (only one NULL in older versions; fixed in newer) |
| Oracle | ✅ Yes |
| MS Access | ❌ No — only one NULL allowed |

### Cross-Engine — UNIQUE

| Feature | MySQL | SQLite | PostgreSQL | SQL Server | Oracle | MS Access |
|---------|-------|--------|------------|------------|--------|-----------|
| Inline `UNIQUE` | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Named `UNIQUE` constraint | ✅ | ⚠️ name ignored | ✅ | ✅ | ✅ | ❌ |
| Composite `UNIQUE` | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| UNIQUE auto-creates index | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |

---

## 4. 🚫 NOT NULL

> Prevents NULL values from being stored in a column.

### Inline (most common)
```sql
CREATE TABLE products (
  id    INT           NOT NULL AUTO_INCREMENT PRIMARY KEY,
  name  VARCHAR(100)  NOT NULL,
  price DECIMAL(10,2) NOT NULL,
  notes TEXT          NULL           -- explicitly nullable
);
```

### Columns are nullable by default
```sql
-- These two are equivalent:
description TEXT NULL
description TEXT          -- NULL is the default if omitted
```

### NOT NULL with DEFAULT (best practice)
```sql
CREATE TABLE events (
  id         INT          NOT NULL AUTO_INCREMENT PRIMARY KEY,
  title      VARCHAR(200) NOT NULL,
  is_active  TINYINT(1)   NOT NULL DEFAULT 1,
  created_at DATETIME     NOT NULL DEFAULT CURRENT_TIMESTAMP
);
```

### Cross-Engine — NOT NULL

| Feature | MySQL | SQLite | PostgreSQL | SQL Server | Oracle | MS Access |
|---------|-------|--------|------------|------------|--------|-----------|
| `NOT NULL` inline | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Columns nullable by default | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `ALTER COLUMN` to add/remove NOT NULL | ✅ | ❌ recreate table | ✅ | ⚠️ `ALTER COLUMN col TYPE NOT NULL` | ⚠️ `MODIFY col NOT NULL` | ❌ |

---

## 5. ✅ CHECK

> Validates that column values satisfy a boolean expression.

### Inline
```sql
CREATE TABLE employees (
  id     INT            NOT NULL AUTO_INCREMENT PRIMARY KEY,
  name   VARCHAR(100)   NOT NULL,
  salary DECIMAL(10,2)  NOT NULL CHECK (salary >= 0),
  age    INT            CHECK (age BETWEEN 18 AND 70)
);
```

### Table-level (named — recommended)
```sql
CREATE TABLE products (
  id       INT           NOT NULL AUTO_INCREMENT,
  name     VARCHAR(100)  NOT NULL,
  price    DECIMAL(10,2) NOT NULL,
  discount DECIMAL(5,2)  NOT NULL DEFAULT 0,
  CONSTRAINT pk_products        PRIMARY KEY (id),
  CONSTRAINT chk_price_positive CHECK (price > 0),
  CONSTRAINT chk_discount_range CHECK (discount BETWEEN 0 AND 100)
);
```

### Multi-column CHECK
```sql
CREATE TABLE bookings (
  id         INT      NOT NULL AUTO_INCREMENT PRIMARY KEY,
  start_date DATE     NOT NULL,
  end_date   DATE     NOT NULL,
  CONSTRAINT chk_dates CHECK (end_date >= start_date)
);
```

### CHECK with expression
```sql
CREATE TABLE accounts (
  id       INT          NOT NULL AUTO_INCREMENT PRIMARY KEY,
  username VARCHAR(50)  NOT NULL,
  email    VARCHAR(150) NOT NULL,
  role     VARCHAR(20)  NOT NULL,
  CONSTRAINT chk_valid_role CHECK (role IN ('admin', 'editor', 'viewer')),
  CONSTRAINT chk_email_fmt  CHECK (email LIKE '%@%.%')
);
```

### Cross-Engine — CHECK

| Feature | MySQL | SQLite | PostgreSQL | SQL Server | Oracle | MS Access |
|---------|-------|--------|------------|------------|--------|-----------|
| `CHECK` inline | ✅ 8.0.16+ (enforced) | ✅ | ✅ | ✅ | ✅ | ✅ |
| Named `CHECK` | ✅ | ⚠️ name ignored | ✅ | ✅ | ✅ | ❌ |
| Multi-column `CHECK` | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `CHECK` with subquery | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| Enforce existing data on add | ✅ | ✅ | ✅ | ⚠️ use `WITH CHECK` | ✅ | ❌ |

> ⚠️ **MySQL < 8.0.16**: CHECK constraints are parsed but **silently ignored** — they have no effect. Upgrade to 8.0.16+ for enforcement.

---

## 6. 📋 DEFAULT

> Provides an automatic value when no value is specified on INSERT.

### Basic DEFAULT
```sql
CREATE TABLE orders (
  id          INT          NOT NULL AUTO_INCREMENT PRIMARY KEY,
  status      VARCHAR(20)  NOT NULL DEFAULT 'pending',
  is_paid     TINYINT(1)   NOT NULL DEFAULT 0,
  created_at  DATETIME     NOT NULL DEFAULT CURRENT_TIMESTAMP,
  updated_at  DATETIME     NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
  notes       TEXT                  DEFAULT NULL
);
```

### DEFAULT with expressions (MySQL 8.0.13+)
```sql
CREATE TABLE events (
  id         INT         NOT NULL AUTO_INCREMENT PRIMARY KEY,
  code       VARCHAR(20) NOT NULL DEFAULT (CONCAT('EVT-', LPAD(id, 6, '0'))),
  expires_at DATETIME    NOT NULL DEFAULT (NOW() + INTERVAL 30 DAY)
);
```

### Using DEFAULT in INSERT
```sql
-- Omit the column — default applies
INSERT INTO orders (status) VALUES ('processing');

-- Explicitly use DEFAULT keyword
INSERT INTO orders (status, is_paid) VALUES (DEFAULT, 1);
```

### Cross-Engine — DEFAULT

| Feature | MySQL | SQLite | PostgreSQL | SQL Server | Oracle | MS Access |
|---------|-------|--------|------------|------------|--------|-----------|
| Literal `DEFAULT` | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `DEFAULT CURRENT_TIMESTAMP` | ✅ | ✅ | ✅ | ⚠️ `DEFAULT GETDATE()` | ⚠️ `DEFAULT SYSDATE` | ⚠️ `DEFAULT Now()` |
| `DEFAULT` expression | ✅ 8.0.13+ | ✅ | ✅ | ✅ | ✅ | ❌ |
| `ON UPDATE CURRENT_TIMESTAMP` | ✅ | ❌ use trigger | ❌ use trigger | ❌ use trigger | ❌ use trigger | ❌ |

---

## 7. 🔢 AUTO_INCREMENT / Identity

> Automatically generates a unique integer for each new row.

### MySQL — AUTO_INCREMENT
```sql
CREATE TABLE users (
  id   INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(100) NOT NULL
);

-- Reset the counter
ALTER TABLE users AUTO_INCREMENT = 1000;

-- Get last inserted ID
SELECT LAST_INSERT_ID();
```

### Cross-Engine — Auto-generated Keys

| Engine | Syntax | Get Last ID |
|--------|--------|-------------|
| **MySQL** | `INT AUTO_INCREMENT PRIMARY KEY` | `SELECT LAST_INSERT_ID();` |
| **SQLite** | `INTEGER PRIMARY KEY` (implicit) or `INTEGER PRIMARY KEY AUTOINCREMENT` | `SELECT last_insert_rowid();` |
| **PostgreSQL** | `SERIAL` / `BIGSERIAL` or `GENERATED ALWAYS AS IDENTITY` | `SELECT lastval();` or `RETURNING id` |
| **SQL Server** | `INT IDENTITY(1,1)` | `SELECT SCOPE_IDENTITY();` or `OUTPUT INSERTED.id` |
| **Oracle** | `NUMBER GENERATED ALWAYS AS IDENTITY` or Sequence + Trigger | `SELECT seq.CURRVAL FROM DUAL;` |
| **MS Access** | `AUTOINCREMENT` or `COUNTER` | `SELECT @@IDENTITY;` |

### PostgreSQL — IDENTITY (modern approach)
```sql
CREATE TABLE users (
  id   INT  GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
  name TEXT NOT NULL
);

-- Or allow manual override:
id INT GENERATED BY DEFAULT AS IDENTITY PRIMARY KEY
```

### SQL Server — IDENTITY
```sql
CREATE TABLE users (
  id   INT IDENTITY(1,1) PRIMARY KEY,  -- start=1, increment=1
  name NVARCHAR(100) NOT NULL
);
```

---

## 8. ➕ Adding Constraints to Existing Tables

> Use ALTER TABLE to add constraints after table creation.

### Add PRIMARY KEY
```sql
ALTER TABLE employees
ADD CONSTRAINT pk_employees PRIMARY KEY (id);
```

### Add FOREIGN KEY
```sql
ALTER TABLE orders
ADD CONSTRAINT fk_orders_customer
  FOREIGN KEY (customer_id) REFERENCES customers(id)
  ON DELETE CASCADE;
```

### Add UNIQUE
```sql
ALTER TABLE users
ADD CONSTRAINT uq_users_email UNIQUE (email);
```

### Add CHECK
```sql
ALTER TABLE products
ADD CONSTRAINT chk_price CHECK (price > 0);
```

### Add DEFAULT
```sql
-- MySQL
ALTER TABLE orders MODIFY COLUMN status VARCHAR(20) NOT NULL DEFAULT 'pending';

-- PostgreSQL / SQL Server
ALTER TABLE orders ALTER COLUMN status SET DEFAULT 'pending';
```

### Add NOT NULL
```sql
-- MySQL
ALTER TABLE users MODIFY COLUMN email VARCHAR(150) NOT NULL;

-- PostgreSQL
ALTER TABLE users ALTER COLUMN email SET NOT NULL;

-- SQL Server
ALTER TABLE users ALTER COLUMN email VARCHAR(150) NOT NULL;
```

### Cross-Engine — ALTER TABLE ADD CONSTRAINT

| Constraint | MySQL | SQLite | PostgreSQL | SQL Server | Oracle | MS Access |
|------------|-------|--------|------------|------------|--------|-----------|
| `ADD PRIMARY KEY` | ✅ | ❌ recreate | ✅ | ✅ | ✅ | ❌ |
| `ADD FOREIGN KEY` | ✅ | ❌ recreate | ✅ | ✅ | ✅ | ✅ |
| `ADD UNIQUE` | ✅ | ❌ recreate | ✅ | ✅ | ✅ | ❌ |
| `ADD CHECK` | ✅ | ❌ recreate | ✅ | ✅ | ✅ | ❌ |
| `SET DEFAULT` | ⚠️ use MODIFY | ❌ recreate | ✅ | ⚠️ `ADD DEFAULT` | ⚠️ `MODIFY` | ❌ |
| `SET NOT NULL` | ⚠️ use MODIFY | ❌ recreate | ✅ | ⚠️ `ALTER COLUMN` | ⚠️ `MODIFY` | ❌ |

> ⚠️ **SQLite**: Does **not** support ALTER TABLE ADD CONSTRAINT for most cases. The workaround is: create a new table with the desired constraints → copy data → drop old table → rename new table.

---

## 9. ➖ Dropping Constraints

### Drop PRIMARY KEY
```sql
-- MySQL
ALTER TABLE employees DROP PRIMARY KEY;

-- PostgreSQL / SQL Server / Oracle
ALTER TABLE employees DROP CONSTRAINT pk_employees;
```

### Drop FOREIGN KEY
```sql
-- MySQL
ALTER TABLE orders DROP FOREIGN KEY fk_orders_customer;

-- PostgreSQL / SQL Server / Oracle
ALTER TABLE orders DROP CONSTRAINT fk_orders_customer;
```

### Drop UNIQUE
```sql
-- MySQL
ALTER TABLE users DROP INDEX uq_users_email;

-- PostgreSQL / Oracle
ALTER TABLE users DROP CONSTRAINT uq_users_email;

-- SQL Server
ALTER TABLE users DROP CONSTRAINT uq_users_email;
```

### Drop CHECK
```sql
-- MySQL / PostgreSQL / SQL Server / Oracle
ALTER TABLE products DROP CONSTRAINT chk_price;
```

### Drop DEFAULT
```sql
-- MySQL
ALTER TABLE orders MODIFY COLUMN status VARCHAR(20) NOT NULL;  -- remove DEFAULT by omitting it

-- PostgreSQL
ALTER TABLE orders ALTER COLUMN status DROP DEFAULT;

-- SQL Server
ALTER TABLE orders DROP CONSTRAINT df_orders_status;   -- must know the constraint name
```

### Drop NOT NULL
```sql
-- MySQL
ALTER TABLE users MODIFY COLUMN email VARCHAR(150) NULL;

-- PostgreSQL
ALTER TABLE users ALTER COLUMN email DROP NOT NULL;

-- SQL Server
ALTER TABLE users ALTER COLUMN email VARCHAR(150) NULL;
```

### Cross-Engine — DROP CONSTRAINT

| Constraint | MySQL | SQLite | PostgreSQL | SQL Server | Oracle | MS Access |
|------------|-------|--------|------------|------------|--------|-----------|
| `DROP PRIMARY KEY` | ✅ | ❌ recreate | ✅ | ✅ | ✅ | ❌ |
| `DROP FOREIGN KEY` | ✅ (separate keyword) | ❌ | ✅ | ✅ | ✅ | ✅ |
| `DROP UNIQUE` | ⚠️ `DROP INDEX` | ❌ | ✅ | ✅ | ✅ | ❌ |
| `DROP CHECK` | ✅ | ❌ | ✅ | ✅ | ✅ | ❌ |
| `DROP DEFAULT` | ⚠️ via MODIFY | ❌ | ✅ `DROP DEFAULT` | ⚠️ drop named constraint | ⚠️ MODIFY | ❌ |

---

## 10. 🔍 Viewing & Inspecting Constraints

### MySQL
```sql
-- All constraints on a table
SELECT constraint_name, constraint_type, table_name
FROM information_schema.TABLE_CONSTRAINTS
WHERE table_schema = 'your_db' AND table_name = 'employees';

-- Foreign key details
SELECT constraint_name, column_name, referenced_table_name, referenced_column_name
FROM information_schema.KEY_COLUMN_USAGE
WHERE table_schema = 'your_db' AND table_name = 'employees'
  AND referenced_table_name IS NOT NULL;

-- Check constraints (MySQL 8.0.16+)
SELECT constraint_name, check_clause
FROM information_schema.CHECK_CONSTRAINTS
WHERE constraint_schema = 'your_db';

-- Quick view using SHOW
SHOW CREATE TABLE employees;
```

### PostgreSQL
```sql
-- All constraints
SELECT conname AS name, contype AS type, pg_get_constraintdef(oid) AS definition
FROM pg_constraint
WHERE conrelid = 'employees'::regclass;

-- contype codes: p=primary key, f=foreign key, u=unique, c=check, n=not null
```

### SQL Server
```sql
SELECT name, type_desc, definition
FROM sys.check_constraints
WHERE parent_object_id = OBJECT_ID('employees');

SELECT fk.name, col.name AS column, ref.name AS ref_table
FROM sys.foreign_keys fk
JOIN sys.foreign_key_columns fkc ON fk.object_id = fkc.constraint_object_id
JOIN sys.columns col ON fkc.parent_column_id = col.column_id AND fkc.parent_object_id = col.object_id
JOIN sys.tables ref ON fkc.referenced_object_id = ref.object_id;
```

### Oracle
```sql
SELECT constraint_name, constraint_type, search_condition, status
FROM user_constraints
WHERE table_name = 'EMPLOYEES';
```

### SQLite
```sql
PRAGMA table_info(employees);         -- columns + NOT NULL + DEFAULT
PRAGMA foreign_key_list(employees);   -- FK details
PRAGMA index_list(employees);         -- indexes (includes UNIQUE)
```

---

## 11. ⏸️ Deferrable Constraints {: #11--deferrable-constraints}

> Delay constraint checking until end of transaction (useful for circular FKs or bulk operations).

### PostgreSQL — DEFERRABLE
```sql
CREATE TABLE employees (
  id         INT  NOT NULL PRIMARY KEY,
  manager_id INT,
  CONSTRAINT fk_manager
    FOREIGN KEY (manager_id) REFERENCES employees(id)
    DEFERRABLE INITIALLY DEFERRED   -- checked at COMMIT, not on each statement
);

-- Or defer at runtime within a transaction:
BEGIN;
SET CONSTRAINTS fk_manager DEFERRED;
  INSERT INTO employees (id, manager_id) VALUES (1, 2);
  INSERT INTO employees (id, manager_id) VALUES (2, 1);
COMMIT;
```

### SQL Server — WITH NOCHECK
```sql
-- Add FK but don't validate existing data
ALTER TABLE orders
ADD CONSTRAINT fk_orders_customer
  FOREIGN KEY (customer_id) REFERENCES customers(id)
  WITH NOCHECK;

-- Temporarily disable a constraint
ALTER TABLE orders NOCHECK CONSTRAINT fk_orders_customer;
ALTER TABLE orders  CHECK CONSTRAINT fk_orders_customer;
```

### Oracle — DISABLE / ENABLE
```sql
ALTER TABLE orders DISABLE CONSTRAINT fk_orders_customer;
ALTER TABLE orders ENABLE  CONSTRAINT fk_orders_customer;
ALTER TABLE orders ENABLE  NOVALIDATE CONSTRAINT fk_orders_customer;  -- enable without validating existing rows
```

### Cross-Engine — Deferrable / Disable

| Feature | MySQL | SQLite | PostgreSQL | SQL Server | Oracle | MS Access |
|---------|-------|--------|------------|------------|--------|-----------|
| `DEFERRABLE INITIALLY DEFERRED` | ❌ | ❌ | ✅ | ❌ | ✅ | ❌ |
| `DISABLE CONSTRAINT` | ⚠️ `SET FOREIGN_KEY_CHECKS=0` | ❌ | ⚠️ drop & recreate | ✅ `NOCHECK CONSTRAINT` | ✅ | ❌ |
| `WITH NOCHECK` (skip existing) | ❌ | ❌ | ❌ | ✅ | ⚠️ `ENABLE NOVALIDATE` | ❌ |

---

## 12. 📝 Constraint Naming Best Practices

> Always name your constraints — it makes ALTER, DROP, and error messages far easier.

### Recommended Naming Convention

| Constraint | Prefix | Pattern | Example |
|------------|--------|---------|---------|
| Primary Key | `pk_` | `pk_<table>` | `pk_employees` |
| Foreign Key | `fk_` | `fk_<table>_<ref_table>` | `fk_orders_customers` |
| Unique | `uq_` | `uq_<table>_<column>` | `uq_users_email` |
| Check | `chk_` | `chk_<table>_<rule>` | `chk_products_price` |
| Default | `df_` | `df_<table>_<column>` | `df_orders_status` |
| Index | `idx_` | `idx_<table>_<column>` | `idx_employees_dept` |

### Full Example — All Constraints Named
```sql
CREATE TABLE employees (
  id          INT            NOT NULL,
  name        VARCHAR(100)   NOT NULL,
  email       VARCHAR(150)   NOT NULL,
  dept_id     INT,
  salary      DECIMAL(10,2)  NOT NULL DEFAULT 0.00,
  role        VARCHAR(20)    NOT NULL DEFAULT 'viewer',
  start_date  DATE           NOT NULL,
  end_date    DATE,
  created_at  DATETIME       NOT NULL DEFAULT CURRENT_TIMESTAMP,

  CONSTRAINT pk_employees          PRIMARY KEY (id),
  CONSTRAINT uq_employees_email    UNIQUE (email),
  CONSTRAINT fk_employees_dept     FOREIGN KEY (dept_id)
                                     REFERENCES departments(id)
                                     ON DELETE SET NULL
                                     ON UPDATE CASCADE,
  CONSTRAINT chk_salary_positive   CHECK (salary >= 0),
  CONSTRAINT chk_valid_role        CHECK (role IN ('admin', 'editor', 'viewer')),
  CONSTRAINT chk_dates_order       CHECK (end_date IS NULL OR end_date >= start_date)
);
```

---

## 13. 📊 Cross-Engine Master Table

| Constraint | MySQL | SQLite | PostgreSQL | SQL Server | Oracle | MS Access |
|------------|-------|--------|------------|------------|--------|-----------|
| `PRIMARY KEY` | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `FOREIGN KEY` (enforced) | ✅ InnoDB | ⚠️ pragma needed | ✅ | ✅ | ✅ | ✅ |
| `UNIQUE` | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `NOT NULL` | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `CHECK` (enforced) | ✅ 8.0.16+ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `DEFAULT` | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Named constraints | ✅ | ⚠️ ignored | ✅ | ✅ | ✅ | ❌ |
| `ALTER TABLE ADD CONSTRAINT` | ✅ | ❌ | ✅ | ✅ | ✅ | ⚠️ |
| `ALTER TABLE DROP CONSTRAINT` | ✅ | ❌ | ✅ | ✅ | ✅ | ❌ |
| Deferrable constraints | ❌ | ❌ | ✅ | ❌ | ✅ | ❌ |
| Disable / re-enable constraint | ⚠️ FK only | ❌ | ❌ | ✅ | ✅ | ❌ |
| Auto-increment | ✅ `AUTO_INCREMENT` | ✅ `AUTOINCREMENT` | ✅ `SERIAL` / `IDENTITY` | ✅ `IDENTITY` | ✅ `IDENTITY` / Sequence | ✅ `AUTOINCREMENT` |

---

## 14. 🛠️ Common Patterns & Examples {: #14--common-patterns--examples}

---

### Pattern 1 — Prevent orphan rows (FK + Cascade)
```sql
-- Deleting a customer automatically deletes their orders
CREATE TABLE orders (
  id          INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
  customer_id INT NOT NULL,
  CONSTRAINT fk_orders_cust
    FOREIGN KEY (customer_id) REFERENCES customers(id)
    ON DELETE CASCADE
);
```

### Pattern 2 — Enforce valid status values (CHECK)
```sql
CONSTRAINT chk_order_status
  CHECK (status IN ('draft', 'pending', 'confirmed', 'shipped', 'cancelled'))
```

### Pattern 3 — Prevent negative numbers (CHECK)
```sql
CONSTRAINT chk_qty_positive   CHECK (qty > 0),
CONSTRAINT chk_price_positive CHECK (price >= 0.00)
```

### Pattern 4 — Enforce date logic (multi-column CHECK)
```sql
CONSTRAINT chk_date_range CHECK (end_date IS NULL OR end_date > start_date)
```

### Pattern 5 — Unique combination, not individual columns
```sql
-- A user can only have one membership per team
CONSTRAINT uq_team_user UNIQUE (team_id, user_id)
```

### Pattern 6 — Soft delete with UNIQUE only on active rows (PostgreSQL partial index)
```sql
-- Only enforce uniqueness on active (non-deleted) rows
CREATE UNIQUE INDEX uq_active_email
  ON users(email)
  WHERE deleted_at IS NULL;
```

### Pattern 7 — Self-referencing FK (tree/hierarchy)
```sql
CREATE TABLE categories (
  id        INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
  name      VARCHAR(100) NOT NULL,
  parent_id INT,
  CONSTRAINT fk_category_parent
    FOREIGN KEY (parent_id) REFERENCES categories(id)
    ON DELETE SET NULL
);
```

### Pattern 8 — Audit timestamps (DEFAULT + AUTO UPDATE)
```sql
created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
updated_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
```

### Pattern 9 — SQLite workaround for adding constraints
```sql
-- SQLite does not support ALTER TABLE ADD CONSTRAINT.
-- Standard workaround:

-- Step 1: Create new table with desired constraints
CREATE TABLE employees_new (
  id     INTEGER PRIMARY KEY AUTOINCREMENT,
  name   TEXT    NOT NULL,
  email  TEXT    NOT NULL UNIQUE,
  salary REAL    NOT NULL CHECK (salary >= 0)
);

-- Step 2: Copy data
INSERT INTO employees_new SELECT * FROM employees;

-- Step 3: Drop old table
DROP TABLE employees;

-- Step 4: Rename new table
ALTER TABLE employees_new RENAME TO employees;
```

### Pattern 10 — Find tables with no PK (data quality check)
```sql
-- MySQL
SELECT table_name
FROM information_schema.tables t
WHERE table_schema = DATABASE()
  AND table_type = 'BASE TABLE'
  AND table_name NOT IN (
    SELECT table_name
    FROM information_schema.table_constraints
    WHERE constraint_type = 'PRIMARY KEY'
      AND table_schema = DATABASE()
  );
```

---

## Quick Reference Card

| Constraint | Purpose | NULL allowed? | Per table limit |
|------------|---------|---------------|-----------------|
| `PRIMARY KEY` | Unique row identity | ❌ Never | 1 only |
| `FOREIGN KEY` | Link to another table's PK | ✅ (means no parent) | Many |
| `UNIQUE` | No duplicate values | ✅ (multiple NULLs OK) | Many |
| `NOT NULL` | Value required | — | Per column |
| `CHECK` | Custom validation rule | ✅ (NULL skips check) | Many |
| `DEFAULT` | Auto-fill when omitted | — | Per column |

> 💡 **NULL skips CHECK**: A NULL value in a CHECK column does **not** trigger a violation — the check is simply skipped. Combine `NOT NULL` + `CHECK` to fully control a column.

---

*Syntax primarily shown for MySQL 8.x. Engine-specific alternatives noted throughout.*
