
# Introduction to Type Hints in Python

## 1. Introduction

Python is a dynamically typed programming language.

This means we do not need to explicitly declare the data type of a variable when creating it.

Example:

```python
name = "Python"
age = 25
salary = 45000.50
```

Python identifies the data types automatically at runtime.

However, when applications become larger, understanding which data types a variable or function expects becomes important.

Consider this function:

```python
def calculate_salary(salary, bonus):
    return salary + bonus
```

Questions:

- Should `salary` be an integer or float?
- Should `bonus` be a string or number?
- What should the function return?

The function does not communicate these expectations clearly.

We can improve readability using **Type Hints**.

```python
def calculate_salary(salary: float, bonus: float) -> float:
    return salary + bonus
```

Now we can understand:

- `salary: float` means salary is expected to be a float.
- `bonus: float` means bonus is expected to be a float.
- `-> float` indicates the expected return type.

This is called type hinting.

---

## 2. What Are Type Hints?

Type hints are annotations that indicate the expected data types of variables, function parameters, and return values.

They help developers understand how data should be used in a program.

### Without Type Hints

```python
def add_numbers(a, b):
    return a + b
```

We do not know what types of values are expected.

### With Type Hints

```python
def add_numbers(a: int, b: int) -> int:
    return a + b
```

Now the expected types are clearly communicated.

### Syntax

```python
variable_name: data_type = value
```

For functions:

```python
def function_name(parameter: data_type) -> return_type:
    pass
```

---

## 3. Type Hints for Variables

We can specify the expected type of a variable.

### Example 1: Integer

```python
age: int = 25

print(age)
```

### Example 2: String

```python
name: str = "John"

print(name)
```

### Example 3: Float

```python
salary: float = 45000.50

print(salary)
```

### Example 4: Boolean

```python
is_active: bool = True

print(is_active)
```

### Example 5: None

```python
result: None = None

print(result)
```

### Important Note

Type hints do not enforce types automatically.

For example:

```python
age: int = 25

age = "Python"

print(age)
```

Output:

```text
Python
```

Python allows this assignment at runtime.

The annotation communicates the expected type, but Python does not automatically reject the assignment.

Static type checkers and compatible IDE tools can identify this kind of mismatch.

---

## 4. Type Hints for Function Parameters

Function parameters are one of the most common places to use type hints.

### Without Type Hints

```python
def greet(name):
    return "Hello " + name
```

### With Type Hints

```python
def greet(name: str):
    return "Hello " + name
```

Here:

- `name: str` indicates that the function expects a string.
- The function returns a string in this example.

### Another Example

```python
def calculate_total(price: float, quantity: int):
    return price * quantity


result = calculate_total(100.5, 3)

print(result)
```

Output:

```text
301.5
```

Type hints make the function's expected inputs easier to understand.

---

## 5. Return Type Hints

We can also specify the expected return type of a function.

### Syntax

```python
def function_name() -> return_type:
    return value
```

### Example 1: Integer Return

```python
def add(a: int, b: int) -> int:
    return a + b


result = add(10, 20)

print(result)
```

Output:

```text
30
```

### Example 2: String Return

```python
def get_username() -> str:
    return "John"


print(get_username())
```

Output:

```text
John
```

### Example 3: Boolean Return

```python
def is_adult(age: int) -> bool:
    return age >= 18


print(is_adult(25))
```

Output:

```text
True
```

### Example 4: Function That Returns Nothing

```python
def display_message() -> None:
    print("Welcome to Python")


display_message()
```

Output:

```text
Welcome to Python
```

`None` indicates that the function does not return a meaningful value.

---

## 6. Type Hints for Collection Data Types

Python collections can also be annotated.

For example:

- `list`
- `tuple`
- `set`
- `dict`

Modern Python supports built-in generic types.

### 6.1 List Type Hint

Syntax:

```python
variable: list[data_type]
```

Example:

```python
numbers: list[int] = [10, 20, 30]

print(numbers)
```

This communicates that the list is expected to contain integers.

Another example:

