# Python Generator Expressions

---

## 1. Introduction

A **generator expression** is a compact syntax for creating generators on-the-fly. It is structurally similar to a list comprehension, but uses **round parentheses `()`** instead of square brackets `[]`.

While list comprehensions allocate memory for the entire list immediately, generator expressions evaluate lazily, consuming minimal RAM.

---

## 2. Syntax Comparison

```python
# List Comprehension: Eager evaluation (creates entire list in RAM)
list_comp = [x ** 2 for x in range(5)]
print("List:", list_comp, type(list_comp))

# Generator Expression: Lazy evaluation (creates a generator object)
gen_exp = (x ** 2 for x in range(5))
print("Gen: ", gen_exp, type(gen_exp))
```

**Output:**

```text
List: [0, 1, 4, 9, 16] <class 'list'>
Gen:  <generator object <genexpr> at 0x...> <class 'generator'>
```

---

## 3. Consuming Generator Expressions

```python
gen = (x * 10 for x in range(1, 4))

# Using next()
print(next(gen))  # 10
print(next(gen))  # 20

# Using for loop for remainder
for item in gen:
    print("Loop:", item)
```

**Output:**

```text
10
20
Loop: 30
```

---

## 4. Memory Efficiency Demonstration

```python
import sys

# 1,000,000 items in list comprehension
list_large = [x for x in range(1_000_000)]

# 1,000,000 items in generator expression
gen_large = (x for x in range(1_000_000))

print(f"List size in RAM:      {sys.getsizeof(list_large):>10} bytes")
print(f"Generator size in RAM: {sys.getsizeof(gen_large):>10} bytes")
```

**Output:**

```text
List size in RAM:         8448728 bytes
Generator size in RAM:        208 bytes
```

---

## 5. Passing Directly to Aggregation Functions

When a generator expression is passed as the single argument to a function like `sum()`, `max()`, `min()`, or `any()`, the outer parentheses can be omitted:

```python
# Sum of squares up to 10
total = sum(x ** 2 for x in range(1, 11))
print("Sum of squares:", total)

# Check if any negative number exists
has_negative = any(x < 0 for x in [10, -5, 20])
print("Has negative?   ", has_negative)
```

**Output:**

```text
Sum of squares: 385
Has negative?    True
```
