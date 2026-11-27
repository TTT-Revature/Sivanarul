
# Introduction to SQL and Relational Databases

## 1. Introduction to Databases

A database is an organized collection of information that can be stored, accessed, managed, and updated.

### Real-world example

Imagine a college managing information about students.

The college needs to maintain:

- Student details
- Course information
- Faculty details
- Student marks
- Attendance records

Storing all this information in separate text files can become difficult to manage.

A database provides a structured way to store and retrieve this information.

### Example

```text
College Database
       |
       |--- Students
       |
       |--- Courses
       |
       |--- Faculty
       |
       |--- Marks
       |
       |--- Attendance
```

A database helps applications manage large amounts of information efficiently.

---

## 2. What Is a DBMS?

DBMS stands for **Database Management System**.

It is software that allows users and applications to create, store, retrieve, update, and manage data in databases.

Examples:

- MySQL
- PostgreSQL
- Oracle Database
- Microsoft SQL Server
- SQLite

### How does a DBMS work?

```text
User / Application
        |
        v
       DBMS
        |
        v
     Database
        |
        v
   Stored Data
```

For example:

A Python application sends a query to the DBMS.

The DBMS processes the query and returns the requested data.

### Responsibilities of a DBMS

1. Data storage and retrieval.
2. Data insertion, updating, and deletion.
3. Access control and security.
4. Transaction management.
5. Data consistency.
6. Backup and recovery.
7. Managing concurrent users.

---

## 3. What Is a Relational Database?

A Relational Database stores data in the form of tables.

Each table contains rows and columns.

Example: Student Table

| student_id | name | age | city |
|---|---|---|---|
| 101 | Arun | 22 | Chennai |
| 102 | Kumar | 23 | Madurai |
| 103 | Priya | 21 | Coimbatore |

Here:

- Table: Students
- Rows: Individual student records.
- Columns: Attributes such as student_id, name, age, city.

A relational database can contain multiple tables connected through relationships.

### Visual representation

```text
             College Database
                    |
          ----------------------
          |                    |
          v                    v
     Students Table       Courses Table
          |                    |
          |                    |
          v                    v
    Student Records      Course Records
```

The relationship between tables allows us to organize related information without unnecessarily duplicating it.

---

## 4. Tables, Rows, and Columns

These are the fundamental components of a relational database.

### A. Table

A table stores related information.

Example:

```text
Students
```

### B. Row

A row represents one complete record.

Example:

```text
101 | Arun | 22 | Chennai
```

This represents one student.

### C. Column

A column represents an attribute or property.

Example:

```text
student_id
name
age
city
```

### Visual representation

| student_id | name | age | city |
|---|---|---|---|
| 101 | Arun | 22 | Chennai |
| 102 | Kumar | 23 | Madurai |
| 103 | Priya | 21 | Coimbatore |

- One row = One record.
- One column = One attribute.
- One table = Collection of related records.

---

## 5. What Is SQL?

SQL stands for **Structured Query Language**.

It is a language used to communicate with relational database management systems.

Using SQL, we can:

- Create databases and tables.
- Insert records.
- Retrieve records.
- Update existing records.
- Delete records.
- Control permissions.
- Manage transactions.

### Example

Suppose we have a Students table.

We want to retrieve all student records.

```sql
SELECT * FROM Students;
```

Explanation:

- SELECT retrieves data.
- * represents all columns.
- FROM specifies the table.

The database returns the records stored in the Students table.

### Important distinction

SQL is a language.

MySQL and PostgreSQL are database management systems that support SQL.

---

## 6. SQL vs MySQL vs PostgreSQL vs SQLite

These terms are related but are not the same.

| Name | Description |
|---|---|
| SQL | Language used to communicate with relational databases |
| MySQL | Relational database management system |
| PostgreSQL | Relational database management system |
| SQLite | Lightweight embedded relational database |
| Oracle Database | Enterprise relational database management system |
| SQL Server | Microsoft's relational database management system |

### Example

Think of SQL as a language used to communicate.

MySQL and PostgreSQL are systems that understand SQL and manage the stored data.

Different database systems may support different SQL features and syntax variations.

---

## 7. How SQL Works

Consider a Python application that needs student information.

```text
Python Application
        |
        | SQL Query
        v
   Database Driver
        |
        v
       DBMS
        |
        v
   Database Tables
        |
        v
    Query Result
        |
        v
Python Application
```

Example SQL query:

```sql
SELECT name, age
FROM Students
WHERE age > 21;
```

The database processes the query and returns students whose age is greater than 21.

The Python application can then use the returned data.

---

## 8. Types of SQL Commands

SQL commands are commonly grouped into five categories.

