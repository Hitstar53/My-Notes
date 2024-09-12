Find SQL Top 50 Practice Problems [here](https://leetcode.com/studyplan/top-sql-50/)
## Table of Contents
[[#1. Data Definition Language (DDL)]]
[[#2. Data Manipulation Language (DML)]]
[[#3. Data Query Language (DQL)]]
[[#4. Data Control Language (DCL)]]
[[#5. Transaction Control Language (TCL)]]
[[#6. Joins]]
[[#7. Aggregate Functions]]
[[#8. Window Functions]]
[[#9. Subqueries]]
[[#10. Views]]
[[#11. Indexes]]
[[#12. Stored Procedures and Functions]]

## 1. Data Definition Language (DDL)

### CREATE DATABASE
```mysql
CREATE DATABASE company;
```
### SHOW DATABASES
```mysql
SHOW DATABASES;
```
### USE DATABASE 
```mysql
USE company;
```
### ALTER DATABASE
```mysql
ALTER DATABASE company MODIFY NAME = companies;
```
### DROP DATABASE
```mysql
DROP DATABASE company;
```

### CREATE TABLE
```mysql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50),
    hire_date DATE,
    salary DECIMAL(10, 2)
);
```

### SHOW TABLE
```mysql
SHOW TABLES;
```

### DESCRIBE TABLE
```mysql
DESC employees;
```

### ALTER TABLE
Add a column:
```mysql
ALTER TABLE employees ADD email VARCHAR(100);
```

Modify a column:
```mysql
ALTER TABLE employees ALTER COLUMN salary DECIMAL(12, 2);
```

Rename a column:
```mysql
ALTER TABLE employees RENAME COLUMN salary TO income;
```

Drop a column:
```mysql
ALTER TABLE employees DROP COLUMN email;
```

### RENAME TABLE
```mysql
RENAME TABLE employees TO employee_details;
```

### DROP TABLE
```mysql
DROP TABLE employees;
```

### TRUNCATE TABLE
```mysql
TRUNCATE TABLE employees;
```

## 2. Data Manipulation Language (DML)

### INSERT
```mysql
INSERT INTO employees (employee_id, first_name, last_name, hire_date, salary)
VALUES (1, 'John', 'Doe', '2023-01-15', 50000.00);
```

### UPDATE
```mysql
UPDATE employees
SET salary = 55000.00
WHERE employee_id = 1;
```

```mysql
UPDATE CUSTOMERS SET AGE = AGE+5, SALARY = SALARY+3000;
```

### DELETE
```mysql
DELETE FROM employees
WHERE employee_id = 1;
```

## 3. Data Query Language (DQL)

### SELECT
Basic select: Show all records
```mysql
SELECT * FROM employees;
```

Select specific columns:
```mysql
SELECT first_name, last_name, salary FROM employees;
```

using AS keyword:
```mysql
SELECT first_name AS Name FROM employees;
```
### WHERE
```mysql
SELECT * FROM employees
WHERE salary > 50000;
```

### EXISTS
```mysql
SELECT SupplierName FROM Suppliers  
WHERE EXISTS (SELECT ProductName FROM Products WHERE Products.SupplierID = Suppliers.supplierID AND Price < 20);
```

### IN / NOT IN 
```mysql
SELECT * from CUSTOMERS WHERE NAME IN ('Khilan', 'Hardik', 'Muffy');

SELECT * from CUSTOMERS WHERE AGE NOT IN (25, 23, 22);
```

###  AND / OR
```mysql
SELECT * FROM CUSTOMERS 
WHERE (AGE = 25 OR salary < 4500) AND (name = 'Komal' OR name = 'Kaushik');
```

### ANY / ALL
```mysql
SELECT product_id, product_name, unit_price 
FROM Product
WHERE unit_price > ANY (SELECT price FROM Sales WHERE seller_id = 1);

SELECT product_id, product_name, unit_price 
FROM Product 
WHERE unit_price > ALL (SELECT price FROM Sales WHERE seller_id = 1 );
```

### BETWEEN
```mysql
SELECT * FROM Products 
WHERE Price BETWEEN 10 AND 20;
```

### LIKE
```mysql
SELECT * FROM CUSTOMERS WHERE NAME LIKE 'K___%';

/* wildcards
_ - matches a single character
% - matches zero, one or more characters
*/
```

### ORDER BY
```mysql
SELECT * FROM employees
ORDER BY salary DESC;
```

### LIMIT / TOP
```mysql
SELECT * FROM employees
LIMIT 10;

SELECT TOP 4 * FROM employees;

SELECT TOP 4 * FROM CUSTOMERS ORDER BY SALARY DESC;

SELECT TOP 40 PERCENT * FROM CUSTOMERS ORDER BY SALARY
```

### DISTINCT
```mysql
SELECT DISTINCT department FROM employees;

SELECT COUNT(DISTINCT AGE) as UniqueAge FROM CUSTOMERS;
```

### CONCAT
```mysql
SELECT CONCAT(NAME,' ',AGE) AS DETAILS, ADDRESS FROM CUSTOMERS ORDER BY NAME;
```

## 4. Data Control Language (DCL)

### GRANT
```mysql
GRANT SELECT, INSERT ON employees TO user1;
```

### REVOKE
```mysql
REVOKE INSERT ON employees FROM user1;
```

## 5. Transaction Control Language (TCL)

### BEGIN TRANSACTION
```mysql
BEGIN TRANSACTION;
```

### COMMIT
```mysql
COMMIT;
```

### ROLLBACK
```mysql
ROLLBACK;
```

## 6. Joins

### INNER JOIN
= (A ∩ B)
```mysql
SELECT e.first_name, e.last_name, d.department_name
FROM employees e
JOIN departments d ON e.department_id = d.department_id;
```

### LEFT OUTER JOIN
= A ∪ (A ∩ B)
```mysql
SELECT e.first_name, e.last_name, d.department_name
FROM employees e
LEFT JOIN departments d ON e.department_id = d.department_id;
```

### RIGHT OUTER JOIN
= B ∪ (A ∩ B)
```mysql
SELECT e.first_name, e.last_name, d.department_name
FROM employees e
RIGHT JOIN departments d ON e.department_id = d.department_id;
```

### FULL OUTER JOIN
= (A ∪ B)
```mysql
SELECT employees.emp_name, salaries.salary FROM employees 
LEFT JOIN salaries ON employees.emp_id = salaries.emp_id 
UNION 
SELECT employees.emp_name, salaries.salary FROM employees 
RIGHT JOIN salaries ON employees.emp_id = salaries.emp_id;
```

### CROSS JOIN
= (A × B)
```mysql
SELECT e.first_name, e.last_name, d.department_name
FROM employees e
CROSS JOIN departments d ON e.department_id = d.department_id;
```

## 7. Aggregate Functions

### COUNT
```mysql
SELECT COUNT(*) FROM employees;
```

### LENGTH
```mysql
SELECT * FROM Tweets WHERE LENGTH(content) > 15;
```

### SUM
```mysql
SELECT SUM(salary) FROM employees;
```

### AVG
```mysql
SELECT AVG(salary) FROM employees;
```

### MAX
```mysql
SELECT MAX(salary) FROM employees;
```

### MIN
```mysql
SELECT MIN(salary) FROM employees;
```

### ROUND
```mysql
SELECT ProductName, ROUND(Price, 2) AS RoundedPrice  
FROM Products;
```

### GROUP BY
```mysql
SELECT department_id, AVG(salary)
FROM employees
GROUP BY department_id

SELECT AGE, MIN(SALARY) AS MIN_SALARY 
FROM CUSTOMERS 
GROUP BY AGE 
ORDER BY MIN_SALARY DESC;
```

### HAVING
```mysql
SELECT department_id, AVG(salary)
FROM employees
GROUP BY department_id
HAVING AVG(salary) > 50000;
```

### IF
```mysql
SELECT IF(500<1000, "YES", "NO");

SELECT OrderID, Quantity, IF(Quantity>10, "MORE", "LESS") AS Threshold
FROM OrderDetails;
```

### CASE
```mysql
SELECT OrderID, Quantity,  
CASE  
    WHEN Quantity > 30 THEN "The quantity is greater than 30"  
    WHEN Quantity = 30 THEN "The quantity is 30"  
    ELSE "The quantity is under 30"  
END AS Threshold
FROM OrderDetails;
```

## 8. Window Functions

### ROW NUMBER
```postgresql
SELECT employee_id, department_id, salary, 
ROW_NUMBER() OVER (PARTITION BY department_id ORDER BY salary DESC) AS rn
FROM employees;
```

### RANK
```postgresql
SELECT employee_id, department_id, salary, 
RANK() OVER (PARTITION BY department_id ORDER BY salary DESC) AS rk
FROM employees;
```

### DENSE RANK
```postgresql
SELECT employee_id, department_id, salary, 
DENSE_RANK() OVER (PARTITION BY department_id ORDER BY salary DESC) AS drk
FROM employees;
```

### LAG
```postgresql
SELECT employee_id, department_id, salary, 
LAG(salary, 1, 0) OVER (PARTITION BY department_id ORDER BY salary) AS prev_salary
FROM employees;
```

### LEAD
```postgresql
SELECT employee_id, department_id, salary, 
LEAD(salary, 1, 0) OVER (PARTITION BY department_id ORDER BY salary) AS next_salary
FROM employees;
```

## 9. Subqueries

### Subquery in WHERE clause
```mysql
SELECT first_name, last_name
FROM employees
WHERE department_id IN (SELECT department_id FROM departments WHERE location_id = 1700);
```

### Subquery in SELECT clause
```mysql
SELECT e.first_name, e.last_name,
       (SELECT AVG(salary) FROM employees WHERE department_id = e.department_id) AS dept_avg_salary
FROM employees e;
```

### Subquery in UPDATE clause
```mysql
UPDATE CUSTOMERS SET SALARY = SALARY * 0.25
WHERE AGE IN (SELECT AGE FROM CUSTOMERS_BKP WHERE AGE >= 27 );
```

## 10. Views

### Create View
```mysql
CREATE VIEW high_salary_employees AS
SELECT * FROM employees WHERE salary > 70000;
```

### Query View
```mysql
SELECT * FROM high_salary_employees;
```

### Update View
```mysql
UPDATE high_salary_employees
SET salary = 85000 WHERE name = 'Ramesh';
```

### Drop View
```mysql
DROP VIEW high_salary_employees;
```

## 11. Indexes

### Create Index
```mysql
CREATE INDEX idx_last_name ON employees(last_name);
```

### Drop Index
```mysql
DROP INDEX idx_last_name ON employees;
```

## 12. Stored Procedures, Functions and CTEs

### CTE (Common Table Expression)
```mysql
WITH cte_name AS (
    SELECT column1, column2
    FROM table_name
    WHERE condition
)

SELECT * FROM cte_name;
```

### Create Stored Procedure
```mysql
CREATE PROCEDURE get_employees_by_dept(IN dept_id INT)
BEGIN
    SELECT * FROM employees WHERE department_id = dept_id;
END;
```

### Execute Stored Procedure
```mysql
CALL get_employees_by_dept(10);
```

### Create Function
```mysql
CREATE FUNCTION calculate_bonus(salary DECIMAL(10,2)) RETURNS DECIMAL(10,2)
BEGIN
    DECLARE bonus DECIMAL(10,2);
    SET bonus = salary * 0.1;
    RETURN bonus;
END;
```

### Use Function
```mysql
SELECT first_name, last_name, calculate_bonus(salary) AS bonus
FROM employees;
```