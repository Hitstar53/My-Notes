## Introduction to SQL
Structured Query Language (SQL) is the standard language for managing and manipulating relational databases. It is used to perform tasks such as retrieving data, inserting new records, updating existing ones, and deleting data. SQL commands are traditionally categorized into several groups, which define their role in the database.

> [!seealso] Resources:
> Find Leetcode (Basic) SQL Top 50 Problems [here](https://leetcode.com/studyplan/top-sql-50/)
> More SQL Practice Problems on HackerRank [here](https://www.hackerrank.com/domains/sql)
> Find Notes on DBMS Concepts [here](https://takeuforward.org/dbms/most-asked-dbms-interview-questions)
> Find external notes for SQL [here](https://www.w3schools.com/sql/)

## Table of Contents
1. [[#Section 1 Data Definition Language (DDL)]]
2. [[#Section 2 Data Manipulation Language (DML)]]
3. [[#Section 3 Data Query Language (DQL)]]
4. [[#Section 4 Data Control Language (DCL)]]
5. [[#Section 5 Transaction Control Language (TCL)]]
6. [[#Section 6 Joins]]
7. [[#Section 7 Aggregate Functions]]
8. [[#Section 8 Set Operations]]
9. [[#Section 9 Window Functions]]
10. [[#Section 10 Subqueries]]
11. [[#Section 11 Date Functions]]
12. [[#Section 12 Views]]
13. [[#Section 13 Indexes]]
14. [[#Section 14 SPs, Functions & CTEs]]

## Section 1: Data Definition Language (DDL)
DDL commands are used to define and manage the structure of your database and its objects, such as tables, indexes, and views. These commands are foundational, as they build the framework where your data will live.

> [!tip]
> - Use DDL to set up your database schema from scratch or to modify it as your application's needs evolve.
> - Be cautious with `DROP` and `TRUNCATE`, as they can lead to irreversible data loss. `DROP` removes the entire table structure, while `TRUNCATE` only removes all rows.
> - `TRUNCATE` is generally faster than `DELETE` for clearing a table because it deallocates the data pages with minimal logging, whereas `DELETE` removes rows one by one and logs each deletion.

### Databases:
##### 1. CREATE DATABASE
```mysql
CREATE DATABASE company;
```

2. SHOW DATABASE
```mysql
SHOW DATABASES;
```
##### 2. USE DATABASE 
```mysql
USE company;
```
##### 3. ALTER DATABASE
```mysql
ALTER DATABASE company MODIFY NAME = companies;
```
##### 4. DROP DATABASE
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
ALTER TABLE employees ALTER COLUMN salary DECIMAL(12, 2);
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
DML commands are used to manage the data within your database tables. These are the most frequently used commands in day-to-day operations.

> [!tip]
> - Always use a `WHERE` clause with `UPDATE` and `DELETE` statements unless you intend to modify every single row in the table. Forgetting the `WHERE` clause is a common and dangerous mistake.
> - Wrap related DML operations in a transaction (using `BEGIN TRANSACTION`, `COMMIT`, `ROLLBACK`) to ensure data integrity. If one part of the operation fails, you can roll back the entire set of changes.

##### 1. INSERT
```mysql
INSERT INTO employees (employee_id, first_name, last_name, hire_date, salary)
VALUES (1, 'John', 'Doe', '2023-01-15', 50000.00);
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
```

## Section 3: Data Query Language (DQL)
DQL is used to retrieve data from the database. The `SELECT` statement is the cornerstone of SQL, allowing for powerful and complex data retrieval.

> [!tip]
> - **Performance:** Avoid using `SELECT *` in production code. Explicitly name the columns you need. This reduces the amount of data transferred and can sometimes allow the database to use more efficient query plans (like index-only scans).
> - **Readability:** Use aliases (`AS`) for columns and tables, especially in complex queries with joins, to make your code much easier to understand.
> - **Filtering:** Apply `WHERE` clauses as early as possible in your query to filter the dataset. The less data subsequent operations (like joins or aggregations) have to process, the faster your query will be.

##### 1. SELECT
```mysql
-- Show all records
SELECT * FROM employees;

-- Show specific columns
SELECT first_name, last_name, salary FROM employees;

-- using AS keyword to rename column while displaying
SELECT first_name AS Name FROM employees;
```
##### 2. WHERE
```mysql
SELECT * FROM employees
WHERE salary > 50000;
```

##### 3. IF
```mysql
SELECT IF(500<1000, "YES", "NO");

SELECT OrderID, Quantity, IF(Quantity>10, "MORE", "LESS") AS Threshold
FROM OrderDetails;
```

##### 4. CASE
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
```mysql
SELECT SupplierName FROM Suppliers  
WHERE EXISTS (SELECT ProductName FROM Products WHERE Products.SupplierID = Suppliers.supplierID AND Price < 20);
```

##### 6. IN & NOT IN 
```mysql
SELECT * from CUSTOMERS WHERE NAME IN ('Khilan', 'Hardik', 'Muffy');

SELECT * from CUSTOMERS WHERE AGE NOT IN (25, 23, 22);
```

##### 7. AND & OR
```mysql
SELECT * FROM CUSTOMERS 
WHERE (AGE = 25 OR salary < 4500) AND (name = 'Komal' OR name = 'Kaushik');
```

##### 8. ANY & ALL
```mysql
SELECT product_id, product_name, unit_price 
FROM Product
WHERE unit_price > ANY (SELECT price FROM Sales WHERE seller_id = 1);

SELECT product_id, product_name, unit_price 
FROM Product 
WHERE unit_price > ALL (SELECT price FROM Sales WHERE seller_id = 1 );
```

##### 9. BETWEEN
```mysql
SELECT * FROM Products 
WHERE Price BETWEEN 10 AND 20;
```

##### 9. COALESCE
```mysql
SELECT name, COALESCE(phone, 'Not Provided') AS contact_info 
FROM users;
```

##### 11. LIKE
```mysql
SELECT * FROM CUSTOMERS WHERE NAME LIKE 'K___%';

/* wildcards
_ - matches a single character
% - matches zero, one or more characters
*/
```

##### 12. REGEXP & RLIKE
```mysql
SELECT DISTINCT CITY 
FROM STATION 
WHERE CITY REGEXP '^[AEIOUaeiou]';

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
```mysql
SELECT * FROM employees
ORDER BY salary DESC;
```

##### 14. LIMIT & TOP
```mysql
SELECT * FROM employees
LIMIT 10;

SELECT TOP 4 * FROM employees;

SELECT TOP 4 * FROM CUSTOMERS ORDER BY SALARY DESC;

SELECT TOP 40 PERCENT * FROM CUSTOMERS ORDER BY SALARY
```

##### 15. DISTINCT
```mysql
SELECT DISTINCT department FROM employees;

SELECT COUNT(DISTINCT AGE) as UniqueAge FROM CUSTOMERS;
```

##### 16. CONCAT
```mysql
SELECT CONCAT(NAME,' ',AGE) AS DETAILS, ADDRESS FROM CUSTOMERS ORDER BY NAME;
```

##### 17. CAST & CONVERT
```mysql
SELECT CAST(salary AS CHAR) AS salary_string
FROM employees;

SELECT CONVERT(salary, CHAR) AS salary_string
FROM employees;
```

## Section 4: Data Control Language (DCL)

##### 1. GRANT
```mysql
GRANT SELECT, INSERT ON employees TO user1;
```

##### 2. REVOKE
```mysql
REVOKE INSERT ON employees FROM user1;
```

## Section 5: Transaction Control Language (TCL)
TCL commands are used to manage transactions in the database, ensuring that a series of operations are treated as a single, atomic unit. This is critical for maintaining data integrity.

> [!tip]
> - Transactions are essential for operations that require multiple steps, like transferring money between two accounts (a debit from one and a credit to another). If either step fails, the entire transaction can be rolled back, leaving the database in a consistent state.
> - `SAVEPOINT` is useful for complex transactions where you might want to undo only a portion of the work without rolling back the entire transaction.

##### 1. BEGIN TRANSACTION
```mysql
BEGIN TRANSACTION;
```

##### 2. COMMIT
```mysql
COMMIT;
```

##### 3. ROLLBACK
```mysql
ROLLBACK;
```

## Section 6: Joins
Joins are fundamental to relational databases. They are used to combine rows from two or more tables based on a related column between them, allowing you to query data across your entire schema.  

> [!tip]
> - **Choosing the Right Join:** `INNER JOIN` is for when you only want records that exist in both tables. `LEFT JOIN` is perfect when you want all records from the "left" table, regardless of whether they have a match in the "right" table (e.g., finding all customers and their orders, even if a customer has no orders).
> - **Performance:** Ensure that the columns used in your `ON` clause are indexed. Joining on indexed columns is significantly faster than joining on unindexed ones.
> - **Readability:** Always use table aliases when joining multiple tables to keep your query clean and avoid ambiguity with column names.

##### 1. INNER JOIN
= (A ∩ B)
```mysql
SELECT e.first_name, e.last_name, d.department_name
FROM employees e
JOIN departments d ON e.department_id = d.department_id;
```

##### 2. LEFT OUTER JOIN
= A ∪ (A ∩ B)
```mysql
SELECT e.first_name, e.last_name, d.department_name
FROM employees e
LEFT JOIN departments d ON e.department_id = d.department_id;
```

##### 3. RIGHT OUTER JOIN
= B ∪ (A ∩ B)
```mysql
SELECT e.first_name, e.last_name, d.department_name
FROM employees e
RIGHT JOIN departments d ON e.department_id = d.department_id;
```

##### 4. FULL OUTER JOIN
= (A ∪ B)
```mysql
SELECT employees.emp_name, salaries.salary FROM employees 
LEFT JOIN salaries ON employees.emp_id = salaries.emp_id 
UNION 
SELECT employees.emp_name, salaries.salary FROM employees 
RIGHT JOIN salaries ON employees.emp_id = salaries.emp_id;
```

##### 5. CROSS JOIN
= (A × B)
```mysql
SELECT e.first_name, e.last_name, d.department_name
FROM employees e
CROSS JOIN departments d ON e.department_id = d.department_id;
```

## Section 7: Aggregate Functions
These commands are used to summarize data. `GROUP BY` collapses multiple rows into a single summary row, and aggregate functions perform a calculation on a set of values to return a single value.  

> [!tip]
> - **`WHERE` vs. `HAVING`:** This is a critical distinction. `WHERE` filters rows _before_ any grouping or aggregation occurs. `HAVING` filters groups _after_ the aggregation has been performed. You cannot use an aggregate function in a `WHERE` clause.
> - **Multi-column Grouping:** You can group by multiple columns to get more granular aggregations (e.g., `GROUP BY country, city`).

##### 1. COUNT
```mysql
SELECT COUNT(*) FROM employees;
```

##### 2. LENGTH
```mysql
SELECT * FROM Tweets WHERE LENGTH(content) > 15;
```

##### 3. SUM
```mysql
SELECT SUM(salary) FROM employees;
```

##### 4. AVG
```mysql
SELECT AVG(salary) FROM employees;
```

##### 5. MAX
```mysql
SELECT MAX(salary) FROM employees;
```

##### 6. MIN
```mysql
SELECT MIN(salary) FROM employees;
```

##### 7. ROUND
```mysql
SELECT ProductName, ROUND(Price, 2) AS RoundedPrice  
FROM Products;
```

##### 8. GROUP BY
```mysql
SELECT department_id, AVG(salary)
FROM employees
GROUP BY department_id

SELECT AGE, MIN(SALARY) AS MIN_SALARY 
FROM CUSTOMERS 
GROUP BY AGE 
ORDER BY MIN_SALARY DESC;
```

##### 9. HAVING
```mysql
SELECT department_id, AVG(salary)
FROM employees
GROUP BY department_id
HAVING AVG(salary) > 50000;
```

## Section 8: Set Operations
Set operators combine the results of two or more `SELECT` statements into a single result set. While joins combine tables horizontally based on columns, set operators combine results vertically based on rows.  

> [!tip]
> - **`UNION` vs. `UNION ALL`:** `UNION` removes duplicate rows from the combined result set, which requires a sorting operation behind the scenes. `UNION ALL` includes all rows, including duplicates, and is therefore much faster. If you know your combined results won't have duplicates or if duplicates are acceptable, always use `UNION ALL` for better performance.
> - **Requirements:** The `SELECT` statements involved must have the same number of columns, and the corresponding columns must have compatible data types.

##### 1. UNION & UNION ALL
```mysql
SELECT name FROM students
UNION
SELECT name FROM teachers;

SELECT name FROM students
UNION ALL
SELECT name FROM teachers;
```

##### 2. INTERSECT
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

## Section 9: Window Functions
Window functions perform calculations across a set of rows that are related to the current row. Unlike aggregate functions, they do not collapse rows; they return a value for each row based on the "window" of data defined by the `OVER()` clause.  

> [!tip]
> - **Running Totals & Moving Averages:** Use `SUM() OVER (...)` or `AVG() OVER (...)` to calculate metrics that accumulate or average over a specific window of rows.
> - **Ranking:** `ROW_NUMBER()` gives a unique number to each row. `RANK()` gives the same rank to tied values but leaves gaps. `DENSE_RANK()` gives the same rank to tied values but does not leave gaps. Choose the one that fits your specific ranking logic.
> - **Comparing to Previous/Next Rows:** `LAG()` and `LEAD()` are incredibly useful for comparing a row's value to the value in the preceding or following row, respectively (e.g., calculating day-over-day growth).

##### 1. ROW NUMBER
```postgresql
SELECT employee_id, department_id, salary, 
ROW_NUMBER() OVER (PARTITION BY department_id ORDER BY salary DESC) AS rn
FROM employees;
```

##### 2. RANK
```postgresql
SELECT employee_id, department_id, salary, 
RANK() OVER (PARTITION BY department_id ORDER BY salary DESC) AS rk
FROM employees;
```

##### 3. DENSE RANK
```postgresql
SELECT employee_id, department_id, salary, 
DENSE_RANK() OVER (PARTITION BY department_id ORDER BY salary DESC) AS drk
FROM employees;
```

##### 4. LAG
```postgresql
SELECT employee_id, department_id, salary, 
LAG(salary, 1, 0) OVER (PARTITION BY department_id ORDER BY salary) AS prev_salary
FROM employees;
```

##### 5. LEAD
```postgresql
SELECT employee_id, department_id, salary, 
LEAD(salary, 1, 0) OVER (PARTITION BY department_id ORDER BY salary) AS next_salary
FROM employees;
```

## Section 10: Subqueries
These are methods for nesting queries within other queries, which is essential for performing complex, multi-step logic.

> [!tip]
> - **Subquery vs. Join:** Often, a subquery can be rewritten as a `JOIN`, which can be more readable and sometimes more performant. However, subqueries are very powerful, especially with operators like `IN`, `NOT IN`, `EXISTS`, and `NOT EXISTS`.
> - **Performance:** For checking existence, `EXISTS` is generally more efficient than `IN` because it stops processing as soon as it finds a match, whereas `IN` may need to scan the entire subquery result.  
> - **Readability:** For complex queries, always prefer CTEs over nested subqueries. They break the logic into named, sequential steps, making the query vastly easier to read, debug, and maintain.

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

## Section 11: Date Functions
Date functions are essential for manipulating and querying temporal data. They allow you to extract components from dates, perform arithmetic, and format them for display. Syntax often varies between SQL dialects (like MySQL, PostgreSQL, and SQL Server).  

> [!tip]
> - **Time-based Filtering:** Use date functions in `WHERE` clauses to filter records within a specific time frame, such as the last 30 days or the current month.  
> - **Reporting and Grouping:** `EXTRACT` or `DATE_TRUNC` are powerful for grouping data by month, year, or quarter to create summary reports.  
> - **Calculating Durations:** `DATEDIFF` is perfect for calculating user age, subscription length, or the time between two events.

##### 1. CURRENT DATE & TIME
```mysql
SELECT CURDATE();  -- current date
SELECT CURTIME();  -- current time
SELECT NOW();      -- current date & time

/* data types
- `DATE` - format YYYY-MM-DD
- `DATETIME` - format: YYYY-MM-DD HH:MI:SS
- `TIMESTAMP` - format: YYYY-MM-DD HH:MI:SS
- `YEAR` - format YYYY or YY
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

## Section 12: Views
A view is a virtual table based on the result-set of a stored SQL query. It contains rows and columns, just like a real table, but does not store the data itself. Views are used to simplify complex queries, provide a layer of security, and ensure data consistency.  

> [!tip]
> - **Simplification:** Encapsulate a complex join or calculation into a view. This allows end-users to query the view with a simple `SELECT` statement without needing to understand the underlying complexity.
> - **Security:** Grant users access to a view that only exposes certain columns or rows, thereby restricting their access to sensitive data in the underlying tables.  
> - **Maintenance:** If the logic of a complex query needs to change, you only need to update the view definition (`ALTER VIEW`), and all applications using the view will automatically get the new logic.

##### 1. Create View
```mysql
CREATE VIEW high_salary_employees AS
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
**Note:** Not available in MySQL, Only in PostgreSQL / RedshiftSQL
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

## Section 13: Indexes & Constraints
These are database objects used to enforce data integrity and improve query performance.

> [!tip]
> - **Data Integrity:** Constraints are rules that prevent invalid data from being entered into your tables. A `PRIMARY KEY` (which is both `UNIQUE` and `NOT NULL`) is essential for uniquely identifying each row. A `FOREIGN KEY` is crucial for maintaining referential integrity between tables.
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

### Constraints:
##### 1. Primary Key
```mysql
-- Create primary key for single column
CREATE TABLE Persons (  
    ID int NOT NULL,  
    LastName varchar(255) NOT NULL,  
    FirstName varchar(255),  
    Age int,  
    PRIMARY KEY (ID)  
);
-- or
CREATE TABLE Persons (  
    ID int NOT NULL PRIMARY KEY,  
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
    CONSTRAINT PK_Person PRIMARY KEY (ID,LastName)  
);

-- adding primary key after table is created
ALTER TABLE Persons ADD PRIMARY KEY (ID);
-- or
ALTER TABLE Persons ADD CONSTRAINT PK_Person PRIMARY KEY (ID,LastName);

-- dropping a primary key
ALTER TABLE Persons DROP PRIMARY KEY;
-- or
ALTER TABLE Persons DROP CONSTRAINT PK_Person;
```

##### 2. Foreign Key
```mysql
-- adding a single foreign key
CREATE TABLE Orders (  
    OrderID int NOT NULL,  
    OrderNumber int NOT NULL,  
    PersonID int,  
    PRIMARY KEY (OrderID),  
    FOREIGN KEY (PersonID) REFERENCES Persons(PersonID)  
);
-- or
CREATE TABLE Orders (  
    OrderID int NOT NULL PRIMARY KEY,  
    OrderNumber int NOT NULL,  
    PersonID int FOREIGN KEY REFERENCES Persons(PersonID)  
);

-- adding foreign key consisting of multiple columns
CREATE TABLE Orders (  
    OrderID int NOT NULL,  
    OrderNumber int NOT NULL,  
    PersonID int,  
    PRIMARY KEY (OrderID),  
    CONSTRAINT FK_PersonOrder FOREIGN KEY (PersonID)  
    REFERENCES Persons(PersonID)  
);

-- adding foreign key after table was created
ALTER TABLE Orders ADD FOREIGN KEY (PersonID) REFERENCES Persons(PersonID);
-- or for multiple columns
ALTER TABLE Orders  
ADD CONSTRAINT FK_PersonOrder  
FOREIGN KEY (PersonID) REFERENCES Persons(PersonID);

-- dropping a foreign key
ALTER TABLE Orders DROP FOREIGN KEY FK_PersonOrder;
-- or
ALTER TABLE Orders DROP CONSTRAINT FK_PersonOrder;
```

##### 3. Unique
```mysql
-- adding a Unique constraint while creation
CREATE TABLE Persons (  
    ID int NOT NULL UNIQUE,  
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
    UNIQUE (ID)  
);

-- adding unique constraint after table was created
ALTER TABLE Persons ADD UNIQUE (ID);
-- or
ALTER TABLE Persons ADD CONSTRAINT UC_Person UNIQUE (ID,LastName);

-- dropping a unique constraint
ALTER TABLE Persons DROP INDEX UC_Person;
-- or
ALTER TABLE Persons DROP CONSTRAINT UC_Person;
```

##### 4. Not Null
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

##### 5. Default
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

## Section 14: SPs, Functions & CTEs

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

### Stored Procedures:
##### 1.Create Stored Procedure
```mysql
CREATE PROCEDURE get_employees_by_dept(IN dept_id INT)
BEGIN
    SELECT * FROM employees WHERE department_id = dept_id;
END;
```

##### 2. Execute Stored Procedure
```mysql
CALL get_employees_by_dept(10);
```

### Functions
##### 1. Create Function
```mysql
CREATE FUNCTION calculate_bonus(salary DECIMAL(10,2)) RETURNS DECIMAL(10,2)
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