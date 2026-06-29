---
layout: post
cover_color: #000000

keywords: SQL, Functions, Aggregate, String, Math, Date & Time, Comparison & Logical, Window Functions, Type Conversion, Security & Hashing, JSON, NULL Handling, Common Patterns, SQL Functions Reference

title: SQL Functions Cheatsheet

description: >-
  A comprehensive cheatsheet covering all SQL functions, including Aggregate, String, Math, Date & Time, Comparison & Logical, Window Functions, Type Conversion, Security & Hashing, JSON, NULL Handling, and Common Patterns. Includes inline and table-level syntax, add/drop/modify examples, cross-engine compatibility.

date: 2026-04-22 10:00:00 +0800
author: Mahmoud Lotfi
file_name: 2026-04-22-sql-functions-cheatsheet.md
categories: [SQL, Functions, cheatsheet]
tags: [SQL, Functions, cheatsheet]
pin: False
math: true
mermaid: true
comments: true
toc: true
render_with_liquid: false

image:
  path: /assets/img/posts/sql.jpg
  alt: SQL Functions Cheatsheet
  lqip: data:image/webp;base64,UklGRjoAAABXRUJQVlA4IC4AAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA

---

# 1. 📊 SQL Functions Cheatsheet

> Grouped by category · Common syntax examples · Cross-engine compatibility

---

## 1.1. Legend
| Symbol | Meaning |
|--------|---------|
| ✅ | Supported (same or very similar syntax) |
| ⚠️ | Supported with different syntax |
| ❌ | Not supported / no direct equivalent |

---

Here's your SQL Functions Cheatsheet! It covers **11 categories**:

1. **Aggregate** — COUNT, SUM, AVG, GROUP_CONCAT, STDDEV…
2. **String** — CONCAT, TRIM, SUBSTRING, REPLACE, LPAD…
3. **Math / Numeric** — ROUND, FLOOR, CEIL, MOD, RAND, GREATEST…
4. **Date & Time** — NOW, DATEDIFF, DATE_FORMAT, TIMESTAMPDIFF…
5. **Comparison & Logical** — BETWEEN, IN, LIKE, COALESCE, CASE, IF…
6. **Window Functions** — ROW_NUMBER, RANK, LAG, LEAD, NTILE…
7. **Type Conversion** — CAST, HEX, ASCII, TO_BASE64…
8. **Security & Hashing** — MD5, SHA2, AES_ENCRYPT, UUID…
9. **JSON** — JSON_EXTRACT, JSON_SET, JSON_ARRAYAGG…
10. **NULL Handling** — engine-by-engine quick reference
11. **Common Patterns** — running totals, top-N per group, age calc, pivot aggregation

Each section includes a cross-engine compatibility table for **MySQL, SQLite, PostgreSQL, SQL Server, Oracle, and MS Access** with ✅ / ⚠️ / ❌ indicators.

---

## 1.2. 🔢 Aggregate Functions

> Operate on a set of rows and return a single summary value.

| Function | Description | MySQL Syntax Example |
|----------|-------------|----------------------|
| `COUNT()` | Count rows | `SELECT COUNT(*) FROM orders;` |
| `COUNT(DISTINCT)` | Count unique values | `SELECT COUNT(DISTINCT customer_id) FROM orders;` |
| `SUM()` | Sum of values | `SELECT SUM(price) FROM products;` |
| `AVG()` | Average value | `SELECT AVG(salary) FROM employees;` |
| `MIN()` | Minimum value | `SELECT MIN(price) FROM products;` |
| `MAX()` | Maximum value | `SELECT MAX(salary) FROM employees;` |
| `GROUP_CONCAT()` | Concatenate group values | `SELECT GROUP_CONCAT(name) FROM employees GROUP BY dept;` |
| `STD()` / `STDDEV()` | Population std deviation | `SELECT STDDEV(salary) FROM employees;` |
| `VARIANCE()` | Population variance | `SELECT VARIANCE(score) FROM results;` |