### A. DDL – Data Definition Language

DDL commands define or modify database structures.

Common commands:

- CREATE
- ALTER
- DROP
- TRUNCATE

Example:

```sql
CREATE TABLE Students (
    student_id INT,
    name VARCHAR(100),
    age INT
);
```

This creates a table named Students.

### B. DML – Data Manipulation Language

DML commands modify data stored inside tables.

Common commands:

- INSERT
- UPDATE
- DELETE

Example:

```sql
INSERT INTO Students
VALUES (101, 'Arun', 22);
```

This inserts a new student record.

### C. DQL – Data Query Language

DQL is commonly used to retrieve data.

Command:

- SELECT

Example:

```sql
SELECT * FROM Students;
```

This retrieves all columns and records.

Note: Some classifications group SELECT under DML rather than treating DQL as a separate category.

### D. DCL – Data Control Language

DCL commands manage database permissions.

Common commands:

- GRANT
- REVOKE

Example:

```sql
GRANT SELECT ON Students TO analyst_user;
```

This illustrates granting read permission. Exact syntax and user management vary by database system.

### E. TCL – Transaction Control Language

TCL commands manage transactions.

Common commands:

- COMMIT
- ROLLBACK
- SAVEPOINT

Example:

```sql
BEGIN;

UPDATE Students
SET age = 23
WHERE student_id = 101;

ROLLBACK;
```

ROLLBACK cancels the changes made in the current transaction, subject to the database's transaction rules.

### Quick comparison

| Category | Purpose | Commands |
|---|---|---|
| DDL | Define database structure | CREATE, ALTER, DROP |
| DML | Modify table data | INSERT, UPDATE, DELETE |
| DQL | Retrieve data | SELECT |
| DCL | Manage permissions | GRANT, REVOKE |
| TCL | Manage transactions | COMMIT, ROLLBACK |

---

## 9. What Is a Primary Key?

A Primary Key uniquely identifies each record in a table.

Example:

| student_id | name | city |
|---|---|---|
| 101 | Arun | Chennai |
| 102 | Kumar | Madurai |
| 103 | Priya | Coimbatore |

Here, student_id is the primary key.

Why?

- Every student has a unique student_id.
- Two records cannot have the same primary key.
- A primary key cannot contain NULL values.

### SQL implementation

```sql
CREATE TABLE Students (
    student_id INT PRIMARY KEY,
    name VARCHAR(100),
    city VARCHAR(100)
);
```

Now student_id uniquely identifies every student record.

---

## 10. What Is a Foreign Key?

A Foreign Key connects one table to another.

It references a candidate key, commonly the primary key, in another table.

Example:

### Students Table

| student_id | name |
|---|---|
| 101 | Arun |
| 102 | Kumar |
| 103 | Priya |

### Courses Table

| course_id | course_name | student_id |
|---|---|---|
| 1 | Python | 101 |
| 2 | SQL | 102 |
| 3 | Java | 101 |

Here:

- Students.student_id is the Primary Key.
- Courses.student_id is a Foreign Key referencing Students.student_id.

### Visual representation

```text
       Students Table
    --------------------
    student_id (PK)
    name
          |
          |
          v
       Courses Table
    --------------------
    course_id (PK)
    course_name
    student_id (FK)
```

### SQL implementation

```sql
CREATE TABLE Students (
    student_id INT PRIMARY KEY,
    name VARCHAR(100)
);

CREATE TABLE Courses (
    course_id INT PRIMARY KEY,
    course_name VARCHAR(100),
    student_id INT,
    FOREIGN KEY (student_id)
        REFERENCES Students(student_id)
);
```

A foreign key helps maintain referential integrity.

It prevents a course record from referencing a student that does not exist, subject to the defined foreign-key constraints.

---

## 11. Types of Relationships in Relational Databases

Tables can be connected through different relationships.

### A. One-to-One Relationship

One record in Table A is associated with at most one record in Table B, and vice versa.

Example:

```text
Person  --------  Passport
   1                 1
```

One person has one passport record in this example.

### B. One-to-Many Relationship

One record in Table A can be associated with multiple records in Table B.

Example:

```text
Department
     |
     |------ Employee 1
     |
     |------ Employee 2
     |
     |------ Employee 3
```

One department can have multiple employees.

### C. Many-to-Many Relationship

Multiple records in Table A can be associated with multiple records in Table B.

Example:

```text
Students          Courses

Student A ------ Python
     |             |
     |             |
     |---------- SQL
     |
Student B ------ Java
     |
     |---------- Python
```

A student can enroll in multiple courses, and a course can have multiple students.