```python
names: list[str] = ["John", "David", "Sam"]

print(names)
```

### 6.2 Tuple Type Hint

```python
employee: tuple[str, int] = ("John", 25)

print(employee)
```

This indicates:

- First element: string
- Second element: integer

For a tuple containing any number of integers:

```python
numbers: tuple[int, ...] = (10, 20, 30, 40)
```

### 6.3 Set Type Hint

```python
unique_numbers: set[int] = {10, 20, 30}

print(unique_numbers)
```

### 6.4 Dictionary Type Hint

Syntax:

```python
variable: dict[key_type, value_type]
```

Example:

```python
employee: dict[str, int] = {
    "age": 25,
    "experience": 4
}

print(employee)
```

This communicates that:

- Dictionary keys are strings.
- Dictionary values are integers.

---

## 7. Type Hints for Multiple Data Types

Sometimes a variable or function can accept more than one data type.

For example, an employee ID may be an integer or a string.

Python provides `Union` and the modern union operator `|`.

### Example 1: Using Union

```python
from typing import Union

employee_id: Union[int, str] = 101

employee_id = "EMP101"
```

Both types are included in the annotation.

### Example 2: Using the | Operator

Python 3.10 and later support the `|` syntax.

```python
employee_id: int | str = 101

employee_id = "EMP101"
```

This is a shorter way to express the same type union.

### Function Example

```python
def display_id(employee_id: int | str) -> None:
    print(employee_id)


display_id(101)
display_id("EMP101")
```

Both calls are valid according to the annotation.

---

## 8. Optional Type Hints

Sometimes a value may be available or may be `None`.

For example, a customer may or may not have an email address.

We can represent this using `Optional`.

### Example 1: Using Optional

```python
from typing import Optional

email: Optional[str] = "john@example.com"

email = None
```

This means the value can be either:

- A string
- None

### Example 2: Using the | Operator

Python 3.10 and later:

```python
email: str | None = "john@example.com"

email = None
```

### Function Example

```python
def get_email() -> str | None:
    return None
```

This indicates that the function may return a string or `None`.

Important:

`Optional[str]` means `str | None`. It does not mean that the function parameter can simply be omitted. Default values control whether an argument can be omitted.

Example:

```python
def get_customer_email(email: str | None = None) -> str:
    if email is None:
        return "Email not provided"

    return email
```

---

## 9. Type Hints for Dictionaries and API Responses

When integrating APIs, we frequently work with JSON-like dictionary data.

Type hints can help describe the expected structure.

### Example

```python
customer: dict[str, str | int] = {
    "name": "John",
    "age": 25,
    "city": "Chennai"
}
```

This indicates:

- Keys should be strings.
- Values should be strings or integers.

However, this annotation does not enforce the presence of specific keys such as `name`, `age`, or `city`.

For more structured dictionary definitions, Python provides `TypedDict`.

### Example: TypedDict

```python
from typing import TypedDict


class Customer(TypedDict):
    name: str
    age: int
    city: str


customer: Customer = {
    "name": "John",
    "age": 25,
    "city": "Chennai"
}

print(customer)
```

This communicates the expected keys and their associated value types.

TypedDict is useful for documenting dictionary-shaped data, especially API payloads.

Important: TypedDict is a static typing feature. It does not automatically validate incoming JSON at runtime.

---

## 10. Type Hints for Functions as Values

In Python, functions are also objects.

We can pass a function as an argument to another function.

Type hints can describe the expected function signature.

Python provides `Callable` for this purpose.

### Example

```python
from typing import Callable


def execute_operation(
    operation: Callable[[int, int], int],
    a: int,
    b: int
) -> int:
    return operation(a, b)


def add(a: int, b: int) -> int:
    return a + b


result = execute_operation(add, 10, 20)

print(result)
```

Output:

```text
30
```

Explanation:

```python
Callable[[int, int], int]
```

Means:

- The callable accepts two integer arguments.
- It is expected to return an integer.

This is useful when designing callback-based systems, plugins, and reusable integrations.

---

## 11. Understanding Any

Python provides `Any` through the `typing` module.

