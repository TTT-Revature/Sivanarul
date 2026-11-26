# Python Exception Handling: try, except, else, and finally

---

## 1. Introduction to Exception Handling

An **exception** is an error that occurs during program execution (runtime) that disrupts normal flow. Python provides structured exception handling to gracefully capture errors and maintain application stability.

---

## 2. The 4 Blocks Explained

```text
try:
    # Risky code that may raise an exception
except SomeException:
    # Runs ONLY if SomeException occurred in try
else:
    # Runs ONLY if NO exceptions occurred in try
finally:
    # ALWAYS runs, regardless of whether an exception occurred
```

---

## 3. Comprehensive Code Example

```python
def safe_divide(numerator, denominator):
    print(f"\nAttempting: {numerator} / {denominator}")
    try:
        result = numerator / denominator
    except ZeroDivisionError as e:
        print(f"-> [EXCEPT] Error: Cannot divide by zero! ({e})")
        return None
    except TypeError as e:
        print(f"-> [EXCEPT] Error: Invalid operand types! ({e})")
        return None
    else:
        print(f"-> [ELSE] Division succeeded! Result = {result}")
        return result
    finally:
        print("-> [FINALLY] Cleanup execution completed.")

# Case 1: Success
safe_divide(10, 2)

# Case 2: ZeroDivisionError
safe_divide(10, 0)

# Case 3: TypeError
safe_divide(10, "two")
```

**Output:**

```text
Attempting: 10 / 2
-> [ELSE] Division succeeded! Result = 5.0
-> [FINALLY] Cleanup execution completed.

Attempting: 10 / 0
-> [EXCEPT] Error: Cannot divide by zero! (division by zero)
-> [FINALLY] Cleanup execution completed.

Attempting: 10 / two
-> [EXCEPT] Error: Invalid operand types! (unsupported operand type(s) for /: 'int' and 'str')
-> [FINALLY] Cleanup execution completed.
```

---

## 4. Best Practices

1. **Catch Specific Exceptions:** Avoid bare `except:` or `except Exception:` unless logging unknown fatal crashes.
2. **Use `finally` for Resource Cleanup:** Close database connections, sockets, and files (or prefer `with` context managers).
3. **Keep `try` Blocks Minimal:** Only enclose lines of code that are genuinely prone to raising the expected exception.
