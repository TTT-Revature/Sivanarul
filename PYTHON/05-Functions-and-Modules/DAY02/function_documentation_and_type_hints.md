
# Python: Function Documentation and Type Hints

**Suggested filename:** `40_function_documentation_and_type_hints.md`

## 1. Introduction

When writing Python functions, making the code work is not enough.

Other developers should also understand:

- What does the function do?
- What arguments should be passed?
- What does the function return?
- What data types are expected?
- Are there any special conditions or limitations?

Python provides two useful features:

1. **Function documentation (docstrings):** Explains the purpose and behavior of a function.
2. **Type hints:** Communicate the expected data types of parameters and return values.

These features improve code readability, maintainability, and collaboration.

---

## 2. What Is Function Documentation?

Function documentation explains the purpose, parameters, return values, and behavior of a function.

Python uses **docstrings** for documenting functions.

A docstring is a string written as the first statement inside a function.

### Syntax

```python
def function_name():
    """Description of the function."""
    pass
```

### Example 1: Basic docstring

```python
def greet():
    """Display a welcome message."""
    print("Welcome to Python!")

greet()
```

**Output:**

```text
Welcome to Python!
```

The text inside the triple quotes is the function's docstring.

### Example 2: Accessing a docstring

Python stores a function's docstring in its `__doc__` attribute.

```python
def greet():
    """Display a welcome message."""
    print("Welcome to Python!")

print(greet.__doc__)
```

**Output:**

```text
Display a welcome message.
```

We can also use Python's built-in `help()` function.

```python
help(greet)
```

**Output (format may vary):**

```text
Help on function greet:

greet()
    Display a welcome message.
```

---

## 3. Documenting Function Parameters and Return Values

A useful docstring should explain more than just the function's name.

It should describe:

- Purpose
- Parameters
- Return value
- Important behavior

### Example

```python
def calculate_total(price, quantity):
    """
    Calculate the total price.

    Parameters:
        price: Price of one item.
        quantity: Number of items.

    Returns:
        Total price.
    """

    return price * quantity


result = calculate_total(100, 3)

print(result)
```

**Output:**

```text
300
```

### Understanding the documentation

| Section | Purpose |
|---|---|
| Description | Explains what the function does |
| Parameters | Explains the inputs |
| Returns | Explains the returned value |
| Raises | Documents exceptions that callers may need to handle |

The headings and formatting inside a docstring are conventions. Python does not require a particular documentation style.

---

## 4. Common Docstring Styles

Python developers commonly use different documentation styles.

### A. Google-style docstring

```python
def calculate_total(price, quantity):
    """
    Calculate the total price.

    Args:
        price: Price of one item.
        quantity: Number of items.

    Returns:
        The calculated total.
    """
    return price * quantity
```

### B. NumPy-style docstring

```python
def calculate_total(price, quantity):
    """
    Calculate the total price.

    Parameters
    ----------
    price : float
        Price of one item.
    quantity : int
        Number of items.

    Returns
    -------
    float
        The calculated total.
    """
    return price * quantity
```

### C. reStructuredText-style docstring

```python
def calculate_total(price, quantity):
    """
    Calculate the total price.

    :param price: Price of one item.
    :param quantity: Number of items.
    :return: The calculated total.
    """
    return price * quantity
```

**Important:** Choose one documentation style for a project and use it consistently. Google and NumPy styles are commonly seen in Python projects.

---

## 5. What Are Type Hints?

Type hints communicate the expected data types of function parameters and return values.

They help developers understand how a function should be used.

### Without type hints

```python
def add(a, b):
    return a + b
```

What types should `a` and `b` contain?

They could be integers, floats, or even strings.

The function does not communicate its intended input types.

### With type hints

```python
def add(a: int, b: int) -> int:
    return a + b
```

Explanation:

- `a: int` means `a` is expected to be an integer.
- `b: int` means `b` is expected to be an integer.
- `-> int` means the function is expected to return an integer.

### Example

```python
def multiply(a: int, b: int) -> int:
    return a * b


result = multiply(10, 5)

print(result)
```

**Output:**

```text
50
```

**Important:** Type hints do not automatically enforce types at runtime. Python still allows a caller to pass values that do not match the annotations unless additional validation is implemented.

For example:

```python
def add(a: int, b: int) -> int:
    return a + b


print(add("Hello ", "Python"))
```

**Output:**

```text
Hello Python
```

Python does not automatically reject the strings. A static type checker may report that the arguments do not match the annotations.

---

## 6. Type Hints for Different Data Types

### A. Integer

```python
def get_age(age: int) -> int:
    return age

print(get_age(25))
```

### B. String

```python
def get_name(name: str) -> str:
    return name

print(get_name("Arun"))
```

### C. Float

```python
def calculate_salary(salary: float) -> float:
    return salary

print(calculate_salary(45000.50))
```

### D. Boolean

