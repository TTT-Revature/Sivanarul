
# Python Type Conversion

## 1. Introduction

Type conversion is the process of converting a value from one data type into another data type.

In Python, we work with different data types such as:

- `int`
- `float`
- `str`
- `bool`
- `list`
- `tuple`
- `set`
- `dict`

Sometimes, we need to convert one data type into another to perform calculations, process user input, validate data, or communicate with APIs.

### Real-World Example

Imagine an application receives a customer's age from a form.

The user enters:

```python
age = "25"
```

Here, `age` is a string, not an integer.

If we want to perform mathematical operations, we need to convert it into an integer.

```python
age = "25"

age = int(age)

print(age + 5)
```

Output:

```text
30
```

---

## 2. Types of Type Conversion

Python supports two major types of conversion:

1. Implicit Type Conversion
2. Explicit Type Conversion

## 3. Implicit Type Conversion

Implicit type conversion happens automatically by Python.

Python converts one data type into another when it is appropriate for an operation.

### Example 1: Integer to Float

```python
a = 10
b = 5.5

result = a + b

print(result)
print(type(result))
```

Output:

```text
15.5
<class 'float'>
```

### Explanation

- `a` is an integer.
- `b` is a float.
- Python automatically converts the integer into a float for the calculation.
- The result is a float.

Conceptually:

```text
10 (int) + 5.5 (float)
          |
          v
       10.0 + 5.5
          |
          v
        15.5
```

### Example 2: Integer to Complex

```python
a = 10
b = 5 + 2j

result = a + b

print(result)
print(type(result))
```

Output:

```text
(15+2j)
<class 'complex'>
```

### Important Note

Python does not automatically convert every data type.

For example:

```python
age = 25
name = "Sivan"

print(age + name)
```

Output:

```text
TypeError
```

Python cannot directly add an integer and a string.

We must explicitly convert one of the values if that is what the operation requires.

---

## 4. Explicit Type Conversion

Explicit type conversion means converting a value from one data type to another manually.

Python provides built-in functions for this purpose.

Common conversion functions:

| Function | Purpose |
|---|---|
| `int()` | Converts a compatible value into an integer |
| `float()` | Converts a compatible value into a float |
| `str()` | Converts a value into a string |
| `bool()` | Converts a value into a Boolean |
| `list()` | Converts an iterable into a list |
| `tuple()` | Converts an iterable into a tuple |
| `set()` | Converts an iterable into a set |
| `dict()` | Creates a dictionary from compatible key-value pairs |
| `complex()` | Converts a compatible value into a complex number |

## 5. Converting Values Using int()

The `int()` function converts compatible values into integers.

### Example 1: Float to Integer

```python
price = 99.99

result = int(price)

print(result)
print(type(result))
```

Output:

```text
99
<class 'int'>
```

Important: `int()` truncates the fractional part. It does not round to the nearest integer.

### Example 2: String to Integer

```python
age = "25"

result = int(age)

print(result)
print(type(result))
```

Output:

```text
25
<class 'int'>
```

### Example 3: Invalid String Conversion

```python
age = "twenty five"

result = int(age)
```

Output:

```text
ValueError
```

The string does not represent a valid integer.

---

## 6. Converting Values Using float()

The `float()` function converts compatible values into floating-point numbers.

### Example 1: Integer to Float

```python
quantity = 10

result = float(quantity)

print(result)
print(type(result))
```

Output:

```text
10.0
<class 'float'>
```

### Example 2: String to Float

```python
price = "199.50"

result = float(price)

print(result)
print(type(result))
```

Output:

```text
199.5
<class 'float'>
```

### Example 3: Invalid Conversion

```python
price = "two hundred"

result = float(price)
```

Output:

```text
ValueError
```

---

## 7. Converting Values Using str()

The `str()` function converts a value into its string representation.

### Example

```python
age = 25

result = str(age)

print(result)
print(type(result))
```

Output:

```text
25
<class 'str'>
```

### Real-World Example: API Response

Imagine we want to display a customer's age inside a message.

```python
customer_age = 25

message = "Customer age is " + str(customer_age)

print(message)
```

Output:

```text
Customer age is 25
```

An alternative is using an f-string:

```python
customer_age = 25

message = f"Customer age is {customer_age}"

print(message)
```

Both approaches produce a string message.

---

## 8. Converting Values Using bool()

The `bool()` function converts a value into either `True` or `False`.

### Values That Convert to False

Common examples:

```python
print(bool(0))
print(bool(0.0))
print(bool(""))
print(bool([]))
print(bool(()))
print(bool({}))
print(bool(set()))
print(bool(None))
```