### 1.2.1. Cross-Engine Compatibility

| Function | MySQL | SQLite | PostgreSQL | SQL Server | Oracle | MS Access |
|----------|-------|--------|------------|------------|--------|-----------|
| `COUNT()` | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `SUM()` | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `AVG()` | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `GROUP_CONCAT()` | ✅ | ✅ | ⚠️ `STRING_AGG(col, ',')` | ⚠️ `STRING_AGG(col, ',')` | ⚠️ `LISTAGG(col, ',')` | ❌ |
| `STDDEV()` | ✅ | ❌ | ⚠️ `STDDEV_POP()` | ⚠️ `STDEV()` | ✅ | ❌ |
| `VARIANCE()` | ✅ | ❌ | ⚠️ `VAR_POP()` | ⚠️ `VAR()` | ✅ | ❌ |

---

## 1.3. 🔤 String Functions

> Manipulate and analyze text data.

| Function | Description | Syntax Example |
|----------|-------------|----------------|
| `CONCAT()` | Join strings | `SELECT CONCAT(first_name, ' ', last_name) FROM users;` |
| `CONCAT_WS()` | Join with separator | `SELECT CONCAT_WS(', ', city, country) FROM addresses;` |
| `LENGTH()` | Length in bytes | `SELECT LENGTH(email) FROM users;` |
| `CHAR_LENGTH()` | Length in characters | `SELECT CHAR_LENGTH(name) FROM users;` |
| `UPPER()` | Uppercase | `SELECT UPPER(name) FROM users;` |
| `LOWER()` | Lowercase | `SELECT LOWER(email) FROM users;` |
| `TRIM()` | Remove leading/trailing spaces | `SELECT TRIM('  hello  ');` |
| `LTRIM()` | Remove leading spaces | `SELECT LTRIM('  hello');` |
| `RTRIM()` | Remove trailing spaces | `SELECT RTRIM('hello  ');` |
| `SUBSTRING()` | Extract part of string | `SELECT SUBSTRING(phone, 1, 3) FROM users;` |
| `LEFT()` | Leftmost N characters | `SELECT LEFT(name, 5) FROM users;` |
| `RIGHT()` | Rightmost N characters | `SELECT RIGHT(code, 4) FROM products;` |
| `REPLACE()` | Replace occurrences | `SELECT REPLACE(phone, '-', '') FROM users;` |
| `INSTR()` | Position of substring | `SELECT INSTR(email, '@') FROM users;` |
| `LOCATE()` | Position of first occurrence | `SELECT LOCATE('@', email) FROM users;` |
| `LPAD()` | Left-pad string | `SELECT LPAD(id, 6, '0') FROM orders;` |
| `RPAD()` | Right-pad string | `SELECT RPAD(name, 20, '.') FROM products;` |
| `REVERSE()` | Reverse string | `SELECT REVERSE(name) FROM users;` |
| `REPEAT()` | Repeat string N times | `SELECT REPEAT('*', 5);` |
| `FORMAT()` | Format number as string | `SELECT FORMAT(price, 2) FROM products;` |
| `STRCMP()` | Compare two strings | `SELECT STRCMP('abc', 'abd');` |
| `SOUNDEX()` | Phonetic encoding | `SELECT SOUNDEX('Robert');` |

### 1.3.1. Cross-Engine Compatibility

