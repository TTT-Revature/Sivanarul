# Information and Data Models

## 1. Introduction: Data vs. Information

In software engineering and data systems, understanding the difference between **data** and **information** is the foundation of database design:

- **Data**: Raw, unprocessed facts, numbers, characters, or symbols without inherent context or meaning.
  - *Example*: `42`, `"John"`, `2026-11-27`, `105.5`
- **Information**: Data that has been processed, organized, structured, or contextualized to make it meaningful and useful for decision-making.
  - *Example*: "Patient John has a body temperature of 105.5°F on 2026-11-27 (which indicates a severe fever requiring immediate clinical intervention)."

```text
+--------------+       Processing & Context       +-------------------+
|   RAW DATA   | -------------------------------> |    INFORMATION    |
| ("John", 42) |   (Structured into columns & rows) | (John is 42 yrs)  |
+--------------+                                  +-------------------+
```

---

## 2. What Is a Data Model?

A **Data Model** is an abstract blueprint or conceptual framework that defines:
1. **Data structures**: How data is represented and stored (tables, rows, trees, graphs).
2. **Relationships**: How different data elements connect to one another.
3. **Data integrity constraints**: Rules that ensure accuracy, validity, and consistency of data.
4. **Operations**: Permissible actions that can be performed on the data (insert, update, delete, query).

### Why Do We Need Data Models?
- Bridges the communication gap between business stakeholders and technical developers.
- Prevents data redundancy and anomalies.
- Ensures consistency across large-scale distributed applications.
- Provides a formal basis for database query optimization.

---

## 3. The Three Levels of Data Abstraction

ANSI/SPARC architecture defines three distinct levels of data modeling, moving from high-level business logic down to low-level hardware storage:

```text
+----------------------------------------------------------------+
|  1. CONCEPTUAL DATA MODEL (High-Level Business View)            |
|     - Entities, Relationships, Business Rules                  |
|     - Technology & DBMS Independent                            |
+-------------------------------+--------------------------------+
                                |
                                v
+----------------------------------------------------------------+
|  2. LOGICAL DATA MODEL (Structural Representation)             |
|     - Tables, Attributes, Keys, Normalization                  |
|     - DBMS-Independent, Relational Rules Applied               |
+-------------------------------+--------------------------------+
                                |
                                v
+----------------------------------------------------------------+
|  3. PHYSICAL DATA MODEL (Implementation Details)               |
|     - Exact Data Types, Indexes, Constraints, Partitioning    |
|     - Specific to PostgreSQL, MySQL, Oracle, etc.              |
+----------------------------------------------------------------+
```

### A. Conceptual Data Model
- **Target Audience**: Business analysts, domain experts, project managers.
- **Components**: Entities (e.g., `Customer`, `Order`), high-level relationships (e.g., "Customer places Order").
- **Example**: An Entity-Relationship (ER) diagram showing entities as rectangles and relationships as diamonds without worrying about primary keys or column data types.

### B. Logical Data Model
- **Target Audience**: Database architects, data engineers, software engineers.
- **Components**: Entities mapped to relations, attributes identified, primary keys and foreign keys defined, normalization (1NF to 3NF/BCNF) applied.
- **Example**: Specifying that `Customer` has `customer_id (PK)`, `email (Unique)`, `full_name`, and `Order` has `order_id (PK)`, `customer_id (FK)`, `order_date`.

### C. Physical Data Model
- **Target Audience**: Database Administrators (DBAs), DevOps engineers, implementation engineers.
- **Components**: Specific storage engines (e.g., InnoDB), exact data types (e.g., `VARCHAR(255)`, `BIGINT UNSIGNED`), indexes (B-Tree, Hash), tablespaces, constraints, foreign key cascade actions.
- **Example**: Writing the concrete SQL `CREATE TABLE` DDL scripts for a target database engine.

---

## 4. Evolution of Data Models

Throughout database history, several primary models have evolved:

