## Table of Contents
1. [[#Introduction to SQL]]
2. [[#Section 1 Data Definition Language (DDL)]]
3. [[#Section 2 Data Manipulation Language (DML)]]
4. [[#Section 3 Data Query Language (DQL)]]
5. [[#Section 4 Data Control Language (DCL)]]
6. [[#Section 5 Transaction Control Language (TCL)]]
7. [[#Section 6 Subqueries]]
8. [[#Section 7 Joins]]
9. [[#Section 8 Set Operations]]
10. [[#Section 9 Aggregate & String Functions]]
11. [[#Section 10 Window / Analytical Functions]]
12. [[#Section 11 Date Functions]]
13. [[#Section 12 Views & Temp Tables]]
14. [[#Section 13 Indexes, Synonyms & Sequences]]
15. [[#Section 14 Constraints]]
16. [[#Section 15 Functions & CTEs]]
17. [[#Section 16 Stored Procedures & Triggers]]
18. [[#Section 17 Data Dictionary Views - Oracle]]

## Introduction to SQL
Structured Query Language (SQL) is the standard language for managing and manipulating relational databases. It is used to perform tasks such as retrieving data, inserting new records, updating existing ones, and deleting data. SQL commands are traditionally categorized into several groups, which define their role in the database.
#### Database Objects:
1. **Table**: Acts as a basic unit of storage that is composed of rows & columns.
2. **View**: Logically represents the subsets of data from one or more table.
3. **Sequence**: Is a numeric value generator (Oracle).
4. **Index**: Improves performance of queries on large tables.
5. **Synonym**: Give alternative names to Objects (Oracle).

> [!important] Things to Remember About Writing SQL:
> 1. Not Case-Sensitive, unless indicated.
> 2. May be entered on 1 or more lines, however keywords cannot be split.
> 3. Place Clauses on separate lines for readability.
> 4. Use indents for subqueries and inline queries for better readability.
> 5. Lowercase For: database object names (table names, column names)
> 6. Uppercase For: Keywords, Clauses & Functions

> [!seealso] Resources For Practice:
> Find Leetcode (Basic) SQL Top 50 Problems [here](https://leetcode.com/studyplan/top-sql-50/)
> More SQL Practice Problems on HackerRank [here](https://www.hackerrank.com/domains/sql)
> Find Notes on DBMS Concepts [here](https://takeuforward.org/dbms/most-asked-dbms-interview-questions)
> Find external notes for SQL [here](https://www.w3schools.com/sql/)

## Section 1: Data Definition Language (DDL)
DDL commands are used to define and manage the structure of your database and its objects, such as tables, indexes, and views. These commands are foundational, as they build the framework where your data will live. (CREATE, ALTER, DROP, TRUNCATE)

> [!tip] Tips for DDL Statements:
> - Use DDL to set up your database schema from scratch or to modify it as your application's needs evolve.
> - Be cautious with `DROP` and `TRUNCATE`, as they can lead to irreversible data loss. `DROP` removes the entire table structure, while `TRUNCATE` only removes all rows. These cannot be rolled back.
> - `TRUNCATE` is generally faster than `DELETE` for clearing a table because it deallocates the data pages with minimal logging, whereas `DELETE` removes rows one by one and logs each deletion.

### Databases:
##### 1. CREATE DATABASE
```mysql
CREATE DATABASE company;
```
##### 2. SHOW DATABASE
```mysql
SHOW DATABASES;
```
##### 3. USE DATABASE 
```mysql
USE company;
```
##### 4. ALTER DATABASE
```mysql
ALTER DATABASE company MODIFY NAME = companies;
```
##### 5. DROP DATABASE
```mysql
DROP DATABASE company;
```

### Tables:
##### 1. CREATE TABLE
```mysql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50),
    hire_date DATE,
    salary DECIMAL(10, 2)
);
```

##### 2. SHOW TABLE
```mysql
SHOW TABLES;
```

##### 3. DESCRIBE TABLE
```mysql
DESC employees;
```

##### 4. ALTER TABLE
**Add a column:**
```mysql
ALTER TABLE employees ADD email VARCHAR(100);
```

**Modify a column:**
```mysql
ALTER TABLE employees MODIFY COLUMN salary DECIMAL(12, 2);
```

**Rename a column:**
```mysql
ALTER TABLE employees RENAME COLUMN salary TO income;
```

**Drop a column:**
```mysql
ALTER TABLE employees DROP COLUMN email;
```

##### 5. RENAME TABLE
```mysql
RENAME TABLE employees TO employee_details;
```

##### 6. DROP TABLE
```mysql
DROP TABLE employees;
```

##### 7. TRUNCATE TABLE
```mysql
TRUNCATE TABLE employees;
```

## Section 2: Data Manipulation Language (DML)
DML commands are used to manage the data within your database tables. These are the most frequently used commands in day-to-day operations. (INSERT, UPDATE, DELETE)

> [!tip] Tips for DML Statements:
> - Always use a `WHERE` clause with `UPDATE` and `DELETE` statements unless you intend to modify every single row in the table. Forgetting the `WHERE` clause is a common and dangerous mistake.
> - Wrap related DML operations in a transaction (using `BEGIN TRANSACTION`, `COMMIT`, `ROLLBACK`) to ensure data integrity. If one part of the operation fails, you can roll back the entire set of changes.

##### 1. INSERT
```mysql
INSERT INTO employees (employee_id, first_name, last_name, hire_date, salary)
VALUES (1, 'John', 'Doe', '2023-01-15', 50000.00);

INSERT INTO employees VALUES (1, 'John', 'Doe', '2023-01-15', 50000.00);

INSERT INTO employees SELECT * FROM employees_bkp;
```

##### 2. UPDATE
```mysql
-- update a column for only a certain number of records
UPDATE employees
SET salary = 55000.00
WHERE employee_id = 1;

-- update multiple columns for all records
UPDATE CUSTOMERS SET AGE = AGE+5, SALARY = SALARY+3000;
```

##### 3. DELETE
```mysql
DELETE FROM employees
WHERE employee_id = 1;

-- delete all data from the table (slow but can rollback)
DELETE FROM employees;
```

## Section 3: Data Query Language (DQL)
DQL is used to retrieve data from the database. The `SELECT` statement is the cornerstone of SQL, allowing for powerful and complex data retrieval. (SELECT)

> [!tip] Tips for DQL Statements:
> - **Performance:** Avoid using `SELECT *` in production code. Explicitly name the columns you need. This reduces the amount of data transferred and can sometimes allow the database to use more efficient query plans (like index-only scans).
> - **Readability:** Use aliases (`AS`) for columns and tables, especially in complex queries with joins, to make your code much easier to understand.
> - **Filtering:** Apply `WHERE` clauses as early as possible in your query to filter the dataset. The less data subsequent operations (like joins or aggregations) have to process, the faster your query will be.

### Basic Composition of Select
##### 1. SELECT
```mysql
-- Show all records
SELECT * FROM employees;

-- Show specific columns
SELECT first_name, last_name, salary FROM employees;

-- using AS keyword to rename column while displaying
SELECT first_name AS Name FROM employees;
```

##### 2. FROM
```plsql
SELECT * FROM employees;

-- multiple tables
SELECT s.student_name, c.courses FROM students s, courses c;
```

##### 2. WHERE
```mysql
SELECT * FROM employees
WHERE salary > 50000; -- condition for selection
```

### Logical Operators
##### 3. IF
Returns second argument if condition is True, 3rd argument if False.
```mysql
SELECT IF(500<1000, "YES", "NO");

SELECT OrderID, Quantity, IF(Quantity>10, "MORE", "LESS") AS Threshold
FROM OrderDetails;
```

##### 4. CASE
Matches multiple conditions
```mysql
SELECT employee_id, salary,
  CASE
    WHEN salary >= 100000 THEN 'High'
    WHEN salary >= 50000 THEN 'Medium'
    ELSE 'Low'
  END AS salary_range
FROM employees;
```

##### 5. EXISTS
Set True if subquery returns at least 1 record
```mysql
SELECT SupplierName FROM Suppliers  
WHERE EXISTS (SELECT ProductName FROM Products WHERE Products.SupplierID = Suppliers.supplierID AND Price < 20);
```

##### 6. IN & NOT IN 
Set True if operand is a member in the list of expressions
```mysql
SELECT * from CUSTOMERS WHERE NAME IN ('Khilan', 'Hardik', 'Muffy');

SELECT * from CUSTOMERS WHERE AGE NOT IN (25, 23, 22);
```

##### 7. AND & OR
Equivalent to logical AND and OR
```mysql
SELECT * FROM CUSTOMERS 
WHERE (AGE = 25 OR salary < 4500) AND (name = 'Komal' OR name = 'Kaushik');
```

##### 8. ANY & ALL
Set True if any of the subquery values meet the condition
Set True if all of the subquery values meet the condition
```mysql
SELECT product_id, product_name, unit_price 
FROM Product
WHERE unit_price > ANY (SELECT price FROM Sales WHERE seller_id = 1);

SELECT product_id, product_name, unit_price 
FROM Product 
WHERE unit_price > ALL (SELECT price FROM Sales WHERE seller_id = 1 );
```

##### 9. BETWEEN
Set True if operand is within the range (inclusive)
```mysql
SELECT * FROM Products 
WHERE Price BETWEEN 10 AND 20;
```

##### 9. COALESCE
Returns value if not null else returns 2nd argument as fallback
```mysql
SELECT name, COALESCE(phone, 'Not Provided') AS contact_info 
FROM users;
```

##### 11. LIKE / ILIKE
Set True if the operand matches a pattern
```postgresql
SELECT * FROM customers WHERE name LIKE 'K___%';

SELECT * FROM customers WHERE name ILIKE 'K___%';

SELECT * FROM customers WHERE REGEXP_LIKE (name, 'K___%', 'i');

/* wildcards
_ - matches a single character
% - matches zero, one or more characters
i - character insensitive indicator
*/
```

##### 12. REGEXP & RLIKE
Set True if operand matches the regular expression
```mysql
SELECT DISTINCT city 
FROM station 
WHERE city REGEXP '^[AEIOUaeiou]';

/* patterns
^      → Start of string
$      → End of string
.      → Any single character
[abc]  → Matches a, b, or c
[^abc] → Matches anything except a, b, or c
[a-z]  → Range: a through z
*      → 0 or more of the preceding token
+      → 1 or more of the preceding token (not in MySQL REGEXP)
{n,m}  → n to m repetitions (not in MySQL REGEXP)
()     → Group expressions (limited in MySQL REGEXP)
|      → Alternation (A or B)
*/
```

##### 13. ORDER BY
Order the result in ASC (Default), DESC orders
```mysql
SELECT * FROM employees
ORDER BY salary DESC;
```

##### 14. LIMIT & TOP / ROWNUM
Restricts the selection to x number of records returned
```mysql
SELECT * FROM employees
LIMIT 10;

SELECT TOP 4 * FROM employees;

SELECT TOP 4 * FROM CUSTOMERS ORDER BY SALARY DESC;

SELECT TOP 40 PERCENT * FROM CUSTOMERS ORDER BY SALARY;
```

```plsql
SELECT * FROM employees FETCH FIRST 3 ROWS ONLY;

SELECT * FROM employees ROWNUM = 1;
-- or
SELECT * FROM (SELECT * FROM employees ORDER BY salary DESC)
WHERE ROWNUM <= 5;

-- ROWNUM cannot be used after order by clause and needs a subquery in oracle
-- FETCH ROWS is very new and does not work in older instances of oracle
```

##### 15. DISTINCT
Returns only Unique records
```mysql
SELECT DISTINCT department FROM employees;

SELECT COUNT(DISTINCT AGE) as UniqueAge FROM CUSTOMERS;
```

##### 16. CONCAT
Concatenate values together
```plsql
SELECT CONCAT(CONCAT(name,' '),age) AS details FROM customers ORDER BY name;
-- OR
SELECT name || ' ' || age AS details FROM customers ORDER BY name;
```

##### 17. CAST & CONVERT
Convert compatible data types to a different data type
```plsql
SELECT CAST(salary AS CHAR) AS salary_string
FROM employees;
-- OR
SELECT CONVERT(salary, CHAR) AS salary_string
FROM employees;
```

## Section 4: Data Control Language (DCL)

##### 1. GRANT
Grants a user or role the specified permission on specified resource
```plsql
CREATE USER user1 IDENTIFIED BY user1; -- username : password
CREATE ROLE role1;

GRANT CREATE SESSION TO user1, user2;
GRANT SELECT, INSERT ON employees TO user1, user2;
GRANT SELECT, UPDATE, INSERT ON employees TO role1;
GRANT RESOURCE TO role1;
```

##### 2. REVOKE
Revokes a user or role's permission on specified resource
```mysql
REVOKE INSERT ON employees FROM user1;
DROP ROLE role1;
DROP USER user1;
```

## Section 5: Transaction Control Language (TCL)
TCL commands are used to manage transactions in the database, ensuring that a series of operations are treated as a single, atomic unit. This is critical for maintaining data integrity.

> [!tip] Tips for TCL Statements:
> - Transactions are essential for operations that require multiple steps, like transferring money between two accounts (a debit from one and a credit to another). If either step fails, the entire transaction can be rolled back, leaving the database in a consistent state.
> - `SAVEPOINT` is useful for complex transactions where you might want to undo only a portion of the work without rolling back the entire transaction.

##### 1. BEGIN TRANSACTION
Begin a transaction (Block of DML Statments)
```mysql
BEGIN TRANSACTION;
```

##### 2. COMMIT
Commit a transaction (change)
```mysql
COMMIT;
```

##### 3. ROLLBACK
Rollback to a previous commit or savepoint
```mysql
ROLLBACK;
```

##### 4. SAVEPOINT
Save as a temporary rollback point without committing the changes
```plsql
SAVEPOINT name_of_point;

ROLLBACK TO name_of_point;
```

## Section 6: Subqueries
These are methods for nesting queries within other queries, which is essential for performing complex, multi-step logic. Types of Subqueries: Single-Row, Multiple-Row, Inline, Correlated.

> [!tip] Tips for Writing Subqueries:
> - **Subquery vs. Join:** Often, a subquery can be rewritten as a `JOIN`, which can be more readable and sometimes more performant. However, subqueries are very powerful, especially with operators like `IN`, `NOT IN`, `EXISTS`, and `NOT EXISTS`.
> - **Performance:** For checking existence, `EXISTS` is generally more efficient than `IN` because it stops processing as soon as it finds a match, whereas `IN` may need to scan the entire subquery result.  
> - **Readability:** For complex queries, always prefer CTEs over nested subqueries. They break the logic into named, sequential steps, making the query vastly easier to read, debug, and maintain.

### Types of Sub-Queries:
##### 1. Single-Row Subquery
```plsql
SELECT * FROM employees 
WHERE salary > (SELECT AVG(salary) FROM employees);
```

##### 2. Multiple-Row Subquery
```plsql
SELECT * FROM employees 
WHERE salary > ANY(SELECT AVG(salary) FROM employees GROUP BY department_id);

-- or multi-column & rows
SELECT * FROM employees 
WHERE (department_id, salary) IN (SELECT department_id, MAX(salary) 
									FROM employees GROUP BY department_id);
```

##### 3. Inline Subquery
```plsql
SELECT employee_id, first_name, last_name, salary, 
(SELECT MAX(salary) FROM employees) AS avg_salary 
FROM employees;
```

##### 4. Correlated Subquery
```plsql
SELECT ename, sal, deptno 
FROM emp e1 
WHERE e1.sal > (SELECT AVG(e2.sal) 
				FROM emp e2 
				WHERE e1.deptno = e2.depthno);
				
-- example 2
SELECT employee_id, first_name, salary, 
(SELECT SUM(salary) FROM employees WHERE employee_id <= x.employee_id) AS total
FROM employees x
ORDER BY employee_id;
```

### Subquery Examples:
##### 1. Subquery in WHERE clause
```mysql
SELECT first_name, last_name
FROM employees
WHERE department_id IN (SELECT department_id FROM departments WHERE location_id = 1700);
```

##### 2. Subquery in SELECT clause
```mysql
SELECT e.first_name, e.last_name,
       (SELECT AVG(salary) FROM employees WHERE department_id = e.department_id) AS dept_avg_salary
FROM employees e;
```

##### 3. Subquery in UPDATE clause
```mysql
UPDATE CUSTOMERS SET SALARY = SALARY * 0.25
WHERE AGE IN (SELECT AGE FROM CUSTOMERS_BKP WHERE AGE >= 27 );
```

## Section 7: Joins
Joins are fundamental to relational databases. They are used to combine rows from two or more tables based on a related column between them, allowing you to query data across your entire schema.  

> [!tip] Tips for Joining Tables:
> - **Choosing the Right Join:** `INNER JOIN` is for when you only want records that exist in both tables. `LEFT JOIN` is perfect when you want all records from the "left" table, regardless of whether they have a match in the "right" table (e.g., finding all customers and their orders, even if a customer has no orders).
> - **Performance:** Ensure that the columns used in your `ON` clause are indexed. Joining on indexed columns is significantly faster than joining on unindexed ones.
> - **Readability:** Always use table aliases when joining multiple tables to keep your query clean and avoid ambiguity with column names.

##### 1. INNER JOIN
= (A ∩ B): Only records common to both
```mysql
SELECT e.first_name, e.last_name, d.department_name
FROM employees e
JOIN departments d ON e.department_id = d.department_id;
```

##### 2. LEFT OUTER JOIN
= A ∪ (A ∩ B): All records from A but only common from B
```mysql
SELECT e.first_name, e.last_name, d.department_name
FROM employees e
LEFT JOIN departments d ON e.department_id = d.department_id;
```

##### 3. RIGHT OUTER JOIN
= B ∪ (A ∩ B) Only common records from A but all from B
```mysql
SELECT e.first_name, e.last_name, d.department_name
FROM employees e
RIGHT JOIN departments d ON e.department_id = d.department_id;
```

##### 4. FULL OUTER JOIN
= (A ∪ B) All records from both A and B
```mysql
SELECT employees.emp_name, salaries.salary FROM employees 
FULL JOIN salaries ON employees.emp_id = salaries.emp_id;
```

##### 5. CROSS JOIN
= (A × B) Every record from A matched with every record from B
```mysql
SELECT e.first_name, e.last_name, d.department_name
FROM employees e
CROSS JOIN departments d ON e.department_id = d.department_id;
```

## Section 8: Set Operations
Set operators combine the results of two or more `SELECT` statements into a single result set. While joins combine tables horizontally based on columns, set operators combine results vertically based on rows.  

> [!tip] Tips about Set Operations
> - **`UNION` vs. `UNION ALL`:** `UNION` removes duplicate rows from the combined result set, which requires a sorting operation behind the scenes. `UNION ALL` includes all rows, including duplicates, and is therefore much faster. If you know your combined results won't have duplicates or if duplicates are acceptable, always use `UNION ALL` for better performance.
> - **Requirements:** The `SELECT` statements involved must have the same number of columns, and the corresponding columns must have compatible data types.

##### 1. UNION & UNION ALL
Union Merges 2 or more tables and returns combined table (columns must be same) without duplicates. Union All returns combined table along with duplicate records.
```mysql
SELECT name FROM students
UNION
SELECT name FROM teachers;

SELECT name FROM students
UNION ALL
SELECT name FROM teachers;
```

##### 2. INTERSECT
Returns records which are common in both tables;
```mysql
SELECT name FROM students
INTERSECT
SELECT name FROM teachers;
```

##### 3. EXCEPT
```postgresql
SELECT name FROM students
EXCEPT
SELECT name FROM teachers;
```

##### 4. MINUS
Combine rows from both and returns only those in first table but not in second
```plsql
SELECT employee_id, job_id, FROM employees
MINUS
SELECT employee_id, job_id FROM job_history;
```

## Section 9: Aggregate & String Functions
These commands are used to summarize data. `GROUP BY` collapses multiple rows into a single summary row, and aggregate functions perform a calculation on a set of values to return a single value.  

> [!tip] Tips on Aggregate & String Functions:
> - **`WHERE` vs. `HAVING`:** This is a critical distinction. `WHERE` filters rows _before_ any grouping or aggregation occurs. `HAVING` filters groups _after_ the aggregation has been performed. You cannot use an aggregate function in a `WHERE` clause.
> - **Multi-column Grouping:** You can group by multiple columns to get more granular aggregations (e.g., `GROUP BY country, city`).

### General Functions:
##### 1. NVL
Allows to replace Null with an expression
```plsql
SELECT NVL(commission, 0) FROM employees;
```

##### 2. NULLIF
Compares 2 args and returns Null if they are equal else returns 1st argument
```plsql
SELECT NULLIF(TO_CHAR(10), '20') FROM dual;
```

##### 3. NVL2
Returns 2nd argument if not null else returns 3rd argument
```plsql
SELECT NVL2(department_id, 0, 1) FROM employees;
```

### String Functions:
##### 1. LOWER
Converts string to lowercase
```mysql
SELECT LOWER('ABC') FROM dual;
```

##### 2. UPPER
Converts string to uppercase
```mysql
SELECT UPPER('abc') FROM dual;
```

##### 3. INSTR
Searches a string for a substring, returns position of substring from start point
```plsql
SELECT INSTR('Something Specific', 'S', 1, 1) FROM dual;
```

##### 4. SUBSTR
Returns portion of characters based on start and length
```plsql
SELECT SUBSTR('This is a test sentence', 1, 5) FROM dual;
```
```mysql
-- alternatives for mysql
SELECT LEFT('This is a test sentence', 1) FROM dual; -- 'T'
SELECT RIGHT('This is a test sentence', 1) FROM dual; -- 'e'
```

##### 5. LENGTH
```mysql
SELECT * FROM Tweets WHERE LENGTH(content) > 15;
```

### Aggregate Functions:
##### 1. COUNT
```mysql
SELECT COUNT(*) FROM employees;
```

##### 2. SUM
```mysql
SELECT SUM(salary) FROM employees;
```

##### 3. AVG
```mysql
SELECT AVG(salary) FROM employees;
```

##### 4. MAX
```mysql
SELECT MAX(salary) FROM employees;
```

##### 5. MIN
```mysql
SELECT MIN(salary) FROM employees;
```

##### 6. ROUND
```mysql
SELECT ProductName, ROUND(Price, 2) AS RoundedPrice  
FROM Products;
```

##### 7. GROUP BY
```mysql
SELECT department_id, AVG(salary)
FROM employees
GROUP BY department_id

SELECT AGE, MIN(SALARY) AS MIN_SALARY 
FROM CUSTOMERS 
GROUP BY AGE 
ORDER BY MIN_SALARY DESC;
```

##### 8. HAVING
```mysql
SELECT department_id, AVG(salary)
FROM employees
GROUP BY department_id
HAVING AVG(salary) > 50000;
```

## Section 10: Window / Analytical Functions
Window functions perform calculations across a set of rows that are related to the current row. Unlike aggregate functions, they do not collapse rows; they return a value for each row based on the "window" of data defined by the `OVER()` clause.  

> [!tip] Tips About Using Window Functions:
> - **Running Totals & Moving Averages:** Use `SUM() OVER (...)` or `AVG() OVER (...)` to calculate metrics that accumulate or average over a specific window of rows.
> - **Ranking:** `ROW_NUMBER()` gives a unique number to each row. `RANK()` gives the same rank to tied values but leaves gaps. `DENSE_RANK()` gives the same rank to tied values but does not leave gaps. Choose the one that fits your specific ranking logic.
> - **Comparing to Previous/Next Rows:** `LAG()` and `LEAD()` are incredibly useful for comparing a row's value to the value in the preceding or following row, respectively (e.g., calculating day-over-day growth).

##### 1. ROW NUMBER
Assigns a unique number to each row beginning with 1 in order specified.
```postgresql
SELECT employee_id, department_id, salary, 
ROW_NUMBER() OVER (PARTITION BY department_id ORDER BY salary DESC) AS rn
FROM employees;
```

##### 2. RANK
Assigns a rank according to the sort specification, but gives the same rank to duplicate and skips that many ranks for the next. I.e. preserves total row number.
```postgresql
SELECT employee_id, department_id, salary, 
RANK() OVER (PARTITION BY department_id ORDER BY salary DESC) AS rk
FROM employees;
```

##### 3. DENSE RANK
Similar to rank but doesn't skip ranks in case of a tie.
```postgresql
SELECT employee_id, department_id, salary, 
DENSE_RANK() OVER (PARTITION BY department_id ORDER BY salary DESC) AS drk
FROM employees;
```

##### 4. LAG
Read from the pervious nth row
```postgresql
SELECT employee_id, department_id, salary, 
LAG(salary, 1, 0) OVER (PARTITION BY department_id ORDER BY salary) AS prev_salary
FROM employees;
```

##### 5. LEAD
Read from the next nth row
```postgresql
SELECT employee_id, department_id, salary, 
LEAD(salary, 1, 0) OVER (PARTITION BY department_id ORDER BY salary) AS next_salary
FROM employees;
```

##### 6. FIRST_VALUE
Used to return the first value from an ordered sequence
```postgresql
SELECT dept_id, first_name, salary,
FIRST_VALUE(salary) OVER (PARTITION BY dept_id ORDER BY salary DESC) AS max_sal
FROM employees;
```

##### 7. LAST_VALUE
Used to return the last value from an ordered sequence
```postgresql
SELECT dept_id, first_name, salary,
LAST_VALUE(salary) OVER (PARTITION BY dept_id ORDER BY salary) AS max_sal
FROM employees;
```

##### 8. LISTAGG
Used for string aggregation of a given sequence of strings
```postgresql
SELECT department_id, 
LISTAGG(first_name, ',') WITHIN GROUP (ORDER BY first_name) AS employee_names
FROM employees
GROUP BY department_id;
```

## Section 11: Date Functions
Date functions are essential for manipulating and querying temporal data. They allow you to extract components from dates, perform arithmetic, and format them for display. Syntax often varies between SQL dialects (like MySQL, PostgreSQL, and SQL Server).  

> [!tip] Tips on Handling Dates:
> - **Time-based Filtering:** Use date functions in `WHERE` clauses to filter records within a specific time frame, such as the last 30 days or the current month.  
> - **Reporting and Grouping:** `EXTRACT` or `DATE_TRUNC` are powerful for grouping data by month, year, or quarter to create summary reports.  
> - **Calculating Durations:** `DATEDIFF` is perfect for calculating user age, subscription length, or the time between two events.

##### 1. CURRENT DATE & TIME
```mysql
SELECT CURDATE();  -- current date
SELECT CURTIME();  -- current time
SELECT NOW();      -- current date & time of the user session location
SELECT SYSDATE();  -- current date & time of the server's OS location

/* Date types
- `DATE` - format YYYY-MM-DD
- `DATETIME` - format: YYYY-MM-DD HH:MI:SS
- `TIMESTAMP` - format: YYYY-MM-DD HH:MI:SS+TIMEZONE
*/

/* Date Formats 
DD - Numeric day of the month
DY - Abbreviation of day of the week
DAY - Full name of day of the week
W - Week of the month
WW - Week of the year
MM - Numeric month of the year
MON - Abbreviation of the month
MONTH - Full name of the month
Q - Quarter of the year
YY - Last 2 digits of the year
YYYY - Full year in numbers
YEAR - Full Year spelled out
CC - current century
BC/AD - B.C. or A.D, indicator
HH - Numeric hours
MI - Numeric minutes
SS - Numeric seconds
*/
```

##### 2. DATE_FORMAT
```mysql
SELECT DATE_FORMAT(NOW(), '%Y-%m-%d') AS formatted_date;
```

##### 3. DATE_ADD
```mysql
-- Add 10 days to the current date
SELECT DATE_ADD(CURDATE(), INTERVAL 10 DAY) AS future_date;

-- Add 2 months to a specific date
SELECT DATE_ADD('2025-07-26', INTERVAL 2 MONTH);
```

##### 4. DATEDIFF
```mysql
SELECT DATEDIFF('2025-12-31', '2025-01-01') AS days_difference;
```

##### 5. EXTRACT
```postgresql
SELECT EXTRACT(YEAR FROM hire_date) AS hire_year FROM employees;

/* terms that can be extracted
MICROSECOND, SECOND, MINUTE, HOUR, DAY, WEEK, MONTH, QUARTER, YEAR
*/
```

##### 6. MONTHS BETWEEN
```plsql
SELECT MONTHS_BETWEEN(SYSDATE, hire_date) FROM dual;
```

## Section 12: Views & Temp Tables
A view is a virtual table based on the result-set of a stored SQL query. It contains rows and columns, just like a real table, but does not store the data itself. Views are used to simplify complex queries, provide a layer of security, and ensure data consistency.  

> [!tip] Tips on View & Temp Tables:
> - **Simplification:** Encapsulate a complex join or calculation into a view. This allows end-users to query the view with a simple `SELECT` statement without needing to understand the underlying complexity.
> - **Security:** Grant users access to a view that only exposes certain columns or rows, thereby restricting their access to sensitive data in the underlying tables.  
> - **Maintenance:** If the logic of a complex query needs to change, you only need to update the view definition (`ALTER VIEW`), and all applications using the view will automatically get the new logic.

### Views:
##### 1. Create View
```mysql
CREATE OR REPLACE VIEW high_salary_employees AS
SELECT * FROM employees WHERE salary > 70000;
```

##### 2. Query View
```mysql
SELECT * FROM high_salary_employees;
```

##### 3. Update View
```mysql
UPDATE high_salary_employees
SET salary = 85000 WHERE name = 'Ramesh';
```

##### 4. Drop View
```mysql
DROP VIEW high_salary_employees;
```

##### 5. MATERIALIZED VIEWS
**Note:** Not available in MySQL, Only in PostgreSQL / RedshiftSQL / Oracle
```postgresql
CREATE MATERIALIZED VIEW emp_summary AS
SELECT department_id, AVG(salary) AS avg_salary
FROM employees
GROUP BY department_id;

-- Refresh
REFRESH MATERIALIZED VIEW emp_summary;

-- Drop
DROP MATERIALIZED VIEW emp_summary;
```

### Temp Tables:
It is a table that exists for a brief period of time, generally contains a subset of data from a regular table. It is used to store and process intermediate results. It is automatically deleted when the session is ended.
##### 1. Create Temp Table
```plsql
CREATE GLOBAL TEMPORARY TABLE temp_employees (
    emp_id INT,
    emp_name VARCHAR2(50)
) ON COMMIT DELETE ROWS;

-- MySQL
CREATE TEMPORARY TABLE temp_sales AS
SELECT * FROM sales WHERE region = 'Asia';

/*
SCOPE:
GLOBAL - Across sessions
LOCAL - Session specific

ON COMMIT:
DELETE ROWS - deletes rows after commit
PRESERVE ROWS - keeps rows until session is ended
*/
```

## Section 13: Indexes, Synonyms & Sequences
These are database objects used to enforce data integrity and improve query performance, and help with DQL statements.

> [!tip] Tips on Indexes
> - **Performance:** Indexes are the single most important factor in query performance. They allow the database to find rows with specific column values quickly without scanning the entire table. Create indexes on columns that are frequently used in `WHERE` clauses and `JOIN` conditions.

### Indexes:
##### 1. Create Index
```mysql
CREATE INDEX idx_last_name ON employees(last_name);
```

##### 2. Drop Index
```mysql
DROP INDEX idx_last_name ON employees;
```

### Synonyms:
##### 1. Create Synonyms:
```plsql
CREATE SYNONYM EMP FOR employees;
-- or
CREATE PUBLIC SYNONYM EMP FOR employees;
```

##### 2. Drop Synonyms:
```plsql
DROP SYNONYM EMP;
```

### Sequences:
Sequence is used to produce a unique sequence of numeric values in a series according to specified specifications. It is user-defined schema object. It is not associated with any table.
##### 1. Create Sequence
```plsql
-- syntax
CREATE SEQUENCE name_of_sequence (
	[ START WITH initial_value ]
	[ INCREMENT BY incremental_value ]
	[ MAXVALUE {max_value} | NO MAXVALUE ]
	[ MINVALUE {min_value} | NO MINIVALUE ]
	[ CACHE {size_of_cache} | NOCACHE ]
	[ CYCLE | NOCYCLE ];
);

-- example
CREATE SEQUENCE seq1 (
	START WITH 1
	INCREMENT BY 3
	MAXVALUE 30
	NOCACHE
	NOCYCLE
);

INSERT INTO employees (emp_id, emp_name)
VALUES (seq1.NEXTVAL, 'John Doe'); -- get the next value in the sequence

-- Get current value
SELECT seq1.CURRVAL FROM dual; -- get the current value in the sequence
```

## Section 14: Constraints

> [!tip] Tips on Constraints
> - **Data Integrity:** Constraints are rules that prevent invalid data from being entered into your tables. A `PRIMARY KEY` (which is both `UNIQUE` and `NOT NULL`) is essential for uniquely identifying each row. A `FOREIGN KEY` is crucial for maintaining referential integrity between tables.

##### 1. Primary Key
```mysql
-- Create primary key for single column
CREATE TABLE Persons (  
    ID int NOT NULL,  
    LastName varchar(255) NOT NULL,  
    FirstName varchar(255),  
    Age int,  
    CONSTRAINT persons_id_pk PRIMARY KEY (ID)  
);
-- or
CREATE TABLE Persons (  
    ID int PRIMARY KEY,  
    LastName varchar(255) NOT NULL,  
    FirstName varchar(255),  
    Age int  
);
-- Primary key made up of multiple columns
CREATE TABLE Persons (  
    ID int NOT NULL,  
    LastName varchar(255) NOT NULL,  
    FirstName varchar(255),  
    Age int,  
    CONSTRAINT persons_pk PRIMARY KEY (ID,LastName)  
);

-- adding primary key after table is created
ALTER TABLE persons ADD PRIMARY KEY (ID);
-- or
ALTER TABLE persons ADD CONSTRAINT persons_pk PRIMARY KEY (ID,LastName);

-- dropping a primary key
ALTER TABLE persons DROP PRIMARY KEY;
-- or
ALTER TABLE persons DROP CONSTRAINT persons_pk;
```

##### 2. Foreign Key
```mysql
-- adding a single foreign key
CREATE TABLE Orders (  
    OrderID int PRIMARY KEY,  
    OrderNumber int NOT NULL,  
    PersonID int,
    CONSTRAINT orders_persons_fk FOREIGN KEY (PersonID) REFERENCES persons(PersonID)  
);
-- or
CREATE TABLE Orders (  
    OrderID int NOT NULL PRIMARY KEY,  
    OrderNumber int NOT NULL,  
    PersonID int FOREIGN KEY REFERENCES Persons(PersonID)  
);

-- adding foreign key after table was created
ALTER TABLE Orders ADD FOREIGN KEY (PersonID) REFERENCES Persons(PersonID);

-- dropping a foreign key
ALTER TABLE Orders DROP FOREIGN KEY orders_persons_fk;
-- or
ALTER TABLE Orders DROP CONSTRAINT orders_persons_fk;

-- foreign key options
ON DELETE CASCADE /* deletes dependent rows in child when ref in parent is deleted */
ON DELETE SET NULL /* converts values to null in child when ref in parent is deleted */
```

##### 3. Unique
```mysql
-- adding a Unique constraint while creation
CREATE TABLE Persons (  
    ID int UNIQUE,  
    LastName varchar(255) NOT NULL,  
    FirstName varchar(255),  
    Age int  
);
-- or
CREATE TABLE Persons (  
    ID int NOT NULL,  
    LastName varchar(255) NOT NULL,  
    FirstName varchar(255),  
    Age int,  
    CONSTRAINT persons_id_uk UNIQUE (ID)  
);

-- adding unique constraint after table was created
ALTER TABLE Persons ADD UNIQUE (ID);
-- or
ALTER TABLE Persons ADD CONSTRAINT persons_uk UNIQUE (ID,LastName);

-- dropping a unique constraint
ALTER TABLE Persons DROP INDEX persons_id_uk;
-- or
ALTER TABLE Persons DROP CONSTRAINT persons_uk;
```
##### 4. Check
```plsql
CREATE TABLE employees (
	salary int,
	CONSTRAINT emp_salary_ck CHECK (salary > 0)
);
```

##### 5. Not Null
```mysql
-- adding not null while table creation
CREATE TABLE Persons (  
    ID int NOT NULL,  
    LastName varchar(255) NOT NULL,  
    FirstName varchar(255) NOT NULL,  
    Age int  
);

-- adding not null after table was created
ALTER TABLE Persons ALTER COLUMN Age int NOT NULL;
-- or
ALTER TABLE Persons MODIFY COLUMN Age int NOT NULL;
```

##### 6. Default
```mysql
-- adding default while table creation
CREATE TABLE Persons (  
    ID int NOT NULL,  
    LastName varchar(255) NOT NULL,  
    FirstName varchar(255),  
    Age int,  
    City varchar(255) DEFAULT 'Sandnes'  
);

CREATE TABLE Orders (  
    ID int NOT NULL,  
    OrderNumber int NOT NULL,  
    OrderDate date DEFAULT GETDATE()  
);

-- adding default after table was created
ALTER TABLE Persons ALTER City SET DEFAULT 'Sandnes';

-- dropping a default constraint
ALTER TABLE Persons ALTER City DROP DEFAULT;
```

## Section 15: Functions & CTEs
### CTE (Common Table Expression)
##### 1. Create CTE 
```mysql
WITH cte_name AS (
    SELECT column1, column2
    FROM table_name
    WHERE condition
)

SELECT * FROM cte_name;
```

### Functions
Functions manipulate data and return a result.
##### 1. Create Function
```mysql
CREATE FUNCTION calculate_bonus (salary DECIMAL(10,2)) RETURNS DECIMAL(10,2)
BEGIN
    DECLARE bonus DECIMAL(10,2);
    SET bonus = salary * 0.1;
    RETURN bonus;
END;
```

##### 2. Use Function
```mysql
SELECT first_name, last_name, calculate_bonus(salary) AS bonus
FROM employees;
```


## Section 16: Stored Procedures & Triggers
### Stored Procedures:
A stored procedure is a SQL code that can be stored and preserved for anytime use. It can be reused over and over again for repeating the SQL code. Parameters / Arguments can also be passed to the stored procedure to customize and make it more modular.
##### 1. Create Stored Procedure
```mysql
CREATE PROCEDURE get_employees_by_dept(IN dept_id INT)
BEGIN
    SELECT * FROM employees WHERE department_id = dept_id;
END;

-- stored procedure structure (blocks)
CREATE PROCEDURE procedure_name (parameters)
BEGIN
   -- Declaration block
   DECLARE variables;

   -- Initialization block
   SET variables;

   -- Main execution block
   SELECT/INSERT/UPDATE/DELETE logic;

   -- Control flow (IF/LOOP/CASE)

   -- Error handling (optional)

   -- Return or output assignment

END;
```

##### 2. Execute Stored Procedure
```mysql
CALL get_employees_by_dept(10);
```

### Triggers
A trigger is a special type of stored procedure that automatically gets executed when an event occurs in the database server.  It can be created of DDL, DML or logon events, but cannot be executed manually. 
##### 1. Create Trigger
```plsql
-- syntax
CREATE OR REPLACE TRIGGER trigger_name
[BEFORE | AFTER | INSEAD OF]
[INSERT (OR) | UPDATE (OR) | DELETE]
[OF column_name]
ON table_name
[REFERENCING OLD AS o NEW AS n]
[FOR EACH ROW]
WHEN (codition)
DECLARE
	--declaration block
BEGIN
	-- executable block
EXCEPTION
	-- exception handling
END;

-- example
CREATE OR REPLACE TRIGGER display_salary_changes
BEFORE DELETE OR INSERT OR UPDATE
ON employees
FOR EACH ROW
WHEN (NEW.emp_id > 0)
DECLARE
	sal_diff NUMBER;
BEGIN
	sal_diff := :NEW.salary - :OLD.salary;
	DBMS_OUTPUT.PUT_LINE('Old Salary: ' || :OLD.salary);
	DBMS_OUTPUT.PUT_LINE('New Salary: ' || :NEW.salary);
	DBMS_OUTPUT.PUT_LINE('Salary Difference: ' || salary_diff);
END;
```

## Section 17: Data Dictionary Views - Oracle
Apart from user-defined tables in the database, there are other system-defined collections of tables and views known as data dictionaries. They contain information about the database. There are 3 types: **USER** (Info about your own schema), **ALL** (Info of what you can access) and DBA (**DB** Admin, what's in everyone's schema).

##### 1. Tables & Columns:
```plsql
SELECT table_name, tablespace_name, num_rows
FROM user_tables;

-- Describe columns of a specific table
SELECT column_name, data_type, data_length, nullable
FROM user_tab_columns
WHERE table_name = 'EMPLOYEES';

/*
USER_TABLES
ALL_TABLES
USER_TAB_COLUMNS
*/

```
##### 2. Constraints:
```plsql
SELECT constraint_name, constraint_type, table_name, status
FROM user_constraints;

-- Find which columns have primary keys
SELECT table_name, column_name
FROM user_cons_columns
WHERE constraint_name IN (
    SELECT constraint_name
    FROM user_constraints
    WHERE constraint_type = 'P'
);

/*
USER_CONSTRAINTS
ALL_CONSTRAINTS
USER_CONS_COLUMNS
*/
```

##### 3. Indexes:
```plsql
SELECT index_name, table_name, uniqueness
FROM user_indexes;

-- Show columns involved in each index
SELECT index_name, column_name, column_position
FROM user_ind_columns
WHERE table_name = 'EMPLOYEES';


/*
USER_INDEXES
USER_IND_COLUMNS
*/
```

##### 4. Sequences:
```plsql
-- Check details of all user-defined sequences
SELECT sequence_name, last_number, min_value, max_value, increment_by
FROM user_sequences;

/*
USER_SEQUENCES
ALL_SEQUENCES
*/
```

##### 5. Users & Privileges:
```plsql
-- Info about current user
SELECT username, account_status, created
FROM user_users;

-- Roles granted to current user
SELECT * FROM user_role_privs;

-- System privileges granted to current user
SELECT privilege FROM user_sys_privs;

-- Object-level privileges on tables
SELECT grantee, privilege, table_name
FROM user_tab_privs;

/*
USER_USERS – info about current user
ALL_USERS – info about all users
USER_ROLE_PRIVS – roles granted to user
USER_SYS_PRIVS – system privileges
USER_TAB_PRIVS – table privileges
*/
```

##### 6. Views & Synonyms:
```plsql
SELECT view_name, text_length
FROM user_views;

-- Check definition text of a view
SELECT text
FROM user_views
WHERE view_name = 'EMPLOYEE_SUMMARY';

SELECT synonym_name, table_owner, table_name
FROM user_synonyms;

/*
USER_VIEWS
USER_MVIEWS (materialized views)
USER_SYNONYMS
ALL_SYNONYMS
*/
```

##### 7. Stored Procedures & Triggers:
```plsql
SELECT object_name, object_type, status
FROM user_objects
WHERE object_type IN ('PROCEDURE', 'FUNCTION', 'PACKAGE');

-- View PL/SQL source code of a stored procedure
SELECT text
FROM user_source
WHERE name = 'CALC_SALARY'
ORDER BY line;

SELECT trigger_name, table_name, triggering_event, status
FROM user_triggers;

/*
USER_PROCEDURES
USER_SOURCE
USER_OBJECTS
USER_TRIGGERS
ALL_TRIGGERS
*/
```