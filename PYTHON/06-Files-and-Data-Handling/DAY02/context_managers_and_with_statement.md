
# 46. Context Managers and `with` Statement in Python

**Suggested filename:** `46_context_managers_and_with_statement.md`

## 1. Introduction

In Python, some operations require us to acquire and release resources.

Examples:
- Opening a file and closing it.
- Connecting to a database and closing the connection.
- Acquiring a thread lock and releasing it.
- Opening a network connection and cleaning it up.

Consider this example:

```python
file = open("data.txt", "r")

content = file.read()

file.close()
```

There is a potential problem.

What happens if an exception occurs before `file.close()` executes?

The file might remain open longer than necessary.

Python provides **context managers** to manage resources safely.

The `with` statement is the most common way to use a context manager.

---

## 2. What Is a Context Manager?

A context manager is an object that manages the setup and cleanup of a resource.

It defines two important methods:

| Method | Purpose |
|---|---|
| `__enter__()` | Performs setup and returns the object to use inside the block |
| `__exit__()` | Performs cleanup when the block exits |

The context manager ensures that cleanup logic is executed when the `with` block finishes, including when an exception occurs.

### Real-world analogy

Imagine borrowing a book from a library.

1. You register and receive the book.
2. You use the book.
3. You return the book.

The library manages the borrowing and returning process.

Similarly, a context manager manages resource acquisition and cleanup.

---

## 3. Understanding the `with` Statement

The `with` statement is used to execute a block of code within a managed context.

### Syntax

```python
with expression as variable:
    # Operations inside the context
```

Example:

```python
with open("data.txt", "r") as file:
    content = file.read()
    print(content)
```

What happens internally?

1. Python evaluates the context manager expression.
2. Python calls its `__enter__()` method.
3. The returned value is assigned to `file`.
4. The statements inside the `with` block execute.
5. Python calls `__exit__()` when the block exits.

For a file object, this process ensures the file is closed.

---

## 4. Without `with` vs With `with`

### Without the `with` statement

```python
file = open("data.txt", "r")

try:
    content = file.read()
    print(content)

finally:
    file.close()
```

Here, `finally` ensures that the file is closed even if an exception occurs during the operation.

### With the `with` statement

```python
with open("data.txt", "r") as file:
    content = file.read()
    print(content)
```

The context manager handles cleanup automatically.

### Comparison

| Without `with` | With `with` |
|---|---|
| Manual resource cleanup | Automatic cleanup |
| Often requires `try-finally` | Cleanup is built into the context manager |
| More code | Less code |
| Easier to forget cleanup | Safer resource management |

**Important:** The `with` statement does not automatically handle every possible error. It manages the resource lifecycle. You may still need `try-except` to handle errors meaningfully.

---

## 5. Understanding `__enter__()` and `__exit__()`

These are special methods used by the context management protocol.

### `__enter__()`

- Executes when entering the `with` block.
- Performs setup.
- Returns an object that can be assigned using `as`.

### `__exit__()`

- Executes when leaving the `with` block.
- Performs cleanup.
- Receives information about an exception, if one occurred.

The method signature is:

```python
def __exit__(self, exc_type, exc_value, traceback):
    pass
```

Parameters:

| Parameter | Meaning |
|---|---|
| `exc_type` | Exception class, if an exception occurred |
| `exc_value` | Exception instance |
| `traceback` | Traceback object |

If no exception occurs, all three values are `None`.

---

## 6. Creating a Custom Context Manager Using a Class

Python allows us to create our own context managers.

Example:

```python
class MyContextManager:

    def __enter__(self):
        print("Entering the context")
        return self

    def __exit__(self, exc_type, exc_value, traceback):
        print("Exiting the context")


with MyContextManager() as obj:
    print("Inside the with block")
```

Output:

```text
Entering the context
Inside the with block
Exiting the context
```

### Understanding the execution

1. `MyContextManager()` creates an object.
2. `__enter__()` executes.
3. The returned object is assigned to `obj`.
4. The block executes.
5. `__exit__()` executes.

Notice that `__enter__()` returns `self`.

This allows us to access the context manager object through `obj`.

---

## 7. Understanding Exception Handling in `__exit__()`

Let's intentionally create an exception inside a context manager.

```python
class MyContextManager:

    def __enter__(self):
        print("Entering context")
        return self

    def __exit__(self, exc_type, exc_value, traceback):

        print("Exiting context")

        if exc_type:
            print("Exception type:", exc_type.__name__)
            print("Exception message:", exc_value)

        return False


with MyContextManager():
    print("Inside context")
    result = 10 / 0
```

Output:

```text
Entering context
Inside context
Exiting context
Exception type: ZeroDivisionError
Exception message: division by zero
Traceback (most recent call last):
...
ZeroDivisionError: division by zero
```

The important point:

