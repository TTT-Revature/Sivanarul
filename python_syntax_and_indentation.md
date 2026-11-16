
# Python Syntax and Indentation

## 1. What is Python Syntax?

Syntax refers to the rules and structure used to write a programming language.

Just as English has grammar rules, Python has syntax rules that determine how instructions should be written.

For example:

```python
print("Hello, World!")
```

This is valid Python syntax.

But:

```python
print("Hello, World!"
```

This produces a SyntaxError because the closing parenthesis is missing.

**Real-world analogy:**

Think of syntax as grammar in English. If we arrange words incorrectly, the sentence may not communicate properly. Similarly, Python expects code to follow its syntax rules.

---

## 2. Basic Structure of a Python Program

A Python program consists of statements and expressions.

### Statement

A statement is an instruction that Python executes.

```python
name = "Sivanarul"
age = 27

print(name)
print(age)
```

Here:
- `name = "Sivanarul"` is an assignment statement.
- `age = 27` is an assignment statement.
- `print(name)` is a function call statement.

### Expression

An expression is a combination of values, variables, and operators that produces a result.

```python
a = 10
b = 20

result = a + b
print(result)
```

`a + b` is an expression because it produces the value `30`.

---

## 3. What is Indentation?

Indentation means adding spaces at the beginning of a line of code.

Python uses indentation to identify blocks of code.

Unlike some programming languages that use curly braces `{}` to define blocks, Python primarily uses indentation.

Example:

```python
age = 25

if age >= 18:
    print("Eligible to vote")
    print("You are an adult")

print("Program completed")
```

Explanation:

- `if age >= 18:` starts a conditional block.
- The two indented statements belong to the `if` block.
- `print("Program completed")` is outside the block.

**Important:** Python conventionally uses 4 spaces for each indentation level.

---

## 4. Why is Indentation Important?

Indentation helps Python understand which statements belong together.

Consider:

```python
age = 20

if age >= 18:
    print("Eligible")
    print("Adult category")
```

Both print statements execute when the condition is true.

Now consider:

```python
age = 20

if age >= 18:
    print("Eligible")

print("Adult category")
```

Here, the second print statement is outside the `if` block. It executes regardless of whether the condition is true or false.

The position of indentation changes the program's behavior.

---

## 5. Indentation Levels

Python supports multiple levels of indentation.

Example:

```python
age = 25

if age >= 18:
    print("Adult")

    if age >= 21:
        print("Above 21")

        if age >= 25:
            print("25 or older")
```

The indentation represents nested blocks.

Structure:

```text
Main Program
    |
    |-- First if condition
            |
            |-- Second if condition
                    |
                    |-- Third if condition
```

Every nested block should have a consistent indentation level.

---

## 6. Spaces vs Tabs

Python supports spaces and tabs for indentation, but mixing them can cause errors.

Recommended practice:

- Use 4 spaces for each indentation level.
- Avoid mixing tabs and spaces.
- Configure your code editor to insert spaces when pressing Tab.

Example:

```python
if True:
    print("Correct indentation")
```

Avoid inconsistent indentation:

```python
if True:
    print("First line")
      print("Second line")
```

The second statement has an unexpected indentation level and causes an error.

---

## 7. What is an IndentationError?

An IndentationError occurs when Python detects incorrect indentation.

Example:

```python
if True:
print("Hello")
```

Error:

```text
IndentationError: expected an indented block
```

Correct version:

```python
if True:
    print("Hello")
```

### Another example

```python
if True:
    print("First line")
        print("Second line")
```

Possible error:

```text
IndentationError: unexpected indent
```

Correct version:

```python
if True:
    print("First line")
    print("Second line")
```

---

## 8. Python Blocks

A block is a group of statements that belong to a particular control structure, function, or class.

Python uses indentation to define these blocks.

### A. Conditional block

```python
temperature = 35

if temperature > 30:
    print("It is hot")
else:
    print("Weather is comfortable")
```

### B. Loop block

```python
for number in range(1, 4):
    print(number)
```

### C. Function block

```python
def greet():
    print("Hello")
    print("Welcome to Python")

greet()
```

### D. Class block

```python
class Employee:
    def display(self):
        print("Employee details")

employee = Employee()
employee.display()
```

Notice that each block uses indentation to define its boundaries.

---

## 9. Comments in Python