| Function | MySQL | SQLite | PostgreSQL | SQL Server | Oracle | MS Access |
|----------|-------|--------|------------|------------|--------|-----------|
| `CONCAT()` | ✅ | ⚠️ Use `||` operator | ✅ | ✅ | ✅ | ⚠️ `&` operator |
| `LENGTH()` | ✅ | ✅ | ⚠️ `CHAR_LENGTH()` for chars | ⚠️ `LEN()` | ✅ bytes only | ⚠️ `LEN()` |
| `SUBSTRING()` | ✅ | ✅ `SUBSTR()` | ✅ | ✅ | ✅ `SUBSTR()` | ⚠️ `MID()` |
| `INSTR()` | ✅ | ✅ | ⚠️ `POSITION()` | ⚠️ `CHARINDEX()` | ✅ | ⚠️ `InStr()` |
| `LPAD()` / `RPAD()` | ✅ | ❌ | ✅ | ❌ | ✅ | ❌ |
| `REPLACE()` | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `TRIM()` | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `SOUNDEX()` | ✅ | ❌ | ✅ | ✅ | ✅ | ✅ |
| `FORMAT()` | ✅ | ❌ | ⚠️ `TO_CHAR()` | ⚠️ `FORMAT()` | ⚠️ `TO_CHAR()` | ⚠️ `Format()` |

---

## 1.4. 🔢 Math / Numeric Functions

> Perform calculations on numeric data.

| Function | Description | Syntax Example |
|----------|-------------|----------------|
| `ABS()` | Absolute value | `SELECT ABS(-42);` → `42` |
| `ROUND()` | Round to N decimals | `SELECT ROUND(3.14159, 2);` → `3.14` |
| `CEIL()` / `CEILING()` | Round up | `SELECT CEIL(4.1);` → `5` |
| `FLOOR()` | Round down | `SELECT FLOOR(4.9);` → `4` |
| `TRUNCATE()` | Truncate decimals | `SELECT TRUNCATE(3.999, 1);` → `3.9` |
| `MOD()` / `%` | Modulo (remainder) | `SELECT MOD(10, 3);` → `1` |
| `POWER()` / `POW()` | Raise to power | `SELECT POW(2, 8);` → `256` |
| `SQRT()` | Square root | `SELECT SQRT(144);` → `12` |
| `EXP()` | e raised to power | `SELECT EXP(1);` → `2.718...` |
| `LN()` | Natural logarithm | `SELECT LN(2.718);` |
| `LOG()` | Natural log / log base N | `SELECT LOG(100);` |
| `LOG2()` | Base-2 logarithm | `SELECT LOG2(8);` → `3` |
| `LOG10()` | Base-10 logarithm | `SELECT LOG10(1000);` → `3` |
| `PI()` | Value of π | `SELECT PI();` → `3.14159...` |
| `RAND()` | Random float 0–1 | `SELECT RAND();` |
| `SIGN()` | Sign of number (-1, 0, 1) | `SELECT SIGN(-50);` → `-1` |
| `GREATEST()` | Largest of arguments | `SELECT GREATEST(3, 7, 2);` → `7` |
| `LEAST()` | Smallest of arguments | `SELECT LEAST(3, 7, 2);` → `2` |
| `DIV` | Integer division | `SELECT 17 DIV 5;` → `3` |

### 1.4.1. Cross-Engine Compatibility

| Function | MySQL | SQLite | PostgreSQL | SQL Server | Oracle | MS Access |
|----------|-------|--------|------------|------------|--------|-----------|
| `ABS()` | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `ROUND()` | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `CEIL()` | ✅ | ❌ | ✅ | ⚠️ `CEILING()` | ✅ | ❌ |
| `FLOOR()` | ✅ | ❌ | ✅ | ✅ | ✅ | ❌ |
| `TRUNCATE()` | ✅ | ❌ | ⚠️ `TRUNC()` | ❌ | ⚠️ `TRUNC()` | ❌ |
| `MOD()` | ✅ | ⚠️ `%` only | ✅ | ⚠️ `%` only | ✅ | ⚠️ `MOD()` |
| `RAND()` | ✅ | ❌ | ⚠️ `RANDOM()` | ✅ | ⚠️ `DBMS_RANDOM.VALUE` | ⚠️ `Rnd()` |
| `GREATEST()` | ✅ | ❌ | ✅ | ❌ | ✅ | ❌ |
| `LEAST()` | ✅ | ❌ | ✅ | ❌ | ✅ | ❌ |
| `LOG()` | ✅ | ✅ | ✅ | ⚠️ base-10 default | ✅ | ❌ |

