
# Python for Loops and range()

## 1. Introduction to Loops

A loop is a programming structure that allows us to execute the same block of code multiple times.

Imagine you need to print the names of 100 employees.

Without a loop, you might write:

```python
print("Employee 1")
print("Employee 2")
print("Employee 3")
print("Employee 4")
print("Employee 5")
```

Writing separate statements for every employee is inefficient.

Instead, we can use a loop.

```python
for employee in range(1, 6):
    print(f"Employee {employee}")
```

Output:

```text
Employee 1
Employee 2
Employee 3
Employee 4
Employee 5
```

### Why do we need loops?

Loops help us:

- Avoid writing repetitive code.
- Process multiple records.
- Iterate through collections.
- Automate repetitive operations.
- Perform calculations repeatedly.
- Process API responses and datasets.

---

## 2. What Is a for Loop?

A `for` loop is used to iterate over an iterable object.

An iterable is an object that can provide its elements one at a time.

Examples:

- Strings
- Lists
- Tuples
- Sets
- Dictionaries
- Range objects

### Syntax

```python
for variable in iterable:
    # Code to execute
```

Explanation:

| Component | Description |
|---|---|
| `for` | Starts the loop |
| `variable` | Receives the current element |
| `in` | Connects the variable with the iterable |
| `iterable` | Object being iterated |
| `:` | Marks the beginning of the loop block |
| Indented code | Executes during each iteration |

### Example 1: Basic for Loop

```python
for number in [10, 20, 30, 40]:
    print(number)
```

Output:

```text
10
20
30
40
```

What happens internally?

1. Python gets the first element: `10`.
2. Assigns it to `number`.
3. Executes `print(number)`.
4. Moves to the next element.
5. Repeats until all elements are processed.

### Example 2: Iterating Through a String

```python
name = "Python"

for character in name:
    print(character)
```

Output:

```text
P
y
t
h
o
n
```

A string is iterable because Python can provide its characters one at a time.

### Example 3: Iterating Through a List

```python
employees = ["Arun", "Kumar", "Siva", "Ravi"]

for employee in employees:
    print(employee)
```

Output:

```text
Arun
Kumar
Siva
Ravi
```

### Example 4: Iterating Through a Tuple

```python
skills = ("Python", "FastAPI", "SQL")

for skill in skills:
    print(skill)
```

Output:

```text
Python
FastAPI
SQL
```

### Example 5: Iterating Through a Set

```python
skills = {"Python", "Java", "SQL"}

for skill in skills:
    print(skill)
```

Output:

```text
Python
Java
SQL
```

Note: A set does not guarantee a particular iteration order.

---

## 3. Understanding range()

The `range()` function generates a sequence of integers.

It is commonly used when we want to repeat a loop a specific number of times.

### Syntax

```python
range(start, stop, step)
```

| Parameter | Description |
|---|---|
| `start` | Starting value (inclusive) |
| `stop` | Ending boundary (exclusive) |
| `step` | Difference between consecutive values |

Important:

- `start` is optional and defaults to `0`.
- `step` is optional and defaults to `1`.
- `stop` is required.
- The stop value is never included in the generated sequence.

### Example 1: range(stop)

```python
for number in range(5):
    print(number)
```

Output:

```text
0
1
2
3
4
```

Explanation:

`range(5)` generates values starting from `0` and stopping before `5`.

### Example 2: range(start, stop)

```python
for number in range(1, 6):
    print(number)
```

Output:

```text
1
2
3
4
5
```

Explanation:

- Starting value: `1`
- Stopping boundary: `6`
- Generated values: `1, 2, 3, 4, 5`

### Example 3: range(start, stop, step)

```python
for number in range(2, 11, 2):
    print(number)
```

Output:

```text
2
4
6
8
10
```

Explanation:

The step value is `2`, so Python increases the number by two during each iteration.

### Example 4: Negative Step

```python
for number in range(10, 0, -1):
    print(number)
```

Output:

```text
10
9
8
7
6
5
4
3
2
1
```

Explanation:

The negative step makes the sequence move backwards.

### Example 5: Converting range into a List

```python
numbers = range(1, 6)

print(list(numbers))
```

Output:

```text
[1, 2, 3, 4, 5]
```

Important:

`range()` returns a range object, not a list.

We use `list()` when we specifically need to materialize its values as a list.

---

## 4. Understanding Loop Execution Step by Step

Consider this program:

```python
for number in range(1, 4):
    print(number)
```

Execution trace:

| Iteration | Value of number | Output |
|---|---:|---:|
| 1 | 1 | 1 |
| 2 | 2 | 2 |
| 3 | 3 | 3 |

After the third iteration, there are no more values in the range, so the loop terminates.

### Important Concept

The loop variable receives a new value during each iteration.

```python
for number in range(3):
    print("Inside loop:", number)

print("Loop completed")
```

Output:

```text
Inside loop: 0
Inside loop: 1
Inside loop: 2
Loop completed
```

---

