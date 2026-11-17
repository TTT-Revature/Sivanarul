
# Python: Creating and Importing Modules

**Suggested filename:** `43_creating_and_importing_modules.md`

## 1. Introduction

Until now, we have written most of our Python programs in a single file.

For example:

```python
def add(a, b):
    return a + b


def subtract(a, b):
    return a - b


def multiply(a, b):
    return a * b


print(add(10, 20))
print(subtract(20, 10))
print(multiply(5, 4))
```

As an application grows, keeping every function in one file becomes difficult.

Imagine developing an application with:

- User authentication
- Database operations
- Payment processing
- API integrations
- Data processing

Instead of writing everything in one file, we can divide our code into separate files.

Python provides **modules** to organize reusable code.

## 2. What Is a Module?

A module is a Python file containing reusable code.

A module can contain:

- Functions
- Variables
- Classes
- Statements
- Other Python definitions

A Python module normally has the `.py` extension.

For example:

```text
calculator.py
```

The file `calculator.py` is a Python module.

We can import this module into another Python file and reuse its functionality.

## 3. Creating Your First Module

Let's create a simple Python project.

### Project structure

```text
python_project/
│
├── calculator.py
│
└── main.py
```

We have two files:

- `calculator.py` – Contains reusable functions.
- `main.py` – Imports and uses those functions.

### Step 1: Create calculator.py

```python
def add(a, b):
    return a + b


def subtract(a, b):
    return a - b


def multiply(a, b):
    return a * b
```

This file contains three functions.

### Step 2: Create main.py

```python
import calculator

print(calculator.add(10, 20))
print(calculator.subtract(20, 10))
print(calculator.multiply(5, 4))
```

### Output

```text
30
10
20
```

### Understanding the execution

1. Python encounters `import calculator`.
2. Python locates and loads the `calculator` module.
3. The functions defined in that module become accessible through the module name.
4. We call those functions using `calculator.function_name()`.

**Important:** The two files should be in the same directory for this simple example to work without additional path configuration.

## 4. Understanding the import Statement

The `import` statement allows us to access code defined in another module.

### Syntax

```python
import module_name
```

### Example

```python
import math

print(math.sqrt(25))
print(math.pi)
```

**Output:**

```text
5.0
3.141592653589793
```

Explanation:

- `math` is a built-in Python standard-library module.
- `sqrt()` calculates the square root.
- `pi` provides the mathematical constant π.

We access module members using the dot (`.`) operator.

```python
module_name.member_name
```

For example:

```python
math.sqrt(25)
```

Here:
- `math` is the module.
- `sqrt` is a function inside the module.

## 5. Importing Specific Functions

Sometimes we don't want to import the entire module name into our code.

We can import specific functions or variables.

### Syntax

```python
from module_name import function_name
```

### Example

```python
from math import sqrt

print(sqrt(25))
```

**Output:**

```text
5.0
```

Notice that we can call `sqrt()` directly instead of writing `math.sqrt()`.

### Importing Multiple Functions

```python
from math import sqrt, pow, factorial

print(sqrt(64))
print(pow(2, 3))
print(factorial(5))
```

**Output:**

```text
8.0
8.0
120
```

## 6. Importing Everything Using `*`

Python allows us to import all names that a module exposes for star imports.

### Syntax

```python
from module_name import *
```

### Example

```python
from math import *

print(sqrt(25))
print(factorial(5))
```

**Output:**

```text
5.0
120
```

However, this approach is generally discouraged in professional applications.

Why?

- It becomes difficult to identify where a function came from.
- It can cause naming conflicts.
- It reduces code readability.
- It may import more names than necessary.

**Best practice:** Import the module or explicitly import the names you need.

## 7. Importing Modules with Aliases

Python allows us to give a module or imported function a shorter alternative name.

This is called an alias.

### Syntax

```python
import module_name as alias_name
```

### Example 1: Module alias

```python
import math as m

print(m.sqrt(100))
print(m.pi)
```

**Output:**

```text
10.0
3.141592653589793
```

Here, `m` is an alias for `math`.

### Example 2: Function alias

```python
from math import factorial as fact

print(fact(5))
```

**Output:**

```text
120
```

Aliases are commonly used with libraries.

For example:

```python
import pandas as pd
import numpy as np
```

These are widely recognized conventions in Python development.

## 8. Creating a Reusable Module

Let's build a more practical example.

### Project structure

```text
employee_project/
│
├── employee.py
│
└── main.py
```

### employee.py

```python
def calculate_salary(basic_salary, bonus):
    return basic_salary + bonus


def calculate_experience(joining_year, current_year):
    return current_year - joining_year


company_name = "ABC Technologies"
```

### main.py

```python
import employee

salary = employee.calculate_salary(40000, 5000)

experience = employee.calculate_experience(2022, 2026)

print("Company:", employee.company_name)
print("Salary:", salary)
print("Experience:", experience, "years")
```

**Output:**

```text
Company: ABC Technologies
Salary: 45000
Experience: 4 years
```