Output:

```text
False
False
False
False
False
False
False
False
```

### Values That Convert to True

```python
print(bool(10))
print(bool(-5))
print(bool("Python"))
print(bool([1, 2, 3]))
print(bool({"name": "John"}))
```

Output:

```text
True
True
True
True
True
```

### Important Concept: Truthy and Falsy Values

- Falsy values evaluate to `False` in a Boolean context.
- Truthy values evaluate to `True` in a Boolean context.

For example:

```python
username = ""

if username:
    print("Username is available")
else:
    print("Username is empty")
```

Output:

```text
Username is empty
```

This is useful when validating user input.

---

## 9. Converting Between Collection Data Types

Python also allows conversion between collection types.

### 9.1 List to Tuple

```python
numbers = [10, 20, 30]

result = tuple(numbers)

print(result)
print(type(result))
```

Output:

```text
(10, 20, 30)
<class 'tuple'>
```

### 9.2 Tuple to List

```python
numbers = (10, 20, 30)

result = list(numbers)

print(result)
print(type(result))
```

Output:

```text
[10, 20, 30]
<class 'list'>
```

### 9.3 List to Set

```python
numbers = [10, 20, 20, 30, 30]

result = set(numbers)

print(result)
print(type(result))
```

Possible output:

```text
{10, 20, 30}
<class 'set'>
```

Important: Sets remove duplicate values, but they do not guarantee the original sequence order.

### 9.4 String to List

```python
name = "Python"

result = list(name)

print(result)
```

Output:

```text
['P', 'y', 't', 'h', 'o', 'n']
```

### 9.5 String to Tuple

```python
name = "Python"

result = tuple(name)

print(result)
```

Output:

```text
('P', 'y', 't', 'h', 'o', 'n')
```

### 9.6 List of Key-Value Pairs to Dictionary

```python
data = [
    ("name", "John"),
    ("age", 25),
    ("city", "Chennai")
]

result = dict(data)

print(result)
```

Output:

```text
{'name': 'John', 'age': 25, 'city': 'Chennai'}
```

The input must contain compatible key-value pairs.

---

## 10. Important Difference: Type Conversion vs Type Casting

These terms are often used interchangeably in Python discussions.

| Type | Meaning |
|---|---|
| Implicit conversion | Python automatically converts a value during an operation |
| Explicit conversion | The developer manually requests conversion using functions such as `int()` or `str()` |

Example:

```python
# Implicit conversion

a = 10
b = 2.5

result = a + b

print(result)  # 12.5


# Explicit conversion

age = "25"

age = int(age)

print(age + 5)  # 30
```

---

## 11. Common Type Conversion Errors

### Error 1: Converting Invalid Strings

```python
number = "hello"

result = int(number)
```

Error:

```text
ValueError
```

Reason: `"hello"` is not a valid integer representation.

### Error 2: Adding String and Integer

```python
age = 25

result = "Age: " + age
```

Error:

```text
TypeError
```

Solution:

```python
age = 25

result = "Age: " + str(age)

print(result)
```

### Error 3: Converting None to Integer

```python
value = None

result = int(value)
```

Error:

```text
TypeError
```

Reason: `None` does not represent a valid integer.

### Error 4: Converting a Float to Integer and Expecting Rounding

```python
price = 99.99

print(int(price))
```

Output:

```text
99
```

If rounding is required, use:

```python
price = 99.99

print(round(price))
```

Output:

```text
100
```

Note: Python's `round()` uses round-half-to-even for exact halfway cases.

---

## 12. Safe Type Conversion Using try-except

In real-world applications, user input may not always contain valid data.

We can handle conversion errors using exception handling.

### Example

```python
user_input = input("Enter your age: ")

try:
    age = int(user_input)
    print("Your age is:", age)

except ValueError:
    print("Please enter a valid integer.")
```

Example input:

```text
Enter your age: 25
```

Output:

```text
Your age is: 25
```

Invalid input:

```text
Enter your age: twenty
```

Output:

```text
Please enter a valid integer.
```

Important: `input()` always returns a string. Even if the user enters `25`, Python initially receives `"25"`.

---

## 13. Practical Example: Customer Registration

Imagine we are building a customer registration application.

The application receives customer information through input fields.

```python
customer_name = input("Enter customer name: ")
customer_age = input("Enter customer age: ")
customer_balance = input("Enter account balance: ")

try:
    customer_age = int(customer_age)
    customer_balance = float(customer_balance)

    print("Customer Details")
    print("Name:", customer_name)
    print("Age:", customer_age)
    print("Balance:", customer_balance)

except ValueError:
    print("Invalid age or account balance.")
```