Comments are notes written inside source code. Python ignores comments during normal execution.

### Single-line comment

Use `#` to write a comment.

```python
# This is a single-line comment

name = "Python"
print(name)
```

### Inline comment

```python
age = 25  # Employee age
```

### Multi-line explanation

Python does not have a dedicated multi-line comment syntax.

You can use multiple `#` lines:

```python
# This program calculates
# the total price of
# two products

price1 = 100
price2 = 200

total = price1 + price2
print(total)
```

Triple-quoted strings are sometimes used for documentation, but they are string literals, not technically comments.

---

## 10. Python Case Sensitivity

Python is case-sensitive.

This means uppercase and lowercase letters are treated differently.

Example:

```python
name = "Python"

Name = "Java"

print(name)
print(Name)
```

Output:

```text
Python
Java
```

These are two different variables.

Another example:

```python
print("Hello")
```

Correct.

```python
Print("Hello")
```

Incorrect because Python does not recognize `Print` as the built-in `print` function.

---

## 11. Python Syntax Rules to Remember

| Rule | Explanation |
|---|---|
| Indentation | Use 4 spaces as the standard |
| Case sensitivity | `name` and `Name` are different |
| Colon | Required after statements such as `if`, `for`, `while`, `def`, and `class` |
| Parentheses | Must be properly opened and closed |
| Comments | Use `#` |
| Strings | Use matching single or double quotes |
| Blocks | Use consistent indentation |

---

## 12. Practical Example: Employee Eligibility

Let's combine syntax, indentation, variables, conditions, and comments.

```python
# Employee eligibility program

employee_name = "Arun"
employee_age = 24
minimum_age = 18

if employee_age >= minimum_age:
    print("Employee:", employee_name)
    print("Eligible for the position")
else:
    print("Not eligible")
```

Explanation:

1. Variables store employee information.
2. The `if` statement checks the employee's age.
3. Indentation identifies the statements inside the condition.
4. The `else` block executes when the condition is false.
5. Comments explain the purpose of the program.

---

## 13. FDE Connection: Why Syntax and Indentation Matter

As a Forward Deployed Engineer, you may work with customer-specific Python applications, APIs, automation scripts, and AI integrations.

Consider a customer integration:

```python
def process_customer_data(customer):
    if customer["active"]:
        print("Processing customer")

        if customer["verified"]:
            print("Customer verified")
            return True

    return False
```

If indentation is incorrect, the application may:
- Execute the wrong statements.
- Skip important validation.
- Return unexpected results.
- Fail during execution.

As an FDE, you should be able to read existing code, identify syntax errors, debug indentation issues, and understand the execution flow.

---

## 14. Practice Tasks

### Beginner Level

**Task 1:** Write a Python program that prints your name, age, and profession.

**Task 2:** Create two variables and calculate their sum.

**Task 3:** Write an `if-else` program to check whether a number is positive or negative.

### Intermediate Level

**Task 4:** Write a program to check whether a person is eligible to vote.

**Task 5:** Use a `for` loop to print numbers from 1 to 10.

**Task 6:** Create a function that checks whether a number is even or odd.

### Debugging Practice

Identify and correct the indentation error:

```python
age = 25

if age >= 18:
print("Eligible")
    print("Adult")
```

---

## 15. Quick Revision

| Concept | Meaning |
|---|---|
| Syntax | Rules for writing Python code |
| Statement | An instruction executed by Python |
| Expression | Code that produces a value |
| Indentation | Spaces at the beginning of a line |
| Block | Group of statements belonging together |
| Comment | Explanation ignored during normal execution |
| SyntaxError | Invalid Python syntax |
| IndentationError | Incorrect indentation |

---

## 16. Self-Assessment

Try answering these questions without referring to the notes.

1. What is Python syntax?
2. What is indentation?
3. Why does Python use indentation?
4. How many spaces are recommended for one indentation level?
5. What is the difference between a statement and an expression?
6. What happens if indentation is incorrect?
7. Is Python case-sensitive?
8. What is the purpose of comments?
9. Which symbol is used to start a single-line comment?
10. Why is indentation important when developing customer-facing applications?

---

## Learning Note

**Topic:** Python Syntax and Indentation

**Status:** To be completed

**Practical exercises:** To be completed

**Doubt clarification:** Pending

**Next topic:** Python Variables and Constants
