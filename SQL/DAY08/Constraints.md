# SQL Constraints

## 1. What Are Constraints?

Constraints are declarative validation rules applied to columns or tables to maintain **Entity Integrity**, **Referential Integrity**, and **Domain Integrity**. They are enforced automatically by the database engine on every `INSERT`, `UPDATE`, and `DELETE`.

---

## 2. The Six Essential SQL Constraints

```text
+-------------------+-------------------------------------------------------------+
| CONSTRAINT        | PURPOSE                                                     |
+-------------------+-------------------------------------------------------------+
| 1. PRIMARY KEY    | Uniquely identifies each row; strictly NOT NULL + UNIQUE.   |
| 2. FOREIGN KEY    | Enforces referential relationship to another table's PK.    |
| 3. UNIQUE         | Guarantees all values in a column are distinct.             |
| 4. NOT NULL       | Forbids NULL (missing/empty) values.                        |
| 5. CHECK          | Validates values against a boolean expression.              |
| 6. DEFAULT        | Injects a pre-defined value when none is supplied.          |
+-------------------+-------------------------------------------------------------+
```

---

## 3. Comprehensive Syntax & Practical Implementation

```sql
CREATE TABLE products (
    -- 1. PRIMARY KEY
    product_id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,

    -- 2. NOT NULL + UNIQUE
    sku VARCHAR(20) NOT NULL UNIQUE,

    -- 3. NOT NULL
    product_name VARCHAR(100) NOT NULL,

    -- 4. CHECK constraint
    retail_price NUMERIC(10, 2) NOT NULL CHECK (retail_price >= 0.01),
    discount_percentage NUMERIC(5, 2) DEFAULT 0.00 CHECK (discount_percentage BETWEEN 0.00 AND 100.00),

    -- 5. DEFAULT constraint
    is_in_stock BOOLEAN NOT NULL DEFAULT TRUE,
    created_at TIMESTAMP WITH TIME ZONE NOT NULL DEFAULT CURRENT_TIMESTAMP,

    -- 6. Table-level CHECK spanning multiple columns
    CONSTRAINT chk_price_discount CHECK (retail_price * (1 - discount_percentage / 100.0) >= 0)
);
```

---

## 4. Managing Constraints with `ALTER TABLE`

In production environments, schemas evolve. You often need to add, modify, or drop constraints after table creation:

### A. Adding Constraints
```sql
-- Add a UNIQUE constraint
ALTER TABLE products 
ADD CONSTRAINT uq_product_name UNIQUE (product_name);

-- Add a CHECK constraint
ALTER TABLE products 
ADD CONSTRAINT chk_sku_format CHECK (LENGTH(sku) >= 6);

-- Add a FOREIGN KEY constraint
ALTER TABLE products 
ADD COLUMN category_id INT;

ALTER TABLE products 
ADD CONSTRAINT fk_product_category 
FOREIGN KEY (category_id) REFERENCES categories(category_id) 
ON DELETE SET NULL;
```

### B. Dropping Constraints
```sql
-- Drop by explicit constraint name
ALTER TABLE products 
DROP CONSTRAINT chk_sku_format;

-- Drop NOT NULL (PostgreSQL syntax)
ALTER TABLE products 
ALTER COLUMN product_name DROP NOT NULL;
```

---

## 5. Constraint Violations in Action

```sql
-- Fails: retail_price violates CHECK (retail_price >= 0.01)
INSERT INTO products (sku, product_name, retail_price) 
VALUES ('SKU-1001', 'Free Sticker', -5.00);
-- ERROR: new row for relation "products" violates check constraint "products_retail_price_check"

-- Fails: Duplicate SKU violates UNIQUE constraint
INSERT INTO products (sku, product_name, retail_price) VALUES ('SKU-1002', 'Pen', 2.00);
INSERT INTO products (sku, product_name, retail_price) VALUES ('SKU-1002', 'Pencil', 1.00);
-- ERROR: duplicate key value violates unique constraint "products_sku_key"
```

---

## 6. Key Takeaways

- Constraints ensure database consistency independent of application code.
- Always provide explicit, descriptive constraint names (`CONSTRAINT pk_...`, `CONSTRAINT fk_...`, `CONSTRAINT chk_...`).
- Combine `CHECK` constraints with business domains to catch data anomalies early.
