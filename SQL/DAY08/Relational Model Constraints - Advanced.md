# Relational Model Constraints: Advanced

## 1. Beyond Basic Constraints

While primary keys and domain checks form the foundation, enterprise database architectures require advanced constraints to manage complex business logic, cascade rules, and deferred evaluation.

---

## 2. Referential Action Policies (`ON DELETE` / `ON UPDATE`)

When a parent row referenced by a foreign key is updated or deleted, the database must enforce referential integrity according to a pre-defined policy:

```text
Parent Row (e.g., Customer #42) Deleted
                  |
    +-------------+-------------+-------------+-------------+
    |                           |                           |
    v                           v                           v
CASCADE                     SET NULL                    RESTRICT / NO ACTION
Delete all child Orders     Set child customer_id       Block deletion if child
placed by Customer #42      to NULL                     Orders exist (Throws Error)
```

### 1. `CASCADE`
Automatically deletes or updates matching rows in the child table when the parent row is deleted or updated.
- *Best for*: Dependent data that has no meaning without the parent (e.g., deleting an `Order` cascades to its `Order_Items`).

```sql
CREATE TABLE order_items (
    order_id INT REFERENCES orders(order_id) ON DELETE CASCADE,
    item_id INT,
    quantity INT,
    PRIMARY KEY (order_id, item_id)
);
```

### 2. `SET NULL`
Sets the foreign key column in the child table to `NULL` when the parent row is deleted.
- *Requirement*: The FK column must be nullable (cannot have a `NOT NULL` constraint).
- *Best for*: Optional links (e.g., when a `Department` is dissolved, set the employees' `department_id` to NULL).

### 3. `RESTRICT` / `NO ACTION` (Default)
Prevents deletion or updating of the parent row if any child rows reference it.
- *Best for*: Financial or audit data where accidental deletion must be strictly forbidden (e.g., cannot delete a `Customer` if historical `Invoices` exist).

---

## 3. Composite Constraints

Constraints that span multiple columns are known as composite constraints:

### Composite Primary Key
```sql
CREATE TABLE project_assignments (
    employee_id INT REFERENCES employees(employee_id),
    project_id INT REFERENCES projects(project_id),
    role VARCHAR(50),
    PRIMARY KEY (employee_id, project_id) -- Composite Primary Key
);
```

### Composite Unique Constraint
Enforces that the *combination* of two or more columns is unique, even if individual values duplicate:
```sql
CREATE TABLE seat_reservations (
    flight_id VARCHAR(10) NOT NULL,
    seat_number VARCHAR(5) NOT NULL,
    passenger_name VARCHAR(100) NOT NULL,
    CONSTRAINT uq_flight_seat UNIQUE (flight_id, seat_number)
);
```

---

## 4. Immediate vs. Deferred Constraint Checking

By default, SQL constraints are **immediate**—evaluated after every individual SQL statement:
- If an `INSERT` or `UPDATE` violates a constraint, it fails immediately.

In complex transactions (such as circular foreign keys where Table A references Table B and Table B references Table A), immediate checking makes inserts impossible. **Deferred constraints** solve this:

```sql
-- PostgreSQL Syntax for Deferrable Constraints
CREATE TABLE accounts (
    account_id INT PRIMARY KEY,
    owner_id INT,
    CONSTRAINT fk_owner FOREIGN KEY (owner_id) 
        REFERENCES users(user_id) 
        DEFERRABLE INITIALLY DEFERRED
);
```
- **`INITIALLY DEFERRED`**: Constraint checking is postponed until the transaction issues `COMMIT`. If valid at commit time, the transaction succeeds; otherwise, it rolls back entirely.

---

## 5. Summary & Best Practices

1. Use **`ON DELETE CASCADE`** strictly for parent-child ownership relationships (e.g., invoices -> invoice lines).
2. Use **`ON DELETE RESTRICT`** for core master entities (e.g., users, products).
3. Use **composite unique constraints** to prevent duplicate links in association tables.
4. Name all constraints explicitly (`CONSTRAINT fk_name ...`) to ensure clean error handling and maintainable migrations.
