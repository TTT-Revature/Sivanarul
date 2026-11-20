# Readable Code and Function Design

---

## 1. Introduction

Code is read far more often than it is written. Writing **readable code** means choosing clear names, keeping functions short, and structuring logic so that any developer can understand it quickly.

---

## 2. Clear Naming

### Variables

```python
# Bad - What does 'd' mean?
d = 86400

# Good - Self-documenting
seconds_per_day = 86400
```

### Functions

```python
# Bad - Vague
def process(data):
    ...

# Good - Describes the action
def calculate_monthly_revenue(transactions):
    ...
```

### Booleans

```python
# Bad
flag = True

# Good - Reads like English
is_active = True
has_permission = False
can_edit = True
```

---

## 3. Function Design Principles

### Single Responsibility

Each function should do **one thing** and do it well.

```python
# Bad - Does too many things
def handle_order(order):
    validate(order)
    total = sum(item.price for item in order.items)
    tax = total * 0.08
    send_email(order.customer, total + tax)
    save_to_database(order)
    return total + tax

# Good - Each function has one job
def calculate_total(items):
    return sum(item.price for item in items)

def calculate_tax(total, rate=0.08):
    return total * rate

def process_order(order):
    total = calculate_total(order.items)
    tax = calculate_tax(total)
    return total + tax
```

### Keep Functions Short

A good rule of thumb: **a function should fit on one screen** (roughly 20-30 lines). If it is longer, break it into smaller helper functions.

### Limit Parameters

```python
# Bad - Too many parameters
def create_user(name, email, age, role, dept, mgr, start):
    ...

# Good - Use a dataclass or dictionary
from dataclasses import dataclass

@dataclass
class UserInfo:
    name: str
    email: str
    age: int
    role: str = "employee"

def create_user(user_info: UserInfo):
    ...
```

---

## 4. Early Returns (Guard Clauses)

Reduce nesting by handling edge cases first:

```python
# Bad - Deep nesting
def get_discount(customer):
    if customer is not None:
        if customer.is_member:
            if customer.years > 5:
                return 0.20
            else:
                return 0.10
        else:
            return 0.0
    else:
        return 0.0

# Good - Early returns
def get_discount(customer):
    if customer is None:
        return 0.0
    if not customer.is_member:
        return 0.0
    if customer.years > 5:
        return 0.20
    return 0.10
```

---

## 5. Comments and Docstrings

### When to Comment

```python
# Bad - States the obvious
x = x + 1  # Increment x by 1

# Good - Explains WHY
x = x + 1  # Compensate for 0-based index in display
```

### Docstrings

```python
def calculate_bmi(weight_kg: float, height_m: float) -> float:
    """Calculate Body Mass Index.

    Args:
        weight_kg: Weight in kilograms.
        height_m: Height in meters.

    Returns:
        BMI value as a float.

    Raises:
        ValueError: If height is zero or negative.
    """
    if height_m <= 0:
        raise ValueError("Height must be positive")
    return weight_kg / (height_m ** 2)
```

---

## 6. Code Readability Checklist

| Principle | Question |
|---|---|
| **Naming** | Can I understand the variable/function without context? |
| **Length** | Is the function under 30 lines? |
| **Parameters** | Does it take 4 or fewer parameters? |
| **Nesting** | Is the indentation depth 3 levels or less? |
| **Comments** | Do comments explain WHY, not WHAT? |
| **DRY** | Is there duplicated logic I can extract? |

---

## 7. Best Practices

1. **Write code for humans first**, the computer second.
2. **Use descriptive names** even if they are longer — clarity beats brevity.
3. **One function, one job.** If you need "and" to describe it, split it.
4. **Return early** to avoid deep nesting.
5. **Write docstrings** for all public functions and classes.