A many-to-many relationship is usually implemented using a junction table (also called a bridge or associative table).

Example:

```text
Students
   |
   | 1
   |
   | Many
Enrollments
   | Many
   |
   | 1
   |
Courses
```

The Enrollments table stores student_id and course_id.

---

## 12. What Are Constraints?

Constraints are rules applied to table columns to maintain data accuracy and integrity.

Common SQL constraints:

| Constraint | Purpose |
|---|---|
| PRIMARY KEY | Uniquely identifies a record |
| FOREIGN KEY | Maintains relationships between tables |
| NOT NULL | Prevents NULL values |
| UNIQUE | Prevents duplicate values |
| CHECK | Enforces a condition |
| DEFAULT | Provides a default value |

### Example

```sql
CREATE TABLE Employees (

    employee_id INT PRIMARY KEY,

    email VARCHAR(100) UNIQUE,

    name VARCHAR(100) NOT NULL,

    age INT CHECK (age >= 18),

    city VARCHAR(100) DEFAULT 'Chennai'

);
```

Explanation:

- employee_id must be unique and non-NULL.
- email must be unique.
- name cannot be NULL.
- age must be at least 18.
- city defaults to Chennai when no value is supplied.

Constraint support and exact behavior can vary across database systems.

---

## 13. What Is NULL?

NULL represents missing or unknown information.

It is not the same as:

- Zero (0).
- Empty string ('').
- False.

Example:

| employee_id | name | phone |
|---|---|---|
| 101 | Arun | 9876543210 |
| 102 | Kumar | NULL |
| 103 | Priya | 9876500000 |

Kumar's phone number is unknown or not provided.

### Checking NULL values

Incorrect:

```sql
SELECT *
FROM Employees
WHERE phone = NULL;
```

Correct:

```sql
SELECT *
FROM Employees
WHERE phone IS NULL;
```

To find records that have a phone number:

```sql
SELECT *
FROM Employees
WHERE phone IS NOT NULL;
```

Important: NULL is not compared using ordinary equality operators. SQL uses IS NULL and IS NOT NULL.

---

## 14. What Is a Schema?

A Schema describes the logical organization of database objects.

It can include:

- Tables
- Views
- Indexes
- Constraints
- Relationships
- Other database objects

Example:

```text
College Database
       |
       v
College Schema
       |
       |--- Students Table
       |
       |--- Courses Table
       |
       |--- Faculty Table
       |
       |--- Enrollments Table
```

The exact meaning of schema and how it is managed depends on the DBMS.

In PostgreSQL, for example, a database can contain multiple schemas.

---

## 15. Relational Database vs Non-Relational Database

Databases are commonly divided into relational and non-relational systems.

| Feature | Relational Database | Non-Relational Database |
|---|---|---|
| Data model | Tables | Document, key-value, graph, etc. |
| Structure | Usually predefined schema | Often more flexible |
| Relationships | Keys and joins | Depends on the data model |
| Querying | SQL or SQL-like languages | Database-specific APIs or query languages |
| Examples | MySQL, PostgreSQL | MongoDB, Redis, Neo4j |

### Example: Relational Data

```text
Students Table

student_id | name
101        | Arun
102        | Kumar
```

### Example: Document Data

```json
{
    "student_id": 101,
    "name": "Arun",
    "courses": ["Python", "SQL"]
}
```

Relational and non-relational databases serve different requirements. Neither is automatically better in every situation.

---

## 16. Advantages of Relational Databases

1. Structured data storage.
2. Relationships between tables.
3. Data integrity through constraints.
4. Powerful querying using SQL.
5. Transaction support.
6. Reduced duplication through good database design.
7. Mature security and access-control mechanisms.

### Limitations

1. Schema changes may require careful planning.
2. Complex joins can become expensive.
3. Horizontal scaling can require additional architectural work.
4. Poorly designed tables and queries can affect performance.

Modern relational databases also support JSON, replication, partitioning, and distributed deployment features.

---

## 17. SQL in a Python Application

Python applications commonly communicate with relational databases through database drivers.

Example using SQLite:

```python
import sqlite3

connection = sqlite3.connect("college.db")

cursor = connection.cursor()

cursor.execute("""
CREATE TABLE IF NOT EXISTS Students (
    student_id INTEGER PRIMARY KEY,
    name TEXT,
    age INTEGER
)
""")

cursor.execute(
    "INSERT INTO Students (student_id, name, age) VALUES (?, ?, ?)",
    (101, "Arun", 22)
)

connection.commit()

cursor.execute("SELECT * FROM Students")

records = cursor.fetchall()

for record in records:
    print(record)

connection.close()
```

Output:

