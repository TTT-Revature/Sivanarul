# Python List Comprehensions – Syntax, Filtering, and Advanced Patterns

---

## 1. Introduction to List Comprehensions

A **list comprehension** is a concise, expressive, and Pythonic syntactic construct used to create a new list from an existing iterable (such as a list, tuple, range, or string).

List comprehensions replace verbose `for` loops that repeatedly call `.append()`, allowing developers to write cleaner and faster code.

### The Problem: Traditional `for` Loop with `.append()`

Suppose we need to compute the squares of numbers from `1` to `5`:

```python
# Traditional approach
squares = []
for x in range(1, 6):
    squares.append(x ** 2)

print(squares)
```

### The Solution: List Comprehension

```python
# Pythonic approach
squares = [x ** 2 for x in range(1, 6)]

print(squares)
```

**Output:**

```text
[1, 4, 9, 16, 25]
[1, 4, 9, 16, 25]
```

### Why Use List Comprehensions?

1. **Conciseness:** Reduces 3–4 lines of repetitive boilerplate code down to a readable single line.
2. **Readability:** Expresses **what** list to construct declaratively rather than micro-managing **how** to append items procedurally.
3. **Execution Speed:** Implemented at the C level in Python; bytecode utilizes the optimized `LIST_APPEND` opcode without the overhead of repeated attribute lookups for the `.append` method.

---

## 2. Basic Syntax and Anatomy

The standard syntax of a list comprehension consists of brackets containing an expression followed by a `for` clause:

$$[\text{expression} \quad \textbf{for} \quad \text{item} \quad \textbf{in} \quad \text{iterable}]$$

### How It Works Internally:
1. Python iterates over `iterable`, binding each element to `item`.
2. Evaluates `expression` for that `item`.
3. Stores the resulting value directly into the newly constructed list.

---

### Example 1: Transforming Strings (Case Conversion)

```python
names = ["arun", "sivanarul", "priya", "karan"]

uppercase_names = [name.upper() for name in names]
print(uppercase_names)
```

**Output:**

```text
['ARUN', 'SIVANARUL', 'PRIYA', 'KARAN']
```

---

### Example 2: Calculating Lengths of Elements

```python
frameworks = ["Django", "FastAPI", "Flask", "Tornado"]

name_lengths = [len(fw) for fw in frameworks]
print(name_lengths)
```

**Output:**

```text
[6, 7, 5, 7]
```

---

### Example 3: Type Casting Values

```python
price_strings = ["12.50", "45.00", "9.99", "100.25"]

price_floats = [float(p) for p in price_strings]
print(price_floats)
```

**Output:**

```text
[12.5, 45.0, 9.99, 100.25]
```

---

## 3. List Comprehension with Filtering (`if` Condition)

To include only elements that satisfy a specific condition, append an `if` clause at the end:

$$[\text{expression} \quad \textbf{for} \quad \text{item} \quad \textbf{in} \quad \text{iterable} \quad \textbf{if} \quad \text{condition}]$$

The condition is evaluated **before** the expression. If `condition` evaluates to `False`, the item is skipped.

---

### Example 1: Filtering Even Numbers

```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

even_numbers = [num for num in numbers if num % 2 == 0]
print("Even numbers:", even_numbers)
```

**Output:**

```text
Even numbers: [2, 4, 6, 8, 10]
```

---

### Example 2: Filtering and Transforming Simultaneously

```python
# Compute squares of odd numbers only
odd_squares = [num ** 2 for num in numbers if num % 2 != 0]
print("Odd squares:", odd_squares)
```

**Output:**

```text
Odd squares: [1, 9, 25, 49, 81]
```

---

### Example 3: Filtering Words by Length and Starting Letter

```python
languages = ["Python", "PHP", "Perl", "Java", "Prolog", "C++"]

# Keep words starting with 'P' that have more than 3 characters
p_languages = [lang for lang in languages if lang.startswith('P') and len(lang) > 3]
print(p_languages)
```

**Output:**

```text
['Python', 'Perl', 'Prolog']
```

---

## 4. Conditional Transformations (`if-else` Ternary Operator)

When you need to **transform every item** based on a condition (rather than filtering out items), use Python's ternary conditional expression before the `for` clause:

$$[\text{true\_expression} \quad \textbf{if} \quad \text{condition} \quad \textbf{else} \quad \text{false\_expression} \quad \textbf{for} \quad \text{item} \quad \textbf{in} \quad \text{iterable}]$$

### Crucial Syntax Rule:
- **Filtering (`if` at the end):** Selects which items enter the list.
- **Transformation (`if-else` at the beginning):** Decides what value is computed for every item.

```python
# Categorize numbers as 'EVEN' or 'ODD'
numbers = [1, 2, 3, 4, 5, 6]

labels = ["EVEN" if n % 2 == 0 else "ODD" for n in numbers]
print(labels)
```

**Output:**

```text
['ODD', 'EVEN', 'ODD', 'EVEN', 'ODD', 'EVEN']
```

---

### Example 2: Capping Outlier Values

```python
# Cap any value exceeding 100 down to 100
readings = [45, 120, 88, 150, 95, 200]

normalized = [val if val <= 100 else 100 for val in readings]
print("Normalized Readings:", normalized)
```

**Output:**

```text
Normalized Readings: [45, 100, 88, 100, 95, 100]
```

---

## 5. Nested List Comprehensions

List comprehensions can be nested to handle multi-dimensional arrays, matrices, and grids.

