---

layout: post
cover_color: #000000

keywords: SQL, Variables, Parameters, T-SQL, PL/SQL, PL/pgSQL, MySQL, SQLite, PostgreSQL, SQL Server, Oracle, MS Access, ANSI SQL, SQL Functions, SQL Syntax, SQL Features, SQL Comparison, SQL Learning, SQL Cheatsheet, SQL Reference, SQL Tutorial, SQL Guide, SQL Best Practices, SQL Common Mistakes, SQL Pros and Cons, SQL When It Matters, SQL How to Learn, SQL 80% Never Changes, SQL Dialects Complete Guide, SQL Dialects T-SQL, SQL Dialects PL/SQL, SQL Dialects PL/pgSQL, SQL Dialects MySQL, SQL Dialects SQLite, SQL Dialects PostgreSQL, SQL Dialects SQL Server, SQL Dialects Oracle, SQL Dialects MS Access, SQL Dialects ANSI SQL, SQL Dialects SQL Functions, SQL Dialects SQL Syntax, SQL Dialects SQL Features, SQL Dialects SQL Comparison, SQL Dialects SQL Learning, SQL Dialects SQL Cheatsheet, SQL Dialects SQL Reference, SQL Dialects SQL Tutorial, SQL Dialects SQL Guide, SQL Dialects SQL Best Practices, SQL Dialects SQL Common Mistakes, SQL Dialects SQL Pros and Cons, SQL Dialects SQL When It Matters, SQL Dialects SQL How to Learn, SQL Dialects SQL 80% Never Changes, SQL Dialects Complete Guide with Examples, SQL Dialects Complete Guide with Examples Based on Lucky Shrub Gardening Center Use Cases

title: Variables & Parameters in SQL — Complete Guide

description: >-
    A calm, honest guide to all SQL "flavors" — what they are, who uses them, when they matter, and why they're not as scary as they sound. Covers T-SQL, PL/SQL, PL/pgSQL, MySQL, SQLite, PostgreSQL, SQL Server, Oracle, MS Access, ANSI SQL, SQL Functions, SQL Syntax, SQL Features, SQL Comparison, SQL Learning, SQL Cheatsheet, SQL Reference, SQL Tutorial, SQL Guide, SQL Best Practices, SQL Common Mistakes, SQL Pros and Cons, SQL When It Matters, SQL How to Learn, SQL 80% Never Changes, SQL Dialects Complete Guide, SQL Dialects T-SQL, SQL Dialects PL/SQL, SQL Dialects PL/pgSQL, SQL Dialects MySQL, SQL Dialects SQLite, SQL Dialects PostgreSQL, SQL Dialects SQL Server, SQL Dialects Oracle, SQL Dialects MS Access, SQL Dialects ANSI SQL, SQL Dialects SQL Functions, SQL Dialects SQL Syntax, SQL Dialects SQL Features, SQL Dialects SQL Comparison, SQL Dialects SQL Learning, SQL Dialects SQL Cheatsheet, SQL Dialects SQL Reference, SQL Dialects SQL Tutorial, SQL Dialects SQL Guide, SQL Dialects SQL Best Practices, SQL Dialects SQL Common Mistakes, SQL Dialects SQL Pros and Cons, SQL Dialects SQL When It Matters, SQL Dialects SQL How to Learn, SQL Dialects SQL 80% Never Changes, SQL Dialects Complete Guide with Examples, SQL Dialects Complete Guide with Examples Based on Lucky Shrub Gardening Center Use Cases
    

date: 2026-04-23 10:00:00 +0800
author: Mahmoud Lotfi
file_name: 2026-04-23-variables-parameters-all-dialects.md
categories: [SQL, Variables, Parameters]
tags: [SQL, Variables, Parameters]
pin: False
math: true
mermaid: true
comments: true
toc: true
render_with_liquid: false

image:
  path: /assets/img/posts/sql.jpg
  alt: Variables & Parameters in SQL — Complete Guide
  lqip: data:image/webp;base64,UklGRjoAAABXRUJQVlA4IC4AAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA

---

# 📘 Variables & Parameters in SQL
> Complete study notes · ANSI SQL · MySQL · T-SQL · PL/SQL · PL/pgSQL · SQLite
> Same 12 topics — every dialect side by side with examples

---

## Legend
| Symbol | Meaning |
|--------|---------|
| ✅ | Fully supported |
| ⚠️ | Supported with different syntax |
| ❌ | Not supported |

---

