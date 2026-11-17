# Python Generator Functions and the yield Statement

---

## 1. Introduction to Generators

A **generator function** is a special kind of Python function that returns a lazy iterator. Instead of computing all values at once and returning them in a list with `return`, a generator uses the `yield` statement to produce values on-demand, one at a time.

### Advantages of Generators:
- **Memory Efficiency:** Values are computed lazily; does not store massive lists in RAM.
- **Infinite Streams:** Can represent infinite sequences (e.g. sensor readings, fibonacci).
- **State Retention:** Automatically pauses and resumes execution at the `yield` point.

---

## 2. The `yield` Keyword Explained

When Python encounters `yield`, it:
1. Pauses execution of the function.
2. Saves all local variable states.
3. Yields the value to the caller.
4. Resumes execution immediately after the `yield` statement on the next call to `next()`.

```python
def simple_generator():
    print("-> Starting generator")
    yield 10
    print("-> Resuming after first yield")
    yield 20
    print("-> Done")

gen = simple_generator()

print("Got:", next(gen))
print("Got:", next(gen))
```

**Output:**

```text
-> Starting generator
Got: 10
-> Resuming after first yield
Got: 20
```

---

## 3. Practical Example: Fibonacci Sequence Generator

```python
def fibonacci(limit):
    a, b = 0, 1
    count = 0
    while count < limit:
        yield a
        a, b = b, a + b
        count += 1

# Iterate cleanly with a for loop
for num in fibonacci(7):
    print(num, end=" ")
print()
```

**Output:**

```text
0 1 1 2 3 5 8 
```

---

## 4. Reading Massive Files Line-by-Line

Generators are the standard enterprise pattern for processing multi-gigabyte log files without exhausting memory:

```python
def read_large_file(filepath):
    with open(filepath, "r", encoding="utf-8") as f:
        for line in f:
            if "ERROR" in line:
                yield line.strip()

# Only error lines are yielded into memory one by one
# for err in read_large_file("server.log"): ...
```

---

## 5. Summary

| Feature | Regular Function (`return`) | Generator Function (`yield`) |
|---|---|---|
| **Return mechanism** | Returns value once, terminates | Yields values multiple times, pauses |
| **Memory usage** | Stores complete collection | Generates elements lazily ($O(1)$ memory) |
| **Object returned** | Data type of return expression | Generator object (iterator) |
