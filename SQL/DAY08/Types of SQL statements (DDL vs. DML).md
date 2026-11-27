# Types of SQL Statements: DDL vs. DML

## 1. The Structure of SQL Sublanguages

SQL (Structured Query Language) is not a monolithic command set; it is divided into five specialized sublanguages based on operational purpose:

```text
+-------------------------------------------------------------------------+
|                         SQL COMMAND CATEGORIES                          |
+-------------------------------------------------------------------------+
       |                  |                 |               |         |
       v                  v                 v               v         v
+--------------+   +--------------+   +------------+   +---------+  +-----+
|     DDL      |   |     DML      |   |    DQL     |   |   DCL   |  | TCL |
| (Definition) |   | (Manipulation|   |  (Query)   |   |(Control)|  |(Txn)|
+--------------+   +--------------+   +------------+   +---------+  +-----+
| CREATE       |   | INSERT       |   | SELECT     |   | GRANT   |  |COMMIT
| ALTER        |   | UPDATE       |   +------------+   | REVOKE  |  |RLBACK
| DROP         |   | DELETE       |                    +---------+  |SAVEP
| TRUNCATE     |   | MERGE        |                                 +-----+
| RENAME       |   +--------------+
+--------------+
```

---

## 2. DDL – Data Definition Language

DDL commands manage the **structure, schema, and metadata** of database objects (databases, tables, views, indexes, schemas).

### Characteristics of DDL
- Modifies database schema, not table data rows.
- **Implicitly auto-commits** in most database engines (cannot be rolled back in MySQL/Oracle).
- Requires administrative or schema-level privileges.

### Core DDL Commands
```sql
-- 1. CREATE: Creates objects
CREATE TABLE employees (
    emp_id INT PRIMARY KEY,
    name VARCHAR(50),
    department VARCHAR(50)
);

-- 2. ALTER: Modifies existing schema
ALTER TABLE employees ADD COLUMN hire_date DATE DEFAULT CURRENT_DATE;

-- 3. RENAME: Renames an existing object or column
ALTER TABLE employees RENAME COLUMN name TO full_name;

-- 4. TRUNCATE: Deletes all rows quickly by deallocating pages
TRUNCATE TABLE employees;

-- 5. DROP: Completely destroys the object and its structure
DROP TABLE employees;
```

---

## 3. DML – Data Manipulation Language

DML commands manage the **actual data records (rows)** stored within tables.

### Characteristics of DML
- Operates on individual rows or sets of rows.
- **Does not modify the schema** or table definitions.
- Fully transactional: changes can be saved with `COMMIT` or undone with `ROLLBACK`.

### Core DML Commands
```sql
-- 1. INSERT: Adds new records
INSERT INTO employees (emp_id, full_name, department) 
VALUES (101, 'Sophia Davis', 'Engineering');

-- 2. UPDATE: Modifies existing values
UPDATE employees 
SET department = 'Research' 
WHERE emp_id = 101;

-- 3. DELETE: Removes specific rows matching a filter
DELETE FROM employees 
WHERE emp_id = 101;
```

---

## 4. DDL vs. DML: Detailed Comparison

| Feature | DDL (Data Definition Language) | DML (Data Manipulation Language) |
| :--- | :--- | :--- |
| **Purpose** | Defines and modifies database structure/schema | Populates, updates, and deletes data within tables |
| **Target** | Database objects (Tables, Indexes, Views) | Data records / Tuples / Rows |
| **Commands** | `CREATE`, `ALTER`, `DROP`, `TRUNCATE`, `RENAME` | `INSERT`, `UPDATE`, `DELETE`, `MERGE` |
| **Transaction / Rollback** | Auto-commits in many RDBMSs (irreversible) | Fully transactional; supports `ROLLBACK` |
| **Trigger Activation** | Does not fire DML row-level triggers | Triggers row-level `AFTER`/`BEFORE` triggers |
| **Resource Impact** | Acquires exclusive schema metadata locks | Acquires row-level or page-level locks |

---

## 5. Critical Distinction: `DELETE` vs. `TRUNCATE` vs. `DROP`

This is one of the most frequent technical interview topics in database engineering:

```text
DELETE FROM table;       --> Scans rows one-by-one, logs each deletion, fires triggers (Slow, Rollbackable)
TRUNCATE TABLE table;    --> Deallocates whole data pages, resets identity (Fast, High-performance)
DROP TABLE table;        --> Destroys data rows AND table definition entirely (Table ceases to exist)
```

| Criteria | `DELETE` | `TRUNCATE` | `DROP` |
| :--- | :--- | :--- | :--- |
| **Classification** | DML | DDL | DDL |
| **WHERE Clause** | **Supported** (`WHERE id = 5`) | **Not Supported** (All rows) | **Not Supported** |
| **Performance** | Slow (row-by-row logging) | Extremely fast (page deallocation) | Instant |
| **Table Structure** | Preserved | Preserved | **Destroyed** |
| **Identity Reset** | Counter does NOT reset | Resets identity counter to seed | Table removed |
| **Triggers** | Fires `ON DELETE` triggers | Bypasses DML triggers | Drops triggers |

---

## 6. Summary & Best Practices

1. Use **DDL** during migrations, CI/CD schema pipelines, and application setup.
2. Use **DML** within your runtime application service layer to manage business records.
3. Prefer **`TRUNCATE`** over `DELETE` when completely clearing staging or temporary cache tables.
4. Always wrap critical DML updates inside explicit transactions (`BEGIN TRANSACTION ... COMMIT`).
