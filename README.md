# SQL Notes

## Database Management System (DBMS)

### What is a Database?
- A collection of related data stored and organized systematically.

### What is DBMS?
- A software that manages databases and allows users to interact with the data.

### Types of Databases
- Relational
- Time-series based
- NoSql

<img width="639" alt="image" src="https://github.com/user-attachments/assets/755beb1f-aef1-4a73-b133-a9d241c38d35" />


### What is RDBMS?
- A type of DBMS where data is stored in tables with rows and columns.

### Transactions in DBMS
- A sequence of database operations that must be executed as a whole.

### States of a Transaction
1. **Active** - Transaction is executing.
2. **Partially Committed** - Execution completed but not committed.
3. **Failed** - Transaction encountered an error.
4. **Aborted** - Changes are rolled back.
5. **Committed** - Changes are permanently saved.

### ACID Properties
- **Atomicity** - Ensures complete execution or rollback.
- **Consistency** - Maintains database integrity.
- **Isolation** - Transactions are independent.
- **Durability** - Changes remain permanent after commit.
<img width="1236" alt="image" src="https://github.com/user-attachments/assets/0ba2df18-01a9-4a09-947f-e7c3d75b4685" />

---

## SQL Fundamentals

### What is SQL?
- **Structured Query Language (SQL)** is used to interact with databases.
- Became an ANSI standard in 1986 and ISO standard in 1987.

### What Can SQL Do?
- Create, retrieve, update, and delete data.
- Manage databases and set permissions.

### MySQL Data Types
- **String:** CHAR, VARCHAR, TEXT
- **Numeric:** INT, FLOAT, DECIMAL
- **Date & Time:** DATE, DATETIME, TIMESTAMP

### Types of SQL Commands
1. **DDL (Data Definition Language)**
   - CREATE, DROP, ALTER, TRUNCATE, RENAME
2. **DML (Data Manipulation Language)**
   - INSERT, UPDATE, DELETE
3. **DQL (Data Query Language)**
   - SELECT
4. **DCL (Data Control Language)**
   - GRANT, REVOKE

### SQL Constraints
- **NOT NULL** - No NULL values allowed.
- **UNIQUE** - Ensures unique values.
- **PRIMARY KEY** - Uniquely identifies a record.
- **FOREIGN KEY** - Maintains referential integrity.
- **CHECK** - Enforces a condition.
- **DEFAULT** - Sets default value.
  
### Primary Key
- **Uniqueness** - Each value must be unique per row.
- **Immutable** - Should not change once set.
- **Simplicity** - Should be as simple as possible.
- **Non-Intelligent** - Should not contain meaningful information.
- **Indexed** - Automatically indexed for faster retrieval.
- **Referential Integrity** - Basis for foreign keys.
- **Data Type** - Usually integer or string.

### Foreign Key
- **Referential Integrity** - Links records between tables.
- **Nullable** - Can contain NULL values unless restricted.
- **Match Primary Keys** - Must match a primary key in the parent table or be NULL.
- **Ensures Relationships** - Defines relationships between tables.
- **No Uniqueness Requirement** - Does not need to be unique.

### DELETE Command
- Used to remove records from a table.
- Syntax: `DELETE FROM table_name WHERE condition;`
- Example: `DELETE FROM Students WHERE ID = 5;`
- ⚠ Be careful: Running `DELETE` without `WHERE` deletes all records.

### DROP vs TRUNCATE vs DELETE
- **DROP** - Removes table structure and data permanently.
- **TRUNCATE** - Deletes all records but keeps the table structure.
- **DELETE** - Removes specific records based on a condition.

### Functions in SQL
- **Purpose** - Simplifies calculations, enhances reusability, improves performance.
- **Types:**
  1. **Built-in Functions:**
     - **String Functions:** CONCAT, LENGTH, SUBSTRING
     - **Numeric Functions:** ABS, ROUND, CEIL
     - **Date & Time Functions:** NOW, DATE_FORMAT, DATEDIFF
     - **Aggregate Functions:** COUNT, SUM, AVG
  2. **User-Defined Functions (UDFs)**
     - Custom functions created for specific operations.
     - Example:
       ```sql
       DELIMITER $$
       CREATE FUNCTION calculate_bonus(salary DECIMAL(10,2)) 
       RETURNS DECIMAL(10,2)
       DETERMINISTIC
       BEGIN
           RETURN salary * 0.10;
       END $$
       DELIMITER ;
       ```
     - Usage:
       ```sql
       SELECT first_name, last_name, salary, calculate_bonus(salary) AS bonus FROM employees;
       ```
### GROUP BY & HAVING
- **GROUP BY** - Groups rows based on column values.
- **HAVING** - Filters grouped data (similar to WHERE but used with GROUP BY).
- **GROUP_CONCAT** - Concatenates values from multiple rows into a single string.
  - Example:
    ```sql
    SELECT department, GROUP_CONCAT(employee_name) AS employees
    FROM employees
    GROUP BY department;
    ```
   - Output:
     ```
      +------------+------------------+
      | department | employees        |
      +------------+------------------+
      | Finance    | Eve              |
      | HR         | Alice,Bob        |
      | IT         | Charlie,David    |
      +------------+------------------+
     ```
- **WITH ROLLUP** - Provides summary rows for aggregated data.
  - Example:
    ```sql
    SELECT department, SUM(salary) AS total_salary
    FROM employees
    GROUP BY department WITH ROLLUP;
    ```
  - Output:

    ```
      +------------+--------------+
      | department | total_salary |
      +------------+--------------+
      | Finance    | 65000        |
      | HR         | 105000       |
      | IT         | 142000       |
      | NULL       | 312000       | -- Total sum across all departments
      +------------+--------------+
    ```

### CASE WHEN
- Used for conditional logic within SQL queries.
- Example:
  ```sql
  SELECT name, salary,
         CASE 
             WHEN salary > 50000 THEN 'High'
             WHEN salary BETWEEN 30000 AND 50000 THEN 'Medium'
             ELSE 'Low'
         END AS Salary_Category
  FROM employees;
  ```
  - Output:
    ```
    +--------+--------+----------------+
    | name   | salary | Salary_Category|
    +--------+--------+----------------+
    | John   | 60000  | High           |
    | Jane   | 45000  | Medium         |
    | Mike   | 25000  | Low            |
    +--------+--------+----------------+
    ```

### Joins in SQL

<img width="1193" alt="image" src="https://github.com/user-attachments/assets/8ada7a85-bf8a-485c-a2d1-dab8b84d1090" />

1. **INNER JOIN** - Returns only matching records from both tables.
2. **LEFT JOIN** - Returns all records from the left table and matching records from the right table.
3. **RIGHT JOIN** - Returns all records from the right table and matching records from the left table.
4. **CROSS JOIN** - Produces a Cartesian product of two tables.
5. **SELF JOIN** - Joins a table with itself.
6. **FULL OUTER JOIN** - Returns all records from both tables, filling NULLs where no match exists.


### Things to Remember
- SQL keywords are **not** case-sensitive.
- Some database systems require a semicolon (`;`) at the end of queries.

