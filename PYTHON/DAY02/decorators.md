# Python Decorators

---

## 1. Introduction to Decorators

A **decorator** is a design pattern in Python that allows you to dynamically modify or extend the behavior of a function without altering its actual source code.

Decorators wrap another function, leveraging closures and the `@decorator_name` syntax.

---

## 2. Anatomy of a Decorator

```python
def my_decorator(func):
    def wrapper():
        print("1. Action before function execution")
        func()
        print("2. Action after function execution")
    return wrapper

@my_decorator
def say_hello():
    print("   Hello, World!")

say_hello()
```

**Output:**

```text
1. Action before function execution
   Hello, World!
2. Action after function execution
```

---

## 3. Decorating Functions with Arguments (`*args`, `**kwargs`)

To create a decorator that works on any function regardless of its parameters, accept `*args` and `**kwargs` in the wrapper:

```python
import functools

def log_execution(func):
    @functools.wraps(func)  # Preserves function metadata (__name__, __doc__)
    def wrapper(*args, **kwargs):
        print(f"Calling '{func.__name__}' with args={args}, kwargs={kwargs}")
        result = func(*args, **kwargs)
        print(f"'{func.__name__}' returned: {result}")
        return result
    return wrapper

@log_execution
def add(a, b):
    return a + b

add(10, 25)
```

**Output:**

```text
Calling 'add' with args=(10, 25), kwargs={}
'add' returned: 35
```

---

## 4. Practical Real-World Example: Performance Timer

```python
import time
import functools

def execution_timer(func):
    @functools.wraps(func)
    def wrapper(*args, **kwargs):
        start = time.perf_counter()
        result = func(*args, **kwargs)
        duration = time.perf_counter() - start
        print(f"Function '{func.__name__}' executed in {duration:.6f}s")
        return result
    return wrapper

@execution_timer
def process_data(n):
    return sum(i * 2 for i in range(n))

process_data(100_000)
```

**Output:**

```text
Function 'process_data' executed in 0.008412s
```

---

## 5. Summary

- Use `@functools.wraps` to preserve function identity.
- Common uses: Logging, caching, authentication, input validation, and rate limiting.
