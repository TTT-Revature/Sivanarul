
# Logical, Membership and Identity Operators in Python

## 1. Introduction

Python provides different types of operators to perform operations on values and objects.

In this chapter, we will learn three important operator groups:

1. Logical Operators
2. Membership Operators
3. Identity Operators

These operators help us make decisions, check whether data exists inside a collection, and determine whether two variables refer to the same object.

---

# 2. Logical Operators

## 2.1 What are Logical Operators?

Logical operators are used to combine multiple conditions or reverse a condition.

Python provides three logical operators:

| Operator | Meaning |
|---|---|
| `and` | Returns a truthy result only when both operands are truthy |
| `or` | Returns a truthy result when at least one operand is truthy |
| `not` | Reverses the truth value |

### Example

```python
age = 25
has_id = True

print(age >= 18 and has_id)
```

Output:

```text
True
```

Explanation:

- `age >= 18` evaluates to `True`.
- `has_id` is `True`.
- Both conditions are satisfied.
- Therefore, the result is `True`.

## 2.2 AND Operator

The `and` operator evaluates to a truthy result only when both operands are truthy.

### Truth Table

| Condition A | Condition B | A and B |
|---|---|---|
| True | True | True |
| True | False | False |
| False | True | False |
| False | False | False |

### Example

```python
age = 24
salary = 50000

if age >= 18 and salary >= 30000:
    print("Eligible")
else:
    print("Not eligible")
```

Output:

```text
Eligible
```

Real-world example:

A user can access a particular service only when:
- The user is above the required age.
- The user meets the income requirement.

Both conditions must be satisfied.

## 2.3 OR Operator

The `or` operator evaluates to a truthy result when at least one operand is truthy.

### Truth Table

| Condition A | Condition B | A or B |
|---|---|---|
| True | True | True |
| True | False | True |
| False | True | True |
| False | False | False |

### Example

```python
is_admin = False
is_manager = True

if is_admin or is_manager:
    print("Access granted")
else:
    print("Access denied")
```

Output:

```text
Access granted
```

Explanation:

The user can access the application if they are either an administrator or a manager.

Only one condition needs to be satisfied.

## 2.4 NOT Operator

The `not` operator reverses the truth value of an expression.

### Truth Table

| Condition | not Condition |
|---|---|
| True | False |
| False | True |

### Example

```python
is_blocked = False

if not is_blocked:
    print("User can continue")
else:
    print("User is blocked")
```

Output:

```text
User can continue
```

Explanation:

- `is_blocked` is `False`.
- `not False` becomes `True`.
- Therefore, the user can continue.

---

# 3. Truthy and Falsy Values

Python does not require every condition to contain an explicit Boolean value.

Python evaluates certain values as either truthy or falsy.

## 3.1 Falsy Values

The following common values are considered falsy:

```python
False
None
0
0.0
""
[]
()
{}
set()
```

Example:

```python
name = ""

if name:
    print("Name is available")
else:
    print("Name is empty")
```

Output:

```text
Name is empty
```

## 3.2 Truthy Values

Non-empty strings, non-empty collections, and non-zero numbers are generally truthy.

```python
name = "Sivan"
age = 25
skills = ["Python", "FastAPI"]

if name:
    print("Name is available")

if age:
    print("Age is available")

if skills:
    print("Skills are available")
```

Output:

```text
Name is available
Age is available
Skills are available
```

Note:

User-defined objects can customize their truthiness using special methods such as `__bool__()` or `__len__()`.

---

# 4. Short-Circuit Evaluation

Short-circuit evaluation means Python can stop evaluating a logical expression as soon as the result is determined.

This is an important Python concept.

## 4.1 Short-Circuiting with AND

In an `and` expression, if the first operand is falsy, Python does not evaluate the second operand.

Example:

```python
def check_status():
    print("Function executed")
    return True

result = False and check_status()

print(result)
```

Output:

```text
False
```

Notice:

The function was not executed because the first operand was already `False`.

## 4.2 Short-Circuiting with OR

In an `or` expression, if the first operand is truthy, Python does not evaluate the second operand.

Example:

```python
def check_status():
    print("Function executed")
    return True

result = True or check_status()

print(result)
```

Output:

```text
True
```

Notice:

The function was not executed because the first operand was already `True`.

## 4.3 Important Technical Point

Unlike comparison operators, `and` and `or` do not always return Boolean values.

They return one of their operands.

Example:

```python
name = "Python"

result = name and "Available"

print(result)
```

Output:

```text
Available
```

Another example:

```python
name = ""

result = name or "Unknown"

print(result)
```

Output:

```text
Unknown
```

This behavior is commonly used to provide default values.

---

# 5. Membership Operators

## 5.1 What are Membership Operators?

Membership operators are used to check whether a value exists inside a collection or sequence.

Python provides two membership operators:

| Operator | Meaning |
|---|---|
| `in` | Checks whether a value exists |
| `not in` | Checks whether a value does not exist |

These operators commonly work with:
- Strings
- Lists
- Tuples
- Sets
- Dictionaries

## 5.2 IN Operator

The `in` operator checks whether a particular value exists in a collection.