---

## 1.5. 📅 Date & Time Functions

> Work with date and time values.

| Function | Description | Syntax Example |
|----------|-------------|----------------|
| `NOW()` | Current date and time | `SELECT NOW();` → `2025-02-26 14:30:00` |
| `CURDATE()` | Current date only | `SELECT CURDATE();` → `2025-02-26` |
| `CURTIME()` | Current time only | `SELECT CURTIME();` → `14:30:00` |
| `DATE()` | Extract date from datetime | `SELECT DATE(created_at) FROM orders;` |
| `TIME()` | Extract time from datetime | `SELECT TIME(created_at) FROM orders;` |
| `YEAR()` | Extract year | `SELECT YEAR(birth_date) FROM users;` |
| `MONTH()` | Extract month (1–12) | `SELECT MONTH(order_date) FROM orders;` |
| `DAY()` | Extract day of month | `SELECT DAY(invoice_date) FROM invoices;` |
| `HOUR()` | Extract hour | `SELECT HOUR(login_time) FROM sessions;` |
| `MINUTE()` | Extract minute | `SELECT MINUTE(login_time) FROM sessions;` |
| `SECOND()` | Extract second | `SELECT SECOND(login_time) FROM sessions;` |
| `DAYNAME()` | Day name (Monday…) | `SELECT DAYNAME(order_date) FROM orders;` |
| `MONTHNAME()` | Month name (January…) | `SELECT MONTHNAME(order_date) FROM orders;` |
| `DAYOFWEEK()` | Day index (1=Sun) | `SELECT DAYOFWEEK(order_date) FROM orders;` |
| `WEEK()` | Week number | `SELECT WEEK(order_date) FROM orders;` |
| `DATE_FORMAT()` | Format a date | `SELECT DATE_FORMAT(NOW(), '%Y-%m-%d');` |
| `DATE_ADD()` | Add interval to date | `SELECT DATE_ADD(NOW(), INTERVAL 7 DAY);` |
| `DATE_SUB()` | Subtract interval from date | `SELECT DATE_SUB(NOW(), INTERVAL 1 MONTH);` |
| `DATEDIFF()` | Days between two dates | `SELECT DATEDIFF('2025-12-31', '2025-01-01');` → `364` |
| `TIMESTAMPDIFF()` | Difference in specified unit | `SELECT TIMESTAMPDIFF(YEAR, birth_date, NOW()) AS age FROM users;` |
| `STR_TO_DATE()` | Parse string to date | `SELECT STR_TO_DATE('26/02/2025', '%d/%m/%Y');` |
| `UNIX_TIMESTAMP()` | Date to Unix epoch | `SELECT UNIX_TIMESTAMP(NOW());` |
| `FROM_UNIXTIME()` | Unix epoch to datetime | `SELECT FROM_UNIXTIME(1708905600);` |
| `LAST_DAY()` | Last day of the month | `SELECT LAST_DAY('2025-02-01');` → `2025-02-28` |

### 1.5.1. Cross-Engine Compatibility

