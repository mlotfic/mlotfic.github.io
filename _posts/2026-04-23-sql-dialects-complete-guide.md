---
layout: post
cover_color: #000000

keywords: SQL, Dialects, T-SQL, PL/SQL, PL/pgSQL, MySQL, SQLite, PostgreSQL, SQL Server, Oracle, MS Access, ANSI SQL, SQL Functions, SQL Syntax, SQL Features, SQL Comparison, SQL Learning, SQL Cheatsheet, SQL Reference, SQL Tutorial, SQL Guide, SQL Best Practices, SQL Common Mistakes, SQL Pros and Cons, SQL When It Matters, SQL How to Learn, SQL 80% Never Changes, SQL Dialects Complete Guide, SQL Dialects T-SQL, SQL Dialects PL/SQL, SQL Dialects PL/pgSQL, SQL Dialects MySQL, SQL Dialects SQLite, SQL Dialects PostgreSQL, SQL Dialects SQL Server, SQL Dialects Oracle, SQL Dialects MS Access, SQL Dialects ANSI SQL, SQL Dialects SQL Functions, SQL Dialects SQL Syntax, SQL Dialects SQL Features, SQL Dialects SQL Comparison, SQL Dialects SQL Learning, SQL Dialects SQL Cheatsheet, SQL Dialects SQL Reference, SQL Dialects SQL Tutorial, SQL Dialects SQL Guide, SQL Dialects SQL Best Practices, SQL Dialects SQL Common Mistakes, SQL Dialects SQL Pros and Cons, SQL Dialects SQL When It Matters, SQL Dialects SQL How to Learn, SQL Dialects SQL 80% Never Changes, SQL Dialects Complete Guide with Examples, SQL Dialects Complete Guide with Examples Based on Lucky Shrub Gardening Center Use Cases

title: SQL Dialects — T-SQL, PL/SQL, PL/pgSQL and More

description: >-
    A calm, honest guide to all SQL "flavors" — what they are, who uses them, when they matter, and why they're not as scary as they sound. Covers T-SQL, PL/SQL, PL/pgSQL, MySQL, SQLite, PostgreSQL, SQL Server, Oracle, MS Access, ANSI SQL, SQL Functions, SQL Syntax, SQL Features, SQL Comparison, SQL Learning, SQL Cheatsheet, SQL Reference, SQL Tutorial, SQL Guide, SQL Best Practices, SQL Common Mistakes, SQL Pros and Cons, SQL When It Matters, SQL How to Learn, SQL 80% Never Changes, SQL Dialects Complete Guide, SQL Dialects T-SQL, SQL Dialects PL/SQL, SQL Dialects PL/pgSQL, SQL Dialects MySQL, SQL Dialects SQLite, SQL Dialects PostgreSQL, SQL Dialects SQL Server, SQL Dialects Oracle, SQL Dialects MS Access, SQL Dialects ANSI SQL, SQL Dialects SQL Functions, SQL Dialects SQL Syntax, SQL Dialects SQL Features, SQL Dialects SQL Comparison, SQL Dialects SQL Learning, SQL Dialects SQL Cheatsheet, SQL Dialects SQL Reference, SQL Dialects SQL Tutorial, SQL Dialects SQL Guide, SQL Dialects SQL Best Practices, SQL Dialects SQL Common Mistakes, SQL Dialects SQL Pros and Cons, SQL Dialects SQL When It Matters, SQL Dialects SQL How to Learn, SQL Dialects SQL 80% Never Changes, SQL Dialects Complete Guide with Examples, SQL Dialects Complete Guide with Examples Based on Lucky Shrub Gardening Center Use Cases

date: 2026-04-23 10:00:00 +0800
author: Mahmoud Lotfi
file_name: 2026-04-23-sql-dialects-complete-guide.md
categories: [SQL, Dialects, T-SQL, PL/SQL, PL/pgSQL, MySQL, SQLite, PostgreSQL, SQL Server, Oracle, MS Access, ANSI SQL, SQL Functions, SQL Syntax, SQL Features, SQL Comparison, SQL Learning, SQL Cheatsheet, SQL Reference, SQL Tutorial, SQL Guide, SQL Best Practices, SQL Common Mistakes, SQL Pros and Cons, SQL When It Matters, SQL How to Learn, SQL 80% Never Changes, SQL Dialects Complete Guide, SQL Dialects T-SQL, SQL Dialects PL/SQL, SQL Dialects PL/pgSQL, SQL Dialects MySQL, SQL Dialects SQLite, SQL Dialects PostgreSQL, SQL Dialects SQL Server, SQL Dialects Oracle, SQL Dialects MS Access, SQL Dialects ANSI SQL, SQL Dialects SQL Functions, SQL Dialects SQL Syntax, SQL Dialects SQL Features, SQL Dialects SQL Comparison, SQL Dialects SQL Learning, SQL Dialects SQL Cheatsheet, SQL Dialects SQL Reference, SQL Dialects SQL Tutorial, SQL Dialects SQL Guide, SQL Dialects SQL Best Practices, SQL Dialects SQL Common Mistakes, SQL Dialects SQL Pros and Cons, SQL Dialects SQL When It Matters, SQL Dialects SQL How to Learn, SQL Dialects SQL 80% Never Changes, SQL Dialects Complete Guide with Examples, SQL Dialects Complete Guide with Examples Based on Lucky Shrub Gardening Center Use Cases]
pin: False
math: true
mermaid: true
comments: true
toc: true
render_with_liquid: false