### Example with a List

```python
skills = ["Python", "SQL", "FastAPI"]

print("Python" in skills)
print("Java" in skills)
```

Output:

```text
True
False
```

### Example with a String

```python
message = "Welcome to Python"

print("Python" in message)
print("Java" in message)
```

Output:

```text
True
False
```

### Example with a Tuple

```python
numbers = (10, 20, 30, 40)

print(20 in numbers)
```

Output:

```text
True
```

### Example with a Set

```python
allowed_roles = {"admin", "manager", "developer"}

print("admin" in allowed_roles)
```

Output:

```text
True
```

## 5.3 Membership in Dictionaries

When using `in` with a dictionary, Python checks for the existence of a key, not a value.

Example:

```python
employee = {
    "name": "Arun",
    "role": "Developer",
    "salary": 50000
}

print("name" in employee)
print("Arun" in employee)
```

Output:

```text
True
False
```

To check dictionary values:

```python
print("Arun" in employee.values())
```

Output:

```text
True
```

To check dictionary keys explicitly:

```python
print("name" in employee.keys())
```

Output:

```text
True
```

## 5.4 NOT IN Operator

The `not in` operator checks whether a value does not exist in a collection.

Example:

```python
blocked_users = ["user101", "user102", "user103"]

username = "user200"

if username not in blocked_users:
    print("User is allowed")
else:
    print("User is blocked")
```

Output:

```text
User is allowed
```

### Real-World FDE Example

Imagine building an application that checks whether a requested feature is enabled.

```python
enabled_features = ["chat", "reports", "analytics"]

requested_feature = "analytics"

if requested_feature in enabled_features:
    print("Feature is available")
else:
    print("Feature is not available")
```

Output:

```text
Feature is available
```

---

# 6. Identity Operators

## 6.1 What are Identity Operators?

Identity operators are used to check whether two variables refer to the exact same object in memory.

Python provides two identity operators:

| Operator | Meaning |
|---|---|
| `is` | Checks whether two references point to the same object |
| `is not` | Checks whether two references point to different objects |

Important:

Identity and equality are different concepts.

- Equality (`==`) compares values.
- Identity (`is`) compares object identity.

## 6.2 IS Operator

The `is` operator checks whether two variables refer to the same object.

Example:

```python
a = [10, 20, 30]
b = a

print(a is b)
```

Output:

```text
True
```

Explanation:

- `a` refers to a list object.
- `b = a` assigns another reference to the same list.
- Both variables refer to the same object.
- Therefore, `a is b` returns `True`.

## 6.3 IS NOT Operator

The `is not` operator checks whether two variables refer to different objects.

Example:

```python
a = [10, 20, 30]
b = [10, 20, 30]

print(a is not b)
```

Output:

```text
True
```

Explanation:

Both lists contain identical values, but Python creates two separate list objects.

Therefore, their values are equal, but their identities are different.

## 6.4 Difference Between == and is

This is one of the most important concepts in Python.

Example:

```python
a = [10, 20, 30]
b = [10, 20, 30]

print(a == b)
print(a is b)
```

Output:

```text
True
False
```

Explanation:

| Expression | Meaning | Result |
|---|---|---|
| `a == b` | Do both lists contain equal values? | True |
| `a is b` | Do both variables refer to the same object? | False |

Visual representation:

```text
a -------> [10, 20, 30]

b -------> [10, 20, 30]
```

There are two separate list objects.

Now consider:

```python
a = [10, 20, 30]
b = a

print(a == b)
print(a is b)
```

Output:

```text
True
True
```

Visual representation:

```text
a ----\
       ---> [10, 20, 30]
b ----/
```

Both variables refer to the same object.

## 6.5 Why Should We Use `is None`?

In Python, the recommended way to check whether a value is `None` is:

```python
result = None

if result is None:
    print("No result available")
```

Output:

```text
No result available
```

You can also check the opposite:

```python
if result is not None:
    print("Result available")
else:
    print("Result unavailable")
```

Why use `is None`?

`None` is a singleton object in Python. There is only one `None` object, so identity comparison is appropriate.

Avoid using:

```python
if result == None:
    print("No result")
```

Prefer:

```python
if result is None:
    print("No result")
```

---

# 7. Difference Between All Three Operator Groups

| Operator Group | Operators | Purpose |
|---|---|---|
| Logical | `and`, `or`, `not` | Combine or reverse conditions |
| Membership | `in`, `not in` | Check whether a value exists in a collection |
| Identity | `is`, `is not` | Check whether references point to the same object |

### Combined Example

```python
user = {
    "name": "Arun",
    "role": "admin",
    "active": True
}

allowed_roles = ["admin", "manager"]

if user is not None and user["active"] and user["role"] in allowed_roles:
    print("Access granted")
else:
    print("Access denied")
```

Output:

```text
Access granted
```

Explanation:

1. `user is not None` checks that a user object is available.
2. `user["active"]` checks whether the user is active.
3. `user["role"] in allowed_roles` checks whether the user's role is permitted.
4. `and` combines all three conditions.

Note: This is an educational example. Production authentication and authorization must also include proper server-side validation and access-control checks.

