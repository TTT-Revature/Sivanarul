
# Python Loop Control Statements: break, continue and pass

## 1. Introduction

Python provides three important statements to control loop execution:

1. `break`
2. `continue`
3. `pass`

Although all three are used inside loops, their purposes are different.

| Statement | Purpose |
|---|---|
| `break` | Terminates the nearest enclosing loop |
| `continue` | Skips the remaining code in the current iteration |
| `pass` | Does nothing; acts as a placeholder |

Let's understand each statement with examples.

---

# 2. break Statement

## What is break?

The `break` statement immediately terminates the nearest enclosing loop.

Once Python encounters `break`, it exits that loop and continues executing the code after the loop.

### Syntax

```python
for variable in iterable:
    if condition:
        break
```

The same concept applies to a `while` loop.

### Example 1: Basic break with for Loop

```python
for number in range(1, 10):
    print(number)

    if number == 5:
        break
```

Output:

```text
1
2
3
4
5
```

### Execution Explanation

| Iteration | number | Condition (`number == 5`) | Action |
|---|---:|---|---|
| 1 | 1 | False | Print 1 |
| 2 | 2 | False | Print 2 |
| 3 | 3 | False | Print 3 |
| 4 | 4 | False | Print 4 |
| 5 | 5 | True | Execute break |

When the value reaches 5, Python terminates the loop.

Numbers 6, 7, 8, and 9 are not processed.

### Example 2: break with while Loop

```python
number = 1

while number <= 10:

    print(number)

    if number == 5:
        break

    number += 1
```

Output:

```text
1
2
3
4
5
```

### Example 3: Searching for an Element

Imagine we have a list of employee names and want to find a particular employee.

```python
employees = ["Arun", "Kumar", "Siva", "Ravi"]

for employee in employees:

    if employee == "Siva":
        print("Employee found")
        break

    print("Checking:", employee)
```

Output:

```text
Checking: Arun
Checking: Kumar
Employee found
```

Once the employee is found, there is no need to continue searching.

### Example 4: Finding a Number

```python
numbers = [10, 20, 30, 40, 50]

target = 30

for number in numbers:

    if number == target:
        print("Target found:", number)
        break
```

Output:

```text
Target found: 30
```

### Example 5: break in Nested Loops

When using nested loops, `break` terminates only the nearest enclosing loop.

```python
for row in range(1, 4):

    for column in range(1, 4):

        if column == 2:
            break

        print("Row:", row, "Column:", column)
```

Output:

```text
Row: 1 Column: 1
Row: 2 Column: 1
Row: 3 Column: 1
```

The inner loop terminates whenever `column` becomes 2.

The outer loop continues with the next row.

**Important:** A single `break` does not automatically terminate all nested loops.

---

# 3. continue Statement

## What is continue?

The `continue` statement skips the remaining statements in the current iteration and moves to the next iteration.

Unlike `break`, it does not terminate the entire loop.

### Syntax

```python
for variable in iterable:

    if condition:
        continue

    # Remaining statements
```

### Example 1: Skip Number 3

```python
for number in range(1, 6):

    if number == 3:
        continue

    print(number)
```

Output:

```text
1
2
4
5
```

### Execution Explanation

| Iteration | number | Condition (`number == 3`) | Action |
|---|---:|---|---|
| 1 | 1 | False | Print 1 |
| 2 | 2 | False | Print 2 |
| 3 | 3 | True | Skip print |
| 4 | 4 | False | Print 4 |
| 5 | 5 | False | Print 5 |

When the value reaches 3, Python skips the remaining statements in that iteration.

The loop continues with 4.

### Example 2: Skip Even Numbers

```python
for number in range(1, 11):

    if number % 2 == 0:
        continue

    print(number)
```

Output:

```text
1
3
5
7
9
```

Explanation:

- `%` calculates the remainder.
- Even numbers produce a remainder of 0 when divided by 2.
- `continue` skips those even numbers.
- Odd numbers are printed.

### Example 3: continue with while Loop

```python
number = 0

while number < 5:

    number += 1

    if number == 3:
        continue

    print(number)
```

Output:

```text
1
2
4
5
```

Notice that the increment happens before `continue`.

This ensures that the loop variable continues changing.

### Example 4: Processing Valid Records

Imagine we have customer records, and some records are missing email addresses.

