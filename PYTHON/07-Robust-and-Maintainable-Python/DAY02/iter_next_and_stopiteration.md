# Python iter(), next(), and StopIteration

---

## 1. The Iterator Protocol

The **Iterator Protocol** in Python is defined by two fundamental functions:

1. `iter(iterable)`: Invokes `iterable.__iter__()` and returns an iterator object.
2. `next(iterator)`: Invokes `iterator.__next__()` and returns the next item in the sequence.
3. `StopIteration`: The exception raised by `next()` when no further elements remain.

---

## 2. Using `iter()` and `next()`

```python
colors = ["red", "green", "blue"]

# Convert list to iterator
color_iterator = iter(colors)

# Retrieve items one by one
print(next(color_iterator))  # red
print(next(color_iterator))  # green
print(next(color_iterator))  # blue

# Next call raises StopIteration
try:
    print(next(color_iterator))
except StopIteration:
    print("Iteration finished: No more elements left!")
```

**Output:**

```text
red
green
blue
Iteration finished: No more elements left!
```

---

## 3. How a `for` Loop Works Under the Hood

A Python `for` loop is simply syntactic sugar over `iter()`, `next()`, and `StopIteration`:

```python
items = ["Python", "Java", "C++"]

# What "for item in items:" actually does:
iterator = iter(items)
while True:
    try:
        item = next(iterator)
        print("Processing:", item)
    except StopIteration:
        break
```

**Output:**

```text
Processing: Python
Processing: Java
Processing: C++
```

---

## 4. `next()` with a Default Fallback

To prevent raising `StopIteration`, provide a second argument to `next()` as a fallback:

```python
numbers = [1, 2]
it = iter(numbers)

print(next(it, "END"))  # 1
print(next(it, "END"))  # 2
print(next(it, "END"))  # END (Safe fallback, no exception raised!)
```

**Output:**

```text
1
2
END
```

---

## 5. Creating a Custom Iterator Class

```python
class CountDown:
    def __init__(self, start):
        self.current = start

    def __iter__(self):
        return self

    def __next__(self):
        if self.current <= 0:
            raise StopIteration
        val = self.current
        self.current -= 1
        return val

for count in CountDown(3):
    print(count)
```

**Output:**

```text
3
2
1
```