| Function | MySQL | SQLite | PostgreSQL | SQL Server | Oracle | MS Access |
|----------|-------|--------|------------|------------|--------|-----------|
| `NOW()` | ✅ | ⚠️ `datetime('now')` | ✅ | ⚠️ `GETDATE()` | ⚠️ `SYSDATE` | ⚠️ `Now()` |
| `CURDATE()` | ✅ | ⚠️ `date('now')` | ⚠️ `CURRENT_DATE` | ⚠️ `CAST(GETDATE() AS DATE)` | ⚠️ `TRUNC(SYSDATE)` | ⚠️ `Date()` |
| `DATE_FORMAT()` | ✅ | ⚠️ `strftime('%Y-%m-%d', col)` | ⚠️ `TO_CHAR(col, 'YYYY-MM-DD')` | ⚠️ `FORMAT(col, 'yyyy-MM-dd')` | ⚠️ `TO_CHAR()` | ⚠️ `Format()` |
| `DATEDIFF()` | ✅ | ⚠️ `julianday(d1) - julianday(d2)` | ⚠️ `col1 - col2` (returns interval) | ✅ different arg order | ⚠️ `col1 - col2` | ⚠️ `DateDiff()` |
| `DATE_ADD()` | ✅ | ⚠️ `datetime(col, '+7 days')` | ⚠️ `col + INTERVAL '7 days'` | ⚠️ `DATEADD(day, 7, col)` | ⚠️ `col + 7` | ⚠️ `DateAdd()` |
| `YEAR()` / `MONTH()` / `DAY()` | ✅ | ⚠️ `strftime('%Y', col)` | ⚠️ `EXTRACT(YEAR FROM col)` | ✅ | ⚠️ `EXTRACT(YEAR FROM col)` | ⚠️ `Year()` |
| `UNIX_TIMESTAMP()` | ✅ | ⚠️ `strftime('%s', col)` | ⚠️ `EXTRACT(EPOCH FROM col)` | ⚠️ `DATEDIFF(s,'1970-01-01',col)` | ❌ complex | ❌ |

---

## 1.6. ⚖️ Comparison & Logical Operators

> Filter and evaluate conditions.

| Operator / Function | Description | Syntax Example |
|---------------------|-------------|----------------|
| `=` | Equal | `WHERE status = 'active'` |
| `<>` / `!=` | Not equal | `WHERE status <> 'deleted'` |
| `>`, `<`, `>=`, `<=` | Numeric comparisons | `WHERE salary >= 50000` |
| `<=>` | NULL-safe equal | `WHERE col1 <=> col2` |
| `BETWEEN ... AND ...` | Range check | `WHERE price BETWEEN 10 AND 50` |
| `IN()` | Value in a list | `WHERE country IN ('US', 'UK', 'CA')` |
| `NOT IN()` | Value not in a list | `WHERE status NOT IN ('deleted', 'banned')` |
| `LIKE` | Pattern match (`%` wildcard) | `WHERE name LIKE 'John%'` |
| `NOT LIKE` | Pattern non-match | `WHERE email NOT LIKE '%@spam.com'` |
| `IS NULL` | NULL check | `WHERE phone IS NULL` |
| `IS NOT NULL` | Non-NULL check | `WHERE email IS NOT NULL` |
| `AND` / `&&` | Logical AND | `WHERE age > 18 AND active = 1` |
| `OR` | Logical OR | `WHERE role = 'admin' OR role = 'mod'` |
| `NOT` / `!` | Logical NOT | `WHERE NOT deleted` |
| `COALESCE()` | First non-NULL value | `SELECT COALESCE(phone, email, 'N/A') FROM users;` |
| `NULLIF()` | Returns NULL if equal | `SELECT NULLIF(score, 0) FROM results;` |
| `IF()` | Inline if/else | `SELECT IF(score >= 50, 'Pass', 'Fail') FROM results;` |
| `IFNULL()` | Replace NULL | `SELECT IFNULL(phone, 'Unknown') FROM users;` |
| `CASE` | Multi-condition logic | See below |

**CASE example:**
```sql
SELECT name,
  CASE
    WHEN score >= 90 THEN 'A'
    WHEN score >= 75 THEN 'B'
    WHEN score >= 60 THEN 'C'
    ELSE 'F'
  END AS grade
FROM students;
```

### 1.6.1. Cross-Engine Compatibility