## Table of Contents
1. [Variables — What They Are](#1-variables--what-they-are)
2. [Where Variables Can Be Created](#2-where-variables-can-be-created)
3. [SET / Assign Outside a Procedure](#3-set--assign-outside-a-procedure)
4. [DECLARE Inside a Procedure](#4-declare-inside-a-procedure)
5. [Variable Inside a SELECT](#5-variable-inside-a-select)
6. [SELECT … INTO Variable](#6-select--into-variable)
7. [Parameters — What They Are](#7-parameters--what-they-are)
8. [IN Parameter](#8-in-parameter)
9. [OUT Parameter](#9-out-parameter)
10. [INOUT / IN OUT Parameter](#10-inout--in-out-parameter)
11. [Quick Comparison Tables](#11-quick-comparison-tables)
12. [Common Mistakes by Dialect](#12-common-mistakes-by-dialect)

---

## 1. Variables — What They Are

A **variable** is a named placeholder that stores a value during a session or within a procedure block.

```
variable = a name  +  a stored value  +  the ability to change
```

**Why use variables?**
- Avoid repeating the same value in multiple places
- Store intermediate results for reuse
- Pass values between SQL statements
- Pass values between a procedure and a SQL statement

### Support Overview

| Feature | ANSI SQL | MySQL | T-SQL | PL/SQL | PL/pgSQL | SQLite |
|---------|----------|-------|-------|--------|----------|--------|
| Session variables | ⚠️ implementation-defined | ✅ `@var` | ✅ `@var` via DECLARE | ⚠️ bind variables | ⚠️ `\set` in psql only | ❌ |
| Procedural variables | ✅ DECLARE (SQL/PSM) | ✅ DECLARE inside proc | ✅ DECLARE | ✅ DECLARE | ✅ DECLARE | ❌ no procedures |

> 💡 **SQLite has no variables or procedures** — it is a query-only engine. Variables in SQLite applications are handled in the host language (Python, C, etc.), not in SQL itself.

---

## 2. Where Variables Can Be Created

### Summary Table

| Location | MySQL | T-SQL | PL/SQL | PL/pgSQL | SQLite |
|----------|-------|-------|--------|----------|--------|
| Outside procedure (session) | ✅ `SET @var = val` | ✅ `DECLARE @var` + `SET` | ⚠️ bind var `:var` | ⚠️ `\set` in psql client | ❌ |
| Inside procedure (local) | ✅ `DECLARE var` | ✅ `DECLARE @var` | ✅ `var type;` | ✅ `var type;` | ❌ |
| Inside SELECT statement | ✅ `:=` operator | ✅ `SELECT @var = expr` | ✅ `SELECT INTO` | ✅ `SELECT INTO` | ❌ |

### The `@` Prefix Rule

```
MySQL:       @var   → session variable (outside or inside proc with SET)
             var    → local variable inside proc (DECLARE, no @)

T-SQL:       @var   → ALL variables use @ — both session and local
                      local variables MUST be declared with DECLARE first

PL/SQL:      v_var  → convention only (no @). Variables declared in DECLARE block
                      No @ symbol at all

PL/pgSQL:    v_var  → convention only. Variables declared in DECLARE block
                      No @ symbol at all

SQLite:      N/A    → no variables in SQL layer
```

---

## 3. ⚙️ SET / Assign Outside a Procedure

### MySQL
```sql
SET @order_id = 3;

-- Use the variable
SELECT * FROM orders WHERE id = @order_id;
UPDATE orders SET status = 'cancelled' WHERE id = @order_id;
DELETE FROM orders WHERE id = @order_id;
```

### T-SQL (SQL Server)
```sql
-- T-SQL requires DECLARE before SET — even outside a procedure
DECLARE @order_id INT;
SET @order_id = 3;

-- Or combine declaration and assignment (SQL Server 2008+)
DECLARE @order_id INT = 3;

-- Use the variable
SELECT * FROM orders WHERE id = @order_id;
UPDATE orders SET status = 'cancelled' WHERE id = @order_id;
DELETE FROM orders WHERE id = @order_id;
```

### PL/SQL (Oracle)
```sql
-- Oracle does not have standalone session variables like MySQL @var
-- Variables must live inside a PL/SQL anonymous block or procedure

-- Using a bind variable in SQL*Plus / SQLcl client tool
VARIABLE order_id NUMBER;
EXEC :order_id := 3;

SELECT * FROM orders WHERE id = :order_id;

-- Or use a full anonymous block
DECLARE
  v_order_id NUMBER := 3;
BEGIN
  UPDATE orders SET status = 'cancelled' WHERE id = v_order_id;
  COMMIT;
END;
/
```

### PL/pgSQL (PostgreSQL)
```sql
-- PostgreSQL has no standalone session variable syntax like MySQL
-- Use a temporary table, a custom setting, or a CTE instead

-- Option 1: \set in psql client (client-side only, not SQL)
\set order_id 3
SELECT * FROM orders WHERE id = :order_id;

-- Option 2: Use a CTE as an inline variable
WITH params AS (SELECT 3 AS order_id)
SELECT o.*
FROM orders o, params p
WHERE o.id = p.order_id;

-- Option 3: Full DO block (anonymous procedure)
DO $$
DECLARE
  v_order_id INT := 3;
BEGIN
  UPDATE orders SET status = 'cancelled' WHERE id = v_order_id;
END;
$$;
```

### SQLite
```sql
-- SQLite has NO variable support in SQL
-- Variables must be handled in the calling application (Python, etc.)

-- Python example using SQLite
import sqlite3
conn = sqlite3.connect('mydb.sqlite')
order_id = 3
conn.execute("SELECT * FROM orders WHERE id = ?", (order_id,))
```

---

## 4. DECLARE Inside a Procedure

### Rules Summary

| | MySQL | T-SQL | PL/SQL | PL/pgSQL |
|--|-------|-------|--------|----------|
| Keyword | `DECLARE` | `DECLARE` | (in DECLARE section) | `DECLARE` |
| Prefix | No `@` | `@` required | No `@` | No `@` |
| Needs data type | ✅ | ✅ | ✅ | ✅ |
| Needs DEFAULT/value | optional | optional | optional | optional |
| Must come before logic | ✅ | ❌ flexible | ✅ | ✅ |

---

### MySQL
```sql
DELIMITER //

CREATE PROCEDURE get_min_order_cost()
BEGIN
  -- Declare at the top, before any logic
  DECLARE minimum_order_cost DECIMAL(10,2) DEFAULT 0.00;

  -- Assign value
  SET minimum_order_cost = (SELECT MIN(cost) FROM orders);

  -- Use it
  SELECT minimum_order_cost AS min_cost;
END //

DELIMITER ;

CALL get_min_order_cost();
```

### T-SQL (SQL Server)
```sql
CREATE PROCEDURE get_min_order_cost
AS
BEGIN
  SET NOCOUNT ON;

  -- T-SQL: DECLARE can appear anywhere in the block
  DECLARE @minimum_order_cost DECIMAL(10,2);

  -- Assign using SET
  SET @minimum_order_cost = (SELECT MIN(cost) FROM orders);

  -- Or assign using SELECT
  SELECT @minimum_order_cost = MIN(cost) FROM orders;

  -- Use it
  SELECT @minimum_order_cost AS min_cost;
END;
GO

EXEC get_min_order_cost;
```

### PL/SQL (Oracle)
```sql
CREATE OR REPLACE PROCEDURE get_min_order_cost
AS
  -- Variables declared BEFORE BEGIN, in the declaration section
  v_minimum_cost  NUMBER(10,2) := 0;    -- := is assignment in PL/SQL
BEGIN
  -- Assign using SELECT INTO
  SELECT MIN(cost)
  INTO v_minimum_cost
  FROM orders;

  -- Output result
  DBMS_OUTPUT.PUT_LINE('Min cost: ' || v_minimum_cost);
END get_min_order_cost;
/

-- Execute
EXEC get_min_order_cost;
```

### PL/pgSQL (PostgreSQL)
```sql
CREATE OR REPLACE FUNCTION get_min_order_cost()
RETURNS NUMERIC
LANGUAGE plpgsql
AS $$
DECLARE
  -- Variables declared in DECLARE section before BEGIN
  v_minimum_cost  NUMERIC(10,2) := 0;
BEGIN
  -- Assign using SELECT INTO
  SELECT MIN(cost)
  INTO v_minimum_cost
  FROM orders;

  RETURN v_minimum_cost;
END;
$$;

-- Call it
SELECT get_min_order_cost();
```

> 💡 **PostgreSQL uses FUNCTIONS, not PROCEDURES** for most cases. Procedures (with `CREATE PROCEDURE`) were added in PostgreSQL 11 but functions remain the standard way.

---

## 5. Variable Inside a SELECT

Assigning a value to a variable **directly inside a SELECT statement**.

> ⚠️ **The critical operator difference:**
> ```
> =    checks equality   (used in WHERE, comparisons)
> :=   assigns a value   (used in MySQL SELECT assignment)
> ```

### MySQL
```sql
-- Use := to assign inside SELECT
SELECT @max_order := MAX(cost) FROM orders;

-- Retrieve stored value
SELECT @max_order AS most_expensive_order;
-- Output: 1250.00
```

### T-SQL (SQL Server)
```sql
-- T-SQL uses = for assignment inside SELECT (must DECLARE first)
DECLARE @max_order DECIMAL(10,2);

SELECT @max_order = MAX(cost) FROM orders;

SELECT @max_order AS most_expensive_order;
-- Output: 1250.00
```

> ⚠️ **T-SQL quirk**: If `SELECT @var = col FROM table` returns multiple rows,
> `@var` gets the LAST value — not an error, just silent behaviour.
> Use `SET @var = (SELECT ...)` to be explicit when expecting one row.

### PL/SQL (Oracle)
```sql
-- Oracle uses SELECT INTO inside a block, not := in SELECT
DECLARE
  v_max_order NUMBER(10,2);
BEGIN
  SELECT MAX(cost)
  INTO v_max_order          -- INTO keyword assigns the result
  FROM orders;

  DBMS_OUTPUT.PUT_LINE('Max order: ' || v_max_order);
END;
/
```

### PL/pgSQL (PostgreSQL)
```sql
DO $$
DECLARE
  v_max_order NUMERIC(10,2);
BEGIN
  SELECT MAX(cost)
  INTO v_max_order
  FROM orders;

  RAISE NOTICE 'Max order: %', v_max_order;
END;
$$;
```

### SQLite
```sql
-- Not applicable — SQLite has no variable assignment in SQL
-- Use application-side variables (Python, etc.)
cursor.execute("SELECT MAX(cost) FROM orders")
max_order = cursor.fetchone()[0]
```

---

## 6. SELECT … INTO Variable

Assign the **result of an aggregate or function** directly to a variable.

### MySQL
```sql
-- Calculate average and store in a variable
SELECT AVG(cost)
INTO @average_cost
FROM orders;

SELECT @average_cost AS average_order_cost;
-- Output: 450.75
```

### T-SQL (SQL Server)
```sql
-- T-SQL: use SELECT @var = expr or SET @var = (SELECT ...)
DECLARE @average_cost DECIMAL(10,2);

-- Method 1: SELECT assignment
SELECT @average_cost = AVG(cost) FROM orders;

-- Method 2: SET with subquery (safer — enforces single value)
SET @average_cost = (SELECT AVG(cost) FROM orders);

SELECT @average_cost AS average_order_cost;
```

### PL/SQL (Oracle)
```sql
DECLARE
  v_average_cost  NUMBER(10,2);
  v_count         NUMBER;
BEGIN
  -- Single column into single variable
  SELECT AVG(cost) INTO v_average_cost FROM orders;

  -- Multiple columns into multiple variables
  SELECT COUNT(*), AVG(cost)
  INTO v_count, v_average_cost
  FROM orders;

  DBMS_OUTPUT.PUT_LINE('Count: ' || v_count || ', Avg: ' || v_average_cost);
END;
/
```

### PL/pgSQL (PostgreSQL)
```sql
DO $$
DECLARE
  v_average_cost  NUMERIC(10,2);
  v_count         INT;
BEGIN
  -- Single value
  SELECT AVG(cost) INTO v_average_cost FROM orders;

  -- Multiple values in one SELECT INTO
  SELECT COUNT(*), AVG(cost)
  INTO v_count, v_average_cost
  FROM orders;

  RAISE NOTICE 'Count: %, Avg: %', v_count, v_average_cost;
END;
$$;
```

### SQLite
```sql
-- Not applicable in SQL layer
-- Python equivalent:
cursor.execute("SELECT AVG(cost) FROM orders")
average_cost = cursor.fetchone()[0]
```

---

## 7. Parameters — What They Are

A **parameter** is the bridge between the outside world and the inside of a procedure or function.

```
Variable  =  stores a value internally (private to the block/session)
Parameter =  the doorway: passes values IN or OUT of the procedure
```

### Parameter Types by Dialect

| Type | MySQL | T-SQL | PL/SQL | PL/pgSQL | SQLite |
|------|-------|-------|--------|----------|--------|
| Input only | `IN` (default) | no keyword (all params are input) | `IN` | function arguments | ❌ |
| Output only | `OUT` | `OUTPUT` | `OUT` | `RETURNS` / `OUT` in proc | ❌ |
| Both | `INOUT` | N/A | `IN OUT` | `INOUT` in proc | ❌ |

> 💡 **Functions vs Procedures:**
> ```
> Function  → Returns exactly one value. Used inside SELECT expressions.
> Procedure → May have no return, or return via OUT parameters.
>
> MySQL, PL/SQL, PL/pgSQL → both exist
> T-SQL                   → both exist (scalar functions, table functions, procs)
> SQLite                  → no procedures; no user-defined functions in pure SQL
> ```

---

## 8. IN Parameter

Passes a value **INTO** the procedure. The procedure uses it but cannot send back a new value through it.

```
Caller ──── value ──────▶  Procedure
           (IN)              reads it, cannot modify outside
```

### MySQL
```sql
DELIMITER //

CREATE PROCEDURE calculate_tax(IN employee_salary DECIMAL(10,2))
BEGIN
  SELECT ROUND(employee_salary * 0.20, 2) AS tax_amount;
END //

DELIMITER ;

CALL calculate_tax(5000.00);   -- Output: 1000.00
CALL calculate_tax(8500.00);   -- Output: 1700.00
```

### T-SQL (SQL Server)
```sql
-- T-SQL: all parameters are IN by default — no keyword needed
CREATE PROCEDURE calculate_tax
    @employee_salary DECIMAL(10,2)    -- input parameter
AS
BEGIN
  SET NOCOUNT ON;
  SELECT ROUND(@employee_salary * 0.20, 2) AS tax_amount;
END;
GO

EXEC calculate_tax @employee_salary = 5000.00;  -- Output: 1000.00
EXEC calculate_tax 8500.00;                      -- positional also works
```

### PL/SQL (Oracle)
```sql
CREATE OR REPLACE PROCEDURE calculate_tax(
  p_salary IN NUMBER                   -- IN keyword explicit
)
AS
  v_tax NUMBER(10,2);
BEGIN
  v_tax := p_salary * 0.20;
  DBMS_OUTPUT.PUT_LINE('Tax: ' || v_tax);
END calculate_tax;
/

-- Execute
EXEC calculate_tax(5000);    -- Output: Tax: 1000
```

### PL/pgSQL (PostgreSQL)
```sql
-- PostgreSQL uses FUNCTIONS for this pattern
CREATE OR REPLACE FUNCTION calculate_tax(p_salary NUMERIC)
RETURNS NUMERIC
LANGUAGE plpgsql
AS $$
BEGIN
  RETURN ROUND(p_salary * 0.20, 2);
END;
$$;

-- Call inside a query
SELECT calculate_tax(5000);                -- 1000.00
SELECT name, calculate_tax(salary) AS tax FROM employees;
```

---

## 9. OUT Parameter

**Passes a value OUT** from the procedure. The procedure writes to it; the caller reads it.

```
Caller ──────────────────▶  Procedure
                             writes result to OUT param
       ◀──── value ────────
              (OUT)
```

### MySQL
```sql
DELIMITER //

CREATE PROCEDURE get_lowest_cost(OUT lowest_cost DECIMAL(10,2))
BEGIN
  SELECT MIN(cost)
  INTO lowest_cost
  FROM orders;
END //

DELIMITER ;

-- Call: pass a variable to receive the output
CALL get_lowest_cost(@result);

-- Read the returned value
SELECT @result AS lowest_order_cost;
-- Output: 25.00
```

### T-SQL (SQL Server)
```sql
-- T-SQL uses OUTPUT keyword (not OUT)
CREATE PROCEDURE get_lowest_cost
    @lowest_cost DECIMAL(10,2) OUTPUT    -- OUTPUT keyword
AS
BEGIN
  SET NOCOUNT ON;
  SELECT @lowest_cost = MIN(cost) FROM orders;
END;
GO

-- Call: must also use OUTPUT keyword when calling
DECLARE @result DECIMAL(10,2);
EXEC get_lowest_cost @lowest_cost = @result OUTPUT;
SELECT @result AS lowest_order_cost;
-- Output: 25.00
```

### PL/SQL (Oracle)
```sql
CREATE OR REPLACE PROCEDURE get_lowest_cost(
  p_lowest_cost OUT NUMBER             -- OUT keyword
)
AS
BEGIN
  SELECT MIN(cost)
  INTO p_lowest_cost
  FROM orders;
END get_lowest_cost;
/

-- Execute using an anonymous block
DECLARE
  v_result NUMBER;
BEGIN
  get_lowest_cost(v_result);
  DBMS_OUTPUT.PUT_LINE('Lowest cost: ' || v_result);
END;
/
-- Output: Lowest cost: 25
```

### PL/pgSQL (PostgreSQL)
```sql
-- Option 1: Function with RETURNS (most common in PostgreSQL)
CREATE OR REPLACE FUNCTION get_lowest_cost()
RETURNS NUMERIC
LANGUAGE plpgsql
AS $$
DECLARE
  v_lowest NUMERIC;
BEGIN
  SELECT MIN(cost) INTO v_lowest FROM orders;
  RETURN v_lowest;
END;
$$;

SELECT get_lowest_cost();   -- 25.00

-- Option 2: Procedure with OUT parameter (PostgreSQL 11+)
CREATE OR REPLACE PROCEDURE get_lowest_cost(OUT p_lowest NUMERIC)
LANGUAGE plpgsql
AS $$
BEGIN
  SELECT MIN(cost) INTO p_lowest FROM orders;
END;
$$;

-- Call
CALL get_lowest_cost(NULL);
```

---

## 10. INOUT / IN OUT Parameter

**Combination of IN and OUT.** The caller passes a value in; the procedure modifies it and sends the new value back.

```
Caller ──── value ────▶  Procedure
       (passed IN)        modifies it
       ◀── new value ───
            (OUT)
```

### MySQL
```sql
DELIMITER //

CREATE PROCEDURE square_a_number(INOUT number INT)
BEGIN
  SET number = number * number;
END //

DELIMITER ;

-- Set the input variable
SET @x_number = 5;

-- Call — same variable is input AND output
CALL square_a_number(@x_number);

SELECT @x_number AS squared_result;   -- Output: 25
```

**Step-by-step trace:**
```
SET @x_number = 5             →  @x_number = 5
CALL square_a_number(@x_number)
  receives:  number = 5        (IN behaviour)
  executes:  SET number = 5*5 = 25
  returns:   number = 25       (OUT behaviour)
SELECT @x_number              →  25
```

### T-SQL (SQL Server)
```sql
-- T-SQL does not have INOUT — simulate with OUTPUT parameter
-- The parameter serves as both input and output
CREATE PROCEDURE square_a_number
    @number INT OUTPUT                 -- OUTPUT = both read and write
AS
BEGIN
  SET @number = @number * @number;
END;
GO

DECLARE @x_number INT = 5;
EXEC square_a_number @number = @x_number OUTPUT;
SELECT @x_number AS squared_result;   -- Output: 25
```

### PL/SQL (Oracle)
```sql
-- Oracle uses IN OUT (two words, with a space)
CREATE OR REPLACE PROCEDURE square_a_number(
  p_number IN OUT NUMBER               -- IN OUT (space between them)
)
AS
BEGIN
  p_number := p_number * p_number;     -- := is assignment in PL/SQL
END square_a_number;
/

-- Execute
DECLARE
  v_num NUMBER := 5;
BEGIN
  square_a_number(v_num);
  DBMS_OUTPUT.PUT_LINE('Squared: ' || v_num);   -- Output: Squared: 25
END;
/
```

### PL/pgSQL (PostgreSQL)
```sql
-- INOUT in PostgreSQL procedures (PostgreSQL 11+)
CREATE OR REPLACE PROCEDURE square_a_number(INOUT p_number INT)
LANGUAGE plpgsql
AS $$
BEGIN
  p_number := p_number * p_number;
END;
$$;

-- Call
CALL square_a_number(5);
-- Output: p_number = 25
```

---

## 11. Quick Comparison Tables

### Variables Declaration Syntax

| | MySQL | T-SQL | PL/SQL | PL/pgSQL | SQLite |
|--|-------|-------|--------|----------|--------|
| **Session variable** | `SET @var = val` | `DECLARE @var INT; SET @var = val` | `:var` (bind) | `\set var val` (psql) | ❌ |
| **Local (in proc)** | `DECLARE var INT DEFAULT 0;` | `DECLARE @var INT = 0;` | `v_var NUMBER := 0;` | `v_var INT := 0;` | ❌ |
| **Uses `@` prefix** | Session only | Always | Never | Never | — |
| **Assign operator** | `=` (SET) · `:=` (SELECT) | `=` (both SET and SELECT) | `:=` always | `:=` always | — |
| **SELECT assign** | `SELECT @v := expr` | `SELECT @v = expr` | `SELECT … INTO v` | `SELECT … INTO v` | ❌ |
| **NULL default** | ✅ | ✅ | ✅ | ✅ | — |

---

### Parameter Types

| Type | MySQL | T-SQL | PL/SQL | PL/pgSQL | SQLite |
|------|-------|-------|--------|----------|--------|
| Input | `IN` (default) | no keyword | `IN` (default) | argument (no keyword) | ❌ |
| Output | `OUT` | `OUTPUT` | `OUT` | `OUT` in proc / `RETURNS` in func | ❌ |
| Both | `INOUT` | `OUTPUT` (serves as both) | `IN OUT` ← space! | `INOUT` in proc | ❌ |
| Call keyword | `CALL` | `EXEC` / `EXECUTE` | `EXEC` / anon block | `CALL` / `SELECT` | ❌ |

---

### Key Syntax Differences at a Glance

| Task | MySQL | T-SQL | PL/SQL | PL/pgSQL |
|------|-------|-------|--------|----------|
| Delimiter change | `DELIMITER //` | `GO` (batch separator) | `/` (block end) | `$$` (dollar quote) |
| Print to screen | `SELECT value;` | `PRINT @var;` | `DBMS_OUTPUT.PUT_LINE()` | `RAISE NOTICE '% ', var;` |
| Assignment in block | `SET var = val` | `SET @var = val` | `v_var := val` | `v_var := val` |
| Error handling | `DECLARE … HANDLER` | `TRY … CATCH` | `EXCEPTION WHEN` | `EXCEPTION WHEN` |
| No rows found error | `SQLSTATE '02000'` | check `@@ROWCOUNT` | `WHEN NO_DATA_FOUND` | `WHEN NO_DATA_FOUND` |

---

## 12. Common Mistakes by Dialect

### MySQL

```sql
-- ❌ WRONG: = instead of := inside SELECT
SELECT @max_order = MAX(cost) FROM orders;   -- does NOT assign — checks equality

-- ✅ CORRECT
SELECT @max_order := MAX(cost) FROM orders;

-- ❌ WRONG: @ inside DECLARE
DECLARE @min_cost DECIMAL(10,2) DEFAULT 0;   -- error: @ not used with DECLARE

-- ✅ CORRECT
DECLARE min_cost DECIMAL(10,2) DEFAULT 0;

-- ❌ WRONG: DECLARE after logic statements
BEGIN
  SELECT COUNT(*) FROM orders;
  DECLARE total INT DEFAULT 0;    -- too late — DECLARE must be first
END;

-- ✅ CORRECT
BEGIN
  DECLARE total INT DEFAULT 0;    -- at the very top
  SELECT COUNT(*) FROM orders;
END;

-- ❌ WRONG: forgetting @ for session variable
SET order_id = 3;     -- MySQL treats this as a system variable — unexpected

-- ✅ CORRECT
SET @order_id = 3;
```

---

### T-SQL (SQL Server)

```sql
-- ❌ WRONG: using variable without DECLARE
SET @total = 100;     -- error: must declare first

-- ✅ CORRECT
DECLARE @total INT;
SET @total = 100;

-- ❌ WRONG: forgetting OUTPUT keyword when calling a procedure with OUTPUT param
DECLARE @result DECIMAL(10,2);
EXEC get_lowest_cost @lowest_cost = @result;      -- missing OUTPUT — gets NULL

-- ✅ CORRECT
EXEC get_lowest_cost @lowest_cost = @result OUTPUT;

-- ❌ WRONG: using LIMIT (MySQL syntax — not T-SQL)
SELECT * FROM employees ORDER BY salary DESC LIMIT 5;   -- syntax error

-- ✅ CORRECT
SELECT TOP 5 * FROM employees ORDER BY salary DESC;

-- ❌ WRONG: expecting SELECT @var = expr to fail on multiple rows
-- T-SQL silently takes the LAST row — not an error but often wrong
SELECT @name = name FROM employees;   -- if multiple rows, @name = last one

-- ✅ CORRECT: use TOP 1 or aggregate when expecting one value
SELECT TOP 1 @name = name FROM employees ORDER BY id;
```

---

### PL/SQL (Oracle)

```sql
-- ❌ WRONG: using = instead of := for assignment
v_salary = 5000;        -- syntax error in PL/SQL

-- ✅ CORRECT
v_salary := 5000;

-- ❌ WRONG: forgetting DECLARE section before BEGIN
BEGIN
  v_salary NUMBER := 5000;   -- variables cannot be declared here
END;

-- ✅ CORRECT
DECLARE
  v_salary NUMBER := 5000;   -- must be in DECLARE section
BEGIN
  NULL;
END;

-- ❌ WRONG: INOUT written as one word
CREATE PROCEDURE p(p_num INOUT NUMBER) ...   -- error: must be IN OUT

-- ✅ CORRECT
CREATE PROCEDURE p(p_num IN OUT NUMBER) ...  -- space between IN and OUT

-- ❌ WRONG: forgetting to handle NO_DATA_FOUND when using SELECT INTO
BEGIN
  SELECT salary INTO v_salary FROM employees WHERE id = 9999;
  -- if no row found → unhandled exception crashes the block
END;

-- ✅ CORRECT
BEGIN
  SELECT salary INTO v_salary FROM employees WHERE id = 9999;
EXCEPTION
  WHEN NO_DATA_FOUND THEN
    v_salary := 0;
END;

-- ❌ WRONG: using CONCAT() — Oracle uses || for strings
SELECT CONCAT(first_name, ' ', last_name) FROM employees;  -- works in 11g+ but non-standard

-- ✅ ORACLE NATIVE
SELECT first_name || ' ' || last_name FROM employees;
```

---

### PL/pgSQL (PostgreSQL)

```sql
-- ❌ WRONG: forgetting LANGUAGE clause
CREATE OR REPLACE FUNCTION get_tax(p_salary NUMERIC)
RETURNS NUMERIC
AS $$
BEGIN
  RETURN p_salary * 0.20;
END;
$$;
-- Error: language not specified

-- ✅ CORRECT
CREATE OR REPLACE FUNCTION get_tax(p_salary NUMERIC)
RETURNS NUMERIC
LANGUAGE plpgsql     -- required
AS $$
BEGIN
  RETURN p_salary * 0.20;
END;
$$;

-- ❌ WRONG: using CALL on a function (not a procedure)
CALL get_tax(5000);   -- error: get_tax is a function, not a procedure

-- ✅ CORRECT
SELECT get_tax(5000);

-- ❌ WRONG: forgetting $$ delimiter pair
CREATE OR REPLACE FUNCTION get_tax(p_salary NUMERIC)
RETURNS NUMERIC LANGUAGE plpgsql AS
BEGIN           -- error: missing opening $$
  RETURN p_salary * 0.20;
END;

-- ✅ CORRECT — $$ wraps the function body
AS $$
BEGIN
  RETURN p_salary * 0.20;
END;
$$;

-- ❌ WRONG: SELECT INTO with multiple rows — crashes in strict mode
SELECT name INTO v_name FROM employees;   -- error if more than 1 row returned

-- ✅ CORRECT: add LIMIT 1 or use aggregate
SELECT name INTO v_name FROM employees ORDER BY id LIMIT 1;
```

---

### SQLite

```sql
-- SQLite has no variables, no procedures, no functions in SQL
-- All variable logic must go in the host application

-- ❌ Not possible in SQLite SQL
DECLARE @x INT;
SET @x = 5;
SELECT @x;

-- ✅ Handle in Python instead
import sqlite3
conn = sqlite3.connect(':memory:')
x = 5
result = conn.execute("SELECT * FROM orders WHERE id = ?", (x,)).fetchall()

-- ❌ Not possible — no stored procedures
CREATE PROCEDURE my_proc() BEGIN ... END;

-- ✅ Use Python function wrapping SQL instead
def get_orders_by_status(conn, status):
    return conn.execute(
        "SELECT * FROM orders WHERE status = ?", (status,)
    ).fetchall()
```

---

## The One-Page Summary

```
┌──────────────────────────────────────────────────────────────────────┐
│              VARIABLES & PARAMETERS — ALL DIALECTS                   │
│                                                                      │
│  VARIABLE = storage box for a value inside SQL                       │
│  PARAMETER = the door between outside and inside a procedure         │
│                                                                      │
│  SESSION VARIABLE (outside proc):                                    │
│    MySQL:      SET @var = val                                        │
│    T-SQL:      DECLARE @var INT; SET @var = val                      │
│    Oracle:     anonymous block or bind variable :var                 │
│    PostgreSQL: \set in psql, or CTE, or DO block                     │
│    SQLite:     not available — use host language                     │
│                                                                      │
│  LOCAL VARIABLE (inside proc):                                       │
│    MySQL:      DECLARE var INT DEFAULT 0;                            │
│    T-SQL:      DECLARE @var INT = 0;                                 │
│    Oracle:     v_var NUMBER := 0;    (in DECLARE section)            │
│    PostgreSQL: v_var INT := 0;       (in DECLARE section)            │
│                                                                      │
│  ASSIGNMENT OPERATOR:                                                │
│    MySQL SELECT:  := (colon-equals)                                  │
│    T-SQL SELECT:  = (equals)                                         │
│    Oracle/PG:    := (colon-equals, always)                          │
│                                                                      │
│  PARAMETER TYPES:                                                    │
│    IN    → MySQL IN    / T-SQL default / Oracle IN    / PG arg      │
│    OUT   → MySQL OUT   / T-SQL OUTPUT  / Oracle OUT   / PG RETURNS  │
│    INOUT → MySQL INOUT / T-SQL OUTPUT  / Oracle IN OUT/ PG INOUT    │
│                                                                      │
│  CALL:                                                               │
│    MySQL: CALL proc()                                                │
│    T-SQL: EXEC proc                                                  │
│    Oracle: EXEC proc or anonymous block                              │
│    PostgreSQL: CALL proc() or SELECT func()                          │
│    SQLite: ❌ not available                                           │
└──────────────────────────────────────────────────────────────────────┘
```

---

*Examples use an `orders` table with a `cost` column and an `employees` table with `salary`, `name`, and `dept_id` columns throughout.*
