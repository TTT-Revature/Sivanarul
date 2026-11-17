
# Python Nested Loops

## 1. Introduction to Nested Loops

A nested loop means placing one loop inside another loop.

In Python, we can place:

- A `for` loop inside another `for` loop.
- A `while` loop inside another `while` loop.
- A `for` loop inside a `while` loop.
- A `while` loop inside a `for` loop.

The inner loop executes as part of every iteration of the outer loop.

### Real-World Analogy

Imagine a company has:

- 3 departments.
- Each department has 2 employees.

If we want to process every employee in every department, we can use nested loops.

The outer loop handles departments, and the inner loop handles employees.

---

## 2. Basic Nested for Loop

### Syntax

```python
for outer_variable in outer_iterable:

    for inner_variable in inner_iterable:
        # Inner loop statements

    # Outer loop statements
```

### Example

```python
for row in range(1, 4):

    for column in range(1, 3):
        print("Row:", row, "Column:", column)
```

Output:

```text
Row: 1 Column: 1
Row: 1 Column: 2
Row: 2 Column: 1
Row: 2 Column: 2
Row: 3 Column: 1
Row: 3 Column: 2
```

### Explanation

The outer loop:

```python
for row in range(1, 4):
```

Generates:

```text
1, 2, 3
```

The inner loop:

```python
for column in range(1, 3):
```

Generates:

```text
1, 2
```

For every outer iteration, the inner loop completes all its iterations.

---

## 3. Understanding Nested Loop Execution

Let's understand the execution step by step.

```python
for i in range(1, 4):

    for j in range(1, 3):
        print(i, j)
```

### Execution Trace

| Outer iteration | Inner iteration | i | j | Output |
|---|---|---:|---:|---|
| 1 | 1 | 1 | 1 | 1 1 |
| 1 | 2 | 1 | 2 | 1 2 |
| 2 | 1 | 2 | 1 | 2 1 |
| 2 | 2 | 2 | 2 | 2 2 |
| 3 | 1 | 3 | 1 | 3 1 |
| 3 | 2 | 3 | 2 | 3 2 |

### Important Execution Rule

For every single iteration of the outer loop, the inner loop runs completely.

In this example:

- Outer loop executes 3 times.
- Inner loop executes 2 times per outer iteration.
- Total inner loop executions = 3 × 2 = 6.

This is the most important concept in nested loops.

---

## 4. Nested Loops with range()

The `range()` function is commonly used with nested loops when we need to control the number of iterations.

### Example 1: Print a 3 × 3 Grid

```python
for row in range(1, 4):

    for column in range(1, 4):
        print("*", end=" ")

    print()
```

Output:

```text
* * *
* * *
* * *
```

### Explanation

- The outer loop controls the rows.
- The inner loop controls the columns.
- `end=" "` prints stars on the same line.
- `print()` moves the cursor to the next line after each row.

### Example 2: Print Row and Column Numbers

```python
for row in range(1, 4):

    for column in range(1, 4):
        print(column, end=" ")

    print()
```

Output:

```text
1 2 3
1 2 3
1 2 3
```

### Example 3: Print Increasing Numbers

```python
for row in range(1, 4):

    for column in range(1, 4):
        print(row, end=" ")

    print()
```

Output:

```text
1 1 1
2 2 2
3 3 3
```

---

## 5. Pattern Printing Using Nested Loops

Pattern printing is one of the best ways to understand nested loops.

### Pattern 1: Right-Angled Triangle

```python
for row in range(1, 5):

    for column in range(row):
        print("*", end=" ")

    print()
```

Output:

```text
*
* *
* * *
* * * *
```

Explanation:

| Row | Number of stars |
|---|---:|
| 1 | 1 |
| 2 | 2 |
| 3 | 3 |
| 4 | 4 |

The inner loop executes according to the current row number.

### Pattern 2: Inverted Triangle

```python
for row in range(4, 0, -1):

    for column in range(row):
        print("*", end=" ")

    print()
```

Output:

```text
* * * *
* * *
* *
*
```

The outer loop decreases from 4 to 1.

### Pattern 3: Increasing Number Triangle