### 1. Flattening a 2D Matrix into a 1D List

```python
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

# Nested comprehension: outer loop comes first
flattened = [val for row in matrix for val in row]
print("Flattened Matrix:", flattened)
```

**Equivalent traditional loop:**
```python
flattened = []
for row in matrix:
    for val in row:
        flattened.append(val)
```

**Output:**

```text
Flattened Matrix: [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

---

### 2. Generating a 2D Grid / Matrix

To construct a 2D list of lists, place a list comprehension inside another list comprehension:

```python
# Create a 3x4 matrix filled with zeros
rows, cols = 3, 4
grid = [[0 for _ in range(cols)] for _ in range(rows)]

import pprint
pprint.pprint(grid)
```

**Output:**

```text
[[0, 0, 0, 0],
 [0, 0, 0, 0],
 [0, 0, 0, 0]]
```

---

### 3. Transposing a Matrix (Swapping Rows and Columns)

```python
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

transposed = [[row[i] for row in matrix] for i in range(len(matrix[0]))]
print("Transposed Matrix:", transposed)
```

**Output:**

```text
Transposed Matrix: [[1, 4, 7], [2, 5, 8], [3, 6, 9]]
```

---

## 6. Comprehensions with Multiple Iterables

### 1. Cartesian Product (All Combinations)

```python
colors = ["Red", "Green"]
sizes = ["S", "M", "L"]

product_combinations = [f"{color}-{size}" for color in colors for size in sizes]
print(product_combinations)
```

**Output:**

```text
['Red-S', 'Red-M', 'Red-L', 'Green-S', 'Green-M', 'Green-L']
```

---

### 2. Parallel Iteration with `zip()`

```python
names = ["Arun", "Siva", "Priya"]
scores = [85, 92, 88]

student_cards = [f"{name}: {score}" for name, score in zip(names, scores)]
print(student_cards)
```

**Output:**

```text
['Arun: 85', 'Siva: 92', 'Priya: 88']
```

---

## 7. Performance Benchmark: Loop vs `map()` vs List Comprehension

Why are list comprehensions faster than standard `for` loops in Python?

1. No overhead of repeatedly looking up the `.append` method on the list object in Python namespace.
2. List construction and sizing happens in specialized C code using the Python runtime's internal list allocation strategy.

```python
import timeit

setup_code = "data = list(range(10000))"

# Approach 1: Standard For Loop
loop_code = """
res = []
for x in data:
    res.append(x * 2)
"""

# Approach 2: List Comprehension
comp_code = "res = [x * 2 for x in data]"

# Approach 3: map with lambda
map_code = "res = list(map(lambda x: x * 2, data))"

t_loop = timeit.timeit(loop_code, setup=setup_code, number=500)
t_comp = timeit.timeit(comp_code, setup=setup_code, number=500)
t_map  = timeit.timeit(map_code,  setup=setup_code, number=500)

print(f"For Loop + append:  {t_loop:.4f} seconds")
print(f"List Comprehension: {t_comp:.4f} seconds (Fastest)")
print(f"map() + lambda:     {t_map:.4f} seconds")
```

**Typical Output:**

```text
For Loop + append:  0.2854 seconds
List Comprehension: 0.1621 seconds (Fastest)
map() + lambda:     0.3120 seconds
```

---

## 8. When NOT to Use List Comprehensions (Anti-Patterns)

While list comprehensions are powerful, writing unreadable one-liners harms maintainability.

### 1. Excessive Nesting (The "Write-Only" Code)
Avoid nesting more than two loops or multiple complex conditions in a single comprehension.

```python
# BAD: Hard to read, debug, and maintain
bad = [x for sub1 in matrix for sub2 in sub1 for x in sub2 if x > 10 if x % 2 == 0]

# GOOD: Use standard readable loops with clear variable names
```

### 2. Running Side Effects Inside Comprehensions
List comprehensions are meant for **creating new data**, not for executing operations that discard results.

```python
# BAD: Do NOT use list comprehension solely to print or write files
[print(x) for x in range(5)]  # Creates an unused list of [None, None, ...] in memory!

# GOOD: Use a standard for loop for side effects
for x in range(5):
    print(x)
```

### 3. Extremely Large Datasets (Memory Exhaustion)
A list comprehension builds the **entire list in RAM at once**. If you are iterating over 50,000,000 records, use a **generator expression** `(x for x in ...)` instead to stream items on demand with $O(1)$ memory.

---

## 9. Practice Problems

### Problem 1: Extract Vowels from a String
Write a list comprehension that extracts all unique vowels from a given sentence in lowercase, sorted alphabetically.

```python
sentence = "Deep Learning with Python and TensorFlow"

vowels = sorted(list({char.lower() for char in sentence if char.lower() in 'aeiou'}))
print("Vowels found:", vowels)
```

**Output:**

```text
Vowels found: ['a', 'e', 'i', 'o']
```

---

### Problem 2: Filtering and Sanitizing User Input
Given a list of phone numbers with various formatting artifacts, extract only the digits and keep numbers that have exactly 10 digits.

```python
raw_phones = [
    "(123) 456-7890",
    "987-654-3210",
    "123-45",
    "Call 800-555-0199 now",
    "9999"
]

clean_phones = [
    clean for raw in raw_phones
    if len(clean := "".join(ch for ch in raw if ch.isdigit())) == 10
]

print(clean_phones)
```

**Output:**

```text
['1234567890', '9876543210', '8005550199']
```