```python
customers = [
    {"name": "Arun", "email": "arun@example.com"},
    {"name": "Kumar", "email": ""},
    {"name": "Siva", "email": "siva@example.com"}
]

for customer in customers:

    if not customer["email"]:
        continue

    print("Processing:", customer["email"])
```

Output:

```text
Processing: arun@example.com
Processing: siva@example.com
```

The records without email addresses are skipped.

### Example 5: Skip Negative Numbers

```python
numbers = [10, -5, 20, -3, 30]

for number in numbers:

    if number < 0:
        continue

    print(number)
```

Output:

```text
10
20
30
```

---

# 4. pass Statement

## What is pass?

The `pass` statement is a null operation.

It does nothing when executed.

It is used when Python requires a statement syntactically, but we do not want to implement the logic yet.

### Syntax

```python
pass
```

### Example 1: Basic pass

```python
for number in range(1, 6):

    if number == 3:
        pass

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

When `number` becomes 3, Python executes `pass`.

However, `pass` does not skip the iteration.

The `print()` statement still executes.

### Example 2: pass with while Loop

```python
number = 1

while number <= 5:

    if number == 3:
        pass

    print(number)

    number += 1
```

Output:

```text
1
2
3
4
5
```

### Example 3: Placeholder for Future Implementation

Imagine we are developing an employee management application.

We have planned different operations, but some functionality is not implemented yet.

```python
def add_employee():
    pass


def update_employee():
    pass


def delete_employee():
    pass


def view_employee():
    print("Displaying employee details")
```

Python accepts this code because `pass` provides a valid statement inside the unfinished functions.

Without a statement, an empty function body would produce an indentation or syntax error.

### Example 4: Placeholder in Conditional Statements

```python
age = 25

if age >= 18:
    pass
else:
    print("Not eligible")
```

No action is performed when the condition is True.

This is syntactically valid, although it is only useful as a temporary placeholder.

---

# 5. Difference Between break, continue and pass

This is one of the most important comparisons in Python loops.

| Feature | break | continue | pass |
|---|---|---|---|
| Terminates loop | Yes | No | No |
| Skips current iteration | Exits the loop | Yes | No |
| Executes remaining statements | No | Skips remaining loop-body statements in current iteration | Yes |
| Main purpose | Stop loop | Skip an iteration | Placeholder |
| Works in loops | Yes | Yes | Yes |
| Can be used in functions | No, not independently | No, not independently | Yes |

### Visual Understanding

Suppose we have:

```python
for number in range(1, 6):
    print(number)

    if number == 3:
        # Control statement here

    print("Next statement")
```

Depending on the statement:

**Using break**

```python
if number == 3:
    break
```

Output:

```text
1
Next statement
2
Next statement
3
```

The loop terminates at 3.

**Using continue**

```python
if number == 3:
    continue
```

Output:

```text
1
Next statement
2
Next statement
3
4
Next statement
5
Next statement
```

The `continue` skips the second print statement only for number 3.

**Using pass**

```python
if number == 3:
    pass
```

Output:

```text
1
Next statement
2
Next statement
3
Next statement
4
Next statement
5
Next statement
```

The `pass` statement has no effect on execution flow.

---

# 6. Loop Control Statements with else

Python supports `else` blocks with both `for` and `while` loops.

The loop's `else` block executes when the loop completes normally, without being terminated by `break`.

### Example 1: break prevents else

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

### Example 2: continue does not prevent else

```python
for number in range(1, 6):

    if number == 3:
        continue

    print(number)

else:
    print("Loop completed")
```

Output:

```text
1
2
4
5
Loop completed
```

The loop completes normally, so the `else` block executes.

### Example 3: pass does not prevent else

```python
for number in range(1, 4):

    if number == 2:
        pass

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

`pass` does not affect normal loop completion.

---

# 7. Practical FDE Applications

Forward Deployed Engineers frequently work with APIs, external integrations, customer records, and automated workflows.

These control statements help manage those operations.

## Example 1: Stop Processing When an Error Occurs

```python
api_responses = [
    {"status": 200},
    {"status": 200},
    {"status": 500},
    {"status": 200}
]

for response in api_responses:

    if response["status"] >= 500:
        print("Server error detected")
        break

    print("Response processed:", response["status"])
```

Output:

```text
Response processed: 200
Response processed: 200
Server error detected
```

The processing stops when a server error is detected.

## Example 2: Skip Invalid Customer Records

```python
customers = [
    {"name": "Arun", "age": 25},
    {"name": "", "age": 30},
    {"name": "Siva", "age": 28}
]

for customer in customers:

    if not customer["name"]:
        continue

    print("Valid customer:", customer["name"])
```

