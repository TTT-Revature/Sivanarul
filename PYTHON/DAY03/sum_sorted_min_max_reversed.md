# Python sum(), sorted(), min(), max(), reversed()

---

## 1. Introduction

Python provides high-performance built-in functions for aggregating, ordering, and querying collections. Rather than writing manual accumulator loops or sorting algorithms, using `sum()`, `sorted()`, `min()`, `max()`, and `reversed()` delivers optimized C-level speed and clear code.

---

## 2. sum()

Calculates the arithmetic total of numeric values in an iterable.

### Basic Usage & Start Offset

```python
numbers = [10, 20, 30, 40]
print("Sum:", sum(numbers))

# Adding an initial starting value
print("Sum with initial 100:", sum(numbers, 100))

# Summing with a generator expression
orders = [{"item": "Desk", "price": 150.0}, {"item": "Chair", "price": 85.0}]
total_price = sum(order["price"] for order in orders)
print(f"Total: ${total_price:.2f}")
```

**Output:**

```text
Sum: 100
Sum with initial 100: 200
Total: $235.00
```

> **Note:** For concatenating strings, avoid `sum()` (it raises `TypeError`); use `"".join(seq)` instead.

---

## 3. sorted()

Returns a **brand-new sorted list** from any iterable without mutating the original source.

### Default and Reverse Ordering

```python
scores = [45, 92, 18, 77, 63]
ordered_scores = sorted(scores)
descending_scores = sorted(scores, reverse=True)

print("Original:  ", scores)
print("Sorted:    ", ordered_scores)
print("Descending:", descending_scores)
```

**Output:**

```text
Original:   [45, 92, 18, 77, 63]
Sorted:     [18, 45, 63, 77, 92]
Descending: [92, 77, 63, 45, 18]
```

### Custom Sorting with `key`

```python
words = ["watermelon", "fig", "banana", "kiwi"]
by_length = sorted(words, key=len)
print("By length:", by_length)

students = [("Alice", 85), ("Bob", 95), ("Charlie", 78)]
by_grade = sorted(students, key=lambda s: s[1], reverse=True)
print("By score:", by_grade)
```

**Output:**

```text
By length: ['fig', 'kiwi', 'banana', 'watermelon']
By score: [('Bob', 95), ('Alice', 85), ('Charlie', 78)]
```

---

## 4. min() and max()

Locate the minimum and maximum items within an iterable or across multiple arguments.

### Basic Numbers and Strings

```python
values = [14, 88, 2, 45, 61]
print("Min:", min(values))
print("Max:", max(values))

print("Lexicographical min:", min("banana", "apple", "date"))
```

**Output:**

```text
Min: 2
Max: 88
Lexicographical min: apple
```

### Dictionary Extremes using `key` and `default`

```python
inventory = {"Apples": 45, "Bananas": 12, "Oranges": 90}

cheapest = min(inventory, key=inventory.get)
most_stocked = max(inventory, key=inventory.get)

print(f"Lowest: {cheapest} ({inventory[cheapest]})")
print(f"Highest: {most_stocked} ({inventory[most_stocked]})")

# Preventing ValueError on empty inputs with default
empty_list = []
safe_val = min(empty_list, default=0)
print("Safe min on empty:", safe_val)
```

**Output:**

```text
Lowest: Bananas (12)
Highest: Oranges (90)
Safe min on empty: 0
```

---

## 5. reversed()

Returns a lightweight reverse iterator over a sequence without allocating a duplicated list in memory.

```python
digits = [1, 2, 3, 4, 5]

# Iterating in reverse
for digit in reversed(digits):
    print(digit, end=" ")
print()

# Materializing a reversed list or string
rev_list = list(reversed(digits))
rev_str = "".join(reversed("Python"))

print("Reversed list:", rev_list)
print("Reversed text:", rev_str)
```

**Output:**

```text
5 4 3 2 1 
Reversed list: [5, 4, 3, 2, 1]
Reversed text: nohtyP
```

---

## 6. Comparison Reference

| Function | Modifies Input? | Returns | Key Feature |
|---|---|---|---|
| `sum(it, start=0)` | No | Number | Fast arithmetic accumulation |
| `sorted(it, key=None, reverse=False)` | No | New `list` | Stable Timsort algorithm |
| `min(it, default=d, key=k)` | No | Single item | Supports custom comparator keys |
| `max(it, default=d, key=k)` | No | Single item | Supports custom comparator keys |
| `reversed(seq)` | No | Iterator | $O(1)$ memory consumption |

---

## 7. Best Practices

1. **Prefer `sorted(iterable)`** when immutability is desired; use `list.sort()` only when you specifically want in-place modification.
2. **Always supply `default=`** to `min()` and `max()` when querying data sources that may be empty to avoid `ValueError`.
3. **Use generator expressions inside `sum()`** rather than building intermediate list comprehensions.
4. **Use `reversed()`** when streaming large sequences backwards to avoid cloning memory.