| Model | Structural Basis | Primary Strengths | Limitations |
| :--- | :--- | :--- | :--- |
| **Hierarchical Model** (1960s) | Tree / Inverted Tree (1:N only) | Fast for 1:N navigational queries | Cannot naturally represent M:N relationships |
| **Network Model** (1970s) | Graph (records & sets) | Supports M:N relationships | Extremely complex navigational pointers |
| **Relational Model** (1970–Present) | Mathematical relations (Tables with rows & columns) | Declarative querying (SQL), mathematical integrity, independence of physical storage | Requires schema migrations, joins can be expensive on massive scale |
| **Object-Oriented Model** (1990s) | Objects, Classes, Inheritance | Eliminates object-relational impedance mismatch | Lacks standard declarative query engine like SQL |
| **NoSQL / Document / Graph** (2000s–Present) | JSON documents, Key-Value pairs, Graph nodes/edges | Schema flexibility, horizontal scalability | Weak multi-record ACID transactions, eventual consistency |

---

## 5. End-to-End Walkthrough: University Enrollment

Let us examine how a university enrollment system transitions across the three data model levels:

### 1. Conceptual Level
- **Entities**: Student, Course, Professor.
- **Relationships**:
  - A Professor teaches one or more Courses.
  - A Student enrolls in one or more Courses.
  - A Course has many enrolled Students.

### 2. Logical Level
- `Student(student_id [PK], first_name, last_name, email, enrollment_date)`
- `Professor(professor_id [PK], full_name, department, email)`
- `Course(course_id [PK], course_title, credits, professor_id [FK])`
- `Enrollment(enrollment_id [PK], student_id [FK], course_id [FK], grade, semester)`

### 3. Physical Level (PostgreSQL DDL)
```sql
CREATE TABLE professors (
    professor_id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    full_name VARCHAR(100) NOT NULL,
    department VARCHAR(50) NOT NULL,
    email VARCHAR(120) UNIQUE NOT NULL
);

CREATE TABLE courses (
    course_id VARCHAR(10) PRIMARY KEY,
    course_title VARCHAR(150) NOT NULL,
    credits SMALLINT NOT NULL CHECK (credits BETWEEN 1 AND 6),
    professor_id INT REFERENCES professors(professor_id) ON DELETE SET NULL
);

CREATE TABLE students (
    student_id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    email VARCHAR(120) UNIQUE NOT NULL,
    enrollment_date DATE NOT NULL DEFAULT CURRENT_DATE
);

CREATE TABLE enrollments (
    enrollment_id BIGINT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    student_id INT NOT NULL REFERENCES students(student_id) ON DELETE CASCADE,
    course_id VARCHAR(10) NOT NULL REFERENCES courses(course_id) ON DELETE RESTRICT,
    grade VARCHAR(2) CHECK (grade IN ('A+', 'A', 'B', 'C', 'D', 'F', 'W')),
    semester VARCHAR(10) NOT NULL,
    CONSTRAINT uq_student_course_semester UNIQUE (student_id, course_id, semester)
);
```

---

## 6. Common Pitfalls & Best Practices

1. **Jumping straight to Physical SQL**: Designing tables in SQL without first understanding the logical entities leads to circular foreign keys and messy denormalization.
2. **Confusing Data with Information**: Raw numbers without units or metadata lead to incorrect interpretations (e.g., storing `amount = 50` without knowing if currency is USD, EUR, or JPY).
3. **Over-normalization or Premature Denormalization**: Strive for Third Normal Form (3NF) during logical modeling; only denormalize at the physical level when proven performance benchmarks require it.

---

## 7. Quick Review & Practice Exercises

### Conceptual Review
1. What are the key differences between Conceptual, Logical, and Physical data models?
2. Why is physical data independence considered one of the greatest achievements of the relational model?

### Practical Exercise
Create a **Logical Data Model** for an online food delivery application (e.g., UberEats / DoorDash). Identify:
- 4 primary entities
- Primary keys and Foreign keys for each entity
- Cardinality of relationships connecting them
