# 📘 MySQL — Variables & Parameters in Stored Procedures
> Study notes with examples · Based on Lucky Shrub Gardening Center use cases

---

## Table of Contents
1. [Variables — What They Are](#1--variables--what-they-are)
2. [Where Variables Can Be Created](#2--where-variables-can-be-created)
3. [Method 1 — SET Outside a Procedure](#3--method-1--set-outside-a-procedure)
4. [Method 2 — DECLARE Inside a Procedure](#4--method-2--declare-inside-a-procedure)
5. [Method 3 — Variable Inside a SELECT](#5--method-3--variable-inside-a-select)
6. [Method 4 — SELECT … INTO Variable](#6--method-4--select--into-variable)
7. [Parameters — What They Are](#7--parameters--what-they-are)
8. [IN Parameter](#8--in-parameter)
9. [OUT Parameter](#9--out-parameter)
10. [INOUT Parameter](#10--inout-parameter)
11. [Quick Comparison Table](#11--quick-comparison-table)
12. [Common Mistakes](#12--common-mistakes)

---

## 1. 📌 Variables — What They Are

A **variable** is a named placeholder that stores a value.

```
variable = a name  +  a stored value  +  the ability to change
```

**Why use variables?**
- Pass values **between SQL statements**
- Pass values **between a procedure and a SQL statement**
- Avoid repeating the same value in multiple places
- Store intermediate results for reuse

---

## 2. 🗺️ Where Variables Can Be Created

| Location | Command | Has `@` prefix? |
|----------|---------|-----------------|
| Outside a stored procedure | `SET` | ✅ Yes — `@variable_name` |
| Inside a stored procedure | `DECLARE` | ❌ No — `variable_name` |
| Inside a `SELECT` statement | Assignment operator `:=` | ✅ Yes — `@variable_name` |
| Inside a `SELECT … INTO` | `SELECT func() INTO var` | ✅ Yes — `@variable_name` |

---

## 3. ⚙️ Method 1 — SET Outside a Procedure

Use `SET` to create and assign a value to a variable **outside** any procedure.

### Syntax
```sql
SET @variable_name = value;
```

### Example — Target a specific order by ID
```sql
-- Create a variable to hold the order ID
SET @order_id = 3;

-- Use the variable in a query
SELECT * FROM orders WHERE id = @order_id;

-- Use the variable in a DELETE
DELETE FROM orders WHERE id = @order_id;

-- Use the variable in an UPDATE
UPDATE orders SET status = 'cancelled' WHERE id = @order_id;
```

> 💡 **Key point**: Once `@order_id` is set, you can reuse it across multiple statements without retyping the value `3`.

---

## 4. 🏗️ Method 2 — DECLARE Inside a Procedure

Use `DECLARE` to create a variable **inside** a stored procedure.

### Syntax
```sql
DECLARE variable_name datatype DEFAULT default_value;
```

### Rules
- No `@` prefix — just the plain variable name
- Must specify a **data type** (INT, DECIMAL, VARCHAR, etc.)
- Must specify a **DEFAULT** value
- Must be declared at the **top** of the procedure body (before any logic)

### Example — Find the minimum order cost
```sql
DELIMITER //

CREATE PROCEDURE get_min_order_cost()
BEGIN
  -- Declare variable at the top
  DECLARE minimum_order_cost DECIMAL(10,2) DEFAULT 0.00;

  -- Assign a value using SET
  SET minimum_order_cost = (SELECT MIN(cost) FROM orders);

  -- Use the variable
  SELECT minimum_order_cost AS min_cost;
END //

DELIMITER ;

-- Call the procedure
CALL get_min_order_cost();
```

---

## 5. 📝 Method 3 — Variable Inside a SELECT

Assign a value to a variable **directly inside a SELECT statement** using the `:=` assignment operator.

### Syntax
```sql
SELECT @variable_name := expression;
```

> ⚠️ **Important**: Use `:=` (assignment operator) inside SELECT — NOT `=`.
> The `=` operator inside SELECT checks equality, it does NOT assign.

```
:=   →  assigns a value to the variable         ← use this inside SELECT
=    →  checks if two values are equal           ← use this in WHERE, SET
```

### Example — Store the most expensive order
```sql
-- Assign the max order cost to a variable
SELECT @max_order := MAX(cost) FROM orders;

-- Retrieve the stored value
SELECT @max_order;
-- Output: 1250.00  (or whatever the max is)
```

---

## 6. 📥 Method 4 — SELECT … INTO Variable

Assign the **result of a function** directly to a variable using `SELECT … INTO`.

### Syntax
```sql
SELECT function_name(column)
INTO @variable_name
FROM table_name;
```

### Example — Store the average order cost
```sql
-- Calculate average and store in a variable
SELECT AVG(cost)
INTO @average_cost
FROM orders;

-- Use the variable
SELECT @average_cost AS average_order_cost;
-- Output: 450.75
```

> 💡 Use this when a function (AVG, SUM, COUNT, MAX, MIN) returns a single value you want to store for later use.

---

## 7. 🎛️ Parameters — What They Are

A **parameter** passes arguments (values) into or out of a stored procedure **from the outside**.

```
Variable  =  stores a value internally (inside the procedure or session)
Parameter =  the bridge between outside and inside the procedure
```

### Functions vs Procedures

| | Functions | Procedures |
|--|-----------|------------|
| Parameter types | `IN` only | `IN`, `OUT`, `INOUT` |
| Returns value | Yes — one value | Via OUT / INOUT parameters |

---

## 8. ➡️ IN Parameter

**Default parameter type.** Passes a value **INTO** the procedure. The procedure uses it but cannot send it back.

```
Caller ──── value ──────▶ Procedure
           (IN)           (reads it, cannot modify outside)
```

### Syntax
```sql
CREATE PROCEDURE procedure_name(IN param_name datatype)
BEGIN
  -- use param_name here
END;
```

> If you don't write `IN`, `OUT`, or `INOUT`, MySQL assumes **IN** by default.

### Example — Calculate 20% tax on a salary
```sql
DELIMITER //

CREATE PROCEDURE calculate_tax(IN employee_salary DECIMAL(10,2))
BEGIN
  SELECT employee_salary * 0.20 AS tax_amount;
END //

DELIMITER ;

-- Call the procedure with a specific salary
CALL calculate_tax(5000.00);
-- Output: tax_amount = 1000.00

CALL calculate_tax(8500.00);
-- Output: tax_amount = 1700.00
```

---

## 9. ⬅️ OUT Parameter

**Passes a value OUT** from the procedure to an external variable. The procedure writes to it; the caller reads it.

```
Caller ──────────────────▶ Procedure
       (nothing passed in)  (writes result to OUT param)
           ◀── value ──────
              (OUT)
```

### Syntax
```sql
CREATE PROCEDURE procedure_name(OUT param_name datatype)
BEGIN
  -- assign a value to param_name
  SET param_name = some_value;
END;
```

### Example — Get the lowest cost order
```sql
DELIMITER //

CREATE PROCEDURE get_lowest_cost(OUT lowest_cost DECIMAL(10,2))
BEGIN
  SELECT MIN(cost)
  INTO lowest_cost
  FROM orders;
END //

DELIMITER ;

-- Call the procedure — pass a variable to receive the output
CALL get_lowest_cost(@result);

-- Display the returned value
SELECT @result AS lowest_order_cost;
-- Output: lowest_order_cost = 25.00
```

> 💡 **Notice the pattern**:
> 1. `CALL` passes a variable prefixed with `@`
> 2. The procedure writes into it via the `OUT` parameter
> 3. `SELECT @result` reads it back

---

## 10. 🔁 INOUT Parameter

**Combination of IN and OUT.** The caller passes a value in, the procedure modifies it, and the new value is returned back to the caller's variable.

```
Caller ──── value ────▶ Procedure
       (passed IN)       (modifies it)
       ◀── new value ───
            (OUT)
```

### Syntax
```sql
CREATE PROCEDURE procedure_name(INOUT param_name datatype)
BEGIN
  -- read param_name (IN behaviour)
  -- modify param_name (OUT behaviour)
  SET param_name = new_value;
END;
```

### Example — Square a number
```sql
DELIMITER //

CREATE PROCEDURE square_a_number(INOUT number INT)
BEGIN
  -- Read the input value and return its square in the same parameter
  SET number = number * number;
END //

DELIMITER ;

-- Set the input variable
SET @x_number = 5;

-- Call — the same variable is both input and output
CALL square_a_number(@x_number);

-- Read the result
SELECT @x_number AS squared_result;
-- Output: squared_result = 25
```

### Step-by-step trace
```
SET @x_number = 5          →  @x_number holds 5
CALL square_a_number(@x_number)
  procedure receives:   number = 5     (IN behaviour)
  procedure executes:   SET number = 5 * 5 = 25
  procedure returns:    number = 25    (OUT behaviour)
SELECT @x_number           →  displays 25
```

---

## 11. 📊 Quick Comparison Table

| Feature | `SET @var` | `DECLARE var` | `SELECT @var :=` | `SELECT INTO @var` |
|---------|-----------|---------------|------------------|--------------------|
| Where | Outside proc | Inside proc | Anywhere | Anywhere |
| Prefix | `@` | None | `@` | `@` |
| Needs data type | ❌ | ✅ | ❌ | ❌ |
| Needs DEFAULT | ❌ | ✅ | ❌ | ❌ |
| Assign operator | `=` | — | `:=` | `INTO` keyword |

---

| Parameter | Direction | Passes value IN? | Returns value OUT? | Use case |
|-----------|-----------|------------------|--------------------|----------|
| `IN` | Inbound | ✅ | ❌ | Pass a filter value or input to a procedure |
| `OUT` | Outbound | ❌ | ✅ | Return a computed result to the caller |
| `INOUT` | Both | ✅ | ✅ | Transform a value: pass it in, get modified value back |

---

## 12. ⚠️ Common Mistakes

### Mistake 1 — Using `=` instead of `:=` inside SELECT
```sql
-- ❌ WRONG — this checks equality, does NOT assign
SELECT @max_order = MAX(cost) FROM orders;

-- ✅ CORRECT — use := to assign inside SELECT
SELECT @max_order := MAX(cost) FROM orders;
```

### Mistake 2 — Forgetting `@` outside procedures
```sql
-- ❌ WRONG
SET order_id = 3;      -- no @ → MySQL thinks it's a system variable

-- ✅ CORRECT
SET @order_id = 3;
```

### Mistake 3 — Using `@` inside DECLARE
```sql
-- ❌ WRONG — DECLARE does not use @
DECLARE @minimum_cost DECIMAL(10,2) DEFAULT 0.00;

-- ✅ CORRECT — no @ with DECLARE
DECLARE minimum_cost DECIMAL(10,2) DEFAULT 0.00;
```

### Mistake 4 — Forgetting to SELECT the OUT variable after CALL
```sql
-- ❌ WRONG — calls the procedure but never reads the result
CALL get_lowest_cost(@result);

-- ✅ CORRECT — call first, then SELECT to see the value
CALL get_lowest_cost(@result);
SELECT @result AS lowest_order_cost;
```

### Mistake 5 — DECLARE after logic statements inside a procedure
```sql
-- ❌ WRONG — DECLARE must come before any SELECT/SET/logic
BEGIN
  SELECT * FROM orders;
  DECLARE min_cost DECIMAL(10,2) DEFAULT 0.00;  -- too late!
END;

-- ✅ CORRECT — all DECLAREs first
BEGIN
  DECLARE min_cost DECIMAL(10,2) DEFAULT 0.00;  -- at the top
  SELECT * FROM orders;
END;
```

---

## Summary — The Mental Model

```
VARIABLE  = a named storage box you can read and write
             @var  → outside / session level  (use SET or :=)
             var   → inside procedure only    (use DECLARE)

PARAMETER = the doorway between outside and inside a procedure
             IN    → values come IN     (input only)
             OUT   → values go OUT      (output only)
             INOUT → values go both IN and OUT (transform)
```

---

*Examples based on Lucky Shrub Gardening Center database — orders table with cost and employee salary data.*
