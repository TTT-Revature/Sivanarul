# Python Assertions (`assert`)

---

## 1. Introduction to Assertions

An **assertion** is a debugging aid that tests if a specific condition is `True`. If the condition evaluates to `False`, Python immediately raises an `AssertionError`.

Assertions are meant for **developer sanity checks** (testing internal invariables that should never be false unless there is a bug in the code).

---

## 2. Syntax

```python
assert condition, "Optional error message if condition is False"
```

---

## 3. Code Example

```python
def calculate_discount(price, discount_pct):
    # Developer sanity check: discount must never be outside 0% - 100%
    assert 0 <= discount_pct <= 1.0, f"Discount must be between 0.0 and 1.0, got {discount_pct}"
    assert price >= 0, "Price cannot be negative"
    
    return price * (1 - discount_pct)

# Valid call
print("Discounted price:", calculate_discount(100, 0.20))

# Invalid call triggering AssertionError
try:
    calculate_discount(100, 1.5)  # 150% discount!
except AssertionError as err:
    print("Assertion triggered:", err)
```

**Output:**

```text
Discounted price: 80.0
Assertion triggered: Discount must be between 0.0 and 1.0, got 1.5
```

---

## 4. When NOT to Use Assertions

> **Critical Warning:** Running Python with the `-O` (optimize) flag (`python -O app.py`) **completely disables all assertions globally**.

- **Do NOT** use `assert` for user input validation or security checks.
- **Do NOT** assert function side effects: `assert remove_user(id)` will fail silently in optimized mode!
- **Use standard `if ... raise ValueError(...)`** for regular production validations.