image:
  path: /assets/img/posts/sql.jpg
  alt: SQL Dialects — T-SQL, PL/SQL, PL/pgSQL and More
  lqip: data:image/webp;base64,UklGRjoAAABXRUJQVlA4IC4AAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA

---

## First — A Word Before We Start

If someone made you feel like you're behind because you "only know SQL" —
**they were wrong.**

Here is the truth:

```
SQL is SQL.
The dialects are just accents of the same language.

If you speak English, you can understand someone from London,
New York, Sydney, and Cairo — even if they say things slightly differently.

SQL dialects work the same way.
MySQL, T-SQL, PL/SQL — they all share 80% identical syntax.
The differences are in the remaining 20%.
And that 20% is something you learn in a few days, not years.
```

Every senior developer who "shows off" with T-SQL or PL/SQL started exactly
where you are. They just used a specific database engine long enough to
learn its quirks.

---

## Table of Contents
1. [What Is a SQL Dialect?](#1-what-is-a-sql-dialect)
2. [The Standard — ANSI SQL](#2-the-standard--ansi-sql)
3. [T-SQL — Transact-SQL (SQL Server & Azure)](#3-t-sql--transact-sql-sql-server--azure)
4. [PL/SQL — Oracle](#4-plsql--oracle)
5. [PL/pgSQL — PostgreSQL](#5-plpgsql--postgresql)
6. [MySQL SQL — MySQL & MariaDB](#6-mysql-sql--mysql--mariadb)
7. [SQLite](#7-sqlite)
8. [Side-by-Side Comparison — Same Task, Every Dialect](#8-side-by-side-comparison--same-task-every-dialect)
9. [Who Talks About Which Dialect — and Where](#9-who-talks-about-which-dialect--and-where)
10. [When Does the Dialect Actually Matter?](#10-when-does-the-dialect-actually-matter)
11. [Pros & Cons of Each](#11-pros--cons-of-each)
12. [How to Learn a New Dialect Quickly](#12-how-to-learn-a-new-dialect-quickly)
13. [The 80% That Never Changes](#13-the-80-that-never-changes)

---

## 1. What Is a SQL Dialect?

**SQL (Structured Query Language)** is the universal language for databases.
It was standardized by ANSI (American National Standards Institute) so that, in theory, every database speaks the same language.

In practice, every database vendor **extended** the standard with their own extra features, syntax shortcuts, and built-in functions. These extensions became their **dialect**.

```
Analogy: Human languages

Standard English  →  ANSI SQL
─────────────────────────────────────────────────────────────
British English   →  T-SQL      (Microsoft SQL Server)
American English  →  PL/SQL     (Oracle)
Australian English →  PL/pgSQL  (PostgreSQL)
Egyptian Arabic   →  MySQL SQL  (MySQL / MariaDB)

They share the same grammar foundations.
They differ in vocabulary, idioms, and some syntax.
Speakers of one can understand speakers of another.
Learning one makes the next one much faster.
```

### Why Did Dialects Appear?

The ANSI SQL standard evolves slowly. Database vendors needed features NOW — stored procedures, error handling, loops, variables, window functions. So each vendor added their own solutions.

Over time these became the dialect. Some of these vendor innovations were so good that later ANSI SQL standards adopted them.

---

## 2. The Standard — ANSI SQL

**What it is:** The international standard SQL specification, maintained by ANSI and ISO. Updated in versions: SQL-86, SQL-92, SQL:1999, SQL:2003, SQL:2011, SQL:2016, SQL:2023.

**Who uses pure ANSI SQL?** Almost nobody directly — but every dialect is measured against it.

**Why it matters:** If you write queries using only ANSI standard syntax, they should work on any database engine with little or no modification.

### Core ANSI SQL (works everywhere)
```sql
-- SELECT
SELECT name, salary FROM employees WHERE dept_id = 3;

-- JOIN
SELECT e.name, d.name AS dept
FROM employees e
JOIN departments d ON e.dept_id = d.id;

-- GROUP BY
SELECT dept_id, COUNT(*), AVG(salary)
FROM employees
GROUP BY dept_id
HAVING AVG(salary) > 50000;

-- Subquery
SELECT name FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);

-- CASE
SELECT name,
  CASE WHEN salary > 80000 THEN 'Senior' ELSE 'Junior' END AS level
FROM employees;
```

All of the above work identically in MySQL, SQL Server, PostgreSQL, Oracle, and SQLite.
**This is the foundation. Master this and you already speak every dialect.**

---

## 3. T-SQL — Transact-SQL (SQL Server & Azure)

### What Is It?
T-SQL (Transact-SQL) is Microsoft's extension of SQL, used in:
- **Microsoft SQL Server** (on-premise)
- **Azure SQL Database** (Microsoft's cloud database)
- **Azure Synapse Analytics** (big data / analytics)

### Who Uses It?
```
✅ Enterprise companies running Windows/.NET ecosystems
✅ Banks, insurance companies, government agencies on Microsoft stack
✅ Business Intelligence teams using SSRS, SSAS, Power BI
✅ .NET / C# developers who need SQL in Microsoft environments
✅ Companies using SharePoint or Dynamics 365 (they run on SQL Server)
```

### Signature T-SQL Features

#### Variables — `@` prefix, `DECLARE` before use
```sql
-- Declare and use variables
DECLARE @employee_id INT = 5;
DECLARE @full_name   NVARCHAR(100);

SELECT @full_name = CONCAT(first_name, ' ', last_name)
FROM employees
WHERE id = @employee_id;

PRINT @full_name;           -- prints to messages pane
SELECT @full_name AS name;  -- returns as result set
```

#### Conditional Logic — `IF … ELSE`
```sql
DECLARE @salary DECIMAL(10,2) = 75000;

IF @salary > 80000
    PRINT 'Senior level';
ELSE IF @salary > 50000
    PRINT 'Mid level';
ELSE
    PRINT 'Junior level';
```

#### Error Handling — `TRY … CATCH`
```sql
BEGIN TRY
    INSERT INTO orders (customer_id, amount)
    VALUES (999, 500.00);                 -- customer 999 might not exist
    PRINT 'Order inserted successfully';
END TRY
BEGIN CATCH
    PRINT 'Error: ' + ERROR_MESSAGE();
    PRINT 'Error number: ' + CAST(ERROR_NUMBER() AS VARCHAR);
END CATCH;
```

#### Stored Procedure
```sql
CREATE PROCEDURE get_employee_by_dept
    @dept_id    INT,
    @min_salary DECIMAL(10,2) = 0        -- default value
AS
BEGIN
    SET NOCOUNT ON;                      -- suppress "rows affected" messages

    SELECT id, name, salary
    FROM employees
    WHERE dept_id = @dept_id
      AND salary >= @min_salary
    ORDER BY salary DESC;
END;
GO

-- Call it
EXEC get_employee_by_dept @dept_id = 3, @min_salary = 50000;
```

#### TOP instead of LIMIT
```sql
-- T-SQL does NOT use LIMIT
SELECT TOP 10 * FROM employees ORDER BY salary DESC;

-- Or with OFFSET for pagination
SELECT * FROM employees
ORDER BY salary DESC
OFFSET 20 ROWS FETCH NEXT 10 ROWS ONLY;
```

#### String Functions (different names)
```sql
-- T-SQL specific string functions
SELECT LEN('hello');                     -- length (MySQL uses LENGTH())
SELECT SUBSTRING('hello world', 1, 5);   -- same as MySQL
SELECT CHARINDEX('@', email);            -- find position (MySQL uses INSTR())
SELECT ISNULL(phone, 'N/A');            -- replace NULL (MySQL uses IFNULL())
SELECT FORMAT(salary, 'N2');            -- format number with 2 decimals
SELECT GETDATE();                        -- current date/time (MySQL: NOW())
SELECT DATEADD(DAY, 7, GETDATE());      -- add 7 days (MySQL: DATE_ADD())
SELECT DATEDIFF(DAY, start_dt, end_dt); -- days between (MySQL: DATEDIFF())
```

#### Temporary Tables
```sql
-- Local temp table (# prefix) — only visible in current session
CREATE TABLE #temp_employees (
    id   INT,
    name VARCHAR(100)
);

INSERT INTO #temp_employees
SELECT id, name FROM employees WHERE dept_id = 3;

SELECT * FROM #temp_employees;
DROP TABLE #temp_employees;

-- Global temp table (## prefix) — visible to all sessions
CREATE TABLE ##global_temp ( id INT, name VARCHAR(100) );
```

#### CTE (same as standard, just common in T-SQL world)
```sql
WITH dept_summary AS (
    SELECT dept_id, COUNT(*) AS cnt, AVG(salary) AS avg_sal
    FROM employees
    GROUP BY dept_id
)
SELECT d.name, ds.cnt, ds.avg_sal
FROM departments d
JOIN dept_summary ds ON ds.dept_id = d.id;
```

### T-SQL Specific Keywords

| T-SQL | Standard / MySQL equivalent |
|-------|----------------------------|
| `TOP n` | `LIMIT n` |
| `GETDATE()` | `NOW()` |
| `ISNULL(x, y)` | `IFNULL(x, y)` or `COALESCE(x, y)` |
| `LEN()` | `LENGTH()` or `CHAR_LENGTH()` |
| `CHARINDEX()` | `LOCATE()` or `INSTR()` |
| `DATEADD()` | `DATE_ADD()` |
| `DATEDIFF()` | `DATEDIFF()` (same name, different arg order!) |
| `PRINT` | `SELECT` (no PRINT in MySQL) |
| `GO` | `;` (batch separator, not needed in MySQL) |
| `NVARCHAR` | `VARCHAR` (Unicode by default in MySQL utf8mb4) |
| `EXEC` / `EXECUTE` | `CALL` |
| `##temp_table` | No direct equivalent |
| `IDENTITY(1,1)` | `AUTO_INCREMENT` |

---

## 4. PL/SQL — Oracle

### What Is It?
PL/SQL (Procedural Language / SQL) is Oracle's extension. The most powerful and feature-rich dialect. Used in:
- **Oracle Database** (on-premise, typically large enterprise)
- **Oracle Cloud** (cloud version)

### Who Uses It?
```
✅ Large enterprises with Oracle licenses (banks, telecoms, hospitals)
✅ ERP systems running on Oracle (Oracle E-Business Suite, SAP on Oracle)
✅ Government and military systems in many countries
✅ Data warehouses on Oracle Exadata
✅ Senior DBAs and Oracle-certified professionals
```

### Signature PL/SQL Features

#### Anonymous Block Structure
PL/SQL uses a unique `BEGIN … END` block structure even for ad-hoc code:
```sql
-- Every PL/SQL block has: DECLARE, BEGIN, EXCEPTION, END
DECLARE
    v_salary    NUMBER(10,2);      -- variable declaration
    v_emp_name  VARCHAR2(100);     -- VARCHAR2 is Oracle's string type
BEGIN
    SELECT salary, first_name || ' ' || last_name   -- || is string concat
    INTO v_salary, v_emp_name
    FROM employees
    WHERE id = 5;

    DBMS_OUTPUT.PUT_LINE('Employee: ' || v_emp_name);   -- Oracle's PRINT
    DBMS_OUTPUT.PUT_LINE('Salary: ' || v_salary);

EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('Employee not found');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Error: ' || SQLERRM);
END;
/                           -- / executes the block in SQL*Plus
```

#### Stored Procedure
```sql
CREATE OR REPLACE PROCEDURE give_raise(
    p_emp_id  IN  NUMBER,
    p_percent IN  NUMBER,
    p_new_sal OUT NUMBER
)
AS
    v_current_salary NUMBER(10,2);
BEGIN
    SELECT salary INTO v_current_salary
    FROM employees
    WHERE id = p_emp_id;

    p_new_sal := v_current_salary * (1 + p_percent / 100);

    UPDATE employees
    SET salary = p_new_sal
    WHERE id = p_emp_id;

    COMMIT;
EXCEPTION
    WHEN NO_DATA_FOUND THEN
        RAISE_APPLICATION_ERROR(-20001, 'Employee not found: ' || p_emp_id);
END give_raise;
/

-- Execute
DECLARE
    v_new_salary NUMBER;
BEGIN
    give_raise(5, 10, v_new_salary);
    DBMS_OUTPUT.PUT_LINE('New salary: ' || v_new_salary);
END;
/
```

#### Cursor (loop through result set row by row)
```sql
DECLARE
    CURSOR emp_cursor IS
        SELECT id, name, salary
        FROM employees
        WHERE dept_id = 3;

    v_emp emp_cursor%ROWTYPE;   -- variable matching cursor row structure
BEGIN
    OPEN emp_cursor;

    LOOP
        FETCH emp_cursor INTO v_emp;
        EXIT WHEN emp_cursor%NOTFOUND;    -- stop when no more rows

        DBMS_OUTPUT.PUT_LINE(v_emp.name || ': ' || v_emp.salary);
    END LOOP;

    CLOSE emp_cursor;
END;
/
```

### Oracle-Specific Keywords

| Oracle / PL/SQL | Standard / MySQL equivalent |
|----------------|----------------------------|
| `VARCHAR2` | `VARCHAR` |
| `NUMBER` | `DECIMAL` / `INT` |
| `SYSDATE` | `NOW()` / `CURDATE()` |
| `NVL(x, y)` | `IFNULL(x, y)` or `COALESCE(x, y)` |
| `DECODE()` | `CASE WHEN … END` |
| `ROWNUM` | `LIMIT` (old Oracle) |
| `FETCH FIRST n ROWS ONLY` | `LIMIT n` (Oracle 12c+) |
| `||` (concat) | `CONCAT()` |
| `DBMS_OUTPUT.PUT_LINE()` | `SELECT` or `PRINT` |
| `CREATE OR REPLACE` | `CREATE OR REPLACE` (same in MySQL 8+) |
| `/` (block terminator) | `;` |
| `COMMIT` / `ROLLBACK` | `COMMIT` / `ROLLBACK` (same) |
| `:=` (assignment) | `=` (in MySQL stored proc) |
| `%TYPE` / `%ROWTYPE` | No direct equivalent in MySQL |
| Sequences | `AUTO_INCREMENT` |

---

## 5. PL/pgSQL — PostgreSQL

### What Is It?
PL/pgSQL is PostgreSQL's procedural language — heavily inspired by Oracle's PL/SQL, but open source. PostgreSQL itself is known as the most standards-compliant SQL database.

### Who Uses It?
```
✅ Open-source / startup / SaaS companies
✅ GIS / spatial data teams (PostGIS runs on PostgreSQL)
✅ Python / Django developers (PostgreSQL is Django's recommended database)
✅ Data engineers building data warehouses (Redshift is based on PostgreSQL)
✅ Companies who want Oracle-level power without Oracle's license cost
✅ Cloud: Supabase, Neon, Amazon RDS PostgreSQL, Google Cloud SQL
```

### Signature PL/pgSQL Features

#### Function (PostgreSQL calls them functions, not procedures)
```sql
-- PostgreSQL uses $$ as delimiter instead of DELIMITER //
CREATE OR REPLACE FUNCTION get_tax(p_salary NUMERIC)
RETURNS NUMERIC
LANGUAGE plpgsql
AS $$
DECLARE
    v_tax NUMERIC;
BEGIN
    v_tax := p_salary * 0.20;
    RETURN v_tax;
END;
$$;

-- Call it
SELECT get_tax(5000);        -- 1000.00
SELECT get_tax(salary) AS tax FROM employees;
```

#### Error Handling
```sql
CREATE OR REPLACE FUNCTION safe_divide(a NUMERIC, b NUMERIC)
RETURNS NUMERIC
LANGUAGE plpgsql
AS $$
BEGIN
    IF b = 0 THEN
        RAISE EXCEPTION 'Division by zero is not allowed';
    END IF;
    RETURN a / b;

EXCEPTION
    WHEN division_by_zero THEN
        RAISE WARNING 'Caught division by zero';
        RETURN NULL;
END;
$$;
```

#### RETURNING clause (PostgreSQL unique feature)
```sql
-- Insert and get back the new row's ID in one statement
INSERT INTO employees (name, salary, dept_id)
VALUES ('Sara Ahmed', 72000, 3)
RETURNING id, name;           -- immediately returns the generated id
-- Output: id=15, name='Sara Ahmed'

-- Update and get back the changed values
UPDATE employees
SET salary = salary * 1.10
WHERE dept_id = 3
RETURNING id, name, salary AS new_salary;
```

#### Dollar Quoting (unique to PostgreSQL)
```sql
-- Instead of escaping quotes, PostgreSQL uses $$
SELECT $$ It's a beautiful day $$ AS message;

-- Or tagged dollar quotes for nested situations
SELECT $msg$ He said "Hello" $msg$ AS quote;
```

### PostgreSQL-Specific Keywords

| PostgreSQL | Standard / MySQL equivalent |
|-----------|----------------------------|
| `SERIAL` / `BIGSERIAL` | `AUTO_INCREMENT` |
| `GENERATED ALWAYS AS IDENTITY` | `AUTO_INCREMENT` |
| `RETURNING` | No direct equivalent in MySQL |
| `$$` delimiter | `DELIMITER //` in MySQL |
| `RAISE NOTICE` / `RAISE EXCEPTION` | `SIGNAL` in MySQL |
| `LANGUAGE plpgsql` | Not needed in MySQL |
| `::` type cast (`'5'::INT`) | `CAST('5' AS SIGNED)` |
| `ILIKE` (case-insensitive LIKE) | `LIKE` (already case-insensitive in MySQL) |
| `||` concat | `CONCAT()` |
| `EXPLAIN ANALYZE` | `EXPLAIN` |
| `CREATE SCHEMA` | `CREATE DATABASE` |
| `\copy` (import CSV) | `LOAD DATA INFILE` |

---

## 6. MySQL SQL — MySQL & MariaDB

### What Is It?
MySQL is the world's most widely deployed open-source database. MariaDB is a fork of MySQL with some additional features. Their SQL dialect is what you already know.

### Who Uses It?
```
✅ Web applications (LAMP stack: Linux, Apache, MySQL, PHP)
✅ WordPress, Joomla, Drupal — all use MySQL
✅ E-commerce platforms (Magento, WooCommerce)
✅ Any Python/PHP/Node.js web backend
✅ Cloud: Amazon RDS MySQL, Google Cloud SQL, PlanetScale
✅ You — right now
```

### What Makes MySQL Unique

```sql
-- IFNULL (instead of NVL or ISNULL)
SELECT IFNULL(phone, 'No phone') FROM users;

-- AUTO_INCREMENT
CREATE TABLE users (
  id INT NOT NULL AUTO_INCREMENT PRIMARY KEY
);

-- ON DUPLICATE KEY UPDATE (upsert)
INSERT INTO products (sku, stock)
VALUES ('ABC', 50)
ON DUPLICATE KEY UPDATE stock = stock + 50;

-- GROUP_CONCAT (aggregate strings)
SELECT dept_id,
  GROUP_CONCAT(name ORDER BY name SEPARATOR ', ') AS employee_list
FROM employees
GROUP BY dept_id;

-- DELIMITER change for procedures
DELIMITER //
CREATE PROCEDURE my_proc()
BEGIN
  SELECT 'hello';
END //
DELIMITER ;

CALL my_proc();
```

---

## 7. SQLite

### What Is It?
SQLite is a **serverless**, **file-based** database engine. The entire database lives in a single file on disk. No installation, no server process.

### Who Uses It?
```
✅ Mobile apps — Android and iOS both use SQLite internally
✅ Desktop apps — browsers (Firefox, Chrome store history in SQLite)
✅ Python scripts (sqlite3 is built into Python — zero install)
✅ Embedded systems and IoT devices
✅ Prototyping / learning / testing
✅ Any situation where "I just need a simple database in a file"
```

### SQLite Quirks

```sql
-- SQLite is very flexible with types (TYPE AFFINITY, not strict)
CREATE TABLE test (
  id   INTEGER PRIMARY KEY,   -- auto-increment is implicit for INTEGER PRIMARY KEY
  data ANY                    -- accepts any type!
);

-- Date functions use strftime
SELECT strftime('%Y-%m-%d', 'now');           -- current date
SELECT strftime('%Y', hire_date) FROM employees;  -- extract year

-- No RIGHT JOIN (use reversed LEFT JOIN instead)
-- No FULL OUTER JOIN natively
-- String concat uses || not CONCAT()
SELECT first_name || ' ' || last_name AS full_name FROM employees;

-- PRAGMA — SQLite's configuration commands
PRAGMA foreign_keys = ON;     -- enable FK enforcement (OFF by default!)
PRAGMA table_info(employees); -- show column info
PRAGMA index_list(employees); -- show indexes
```

---

## 8. Side-by-Side Comparison — Same Task, Every Dialect

### Task: Get current date and time

| Dialect | Syntax |
|---------|--------|
| MySQL | `SELECT NOW();` |
| T-SQL | `SELECT GETDATE();` |
| Oracle | `SELECT SYSDATE FROM DUAL;` |
| PostgreSQL | `SELECT NOW();` or `SELECT CURRENT_TIMESTAMP;` |
| SQLite | `SELECT datetime('now');` |

---

### Task: Get first 5 rows ordered by salary

| Dialect | Syntax |
|---------|--------|
| MySQL | `SELECT * FROM employees ORDER BY salary DESC LIMIT 5;` |
| T-SQL | `SELECT TOP 5 * FROM employees ORDER BY salary DESC;` |
| Oracle (12c+) | `SELECT * FROM employees ORDER BY salary DESC FETCH FIRST 5 ROWS ONLY;` |
| Oracle (old) | `SELECT * FROM (SELECT * FROM employees ORDER BY salary DESC) WHERE ROWNUM <= 5;` |
| PostgreSQL | `SELECT * FROM employees ORDER BY salary DESC LIMIT 5;` |
| SQLite | `SELECT * FROM employees ORDER BY salary DESC LIMIT 5;` |

---

### Task: Replace NULL with a default value

| Dialect | Syntax |
|---------|--------|
| MySQL | `SELECT IFNULL(phone, 'N/A') FROM users;` |
| T-SQL | `SELECT ISNULL(phone, 'N/A') FROM users;` |
| Oracle | `SELECT NVL(phone, 'N/A') FROM users;` |
| PostgreSQL | `SELECT COALESCE(phone, 'N/A') FROM users;` |
| SQLite | `SELECT COALESCE(phone, 'N/A') FROM users;` |
| **All dialects** | `SELECT COALESCE(phone, 'N/A') FROM users;` ← this works everywhere |

---

### Task: Auto-increment primary key

| Dialect | Syntax |
|---------|--------|
| MySQL | `id INT NOT NULL AUTO_INCREMENT PRIMARY KEY` |
| T-SQL | `id INT IDENTITY(1,1) PRIMARY KEY` |
| Oracle | `id NUMBER GENERATED ALWAYS AS IDENTITY PRIMARY KEY` |
| PostgreSQL | `id SERIAL PRIMARY KEY` or `id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY` |
| SQLite | `id INTEGER PRIMARY KEY` (implicit autoincrement) |

---

### Task: Simple stored procedure

| Dialect | Syntax style |
|---------|-------------|
| MySQL | `DELIMITER // … CREATE PROCEDURE … BEGIN … END // DELIMITER ;` then `CALL` |
| T-SQL | `CREATE PROCEDURE … AS BEGIN … END` then `EXEC` |
| Oracle | `CREATE OR REPLACE PROCEDURE … AS BEGIN … END; /` then anonymous block |
| PostgreSQL | `CREATE OR REPLACE FUNCTION … LANGUAGE plpgsql AS $$ … $$` then `SELECT` |
| SQLite | ❌ No stored procedures |

---

### Task: String concatenation

| Dialect | Syntax |
|---------|--------|
| MySQL | `CONCAT(first_name, ' ', last_name)` |
| T-SQL | `first_name + ' ' + last_name` or `CONCAT(first_name, ' ', last_name)` |
| Oracle | `first_name \|\| ' ' \|\| last_name` |
| PostgreSQL | `first_name \|\| ' ' \|\| last_name` or `CONCAT(...)` |
| SQLite | `first_name \|\| ' ' \|\| last_name` |

---

## 9. Who Talks About Which Dialect — and Where

### When someone says "T-SQL"
```
They work in → Microsoft SQL Server, Azure SQL, Power BI, SSRS
They probably → work in finance, enterprise, government, .NET shops
LinkedIn keywords → SSMS, SSRS, SSIS, Azure Data Factory, Power BI
Job titles → DBA, BI Developer, Data Analyst (Microsoft stack)
```

### When someone says "PL/SQL"
```
They work in → Oracle Database, Oracle Cloud, Oracle ERP
They probably → work in large enterprises, banks, telecoms, legacy systems
LinkedIn keywords → Oracle Certified, SQL*Plus, Oracle Apex, Toad
Job titles → Oracle DBA, Oracle Developer, Senior Database Engineer
```

### When someone says "PL/pgSQL" or just "Postgres"
```
They work in → PostgreSQL, Amazon RDS, Supabase, Neon, Heroku
They probably → work in startups, SaaS, open source, Python shops
LinkedIn keywords → PostGIS, pgAdmin, Django, SQLAlchemy, dbt
Job titles → Data Engineer, Backend Developer, GIS Developer
```

### When someone says "MySQL"
```
They work in → Web applications, LAMP stack, WordPress sites
They probably → work in web development, e-commerce, SMEs
LinkedIn keywords → PHP, Laravel, WordPress, WAMP, XAMPP
Job titles → Web Developer, Full Stack Developer, Backend Developer
```

### The reality in enterprise Egypt and Middle East
```
Utility companies, government, banks → Oracle or SQL Server (T-SQL or PL/SQL)
Startups, tech companies           → PostgreSQL or MySQL
Web agencies                       → MySQL mostly
Data engineers (like you)          → MySQL + PostgreSQL + cloud SQL
```

---

## 10. When Does the Dialect Actually Matter?

### It DOES matter when:

```
✅ You're writing stored procedures and functions
   → Syntax for DECLARE, error handling, loops differ significantly

✅ You're handling dates and times
   → Every dialect has different function names

✅ You're doing pagination (LIMIT vs TOP vs FETCH FIRST)

✅ You're concatenating strings
   → CONCAT() vs || vs +

✅ You're handling NULLs
   → IFNULL vs ISNULL vs NVL vs COALESCE

✅ You're using auto-increment / identity columns

✅ You're using database-specific features
   → T-SQL: temp tables, MERGE
   → Oracle: sequences, ROWNUM, CONNECT BY
   → PostgreSQL: RETURNING, GiST indexes, PostGIS
```

### It does NOT matter when:

```
❌ Writing basic SELECT, FROM, WHERE, GROUP BY, HAVING, ORDER BY
   → 100% identical across all dialects

❌ Writing JOINs (INNER, LEFT, RIGHT, FULL OUTER)
   → Same everywhere (except SQLite has no RIGHT JOIN)

❌ Writing subqueries and CTEs
   → Same everywhere (CTEs require MySQL 8.0+, SQL Server 2005+)

❌ Using aggregate functions COUNT, SUM, AVG, MIN, MAX
   → Same everywhere

❌ Using CASE WHEN
   → Same everywhere

❌ Using standard window functions (ROW_NUMBER, RANK, LAG, LEAD)
   → Same everywhere (MySQL 8.0+, others for years)

❌ Designing schemas (CREATE TABLE, constraints, indexes)
   → Mostly the same, with minor differences in column type names
```

**Conclusion**: The vast majority of daily SQL work uses syntax that is identical across all dialects. Dialects matter most when you go deep into procedural programming (loops, error handling, dynamic SQL).

---

## 11. Pros & Cons of Each

### T-SQL (SQL Server)

| ✅ Pros | ❌ Cons |
|---------|---------|
| Excellent GUI tools (SSMS — free) | Expensive license for SQL Server Enterprise |
| Deep integration with Microsoft ecosystem | Windows-centric (Linux support is newer) |
| Strong BI/reporting tools (SSRS, SSIS) | Azure cloud costs can be high |
| Good error handling with TRY/CATCH | Vendor lock-in to Microsoft |
| Temp tables are very practical | LIMIT syntax is more verbose |
| Wide enterprise adoption | Less popular in open-source world |

---

### PL/SQL (Oracle)

| ✅ Pros | ❌ Cons |
|---------|---------|
| Most feature-rich procedural SQL | Extremely expensive licensing |
| Best performance for huge datasets | Steep learning curve |
| Mature, battle-tested in enterprise | Heavy, complex to set up and maintain |
| Excellent for complex business logic | Less relevant in modern cloud/startup world |
| Oracle certifications are well-respected | Declining market share vs PostgreSQL |
| Strong cursor and collection support | Syntax is verbose and old-fashioned |

---

### PL/pgSQL (PostgreSQL)

| ✅ Pros | ❌ Cons |
|---------|---------|
| Free and open source | Harder to set up for beginners vs MySQL |
| Most ANSI-standards compliant | Fewer GUI tools vs SQL Server |
| Excellent for spatial data (PostGIS) | `$$` dollar-quoting looks odd at first |
| Best for complex queries | Less corporate enterprise support |
| RETURNING clause is very useful | Configuration can be complex |
| Growing fast — huge community | |
| Best dbt integration | |

---

### MySQL SQL

| ✅ Pros | ❌ Cons |
|---------|---------|
| Easiest to install and learn | Less strict than PostgreSQL |
| Massive community and tutorials | Weaker procedural language than Oracle/PG |
| Free (Community Edition) | Some ANSI features came late (CTEs in 8.0) |
| Best web ecosystem (PHP, WordPress) | MyISAM engine has no transactions |
| Excellent cloud support (RDS, etc.) | Oracle ownership (some distrust) |
| Fast for read-heavy workloads | Less powerful for analytics vs PostgreSQL |

---

### SQLite

| ✅ Pros | ❌ Cons |
|---------|---------|
| Zero setup — just a file | No stored procedures |
| Built into Python (no install) | Not for multi-user / high concurrency |
| Extremely lightweight | No RIGHT JOIN or FULL OUTER JOIN |
| Perfect for learning and prototyping | No user management / permissions |
| Used in mobile apps (Android/iOS) | Not suitable for production web apps |
| No server process needed | FK enforcement is OFF by default |

---

## 12. How to Learn a New Dialect Quickly

If you know MySQL and need to work in T-SQL or PostgreSQL:

### Step 1 — Accept that 80% is already done
You don't learn a new language. You learn ~20% new vocabulary.

### Step 2 — Make a cheat sheet of the 10 key differences
```
For MySQL → T-SQL:
  NOW()       →  GETDATE()
  LIMIT n     →  TOP n  or  FETCH FIRST n ROWS ONLY
  IFNULL()    →  ISNULL()
  LENGTH()    →  LEN()
  INSTR()     →  CHARINDEX()
  CALL proc   →  EXEC proc
  CONCAT()    →  + operator or CONCAT()
  DATE_ADD()  →  DATEADD()
  AUTO_INCREMENT → IDENTITY(1,1)
  DELIMITER   →  GO (for batch separation, optional)
```

### Step 3 — Run your existing queries and fix errors
Take a query you know works in MySQL. Run it in SQL Server. Fix each error as it comes up. Each fix teaches you one dialect difference.

### Step 4 — Learn the procedural extensions for that engine
This is where dialects diverge most. Spend 2-3 days on:
- Variable declaration syntax
- IF/ELSE and LOOP syntax
- Error handling (TRY/CATCH vs EXCEPTION)
- How to write a stored procedure

### Step 5 — Use it in a real project
Nothing cements knowledge like building something real.

---

## 13. The 80% That Never Changes

This is what you already know that works in EVERY dialect:

```sql
-- ✅ Works in MySQL, SQL Server, Oracle, PostgreSQL, SQLite

-- Selecting data
SELECT col1, col2, col3 FROM table_name;
SELECT DISTINCT col FROM table;
SELECT * FROM table WHERE col = 'value';
SELECT * FROM table WHERE col BETWEEN 10 AND 50;
SELECT * FROM table WHERE col IN ('a', 'b', 'c');
SELECT * FROM table WHERE col LIKE '%pattern%';
SELECT * FROM table WHERE col IS NULL;
SELECT * FROM table ORDER BY col DESC;

-- Aggregation
SELECT dept_id, COUNT(*), SUM(sal), AVG(sal), MIN(sal), MAX(sal)
FROM employees
GROUP BY dept_id
HAVING COUNT(*) > 3;

-- Joins
SELECT * FROM a INNER JOIN b ON a.id = b.a_id;
SELECT * FROM a LEFT  JOIN b ON a.id = b.a_id;
SELECT * FROM a RIGHT JOIN b ON a.id = b.a_id;  -- (not SQLite)

-- Subqueries
SELECT * FROM employees WHERE salary > (SELECT AVG(salary) FROM employees);
SELECT * FROM employees WHERE dept_id IN (SELECT id FROM departments WHERE active=1);
SELECT * FROM (SELECT dept_id, AVG(salary) AS avg FROM employees GROUP BY dept_id) t;

-- CTEs (MySQL 8.0+, others for years)
WITH summary AS (SELECT dept_id, AVG(salary) avg FROM employees GROUP BY dept_id)
SELECT * FROM summary WHERE avg > 50000;

-- CASE
SELECT CASE WHEN sal > 80000 THEN 'High' WHEN sal > 50000 THEN 'Mid' ELSE 'Low' END
FROM employees;

-- Window functions (MySQL 8.0+, others for years)
SELECT name, salary, RANK() OVER (PARTITION BY dept_id ORDER BY salary DESC)
FROM employees;

-- DML
INSERT INTO table (col1, col2) VALUES (val1, val2);
UPDATE table SET col = val WHERE condition;
DELETE FROM table WHERE condition;

-- DDL
CREATE TABLE t (id INT PRIMARY KEY, name VARCHAR(100) NOT NULL);
ALTER TABLE t ADD COLUMN email VARCHAR(150);
DROP TABLE IF EXISTS t;
CREATE INDEX idx ON t(col);
```

**If you can write all of the above — you already know 80% of every SQL dialect.**
The remaining 20% is syntax sugar. You learn it as you go.

---

## The One-Page Summary

```
┌───────────────────────────────────────────────────────────────┐
│                  SQL DIALECTS — THE HONEST TRUTH              │
│                                                               │
│  ANSI SQL     = the universal standard. Core of all dialects  │
│  T-SQL        = Microsoft SQL Server & Azure                  │
│  PL/SQL       = Oracle (expensive enterprise)                 │
│  PL/pgSQL     = PostgreSQL (free, powerful, growing fast)     │
│  MySQL SQL    = MySQL & MariaDB (web, what you know)          │
│  SQLite       = embedded / mobile / scripts                   │
│                                                               │
│  80% of SQL is IDENTICAL across all dialects                  │
│  SELECT, JOIN, GROUP BY, CASE, CTE, window functions          │
│                                                               │
│  20% differs:                                                 │
│    → Date functions   → LIMIT vs TOP vs FETCH FIRST           │
│    → NULL handling    → String concat                         │
│    → Procedure syntax → Error handling                        │
│    → Auto-increment   → Type names                            │
│                                                               │
│  When someone "shows off" with T-SQL or PL/SQL:              │
│    They know the 20% extra for that engine.                   │
│    You already know the 80% foundation they built on.         │
│    The 20% gap is days of reading, not years of study.       │
│                                                               │
│  The right response is curiosity, not intimidation.           │
└───────────────────────────────────────────────────────────────┘
```

---

*Written for MySQL developers expanding into other SQL environments. No prior T-SQL, PL/SQL, or PostgreSQL knowledge assumed.*
