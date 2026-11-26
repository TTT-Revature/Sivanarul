# Python Assertions and Testing Exceptions

---

## 1. The `assert` Statement in Tests

The `assert` statement checks whether a condition is true. If it fails, it raises `AssertionError`.

```python
def get_grade(score):
    if score >= 90:
        return "A"
    elif score >= 80:
        return "B"
    elif score >= 70:
        return "C"
    else:
        return "F"

# Direct assertions
assert get_grade(95) == "A"
assert get_grade(85) == "B"
assert get_grade(50) == "F"
print("All assertions passed!")
```

**Output:**

```text
All assertions passed!
```

### Assert with Custom Message

```python
result = get_grade(75)
assert result == "C", f"Expected 'C', got '{result}'"
```

---

## 2. unittest Assertion Methods

`unittest` provides rich assertion methods with better error messages than plain `assert`:

```python
import unittest

class TestGrading(unittest.TestCase):

    def test_grade_a(self):
        self.assertEqual(get_grade(95), "A")

    def test_grade_b(self):
        self.assertEqual(get_grade(85), "B")

    def test_failing_grade(self):
        self.assertEqual(get_grade(50), "F")

    def test_boundary_a(self):
        self.assertEqual(get_grade(90), "A")

    def test_boundary_b(self):
        self.assertEqual(get_grade(80), "B")
```

### Comparison of `assert` vs `unittest` Assertions

| Feature | `assert` | `unittest` Methods |
|---|---|---|
| Error message | Generic `AssertionError` | Detailed diff (e.g., `'B' != 'A'`) |
| Test runner | Manual | Integrated with test discovery |
| Test counting | None | Reports pass/fail counts |
| Recommended for | Quick checks, scripts | Formal test suites |

---

## 3. Testing That Exceptions Are Raised

### Using `assertRaises`

```python
import unittest

def withdraw(balance, amount):
    if amount <= 0:
        raise ValueError("Amount must be positive")
    if amount > balance:
        raise ValueError("Insufficient funds")
    return balance - amount


class TestWithdraw(unittest.TestCase):

    def test_negative_amount(self):
        with self.assertRaises(ValueError):
            withdraw(100, -50)

    def test_overdraw(self):
        with self.assertRaises(ValueError):
            withdraw(100, 200)

    def test_valid_withdrawal(self):
        self.assertEqual(withdraw(100, 30), 70)
```

### Checking the Exception Message

```python
class TestWithdrawMessages(unittest.TestCase):

    def test_negative_amount_message(self):
        with self.assertRaises(ValueError) as context:
            withdraw(100, -50)
        self.assertEqual(str(context.exception), "Amount must be positive")

    def test_overdraw_message(self):
        with self.assertRaises(ValueError) as context:
            withdraw(100, 200)
        self.assertEqual(str(context.exception), "Insufficient funds")
```

---

## 4. Testing with `assertWarns`

```python
import warnings

def deprecated_function():
    warnings.warn("This function is deprecated", DeprecationWarning)
    return 42


class TestDeprecation(unittest.TestCase):

    def test_deprecation_warning(self):
        with self.assertWarns(DeprecationWarning):
            result = deprecated_function()
        self.assertEqual(result, 42)
```

---

## 5. Assertion Methods Summary

| Method | Checks |
|---|---|
| `assertEqual(a, b)` | `a == b` |
| `assertNotEqual(a, b)` | `a != b` |
| `assertTrue(x)` | `bool(x) is True` |
| `assertFalse(x)` | `bool(x) is False` |
| `assertIs(a, b)` | `a is b` (same object) |
| `assertIsNone(x)` | `x is None` |
| `assertIn(a, b)` | `a in b` |
| `assertRaises(Exc)` | Code raises `Exc` |
| `assertWarns(Warn)` | Code raises warning `Warn` |
| `assertAlmostEqual(a, b)` | `round(a-b, 7) == 0` |
| `assertGreater(a, b)` | `a > b` |
| `assertRegex(s, r)` | `re.search(r, s)` |

---

## 6. Best Practices

1. **Test both valid and invalid inputs** — always verify that errors are raised for bad data.
2. **Check exception messages** when the message is part of the contract.
3. **Test boundary values**: 0, negative, empty strings, None.
4. **Use `unittest` assertions** over plain `assert` in test files for better error reports.
5. **One assertion concept per test method** — each test should verify one behavior.