Output:

```text
Valid customer: Arun
Valid customer: Siva
```

## Example 3: Develop a Feature in Stages

```python
def authenticate_user():
    print("Authentication implemented")


def process_payment():
    pass


def generate_invoice():
    pass


authenticate_user()
process_payment()
generate_invoice()
```

Output:

```text
Authentication implemented
```

The `pass` statements allow us to define the structure before implementing all functionality.

**Production note:** A placeholder should eventually be replaced with actual implementation or an explicit error. Silent placeholders can hide incomplete functionality.

---

# 8. Common Mistakes

## Mistake 1: Using break Outside a Loop

Incorrect:

```python
if True:
    break
```

Output:

```text
SyntaxError: 'break' outside loop
```

`break` must be inside a loop.

## Mistake 2: Using continue Outside a Loop

Incorrect:

```python
if True:
    continue
```

Output:

```text
SyntaxError: 'continue' not properly in loop
```

`continue` must be inside a loop.

## Mistake 3: Thinking pass Skips an Iteration

Incorrect assumption:

```python
for number in range(1, 4):

    if number == 2:
        pass

    print(number)
```

Output:

```text
1
2
3
```

`pass` does not skip the number 2.

Use `continue` if you want to skip the current iteration.

## Mistake 4: Assuming break Exits Every Nested Loop

```python
for row in range(1, 3):

    for column in range(1, 4):

        if column == 2:
            break

        print(row, column)
```

`break` terminates only the inner loop. The outer loop continues.

## Mistake 5: Infinite Loop with continue

Incorrect:

```python
number = 1

while number <= 5:

    if number == 3:
        continue

    number += 1
```

When `number` reaches 3, the increment is skipped. The loop never progresses beyond 3.

Correction:

```python
number = 1

while number <= 5:

    current = number
    number += 1

    if current == 3:
        continue

    print(current)
```

---

# 9. Practice Exercises

Try solving these without looking at the examples.

## Beginner Level

1. Print numbers from 1 to 10, but stop when the number reaches 6 using `break`.
2. Print numbers from 1 to 10, but skip number 5 using `continue`.
3. Write a loop using `pass` when the number is equal to 3.
4. Print only odd numbers from 1 to 20 using `continue`.
5. Stop a loop when a particular employee name is found.

## Intermediate Level

6. Find a target number in a list and terminate the search using `break`.
7. Iterate through a list and skip all negative numbers using `continue`.
8. Write a nested loop where the inner loop terminates when its column value reaches 3.
9. Create a loop with an `else` block and observe the difference between normal completion and `break`.
10. Build a number-search program using a while loop and `break`.

## Practical FDE Exercises

11. Process customer records and skip records with missing email addresses.
12. Stop processing API response records when a critical server error occurs.
13. Build a validation workflow that skips invalid records.
14. Create an employee management application with placeholder functions using `pass`.
15. Process a list of API responses and stop when a specified status code is encountered.

---

# 10. Quick Revision

| Statement | What happens? | Example use case |
|---|---|---|
| `break` | Exits the nearest enclosing loop | Stop searching after finding a record |
| `continue` | Skips current iteration | Ignore invalid customer records |
| `pass` | Performs no operation | Placeholder for future implementation |

Remember:

- `break` = Stop the loop.
- `continue` = Skip this iteration.
- `pass` = Do nothing.

---

# 11. Self-Assessment Questions

1. What is a loop control statement?
2. What is the purpose of `break`?
3. What happens after Python executes `break`?
4. What is the purpose of `continue`?
5. Does `continue` terminate the loop?
6. What is the purpose of `pass`?
7. Does `pass` skip the current iteration?
8. What is the difference between `break` and `continue`?
9. Can we use `break` inside nested loops?
10. Does `continue` prevent the loop's `else` block from executing?
11. What happens to the loop's `else` block when `break` executes?
12. Why is `pass` useful during application development?

---

# 12. Learning Outcome

After completing this chapter, you should be able to:

- Control loop execution using `break`.
- Skip selected iterations using `continue`.
- Use `pass` as a placeholder.
- Understand control flow in nested loops.
- Understand how loop control statements interact with `else`.
- Apply loop control to API processing and data validation workflows.

## Next Topic

**Nested Loops and Loop Patterns in Python**

We will explore nested iteration, execution tracing, pattern printing, and practical problems involving multiple levels of loops.
