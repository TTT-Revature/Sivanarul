# CREATE TABLE Statement

## 1. Introduction

The `CREATE TABLE` statement is the fundamental DDL command used to establish a new table within a database schema, specifying its column names, data types, default values, and integrity constraints.

```text
+--------------------------------------------------------------------------+
|  CREATE TABLE [schema.]table_name (                                      |
|      column1_name data_type [column_constraints],                         |
|      column2_name data_type [column_constraints],                         |
|      ...                                                                 |
|      [table_level_constraints]                                           |
|  );                                                                      |
+--------------------------------------------------------------------------+
```

---

## 2. Anatomy of Column Definitions

Each column in a `CREATE TABLE` definition consists of:
1. **Column Name**: Identifier adhering to naming conventions (snake_case recommended).
2. **Data Type**: Memory representation (e.g., `VARCHAR`, `INT`, `DECIMAL`, `DATE`).
3. **Nullability**: `NOT NULL` (mandatory) or `NULL` (optional).
4. **Default Value**: `DEFAULT <expression>` if omitted during insert.
5. **Inline Constraint**: E.g., `PRIMARY KEY`, `UNIQUE`, `CHECK`.

---

## 3. Column-Level vs. Table-Level Constraints

Constraints can be declared either **inline (column-level)** or **at the bottom (table-level)**:

- **Column-Level**: Placed directly after the column definition. Suitable for single-column rules.
- **Table-Level**: Placed after all column definitions. **Mandatory** for composite keys (keys that combine two or more columns) and allows explicit constraint naming.

```sql
-- Example contrasting Column-Level vs Table-Level
CREATE TABLE course_registrations (
    -- Column-level constraints
    registration_id BIGINT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    student_id INT NOT NULL,
    course_id VARCHAR(10) NOT NULL,
    registered_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
    status VARCHAR(15) DEFAULT 'PENDING' CHECK (status IN ('PENDING', 'CONFIRMED', 'CANCELLED')),

    -- Table-level composite constraint (spans two columns)
    CONSTRAINT uq_student_course UNIQUE (student_id, course_id),

    -- Table-level foreign key constraints with explicit names
    CONSTRAINT fk_reg_student FOREIGN KEY (student_id) REFERENCES students(student_id) ON DELETE CASCADE,
    CONSTRAINT fk_reg_course FOREIGN KEY (course_id) REFERENCES courses(course_id) ON DELETE RESTRICT
);
```

---

## 4. Production-Grade Example: Banking Application

Let us build a complete production-grade schema for a banking subsystem:

```sql
-- 1. Create Customers Table
CREATE TABLE customers (
    customer_id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    email VARCHAR(100) NOT NULL UNIQUE,
    national_id VARCHAR(20) NOT NULL UNIQUE,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

-- 2. Create Bank Accounts Table
CREATE TABLE bank_accounts (
    account_number VARCHAR(16) PRIMARY KEY,
    customer_id INT NOT NULL,
    account_type VARCHAR(20) NOT NULL,
    balance NUMERIC(15, 2) NOT NULL DEFAULT 0.00,
    currency VARCHAR(3) NOT NULL DEFAULT 'USD',
    is_active BOOLEAN NOT NULL DEFAULT TRUE,
    opened_date DATE NOT NULL DEFAULT CURRENT_DATE,

    -- Business checks
    CONSTRAINT chk_account_type CHECK (account_type IN ('CHECKING', 'SAVINGS', 'INVESTMENT')),
    CONSTRAINT chk_positive_balance CHECK (balance >= 0.00),
    CONSTRAINT chk_valid_currency CHECK (currency IN ('USD', 'EUR', 'GBP', 'INR')),

    -- Foreign Key Relationship
    CONSTRAINT fk_account_owner FOREIGN KEY (customer_id) 
        REFERENCES customers(customer_id) 
        ON DELETE RESTRICT
);
```

---

## 5. Useful CREATE TABLE Variants

### A. `CREATE TABLE IF NOT EXISTS`
Prevents execution errors if a table with the same name already exists in the schema. Crucial for automated deployment scripts and idempotent CI/CD migrations.
```sql
CREATE TABLE IF NOT EXISTS audit_logs (
    log_id BIGINT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    action_description TEXT NOT NULL,
    logged_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### B. `CREATE TABLE AS SELECT` (CTAS)
Creates a new table and immediately populates it with the results of a `SELECT` query.
```sql
CREATE TABLE vip_customers AS
SELECT customer_id, first_name, last_name, email
FROM customers
WHERE customer_id IN (
    SELECT customer_id FROM bank_accounts WHERE balance > 100000.00
);
```
*(Note: CTAS copies column data and nullability, but typically does NOT copy indexes, auto-increment sequences, or foreign keys).*

---

## 6. Common Mistakes

1. **Omitting `NOT NULL` on business-critical fields**: Allowing NULL emails or order totals causes silent application bugs.
2. **Anonymous Constraints**: Writing `PRIMARY KEY` or `FOREIGN KEY` without naming them makes debugging error logs difficult (`"violates constraint fk_account_owner"` is vastly superior to `"violates constraint sys_c001239"`).
3. **Using imprecise data types for monetary values**: Never use `FLOAT` or `DOUBLE` for financial figures; always use exact `NUMERIC(p, s)` / `DECIMAL(p, s)`.
