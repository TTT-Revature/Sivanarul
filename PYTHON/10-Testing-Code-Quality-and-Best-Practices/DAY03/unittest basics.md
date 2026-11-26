# Python unittest Basics

---

## 1. Introduction

`unittest` is Python's built-in testing framework, included in the standard library. It provides a structured way to write, organize, and run tests using classes and assertion methods.

---

## 2. Writing Your First Test

### Code to Test (`calculator.py`)

```python
# calculator.py
def add(a, b):
    return a + b

def divide(a, b):
    if b == 0:
        raise ZeroDivisionError("Cannot divide by zero")
    return a / b
```

### Test File (`test_calculator.py`)

```python
import unittest
from calculator import add, divide

class TestCalculator(unittest.TestCase):

    def test_add_positive_numbers(self):
        self.assertEqual(add(3, 5), 8)

    def test_add_negative_numbers(self):
        self.assertEqual(add(-2, -3), -5)

    def test_add_mixed(self):
        self.assertEqual(add(-1, 5), 4)

    def test_divide_normal(self):
        self.assertEqual(divide(10, 2), 5.0)

    def test_divide_by_zero(self):
        with self.assertRaises(ZeroDivisionError):
            divide(10, 0)

if __name__ == "__main__":
    unittest.main()
```

### Running Tests

```bash
python -m unittest test_calculator.py -v
```

**Output:**

```text
test_add_mixed (__main__.TestCalculator) ... ok
test_add_negative_numbers (__main__.TestCalculator) ... ok
test_add_positive_numbers (__main__.TestCalculator) ... ok
test_divide_by_zero (__main__.TestCalculator) ... ok
test_divide_normal (__main__.TestCalculator) ... ok

----------------------------------------------------------------------
Ran 5 tests in 0.001s

OK
```

---

## 3. Common Assertion Methods

| Method | Checks |
|---|---|
| `assertEqual(a, b)` | `a == b` |
| `assertNotEqual(a, b)` | `a != b` |
| `assertTrue(x)` | `bool(x) is True` |
| `assertFalse(x)` | `bool(x) is False` |
| `assertIs(a, b)` | `a is b` |
| `assertIsNone(x)` | `x is None` |
| `assertIn(a, b)` | `a in b` |
| `assertIsInstance(a, b)` | `isinstance(a, b)` |
| `assertRaises(Error)` | Function raises the specified exception |
| `assertAlmostEqual(a, b)` | Round(a-b, 7) == 0 |

---

## 4. setUp and tearDown

Use `setUp()` and `tearDown()` to run code before and after **each** test method:

```python
import unittest

class TestUserDatabase(unittest.TestCase):

    def setUp(self):
        """Runs before EACH test method."""
        self.users = ["Alice", "Bob", "Charlie"]

    def tearDown(self):
        """Runs after EACH test method."""
        self.users.clear()

    def test_user_count(self):
        self.assertEqual(len(self.users), 3)

    def test_add_user(self):
        self.users.append("Diana")
        self.assertIn("Diana", self.users)
        self.assertEqual(len(self.users), 4)

    def test_remove_user(self):
        self.users.remove("Bob")
        self.assertNotIn("Bob", self.users)
```

---

## 5. setUpClass and tearDownClass

Use `setUpClass()` and `tearDownClass()` for expensive one-time setup (e.g., database connection):

```python
class TestWithDatabase(unittest.TestCase):

    @classmethod
    def setUpClass(cls):
        """Runs once before ALL tests in this class."""
        cls.connection = "DatabaseConnection()"
        print("Database connected")

    @classmethod
    def tearDownClass(cls):
        """Runs once after ALL tests in this class."""
        cls.connection = None
        print("Database disconnected")

    def test_query(self):
        self.assertIsNotNone(self.connection)
```

---

## 6. Running Tests

```bash
# Run all tests in a file
python -m unittest test_calculator.py

# Run with verbose output
python -m unittest test_calculator.py -v

# Run a specific test class
python -m unittest test_calculator.TestCalculator

# Run a specific test method
python -m unittest test_calculator.TestCalculator.test_add_positive_numbers

# Discover and run all tests in a directory
python -m unittest discover -s tests -p "test_*.py"
```

---

## 7. Best Practices

1. **Name test files** `test_<module>.py` and test methods `test_<behavior>`.
2. **One test class per module** being tested.
3. **Use `setUp()`** for repeated setup logic instead of duplicating code in each test.
4. **Keep tests fast** — mock external dependencies (databases, APIs).
5. **Run tests before every commit** to catch regressions early.