---

# 8. Common Mistakes

## Mistake 1: Using && Instead of and

Incorrect:

```python
if age >= 18 && age <= 60:
    print("Eligible")
```

Python does not use `&&` for logical AND.

Correct:

```python
if age >= 18 and age <= 60:
    print("Eligible")
```

## Mistake 2: Incorrect Use of OR

Incorrect:

```python
role = "admin"

if role == "admin" or "manager":
    print("Access granted")
```

This condition is always truthy because `"manager"` is a non-empty string.

Correct:

```python
if role == "admin" or role == "manager":
    print("Access granted")
```

Another correct approach:

```python
if role in ("admin", "manager"):
    print("Access granted")
```

## Mistake 3: Using is Instead of ==

Incorrect when comparing values:

```python
a = [10, 20]
b = [10, 20]

print(a is b)
```

This returns `False` because they are different objects.

Correct:

```python
print(a == b)
```

Output:

```text
True
```

## Mistake 4: Assuming Dictionary Membership Checks Values

```python
employee = {"name": "Arun"}

print("Arun" in employee)
```

Output:

```text
False
```

Because dictionary membership checks keys by default.

Correct:

```python
print("Arun" in employee.values())
```

Output:

```text
True
```

---

# 9. Practical FDE Use Cases

These operators are frequently used when developing real-world applications.

## Use Case 1: API Request Validation

```python
username = "Arun"
password = "password123"

if username and password:
    print("Request data is available")
else:
    print("Missing required fields")
```

## Use Case 2: Role-Based Access

```python
user_role = "admin"

if user_role in ["admin", "manager"]:
    print("Permission granted")
else:
    print("Permission denied")
```

## Use Case 3: Checking Optional Data

```python
user = None

if user is None:
    print("User does not exist")
```

## Use Case 4: Checking Feature Availability

```python
features = ["chat", "reports", "analytics"]

if "analytics" in features:
    print("Analytics feature enabled")
```

## Use Case 5: Safe Attribute Access with Short-Circuiting

```python
user = None

if user is not None and user.is_active:
    print("User is active")
else:
    print("User is unavailable or inactive")
```

Because `and` short-circuits, Python will not try to access `user.is_active` when `user` is `None`.

---

# 10. Quick Revision

| Concept | Operator | Example |
|---|---|---|
| Logical AND | `and` | `True and False` |
| Logical OR | `or` | `True or False` |
| Logical NOT | `not` | `not True` |
| Membership | `in` | `"Python" in skills` |
| Non-membership | `not in` | `"Java" not in skills` |
| Identity | `is` | `a is b` |
| Non-identity | `is not` | `a is not b` |
| Equality | `==` | `a == b` |

Important points:

- `and` requires both operands to be truthy to return a truthy result.
- `or` returns a truthy result when at least one operand is truthy.
- `not` reverses the truth value.
- `and` and `or` use short-circuit evaluation.
- `in` checks membership.
- Dictionary membership checks keys by default.
- `is` checks object identity.
- `==` checks equality.
- Use `is None` to check for `None`.

---

# 11. Practice Exercises

Try these exercises without immediately looking at the answers.

## Exercise 1: Logical Operators

Predict the output:

```python
a = 10
b = 20

print(a > 5 and b > 15)
print(a > 15 or b > 15)
print(not a > 5)
```

## Exercise 2: Membership Operators

Predict the output:

```python
languages = ["Python", "Java", "JavaScript"]

print("Python" in languages)
print("C++" not in languages)
print("Java" in languages)
```

## Exercise 3: Dictionary Membership

Predict the output:

```python
employee = {
    "name": "Arun",
    "department": "IT"
}

print("name" in employee)
print("Arun" in employee)
print("Arun" in employee.values())
```

## Exercise 4: Identity vs Equality

Predict the output:

```python
x = [1, 2, 3]
y = [1, 2, 3]
z = x

print(x == y)
print(x is y)
print(x is z)
```

## Exercise 5: Short-Circuit Evaluation

Predict the output:

```python
def display():
    print("Function called")
    return True

result = False and display()

print(result)
```

## Exercise 6: Real-World Application

Create a program with these conditions:

- A user must be at least 18 years old.
- The user must have an active account.
- The user role must be either `admin` or `manager`.

Use logical and membership operators to determine whether access should be granted.

---

# 12. Self-Assessment

Before moving to the next topic, make sure you can explain:

1. What is the difference between `and` and `or`?
2. What is short-circuit evaluation?
3. What are truthy and falsy values?
4. What is the difference between `in` and `not in`?
5. How does membership checking work with dictionaries?
6. What is the difference between `==` and `is`?
7. Why should we use `is None` instead of `== None`?
8. Can `and` and `or` return values other than Boolean values?

---

# 13. Connection to Forward Deployed Engineering

As a Forward Deployed Engineer, you will frequently work with:

- API request validation.
- User authentication and authorization.
- Feature availability checks.
- Configuration validation.
- Data filtering.
- Optional values and missing data.
- Business rules and conditional workflows.

Understanding these operators gives you the foundation to write reliable application logic before moving into advanced Python concepts and API development.

