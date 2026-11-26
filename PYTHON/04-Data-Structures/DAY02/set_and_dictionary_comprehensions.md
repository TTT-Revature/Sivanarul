# Python Set and Dictionary Comprehensions

---

## 1. Introduction

Following the success of list comprehensions, Python extended the comprehension syntax to **sets** and **dictionaries**.

Comprehensions provide a clean, declarative syntax for transforming and filtering collections without relying on multi-line imperative loops or complex `lambda` functions.

| Comprehension Type | Enclosing Syntax | Resulting Data Type | Primary Advantage |
| :--- | :---: | :---: | :--- |
| **List Comprehension** | `[...]` | `list` | Ordered, duplicate-preserving sequence |
| **Set Comprehension** | `{...}` | `set` | Unordered, automatically deduplicated collection |
| **Dictionary Comprehension** | `{k: v ...}` | `dict` | Fast key-value associative mapping |

---

## 2. Set Comprehensions

A **set comprehension** constructs a new `set` by evaluating an expression for every item in an iterable, automatically discarding any duplicate values.

### Basic Syntax

$$\{\text{expression} \quad \textbf{for} \quad \text{item} \quad \textbf{in} \quad \text{iterable}\}$$

---

### Example 1: Deduplication of Word Lengths

Given a list of words, determine all distinct word lengths:

```python
words = ["python", "java", "ruby", "c", "rust", "go", "kotlin"]

# Set comprehension automatically removes duplicate lengths
unique_lengths = {len(w) for w in words}

print("Unique word lengths:", unique_lengths)
print("Type:", type(unique_lengths))
```

**Output:**

```text
Unique word lengths: {1, 2, 4, 6}
Type: <class 'set'>
```

---

### Example 2: Set Comprehension with Filtering (`if`)

$$\{\text{expression} \quad \textbf{for} \quad \text{item} \quad \textbf{in} \quad \text{iterable} \quad \textbf{if} \quad \text{condition}\}$$

```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 2, 4, 6]

# Extract unique squares of even numbers only
even_squares = {n ** 2 for n in numbers if n % 2 == 0}
print("Unique even squares:", even_squares)
```

**Output:**

```text
Unique even squares: {16, 64, 4, 36, 100}
```

---

### Example 3: Extracting Unique File Extensions

In system automation and data engineering pipelines, extracting clean file extensions is a common task:

```python
filenames = [
    "data_2026.csv",
    "report.pdf",
    "script.py",
    "backup_data.csv",
    "notes.txt",
    "summary.pdf",
    "app.py"
]

extensions = {fname.split(".")[-1].lower() for fname in filenames}
print("Unique extensions found:", extensions)
```

**Output:**

```text
Unique extensions found: {'py', 'pdf', 'csv', 'txt'}
```

---

### Example 4: Sanitizing Dirty Text Data

```python
raw_tags = ["  Python ", "python", "DJANGO", " Django ", "FastAPI", "fastapi "]

clean_tags = {tag.strip().lower() for tag in raw_tags}
print("Clean tags:", clean_tags)
```

**Output:**

```text
Clean tags: {'django', 'python', 'fastapi'}
```

---

## 3. Dictionary Comprehensions

A **dictionary comprehension** constructs a new dictionary by evaluating a pair of expressions (`key_expression: value_expression`) for each item in an iterable.

### Basic Syntax

$$\{\text{key\_expression} : \text{value\_expression} \quad \textbf{for} \quad \text{item} \quad \textbf{in} \quad \text{iterable}\}$$

---

### Example 1: Mapping Numbers to Their Squares

```python
squares_map = {x: x ** 2 for x in range(1, 6)}
print(squares_map)
```

**Output:**

```text
{1: 1, 2: 4, 3: 9, 4: 16, 5: 25}
```

---

### Example 2: Mapping Words to Character Counts

```python
technologies = ["Python", "FastAPI", "Docker", "Kubernetes", "PostgreSQL"]

tech_lengths = {tech: len(tech) for tech in technologies}
print(tech_lengths)
```

**Output:**

```text
{'Python': 6, 'FastAPI': 7, 'Docker': 6, 'Kubernetes': 10, 'PostgreSQL': 10}
```

