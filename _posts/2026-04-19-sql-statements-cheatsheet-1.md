---

title: SQL Statements Cheatsheet

description: >-
  A comprehensive cheatsheet covering all SQL statements, including DDL, DML, DQL, Joins, Subqueries & CTEs, Grouping & Aggregation, Filtering & Sorting, Indexes, Views, Stored Procedures & Functions, Triggers, Transactions, DCL, and Common Patterns. Includes inline and table-level syntax, add/drop/modify examples, cross-engine compatibility.
date: 2026-04-22 10:00:00 +0800
author: Mahmoud Lotfi
file_name: 2026-04-22-sql-statements-cheatsheet-1.md
categories: [SQL, statements, cheatsheet]
tags: [SQL, statements, cheatsheet]
pin: False
math: true
mermaid: true
comments: true
toc: true
render_with_liquid: false

image:
  path: /assets/img/posts/sql.jpg
  alt: SQL Statements Cheatsheet
  lqip: data:image/webp;base64,UklGRjoAAABXRUJQVlA4IC4AAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
---

# 📘 SQL Statements Cheatsheet
> Grouped by category · Full syntax examples · Cross-engine compatibility

---

## Legend
| Symbol | Meaning |
|--------|---------|
| ✅ | Supported (same or very similar syntax) |
| ⚠️ | Supported with different syntax |
| ❌ | Not supported / no direct equivalent |

---

## In article
Here's your SQL Statements Cheatsheet! It covers **14 categories**:

| # | Category | What's Inside |
|---|----------|---------------|
| 1 | **DDL** | CREATE / ALTER / DROP / TRUNCATE TABLE, DATABASE, INDEX |
| 2 | **DML** | INSERT, UPDATE, DELETE, REPLACE, multi-row & JOIN-based |
| 3 | **DQL** | SELECT anatomy, DISTINCT, pagination, expressions |
| 4 | **Joins** | INNER, LEFT, RIGHT, FULL OUTER, CROSS, SELF, multi-join |
| 5 | **Subqueries & CTEs** | Scalar, derived table, EXISTS, IN, WITH, Recursive CTEs |
| 6 | **Grouping** | GROUP BY, HAVING, ROLLUP, GROUPING SETS, window aggregates |
| 7 | **Filtering & Sorting** | WHERE patterns, REGEXP, ORDER BY, NULLS LAST |
| 8 | **Indexes** | CREATE INDEX, composite, FULLTEXT, partial, EXPLAIN |
| 9 | **Views** | CREATE VIEW, updatable views, Materialized Views |
| 10 | **Procedures & Functions** | Stored procedures, UDFs, CALL / EXEC |
| 11 | **Triggers** | BEFORE/AFTER INSERT/UPDATE/DELETE, audit log example |
| 12 | **Transactions** | START/COMMIT/ROLLBACK, SAVEPOINT, isolation levels |
| 13 | **DCL** | GRANT, REVOKE, CREATE/DROP USER |
| 14 | **Patterns** | Upsert, pagination, pivot, running total, duplicates, date range |

Each section includes a full cross-engine compatibility table for **MySQL, SQLite, PostgreSQL, SQL Server, Oracle, and MS Access**.

---



