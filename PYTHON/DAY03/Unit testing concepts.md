# Python Unit Testing Concepts

---

## 1. Introduction

**Unit testing** is the practice of testing individual, isolated pieces of code (units) — typically functions or methods — to verify they produce the expected output for a given input.

### Real-World Analogy

Before assembling a car, each component (engine, brakes, lights) is tested individually. If a brake pad fails during component testing, you fix it before it reaches the assembly line.

---

## 2. Why Write Unit Tests?

| Benefit | Explanation |
|---|---|
| **Catch bugs early** | Detect issues before they reach production |
| **Enable refactoring** | Change code confidently — tests confirm nothing is broken |
| **Document behavior** | Tests describe what the code is supposed to do |
| **Save time** | Automated tests run in seconds vs. manual testing |
| **Improve design** | Writing testable code leads to cleaner, modular design |

---

## 3. What Makes a Good Unit Test?

### The AAA Pattern: Arrange, Act, Assert

```python
def calculate_discount(price, discount_percent):
    """Return the discounted price."""
    if discount_percent < 0 or discount_percent > 100:
        raise ValueError("Discount must be between 0 and 100")
    return price * (1 - discount_percent / 100)


def test_calculate_discount():
    # Arrange: Set up test data
    price = 200.0
    discount = 25

    # Act: Call the function being tested
    result = calculate_discount(price, discount)

    # Assert: Verify the result
    assert result == 150.0
```

---

## 4. Test Categories

| Test Type | Scope | Speed | Example |
|---|---|---|---|
| **Unit Test** | Single function/method | Very fast | Test `calculate_discount()` |
| **Integration Test** | Multiple modules together | Moderate | Test API + database interaction |
| **End-to-End Test** | Entire application flow | Slow | Test user login to dashboard |

The **testing pyramid** recommends: many unit tests, fewer integration tests, fewest E2E tests.

---

## 5. Key Terminology

| Term | Meaning |
|---|---|
| **Test case** | A single scenario being tested |
| **Test suite** | A collection of related test cases |
| **Test runner** | Tool that executes tests and reports results |
| **Fixture** | Setup/teardown code that prepares the test environment |
| **Assertion** | A statement that checks if a condition is true |
| **Mock** | A fake object that replaces a real dependency during testing |
| **Code coverage** | Percentage of code executed by tests |

---

## 6. What to Test and What Not to Test

### Do Test:
- Business logic and calculations
- Edge cases (empty input, zero, negative numbers, boundaries)
- Error handling (invalid input raises correct exceptions)
- Return values and side effects

### Don't Test:
- Python built-in functions (`len()`, `sorted()`)
- Third-party library internals
- Simple getters/setters with no logic
- Private implementation details (test behavior, not internals)

---

## 7. Best Practices

1. **Each test should test one thing.** One assertion per logical concept.
2. **Tests must be independent.** Test A must not depend on Test B running first.
3. **Use descriptive test names:** `test_discount_raises_error_for_negative_percent`.
4. **Run tests frequently** — ideally on every save or commit.
5. **Aim for meaningful coverage**, not 100%. Focus on critical business logic.