---

### Example 3: Character ASCII Code Lookup

```python
ascii_table = {char: ord(char) for char in "REVATURE"}
print(ascii_table)
```

**Output:**

```text
{'R': 82, 'E': 69, 'V': 86, 'A': 65, 'T': 84, 'U': 85}
```

---

## 4. Dictionary Comprehensions with Filtering (`if`)

$$\{\text{key\_expr} : \text{val\_expr} \quad \textbf{for} \quad \text{item} \quad \textbf{in} \quad \text{iterable} \quad \textbf{if} \quad \text{condition}\}$$

---

### Example 1: Filtering Scores by Threshold

```python
student_marks = {
    "Arun": 88,
    "Sivanarul": 94,
    "Priya": 72,
    "Karan": 64,
    "Deepa": 91
}

# Keep only students scoring 85 or above
distinction = {name: mark for name, mark in student_marks.items() if mark >= 85}
print("Distinction Students:", distinction)
```

**Output:**

```text
Distinction Students: {'Arun': 88, 'Sivanarul': 94, 'Deepa': 91}
```

---

### Example 2: Filtering Low-Stock Inventory

```python
inventory = {
    "LAPTOPS": 42,
    "KEYBOARDS": 8,
    "MONITORS": 15,
    "MICE": 4,
    "CABLES": 3
}

# Flag items requiring restocking (stock < 10)
reorder_alerts = {item: qty for item, qty in inventory.items() if qty < 10}
print("Items to reorder:", reorder_alerts)
```

**Output:**

```text
Items to reorder: {'KEYBOARDS': 8, 'MICE': 4, 'CABLES': 3}
```

---

## 5. Dictionary Comprehensions with Conditional Values (`if-else`)

When every entry should be included but its value needs to change conditionally:

$$\{\text{key} : (\text{true\_val} \quad \textbf{if} \quad \text{condition} \quad \textbf{else} \quad \text{false\_val}) \quad \textbf{for} \quad \text{item} \quad \textbf{in} \quad \text{iterable}\}$$

```python
exam_scores = {"Arun": 82, "Priya": 48, "Siva": 95, "Karan": 38}

# Evaluate performance category
grade_summary = {
    student: ("PASS" if score >= 50 else "FAIL")
    for student, score in exam_scores.items()
}

print(grade_summary)
```

**Output:**

```text
{'Arun': 'PASS', 'Priya': 'FAIL', 'Siva': 'PASS', 'Karan': 'FAIL'}
```

---

## 6. Pairing Iterables with `zip()` in Dictionary Comprehensions

You can cleanly merge two separate lists (one containing keys, another containing values) into a dictionary.

```python
employee_ids = [101, 102, 103, 104]
employee_names = ["Arun", "Sivanarul", "Priya", "Kavitha"]

# Construct dictionary using zip
id_to_employee = {emp_id: name for emp_id, name in zip(employee_ids, employee_names)}
print(id_to_employee)

# Alternatively using dict constructor directly:
# id_to_employee = dict(zip(employee_ids, employee_names))
```

**Output:**

```text
{101: 'Arun', 102: 'Sivanarul', 103: 'Priya', 104: 'Kavitha'}
```

---

## 7. Inverting and Swapping Dictionaries

Swapping the keys and values of a dictionary is an essential algorithmic operation (e.g., turning an `ID -> Name` lookup into a `Name -> ID` lookup).

### 1. Basic Inversion (When Values Are Unique)

```python
country_to_capital = {
    "India": "New Delhi",
    "France": "Paris",
    "Japan": "Tokyo"
}

# Swap keys and values
capital_to_country = {capital: country for country, capital in country_to_capital.items()}
print(capital_to_country)
```

**Output:**

```text
{'New Delhi': 'India', 'Paris': 'France', 'Tokyo': 'Japan'}
```

---

### 2. Inverting When Duplicate Values Exist (The Overwrite Trap)

If multiple keys share the same value, a simple inversion will overwrite previous keys:

