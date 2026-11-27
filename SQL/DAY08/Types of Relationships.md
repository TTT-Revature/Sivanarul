# Types of Relationships in Relational Databases

## 1. What Is a Relationship in a Database?

In a relational database, data is decomposed into specialized tables to prevent duplication (normalization). A **relationship** is a logical association or link established between two or more tables based on common attributes, typically connecting a **Primary Key (PK)** in one table to a **Foreign Key (FK)** in another.

```text
+-----------------------+                    +------------------------+
|      DEPARTMENTS      | 1                N |       EMPLOYEES        |
|-----------------------|--------------------|------------------------|
| department_id (PK)    |<-------------------| department_id (FK)     |
| department_name       |                    | employee_id (PK)       |
+-----------------------+                    +------------------------+
```

---

## 2. Cardinality and Modality

When modeling relationships, two concepts govern the connection:
- **Cardinality (Maximum)**: How many instances of Entity B can associate with one instance of Entity A?
  - Options: One-to-One (1:1), One-to-Many (1:N), Many-to-Many (N:M).
- **Modality / Optionality (Minimum)**: Is participation mandatory (minimum 1) or optional (minimum 0)?
  - Mandatory: A row *must* be connected to another row.
  - Optional: A row *can* exist without being connected to another row.

---

## 3. The Three Primary Types of Relationships

### A. One-to-One (1:1) Relationship

#### Definition
Each record in Table A is linked to **at most one** record in Table B, and each record in Table B is linked to **at most one** record in Table A.

#### Real-World Examples
- A `Person` and their `Passport`.
- A `User` account and their sensitive `UserProfile` / `UserSecuritySettings`.
- A `Vehicle` and its `RegistrationCertificate`.

#### Implementation Pattern
Put the foreign key in either table (usually the child/dependent table) and place a **`UNIQUE`** constraint on that foreign key column.

```sql
CREATE TABLE users (
    user_id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    username VARCHAR(50) NOT NULL UNIQUE,
    email VARCHAR(100) NOT NULL UNIQUE
);

CREATE TABLE user_profiles (
    profile_id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    user_id INT NOT NULL UNIQUE, -- UNIQUE constraint enforces 1:1
    bio TEXT,
    avatar_url VARCHAR(255),
    date_of_birth DATE,
    CONSTRAINT fk_profile_user FOREIGN KEY (user_id) REFERENCES users(user_id) ON DELETE CASCADE
);
```

#### Why not keep both in one table?
- **Security**: Strict access control can protect the secondary table.
- **Performance**: Large text or BLOB columns are kept separate from frequently queried core tables.
- **Sparse Data**: Avoids hundreds of NULL columns if only a small percentage of users have extended profiles.

---

### B. One-to-Many (1:N) Relationship

#### Definition
A single record in Table A can be associated with **multiple** records in Table B, but each record in Table B is associated with **exactly one** record in Table A. This is the **most common** relationship in relational databases.

#### Real-World Examples
- One `Department` has many `Employees`.
- One `Customer` places many `Orders`.
- One `Author` writes many `Books`.
- One `Blog Post` receives many `Comments`.

#### Implementation Pattern
The Primary Key from the "One" side is placed as a Foreign Key inside the "Many" side table.

```sql
CREATE TABLE departments (
    department_id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    department_name VARCHAR(100) NOT NULL,
    office_location VARCHAR(100)
);

CREATE TABLE employees (
    employee_id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    salary NUMERIC(10, 2) NOT NULL,
    department_id INT, -- Foreign key lives on the MANY side
    CONSTRAINT fk_emp_dept FOREIGN KEY (department_id) 
        REFERENCES departments(department_id) 
        ON DELETE SET NULL
);
```

---

### C. Many-to-Many (N:M) Relationship

#### Definition
Multiple records in Table A can be associated with multiple records in Table B, and vice-versa.

#### Real-World Examples
- `Students` and `Courses` (A student takes multiple courses; a course has multiple students).
- `Orders` and `Products` (An order contains multiple products; a product is bought in multiple orders).
- `Actors` and `Movies` (An actor stars in multiple movies; a movie features multiple actors).

#### Implementation Pattern
Relational tables cannot directly represent N:M relationships without causing severe data duplication. Therefore, an **intermediate bridge table** (also called **junction table**, **association table**, or **cross-reference table**) is introduced.

```text
+--------------+ 1        N +------------------+ N        1 +--------------+
|   STUDENTS   |------------|   ENROLLMENTS    |------------|   COURSES    |
|--------------|            |------------------|            |--------------|
| student_id   |            | student_id (FK)  |            | course_id    |
| student_name |            | course_id (FK)   |            | course_title |
+--------------+            | enrollment_date  |            +--------------+
                            +------------------+
```

```sql
CREATE TABLE students (
    student_id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    full_name VARCHAR(100) NOT NULL
);

CREATE TABLE courses (
    course_id VARCHAR(10) PRIMARY KEY,
    course_title VARCHAR(150) NOT NULL
);

-- Junction Table decomposing N:M into two 1:N relationships
CREATE TABLE enrollments (
    student_id INT NOT NULL,
    course_id VARCHAR(10) NOT NULL,
    enrolled_at DATE NOT NULL DEFAULT CURRENT_DATE,
    final_score NUMERIC(5, 2),
    PRIMARY KEY (student_id, course_id), -- Composite Primary Key
    CONSTRAINT fk_enroll_student FOREIGN KEY (student_id) REFERENCES students(student_id) ON DELETE CASCADE,
    CONSTRAINT fk_enroll_course FOREIGN KEY (course_id) REFERENCES courses(course_id) ON DELETE CASCADE
);
```

---

## 4. Special Relationship Types

### Self-Referencing (Recursive / Unary) Relationship
An entity is related to itself. A foreign key in the table references the primary key of the same table.

#### Examples
- Employee reporting hierarchy: An employee has a manager who is also an employee.
- Category tree: A category has a parent category.

```sql
CREATE TABLE employees (
    employee_id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    full_name VARCHAR(100) NOT NULL,
    manager_id INT, -- References employee_id in this same table
    CONSTRAINT fk_employee_manager FOREIGN KEY (manager_id) 
        REFERENCES employees(employee_id) 
        ON DELETE SET NULL
);
```

---

## 5. Summary Matrix of Relationships

| Relationship | FK Location | Key Constraints | Bridge Table Needed? |
| :--- | :--- | :--- | :--- |
| **1:1** | Dependent table | FK column must be `UNIQUE` | No |
| **1:N** | The "Many" table | Standard FK (allows duplicates) | No |
| **N:M** | Bridge / Junction table | Pair of FKs, usually composite PK | **Yes** |
| **Recursive** | Same table | FK pointing to own table PK | No |

---

## 6. Hands-On Practice Questions

1. Design a schema for a Hospital system connecting `Patients`, `Doctors`, and `Appointments`. What is the cardinality between `Patients` and `Doctors`? What entity acts as the junction table?
2. If you remove the `UNIQUE` constraint on the foreign key in a 1:1 relationship, what type of relationship does it immediately become?