## 5. Using range() for Calculations

### Example 1: Sum of Numbers

Calculate the sum of numbers from 1 to 5.

```python
total = 0

for number in range(1, 6):
    total = total + number

print("Total:", total)
```

Output:

```text
Total: 15
```

Execution:

| Iteration | number | total |
|---|---:|---:|
| 1 | 1 | 1 |
| 2 | 2 | 3 |
| 3 | 3 | 6 |
| 4 | 4 | 10 |
| 5 | 5 | 15 |

### Example 2: Multiplication Table

```python
number = 5

for value in range(1, 11):
    print(number, "x", value, "=", number * value)
```

Output:

```text
5 x 1 = 5
5 x 2 = 10
5 x 3 = 15
5 x 4 = 20
5 x 5 = 25
5 x 6 = 30
5 x 7 = 35
5 x 8 = 40
5 x 9 = 45
5 x 10 = 50
```

### Example 3: Print Even Numbers

```python
for number in range(2, 21, 2):
    print(number)
```

Output:

```text
2
4
6
8
10
12
14
16
18
20
```

### Example 4: Find the Factorial

Factorial of 5:

`5! = 5 × 4 × 3 × 2 × 1 = 120`

```python
number = 5
factorial = 1

for value in range(1, number + 1):
    factorial = factorial * value

print("Factorial:", factorial)
```

Output:

```text
Factorial: 120
```

---

## 6. Iterating Through Dictionaries

A dictionary stores data in key-value pairs.

```python
employee = {
    "name": "Arun",
    "role": "Python Developer",
    "salary": 50000
}
```

### Example 1: Iterate Through Keys

```python
for key in employee:
    print(key)
```

Output:

```text
name
role
salary
```

By default, iterating through a dictionary gives its keys.

### Example 2: Iterate Through Values

```python
for value in employee.values():
    print(value)
```

Output:

```text
Arun
Python Developer
50000
```

### Example 3: Iterate Through Keys and Values

```python
for key, value in employee.items():
    print(key, ":", value)
```

Output:

```text
name : Arun
role : Python Developer
salary : 50000
```

`items()` provides key-value pairs that can be unpacked into two loop variables.

---

## 7. Using enumerate() with for Loops

Sometimes we need both the index and the value while iterating through a collection.

We can use `enumerate()`.

### Example

```python
employees = ["Arun", "Kumar", "Siva"]

for index, employee in enumerate(employees):
    print(index, employee)
```

Output:

```text
0 Arun
1 Kumar
2 Siva
```

### Starting the Index from 1

```python
employees = ["Arun", "Kumar", "Siva"]

for index, employee in enumerate(employees, start=1):
    print(index, employee)
```

Output:

```text
1 Arun
2 Kumar
3 Siva
```

Real-world application:

When processing API records, we may need to identify the position of a particular record.

---

## 8. Nested for Loops

A nested loop means placing one loop inside another loop.

The inner loop executes completely for every iteration of the outer loop.

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

Execution:

1. Outer loop starts with `row = 1`.
2. Inner loop runs with `column = 1` and `column = 2`.
3. Outer loop moves to `row = 2`.
4. Inner loop runs again completely.
5. The process repeats until the outer loop finishes.

### Example: Pattern Printing

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

The outer loop controls the rows, and the inner loop controls the number of stars in each row.

---

## 9. The else Clause with for Loops

Python supports an `else` block with loops.

The `else` block executes when the loop finishes normally, without being terminated by `break`.

### Example

```python
for number in range(1, 4):
    print(number)
else:
    print("Loop completed")
```

Output:

```text
1
2
3
Loop completed
```

### Example: Loop with break

```python
for number in range(1, 6):
    if number == 3:
        break

    print(number)
else:
    print("Loop completed")
```

Output:

```text
1
2
```

The `else` block does not execute because `break` terminates the loop.

This feature is useful when searching for an item in a collection.

---

## 10. Common Mistakes with for Loops and range()

### Mistake 1: Forgetting That the Stop Value Is Exclusive

Incorrect assumption:

```python
for number in range(1, 5):
    print(number)
```

Expected by a beginner:

```text
1
2
3
4
5
```

Actual output:

```text
1
2
3
4
```

Correction:

```python
for number in range(1, 6):
    print(number)
```

### Mistake 2: Using an Incorrect Step

```python
for number in range(1, 10, 0):
    print(number)
```

Error:

```text
ValueError: range() arg 3 must not be zero
```

The step cannot be zero.

### Mistake 3: Incorrect Indentation

Incorrect:

```python
for number in range(3):
print(number)
```

Correct:

```python
for number in range(3):
    print(number)
```

### Mistake 4: Expecting a List from range()

```python
numbers = range(5)

print(type(numbers))
```

Output:

```text
<class 'range'>
```

Use `list(range(5))` if you need a list.

### Mistake 5: Modifying a Collection While Iterating

Avoid removing elements directly from a list while iterating over it. This can cause elements to be skipped.

