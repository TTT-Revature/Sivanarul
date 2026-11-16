
# Python Variables and Naming Conventions

## 1. What is a Variable?

A variable is a name used to refer to an object in Python.

It allows us to store and access data while executing a program.

Example:

```python
name = "Sivanarul"
age = 27
salary = 41666.50

print(name)
print(age)
print(salary)
```

Output:

```text
Sivanarul
27
41666.5
```

Here:
- `name` refers to a string object.
- `age` refers to an integer object.
- `salary` refers to a floating-point object.

**Real-world analogy:**

Think of a variable as a label attached to a storage container.

The label helps us identify and access the information associated with it.

In Python, a variable name refers to an object rather than acting as a fixed physical box.

---

## 2. How to Create a Variable?

Python does not require us to declare a variable's data type explicitly.

We can create a variable by assigning a value using the `=` operator.

Syntax:

```python
variable_name = value
```

Example:

```python
employee_name = "Arun"
employee_age = 25
is_active = True
```

Python determines the object's type at runtime.

We can check the type using the `type()` function.

```python
name = "Arun"
age = 25
salary = 30000.50
is_active = True

print(type(name))
print(type(age))
print(type(salary))
print(type(is_active))
```

Output:

```text
<class 'str'>
<class 'int'>
<class 'float'>
<class 'bool'>
```

---

## 3. Dynamic Typing in Python

Python is a dynamically typed language.

It means we do not need to specify a variable's type when assigning a value.

A variable name can also be reassigned to an object of another type.

Example:

```python
data = 100
print(type(data))

data = "Python"
print(type(data))

data = 25.5
print(type(data))
```

Output:

```text
<class 'int'>
<class 'str'>
<class 'float'>
```

Notice that the same variable name refers to different objects at different points in the program.

**Important:** Python is dynamically typed, but it is also strongly typed. It does not automatically combine incompatible types in every operation.

Example:

```python
age = 25
name = "Arun"

print(age + name)
```

This raises a `TypeError`.

---

## 4. Variable Assignment

Assignment means associating a variable name with an object.

### A. Single Assignment

```python
name = "Python"
```

### B. Multiple Assignment

We can assign values to multiple variables in one statement.

```python
name, age, city = "Arun", 25, "Chennai"

print(name)
print(age)
print(city)
```

### C. Assigning the Same Value

```python
a = b = c = 100

print(a)
print(b)
print(c)
```

All three names initially refer to the same integer object.

### D. Reassigning a Variable

```python
price = 1000
print(price)

price = 1500
print(price)
```

Output:

```text
1000
1500
```

The variable name now refers to the newly assigned value.

---

## 5. Understanding Variable References and Memory

Python variables are names that refer to objects.

Let's understand this with an example.

```python
a = 100
b = a

print(a)
print(b)
print(a is b)
```

Output:

```text
100
100
True
```

Here:
- `a` refers to the integer object `100`.
- `b` also refers to that same object.
- `is` checks whether both names refer to the same object.

We can inspect an object's identity using `id()`.

```python
a = 100
b = a

print(id(a))
print(id(b))
```

Both IDs will be the same while both names refer to the same object.

### Mutable Object Example

```python
list_a = [10, 20, 30]
list_b = list_a

list_b.append(40)

print(list_a)
print(list_b)
```

Output:

```text
[10, 20, 30, 40]
[10, 20, 30, 40]
```

Why?

Both variables refer to the same list object. Modifying the list through one reference is visible through the other.

This concept is important when working with Python applications, APIs, and data processing.

---

## 6. Rules for Naming Variables

Python has specific rules for variable names.

| Rule | Example |
|---|---|
| Must begin with a letter or underscore | `name`, `_age` |
| Cannot begin with a number | `1name` is invalid |
| Can contain letters, numbers, and underscores | `employee_1` |
| Cannot contain spaces | `employee name` is invalid |
| Cannot use special symbols such as `@`, `$`, `%` | `employee@name` is invalid |
| Variable names are case-sensitive | `name` and `Name` are different |
| Cannot use Python keywords | `class`, `if`, `for` are invalid |

Valid examples:

```python
name = "Arun"
employee_age = 25
employee1 = "Kumar"
_total = 5000
```

Invalid examples:

```python
1name = "Arun"
employee name = "Arun"
employee@name = "Arun"
class = "Python"
```

---

## 7. What are Naming Conventions?

Naming conventions are recommended practices for choosing meaningful names in a program.

Python has commonly accepted naming conventions described in PEP 8.

PEP 8 is the official Python style guide.

### A. Snake Case

Use lowercase words separated by underscores.

Commonly used for:
- Variables
- Functions
- Methods

Example:

```python
employee_name = "Arun"
total_salary = 50000
customer_address = "Chennai"
```

### B. Pascal Case

Start every word with an uppercase letter.

Commonly used for:
- Class names

Example:

```python
class EmployeeDetails:
    pass

class CustomerAccount:
    pass
```

### C. Uppercase with Underscores

Commonly used for constants.

Example:

```python
MAX_RETRY_COUNT = 3
DATABASE_TIMEOUT = 30
API_BASE_URL = "https://example.com"
```