| Function | MySQL | SQLite | PostgreSQL | SQL Server | Oracle | MS Access |
|----------|-------|--------|------------|------------|--------|-----------|
| `BETWEEN` / `IN` / `LIKE` | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `COALESCE()` | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `CASE` | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `IF()` | ✅ | ❌ | ❌ use `CASE` | ❌ | ❌ | ⚠️ `IIF()` |
| `IFNULL()` | ✅ | ✅ | ⚠️ `COALESCE()` | ⚠️ `ISNULL()` | ⚠️ `NVL()` | ⚠️ `Nz()` |
| `NULLIF()` | ✅ | ✅ | ✅ | ✅ | ✅ | ❌ |
| `<=>` NULL-safe equal | ✅ | ❌ | ⚠️ `IS NOT DISTINCT FROM` | ❌ | ❌ | ❌ |

---

## 1.7. 🪟 Window Functions

> Calculations across a set of rows related to the current row — no GROUP BY collapse.

| Function | Description | Syntax Example |
|----------|-------------|----------------|
| `ROW_NUMBER()` | Sequential row number | `SELECT ROW_NUMBER() OVER (ORDER BY salary DESC) AS rn FROM employees;` |
| `RANK()` | Rank with gaps | `SELECT RANK() OVER (PARTITION BY dept ORDER BY salary DESC) FROM employees;` |
| `DENSE_RANK()` | Rank without gaps | `SELECT DENSE_RANK() OVER (ORDER BY score DESC) FROM results;` |
| `NTILE(n)` | Divide into N buckets | `SELECT NTILE(4) OVER (ORDER BY salary) AS quartile FROM employees;` |
| `LAG()` | Previous row value | `SELECT LAG(sales, 1) OVER (ORDER BY month) AS prev_sales FROM revenue;` |
| `LEAD()` | Next row value | `SELECT LEAD(sales, 1) OVER (ORDER BY month) AS next_sales FROM revenue;` |
| `FIRST_VALUE()` | First value in window | `SELECT FIRST_VALUE(name) OVER (PARTITION BY dept ORDER BY salary DESC) FROM employees;` |
| `LAST_VALUE()` | Last value in window | `SELECT LAST_VALUE(name) OVER (PARTITION BY dept ORDER BY salary) FROM employees;` |
| `CUME_DIST()` | Cumulative distribution | `SELECT CUME_DIST() OVER (ORDER BY salary) FROM employees;` |
| `PERCENT_RANK()` | Relative rank 0–1 | `SELECT PERCENT_RANK() OVER (ORDER BY score) FROM results;` |

**Full example:**
```sql
SELECT
  name,
  dept,
  salary,
  RANK()       OVER (PARTITION BY dept ORDER BY salary DESC) AS dept_rank,
  SUM(salary)  OVER (PARTITION BY dept)                      AS dept_total,
  LAG(salary)  OVER (PARTITION BY dept ORDER BY salary DESC) AS prev_salary
FROM employees;
```

### 1.7.1. Cross-Engine Compatibility

| Function | MySQL | SQLite | PostgreSQL | SQL Server | Oracle | MS Access |
|----------|-------|--------|------------|------------|--------|-----------|
| `ROW_NUMBER()` | ✅ 8.0+ | ✅ 3.25+ | ✅ | ✅ | ✅ | ❌ |
| `RANK()` | ✅ 8.0+ | ✅ 3.25+ | ✅ | ✅ | ✅ | ❌ |
| `DENSE_RANK()` | ✅ 8.0+ | ✅ 3.25+ | ✅ | ✅ | ✅ | ❌ |
| `LAG()` / `LEAD()` | ✅ 8.0+ | ✅ 3.25+ | ✅ | ✅ | ✅ | ❌ |
| `FIRST_VALUE()` | ✅ 8.0+ | ✅ 3.25+ | ✅ | ✅ | ✅ | ❌ |
| `NTILE()` | ✅ 8.0+ | ✅ 3.25+ | ✅ | ✅ | ✅ | ❌ |

---

## 1.8. 🔁 Conversion & Type Functions

> Cast or convert between data types.