```python
for row in range(1, 5):

    for column in range(1, row + 1):
        print(column, end=" ")

    print()
```

Output:

```text
1
1 2
1 2 3
1 2 3 4
```

### Pattern 4: Repeated Row Number

```python
for row in range(1, 5):

    for column in range(row):
        print(row, end=" ")

    print()
```

Output:

```text
1
2 2
3 3 3
4 4 4 4
```

### Pattern 5: Pyramid Pattern

```python
rows = 4

for row in range(1, rows + 1):

    for space in range(rows - row):
        print(" ", end=" ")

    for star in range(2 * row - 1):
        print("*", end=" ")

    print()
```

Output:

```text
      *
    * * *
  * * * * *
* * * * * * *
```

Explanation:

The first inner loop prints spaces.

The second inner loop prints stars.

The number of stars increases by two for every row.

---

## 6. Nested Loops with Lists

Nested loops are useful when working with collections that contain other collections.

### Example: List of Lists

```python
students = [
    ["Arun", "Python"],
    ["Kumar", "Java"],
    ["Siva", "SQL"]
]

for student in students:

    for value in student:
        print(value)

    print()
```

Output:

```text
Arun
Python

Kumar
Java

Siva
SQL
```

Explanation:

The outer loop accesses each inner list.

The inner loop accesses the elements inside that list.

### Example: Process Multiple Subjects

```python
students = [
    {"name": "Arun", "subjects": ["Python", "SQL"]},
    {"name": "Kumar", "subjects": ["Java", "C++"]}
]

for student in students:

    print("Student:", student["name"])

    for subject in student["subjects"]:
        print("Subject:", subject)
```

Output:

```text
Student: Arun
Subject: Python
Subject: SQL
Student: Kumar
Subject: Java
Subject: C++
```

This structure is common when processing hierarchical data.

---

## 7. Nested Loops with Dictionaries

Dictionaries can also contain nested dictionaries or lists.

### Example: Employee Department Details

```python
company = {
    "Python": ["Arun", "Siva"],
    "Java": ["Kumar", "Ravi"],
    "Data Science": ["Priya", "Anu"]
}

for department, employees in company.items():

    print("Department:", department)

    for employee in employees:
        print("Employee:", employee)
```

Output:

```text
Department: Python
Employee: Arun
Employee: Siva
Department: Java
Employee: Kumar
Employee: Ravi
Department: Data Science
Employee: Priya
Employee: Anu
```

Explanation:

- Outer loop accesses department names and employee lists.
- Inner loop processes employees in each department.

---

## 8. Nested while Loops

A while loop can also contain another while loop.

### Example

```python
row = 1

while row <= 3:

    column = 1

    while column <= 3:
        print(row, column)
        column += 1

    row += 1
```

Output:

```text
1 1
1 2
1 3
2 1
2 2
2 3
3 1
3 2
3 3
```

### Explanation

1. Initialize `row` to 1.
2. Check whether `row` is less than or equal to 3.
3. Initialize `column` to 1.
4. Run the inner loop until `column` becomes 4.
5. Increase `row`.
6. Repeat until `row` becomes 4.

Important:

The inner variable `column` is initialized inside the outer loop because it must restart from 1 for every new row.

---

## 9. Mixing for and while Loops

Python allows different loop types to be nested.

### Example 1: for inside while

```python
row = 1

while row <= 3:

    for column in range(1, 4):
        print(row, column)

    row += 1
```

Output:

```text
1 1
1 2
1 3
2 1
2 2
2 3
3 1
3 2
3 3
```

### Example 2: while inside for

```python
for row in range(1, 4):

    column = 1

    while column <= 3:
        print(row, column)
        column += 1
```

Both examples produce the same output.

The choice depends on whether each level of repetition is better expressed using iteration over an iterable or a condition.

---

## 10. break and continue in Nested Loops

Understanding loop control statements in nested loops is important.

### Example 1: break in Inner Loop

```python
for row in range(1, 4):

    for column in range(1, 4):

        if column == 2:
            break

        print(row, column)
```

Output:

```text
1 1
2 1
3 1
```

Explanation:

The inner loop terminates when `column` becomes 2.