### D. Leading Underscore

A leading underscore indicates that a name is intended for internal use.

Example:

```python
_internal_value = 100
```

This is a convention, not strict access control.

---

## 8. What are Constants?

A constant is a value that a developer intends not to change during program execution.

Python does not enforce constants directly.

By convention, we write constant names using uppercase letters and underscores.

Example:

```python
PI = 3.14159
MAX_USERS = 100
COMPANY_NAME = "Tech Solutions"

print(PI)
print(MAX_USERS)
```

Python still allows reassignment:

```python
MAX_USERS = 100
MAX_USERS = 200
```

Therefore, uppercase naming communicates the intention but does not make the value immutable.

---

## 9. Python Keywords

Keywords are reserved words that have special meaning in Python.

We cannot use them as variable names.

Examples:

```text
if
else
for
while
class
def
return
import
from
try
except
True
False
None
```

We can view the complete keyword list using:

```python
import keyword

print(keyword.kwlist)
```

We can check whether a word is a keyword:

```python
import keyword

print(keyword.iskeyword("class"))
print(keyword.iskeyword("employee"))
```

Output:

```text
True
False
```

---

## 10. Difference Between Variables and Data Types

A variable name refers to an object, and the object has a data type.

Example:

```python
name = "Python"
age = 25
price = 99.50
```

| Variable | Value | Data Type |
|---|---|---|
| `name` | `"Python"` | String |
| `age` | `25` | Integer |
| `price` | `99.50` | Float |

We can identify the data type using `type()`.

```python
print(type(name))
print(type(age))
print(type(price))
```

---

## 11. Practical Example: Employee Management

Let's combine variables, data types, and naming conventions.

```python
# Employee information

employee_name = "Arun"
employee_id = 101
employee_salary = 45000.50
is_active = True

# Display employee details

print("Employee Name:", employee_name)
print("Employee ID:", employee_id)
print("Employee Salary:", employee_salary)
print("Active Status:", is_active)
```

The names are meaningful and follow snake_case.

This makes the code easier to read and maintain.

---

## 12. FDE Connection: Variables in Real-World Applications

As a Forward-Deployed Engineer, you may work with customer data, API integrations, AI services, databases, and automation systems.

Consider a customer integration example:

```python
customer_name = "Arun"
customer_id = 101
api_timeout = 30
max_retry_count = 3
is_customer_active = True

print("Processing customer:", customer_name)
```

Why are meaningful variable names important?

1. Customer-specific integrations can contain many variables.
2. Meaningful names make debugging easier.
3. Other engineers can understand your code.
4. Clear naming reduces confusion during maintenance.
5. Consistent naming improves collaboration.

### Example: API Configuration

```python
API_BASE_URL = "https://api.example.com"
API_TIMEOUT = 30
MAX_RETRIES = 3

customer_id = 101
request_status = "pending"
```

Notice how constants and normal variables are named differently.

**Security note:** Never hardcode real API keys, passwords, or database credentials in source code. Use environment variables or an appropriate secrets manager.

---

## 13. Practice Tasks

### Beginner Level

**Task 1:** Create variables for your name, age, city, and profession.

**Task 2:** Create variables using integer, float, string, and Boolean values. Print their types.

**Task 3:** Assign one value to three different variables.

### Intermediate Level

**Task 4:** Create an employee record using meaningful variable names.

**Task 5:** Reassign an integer variable with a string value and observe its type.

**Task 6:** Create two variables referring to the same list. Modify the list through one variable and observe the other.

### Naming Practice

**Task 7:** Identify which names are valid:

```python
employee_name = "Arun"
1employee = "Arun"
employee_age = 25
employee@id = 101
_total_amount = 5000
class = "Python"
```

**Task 8:** Convert these names into recommended Python naming conventions:

- Employee Name
- Customer Account
- Total Salary
- Maximum Retry Count

---

## 14. Quick Revision

| Concept | Meaning |
|---|---|
| Variable | A name referring to an object |
| Assignment | Associating a name with an object |
| Dynamic Typing | Variable names can refer to objects of different types |
| `type()` | Returns an object's type |
| `id()` | Returns an object's identity |
| `is` | Checks object identity |
| Snake Case | `employee_name` |
| Pascal Case | `EmployeeDetails` |
| Constant Convention | `MAX_RETRY_COUNT` |
| PEP 8 | Python style guide |

---

## 15. Self-Assessment

Try answering these questions without referring to the notes.

1. What is a variable in Python?
2. How do you create a variable?
3. What is dynamic typing?
4. Does Python require explicit variable type declaration?
5. What is the difference between `=` and `==`?
6. What does the `type()` function do?
7. What does the `id()` function return?
8. What is the difference between `is` and `==`?
9. What is snake_case?
10. What is PascalCase?
11. Why do Python developers use uppercase names for constants?
12. Can we change the value of a Python constant?
13. What is PEP 8?
14. Why should we use meaningful variable names?
15. What happens when two variables refer to the same mutable object?

---

## Learning Note

**Topic:** Python Variables and Naming Conventions

**Status:** To be completed

**Practical exercises:** To be completed

**Doubt clarification:** Pending

**Next topic:** Python Data Types