```python
# Multiple employees belong to the same department
employee_departments = {
    "Arun": "Engineering",
    "Priya": "HR",
    "Siva": "Engineering",
    "Karan": "Finance",
    "Deepa": "Engineering"
}

# BAD: Overwriting occurs! Only the last employee per department is retained
bad_inversion = {dept: emp for emp, dept in employee_departments.items()}
print("Bad Inversion:", bad_inversion)

# CORRECT: Grouping into a list or set of employees per department
all_departments = set(employee_departments.values())
department_groups = {
    dept: [emp for emp, d in employee_departments.items() if d == dept]
    for dept in all_departments
}
print("\nProper Grouping:")
for dept, members in department_groups.items():
    print(f"  {dept:<12}: {members}")
```

**Output:**

```text
Bad Inversion: {'Engineering': 'Deepa', 'HR': 'Priya', 'Finance': 'Karan'}

Proper Grouping:
  HR          : ['Priya']
  Finance     : ['Karan']
  Engineering : ['Arun', 'Siva', 'Deepa']
```

---

## 8. Nested Dictionary Comprehensions

Dictionary comprehensions can be nested to construct multi-level hierarchies such as multiplication tables, matrix lookups, or grid configurations:

```python
# Construct a nested multiplication table for numbers 1 to 3
multiplication_grid = {
    i: {j: i * j for j in range(1, 4)}
    for i in range(1, 4)
}

import pprint
pprint.pprint(multiplication_grid)
```

**Output:**

```text
{1: {1: 1, 2: 2, 3: 3},
 2: {1: 2, 2: 4, 3: 6},
 3: {1: 3, 2: 6, 3: 9}}
```

---

## 9. Generator Expressions vs Comprehensions

When dealing with massive sequences (e.g., millions of records), building entire lists, sets, or dictionaries in memory can cause `MemoryError`.

A **generator expression** uses round parentheses `()` and computes values **lazily** (one at a time on demand):

```python
import sys

# List comprehension: generates all 100,000 items in memory at once
list_comp = [x ** 2 for x in range(100000)]

# Generator expression: generates items on-the-fly
gen_expr = (x ** 2 for x in range(100000))

print(f"List Comprehension Size: {sys.getsizeof(list_comp):>8} bytes")
print(f"Generator Expression Size: {sys.getsizeof(gen_expr):>6} bytes")
```

**Output:**

```text
List Comprehension Size:   824456 bytes
Generator Expression Size:    208 bytes
```

---

## 10. Comprehension Comparison Matrix

| Feature | List Comprehension | Set Comprehension | Dict Comprehension |
| :--- | :---: | :---: | :---: |
| **Syntax** | `[x for x in data]` | `{x for x in data}` | `{k: v for k, v in data}` |
| **Output Type** | `list` | `set` | `dict` |
| **Duplicates** | Preserved | Automatically removed | Keys must be unique |
| **Ordering** | Guaranteed (Ordered) | Arbitrary (Unordered) | Insertion Ordered (3.7+) |
| **Key Hashability** | N/A | Every element must be hashable | Keys must be hashable |

---

## 11. Practice Problems

### Problem 1: Word Length Filter with Set Comprehension
Given a paragraph of text, extract a set containing all unique words that have 5 or more characters, normalized to lowercase.

```python
paragraph = "Python is an incredible language and developers love Python for web development and data science"

long_words = {word.lower() for word in paragraph.split() if len(word) >= 5}
print(long_words)
```

**Output:**

```text
{'development', 'language', 'python', 'developers', 'science', 'incredible'}
```

---

### Problem 2: Filtering and Applying Discounts with Dict Comprehension
Given a store catalog with product prices, create a new dictionary containing only products priced over \$50, with a 10% discount applied to each.

```python
catalog = {
    "Laptop": 1200.00,
    "Mouse": 25.00,
    "Monitor": 300.00,
    "USB Cable": 12.00,
    "Headphones": 85.00
}

discounted_catalog = {
    item: round(price * 0.90, 2)
    for item, price in catalog.items()
    if price > 50.00
}

print(discounted_catalog)
```

**Output:**

```text
{'Laptop': 1080.0, 'Monitor': 270.0, 'Headphones': 76.5}
```