```python
def is_active(status: bool) -> bool:
    return status

print(is_active(True))
```

### E. List

```python
def get_numbers(numbers: list[int]) -> list[int]:
    return numbers

print(get_numbers([10, 20, 30]))
```

### F. Dictionary

```python
def get_employee(employee: dict[str, int]) -> dict[str, int]:
    return employee

print(get_employee({"age": 25, "experience": 4}))
```

### G. Tuple

```python
def get_coordinates() -> tuple[int, int]:
    return (10, 20)

print(get_coordinates())
```

### H. Set

```python
def get_unique_numbers(numbers: set[int]) -> set[int]:
    return numbers

print(get_unique_numbers({10, 20, 30}))
```

**Note:** Built-in generic type syntax such as `list[int]` and `dict[str, int]` is supported from Python 3.9 onwards.

---

## 7. Type Hints for Optional Values

Sometimes a function parameter or return value can contain `None`.

Python supports the `|` union operator for this purpose.

This syntax requires Python 3.10 or later.

### Example

```python
def get_username(user_id: int) -> str | None:
    if user_id == 101:
        return "Arun"

    return None


print(get_username(101))
print(get_username(999))
```

**Output:**

```text
Arun
None
```

Explanation:

`str | None` means the function may return either:

- A string.
- `None`.

### Older syntax

For older Python versions, use `Optional` from the `typing` module.

```python
from typing import Optional

def get_username(user_id: int) -> Optional[str]:
    if user_id == 101:
        return "Arun"

    return None
```

**Remember:** `Optional[str]` means `str` or `None`. It does not automatically mean that a function argument can be omitted.

---

## 8. Type Hints for Multiple Possible Types

Sometimes a function accepts different types of input.

For example, an employee ID might be an integer or a string.

### Using the union operator

```python
def display_employee_id(employee_id: int | str) -> None:
    print(employee_id)


display_employee_id(101)
display_employee_id("EMP101")
```

**Output:**

```text
101
EMP101
```

The annotation `int | str` means either an integer or a string is expected.

### Older syntax using Union

```python
from typing import Union

def display_employee_id(employee_id: Union[int, str]) -> None:
    print(employee_id)
```

Both approaches communicate the same type alternatives.

---

## 9. Type Hints for Functions That Return Nothing

Sometimes a function performs an action but does not return a meaningful value.

Use `None` as the return annotation.

```python
def display_message(message: str) -> None:
    print(message)


display_message("Welcome to Python")
```

**Output:**

```text
Welcome to Python
```

Here:

- `message: str` expects a string.
- `-> None` indicates that the function does not return a meaningful value.

A function without an explicit `return` statement also returns `None`.

---

## 10. Combining Docstrings and Type Hints

In professional Python development, we commonly use both together.

### Example: Employee salary calculation

```python
def calculate_salary(
    basic_salary: float,
    bonus: float
) -> float:
    """
    Calculate an employee's total salary.

    Args:
        basic_salary: Employee's basic salary.
        bonus: Additional bonus amount.

    Returns:
        Total salary before deductions.
    """

    return basic_salary + bonus


salary = calculate_salary(40000.0, 5000.0)

print(salary)
```

**Output:**

```text
45000.0
```

Notice the responsibilities:

- Docstring explains what the function does.
- Type hints communicate expected data types.
- Function logic performs the calculation.

They complement each other.

---

## 11. Understanding `__annotations__`

Python stores function annotations in the `__annotations__` attribute.

### Example

```python
def calculate_total(price: float, quantity: int) -> float:
    return price * quantity


print(calculate_total.__annotations__)
```

**Output:**

```text
{'price': <class 'float'>, 'quantity': <class 'int'>, 'return': <class 'float'>}
```

This allows us to inspect the annotations at runtime.

**Important:** Annotations are metadata. Inspecting them does not automatically validate the actual arguments or return value.

---

## 12. Type Hints and Static Type Checking

If type hints do not enforce types automatically, how do developers find type-related mistakes?

They can use static type checkers.

Examples include:

- Mypy
- Pyright

### Example

```python
def calculate_total(price: int, quantity: int) -> int:
    return price * quantity


result = calculate_total("100", 3)
```

A static type checker can identify that `"100"` is a string, while the function expects an integer.

The Python interpreter itself does not automatically reject this call just because of the annotations.

### Why use static type checking?

It helps identify:

- Incorrect argument types.
- Unexpected return types.
- Incorrect function calls.
- Some possible `None` handling problems.
- Inconsistent data structures.

---

## 13. Practical Example: API Response Documentation

Imagine building a function that prepares a customer response for an API.

```python
def create_customer_response(
    customer_id: int,
    name: str,
    active: bool
) -> dict[str, int | str | bool]:
    """
    Create a customer response dictionary.

    Args:
        customer_id: Unique customer identifier.
        name: Customer's name.
        active: Whether the customer account is active.

    Returns:
        A dictionary containing customer details.
    """

    return {
        "customer_id": customer_id,
        "name": name,
        "active": active
    }


response = create_customer_response(
    101,
    "Arun",
    True
)

print(response)
```

