# PEP 8 and Python Naming Conventions

---

## 1. What is PEP 8?

**PEP 8** is Python's official style guide. It defines conventions for writing clean, readable, and consistent Python code. Following PEP 8 ensures your code is easy to read by any Python developer.

---

## 2. Naming Conventions

| Element | Convention | Example |
|---|---|---|
| **Variables** | `snake_case` | `user_name`, `total_price` |
| **Functions** | `snake_case` | `calculate_tax()`, `get_user()` |
| **Constants** | `UPPER_SNAKE_CASE` | `MAX_RETRIES`, `API_KEY` |
| **Classes** | `PascalCase` | `UserAccount`, `HttpResponse` |
| **Modules** | `snake_case` | `data_utils.py`, `file_handler.py` |
| **Packages** | `lowercase` (no underscores) | `mypackage`, `utilities` |
| **Private** | `_single_leading_underscore` | `_internal_cache`, `_helper()` |
| **Name mangling** | `__double_leading_underscore` | `__secret_key` |
| **Magic methods** | `__double_both__` | `__init__`, `__str__` |

### Examples

```python
# Variables
user_age = 25
total_items = 100

# Constants
MAX_CONNECTIONS = 50
DEFAULT_TIMEOUT = 30

# Functions
def calculate_discount(price, percent):
    return price * (1 - percent / 100)

# Classes
class ShoppingCart:
    def __init__(self):
        self._items = []        # Private attribute

    def add_item(self, item):
        self._items.append(item)
```

---

## 3. Code Layout Rules

### Indentation: 4 Spaces (Never Tabs)

```python
# Correct
def greet(name):
    if name:
        print(f"Hello, {name}!")

# Wrong - using tabs or 2 spaces
def greet(name):
  if name:
    print(f"Hello, {name}!")
```

### Maximum Line Length: 79 Characters

```python
# Break long lines with parentheses
result = (first_variable
          + second_variable
          - third_variable)

# Break long function calls
user = create_user(
    username="sivanarul",
    email="siva@example.com",
    role="developer",
)
```

### Blank Lines

```python
import os
import sys
                            # 2 blank lines before top-level definitions

class User:
    def __init__(self, name):
        self.name = name
                            # 1 blank line between methods
    def greet(self):
        return f"Hi, {self.name}"
                            # 2 blank lines before next top-level definition

def helper_function():
    pass
```

---

## 4. Import Conventions

```python
# Standard library imports first
import os
import sys

# Third-party imports second
import requests
import flask

# Local imports last
from myproject.utils import format_output
from myproject.models import User
```

**Avoid wildcard imports:**

```python
# Bad - pollutes namespace, unclear what is imported
from os import *

# Good - explicit
from os import path, getcwd
```

---

## 5. Whitespace Rules

```python
# Around operators
x = 5 + 3              # Good
x=5+3                  # Bad

# No space inside brackets
my_list = [1, 2, 3]    # Good
my_list = [ 1, 2, 3 ]  # Bad

# No space before colon in slices
items[1:3]              # Good
items[1 : 3]            # Bad

# No space before function call parenthesis
print("hello")          # Good
print ("hello")         # Bad

# Space after comma
func(a, b, c)           # Good
func(a,b,c)             # Bad
```

---

## 6. Quick Reference Table

| Rule | Good | Bad |
|---|---|---|
| Indentation | 4 spaces | Tabs or 2 spaces |
| Line length | 79 chars or less | 200+ char lines |
| Variable names | `user_name` | `userName`, `UserName` |
| Class names | `ShoppingCart` | `shopping_cart`, `SHOPPINGCART` |
| Constants | `MAX_SIZE` | `max_size`, `MaxSize` |
| Imports | Grouped and sorted | `from x import *` |
| Trailing whitespace | None | Spaces at end of lines |

---

## 7. Best Practices

1. **Use a linter** like `flake8` or a formatter like `black` to enforce PEP 8 automatically.
2. **Configure your IDE** to show PEP 8 warnings in real time.
3. **Consistency matters more than perfection** — follow the existing style in a project.
4. **Read PEP 8:** `https://peps.python.org/pep-0008/`
