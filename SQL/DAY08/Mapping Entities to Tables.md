# Mapping Entities to Tables

## 1. What Is ER-to-Relational Mapping?

Entity-Relationship (ER) modeling is an intuitive, visual technique for conceptual database design. However, relational database engines (PostgreSQL, MySQL, Oracle) do not understand ER diagrams directly; they only execute relational schemas expressed as **tables**, **columns**, and **constraints**.

**ER-to-Relational Mapping** is the formal, algorithmic translation process that converts ER diagrams into clean, normalized relational database schemas.

```text
+----------------------------+
|    CONCEPTUAL ER MODEL     |  (Entities, Attributes, Relationships)
+----------------------------+
               |
               |  Mapping Algorithms & Rules
               v
+----------------------------+
|     RELATIONAL SCHEMA      |  (Tables, Columns, PKs, FKs, Constraints)
+----------------------------+
```

---

## 2. Standard Mapping Rules

### Rule 1: Mapping Strong (Regular) Entity Types
For each strong entity type in the ER schema, create a new table.
- Include all simple attributes as columns.
- Choose one of the key attributes as the **Primary Key (PK)**.

```text
ER Entity: [CUSTOMER (customer_id*, name, email, phone)]
           ↓
Relational Table: CUSTOMERS (customer_id [PK], name, email, phone)
```

### Rule 2: Mapping Weak Entity Types
A weak entity cannot be uniquely identified by its own attributes alone; it depends on an owner entity via an identifying relationship.
- Create a table for the weak entity.
- Include all simple attributes of the weak entity.
- Add the Primary Key of the owner entity as a **Foreign Key (FK)**.
- Form the **Composite Primary Key** from `{Owner_PK, Weak_Entity_Partial_Key}`.

```text
ER: DEPENDENT (dependent_name, birth_date, relationship) owned by EMPLOYEE (employee_id)
    ↓
Table: DEPENDENTS (
    employee_id [PK, FK],
    dependent_name [PK],
    birth_date,
    relationship
)
```

### Rule 3: Mapping 1:1 Binary Relationships
When Entity A and Entity B share a 1:1 relationship:
- **Foreign Key Approach (Most Common)**: Choose one table (preferably the one with total/mandatory participation) and include the other table's PK as an FK with a `UNIQUE` constraint.
- **Merged Table Approach**: If both entities participate totally in the relationship, combine them into a single table.

### Rule 4: Mapping 1:N Binary Relationships
For a 1:N relationship between table A (the "1" side) and table B (the "N" side):
- Put the Primary Key of Table A into Table B as a **Foreign Key**.
- Table B does *not* require a UNIQUE constraint on that FK, allowing multiple rows in B to reference the same row in A.

### Rule 5: Mapping N:M Binary Relationships
For an N:M relationship between Entity A and Entity B:
- Create a dedicated **Junction / Bridge Table**.
- Include the Primary Key of Entity A as an FK.
- Include the Primary Key of Entity B as an FK.
- The Primary Key of the junction table is typically the **composite key** of both foreign keys.
- Include any attributes associated with the relationship itself (e.g., `date_enrolled`, `quantity`).

### Rule 6: Mapping Multivalued Attributes
A relational table column must store atomic values (First Normal Form). If an entity has an attribute that can hold multiple values (e.g., an employee having multiple phone numbers):
- Create a new table for the multivalued attribute.
- Add the entity's PK as an FK.
- The PK of the new table is `{entity_id, attribute_value}`.

```text
ER: Employee with multivalued attribute "phone_numbers"
    ↓
Table: EMPLOYEE_PHONES (
    employee_id [PK, FK],
    phone_number [PK]
)
```

### Rule 7: Mapping Composite Attributes
Composite attributes are attributes that can be divided into smaller sub-parts (e.g., `Address` composed of `Street`, `City`, `State`, `ZipCode`):
- **Flatten the attribute**: Do not create a single column; instead, create a column for each atomic component attribute in the table.

```text
Address -> street_address, city, state, postal_code
```

### Rule 8: Handling Derived Attributes
Derived attributes are values that can be computed from existing stored attributes (e.g., `Age` calculated from `date_of_birth`, or `Total_Amount` calculated from `Quantity * Unit_Price`):
- **Do not store derived attributes directly in physical tables** to avoid synchronization errors.
- Compute them on the fly using SQL `VIEW`, generated columns, or runtime queries.

---

## 3. Complete End-to-End Mapping Example

Consider an **E-Commerce Order System**:

```text
Entities:
  - CUSTOMER: customer_id (PK), name (first, last), email, phone_numbers [multivalued]
  - PRODUCT: product_id (PK), name, price, stock_quantity
  - ORDER: order_id (PK), order_date, shipping_address (street, city, zip)
Relationships:
  - Customer PLACES Order (1:N)
  - Order CONTAINS Product (N:M with attribute quantity, unit_price)
```

### Generated Relational Schema (PostgreSQL DDL)

```sql
-- 1. Regular Entity: Customers (Flattened name, removed multivalued phone)
CREATE TABLE customers (
    customer_id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL
);

-- 2. Multivalued Attribute: Customer Phone Numbers
CREATE TABLE customer_phones (
    customer_id INT NOT NULL,
    phone_number VARCHAR(20) NOT NULL,
    phone_type VARCHAR(15) DEFAULT 'Mobile',
    PRIMARY KEY (customer_id, phone_number),
    CONSTRAINT fk_cust_phones FOREIGN KEY (customer_id) 
        REFERENCES customers(customer_id) ON DELETE CASCADE
);

-- 3. Regular Entity: Products
CREATE TABLE products (
    product_id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    product_name VARCHAR(150) NOT NULL,
    unit_price NUMERIC(10, 2) NOT NULL CHECK (unit_price >= 0),
    stock_quantity INT NOT NULL DEFAULT 0 CHECK (stock_quantity >= 0)
);

-- 4. Entity with 1:N Relationship: Orders (Contains customer_id as FK, flattened address)
CREATE TABLE orders (
    order_id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    customer_id INT NOT NULL,
    order_date TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    shipping_street VARCHAR(150) NOT NULL,
    shipping_city VARCHAR(50) NOT NULL,
    shipping_zip VARCHAR(10) NOT NULL,
    CONSTRAINT fk_order_customer FOREIGN KEY (customer_id) 
        REFERENCES customers(customer_id) ON DELETE RESTRICT
);

-- 5. N:M Relationship Bridge: Order Items
CREATE TABLE order_items (
    order_id INT NOT NULL,
    product_id INT NOT NULL,
    quantity INT NOT NULL CHECK (quantity > 0),
    unit_price NUMERIC(10, 2) NOT NULL,
    PRIMARY KEY (order_id, product_id),
    CONSTRAINT fk_items_order FOREIGN KEY (order_id) 
        REFERENCES orders(order_id) ON DELETE CASCADE,
    CONSTRAINT fk_items_product FOREIGN KEY (product_id) 
        REFERENCES products(product_id) ON DELETE RESTRICT
);
```

---

## 4. Key Takeaways

1. Entities become **Tables**.
2. Simple attributes become **Columns**.
3. Multivalued attributes become **Separate Tables**.
4. 1:N relationships place the PK of the 1-side into the N-side as a **Foreign Key**.
5. N:M relationships require a dedicated **Junction Table**.
6. Composite attributes are **flattened** into individual scalar columns.