**Output:**

```text
{
    'customer_id': 101,
    'name': 'Arun',
    'active': True
}
```

This example demonstrates how type hints and docstrings make a function easier to understand when working with API data.

**Production note:** Type hints and docstrings do not validate incoming API requests. Use appropriate runtime validation, such as Pydantic models in FastAPI, when handling untrusted external data.

---

## 14. Common Mistakes

### Mistake 1: Thinking type hints enforce data types

Incorrect assumption:

```python
def add(a: int, b: int) -> int:
    return a + b

add("Hello", "World")
```

Python does not automatically reject this call.

### Mistake 2: Writing a docstring outside the function

Incorrect:

```python
"""Calculate the total."""

def calculate_total(a, b):
    return a + b
```

This is a module-level string, not the function's docstring.

Correct:

```python
def calculate_total(a, b):
    """Calculate the total."""
    return a + b
```

### Mistake 3: Confusing `None` with no return annotation

```python
def display():
    print("Hello")
```

This function returns `None`, but it has no explicit return annotation.

```python
def display() -> None:
    print("Hello")
```

This explicitly communicates that the function returns no meaningful value.

### Mistake 4: Writing misleading documentation

If the function calculates a total but the docstring says it calculates an average, the documentation becomes misleading.

Always update documentation when function behavior changes.

---

## 15. FDE Connection

As a Forward-Deployed Engineer, you may work with:

- Customer-specific integrations.
- API request and response processing.
- Reusable Python utilities.
- AI pipelines.
- Data transformation functions.
- Shared codebases maintained by multiple developers.

Consider a reusable function:

```python
def process_customer_data(
    customer_id: int,
    records: list[dict[str, str]]
) -> dict[str, int | str]:
    """
    Process customer records and return a summary.

    Args:
        customer_id: Unique customer identifier.
        records: List of customer record dictionaries.

    Returns:
        A summary containing customer ID and record count.
    """

    return {
        "customer_id": customer_id,
        "record_count": len(records)
    }


records = [
    {"name": "Arun"},
    {"name": "Kumar"}
]

result = process_customer_data(101, records)

print(result)
```

**Output:**

```text
{'customer_id': 101, 'record_count': 2}
```

When another engineer reads this function, they can understand its purpose, expected inputs, and output without examining every line of implementation.

That is why documentation and type hints matter in collaborative engineering.

---

## 16. Practice Exercises

### Exercise 1: Basic docstring

Create a function called `greet_user()`.

- Accept a name.
- Display a welcome message.
- Add a docstring explaining its purpose.

### Exercise 2: Integer type hints

Create a function called `square()`.

- Accept an integer.
- Return its square.
- Add parameter and return type hints.

Expected:

```python
print(square(5))
```

Output:

```text
25
```

### Exercise 3: List type hints

Create a function that accepts a list of integers and returns the maximum number.

Use:

```python
list[int]
```

as the parameter annotation.

### Exercise 4: Optional return type

Create a function that searches for a user by ID.

- Accept an integer ID.
- Return a username if found.
- Return `None` if not found.
- Add the appropriate return type hint.

### Exercise 5: Complete documentation

Create a function called `calculate_discount()`.

- Accept original price and discount percentage.
- Return the discounted price.
- Add parameter and return type hints.
- Write a meaningful docstring.

---

## 17. Quick Revision

| Concept | Meaning |
|---|---|
| Docstring | Documentation written inside a function or other documented object |
| `"""..."""` | Common syntax for writing docstrings |
| `__doc__` | Attribute containing a function's docstring |
| `help()` | Displays documentation |
| `a: int` | Parameter annotation |
| `-> str` | Return annotation |
| `list[int]` | List expected to contain integers |
| `str | None` | String or None |
| `-> None` | Function returns no meaningful value |
| `__annotations__` | Stores function annotations |
| Mypy / Pyright | Static type-checking tools |

## 18. Self-Assessment

Before moving to the next topic, make sure you can answer:

1. What is a docstring?
2. Where should a function's docstring be written?
3. How do you access a function's documentation?
4. What is the purpose of type hints?
5. Does Python enforce type hints automatically?
6. What is the difference between `a: int` and `-> int`?
7. What does `list[str]` represent?
8. What does `str | None` mean?
9. What is the purpose of `-> None`?
10. What is the difference between a docstring and a type hint?

## 19. Learning Outcome

After completing this chapter, you should be able to:

- Write meaningful function docstrings.
- Document parameters and return values.
- Add type hints to function parameters.
- Add return type annotations.
- Use collection and union type hints.
- Understand the limitations of runtime type enforcement.
- Recognize how static type checkers help maintain code quality.
- Write more readable and maintainable Python functions.

**Next recommended topic:** Lambda Functions in Python.

