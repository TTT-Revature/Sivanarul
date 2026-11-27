# Relational Model Constraints: Introduction

## 1. Why Do We Need Constraints?

In database systems, **constraints** are declarative rules and restrictions enforced on table columns and relations. Their sole purpose is to guarantee **Data Integrity**—ensuring data remains accurate, valid, and trustworthy throughout its lifecycle.

Without constraints, the database becomes vulnerable to the **GIGO Principle (Garbage In, Garbage Out)**:
- Users could insert negative salaries.
- Duplicate customer IDs could be issued.
- Orders could reference non-existent customers.
- Critical fields like email or phone numbers could be accidentally omitted.

```text
+-----------------------+     Violates Constraint     +--------------------------+
|  Client Application   | --------------------------> |    DATABASE ENGINE       |
|  INSERT salary = -500 |                             |   Constraint CHECK fails |
+-----------------------+ <-------------------------- |  Transaction REJECTED    |
                                Error returned        +--------------------------+
```

---

## 2. The Three Fundamental Relational Integrity Rules

The relational model mandates three core integrity rules that any production-grade relational database must enforce:

```text
                               +-----------------------------+
                               |     RELATIONAL INTEGRITY    |
                               +-----------------------------+
                                              |
             +--------------------------------+-------------------------------+
             |                                |                               |
             v                                v                               v
+-------------------------+      +-------------------------+      +-------------------------+
|    DOMAIN INTEGRITY     |      |    ENTITY INTEGRITY     |      |  REFERENTIAL INTEGRITY  |
|                         |      |                         |      |                         |
| - Data types            |      | - Primary Key must be   |      | - Foreign Key must      |
| - NOT NULL              |      |   UNIQUE                |      |   reference valid PK    |
| - CHECK value ranges    |      | - Primary Key CANNOT    |      |   or be NULL            |
| - DEFAULT values        |      |   contain NULL          |      |                         |
+-------------------------+      +-------------------------+      +-------------------------+
```

---

## 3. Detailed Breakdown of Fundamental Constraints

### A. Domain Integrity
Ensures that all values stored in a column belong to the defined domain (permissible data type, format, length, and range):
- **Data Type**: If a column is defined as `INTEGER`, the string `"twenty"` cannot be inserted.
- **NOT NULL**: Prevents missing or unknown data in columns required for business logic.
- **CHECK**: Enforces logical boundary conditions (e.g., `age >= 18`).

```sql
CREATE TABLE accounts (
    account_id INT PRIMARY KEY,
    account_number VARCHAR(12) NOT NULL UNIQUE,
    balance NUMERIC(12, 2) NOT NULL CHECK (balance >= 0.00), -- Domain CHECK
    status VARCHAR(10) DEFAULT 'ACTIVE' CHECK (status IN ('ACTIVE', 'FROZEN', 'CLOSED'))
);
```

### B. Entity Integrity
Ensures that each row (entity instance) is identifiable and distinguishable from all other rows:
- Every table must have a **Primary Key**.
- **No part of the Primary Key can ever be NULL**.
- Rationale: If a primary key contained NULL, we could not determine which real-world entity that row represents, breaking tuple identity.

```sql
-- Valid
INSERT INTO accounts (account_id, account_number, balance) VALUES (1, 'ACC-1001', 500.00);

-- FAILS with Entity Integrity Violation (NULL Primary Key)
INSERT INTO accounts (account_id, account_number, balance) VALUES (NULL, 'ACC-1002', 1000.00);

-- FAILS with Entity Integrity Violation (Duplicate Primary Key)
INSERT INTO accounts (account_id, account_number, balance) VALUES (1, 'ACC-1003', 250.00);
```

### C. Referential Integrity
Governs relationships between tables. A **Foreign Key (FK)** links a child table to a parent table:
- The Foreign Key value in the child table **must match** an existing Primary Key in the parent table, **OR** it must be `NULL` (if the relationship is optional).
- It prevents "orphaned" child rows that reference non-existent parents.

```sql
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    full_name VARCHAR(100) NOT NULL
);

CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT, -- Foreign Key
    order_total NUMERIC(10, 2) NOT NULL,
    CONSTRAINT fk_customer FOREIGN KEY (customer_id) 
        REFERENCES customers(customer_id)
);
```

---

## 4. Key Takeaways

1. Constraints guard database integrity directly at the storage engine level.
2. **Domain Integrity** governs valid column values (type, range, format).
3. **Entity Integrity** ensures primary keys are unique and non-NULL.
4. **Referential Integrity** prevents orphaned records between parent and child tables.
