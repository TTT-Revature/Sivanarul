
# Python Basic Data Types

## 1. What are Data Types?

A data type defines the kind of value an object represents and the operations that can be performed on it.

For example:

```python
name = "Sivanarul"
age = 27
salary = 41666.50
is_employed = True
```

Here:

- `name` stores text.
- `age` stores a whole number.
- `salary` stores a decimal number.
- `is_employed` stores a Boolean value.

Python is dynamically typed, so we do not need to declare the data type explicitly when creating variables.

We can identify an object's type using the `type()` function.

```python
name = "Python"
age = 25
salary = 45000.50
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

## 2. Categories of Python Built-in Data Types

Python provides several built-in data types.

| Category | Data Types |
|---|---|
| Numeric | `int`, `float`, `complex` |
| Boolean | `bool` |
| Text | `str` |
| Sequence | `list`, `tuple`, `range` |
| Mapping | `dict` |
| Set | `set`, `frozenset` |
| Binary | `bytes`, `bytearray`, `memoryview` |
| None | `NoneType` |

We will first understand the fundamental data types.

---

## 3. Integer (`int`)

An integer represents a whole number without a decimal component.

Examples:

```python
age = 27
salary = 50000
temperature = -10
quantity = 100

print(type(age))
```

Output:

```text
<class 'int'>
```

### Integer Operations

```python
a = 20
b = 10