- `__exit__()` executes even though an exception occurred.
- It receives information about the exception.
- Returning `False` means the exception is not suppressed.
- The exception continues propagating.

### What if `__exit__()` returns `True`?

```python
class MyContextManager:

    def __enter__(self):
        print("Entering context")
        return self

    def __exit__(self, exc_type, exc_value, traceback):
        print("Exiting context")
        return True


with MyContextManager():
    print("Inside context")
    result = 10 / 0

print("Program continues")
```

Output:

```text
Entering context
Inside context
Exiting context
Program continues
```

The exception was suppressed.

**Important:** Returning `True` suppresses the exception. Use this carefully because suppressing unexpected errors can hide bugs.

---

## 8. Creating Context Managers Using `contextlib`

Python provides a standard-library module called `contextlib`.

It allows us to create context managers without writing a class.

One useful function is `@contextmanager`.

### Example

```python
from contextlib import contextmanager

@contextmanager
def my_context():

    print("Entering context")

    try:
        yield
    finally:
        print("Exiting context")


with my_context():
    print("Inside context")
```

Output:

```text
Entering context
Inside context
Exiting context
```

### Understanding `yield`

The `yield` statement separates the setup and cleanup sections.

Execution:

1. Code before `yield` executes.
2. Control moves into the `with` block.
3. The `with` block executes.
4. Code after `yield` executes when the block exits.

The `finally` block ensures cleanup even if the block raises an exception.

**Important:** A generator-based context manager created using `@contextmanager` must yield exactly once during normal use.

---

## 9. Passing Values Through a Context Manager

A context manager can return a value using `yield`.

Example:

```python
from contextlib import contextmanager

@contextmanager
def employee_context(name):

    print("Opening employee session")

    try:
        yield name
    finally:
        print("Closing employee session")


with employee_context("Arun") as employee:
    print("Employee:", employee)
```

Output:

```text
Opening employee session
Employee: Arun
Closing employee session
```

Here:

- `"Arun"` is passed to the context manager.
- `yield name` provides the value to the `as employee` variable.
- The `finally` block performs cleanup.

---

## 10. Multiple Context Managers

Python allows us to manage multiple resources using one `with` statement.

Example:

```python
with open("input.txt", "r") as source, open("output.txt", "w") as destination:

    content = source.read()

    destination.write(content)
```

This:
- Opens the input file.
- Opens the output file.
- Reads the input.
- Writes the content into the output.
- Closes both files automatically.

### Using parentheses for readability

```python
with (
    open("input.txt", "r") as source,
    open("output.txt", "w") as destination
):
    content = source.read()
    destination.write(content)
```

Parenthesized multiple context managers are supported in Python 3.10 and later.

---

## 11. Nested Context Managers

Context managers can also be nested.

Example:

```python
with open("input.txt", "r") as source:

    with open("output.txt", "w") as destination:

        content = source.read()

        destination.write(content)
```

The inner context exits before the outer context.

Both files are closed automatically.

For simple resource management, multiple context managers in one `with` statement are often more concise.

---

## 12. Context Managers and Exception Safety

Consider a database connection.

A typical workflow:

1. Open a database connection.
2. Execute queries.
3. Commit or roll back a transaction as appropriate.
4. Close the connection.

A context manager can help manage the resource lifecycle.

However, an important distinction exists:

**Not every context manager automatically commits or rolls back a database transaction.**

The exact behavior depends on the database library and its connection context manager.

For example, Python's built-in SQLite connection context manager handles transaction commit or rollback, but it does not automatically close the connection.

This is why understanding the behavior of the specific library matters.

---

## 13. Common Context Managers in Python

Python provides context managers for many operations.

| Context manager | Purpose |
|---|---|
| `open()` | Manage file operations |
| `threading.Lock()` | Manage thread locks |
| `decimal.localcontext()` | Manage decimal calculation settings |
| `contextlib.suppress()` | Suppress specified exceptions |
| `contextlib.redirect_stdout()` | Redirect standard output |
| `contextlib.ExitStack()` | Manage a dynamic collection of context managers |

### Example: Suppressing a specific exception

```python
from contextlib import suppress

with suppress(FileNotFoundError):
    with open("missing.txt", "r") as file:
        print(file.read())

print("Program continues")
```

Output:

```text
Program continues
```

Here, only `FileNotFoundError` is suppressed.

Other exceptions are not automatically suppressed.

---

## 14. Practical Example – File Management System

Let's create a custom context manager that manages a file.

```python
class FileManager:

    def __init__(self, filename, mode):
        self.filename = filename
        self.mode = mode
        self.file = None

    def __enter__(self):
        print("Opening file")

        self.file = open(
            self.filename,
            self.mode,
            encoding="utf-8"
        )

        return self.file

    def __exit__(self, exc_type, exc_value, traceback):
        print("Closing file")

        if self.file is not None:
            self.file.close()

        return False


with FileManager("employee.txt", "w") as file:
    file.write("Employee: Arun\n")
    file.write("Department: Python")
```

