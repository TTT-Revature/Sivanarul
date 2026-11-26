# Reading Tracebacks and Debugging in Python

---

## 1. What is a Traceback?

A **traceback** (stack trace) is Python's detailed diagnostic report generated when an unhandled exception halts execution. It details the call hierarchy leading up to the exact line where the error occurred.

---

## 2. Anatomy of a Traceback

Tracebacks are read from **top to bottom**:

- **Top:** The earliest function or file called (entry point).
- **Middle:** Intermediate function calls that navigated into other modules.
- **Bottom:** The exact line that triggered the crash, followed by the **Error Type** and **Error Message**.

```python
def process_order(item, quantity):
    validate_quantity(quantity)

def validate_quantity(qty):
    if qty <= 0:
        raise ValueError("Order quantity must be positive")

# Calling with invalid quantity
process_order("Laptop", -1)
```

**Traceback Output:**

```text
Traceback (most recent call last):
  File "app.py", line 9, in <module>
    process_order("Laptop", -1)
  File "app.py", line 2, in process_order
    validate_quantity(quantity)
  File "app.py", line 6, in validate_quantity
    raise ValueError("Order quantity must be positive")
ValueError: Order quantity must be positive
```

---

## 3. Common Python Errors

| Exception Type | Common Cause |
|---|---|
| `SyntaxError` | Invalid Python grammar (missing colon, unmatched parenthesis). |
| `TypeError` | Operation applied to incompatible type (e.g., `'str' + 5`). |
| `ValueError` | Correct type, but invalid value (e.g., `int('abc')`). |
| `KeyError` | Looking up a non-existent key in a dictionary. |
| `IndexError` | Sequence index out of bounds. |
| `AttributeError` | Calling a method or attribute that does not exist on the object. |
| `NameError` | Referencing a variable before it is defined. |

---

## 4. Debugging Steps

1. Always read the **bottom line first** to identify the exception type and explanation.
2. Check the **file name and line number** directly above the bottom line.
3. Inspect variable values leading up to the failing line using logging or interactive debuggers.