```text
(101, 'Arun', 22)
```

### Explanation

1. `sqlite3.connect()` connects to a SQLite database file.
2. `cursor()` creates an object used to execute SQL statements.
3. `execute()` runs SQL commands.
4. `commit()` saves the transaction.
5. `fetchall()` retrieves the query results.
6. `close()` closes the connection.

### Important: SQL Injection Prevention

Avoid building SQL queries by directly combining user input with SQL strings.

Unsafe:

```python
query = "SELECT * FROM Students WHERE name = '" + user_input + "'"
```

Safer:

```python
cursor.execute(
    "SELECT * FROM Students WHERE name = ?",
    (user_input,)
)
```

Parameterized queries help prevent SQL injection.

---

## 18. SQL in an FDE Scenario

Imagine an enterprise HR application that manages employee information.

The application needs to:

- Store employee records.
- Retrieve employee details.
- Track department information.
- Manage leave requests.
- Generate reports.
- Connect with external HR systems.

A possible database design:

```text
          HR Database
               |
       -------------------
       |        |        |
       v        v        v
   Employees Departments Leave_Requests
       |        |
       |        |
       ---------
      Relationships
```

A Python FastAPI application may receive an employee request, query PostgreSQL, and return the result through an API.

Example workflow:

```text
Employee
   |
   v
React Frontend
   |
   v
FastAPI Backend
   |
   v
SQL Query
   |
   v
PostgreSQL
   |
   v
Employee Data
   |
   v
API Response
```

FDE applications commonly integrate databases with:

- Python APIs.
- AI-powered applications.
- RAG pipelines and metadata storage.
- Enterprise reporting.
- External business systems.
- Workflow automation.

SQL is an important skill for understanding and integrating enterprise data.

---

## 19. Common Mistakes

1. Confusing SQL with MySQL.
   - SQL is a language; MySQL is a database management system.

2. Confusing a database with a table.
   - A database can contain multiple tables.

3. Assuming a primary key can contain NULL.
   - A primary key cannot contain NULL values.

4. Confusing primary keys and foreign keys.
   - A primary key identifies a record; a foreign key references a key in another table.

5. Using `= NULL`.
   - Use `IS NULL` instead.

6. Assuming every database supports identical SQL syntax.
   - SQL dialects have differences.

7. Storing all information in one large table.
   - This can create duplication and data consistency problems.

8. Concatenating user input directly into SQL.
   - Use parameterized queries to prevent SQL injection.

---

## 20. Practice Exercises

### Beginner

1. What is a database?
2. What is the purpose of a DBMS?
3. What does SQL stand for?
4. What is a relational database?
5. What is the difference between a row and a column?
6. What is the difference between SQL and MySQL?

### Intermediate

7. What is a Primary Key?
8. What is a Foreign Key?
9. Explain one-to-one, one-to-many, and many-to-many relationships.
10. What are SQL constraints?
11. What is the difference between NULL and zero?
12. What are DDL, DML, DQL, DCL, and TCL?

### Advanced

13. Why do relational databases use foreign keys?
14. How does a many-to-many relationship work internally?
15. Why is database normalization important?
16. How does Python communicate with PostgreSQL?
17. What is SQL injection, and how can parameterized queries prevent it?
18. When might a non-relational database be a better choice?

---

## 21. Quick Revision

| Concept | Meaning |
|---|---|
| Database | Organized collection of data |
| DBMS | Software that manages databases |
| RDBMS | Relational Database Management System |
| SQL | Structured Query Language |
| Table | Collection of related records |
| Row | Individual record |
| Column | Attribute |
| Primary Key | Unique identifier for a record |
| Foreign Key | References a key in another table |
| Constraint | Rule applied to data |
| NULL | Missing or unknown value |
| Schema | Logical organization of database objects |
| DDL | Defines database structures |
| DML | Modifies data |
| DQL | Retrieves data |
| DCL | Manages permissions |
| TCL | Manages transactions |

---

## 22. Learning Outcome

After completing this topic, you should be able to:

- Explain databases and DBMS.
- Understand relational database architecture.
- Identify tables, rows, and columns.
- Explain SQL and its purpose.
- Differentiate SQL, MySQL, PostgreSQL, and SQLite.
- Understand primary keys and foreign keys.
- Identify relationships between tables.
- Explain database constraints and NULL.
- Understand SQL command categories.
- Connect Python applications with relational databases.
- Understand the role of SQL in enterprise and FDE applications.

### Recommended Next Topic

**SQL Fundamentals – Database Creation, Table Creation, INSERT, SELECT, UPDATE, and DELETE**

This will introduce practical SQL commands and help you start writing queries against a real database.