The outer loop continues with the next row.

### Example 2: continue in Inner Loop

```python
for row in range(1, 4):

    for column in range(1, 4):

        if column == 2:
            continue

        print(row, column)
```

Output:

```text
1 1
1 3
2 1
2 3
3 1
3 3
```

The inner loop skips the column value 2, but continues processing the remaining columns.

### Example 3: Stop Both Loops

A single `break` only exits the nearest enclosing loop.

If we want to stop both loops, one simple approach is to use a flag.

```python
stop = False

for row in range(1, 4):

    for column in range(1, 4):

        if row == 2 and column == 2:
            stop = True
            break

        print(row, column)

    if stop:
        break
```

Output:

```text
1 1
1 2
1 3
2 1
```

The flag communicates to the outer loop that it should also stop.

---

## 11. Understanding Nested Loop Complexity

Nested loops affect the execution time of a program.

Consider:

```python
for i in range(5):

    for j in range(5):
        print(i, j)
```

The outer loop executes 5 times.

The inner loop executes 5 times for every outer iteration.

Total executions:

5 × 5 = 25

### General Formula

If:

- Outer loop executes N times.
- Inner loop executes M times per outer iteration.

Then the inner loop body executes:

N × M times.

### Example: Different Loop Sizes

```python
for i in range(3):

    for j in range(4):
        print(i, j)
```

Total inner loop executions:

3 × 4 = 12

### Time Complexity

| Structure | Approximate Time Complexity |
|---|---|
| Single loop over N elements | O(N) |
| Two nested loops, each N iterations | O(N²) |
| Three nested loops, each N iterations | O(N³) |
| Outer N and inner M iterations | O(N × M) |

Important:

These are common worst-case complexity descriptions for the shown loop structures. Actual complexity depends on the number of iterations and the operations inside each loop.

Nested loops are not automatically inefficient. They are useful when the problem genuinely requires comparing or processing combinations of elements.

---

## 12. Practical FDE Applications

Forward Deployed Engineers frequently work with structured customer data, API responses, integrations, and datasets.

Nested loops help process hierarchical information.

### Example 1: Process Customer Orders

```python
customers = [
    {
        "name": "Arun",
        "orders": ["Laptop", "Mouse"]
    },
    {
        "name": "Kumar",
        "orders": ["Keyboard", "Monitor"]
    }
]

for customer in customers:

    print("Customer:", customer["name"])

    for order in customer["orders"]:
        print("Order:", order)
```

Output:

```text
Customer: Arun
Order: Laptop
Order: Mouse
Customer: Kumar
Order: Keyboard
Order: Monitor
```

### Example 2: Validate Multiple API Records

```python
api_response = [
    {
        "customer": "Arun",
        "records": [
            {"id": 1, "status": "valid"},
            {"id": 2, "status": "invalid"}
        ]
    },
    {
        "customer": "Kumar",
        "records": [
            {"id": 3, "status": "valid"},
            {"id": 4, "status": "valid"}
        ]
    }
]

for customer in api_response:

    print("Customer:", customer["customer"])

    for record in customer["records"]:

        if record["status"] == "valid":
            print("Valid record:", record["id"])

        else:
            print("Invalid record:", record["id"])
```

Output:

```text
Customer: Arun
Valid record: 1
Invalid record: 2
Customer: Kumar
Valid record: 3
Valid record: 4
```

### Example 3: Compare Two Lists

Imagine we want to identify common skills between two developers.

```python
developer_one = ["Python", "SQL", "FastAPI"]
developer_two = ["Java", "Python", "SQL"]

for skill_one in developer_one:

    for skill_two in developer_two:

        if skill_one == skill_two:
            print("Common skill:", skill_one)
```

Output:

```text
Common skill: Python
Common skill: SQL
```

This example uses nested loops to compare every element in one list with every element in another.

For larger datasets, using a set intersection can be more efficient.

---

## 13. Common Mistakes

### Mistake 1: Incorrect Indentation

Incorrect:

```python
for row in range(3):
for column in range(3):
    print(row, column)
```

Correct:

```python
for row in range(3):
    for column in range(3):
        print(row, column)
```

