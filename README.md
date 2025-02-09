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

