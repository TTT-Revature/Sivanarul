# Relational Model Concepts

## 1. History and Background

The **Relational Model** was introduced in 1970 by computer scientist **Edgar F. (E.F.) Codd** in his landmark paper: *"A Relational Model of Data for Large Shared Data Banks"*.

Prior to the relational model, databases used hierarchical and network models where programmers had to write low-level code navigating physical memory addresses and pointer links. Codd revolutionized data management by:
- Basing data representation on formal **set theory** and **first-order predicate logic**.
- Separating the **logical structure** of data from its **physical storage**.
- Enabling declarative querying via relational algebra (which gave birth to **SQL**).

---

## 2. Formal Terminology vs. Commercial SQL Terms

The mathematical foundation of the relational model uses formal terms that directly map to standard SQL concepts:

| Formal Relational Term | Commercial SQL Term | Plain English Meaning |
| :--- | :--- | :--- |
| **Relation** | **Table** | A 2D structure containing rows and columns |
| **Tuple** | **Row** / Record | A single instance/record in the table |
| **Attribute** | **Column** / Field | A named property or characteristic |
| **Domain** | **Data Type** / Constraints | The valid set of allowable atomic values |
| **Degree (Arity)** | **Column Count** | Total number of attributes in the relation |
| **Cardinality** | **Row Count** | Total number of tuples in the relation |
| **Relation Schema** | **Table Definition** | Name of the table and list of column definitions |
| **Relation State** | **Table Contents** | The current set of rows in the table at a given moment |

```text
Relation: EMPLOYEES (Degree = 4, Cardinality = 3)
+------------+------------+---------------+----------+  <-- Attributes (Columns)
| emp_id     | first_name | email         | salary   |
+------------+------------+---------------+----------+
| 101        | Alice      | a@corp.com    | 75000.00 |  <-- Tuple 1 (Row)
| 102        | Bob        | b@corp.com    | 62000.00 |  <-- Tuple 2 (Row)
| 103        | Charlie    | c@corp.com    | 81000.00 |  <-- Tuple 3 (Row)
+------------+------------+---------------+----------+
```

---

## 3. Fundamental Properties of Relations

For a mathematical table to qualify as a true relation, it must strictly satisfy the following criteria:

### 1. Attribute Values Must Be Atomic
Every cell in a relation must contain exactly one indivisible value (First Normal Form - 1NF). Repeating groups or array lists packed into a single string cell violate pure relational theory.

### 2. Rows (Tuples) Have No Inherent Order
A relation is mathematically a **set** of tuples. Sets are unordered collections. Querying a table without an explicit `ORDER BY` clause guarantees no specific row sequence.

### 3. Columns (Attributes) Have No Inherent Order
Columns are identified by their names, not by their physical left-to-right index.

### 4. All Tuples Must Be Distinct
Because a relation is a set, duplicate tuples cannot theoretically exist. In practice, a table enforces this by defining a **Primary Key**.

---

## 4. Understanding Keys in the Relational Model

Keys are the mechanism by which individual tuples are identified and relationships are established:

```text
+-------------------------------------------------------------+
|  SUPER KEYS                                                 |
|  (Any set of attributes that uniquely identifies a row)     |
|                                                             |
|    +---------------------------------------------------+    |
|    |  CANDIDATE KEYS                                   |    |
|    |  (Minimal Super Key - no redundant columns)       |    |
|    |                                                   |    |
|    |    +--------------------+   +----------------+    |    |
|    |    |    PRIMARY KEY     |   | ALTERNATE KEYS |    |    |
|    |    | (Chosen identifier)|   | (Unchosen CKs) |    |    |
|    |    +--------------------+   +----------------+    |    |
|    +---------------------------------------------------+    |
+-------------------------------------------------------------+
```

### 1. Super Key (SK)
Any attribute or combination of attributes that uniquely identifies a tuple within a relation.
- *Example*: `{emp_id}`, `{emp_id, email}`, `{emp_id, salary}` are all super keys.

### 2. Candidate Key (CK)
A **minimal super key** from which no attribute can be removed without losing the uniqueness property.
- *Example*: `{emp_id}` is a candidate key. `{email}` is also a candidate key. `{emp_id, email}` is NOT a candidate key because `{emp_id}` alone is sufficient.

### 3. Primary Key (PK)
The candidate key chosen by the database architect as the official unique identifier for tuples in the table. Must be strictly `NOT NULL` and `UNIQUE`.

### 4. Alternate Key (AK)
Candidate keys that were not selected as the primary key. In SQL, these are implemented using `UNIQUE` constraints.

### 5. Foreign Key (FK)
An attribute (or set of attributes) in one table that references the Primary Key (or Candidate Key) of another table, establishing a referential link between them.

---

## 5. Summary & Key Takeaways

1. The relational model models data as mathematical relations (tables) governed by set logic.
2. Tables consist of rows (tuples) and columns (attributes).
3. The degree is the number of columns; the cardinality is the number of rows.
4. Candidate keys are minimal unique identifiers; one is designated as the Primary Key.
