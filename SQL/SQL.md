# SQL Crash Course

## 1. SQL Basics (0-5 Minutes)

### What is SQL?
SQL (Structured Query Language) is used to manage and manipulate relational databases.

### Key Concepts
- **Tables**: Store data (e.g., "Employees" table with columns like id, name, salary).
- **Queries**: Commands to retrieve, add, update, or delete data.

### Basic Commands

#### SELECT: Retrieve Data
```sql
SELECT name, salary FROM Employees;
-- Use * for all columns
SELECT * FROM Employees;
```

#### WHERE: Filter Rows
```sql
-- Shows names of employees earning more than 50,000
SELECT name FROM Employees WHERE salary > 50000;
```

#### INSERT: Add Data
```sql
INSERT INTO Employees (id, name, salary) VALUES (1, 'Alice', 60000);
```

#### UPDATE: Modify Data
```sql
UPDATE Employees SET salary = 65000 WHERE name = 'Alice';
```

#### DELETE: Remove Data
```sql
DELETE FROM Employees WHERE id = 1;
```

### Quick Practice
Imagine a table "Students" with columns: id, name, grade.
```sql
-- Get all students with grade > 80
SELECT name FROM Students WHERE grade > 80;

-- Add a student
INSERT INTO Students (id, name, grade) VALUES (1, 'Bob', 85);
```

---

## 2. Intermediate SQL (5-10 Minutes)

### Sorting and Limiting

#### ORDER BY: Sort Results
```sql
SELECT name, salary FROM Employees ORDER BY salary DESC;
```

#### LIMIT: Restrict Output
```sql
-- Top 3 earners
SELECT * FROM Employees ORDER BY salary DESC LIMIT 3;
```

### Aggregations

#### COUNT, SUM, AVG, etc.: Summarize Data
```sql
-- Counts employees earning over 50,000
SELECT COUNT(*) FROM Employees WHERE salary > 50000;

-- Average salary
SELECT AVG(salary) FROM Employees;
```

#### GROUP BY: Aggregate by Category
```sql
-- Average salary per department
SELECT department, AVG(salary) FROM Employees GROUP BY department;
```

### Joins: Combine Tables
Imagine another table "Departments" with columns: id, dept_name.
The Employees table has a `dept_id` column.

#### INNER JOIN: Matches Rows
```sql
SELECT e.name, d.dept_name
FROM Employees e
INNER JOIN Departments d ON e.dept_id = d.id;
```

---

## 3. Advanced SQL (10-15 Minutes)

### Subqueries
```sql
-- Employees earning above average salary
SELECT name
FROM Employees
WHERE salary > (SELECT AVG(salary) FROM Employees);
```

### Indexes
```sql
-- Speed up searches
CREATE INDEX idx_salary ON Employees(salary);
```

### Transactions
```sql
-- Ensure operations succeed or fail together
BEGIN TRANSACTION;
UPDATE Employees SET salary = salary + 1000 WHERE id = 1;
INSERT INTO logs (employee_id, action) VALUES (1, 'Raise');
COMMIT;
-- Use ROLLBACK if needed
```

### Views
```sql
-- Virtual tables for frequent queries
CREATE VIEW HighEarners AS
SELECT name, salary FROM Employees WHERE salary > 70000;

-- Query like a table
SELECT * FROM HighEarners;
```

### Window Functions
```sql
-- Analyze data across rows
SELECT name, salary,
RANK() OVER (ORDER BY salary DESC) AS salary_rank
FROM Employees;
```

---

## Crash Course Recap
### Basics
- SELECT, WHERE, INSERT, UPDATE, DELETE

### Intermediate
- Sorting, aggregations, joins

### Advanced
- Subqueries, indexes, transactions, views, window functions