### Mistake 2: Not Resetting the Inner while Variable

Incorrect:

```python
row = 1
column = 1

while row <= 3:

    while column <= 3:
        print(row, column)
        column += 1

    row += 1
```

Problem:

After the first outer iteration, `column` becomes 4.

The inner loop will not execute again.

Correct:

```python
row = 1

while row <= 3:

    column = 1

    while column <= 3:
        print(row, column)
        column += 1

    row += 1
```

### Mistake 3: Confusing Outer and Inner Variables

```python
for i in range(3):

    for j in range(2):
        print(i, j)
```

Remember:

- `i` belongs to the outer loop.
- `j` belongs to the inner loop.

### Mistake 4: Unexpected Execution Count

```python
for i in range(10):

    for j in range(10):
        print(i, j)
```

The print statement executes 100 times, not 10 times.

### Mistake 5: Using Nested Loops Unnecessarily

Sometimes a nested loop can be replaced with a more efficient approach.

For example, finding common elements between two lists can be done using sets:

```python
developer_one = ["Python", "SQL", "FastAPI"]
developer_two = ["Java", "Python", "SQL"]

common_skills = set(developer_one) & set(developer_two)

print(common_skills)
```

Output:

```text
{'Python', 'SQL'}
```

The order of elements in a set is not guaranteed.

---

## 14. Practice Exercises

Try solving these exercises without looking at the examples.

### Beginner Level

1. Print a 3 × 3 grid using nested loops.
2. Print a right-angled triangle using stars.
3. Print an inverted triangle using stars.
4. Print the following pattern:

```text
1
1 2
1 2 3
1 2 3 4
```

5. Print the following pattern:

```text
1 1 1
2 2 2
3 3 3
```

### Intermediate Level

6. Print multiplication tables from 1 to 5 using nested loops.
7. Print a square pattern of size 5 × 5.
8. Find common elements between two lists using nested loops.
9. Count the total number of elements in a list of lists.
10. Find the largest number in each nested list.

### Practical FDE Exercises

11. Process multiple customers, each having multiple orders.
12. Iterate through multiple departments and their employees.
13. Validate nested customer records containing multiple transactions.
14. Compare product IDs between two API response lists.
15. Identify duplicate values between two datasets.

---

## 15. Quick Revision

| Concept | Description |
|---|---|
| Nested loop | A loop inside another loop |
| Outer loop | Controls the main iteration |
| Inner loop | Executes completely for each outer iteration |
| Nested for | A for loop inside another for loop |
| Nested while | A while loop inside another while loop |
| Mixed loops | Combining for and while loops |
| break | Terminates the nearest enclosing loop |
| continue | Skips the current iteration of the nearest enclosing loop |
| Loop complexity | Depends on the number of iterations at each level |

### Important Formulas

Two loops:

N × M

Three loops:

N × M × P

For two loops that each execute N times:

O(N²)

---

## 16. Self-Assessment Questions

1. What is a nested loop?
2. What is the difference between an outer loop and an inner loop?
3. How many times does the inner loop execute when the outer loop runs 4 times and the inner loop runs 3 times?
4. Can we place a while loop inside a for loop?
5. Can we place a for loop inside a while loop?
6. Why should we initialize an inner while-loop variable inside the outer loop?
7. What happens when `break` executes inside a nested loop?
8. Does `continue` terminate the outer loop?
9. What is the time complexity of two nested loops, each executing N times?
10. How can nested loops help process customer records?
11. Why can nested loops become expensive with large datasets?
12. When can a set or dictionary replace a nested-loop solution?

---

## 17. Learning Outcome

After completing this chapter, you should be able to:

- Understand nested loop execution.
- Write nested for and while loops.
- Combine different types of loops.
- Generate number and star patterns.
- Process lists of lists and nested dictionaries.
- Understand break and continue inside nested loops.
- Calculate basic nested-loop execution counts.
- Recognize when nested loops may affect performance.
- Apply nested loops to customer data and API processing.

### Next Topic

**Loop Patterns and Practical Problems in Python**

We will strengthen loop logic through number patterns, star patterns, searching, counting, and real-world data-processing exercises.
