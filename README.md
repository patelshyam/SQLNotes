
# SQL Notes

- [SQL Notes](#sql-notes)
    * [Database Management System (DBMS)](#database-management-system-dbms)
        + [What is a Database?](#what-is-a-database)
        + [What is DBMS?](#what-is-dbms)
        + [Types of Databases](#types-of-databases)
        + [What is RDBMS?](#what-is-rdbms)
        + [Transactions in DBMS](#transactions-in-dbms)
        + [States of a Transaction](#states-of-a-transaction)
        + [ACID Properties](#acid-properties)
    * [SQL Fundamentals](#sql-fundamentals)
        + [What is SQL?](#what-is-sql)
        + [What Can SQL Do?](#what-can-sql-do)
        + [MySQL Data Types](#mysql-data-types)
        + [Types of SQL Commands](#types-of-sql-commands)
        + [SQL Constraints](#sql-constraints)
        + [Primary Key](#primary-key)
        + [Foreign Key](#foreign-key)
        + [DELETE Command](#delete-command)
        + [DROP vs TRUNCATE vs DELETE](#drop-vs-truncate-vs-delete)
        + [Functions in SQL](#functions-in-sql)
    * [GROUP BY & HAVING](#group-by-having)
    * [CASE WHEN](#case-when)
    * [Joins in SQL](#joins-in-sql)
    * [MySQL: EXISTS, ANY, and ALL Keywords](#mysql-exists-any-and-all-keywords)
        + [1. `EXISTS`](#1-exists)
        + [2. `ANY`](#2-any)
        + [3. `ALL`](#3-all)
        + [Key Differences:](#key-differences)
        + [Things to Remember](#things-to-remember)
    * [MySQL Window Functions](#mysql-window-functions)
        + [1. Introduction](#1-introduction)
        + [2. Syntax](#2-syntax)
        + [3. Common Window Functions](#3-common-window-functions)
            - [a) ROW_NUMBER()](#a-row_number)
            - [b) RANK()](#b-rank)
            - [c) DENSE_RANK()](#c-dense_rank)
            - [d) FIRST_VALUE()](#d-first_value)
            - [e) LAST_VALUE()](#e-last_value)
            - [f) LAG()](#f-lag)
            - [g) LEAD()](#g-lead)
            - [h) SUM()](#h-sum)
            - [i) AVG()](#i-avg)
            - [PARTITION BY Clause](#partition-by-clause)
            - [ORDER BY Clause](#order-by-clause)
            - [Practical Example](#practical-example)
        + [Frame Clause in Window Functions](#frame-clause-in-window-functions)
            - [Example for **ROWS**](#example-for-rows)
            - [Example for Range ](#example-for-range)
    * [Common Table Expression (CTE)](#common-table-expression-cte)
    * [Subqueries in SQL](#subqueries-in-sql)
    * [Views](#views)
    * [Indexing](#indexing)
        + [Why indexing is Important?](#why-indexing-is-important)
        + [How to choose the right Indexing Column](#how-to-choose-the-right-indexing-column)
    * [Query Optimization](#query-optimization)

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
       
## GROUP BY & HAVING
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

## CASE WHEN
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

## Joins in SQL

<img width="1193" alt="image" src="https://github.com/user-attachments/assets/8ada7a85-bf8a-485c-a2d1-dab8b84d1090" />

1. **INNER JOIN** - Returns only matching records from both tables.
2. **LEFT JOIN** - Returns all records from the left table and matching records from the right table.
3. **RIGHT JOIN** - Returns all records from the right table and matching records from the left table.
4. **CROSS JOIN** - Produces a Cartesian product of two tables.
5. **SELF JOIN** - Joins a table with itself.
6. **FULL OUTER JOIN** - Returns all records from both tables, filling NULLs where no match exists.

## MySQL: EXISTS, ANY, and ALL Keywords

### 1. `EXISTS`
- **Purpose:** Used to check if a subquery returns any rows.
- **Returns:** `TRUE` if the subquery returns one or more rows, otherwise `FALSE`.

**Example:**
```sql
SELECT name FROM employees
WHERE EXISTS (
  SELECT 1 FROM departments
  WHERE departments.id = employees.dept_id AND departments.name = 'HR'
);
```

### 2. `ANY`
- **Purpose:** Compares a value to each value in a list or subquery and returns `TRUE` if **any one** of the comparisons is `TRUE`.
- **Often used with:** `=`, `>`, `<`, `>=`, `<=`, or `<>`.

**Example:**
```sql
SELECT name FROM employees
WHERE salary > ANY (
  SELECT salary FROM employees WHERE dept_id = 2
);
```

### 3. `ALL`
- **Purpose:** Compares a value to **all values** in a list or subquery and returns `TRUE` only if **all comparisons** are `TRUE`.
- **Often used with:** `=`, `>`, `<`, `>=`, `<=`, or `<>`.

**Example:**
```sql
SELECT name FROM employees
WHERE salary > ALL (
  SELECT salary FROM employees WHERE dept_id = 3
);
```

### Key Differences:
- `EXISTS`: Focuses on the **existence** of rows.
- `ANY`: Checks if **at least one** comparison is `TRUE`.
- `ALL`: Requires **every** comparison to be `TRUE`.

### Things to Remember
- SQL keywords are **not** case-sensitive.
- Some database systems require a semicolon (`;`) at the end of queries.

## MySQL Window Functions

### 1. Introduction
Window functions perform calculations across a set of table rows related to the current row within a query result.

### 2. Syntax
```sql
SELECT column_name, 
       window_function() OVER (PARTITION BY column_name ORDER BY column_name) AS result
FROM table_name;
```

### 3. Common Window Functions

#### a) ROW_NUMBER()
Assigns a unique number to each row based on the specified order.
```sql
SELECT name, salary,
       ROW_NUMBER() OVER (ORDER BY salary DESC) AS rank
FROM employees;
```

#### b) RANK()
Ranks each row within a partition, with gaps for ties.
```sql
SELECT name, salary,
       RANK() OVER (ORDER BY salary DESC) AS rank
FROM employees;
```

#### c) DENSE_RANK()
Ranks rows without gaps for ties.
```sql
SELECT name, salary,
       DENSE_RANK() OVER (ORDER BY salary DESC) AS rank
FROM employees;
```

#### d) FIRST_VALUE()
Returns the first value in an ordered partition.
```sql
SELECT name, salary,
       FIRST_VALUE(name) OVER (PARTITION BY department ORDER BY salary) AS lowest_paid
FROM employees;
```

#### e) LAST_VALUE()
Returns the last value in an ordered partition.
```sql
SELECT name, salary,
       LAST_VALUE(name) OVER (PARTITION BY department ORDER BY salary RANGE BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING) AS highest_paid
FROM employees;
```

#### f) LAG()
Returns the value from the previous row.
```sql
SELECT name, salary,
       LAG(salary) OVER (PARTITION BY department ORDER BY salary) AS previous_salary
FROM employees;
```

#### g) LEAD()
Returns the value from the next row.
```sql
SELECT name, salary,
       LEAD(salary) OVER (PARTITION BY department ORDER BY salary) AS next_salary
FROM employees;
```

#### h) SUM()
Calculates a cumulative sum.
```sql
SELECT department, salary,
       SUM(salary) OVER (PARTITION BY department ORDER BY salary) AS cumulative_salary
FROM employees;
```

#### i) AVG()
Calculates a moving average.
```sql
SELECT department, salary,
       AVG(salary) OVER (PARTITION BY department ORDER BY salary) AS avg_salary
FROM employees;
```

#### PARTITION BY Clause
Splits the result set into partitions.
```sql
SELECT department, name, salary,
       SUM(salary) OVER (PARTITION BY department) AS department_total
FROM employees;
```

#### ORDER BY Clause
Specifies the order of rows within each partition.
```sql
SELECT name, hire_date,
       ROW_NUMBER() OVER (PARTITION BY department ORDER BY hire_date) AS seniority
FROM employees;
```

#### Practical Example
```sql
SELECT name, department, salary,
       SUM(salary) OVER (PARTITION BY department ORDER BY salary) AS running_total,
       RANK() OVER (PARTITION BY department ORDER BY salary DESC) AS salary_rank
FROM employees;
```
### Frame Clause in Window Functions
- The frame clause in window functions defines the **subset of rows('Frame')** used for caluculating the result of the function for the current row.
- It is specified with the OVER() clause after PARTATION BY and ORDER BY.
- The frame is defined by two parts: **a start** and an **end**, each relative to the **current row**.
  ```sql
      function_name (expression) OVER (
         [PARTITION BY column_name_1, ..., column_name_n]
         [ORDER BY column_name_1 [ASC | DESC], ..., column_name_n [ASC | DESC]]
         [ROWS|RANGE frame_start TO frame_end]
      )
    ```
- The frame start can be:
   - UNBOUNDED PRECEDING (starts at the first row of the partition)
   - N PRECEDING (starts N rows before the current row)
   - CURRENT ROW (starts at the current row)
- The frame end can be:
   - UNBOUNDED FOLLOWING (ends at the last row of the partition)
   - N FOLLOWING (ends N rows after the current row)
   - CURRENT ROW (ends at the current row)
- For ROWS, the frame consists of N rows coming before or after the current row
- For RANGE, the frame consists of rows within a certain value range relative to the value in current row.

<img width="1011" alt="image" src="https://github.com/user-attachments/assets/727db737-1e16-4d9e-b99b-4cde6d6d39cd" />

#### Example for **ROWS**

```sql
   SELECT date, revenue,
      SUM(revenue) OVER (
      ORDER BY date
      ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
   ) running_total
   FROM sales
      ORDER BY date;
```
<img width="1261" alt="image" src="https://github.com/user-attachments/assets/aa886309-7cf4-43ab-8750-5b41cce50749" />

#### Example for Range 

```sql
    SELECT
        shop,
        date,
        revenue_amount,
        MAX(revenue_amount) OVER (
        ORDER BY DATE
        RANGE BETWEEN INTERVAL '3' DAY PRECEDING
        AND INTERVAL '1' DAY FOLLOWING
        ) AS max_revenue
    FROM revenue_per_shop;
```
<img width="483" alt="image" src="https://github.com/user-attachments/assets/ef6f993d-c21e-4562-9d7e-16838e8aa104" />


## Common Table Expression (CTE)

A Common Table Expression (CTE) in SQL is a named temporary result set that exists only within the execution
scope of a single SQL statement

- CTEs can be thought of as alternatives to derived tables, inline views, or subqueries.
- They can be used in SELECT, INSERT, UPDATE, or DELETE statements.
- CTEs help to simplify complex queries, particularly those involving multiple subqueries or recursive queries.
- They make your query more readable and easier to maintain.
- A CTE is defined using the WITH keyword, followed by the CTE name and a query. The CTE can then be
  referred to by its name elsewhere in the query.

```sql
    WITH 
    sales_cte AS 
        (SELECT sales_person, SUM(sales_amount) as total_sales
                   FROM sales_table
                   GROUP BY sales_person)
    SELECT sales_person, total_sales
    FROM sales_cte
    WHERE total_sales > 1000;
```

## Subqueries in SQL

- **IN:-** The IN operator allows you to specify multiple values in a WHERE clause. It returns true if a value
  matches any value in a list.

```sql
    SELECT * FROM employees
    WHERE department_id IN (10, 20, 30);
```
- **NOT IN:-** The NOT IN operator excludes the values in the list. It returns true if a value does not match
  any value in the list.
- **ANY:-** The ANY operator returns true if any subquery value meets the condition.
```sql
    SELECT * FROM employees
    WHERE department_id ANY > (SELECT salary FROM employees WHERE department_id = 10);
```
- **ALL:-** The ALL operator returns true if all subquery value meets the condition.
```sql
    SELECT * FROM employees
    WHERE department_id ALL > (SELECT salary FROM employees WHERE department_id = 10);
```
- **EXISTS:-** The EXISTS operator returns true if the subquery returns one or more records.
- **NOT EXISTS:-** The NOT EXISTS operator returns true if the subquery returns no records.

The difference between In and Any,All operators is that with Any and All you can use the comparison operators like =,>,<

## Views
- A view in SQL is a virtual table based on the result-set of an SQL statement. It contains rows and
  columns, just like a real table. The fields in a view are fields from one or more real tables in the
  database.

- You can add SQL functions, WHERE, and JOIN statements to a view and display the data as
  if the data were coming from one single table.
- A view always shows up-to-date data. The database engine recreates the data every time a
  user queries a view.
- Views can be used to encapsulate complex queries, presenting users with a simpler interface
  to the data.
- They can be used to restrict access to sensitive data in the underlying tables, presenting only
  non-sensitive data to users.

```sql
    CREATE VIEW View_Products AS
    SELECT ProductName, Price
    FROM Products
    WHERE Price > 30;
```
## Indexing
- Indexing in databases involves creating a data structure that improves the speed of data retrieval operations on a 
  database table. Indexes are used to quickly locate data without having to search every row in a table each time a 
  database table is accessed.

### Why indexing is Important?
- **Speeding up Query Execution:** Indexes reduce the amount of data that needs to be scanned for a query, 
  significantly speeding up data retrieval operations. 
- **Optimizing Search Operations:** Indexes help in efficiently searching for records based on the indexed columns.
- **Improving Sorting and Filtering:** Indexes assist in sorting and filtering operations by providing a structured way 
    to access data.
- **Enhancing Join Performance:** Indexes on join columns improve the performance of join operations between tables.

### How to choose the right Indexing Column
- **Primary Key and Unique Constraints:** Always index columns that are primary keys or have unique constraints, as they 
uniquely identify rows.
- **Frequently Used Columns in WHERE Clauses:** Index columns that are frequently used in WHERE clauses to filter data.
- **Columns Used in Joins:** Index columns that are used in join conditions to speed up join operations.
- **Columns Used in ORDER BY and GROUP BY:** Index columns that are used in ORDER BY and GROUP BY clauses for faster 
  sorting and grouping.
- **Selectivity of the Column:** Choose columns with high selectivity (columns with many unique values) to maximize 
  the performance benefits of the index.

## Query Optimization
- Use Column Names Instead of * in a SELECT Statement
- Avoid including a HAVING clause in SELECT statements

  - Bad example
    ```sql
     SELECT s.cust_id,count(s.cust_id)
     FROM SH.sales s
     GROUP BY s.cust_id
     HAVING s.cust_id != '1660' AND s.cust_id != '2';
    ``` 
  - Optimized example

    ```sql
    SELECT s.cust_id,count(cust_id)
    FROM SH.sales s
    WHERE s.cust_id != '1660'
    AND s.cust_id !='2'
    GROUP BY s.cust_id;
    ```
- Consider using an IN predicate when querying an indexed column for example do not do where s.prod = 17 or s.prod = 
  18 instead use IN operator
- Try to use UNION ALL in place of UNION
  - The UNION ALL statement is faster than UNION, because UNION ALL statement does not consider duplicate s, and UNION statement
    does look for duplicates in a table while selection of rows, whether or not they exist.
  - Bad Example
    - ```sql
      SELECT cust_id
      FROM SH.sales
      UNION
      SELECT cust_id
      FROM customers;
      ```
    - Optimized Example
      ```sql
      SELECT cust_id
      FROM SH.sales
      UNION ALL
      SELECT cust_id
      FROM customers;
        ```