| Function | Description | Syntax Example |
|----------|-------------|----------------|
| `CAST()` | Convert to type | `SELECT CAST('42' AS UNSIGNED);` |
| `CONVERT()` | Convert value/charset | `SELECT CONVERT(price, CHAR);` |
| `HEX()` | To hexadecimal | `SELECT HEX(255);` → `FF` |
| `UNHEX()` | From hexadecimal | `SELECT UNHEX('FF');` |
| `BIN()` | To binary string | `SELECT BIN(10);` → `1010` |
| `OCT()` | To octal string | `SELECT OCT(8);` → `10` |
| `ASCII()` | ASCII code of char | `SELECT ASCII('A');` → `65` |
| `CHAR()` | Char from ASCII code | `SELECT CHAR(65);` → `A` |
| `TO_BASE64()` | Encode base64 | `SELECT TO_BASE64('hello');` |
| `FROM_BASE64()` | Decode base64 | `SELECT FROM_BASE64('aGVsbG8=');` |

### 1.8.1. Cross-Engine Compatibility

| Function | MySQL | SQLite | PostgreSQL | SQL Server | Oracle | MS Access |
|----------|-------|--------|------------|------------|--------|-----------|
| `CAST()` | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `CONVERT()` | ✅ | ❌ | ⚠️ `CAST` preferred | ✅ | ❌ | ❌ |
| `HEX()` | ✅ | ✅ | ⚠️ `TO_HEX()` | ⚠️ `CONVERT(VARBINARY...)` | ⚠️ `RAWTOHEX()` | ❌ |
| `ASCII()` | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `TO_BASE64()` | ✅ | ❌ | ⚠️ `encode(col,'base64')` | ❌ | ❌ | ❌ |

---

## 1.9. 🔐 Security & Hash Functions

| Function | Description | Syntax Example |
|----------|-------------|----------------|
| `MD5()` | MD5 hash | `SELECT MD5('password');` |
| `SHA1()` | SHA-1 hash | `SELECT SHA1('password');` |
| `SHA2()` | SHA-2 (224/256/384/512) | `SELECT SHA2('password', 256);` |
| `AES_ENCRYPT()` | AES encryption | `SELECT AES_ENCRYPT('secret', 'key');` |
| `AES_DECRYPT()` | AES decryption | `SELECT AES_DECRYPT(ciphertext, 'key');` |
| `UUID()` | Generate UUID | `SELECT UUID();` → `550e8400-e29b-41d4-a716...` |

### 1.9.1. Cross-Engine Compatibility

| Function | MySQL | SQLite | PostgreSQL | SQL Server | Oracle |
|----------|-------|--------|------------|------------|--------|
| `MD5()` | ✅ | ❌ | ✅ | ⚠️ `HASHBYTES('MD5', col)` | ❌ |
| `SHA2()` | ✅ | ❌ | ⚠️ `digest(col,'sha256')` pgcrypto | ⚠️ `HASHBYTES('SHA2_256', col)` | ❌ |
| `UUID()` | ✅ | ❌ | ⚠️ `gen_random_uuid()` | ⚠️ `NEWID()` | ⚠️ `SYS_GUID()` |

---

## 1.10. 📋 JSON Functions (MySQL 5.7+)

| Function | Description | Syntax Example |
|----------|-------------|----------------|
| `JSON_EXTRACT()` | Extract value by path | `SELECT JSON_EXTRACT(data, '$.name') FROM users;` |
| `->` | Shorthand for JSON_EXTRACT | `SELECT data->'$.name' FROM users;` |
| `->>`  | Extract + unquote result | `SELECT data->>'$.name' FROM users;` |
| `JSON_OBJECT()` | Create JSON object | `SELECT JSON_OBJECT('name', name, 'age', age) FROM users;` |
| `JSON_ARRAY()` | Create JSON array | `SELECT JSON_ARRAY(1, 2, 3);` |
| `JSON_SET()` | Insert or update path | `UPDATE t SET data = JSON_SET(data, '$.age', 30);` |
| `JSON_REMOVE()` | Remove a path | `UPDATE t SET data = JSON_REMOVE(data, '$.temp');` |
| `JSON_CONTAINS()` | Check if value exists at path | `SELECT JSON_CONTAINS(data, '"admin"', '$.role') FROM users;` |
| `JSON_ARRAYAGG()` | Aggregate rows as JSON array | `SELECT JSON_ARRAYAGG(name) FROM employees GROUP BY dept;` |
| `JSON_VALID()` | Validate JSON | `SELECT JSON_VALID('{"a":1}');` → `1` |