`Any` indicates that a value can be of any type from the perspective of static type checking.

### Example

```python
from typing import Any

data: Any = 100

data = "Python"

data = [10, 20, 30]

print(data)
```

Output:

```text
[10, 20, 30]
```

### When Should We Use Any?

Consider an application that receives data from an external system.

We may not know the structure or type of the data in advance.

`Any` can be useful when the type is genuinely unknown.

However, overusing `Any` reduces the benefits of type hints.

Prefer specific types whenever possible.

---

## 12. Type Hints Do Not Perform Runtime Validation

This is one of the most important concepts.

Type hints communicate expected types, but Python does not enforce them by default.

### Example

```python
def add_numbers(a: int, b: int) -> int:
    return a + b


result = add_numbers("Hello", "Python")

print(result)
```

Output:

```text
HelloPython
```

Why?

Because Python executes the operation at runtime.

The type hints do not automatically reject string arguments.

### How Can We Check Types?

We can use `isinstance()` for runtime checks.

```python
def add_numbers(a: int, b: int) -> int:

    if not isinstance(a, int) or not isinstance(b, int):
        raise TypeError("Both values must be integers")

    return a + b


print(add_numbers(10, 20))
```

This example demonstrates runtime validation.

Important: `isinstance(True, int)` returns `True`. If Boolean values must be excluded, use an exact type check or an appropriate validation rule.

---

## 13. Static Type Checking

If type hints do not enforce types automatically, how can we identify type mismatches?

We can use static type checkers.

A static type checker analyzes source code and identifies potential type-related problems without needing to execute the application.

Popular tools include:

- Mypy
- Pyright
- IDE type analysis in Visual Studio Code and PyCharm

### Example

```python
def calculate_total(price: float, quantity: int) -> float:
    return price * quantity


result = calculate_total("100", 5)
```

The code may execute, but a static type checker can report that a string was supplied where a float was expected.

### Example Using Mypy

Install:

```bash
pip install mypy
```

Save the Python file as:

```text
example.py
```

Run:

```bash
mypy example.py
```

Mypy analyzes the code and reports type inconsistencies it can identify.

Important: Static type checkers are analysis tools. They do not automatically validate all external data or guarantee that a program is free from runtime errors.

---

## 14. Type Hints in Forward-Deployed Engineering

Type hints become particularly useful when building integrations between multiple systems.

An FDE may work with:

- FastAPI services
- REST APIs
- Databases
- Third-party SDKs
- AI model responses
- Data processing pipelines
- Shared Python modules

### Example: Customer Integration Service

Imagine we are building a service that receives customer information and calculates a purchase total.

```python
class Customer:
    def __init__(
        self,
        customer_id: int,
        name: str,
        is_active: bool
    ):
        self.customer_id = customer_id
        self.name = name
        self.is_active = is_active


def calculate_total(
    price: float,
    quantity: int
) -> float:
    return price * quantity


def get_customer_status(customer: Customer) -> str:
    if customer.is_active:
        return "Active"

    return "Inactive"


customer = Customer(
    customer_id=101,
    name="John",
    is_active=True
)

total = calculate_total(250.50, 2)

status = get_customer_status(customer)

print("Customer:", customer.name)
print("Status:", status)
print("Total:", total)
```

Output:

```text
Customer: John
Status: Active
Total: 501.0
```

### Why Are Type Hints Useful Here?

1. Other developers can understand what each function expects.
2. IDEs can provide better autocomplete and error detection.
3. Static type checkers can identify potential mismatches.
4. API integration code becomes easier to maintain.
5. Refactoring becomes safer because expected types are documented.

---

## 15. Common Mistakes

### Mistake 1: Thinking Type Hints Enforce Data Types

Incorrect assumption:

```python
age: int = "25"
```

Python does not automatically raise an error because of this annotation.

A static type checker can identify the mismatch.

### Mistake 2: Confusing Type Hints with Type Conversion

These are different concepts.

Type hint:

```python
age: int = 25
```

Type conversion:

```python
age = int("25")
```

A type hint describes an expected type.

