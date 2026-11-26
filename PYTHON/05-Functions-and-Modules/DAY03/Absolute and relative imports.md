# Python Absolute and Relative Imports

---

## 1. Introduction

When working with multi-module Python projects, you need to import code from one module into another. Python supports two import styles:

- **Absolute Imports:** Specify the full path from the project root to the target module.
- **Relative Imports:** Specify the path relative to the current module's position using dots (`.`).

---

## 2. Absolute Imports

An absolute import uses the complete package path starting from the project's top-level package.

### Project Structure:

```text
ecommerce/
├── __init__.py
├── main.py
├── orders/
│   ├── __init__.py
│   ├── processor.py
│   └── validator.py
└── payments/
    ├── __init__.py
    └── gateway.py
```

### Example: Importing from `main.py`

```python
# main.py
from ecommerce.orders.processor import process_order
from ecommerce.payments.gateway import charge_card

process_order("ORD-001")
charge_card(120.50)
```

### Example: Importing within a subpackage (`orders/processor.py`)

```python
# orders/processor.py
from ecommerce.orders.validator import validate_order
from ecommerce.payments.gateway import charge_card

def process_order(order_id):
    validate_order(order_id)
    charge_card(99.99)
    print(f"Order {order_id} processed.")
```

### Advantages of Absolute Imports:
- **Clear and explicit:** Any developer reading the code immediately knows the module's full location.
- **PEP 8 recommended:** The official Python style guide recommends absolute imports.
- **Refactoring-safe:** Moving a file does not silently break deep relative references.

---

## 3. Relative Imports

A relative import specifies the target module relative to the current module's location using dot notation:

- `.` (single dot): Current package (same directory).
- `..` (double dot): Parent package (one level up).
- `...` (triple dot): Grandparent package (two levels up).

### Example: Inside `orders/processor.py`

```python
# orders/processor.py
from .validator import validate_order       # Same package (orders/)
from ..payments.gateway import charge_card  # Parent package, then into payments/

def process_order(order_id):
    validate_order(order_id)
    charge_card(99.99)
    print(f"Order {order_id} processed.")
```

### Advantages of Relative Imports:
- **Concise:** Shorter import statements when modules are in the same or nearby packages.
- **Self-contained packages:** Useful for reusable library packages that may be installed under different names.

### Limitations:
- **Cannot be used in top-level scripts:** Running `python orders/processor.py` directly will fail with `ImportError: attempted relative import with no known parent package`.
- **Harder to read** for deeply nested structures.

---

## 4. Comparison Table

| Feature | Absolute Import | Relative Import |
|---|---|---|
| **Syntax** | `from package.module import name` | `from .module import name` |
| **Readability** | Very clear and explicit | Shorter but can be confusing |
| **PEP 8 Recommendation** | Preferred | Acceptable for internal package use |
| **Works in scripts?** | Yes | No (requires package context) |
| **Refactoring impact** | Must update if package is renamed | Automatically adapts to parent renames |

---

## 5. Best Practices

1. **Default to absolute imports** for application-level code and when collaborating with teams.
2. **Use relative imports** sparingly, primarily within tightly coupled internal subpackages of a reusable library.
3. **Never mix** both styles inconsistently within the same module.
4. **Avoid circular imports** regardless of style: if module A imports module B and module B imports module A, Python raises `ImportError`.