print(a + b)  # Addition
print(a - b)  # Subtraction
print(a * b)  # Multiplication
print(a / b)  # Division
print(a // b) # Floor division
print(a % b)  # Modulus
print(a ** b) # Exponentiation
```

Output:

```text
30
10
200
2.0
2
0
10240000000000
```

**Important:** Python integers can grow beyond fixed 32-bit or 64-bit ranges, subject to available memory.

---

## 4. Float (`float`)

A float represents a number with a fractional or decimal component.

Examples:

```python
price = 99.99
height = 182.5
temperature = -2.5

print(type(price))
```

Output:

```text
<class 'float'>
```

### Float Operations

```python
price = 100.50
tax = 10.25

total = price + tax

print(total)
```

Output:

```text
110.75
```

### Floating-Point Precision

Floating-point numbers cannot represent every decimal value exactly.

Example:

```python
a = 0.1
b = 0.2

print(a + b)
```

Possible output:

```text
0.30000000000000004
```

This happens because many decimal fractions have no exact representation in binary floating-point format.

For financial calculations, consider using the `decimal` module.

```python
from decimal import Decimal

a = Decimal("0.1")
b = Decimal("0.2")

print(a + b)
```

Output:

```text
0.3
```

---

## 5. Complex (`complex`)

A complex number contains a real part and an imaginary part.

Python uses `j` to represent the imaginary component.

Example:

```python
number = 3 + 4j

print(number)
print(type(number))
print(number.real)
print(number.imag)
```

Output:

```text
(3+4j)
<class 'complex'>
3.0
4.0
```

Complex numbers are commonly used in:

- Scientific computing
- Signal processing
- Engineering calculations
- Mathematical applications

---

## 6. Boolean (`bool`)

Boolean represents one of two logical values:

- `True`
- `False`

Example:

```python
is_active = True
is_verified = False

print(type(is_active))
```

Output:

```text
<class 'bool'>
```

### Boolean Expressions

```python
age = 25

print(age >= 18)
print(age < 18)
print(age == 25)
```

Output:

```text
True
False
True
```

### Logical Operators

Python provides three primary logical operators:

| Operator | Meaning |
|---|---|
| `and` | True when both conditions are true |
| `or` | True when at least one condition is true |
| `not` | Reverses the logical result |

Example:

```python
age = 25
has_id = True

print(age >= 18 and has_id)
print(age >= 18 or has_id)
print(not has_id)
```

Output:

```text
True
True
False
```

---

## 7. String (`str`)

A string represents a sequence of characters.

Strings can be created using single quotes, double quotes, or triple quotes.

Example:

```python
name = "Sivanarul"
city = 'Chennai'
description = """Python is a programming language."""

print(type(name))
```

Output:

```text
<class 'str'>
```

### String Operations

#### A. Concatenation

Combining strings using the `+` operator.

```python
first_name = "Sivan"
last_name = "Arul"

full_name = first_name + " " + last_name

print(full_name)
```

#### B. Repetition

```python
message = "Python "

print(message * 3)
```

Output:

```text
Python Python Python
```

#### C. Indexing

Accessing individual characters using their positions.

```python
language = "Python"

print(language[0])
print(language[1])
print(language[-1])
```

Output:

```text
P
y
n
```

Python indexing starts at zero.

#### D. Slicing

Extracting a portion of a string.

```python
language = "Python"

print(language[0:3])
print(language[2:6])
print(language[::-1])
```

Output:

```text
Pyt
thon
nohtyP
```

#### E. Common String Methods

```python
name = "  python developer  "

print(name.upper())
print(name.lower())
print(name.strip())
print(name.title())
print(name.replace("python", "AI"))
```

**Important:** Strings are immutable. Their existing contents cannot be changed directly.

---

## 8. NoneType (`None`)

`None` represents the absence of a value.

It is different from:

- `0`
- `False`
- An empty string
- An empty list

Example:

```python
result = None

print(result)
print(type(result))
```

Output:

```text
None
<class 'NoneType'>
```

### Practical Example

```python
customer_name = None

if customer_name is None:
    print("Customer name is not available")
```

Output:

```text
Customer name is not available
```

Use `is None` when checking whether a value is `None`.

---

## 9. Checking Data Types

Python provides the `type()` and `isinstance()` functions.

### Using type()

```python
age = 25

print(type(age))
```

### Using isinstance()

```python
age = 25

print(isinstance(age, int))
print(isinstance(age, str))
```

Output:

```text
True
False
```

`isinstance()` is particularly useful when validating data.

Example:

```python
def process_age(age):
    if isinstance(age, int):
        print("Valid integer")
    else:
        print("Invalid data type")

process_age(25)
process_age("25")
```

**Note:** In Python, `bool` is a subclass of `int`. Therefore, `isinstance(True, int)` returns `True`. If you need to accept only integers and reject Boolean values, use `type(value) is int`.

---

## 10. Type Conversion (Type Casting)

Type conversion means converting a value from one data type to another.

Python provides built-in conversion functions.

| Function | Conversion |
|---|---|
| `int()` | Converts to integer when possible |
| `float()` | Converts to float |
| `str()` | Converts to string |
| `bool()` | Converts to Boolean |
| `complex()` | Converts to complex number |
| `list()` | Converts an iterable to a list |
| `tuple()` | Converts an iterable to a tuple |
| `set()` | Converts an iterable to a set |

### A. Integer Conversion

```python
value = "100"

number = int(value)

print(number)
print(type(number))
```

### B. Float Conversion

```python
value = "99.50"

price = float(value)

print(price)
```

### C. String Conversion

```python
age = 25

age_text = str(age)

print(age_text)
print(type(age_text))
```

### D. Boolean Conversion

```python
print(bool(1))
print(bool(0))
print(bool(""))
print(bool("Python"))
```

Output:

```text
True
False
False
True
```

**Important:** Most non-empty strings and non-zero numbers are truthy. Empty strings, zero, and `None` are falsy.

### Conversion Error

```python
value = "Python"

number = int(value)
```

This raises:

```text
ValueError
```

Python cannot convert the text `"Python"` into an integer.

---

## 11. Mutable and Immutable Data Types

Python objects can be classified by whether their contents can be changed after creation.

### Immutable Data Types

Immutable objects cannot be modified after creation.

Examples:

- `int`
- `float`
- `complex`
- `bool`
- `str`
- `tuple`
- `frozenset`
- `bytes`

Example:

```python
name = "Python"

name = name + " Developer"

print(name)
```

The original string is not modified. The expression creates a new string object, and the variable is reassigned.

### Mutable Data Types

Mutable objects can be modified after creation.

Examples:

- `list`
- `dict`
- `set`
- `bytearray`

Example:

```python
numbers = [10, 20, 30]

numbers.append(40)

print(numbers)
```

Output:

```text
[10, 20, 30, 40]
```

The existing list object is modified.

This distinction is important when passing objects between functions and sharing data across application components.

---

## 12. Practical Example: Customer Information

Let's combine multiple data types in one program.

```python
customer_name = "Arun"
customer_id = 101
account_balance = 25000.75
is_verified = True
last_login = None

print("Customer Name:", customer_name)
print("Customer ID:", customer_id)
print("Account Balance:", account_balance)
print("Verified:", is_verified)
print("Last Login:", last_login)
```

Data type summary:

| Variable | Data Type |
|---|---|
| `customer_name` | `str` |
| `customer_id` | `int` |
| `account_balance` | `float` |
| `is_verified` | `bool` |
| `last_login` | `NoneType` |

---

## 13. FDE Connection: Data Types in Customer Integrations

As a Forward-Deployed Engineer, you will frequently receive data from external APIs, databases, and customer systems.

One important responsibility is understanding and validating the data types.

Consider this API-like customer response:

```python
customer = {
    "id": 101,
    "name": "Arun",
    "balance": 25000.75,
    "is_verified": True,
    "email": None
}

print(type(customer["id"]))
print(type(customer["name"]))
print(type(customer["balance"]))
print(type(customer["is_verified"]))
print(type(customer["email"]))
```

Why does this matter?

Imagine a customer API sends the following:

```python
customer_age = "25"
```

But your application expects an integer.

You may need to validate and convert the value:

```python
customer_age = "25"

try:
    customer_age = int(customer_age)
    print("Valid age:", customer_age)
except ValueError:
    print("Invalid age received from API")
```

Real-world FDE responsibilities include:

1. Validating incoming customer data.
2. Handling inconsistent data formats.
3. Converting data into expected types.
4. Handling missing values.
5. Debugging integration failures.

---

## 14. Practice Tasks

### Beginner Level

**Task 1:** Create variables using `int`, `float`, `str`, and `bool`.

**Task 2:** Print the data type of each variable using `type()`.

**Task 3:** Create a complex number and print its real and imaginary parts.

**Task 4:** Create a variable containing `None` and check its type.

### Intermediate Level

**Task 5:** Convert the string `"100"` into an integer.

**Task 6:** Convert the integer `250` into a string.

**Task 7:** Check whether a value is an integer using `isinstance()`.

**Task 8:** Demonstrate the difference between mutable and immutable objects.

### FDE-Oriented Practice

**Task 9:** Create a customer dictionary containing:

- Customer ID
- Customer name
- Account balance
- Verification status
- Email address

**Task 10:** Receive an age as a string and safely convert it into an integer.

**Task 11:** Handle a missing customer email using `None`.

---

## 15. Quick Revision

| Concept | Meaning |
|---|---|
| `int` | Whole numbers |
| `float` | Floating-point numbers |
| `complex` | Real and imaginary numbers |
| `bool` | True or False |
| `str` | Text data |
| `NoneType` | Absence of a value |
| `type()` | Identifies an object's type |
| `isinstance()` | Checks whether an object belongs to a type or class |
| Type Casting | Converts values between compatible types |
| Mutable | Object contents can be modified |
| Immutable | Object contents cannot be modified |

---

## 16. Self-Assessment

Try answering these questions without referring to the notes.

1. What is a data type?
2. What are the fundamental Python data types?
3. What is the difference between `int` and `float`?
4. What is a complex number?
5. What are Boolean values?
6. Why are strings immutable?
7. What is the purpose of `None`?
8. What is the difference between `type()` and `isinstance()`?
9. What is type casting?
10. What happens when we convert `"Python"` into an integer?
11. What is the difference between mutable and immutable objects?
12. Why can floating-point calculations produce unexpected decimal results?
13. Why is data type validation important when integrating external APIs?
14. What is the difference between `None`, `False`, and `0`?

---