### Why Is Type Conversion Important Here?

- Customer name should remain a string.
- Age may need to be converted into an integer.
- Account balance may need to be converted into a numeric type.
- Invalid input should be handled safely.

In production applications, conversion is only one part of validation. We must also check business rules, such as whether an age or balance is within an acceptable range.

---

## 14. Type Conversion in Forward-Deployed Engineering

Type conversion is important when integrating different systems.

An FDE may work with:

- REST APIs
- Databases
- CSV and Excel files
- JSON data
- Third-party applications
- AI/LLM responses

Different systems may represent the same information using different data types.

### Example: Processing API Data

Suppose an API returns:

```python
api_response = {
    "customer_id": "101",
    "customer_name": "John",
    "account_balance": "25000.50",
    "is_active": "true"
}
```

Notice that the values are strings.

We may need to convert them before using them in our application.

```python
customer_id = int(api_response["customer_id"])

account_balance = float(
    api_response["account_balance"]
)

is_active = api_response["is_active"].lower() == "true"

print(customer_id)
print(account_balance)
print(is_active)
```

Output:

```text
101
25000.5
True
```

Important: Converting a string to a Boolean using `bool()` does not interpret the words `"true"` and `"false"`.

For example:

```python
print(bool("false"))
```

Output:

```text
True
```

This happens because every non-empty string is truthy.

Therefore, when processing textual Boolean values, we need explicit parsing logic.

For production systems, validate allowed values and handle missing or unexpected data rather than assuming every API response is correct.

---

## 15. Quick Revision

| Concept | Example | Result |
|---|---|---|
| Integer to float | `float(10)` | `10.0` |
| Float to integer | `int(10.8)` | `10` |
| String to integer | `int("25")` | `25` |
| Integer to string | `str(25)` | `"25"` |
| String to float | `float("10.5")` | `10.5` |
| Integer to Boolean | `bool(0)` | `False` |
| List to tuple | `tuple([1, 2])` | `(1, 2)` |
| Tuple to list | `list((1, 2))` | `[1, 2]` |
| List to set | `set([1, 1, 2])` | `{1, 2}` |

---

## 16. Practice Exercises

Try solving these exercises without looking at the answers.

### Exercise 1: Integer Conversion

Convert the following string into an integer.

```python
number = "150"

# Write your code here
```

Expected output:

```text
150
<class 'int'>
```

### Exercise 2: Float Conversion

Convert the following integer into a float.

```python
price = 250

# Write your code here
```

Expected output:

```text
250.0
```

### Exercise 3: String Conversion

Convert the following integer into a string.

```python
employee_id = 101
```

Expected output:

```text
101
<class 'str'>
```

### Exercise 4: List Conversion

Convert the following tuple into a list.

```python
languages = ("Python", "Java", "JavaScript")
```

Expected output:

```text
['Python', 'Java', 'JavaScript']
```

### Exercise 5: Remove Duplicates

Convert the following list into a set.

```python
numbers = [10, 20, 20, 30, 30, 40]
```

Expected result: A set containing `10`, `20`, `30`, and `40`.

### Exercise 6: Handle Invalid Input

Write a program that:

1. Accepts a number from the user.
2. Converts it into an integer.
3. Prints the square of the number.
4. Handles invalid input using `try-except`.

### Exercise 7: API Data Conversion

Consider this dictionary:

```python
employee = {
    "id": "501",
    "salary": "45000.75",
    "experience": "4"
}
```

Convert:

- `id` into an integer.
- `salary` into a float.
- `experience` into an integer.

Print the converted values and their data types.

---

## 17. Self-Assessment Questions

1. What is type conversion in Python?
2. What is the difference between implicit and explicit conversion?
3. Why does Python automatically convert an integer into a float during certain arithmetic operations?
4. What happens when we execute `int("Python")`?
5. What is the difference between `int(10.9)` and `round(10.9)`?
6. What does `bool("")` return?
7. Why does `bool("False")` return `True`?
8. What does the `input()` function return by default?
9. How do we handle invalid type conversion?
10. Why is type conversion important when processing API responses?

---

## 18. Key Takeaways

- Type conversion changes a value from one data type to another.
- Implicit conversion is performed automatically by Python.
- Explicit conversion is requested manually by the developer.
- Python provides functions such as `int()`, `float()`, `str()`, `bool()`, `list()`, `tuple()`, and `set()`.
- Invalid conversions can raise `ValueError` or `TypeError`.
- Use `try-except` when conversion may fail.
- Always validate external data before using it in business logic.
- Type conversion is an important skill when integrating APIs, databases, files, and AI systems.

---