Notice that we reuse functions and variables from another file without rewriting them.

This is one of the main purposes of modules.

## 9. Understanding `__name__` and `__main__`

This is an important Python concept.

Every Python module has a special variable called:

```python
__name__
```

Its value depends on how the module is being executed.

There are two important cases.

### Case 1: Running a file directly

When Python runs a file directly as the main program, its `__name__` value is:

```python
"__main__"
```

Example:

```python
print(__name__)
```

If you run this file directly:

```text
__main__
```

### Case 2: Importing a module

When another Python file imports that module, its `__name__` is normally set to the module's import name.

Example:

**calculator.py**

```python
print(__name__)
```

**main.py**

```python
import calculator
```

When you run `main.py`, the output is:

```text
calculator
```

This happens because `calculator.py` is being imported as a module rather than executed as the main program.

### Why do we use `if __name__ == "__main__"`?

It allows us to write code that should run only when the file is executed directly, not when it is imported.

Example:

**calculator.py**

```python
def add(a, b):
    return a + b


def subtract(a, b):
    return a - b


if __name__ == "__main__":
    print("Calculator module is running directly")

    print(add(10, 20))
```

**main.py**

```python
import calculator

print(calculator.add(5, 5))
```

When running `calculator.py` directly:

```text
Calculator module is running directly
30
```

When running `main.py`:

```text
10
```

The code inside the `if __name__ == "__main__"` block does not execute during the import.

**Important:** Python still executes other top-level statements when importing a module. The `if __name__ == "__main__"` condition is a way to protect code that should only run during direct execution.

## 10. Understanding Python's Module Search Path

When we import a module, how does Python find its file?

Python searches for modules using its module search path.

The search locations include:

1. The directory containing the input script, or the current directory in relevant interactive environments.
2. Locations configured through `PYTHONPATH`.
3. Standard-library module locations.
4. Installed third-party package locations, usually within `site-packages`.

The actual search path is available through `sys.path`.

### Example

```python
import sys

for path in sys.path:
    print(path)
```

**Output:**

The exact paths depend on your Python installation and environment.

Example:

```text
C:\Python\Python313\python313.zip
C:\Python\Python313\DLLs
C:\Python\Python313\Lib
C:\Python\Python313\Lib\site-packages
```

Your paths may be different.

### Important

If Python cannot locate a requested module, it raises:

```text
ModuleNotFoundError
```

Example:

```python
import unknown_module
```

This produces an error similar to:

```text
ModuleNotFoundError: No module named 'unknown_module'
```

## 11. Understanding Built-in, Standard Library, and Third-Party Modules

Python modules can come from different sources.

### A. Built-in modules

These are provided as part of the Python interpreter.

Examples:

```python
import sys
import builtins
```

### B. Standard-library modules

These are included with Python and provide commonly needed functionality.

Examples:

```python
import math
import os
import json
import datetime
import random
import pathlib
```

You generally do not need to install these separately.

### C. Third-party modules

These are created and distributed by external developers or organizations.

Examples:

```python
import pandas
import numpy
import requests
import fastapi
```

You generally install them using `pip`.

For example:

```bash
pip install requests
```

Then use the package:

```python
import requests
```

**Note:** A package can contain multiple modules. The distinction between a module and a package is covered in the next chapter.

## 12. Understanding Import Errors

### Example 1: ModuleNotFoundError

```python
import unknown_module
```

Error:

```text
ModuleNotFoundError: No module named 'unknown_module'
```

Possible reasons:

- Module does not exist.
- Module is not installed.
- Python cannot find its location.
- Module name is incorrect.

### Example 2: ImportError

```python
from math import unknown_function
```

Error:

```text
ImportError: cannot import name 'unknown_function' from 'math'
```

This happens because the module exists, but the requested name cannot be imported from it.

### Difference

| Error | Meaning |
|---|---|
| `ModuleNotFoundError` | Python cannot find the requested module |
| `ImportError` | An import operation failed, such as requesting a name that does not exist |

`ModuleNotFoundError` is a subclass of `ImportError`.

## 13. Common Mistakes

### Mistake 1: Forgetting the module name

Incorrect:

```python
import math

print(sqrt(25))
```

This raises `NameError` because `sqrt` was not imported directly.

Correct:

```python
import math

print(math.sqrt(25))
```

Alternatively:

```python
from math import sqrt

print(sqrt(25))
```

### Mistake 2: Incorrect file name

Suppose your file is named:

```text
calculator.py
```

But you write:

```python
import calculations
```

Python will not find your module unless a module with that name exists in its search path.

### Mistake 3: Naming your file after a standard-library module

Avoid naming your own files:

```text
math.py
random.py
json.py
```

These names can shadow standard-library modules and cause confusing import errors.

Choose meaningful names such as:

```text
employee_utils.py
payment_service.py
data_processor.py
```

### Mistake 4: Executing unnecessary code during import

Consider:

```python
print("Connecting to database...")

def get_data():
    return [10, 20, 30]
```

