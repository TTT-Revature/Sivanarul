# Python Iterable vs Iterator

---

## 1. Introduction

In Python, understanding the difference between an **iterable** and an **iterator** is central to how loops, comprehensions, and generators work.

| Concept | Definition | Magic Method | Examples |
|---|---|---|---|
| **Iterable** | An object that can return its members one at a time. | Implements `__iter__()` | `list`, `tuple`, `str`, `dict`, `set` |
| **Iterator** | An object representing a stream of data that produces values on demand. | Implements `__iter__()` and `__next__()` | generator, file handle, `enumerate`, `zip` |

---

## 2. What is an Iterable?

An iterable is any object capable of returning an iterator when passed to `iter()`. It has stored all its elements in memory or knows how to produce them.

```python
numbers = [10, 20, 30]

# Checking for iterable capability
print(hasattr(numbers, "__iter__"))  # True
print(hasattr(numbers, "__next__"))  # False (Lists are NOT iterators!)
```

**Output:**

```text
True
False
```

---

## 3. What is an Iterator?

An iterator is the stateful helper object that actually advances through the sequence. It remembers its current position and produces the next element via `__next__()`.

```python
numbers = [10, 20, 30]

# Get an iterator from the iterable
num_iter = iter(numbers)

print(hasattr(num_iter, "__iter__"))  # True
print(hasattr(num_iter, "__next__"))  # True (It is an iterator!)
```

**Output:**

```text
True
True
```

---

## 4. Key Differences

```python
nums = [1, 2, 3]

# 1. Iterables can be iterated over multiple times
for x in nums: pass
for x in nums: pass  # Works fine

# 2. Iterators are exhausted after one full traversal
it = iter(nums)
print(list(it))  # [1, 2, 3]
print(list(it))  # [] (Exhausted!)
```

**Output:**

```text
[1, 2, 3]
[]
```

---

## 5. Summary

- **Iterable:** A container holding data (e.g. a book).
- **Iterator:** A bookmark keeping track of the current page and moving forward one page at a time.