Output:

```text
Opening file
Closing file
```

The file is closed automatically when the context exits.

This example demonstrates how a class can implement the context management protocol.

In real applications, prefer Python's built-in `open()` context manager unless you need additional behavior.

---

## 15. FDE Connection – Why Context Managers Matter

Forward-Deployed Engineers work with external systems and resources.

Context managers help ensure that resources are released correctly.

### Scenario 1: File processing

A customer provides a large log file.

```python
with open("application.log", "r", encoding="utf-8") as file:

    for line in file:
        if "ERROR" in line:
            print(line.strip())
```

The file is automatically closed.

### Scenario 2: Database operations

A database library may provide a context manager for transactions or connections.

```python
import sqlite3

connection = sqlite3.connect("company.db")

try:
    with connection:
        connection.execute(
            "INSERT INTO employees (name) VALUES (?)",
            ("Arun",)
        )
finally:
    connection.close()
```

Here:
- The connection context manager manages transaction behavior.
- `finally` ensures the connection is closed.
- Parameterized SQL helps avoid SQL injection.

### Scenario 3: Thread synchronization

When multiple threads access shared data, locks can protect critical sections.

```python
import threading

lock = threading.Lock()

with lock:
    print("Accessing shared resource")
```

The lock is automatically released when the block exits.

### Scenario 4: External API resources

Some HTTP client libraries provide context managers for sessions or responses.

They help release network resources when the operation finishes.

**FDE takeaway:** Context managers are not just a file-handling feature. They are a general resource-management mechanism used in production applications.

---

## 16. Common Mistakes

| Mistake | Explanation |
|---|---|
| Forgetting `__enter__()` | A class will not support the standard context manager protocol |
| Forgetting `__exit__()` | Cleanup behavior is not implemented |
| Not returning from `__enter__()` | The `as` variable receives `None` |
| Returning `True` unnecessarily | Unexpected exceptions may be suppressed |
| Forgetting `finally` with `@contextmanager` | Cleanup may not execute as intended |
| Yielding multiple times | Invalid for a single-use generator context manager |
| Assuming every context manager closes resources | Cleanup behavior depends on its implementation |
| Assuming `with` prevents all errors | It manages entry and exit, not all application errors |

---

## 17. Practice Exercises

### Beginner Level

**Exercise 1:** Open a text file using `with open()` and print its contents.

**Exercise 2:** Write three lines into a file using the `with` statement.

**Exercise 3:** Explain the difference between `__enter__()` and `__exit__()`.

### Intermediate Level

**Exercise 4:** Create a class-based context manager that prints:

```text
Starting
Inside
Finished
```

**Exercise 5:** Modify your context manager to detect whether an exception occurred.

**Exercise 6:** Create a generator-based context manager using `@contextmanager`.

### Advanced Level

**Exercise 7:** Create a custom file manager class that opens and closes a file automatically.

**Exercise 8:** Use two context managers in one `with` statement to copy content from one file to another.

**Exercise 9:** Use `contextlib.suppress()` to handle a missing file without stopping the program.

**Exercise 10 – FDE Scenario:**

You are developing an application that processes customer files.

Create a custom context manager that:

1. Prints a message when file processing starts.
2. Opens the customer file.
3. Allows the main program to process its contents.
4. Closes the file automatically.
5. Prints a completion message even if an exception occurs.

---

## 18. Quick Revision

| Concept | Purpose |
|---|---|
| Context Manager | Manages resource setup and cleanup |
| `with` | Executes code inside a managed context |
| `__enter__()` | Setup operation |
| `__exit__()` | Cleanup operation |
| `exc_type` | Exception class |
| `exc_value` | Exception instance |
| `traceback` | Exception traceback |
| `@contextmanager` | Creates a context manager from a generator |
| `yield` | Separates setup and cleanup |
| `contextlib` | Standard-library context manager utilities |
| `suppress()` | Suppresses specified exceptions |
| `ExitStack` | Manages multiple dynamic contexts |

---

## 19. Self-Assessment

1. What is a context manager?
2. Why do we use the `with` statement?
3. What happens when Python enters a `with` block?
4. What is the purpose of `__enter__()`?
5. What is the purpose of `__exit__()`?
6. What happens if an exception occurs inside a `with` block?
7. What is the difference between returning `True` and `False` from `__exit__()`?
8. What does `@contextmanager` do?
9. Why is `yield` used in generator-based context managers?
10. Can we use multiple context managers in one `with` statement?

---

## 20. Learning Outcome

After completing this chapter, you should be able to:

- Understand context managers.
- Use the `with` statement.
- Explain the context management protocol.
- Implement `__enter__()` and `__exit__()`.
- Build class-based context managers.
- Build generator-based context managers.
- Handle exceptions during resource management.
- Use context managers with files, database connections, and locks.