When another file imports this module, the print statement executes.

Keep module-level code limited and avoid performing unnecessary operations during import.

Use a main guard for code that should run only when the file is executed directly.

## 14. Practical Example: Separating an Application into Modules

Let's organize a small employee application.

### Project structure

```text
employee_app/
│
├── main.py
│
├── salary.py
│
└── employee.py
```

### salary.py

```python
def calculate_salary(basic, bonus):
    return basic + bonus


def calculate_tax(salary):
    return salary * 0.10
```

### employee.py

```python
def get_employee_details():
    return {
        "id": 101,
        "name": "Arun",
        "department": "AI"
    }
```

### main.py

```python
import salary
import employee


details = employee.get_employee_details()

total_salary = salary.calculate_salary(40000, 5000)

tax = salary.calculate_tax(total_salary)

print("Employee:", details["name"])
print("Department:", details["department"])
print("Total Salary:", total_salary)
print("Tax:", tax)
```

**Output:**

```text
Employee: Arun
Department: AI
Total Salary: 45000
Tax: 4500.0
```

### What did we achieve?

Instead of putting everything in one file:

- `salary.py` handles salary calculations.
- `employee.py` handles employee information.
- `main.py` coordinates the application.

This makes the application easier to maintain and extend.

## 15. FDE Connection

As a Forward-Deployed Engineer, you may build applications that integrate multiple systems.

For example, an application might need:

- Customer management.
- Authentication.
- External API connections.
- Database operations.
- AI model integration.
- Data transformation.

You can separate these responsibilities into modules.

Example architecture:

```text
customer_app/
│
├── main.py
│
├── authentication.py
│
├── customer_service.py
│
├── database.py
│
├── api_client.py
│
└── ai_service.py
```

Each module has a specific responsibility.

For example:

- `authentication.py` handles authentication-related functions.
- `customer_service.py` handles customer operations.
- `database.py` manages database-related functionality.
- `api_client.py` handles external API communication.
- `ai_service.py` handles AI-related functionality.

This is a simple illustration of separation of responsibilities.

**Key engineering principle:** Organize code by responsibility rather than putting every function into one large file.

---

## 16. Practice Exercises

### Exercise 1: Create a calculator module

Create two files:

```text
project/
│
├── calculator.py
└── main.py
```

In `calculator.py`, create:

- `add()`
- `subtract()`
- `multiply()`
- `divide()`

Import the module into `main.py` and call all four functions.

### Exercise 2: Import specific functions

Create a module called `operations.py`.

Define:

```python
def square(number):
    return number * number


def cube(number):
    return number ** 3
```

Import only `square()` into another Python file.

### Exercise 3: Use aliases

Import the `math` module using the alias `m`.

Calculate:

- Square root of 144.
- Factorial of 5.
- Value of pi.

### Exercise 4: Understand `__name__`

Create two files:

```text
project/
│
├── test_module.py
└── main.py
```

In `test_module.py`, write:

```python
print(__name__)
```

In `main.py`, import `test_module`.

Predict the output when:

1. You run `test_module.py` directly.
2. You run `main.py`.

### Exercise 5: Use the main guard

Create a module with:

- A function called `greet()`.
- A print statement inside `if __name__ == "__main__"`.

Import the module into another file.

Observe which statements execute.

### Exercise 6: Build a small application

Create three modules:

```text
student_app/
│
├── main.py
├── student.py
└── marks.py
```

Requirements:

- `student.py`: Return student details.
- `marks.py`: Calculate total and average marks.
- `main.py`: Import both modules and display the student report.

---

## 17. Quick Revision

| Concept | Meaning |
|---|---|
| Module | A Python file containing reusable code |
| `.py` | Python source-file extension |
| `import` | Imports a module |
| `from ... import ...` | Imports specific names |
| `as` | Creates an alias |
| `__name__` | Special variable identifying the module's execution/import name |
| `__main__` | Name used when a file is executed as the main program |
| `sys.path` | List of locations searched for modules |
| `ModuleNotFoundError` | Requested module cannot be found |
| `ImportError` | An import operation fails |
| `pip` | Common tool for installing Python packages |

## 18. Self-Assessment

Before moving to the next topic, make sure you can answer:

1. What is a Python module?
2. Why do we create modules?
3. What is the purpose of the `import` statement?
4. What is the difference between `import math` and `from math import sqrt`?
5. What is an alias in Python?
6. What is the purpose of `__name__`?
7. What does `if __name__ == "__main__"` do?
8. How does Python locate imported modules?
9. What is the difference between `ImportError` and `ModuleNotFoundError`?
10. What is the difference between a built-in module and a third-party module?

## 19. Learning Outcome

After completing this chapter, you should be able to:

- Understand Python modules.
- Create reusable Python files.
- Import complete modules.
- Import specific functions and variables.
- Use aliases.
- Understand `__name__` and `__main__`.
- Understand Python's module search path.
- Identify common import errors.
- Organize an application into separate modules.


