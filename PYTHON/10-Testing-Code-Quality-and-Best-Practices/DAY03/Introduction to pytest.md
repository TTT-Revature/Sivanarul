# Introduction to pytest

---

## 1. What is pytest?

**pytest** is a popular third-party Python testing framework that is simpler, more powerful, and more flexible than the built-in `unittest`. It uses plain `assert` statements and automatic test discovery.

### Installation

```bash
pip install pytest
```

---

## 2. Writing Your First pytest Test

### Code to Test (`math_utils.py`)

```python
# math_utils.py
def add(a, b):
    return a + b

def is_even(n):
    return n % 2 == 0

def divide(a, b):
    if b == 0:
        raise ZeroDivisionError("Cannot divide by zero")
    return a / b
```

### Test File (`test_math_utils.py`)

```python
# test_math_utils.py
from math_utils import add, is_even, divide
import pytest

def test_add():
    assert add(2, 3) == 5

def test_add_negative():
    assert add(-1, -4) == -5

def test_is_even_true():
    assert is_even(4) is True

def test_is_even_false():
    assert is_even(7) is False

def test_divide():
    assert divide(10, 2) == 5.0

def test_divide_by_zero():
    with pytest.raises(ZeroDivisionError):
        divide(10, 0)
```

### Running Tests

```bash
pytest test_math_utils.py -v
```

**Output:**

```text
========================= test session starts =========================
test_math_utils.py::test_add PASSED
test_math_utils.py::test_add_negative PASSED
test_math_utils.py::test_is_even_true PASSED
test_math_utils.py::test_is_even_false PASSED
test_math_utils.py::test_divide PASSED
test_math_utils.py::test_divide_by_zero PASSED
========================= 6 passed in 0.02s ==========================
```

---

## 3. pytest vs unittest

| Feature | pytest | unittest |
|---|---|---|
| **Syntax** | Plain `assert` statements | `self.assertEqual()` methods |
| **Test discovery** | Automatic (finds `test_*.py`) | Requires `unittest.main()` or runner |
| **Fixtures** | `@pytest.fixture` decorator | `setUp()` / `tearDown()` methods |
| **Boilerplate** | Minimal — plain functions | Requires class inheritance |
| **Plugins** | 1000+ plugins available | Limited built-in features |
| **Installation** | `pip install pytest` | Built-in (no install needed) |

---

## 4. Fixtures

Fixtures provide reusable setup logic:

```python
import pytest

@pytest.fixture
def sample_users():
    return ["Alice", "Bob", "Charlie"]

def test_user_count(sample_users):
    assert len(sample_users) == 3

def test_contains_alice(sample_users):
    assert "Alice" in sample_users

def test_add_user(sample_users):
    sample_users.append("Diana")
    assert len(sample_users) == 4
```

---

## 5. Parametrized Tests

Run the same test with multiple inputs:

```python
import pytest
from math_utils import add

@pytest.mark.parametrize("a, b, expected", [
    (1, 2, 3),
    (-1, 1, 0),
    (0, 0, 0),
    (100, 200, 300),
])
def test_add_parametrized(a, b, expected):
    assert add(a, b) == expected
```

**Output:**

```text
test_math_utils.py::test_add_parametrized[1-2-3] PASSED
test_math_utils.py::test_add_parametrized[-1-1-0] PASSED
test_math_utils.py::test_add_parametrized[0-0-0] PASSED
test_math_utils.py::test_add_parametrized[100-200-300] PASSED
```

---

## 6. Useful pytest Commands

```bash
# Run all tests in current directory (auto-discovers test_*.py)
pytest

# Verbose output
pytest -v

# Stop on first failure
pytest -x

# Run tests matching a keyword
pytest -k "even"

# Show print() output
pytest -s

# Run tests in a specific file
pytest test_math_utils.py
```

---

## 7. Best Practices

1. **Use plain `assert`** — pytest provides detailed failure output automatically.
2. **Name test files** `test_*.py` and test functions `test_*` for auto-discovery.
3. **Use fixtures** for shared setup logic instead of duplicating code.
4. **Use `@pytest.mark.parametrize`** to test multiple inputs without writing separate functions.
5. **Install `pytest`** in every project's virtual environment.