## Categories
1. [DDL — Data Definition Language](#1--ddl--data-definition-language)
2. [DML — Data Manipulation Language](#2--dml--data-manipulation-language)
3. [DQL — Data Query Language](#3--dql--data-query-language)
4. [Joins](#4--joins)
5. [Subqueries & CTEs](#5--subqueries--ctes)
6. [Grouping & Aggregation](#6--grouping--aggregation)
7. [Filtering & Sorting](#7--filtering--sorting)
8. [Indexes](#8--indexes)
9. [Views](#9--views)
10. [Stored Procedures & Functions](#10--stored-procedures--functions)
11. [Triggers](#11--triggers)
12. [Transactions (TCL)](#12--transactions-tcl)
13. [DCL — Data Control Language](#13--dcl--data-control-language)
14. [Useful Patterns](#14--useful-patterns)

---

## 1. 🏗️ DDL — Data Definition Language

> Create, modify, and delete database structures.

---

### CREATE DATABASE
```sql
CREATE DATABASE shop;
CREATE DATABASE IF NOT EXISTS shop CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```

### DROP DATABASE
```sql
DROP DATABASE shop;
DROP DATABASE IF EXISTS shop;
```

### CREATE TABLE
```sql
CREATE TABLE employees (
  id          INT           NOT NULL AUTO_INCREMENT,
  name        VARCHAR(100)  NOT NULL,
  email       VARCHAR(150)  UNIQUE,
  dept_id     INT,
  salary      DECIMAL(10,2) DEFAULT 0.00,
  created_at  DATETIME      DEFAULT CURRENT_TIMESTAMP,
  PRIMARY KEY (id),
  FOREIGN KEY (dept_id) REFERENCES departments(id) ON DELETE SET NULL
);
```

### CREATE TABLE … AS SELECT (copy structure + data)
```sql
CREATE TABLE employees_backup AS
  SELECT * FROM employees WHERE created_at < '2024-01-01';
```

### ALTER TABLE
```sql
-- Add column
ALTER TABLE employees ADD COLUMN phone VARCHAR(20) AFTER email;

-- Modify column
ALTER TABLE employees MODIFY COLUMN salary DECIMAL(12,2) NOT NULL;

-- Rename column
ALTER TABLE employees RENAME COLUMN phone TO mobile;

-- Drop column
ALTER TABLE employees DROP COLUMN mobile;

-- Add constraint
ALTER TABLE employees ADD CONSTRAINT chk_salary CHECK (salary >= 0);

-- Drop constraint
ALTER TABLE employees DROP CONSTRAINT chk_salary;

-- Rename table
ALTER TABLE employees RENAME TO staff;
```

### DROP TABLE
```sql
DROP TABLE employees;
DROP TABLE IF EXISTS employees;
DROP TABLE employees CASCADE;   -- drops dependent objects too
```

### TRUNCATE TABLE
```sql
TRUNCATE TABLE employees;       -- delete all rows, reset AUTO_INCREMENT, faster than DELETE
```

### CREATE INDEX / DROP INDEX
```sql
CREATE INDEX idx_email ON employees(email);
CREATE UNIQUE INDEX idx_unique_email ON employees(email);
DROP INDEX idx_email ON employees;
```

### Cross-Engine Compatibility — DDL

| Statement | MySQL | SQLite | PostgreSQL | SQL Server | Oracle | MS Access |
|-----------|-------|--------|------------|------------|--------|-----------|
| `CREATE DATABASE` | ✅ | ❌ file-based | ✅ | ✅ `CREATE DATABASE` | ✅ `CREATE SCHEMA` | ❌ |
| `AUTO_INCREMENT` | ✅ | ⚠️ `AUTOINCREMENT` | ⚠️ `SERIAL` or `GENERATED ALWAYS AS IDENTITY` | ⚠️ `IDENTITY(1,1)` | ⚠️ `GENERATED ALWAYS AS IDENTITY` | ⚠️ `AUTOINCREMENT` |
| `CREATE TABLE AS SELECT` | ✅ | ✅ | ✅ | ⚠️ `SELECT INTO new_table FROM ...` | ✅ | ❌ |
| `RENAME COLUMN` | ✅ 8.0+ | ✅ 3.25+ | ✅ | ⚠️ `sp_rename` | ✅ 12c+ | ❌ |
| `TRUNCATE` | ✅ | ❌ use `DELETE` | ✅ | ✅ | ✅ | ❌ |
| `DROP … CASCADE` | ⚠️ for views | ❌ | ✅ | ❌ | ✅ | ❌ |

---

## 2. ✏️ DML — Data Manipulation Language

> Insert, update, delete, and replace rows.

---

### INSERT
```sql
-- Single row
INSERT INTO employees (name, email, salary)
VALUES ('Alice Smith', 'alice@example.com', 75000);

-- Multiple rows
INSERT INTO employees (name, email, salary) VALUES
  ('Bob Jones',    'bob@example.com',   65000),
  ('Carol White',  'carol@example.com', 80000),
  ('David Brown',  'david@example.com', 70000);

-- Insert from SELECT
INSERT INTO employees_archive (id, name, salary)
  SELECT id, name, salary FROM employees WHERE active = 0;
```

### INSERT … ON DUPLICATE KEY UPDATE (Upsert)
```sql
INSERT INTO products (sku, name, stock)
VALUES ('ABC123', 'Widget', 50)
ON DUPLICATE KEY UPDATE
  stock = stock + VALUES(stock),
  name  = VALUES(name);
```

### UPDATE
```sql
-- Single table
UPDATE employees
SET salary = salary * 1.10,
    updated_at = NOW()
WHERE dept_id = 3;

-- Multi-table update (join)
UPDATE employees e
JOIN departments d ON e.dept_id = d.id
SET e.salary = e.salary * 1.15
WHERE d.name = 'Engineering';
```

### DELETE
```sql
-- Delete with condition
DELETE FROM employees WHERE active = 0 AND last_login < '2023-01-01';

-- Delete with join
DELETE e
FROM employees e
JOIN departments d ON e.dept_id = d.id
WHERE d.name = 'Temp';

-- Delete all rows (use TRUNCATE for speed if no WHERE needed)
DELETE FROM employees;
```

### REPLACE INTO (MySQL-specific)
```sql
-- Delete + re-insert if PK/UNIQUE exists, plain insert otherwise
REPLACE INTO products (id, name, price)
VALUES (1, 'Updated Widget', 19.99);
```

### Cross-Engine Compatibility — DML

| Statement | MySQL | SQLite | PostgreSQL | SQL Server | Oracle | MS Access |
|-----------|-------|--------|------------|------------|--------|-----------|
| `INSERT` | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Multi-row `INSERT` | ✅ | ✅ 3.7.11+ | ✅ | ✅ | ✅ 23c+ | ❌ |
| `INSERT … SELECT` | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `ON DUPLICATE KEY UPDATE` | ✅ | ⚠️ `INSERT OR REPLACE` | ⚠️ `ON CONFLICT DO UPDATE` | ⚠️ `MERGE` | ⚠️ `MERGE` | ❌ |
| `UPDATE … JOIN` | ✅ | ❌ use subquery | ⚠️ `UPDATE … FROM` | ⚠️ `UPDATE … FROM` | ⚠️ `MERGE` | ✅ |
| `DELETE … JOIN` | ✅ | ❌ use subquery | ⚠️ `DELETE … USING` | ⚠️ `DELETE … FROM` | ⚠️ `DELETE … WHERE EXISTS` | ✅ |
| `REPLACE INTO` | ✅ | ⚠️ `INSERT OR REPLACE` | ❌ | ❌ | ❌ | ❌ |

---

## 3. 🔍 DQL — Data Query Language

> Retrieve data from tables.

---

### SELECT — Full Anatomy
```sql
SELECT   [DISTINCT] column1, column2, expression AS alias
FROM     table1
JOIN     table2 ON table1.id = table2.fk_id
WHERE    condition
GROUP BY column1
HAVING   aggregate_condition
ORDER BY column1 [ASC|DESC]
LIMIT    10 OFFSET 20;
```

### SELECT with expressions
```sql
SELECT
  name,
  salary,
  salary * 12                          AS annual_salary,
  ROUND(salary / 1000, 1)              AS k_salary,
  CONCAT(first_name, ' ', last_name)   AS full_name,
  CASE WHEN salary > 80000 THEN 'Senior' ELSE 'Junior' END AS level
FROM employees;
```

### DISTINCT
```sql
SELECT DISTINCT dept_id FROM employees;
SELECT COUNT(DISTINCT dept_id) FROM employees;
```

### LIMIT / OFFSET (Pagination)
```sql
SELECT * FROM products ORDER BY name LIMIT 10 OFFSET 20;  -- page 3, 10 per page
```

### Cross-Engine Compatibility — SELECT / Pagination

| Clause | MySQL | SQLite | PostgreSQL | SQL Server | Oracle | MS Access |
|--------|-------|--------|------------|------------|--------|-----------|
| `LIMIT n` | ✅ | ✅ | ✅ | ⚠️ `TOP n` or `FETCH FIRST n ROWS ONLY` | ⚠️ `FETCH FIRST n ROWS ONLY` (12c+) | ⚠️ `TOP n` |
| `LIMIT n OFFSET m` | ✅ | ✅ | ✅ | ⚠️ `OFFSET m ROWS FETCH NEXT n ROWS ONLY` | ⚠️ `OFFSET m ROWS FETCH NEXT n ROWS ONLY` | ❌ |
| `DISTINCT` | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Column aliases in `WHERE` | ❌ use subquery | ❌ | ❌ | ❌ | ❌ | ✅ |
| Column aliases in `ORDER BY` | ✅ | ✅ | ✅ | ✅ | ❌ | ✅ |

---

## 4. 🔗 Joins

> Combine rows from multiple tables.

---

### INNER JOIN — only matching rows
```sql
SELECT e.name, d.name AS dept
FROM employees e
INNER JOIN departments d ON e.dept_id = d.id;
```

### LEFT JOIN — all rows from left, NULLs for no match
```sql
SELECT e.name, d.name AS dept
FROM employees e
LEFT JOIN departments d ON e.dept_id = d.id;
```

### RIGHT JOIN — all rows from right, NULLs for no match
```sql
SELECT e.name, d.name AS dept
FROM employees e
RIGHT JOIN departments d ON e.dept_id = d.id;
```

### FULL OUTER JOIN — all rows from both sides
```sql
-- MySQL does not support FULL OUTER JOIN directly; emulate with UNION:
SELECT e.name, d.name AS dept FROM employees e LEFT  JOIN departments d ON e.dept_id = d.id
UNION
SELECT e.name, d.name AS dept FROM employees e RIGHT JOIN departments d ON e.dept_id = d.id;
```

### CROSS JOIN — cartesian product
```sql
SELECT colors.name, sizes.label
FROM colors CROSS JOIN sizes;
```

### SELF JOIN — join a table to itself
```sql
SELECT e.name AS employee, m.name AS manager
FROM employees e
LEFT JOIN employees m ON e.manager_id = m.id;
```

### Multiple Joins
```sql
SELECT
  o.id        AS order_id,
  c.name      AS customer,
  p.name      AS product,
  oi.qty,
  oi.qty * p.price AS line_total
FROM orders o
JOIN customers  c  ON o.customer_id = c.id
JOIN order_items oi ON oi.order_id  = o.id
JOIN products   p  ON oi.product_id = p.id
WHERE o.status = 'completed'
ORDER BY o.id;
```

### Cross-Engine Compatibility — Joins

| Join Type | MySQL | SQLite | PostgreSQL | SQL Server | Oracle | MS Access |
|-----------|-------|--------|------------|------------|--------|-----------|
| `INNER JOIN` | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `LEFT JOIN` | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `RIGHT JOIN` | ✅ | ❌ swap tables | ✅ | ✅ | ✅ | ✅ |
| `FULL OUTER JOIN` | ❌ emulate with UNION | ❌ | ✅ | ✅ | ✅ | ❌ |
| `CROSS JOIN` | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `SELF JOIN` | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |

---

## 5. 📦 Subqueries & CTEs

> Nested queries and reusable query blocks.

---

### Subquery in WHERE
```sql
-- Employees earning above the company average
SELECT name, salary
FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```

### Subquery in FROM (Derived Table)
```sql
SELECT dept, avg_sal
FROM (
  SELECT dept_id AS dept, AVG(salary) AS avg_sal
  FROM employees
  GROUP BY dept_id
) dept_avgs
WHERE avg_sal > 60000;
```

### Subquery in SELECT (Scalar)
```sql
SELECT
  name,
  salary,
  (SELECT AVG(salary) FROM employees) AS company_avg,
  salary - (SELECT AVG(salary) FROM employees) AS diff_from_avg
FROM employees;
```

### EXISTS / NOT EXISTS
```sql
-- Customers who placed at least one order
SELECT name FROM customers c
WHERE EXISTS (
  SELECT 1 FROM orders o WHERE o.customer_id = c.id
);

-- Customers with no orders
SELECT name FROM customers c
WHERE NOT EXISTS (
  SELECT 1 FROM orders o WHERE o.customer_id = c.id
);
```

### IN / NOT IN with subquery
```sql
SELECT name FROM employees
WHERE dept_id IN (SELECT id FROM departments WHERE location = 'Cairo');
```

### CTE — Common Table Expression (WITH)
```sql
WITH dept_stats AS (
  SELECT dept_id, AVG(salary) AS avg_sal, COUNT(*) AS headcount
  FROM employees
  GROUP BY dept_id
)
SELECT e.name, e.salary, ds.avg_sal, ds.headcount
FROM employees e
JOIN dept_stats ds ON e.dept_id = ds.dept_id
WHERE e.salary > ds.avg_sal;
```

### Multiple CTEs
```sql
WITH
  high_earners AS (
    SELECT * FROM employees WHERE salary > 80000
  ),
  dept_names AS (
    SELECT id, name FROM departments
  )
SELECT h.name, h.salary, d.name AS dept
FROM high_earners h
JOIN dept_names d ON h.dept_id = d.id;
```

### Recursive CTE (Hierarchy / Tree)
```sql
-- Org chart: find all reports under manager id=1
WITH RECURSIVE org_chart AS (
  -- anchor: start with the root manager
  SELECT id, name, manager_id, 0 AS level
  FROM employees WHERE id = 1

  UNION ALL

  -- recursive: find their direct reports
  SELECT e.id, e.name, e.manager_id, oc.level + 1
  FROM employees e
  JOIN org_chart oc ON e.manager_id = oc.id
)
SELECT level, name FROM org_chart ORDER BY level;
```

### Cross-Engine Compatibility — Subqueries & CTEs

| Feature | MySQL | SQLite | PostgreSQL | SQL Server | Oracle | MS Access |
|---------|-------|--------|------------|------------|--------|-----------|
| Subquery in `WHERE` | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Derived table in `FROM` | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `EXISTS` / `NOT EXISTS` | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| CTE (`WITH`) | ✅ 8.0+ | ✅ 3.35+ | ✅ | ✅ | ✅ | ❌ |
| Recursive CTE | ✅ 8.0+ | ✅ 3.35+ | ✅ | ✅ | ✅ | ❌ |
| CTE in `UPDATE`/`DELETE` | ✅ 8.0+ | ✅ | ✅ | ✅ | ✅ | ❌ |

---

## 6. 📊 Grouping & Aggregation

> Summarize and group data.

---

### GROUP BY
```sql
SELECT dept_id, COUNT(*) AS headcount, AVG(salary) AS avg_salary
FROM employees
GROUP BY dept_id;
```

### HAVING — filter after grouping
```sql
SELECT dept_id, AVG(salary) AS avg_sal
FROM employees
GROUP BY dept_id
HAVING AVG(salary) > 60000
ORDER BY avg_sal DESC;
```

### GROUP BY with ROLLUP (subtotals)
```sql
-- Adds a summary row for each group level + grand total
SELECT dept_id, job_title, SUM(salary) AS total
FROM employees
GROUP BY dept_id, job_title WITH ROLLUP;
```

### GROUPING SETS (multiple groupings in one query)
```sql
SELECT dept_id, job_title, SUM(salary)
FROM employees
GROUP BY GROUPING SETS (
  (dept_id, job_title),
  (dept_id),
  ()                    -- grand total
);
```

### Window Aggregate (no row collapse)
```sql
SELECT
  name,
  dept_id,
  salary,
  SUM(salary)  OVER (PARTITION BY dept_id) AS dept_total,
  AVG(salary)  OVER (PARTITION BY dept_id) AS dept_avg,
  salary / SUM(salary) OVER (PARTITION BY dept_id) * 100 AS pct_of_dept
FROM employees;
```

### Cross-Engine Compatibility — Grouping

| Feature | MySQL | SQLite | PostgreSQL | SQL Server | Oracle | MS Access |
|---------|-------|--------|------------|------------|--------|-----------|
| `GROUP BY` | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `HAVING` | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `WITH ROLLUP` | ✅ | ❌ | ⚠️ `ROLLUP(...)` syntax | ⚠️ `ROLLUP(...)` | ⚠️ `ROLLUP(...)` | ❌ |
| `GROUPING SETS` | ✅ 8.0+ | ❌ | ✅ | ✅ | ✅ | ❌ |
| Window aggregates | ✅ 8.0+ | ✅ 3.25+ | ✅ | ✅ | ✅ | ❌ |

---

## 7. 🔎 Filtering & Sorting

> Narrow and order result sets.

---

### WHERE — common patterns
```sql
-- Range
WHERE salary BETWEEN 50000 AND 90000

-- List membership
WHERE country IN ('EG', 'US', 'UK')

-- Pattern matching (% = any chars, _ = one char)
WHERE email LIKE '%@gmail.com'
WHERE code  LIKE 'A__-___'

-- NULL checks (never use = NULL)
WHERE phone IS NULL
WHERE phone IS NOT NULL

-- Date range
WHERE created_at >= '2024-01-01' AND created_at < '2025-01-01'

-- Combining
WHERE (salary > 70000 OR role = 'Lead') AND active = 1
```

### Regular Expression filter
```sql
-- MySQL
WHERE name REGEXP '^[A-Z][a-z]+$'

-- PostgreSQL / Oracle
WHERE name ~ '^[A-Z][a-z]+$'

-- SQL Server
-- No native REGEXP; use LIKE patterns or PATINDEX()
```

### ORDER BY
```sql
-- Single column
SELECT * FROM employees ORDER BY salary DESC;

-- Multiple columns
SELECT * FROM employees ORDER BY dept_id ASC, salary DESC;

-- NULL handling (PostgreSQL / Oracle)
SELECT * FROM employees ORDER BY salary DESC NULLS LAST;

-- By expression
SELECT * FROM employees ORDER BY YEAR(hire_date), salary DESC;
```

### Cross-Engine Compatibility — Filtering & Sorting

| Feature | MySQL | SQLite | PostgreSQL | SQL Server | Oracle | MS Access |
|---------|-------|--------|------------|------------|--------|-----------|
| `WHERE` / `AND` / `OR` | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `LIKE` `%` `_` wildcards | ✅ | ✅ | ✅ | ✅ | ✅ | ⚠️ `*` and `?` |
| `REGEXP` | ✅ | ✅ `REGEXP` | ⚠️ `~` operator | ⚠️ `PATINDEX()` | ⚠️ `REGEXP_LIKE()` | ❌ |
| `BETWEEN` | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `ORDER BY … NULLS LAST` | ❌ use `ISNULL(col,1)` | ✅ | ✅ | ❌ use `CASE` | ✅ | ❌ |

---

## 8. 📇 Indexes

> Speed up queries by creating lookup structures.

---

```sql
-- Basic index
CREATE INDEX idx_salary ON employees(salary);

-- Composite index (order matters — most selective column first)
CREATE INDEX idx_dept_salary ON employees(dept_id, salary);

-- Unique index
CREATE UNIQUE INDEX idx_email ON employees(email);

-- Full-text index (for MATCH … AGAINST searches)
CREATE FULLTEXT INDEX idx_ft_desc ON products(description);

-- Partial / functional index (PostgreSQL)
CREATE INDEX idx_active ON employees(id) WHERE active = TRUE;

-- Drop index
DROP INDEX idx_salary ON employees;          -- MySQL
DROP INDEX idx_salary;                       -- PostgreSQL (auto-detects table)
```

### EXPLAIN — query execution plan
```sql
EXPLAIN SELECT * FROM employees WHERE dept_id = 3;
EXPLAIN ANALYZE SELECT * FROM employees WHERE salary > 60000;  -- PostgreSQL
```

### Cross-Engine Compatibility — Indexes

| Feature | MySQL | SQLite | PostgreSQL | SQL Server | Oracle | MS Access |
|---------|-------|--------|------------|------------|--------|-----------|
| `CREATE INDEX` | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `CREATE UNIQUE INDEX` | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `FULLTEXT INDEX` | ✅ InnoDB | ❌ | ⚠️ GIN/GiST indexes | ⚠️ Full-Text Search | ✅ | ❌ |
| Partial index | ❌ | ✅ | ✅ | ⚠️ filtered index | ✅ function-based | ❌ |
| `EXPLAIN` | ✅ | ✅ | ✅ | ⚠️ `SET SHOWPLAN_ALL ON` | ⚠️ `EXPLAIN PLAN FOR` | ❌ |

---

## 9. 👁️ Views

> Virtual tables based on a SELECT query.

---

```sql
-- Create a view
CREATE VIEW active_employees AS
  SELECT id, name, dept_id, salary
  FROM employees
  WHERE active = 1;

-- Query a view like a table
SELECT * FROM active_employees WHERE dept_id = 2;

-- Create or replace (no need to drop first)
CREATE OR REPLACE VIEW active_employees AS
  SELECT id, name, dept_id, salary, email
  FROM employees
  WHERE active = 1;

-- Drop a view
DROP VIEW active_employees;
DROP VIEW IF EXISTS active_employees;

-- Updatable view (simple views without GROUP BY / DISTINCT)
UPDATE active_employees SET salary = 75000 WHERE id = 5;
```

### Materialized View (pre-computed, stored result)
```sql
-- PostgreSQL
CREATE MATERIALIZED VIEW dept_summary AS
  SELECT dept_id, COUNT(*) AS cnt, AVG(salary) AS avg_sal
  FROM employees GROUP BY dept_id;

-- Refresh the materialized view
REFRESH MATERIALIZED VIEW dept_summary;
```

### Cross-Engine Compatibility — Views

| Feature | MySQL | SQLite | PostgreSQL | SQL Server | Oracle | MS Access |
|---------|-------|--------|------------|------------|--------|-----------|
| `CREATE VIEW` | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `CREATE OR REPLACE VIEW` | ✅ | ❌ drop then create | ✅ | ❌ `ALTER VIEW` | ✅ | ❌ |
| Updatable view | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Materialized view | ❌ | ❌ | ✅ | ⚠️ Indexed Views | ✅ | ❌ |

---

## 10. ⚙️ Stored Procedures & Functions

> Reusable, named blocks of SQL logic.

---

### Stored Procedure (MySQL)
```sql
DELIMITER //

CREATE PROCEDURE give_raise(
  IN  p_dept_id   INT,
  IN  p_pct       DECIMAL(5,2),
  OUT p_affected  INT
)
BEGIN
  UPDATE employees
  SET salary = salary * (1 + p_pct / 100)
  WHERE dept_id = p_dept_id;

  SET p_affected = ROW_COUNT();
END //

DELIMITER ;

-- Call it
CALL give_raise(3, 10, @rows);
SELECT @rows AS rows_updated;
```

### Stored Function (MySQL)
```sql
DELIMITER //

CREATE FUNCTION annual_salary(monthly DECIMAL(10,2))
RETURNS DECIMAL(12,2)
DETERMINISTIC
BEGIN
  RETURN monthly * 12;
END //

DELIMITER ;

-- Use it in a query
SELECT name, annual_salary(salary) AS yearly FROM employees;
```

### Cross-Engine Compatibility — Procedures & Functions

| Feature | MySQL | SQLite | PostgreSQL | SQL Server | Oracle | MS Access |
|---------|-------|--------|------------|------------|--------|-----------|
| Stored Procedures | ✅ | ❌ | ✅ | ✅ | ✅ | ❌ |
| User-Defined Functions | ✅ | ❌ | ✅ | ✅ | ✅ | ✅ VBA |
| `DELIMITER` change | ✅ | ❌ | ❌ uses `$$` | ❌ uses `GO` | ❌ | ❌ |
| `CALL` to execute | ✅ | ❌ | ✅ `CALL` or `SELECT` | ⚠️ `EXEC` | ⚠️ `EXEC` | ❌ |

---

## 11. ⚡ Triggers

> Automatically execute SQL on INSERT / UPDATE / DELETE events.

---

```sql
-- Audit log trigger: record salary changes
CREATE TABLE salary_audit (
  id          INT AUTO_INCREMENT PRIMARY KEY,
  employee_id INT,
  old_salary  DECIMAL(10,2),
  new_salary  DECIMAL(10,2),
  changed_at  DATETIME DEFAULT CURRENT_TIMESTAMP,
  changed_by  VARCHAR(100)
);

DELIMITER //

CREATE TRIGGER trg_salary_audit
AFTER UPDATE ON employees
FOR EACH ROW
BEGIN
  IF OLD.salary <> NEW.salary THEN
    INSERT INTO salary_audit (employee_id, old_salary, new_salary, changed_by)
    VALUES (OLD.id, OLD.salary, NEW.salary, CURRENT_USER());
  END IF;
END //

DELIMITER ;

-- Drop trigger
DROP TRIGGER IF EXISTS trg_salary_audit;
```

### Trigger Timing Options

| Timing | MySQL | PostgreSQL | SQL Server | Oracle |
|--------|-------|------------|------------|--------|
| `BEFORE INSERT` | ✅ | ✅ | ✅ `INSTEAD OF` on views | ✅ |
| `AFTER INSERT` | ✅ | ✅ | ✅ | ✅ |
| `BEFORE UPDATE` | ✅ | ✅ | ✅ | ✅ |
| `AFTER UPDATE` | ✅ | ✅ | ✅ | ✅ |
| `BEFORE DELETE` | ✅ | ✅ | ✅ | ✅ |
| `AFTER DELETE` | ✅ | ✅ | ✅ | ✅ |
| `FOR EACH ROW` (row-level) | ✅ | ✅ | ✅ always row | ✅ |
| Statement-level trigger | ❌ | ✅ | ✅ | ✅ |

---

## 12. 💳 Transactions (TCL)

> Group statements into atomic units of work.

---

```sql
-- Begin a transaction
START TRANSACTION;           -- MySQL, PostgreSQL, SQLite
-- BEGIN;                    -- also valid in PostgreSQL / SQLite
-- BEGIN TRANSACTION;        -- SQL Server / SQLite

-- Make changes
UPDATE accounts SET balance = balance - 500 WHERE id = 1;
UPDATE accounts SET balance = balance + 500 WHERE id = 2;

-- Commit if all good
COMMIT;

-- Roll back on error
ROLLBACK;

-- Savepoints (partial rollback)
SAVEPOINT sp1;
  UPDATE products SET stock = stock - 1 WHERE id = 10;
SAVEPOINT sp2;
  UPDATE orders SET status = 'processed' WHERE id = 99;

ROLLBACK TO SAVEPOINT sp1;   -- undo back to sp1, keep nothing after it
RELEASE SAVEPOINT sp1;       -- discard savepoint (don't rollback, just clean up)
```

### Isolation Levels
```sql
SET TRANSACTION ISOLATION LEVEL READ COMMITTED;
SET TRANSACTION ISOLATION LEVEL REPEATABLE READ;    -- MySQL default
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;
SET TRANSACTION ISOLATION LEVEL READ UNCOMMITTED;
```

### Cross-Engine Compatibility — Transactions

| Feature | MySQL | SQLite | PostgreSQL | SQL Server | Oracle | MS Access |
|---------|-------|--------|------------|------------|--------|-----------|
| `START TRANSACTION` | ✅ | ⚠️ `BEGIN` | ✅ `BEGIN` | ⚠️ `BEGIN TRANSACTION` | ⚠️ implicit | ❌ |
| `COMMIT` | ✅ | ✅ | ✅ | ✅ | ✅ | ❌ |
| `ROLLBACK` | ✅ | ✅ | ✅ | ✅ | ✅ | ❌ |
| `SAVEPOINT` | ✅ | ✅ | ✅ | ✅ | ✅ | ❌ |
| Autocommit by default | ✅ ON | ✅ ON | ✅ ON | ✅ ON | ❌ OFF | ✅ ON |

---

## 13. 🔑 DCL — Data Control Language

> Manage permissions and access.

---

```sql
-- Create a user
CREATE USER 'alice'@'localhost' IDENTIFIED BY 'str0ngP@ss!';
CREATE USER 'app_user'@'%' IDENTIFIED BY 'appP@ss!';   -- any host

-- Grant privileges
GRANT SELECT, INSERT, UPDATE ON shop.employees TO 'alice'@'localhost';
GRANT ALL PRIVILEGES ON shop.* TO 'app_user'@'%';
GRANT SELECT ON shop.* TO 'readonly_user'@'%';

-- Revoke privileges
REVOKE INSERT, UPDATE ON shop.employees FROM 'alice'@'localhost';

-- Show grants for a user
SHOW GRANTS FOR 'alice'@'localhost';

-- Drop a user
DROP USER 'alice'@'localhost';

-- Apply privilege changes
FLUSH PRIVILEGES;
```

### Cross-Engine Compatibility — DCL

| Statement | MySQL | SQLite | PostgreSQL | SQL Server | Oracle | MS Access |
|-----------|-------|--------|------------|------------|--------|-----------|
| `CREATE USER` | ✅ | ❌ file-level security | ✅ | ✅ | ✅ | ❌ |
| `GRANT` | ✅ | ❌ | ✅ | ✅ | ✅ | ❌ |
| `REVOKE` | ✅ | ❌ | ✅ | ✅ | ✅ | ❌ |
| `SHOW GRANTS` | ✅ | ❌ | ⚠️ `\du` in psql / `pg_roles` table | ⚠️ `sys.database_permissions` | ⚠️ `DBA_SYS_PRIVS` | ❌ |

---

## 14. 📐 Useful Patterns

---

### Upsert — Insert or Update
```sql
-- MySQL
INSERT INTO products (sku, name, price) VALUES ('X1', 'Widget', 9.99)
ON DUPLICATE KEY UPDATE price = VALUES(price), name = VALUES(name);

-- PostgreSQL
INSERT INTO products (sku, name, price) VALUES ('X1', 'Widget', 9.99)
ON CONFLICT (sku) DO UPDATE SET price = EXCLUDED.price, name = EXCLUDED.name;

-- SQL Server / Oracle
MERGE INTO products AS target
USING (SELECT 'X1' AS sku, 'Widget' AS name, 9.99 AS price) AS src
ON target.sku = src.sku
WHEN MATCHED     THEN UPDATE SET price = src.price, name = src.name
WHEN NOT MATCHED THEN INSERT (sku, name, price) VALUES (src.sku, src.name, src.price);
```

### Pagination (all engines)
```sql
-- MySQL / PostgreSQL / SQLite
SELECT * FROM products ORDER BY id LIMIT 10 OFFSET 30;  -- page 4

-- SQL Server
SELECT * FROM products ORDER BY id
OFFSET 30 ROWS FETCH NEXT 10 ROWS ONLY;

-- Oracle 12c+
SELECT * FROM products ORDER BY id
OFFSET 30 ROWS FETCH NEXT 10 ROWS ONLY;

-- Oracle 11g and older
SELECT * FROM (
  SELECT p.*, ROWNUM rn FROM products p WHERE ROWNUM <= 40
) WHERE rn > 30;
```

### Copy Table Structure Only
```sql
-- MySQL
CREATE TABLE employees_copy LIKE employees;

-- PostgreSQL
CREATE TABLE employees_copy (LIKE employees INCLUDING ALL);

-- SQL Server
SELECT TOP 0 * INTO employees_copy FROM employees;
```

### Find Duplicates
```sql
SELECT email, COUNT(*) AS cnt
FROM users
GROUP BY email
HAVING COUNT(*) > 1;
```

### Delete Duplicates — Keep Lowest ID
```sql
DELETE FROM users
WHERE id NOT IN (
  SELECT MIN(id) FROM users GROUP BY email
);
```

### Pivot — Rows to Columns
```sql
SELECT
  dept_id,
  SUM(CASE WHEN MONTH(hire_date) = 1  THEN 1 ELSE 0 END) AS jan,
  SUM(CASE WHEN MONTH(hire_date) = 2  THEN 1 ELSE 0 END) AS feb,
  SUM(CASE WHEN MONTH(hire_date) = 3  THEN 1 ELSE 0 END) AS mar
FROM employees
GROUP BY dept_id;
```

### Running Total
```sql
SELECT
  order_date,
  amount,
  SUM(amount) OVER (ORDER BY order_date ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) AS running_total
FROM orders;
```

### Lag / Lead — Compare to Previous Row
```sql
SELECT
  month,
  revenue,
  LAG(revenue, 1)  OVER (ORDER BY month) AS prev_month,
  revenue - LAG(revenue, 1) OVER (ORDER BY month) AS change,
  ROUND(
    (revenue - LAG(revenue, 1) OVER (ORDER BY month))
    / LAG(revenue, 1) OVER (ORDER BY month) * 100, 2
  ) AS pct_change
FROM monthly_revenue;
```

### Recursive: Generate a Date Range
```sql
WITH RECURSIVE date_range AS (
  SELECT '2025-01-01' AS dt
  UNION ALL
  SELECT DATE_ADD(dt, INTERVAL 1 DAY)
  FROM date_range
  WHERE dt < '2025-01-31'
)
SELECT dt FROM date_range;
```

### Conditional Update Based on Another Table
```sql
UPDATE employees e
JOIN departments d ON e.dept_id = d.id
SET e.salary = e.salary * CASE
  WHEN d.name = 'Engineering' THEN 1.15
  WHEN d.name = 'Sales'       THEN 1.10
  ELSE 1.05
END;
```

---

## Quick Reference Card

| Category | Key Statements |
|----------|---------------|
| **DDL** | `CREATE`, `ALTER`, `DROP`, `TRUNCATE`, `RENAME` |
| **DML** | `INSERT`, `UPDATE`, `DELETE`, `REPLACE`, `MERGE` |
| **DQL** | `SELECT`, `FROM`, `WHERE`, `GROUP BY`, `HAVING`, `ORDER BY`, `LIMIT` |
| **Joins** | `INNER`, `LEFT`, `RIGHT`, `FULL OUTER`, `CROSS`, `SELF` |
| **Subqueries** | Scalar, Derived table, `EXISTS`, `IN`, CTE (`WITH`), Recursive CTE |
| **Window** | `OVER()`, `PARTITION BY`, `ROWS BETWEEN` |
| **TCL** | `START TRANSACTION`, `COMMIT`, `ROLLBACK`, `SAVEPOINT` |
| **DCL** | `GRANT`, `REVOKE`, `CREATE USER`, `DROP USER` |
| **Objects** | `CREATE VIEW`, `CREATE INDEX`, `CREATE PROCEDURE`, `CREATE TRIGGER` |

---

*Syntax primarily shown for MySQL 8.x. Engine-specific alternatives noted throughout.*