### 1.10.1. Cross-Engine Compatibility

| Function | MySQL | SQLite | PostgreSQL | SQL Server | Oracle |
|----------|-------|--------|------------|------------|--------|
| `JSON_EXTRACT()` | ✅ | ✅ `json_extract()` | ⚠️ `->>` operator | ⚠️ `JSON_VALUE()` | ⚠️ `JSON_VALUE()` |
| `JSON_OBJECT()` | ✅ | ✅ `json_object()` | ⚠️ `json_build_object()` | ⚠️ `FOR JSON PATH` | ✅ |
| `JSON_ARRAYAGG()` | ✅ 8.0+ | ❌ | ⚠️ `JSON_AGG()` | ⚠️ `FOR JSON PATH` | ✅ 12c+ |
| `JSON_VALID()` | ✅ | ✅ `json_valid()` | ⚠️ try casting | ⚠️ `ISJSON()` | ✅ 12c+ |

---

## 1.11. ⚡ NULL Handling — Quick Reference

```sql
-- Replace NULL with a default value
SELECT COALESCE(phone, 'N/A')    FROM users;   -- All engines ✅
SELECT IFNULL(phone, 'N/A')      FROM users;   -- MySQL, SQLite
SELECT ISNULL(phone, 'N/A')      FROM users;   -- SQL Server
SELECT NVL(phone, 'N/A')         FROM users;   -- Oracle
SELECT IIF(phone IS NULL, 'N/A', phone) FROM users; -- MS Access

-- Return NULL when two values are equal (avoid division by zero etc.)
SELECT NULLIF(score, 0) FROM results;   -- MySQL, PostgreSQL, SQL Server, SQLite

-- NULL-safe equality (never use = with NULLs!)
WHERE col IS NULL                        -- All engines ✅
WHERE col <=> NULL                       -- MySQL only
WHERE col IS NOT DISTINCT FROM NULL      -- PostgreSQL
```

---

## 1.12. 📐 Useful Patterns

### 1.12.1. Age Calculation
```sql
-- MySQL
SELECT TIMESTAMPDIFF(YEAR, birth_date, CURDATE()) AS age FROM users;

-- SQL Server
SELECT DATEDIFF(YEAR, birth_date, GETDATE()) AS age FROM users;

-- PostgreSQL
SELECT DATE_PART('year', AGE(birth_date)) AS age FROM users;

-- SQLite
SELECT (strftime('%Y','now') - strftime('%Y', birth_date)) AS age FROM users;
```

### 1.12.2. Running Total
```sql
SELECT
  order_date,
  amount,
  SUM(amount) OVER (
    ORDER BY order_date
    ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
  ) AS running_total
FROM orders;
```

### 1.12.3. Top N Per Group
```sql
SELECT * FROM (
  SELECT *,
    ROW_NUMBER() OVER (PARTITION BY dept ORDER BY salary DESC) AS rn
  FROM employees
) ranked
WHERE rn <= 3;
```

### 1.12.4. Conditional Aggregation (Pivot-style)
```sql
SELECT
  dept,
  SUM(CASE WHEN gender = 'M' THEN salary END) AS male_total,
  SUM(CASE WHEN gender = 'F' THEN salary END) AS female_total
FROM employees
GROUP BY dept;
```

### 1.12.5. Deduplicate — Keep Latest Row
```sql
DELETE FROM orders
WHERE id NOT IN (
  SELECT MAX(id) FROM orders GROUP BY order_ref
);
```

---

*Based on MySQL 8.x built-in function reference. Version requirements noted where applicable.*