Instead, create a new filtered list:

```python
numbers = [10, 15, 20, 25, 30]

even_numbers = []

for number in numbers:
    if number % 2 == 0:
        even_numbers.append(number)

print(even_numbers)
```

Output:

```text
[10, 20, 30]
```

---

## 11. Practical Applications for Forward Deployed Engineers

A Forward Deployed Engineer often works with customer data, APIs, integrations, and automation.

Loops are essential when processing multiple records.

### Example 1: Processing API Records

Imagine an API returns multiple customer records.

```python
customers = [
    {"name": "Arun", "status": "active"},
    {"name": "Kumar", "status": "inactive"},
    {"name": "Siva", "status": "active"}
]

for customer in customers:
    print(customer["name"], customer["status"])
```

Output:

```text
Arun active
Kumar inactive
Siva active
```

### Example 2: Filtering Active Customers

```python
customers = [
    {"name": "Arun", "status": "active"},
    {"name": "Kumar", "status": "inactive"},
    {"name": "Siva", "status": "active"}
]

for customer in customers:
    if customer["status"] == "active":
        print(customer["name"])
```

Output:

```text
Arun
Siva
```

### Example 3: Validating Customer Records

```python
customers = [
    {"name": "Arun", "email": "arun@example.com"},
    {"name": "", "email": "kumar@example.com"},
    {"name": "Siva", "email": ""}
]

for customer in customers:

    if not customer["name"]:
        print("Customer name is missing")

    elif not customer["email"]:
        print("Customer email is missing")

    else:
        print("Customer record is valid")
```

Output:

```text
Customer record is valid
Customer name is missing
Customer email is missing
```

### Example 4: Processing AI Model Responses

```python
responses = [
    "Python is a programming language.",
    "FastAPI is a Python framework.",
    "RAG combines retrieval with generation."
]

for response in responses:
    print("AI Response:", response)
```

A similar approach can be used to process multiple responses, documents, or results returned by an AI system.

---

## 12. When Should We Use a for Loop?

Use a `for` loop when:

- You want to iterate over a list of employees.
- You want to process API response records.
- You want to read elements from a dataset.
- You want to process characters in a string.
- You want to repeat an operation a known number of times using `range()`.

A `for` loop is generally preferred when iterating over an existing iterable.

---

## 13. Practice Exercises

Try solving these exercises without looking at the answers.

### Beginner Level

1. Print numbers from 1 to 10 using a for loop.
2. Print numbers from 10 to 1 in reverse order.
3. Print all even numbers between 1 and 50.
4. Print all odd numbers between 1 and 50.
5. Print each character of the string `"FORWARD ENGINEER"`.

### Intermediate Level

6. Calculate the sum of numbers from 1 to 100.
7. Print the multiplication table of a number entered by the user.
8. Find the factorial of a number.
9. Count how many vowels exist in a given string.
10. Find the largest number in a list without using `max()`.

### Practical FDE Exercises

11. Iterate through a list of customer dictionaries and print their names.
12. Identify customers whose status is `"active"`.
13. Find records with missing email addresses.
14. Iterate through a list of API response status codes and count successful responses (200–299).
15. Process a list of AI-generated responses and print each response with its index using `enumerate()`.

---

## 14. Quick Revision

| Concept | Meaning |
|---|---|
| `for` | Iterates over an iterable |
| `range(5)` | Generates 0 to 4 |
| `range(1, 5)` | Generates 1 to 4 |
| `range(1, 10, 2)` | Generates odd numbers from 1 to 9 |
| `range(10, 0, -1)` | Generates 10 down to 1 |
| `enumerate()` | Provides index and value |
| `dict.keys()` | Provides dictionary keys |
| `dict.values()` | Provides dictionary values |
| `dict.items()` | Provides key-value pairs |
| Nested loop | A loop inside another loop |
| Loop `else` | Executes if the loop completes without `break` |

---

## 15. Self-Assessment Questions

Make sure you can answer these questions before moving forward.

1. What is a loop in Python?
2. What is the difference between an iterable and an iterator?
3. Why do we use a for loop?
4. What is the purpose of `range()`?
5. What is the difference between `range(5)` and `range(1, 5)`?
6. Why is the stop value excluded in `range()`?
7. What happens when the step value is negative?
8. Can we iterate through a dictionary using a for loop?
9. What is the purpose of `enumerate()`?
10. What is a nested loop?
11. When does the `else` block of a for loop execute?
12. What is the difference between `range()` and `list(range())`?

---

## 16. Learning Outcome

After completing this chapter, you should be able to:

- Understand how for loops work.
- Iterate through different Python collections.
- Generate number sequences using `range()`.
- Use `enumerate()` to access indexes and values.
- Iterate through dictionary keys and values.
- Build nested loops.
- Process customer records and API responses using loops.

### Next Topic

**while Loops in Python**

In the next chapter, we will learn condition-based repetition, infinite loops, loop termination, and practical retry mechanisms.