Type conversion actually converts a value.

### Mistake 3: Overusing Any

```python
from typing import Any

def process_data(data: Any) -> Any:
    return data
```

This provides very little type information.

Prefer specific types when they are known.

### Mistake 4: Forgetting Return Type Annotations

Less descriptive:

```python
def get_age():
    return 25
```

More descriptive:

```python
def get_age() -> int:
    return 25
```

### Mistake 5: Assuming TypedDict Validates JSON

TypedDict describes the expected structure for static analysis.

It does not automatically validate incoming API responses at runtime.

Use a runtime validation tool when external data must be validated.

---

## 16. Quick Revision

| Concept | Example | Purpose |
|---|---|---|
| Variable annotation | `age: int = 25` | Describe expected variable type |
| Parameter annotation | `def greet(name: str)` | Describe expected input |
| Return annotation | `def get_age() -> int` | Describe expected return |
| List type | `list[int]` | List of integers |
| Dictionary type | `dict[str, int]` | String keys and integer values |
| Union | `int \| str` | Either integer or string |
| Optional | `str \| None` | String or None |
| Any | `Any` | Accept any type from static typing perspective |
| Callable | `Callable[[int], str]` | Describe a callable signature |
| TypedDict | `class Customer(TypedDict)` | Describe dictionary structure |
| isinstance() | `isinstance(age, int)` | Runtime class membership check |
| Mypy | `mypy example.py` | Static type checking |

---

## 17. Practice Exercises

Try solving these exercises without looking at the examples.

### Exercise 1: Variable Type Hints

Create variables with annotations for:

- Employee name
- Employee ID
- Salary
- Employment status

Use the appropriate types.

### Exercise 2: Function Parameters

Create a function called `calculate_area`.

Requirements:

- Accept length as a float.
- Accept width as a float.
- Return the calculated area as a float.

### Exercise 3: Return Type

Create a function called `get_employee_name`.

Requirements:

- Accept an employee ID as an integer.
- Return an employee name as a string.

### Exercise 4: Collection Type Hints

Create:

- A list of employee names.
- A tuple containing a name and age.
- A set of unique integer IDs.
- A dictionary containing employee names and their salaries.

Add appropriate type hints.

### Exercise 5: Union Types

Create a function that accepts an employee ID as either an integer or a string.

Use the `|` operator.

### Exercise 6: Optional Types

Create a function that accepts an email address.

Requirements:

- The email may be a string or None.
- If the email is None, return `"Email unavailable"`.
- Otherwise, return the email.

### Exercise 7: TypedDict

Create a `Product` TypedDict containing:

- product_id: integer
- product_name: string
- price: float
- is_available: Boolean

Create an object using this structure.

### Exercise 8: Runtime Validation

Create a function that accepts two integers.

Use `isinstance()` to validate the arguments before performing addition.

Remember that Boolean values are subclasses of integers. Decide whether your validation should allow them.

---

## 18. Self-Assessment Questions

1. What are type hints in Python?
2. Why does Python support type hints even though it is dynamically typed?
3. What is the difference between a type hint and type conversion?
4. How do we specify a function's return type?
5. What does `list[int]` represent?
6. What is the difference between `Union[int, str]` and `int | str`?
7. What does `Optional[str]` mean?
8. What is the purpose of `Any`?
9. Do type hints perform runtime validation?
10. What is static type checking?
11. What is the purpose of Mypy?
12. What is TypedDict used for?
13. Why are type hints useful when building API integrations?

---

## 19. Key Takeaways

- Python is dynamically typed.
- Type hints communicate expected data types.
- Variable annotations describe expected variable types.
- Function annotations describe expected parameters and return types.
- Collection types can be annotated using generic types such as `list[int]` and `dict[str, int]`.
- Union types allow multiple possible types.
- Optional types represent a value that may be None.
- TypedDict describes dictionary-shaped data.
- Callable describes function-like objects.
- Any should be used carefully.
- Type hints do not enforce types automatically at runtime.
- Mypy and Pyright can identify potential type inconsistencies through static analysis.

---

