# Python Tuples – Creation, Operations, Packing, Unpacking, and Immutability

---

## 1. Introduction to Tuples

A **tuple** is a built-in Python sequence data type used to store a collection of items in a single variable.

Tuples are:

- **Ordered:** The elements maintain the exact order in which they were defined.
- **Immutable:** Once created, elements cannot be modified, added, removed, or replaced.
- **Indexed:** Elements are accessible via zero-based positive indexes and negative indexes.
- **Heterogeneous:** Can store elements of multiple distinct data types together.
- **Allow Duplicates:** The same value can appear at different positions within a tuple.
- **Iterable:** Can be looped through using `for` loops and comprehensions.

### Real-World Analogy

Imagine real-world scenarios where data must remain constant and tamper-proof:

1. **GPS Coordinates:** `location = (12.9716, 77.5946)` — Latitude and longitude must not be accidentally altered during program execution.
2. **RGB Color Code:** `color = (255, 128, 0)` — Represents a specific shade of orange; changing one channel changes the entire color identity.
3. **Database Records:** `record = (101, "Sivanarul", "Engineering", 75000.0)` — A snapshot of an immutable row returned from a database query.

---

## 2. Creating Tuples

Tuples are typically defined by enclosing comma-separated values in round parentheses `()`.

### Example 1: Creating Tuples with Round Parentheses

```python
# Tuple of strings
cities = ("Chennai", "Bangalore", "Hyderabad")
print(cities)
print(type(cities))

# Tuple of integers
marks = (90, 85, 92, 88)
print(marks)

# Tuple of mixed data types
employee = (1001, "Arun", True, 45000.50)
print(employee)
```

**Output:**

```text
('Chennai', 'Bangalore', 'Hyderabad')
<class 'tuple'>
(90, 85, 92, 88)
(1001, 'Arun', True, 45000.5)
```

---

### Example 2: The Single-Element Tuple (The Comma Rule)

A very common beginner trap in Python is creating a single-element tuple. If you omit the trailing comma, Python treats the parentheses as a grouping operator for the enclosed value, resulting in a primitive type.

```python
# NOT a tuple!
not_a_tuple = ("apple")
print(type(not_a_tuple))

not_a_tuple_num = (42)
print(type(not_a_tuple_num))

# Correct way: Add a trailing comma
single_item_tuple = ("apple",)
print(type(single_item_tuple))

single_num_tuple = (42,)
print(type(single_num_tuple))
```

**Output:**

```text
<class 'str'>
<class 'int'>
<class 'tuple'>
<class 'tuple'>
```

---

### Example 3: Tuple Packing (Creating Tuples Without Parentheses)

In Python, any comma-separated sequence of values without enclosing brackets is automatically treated as a tuple. This is known as **tuple packing**.

```python
point = 10, 20, 30
print(point)
print(type(point))

single_item = 99,
print(single_item)
print(type(single_item))
```

**Output:**

```text
(10, 20, 30)
<class 'tuple'>
(99,)
<class 'tuple'>
```

---

### Example 4: Creating an Empty Tuple

```python
# Using empty parentheses
empty1 = ()
print(empty1)
print(type(empty1))

# Using the tuple() constructor
empty2 = tuple()
print(empty2)
print(type(empty2))
```

**Output:**

```text
()
<class 'tuple'>
()
<class 'tuple'>
```

---

### Example 5: Using the `tuple()` Constructor

The built-in `tuple()` function converts any iterable (such as a list, string, set, range, or dictionary) into a tuple.

```python
# From a list
numbers_list = [1, 2, 3, 4]
numbers_tuple = tuple(numbers_list)
print(numbers_tuple)

# From a string (splits each character)
greeting_tuple = tuple("PYTHON")
print(greeting_tuple)

# From a range
range_tuple = tuple(range(1, 6))
print(range_tuple)

# From a dictionary (extracts keys)
user_dict = {"id": 1, "name": "Siva"}
dict_keys_tuple = tuple(user_dict)
print(dict_keys_tuple)
```

**Output:**

```text
(1, 2, 3, 4)
('P', 'Y', 'T', 'H', 'O', 'N')
(1, 2, 3, 4, 5)
('id', 'name')
```

---

## 3. Accessing Tuple Elements (Indexing)

Because tuples are ordered sequences, each element is assigned an index position.

- **Positive Indexing:** Begins at `0` for the first element and proceeds left-to-right up to `n - 1`.
- **Negative Indexing:** Begins at `-1` for the last element and proceeds right-to-left down to `-n`.

| Element | `'Python'` | `'Java'` | `'C++'` | `'JavaScript'` |
| :--- | :---: | :---: | :---: | :---: |
| **Positive Index** | `0` | `1` | `2` | `3` |
| **Negative Index** | `-4` | `-3` | `-2` | `-1` |

```python
languages = ("Python", "Java", "C++", "JavaScript")

# Positive Indexing
print(languages[0])   # First element
print(languages[2])   # Third element

# Negative Indexing
print(languages[-1])  # Last element
print(languages[-2])  # Second to last element
```

**Output:**

```text
Python
C++
JavaScript
C++
```

### Handling `IndexError`

Attempting to access an index that falls outside the bounds of the tuple raises an `IndexError`.

```python
languages = ("Python", "Java")

try:
    print(languages[5])
except IndexError as e:
    print(f"Error encountered: {e}")
```

**Output:**

```text
Error encountered: tuple index out of range
```

---

## 4. Slicing Tuples

Tuple slicing extracts a subset (a new sub-tuple) using the slice syntax:

$$\text{tuple}[\text{start} : \text{stop} : \text{step}]$$

- `start`: The starting index (inclusive). Defaults to `0`.
- `stop`: The stopping index (exclusive). Defaults to `len(tuple)`.
- `step`: The step interval. Defaults to `1`.

```python
numbers = (10, 20, 30, 40, 50, 60, 70, 80)

# Slice from index 1 up to index 5 (exclusive)
print(numbers[1:5])

# Slice from beginning up to index 4
print(numbers[:4])

# Slice from index 4 to the end
print(numbers[4:])

# Slice with a step of 2
print(numbers[::2])

# Negative step: Reverse the entire tuple
print(numbers[::-1])

# Slicing with negative indices
print(numbers[-5:-1])
```

**Output:**

```text
(20, 30, 40, 50)
(10, 20, 30, 40)
(50, 60, 70, 80)
(10, 30, 50, 70)
(80, 70, 60, 50, 40, 30, 20, 10)
(40, 50, 60, 70)
```

---

## 5. Tuple Immutability and the "Mutable Element" Exception

### Why Tuples Are Immutable

Once a tuple is allocated in memory, its references cannot be modified. You cannot assign new values to indices, nor can you append or delete items.

```python
fruits = ("apple", "banana", "cherry")

try:
    fruits[0] = "mango"
except TypeError as e:
    print(f"Modification failed: {e}")
```

**Output:**

```text
Modification failed: 'tuple' object does not support item assignment
```

---

### Tuples Containing Mutable Objects

While the tuple itself cannot have its references changed, if any of its elements are mutable objects (such as a `list` or a `dict`), the contents of that mutable object **can** be modified in place.

```python
# A tuple containing two lists
project = ("Alpha", [101, 102], {"status": "Active"})

# Attempting to reassign the entire list fails
try:
    project[1] = [201, 202]
except TypeError as e:
    print(f"Reassigning reference failed: {e}")

# BUT mutating the list internally works!
project[1].append(103)
project[2]["status"] = "Completed"

print(project)
```

**Output:**

```text
Reassigning reference failed: 'tuple' object does not support item assignment
('Alpha', [101, 102, 103], {'status': 'Completed'})
```

> **Key Takeaway:** The tuple strictly protects its internal *references*. The identity (`id()`) of `project[1]` never changes, even when the contents of the list inside it grow.

---

## 6. Tuple Operations

### 1. Concatenation (`+`)

Joining two or more tuples creates a brand new tuple object.

```python
t1 = (1, 2, 3)
t2 = (4, 5, 6)

t3 = t1 + t2
print(t3)
```

**Output:**

```text
(1, 2, 3, 4, 5, 6)
```

---

### 2. Repetition (`*`)

Multiplying a tuple by an integer repeats its sequence.

```python
pattern = ("A", "B") * 3
print(pattern)
```

**Output:**

```text
('A', 'B', 'A', 'B', 'A', 'B')
```

---

### 3. Membership Testing (`in`, `not in`)

Check whether an item exists in a tuple with $O(n)$ search time.

```python
vowels = ('a', 'e', 'i', 'o', 'u')

print('e' in vowels)
print('z' in vowels)
print('b' not in vowels)
```

**Output:**

```text
True
False
True
```

---

### 4. Iteration and `enumerate()`

Tuples can be traversed sequentially with `for` loops.

```python
roles = ("Admin", "Developer", "Tester", "Manager")

for index, role in enumerate(roles, start=1):
    print(f"Role {index}: {role}")
```

**Output:**

```text
Role 1: Admin
Role 2: Developer
Role 3: Tester
Role 4: Manager
```

---

## 7. Built-in Tuple Methods

Because tuples are immutable, they only offer two built-in methods: `count()` and `index()`.

### 1. `count(value)`

Returns the number of times `value` appears in the tuple.

```python
scores = (10, 20, 30, 20, 40, 20, 50)

print(scores.count(20))
print(scores.count(99))
```

**Output:**

```text
3
0
```

---

### 2. `index(value, [start, [stop]])`

Returns the first zero-based index where `value` appears. If `value` is absent, it raises a `ValueError`.

```python
scores = (10, 20, 30, 20, 40)

# Find first occurrence of 20
first_index = scores.index(20)
print(f"First 20 at index: {first_index}")

# Find next occurrence of 20 starting search from index 2
second_index = scores.index(20, 2)
print(f"Second 20 at index: {second_index}")

# Searching for an absent item
try:
    scores.index(99)
except ValueError as e:
    print(f"Error: {e}")
```

**Output:**

```text
First 20 at index: 1
Second 20 at index: 3
Error: tuple.index(x): x not in tuple
```

---

## 8. Tuple Packing and Unpacking

### Tuple Packing

Assigning multiple comma-separated values into a single variable packs them into a tuple.

```python
employee_data = "Sivanarul", 27, "Developer", 75000.0
print(employee_data)
print(type(employee_data))
```

**Output:**

```text
('Sivanarul', 27, 'Developer', 75000.0)
<class 'tuple'>
```

---

### Tuple Unpacking

Extracting values from a tuple directly into individual variables:

```python
name, age, role, salary = employee_data

print(f"Name:   {name}")
print(f"Age:    {age}")
print(f"Role:   {role}")
print(f"Salary: {salary}")
```

**Output:**

```text
Name:   Sivanarul
Age:    27
Role:   Developer
Salary: 75000.0
```

> **Rule:** The number of variables on the left must exactly match the number of elements in the tuple, otherwise a `ValueError` is raised.

```python
coords = (10, 20, 30)

try:
    x, y = coords  # Too few variables
except ValueError as e:
    print(e)
```

**Output:**

```text
too many values to unpack (expected 2)
```

---

### Extended Unpacking (The Asterisk `*` Operator)

When you only need certain values and want to bundle remaining items into a list, use the `*` operator (splat unpacking):

```python
numbers = (1, 2, 3, 4, 5, 6)

# Extract first, last, and bundle middle
first, *middle, last = numbers
print("First: ", first)
print("Middle:", middle)
print("Last:  ", last)

# Extract first two and bundle rest
a, b, *rest = numbers
print("a:", a, "b:", b, "rest:", rest)

# Bundle leading items, extract final
*head, tail = numbers
print("head:", head, "tail:", tail)
```

**Output:**

```text
First:  1
Middle: [2, 3, 4, 5]
Last:   6
a: 1 b: 2 rest: [3, 4, 5, 6]
head: [1, 2, 3, 4, 5] tail: 6
```

---

### Swapping Variables Using Tuple Packing/Unpacking

Python uses tuple packing and unpacking under the hood to swap variables cleanly without requiring a temporary third variable:

```python
a = 100
b = 200

# Swapping in a single line
a, b = b, a

print(f"a = {a}, b = {b}")
```

**Output:**

```text
a = 200, b = 100
```

---

## 9. Named Tuples (`collections.namedtuple`)

Standard tuples require accessing fields by numeric indices (`person[0]`, `person[1]`), which can become ambiguous and error-prone in large applications.

The `collections` module provides `namedtuple`, which grants each element a meaningful field name while preserving all performance and immutability benefits of standard tuples.

```python
from collections import namedtuple

# Define the named tuple structure
Employee = namedtuple('Employee', ['id', 'name', 'department', 'salary'])

# Create an instance
emp1 = Employee(id=101, name="Sivanarul", department="AI Engineering", salary=85000)

# Access by field name
print(f"ID:         {emp1.id}")
print(f"Name:       {emp1.name}")
print(f"Department: {emp1.department}")
print(f"Salary:     ${emp1.salary}")

# Still accessible by index
print(f"Index 0:    {emp1[0]}")

# Conversion to dictionary
print(emp1._asdict())
```

**Output:**

```text
ID:         101
Name:       Sivanarul
Department: AI Engineering
Salary:     $85000
Index 0:    101
{'id': 101, 'name': 'Sivanarul', 'department': 'AI Engineering', 'salary': 85000}
```

---

## 10. Tuples vs Lists: Detailed Comparison

| Feature | `tuple` | `list` |
| :--- | :--- | :--- |
| **Syntax** | Round parentheses `(1, 2)` | Square brackets `[1, 2]` |
| **Mutability** | **Immutable** (cannot be altered) | **Mutable** (elements can be added/deleted/changed) |
| **Memory Size** | Smaller memory footprint | Larger overhead (allocates extra space for growth) |
| **Execution Speed** | Faster iteration and creation | Slightly slower due to dynamic overhead |
| **Dictionary Keys** | **Yes** (if all elements inside are hashable) | **No** (unhashable type: `list`) |
| **Set Elements** | Can be stored in a `set` | Cannot be stored in a `set` |
| **Primary Intent** | Fixed records, heterogeneous data, read-only | Dynamic collections, homogeneous series |

### Memory Verification Example

```python
import sys

sample_list = [10, 20, 30, 40, 50]
sample_tuple = (10, 20, 30, 40, 50)

print(f"List size in bytes:  {sys.getsizeof(sample_list)}")
print(f"Tuple size in bytes: {sys.getsizeof(sample_tuple)}")
```

**Output:**

```text
List size in bytes:  104
Tuple size in bytes: 80
```

---

## 11. Built-in Functions Compatible with Tuples

```python
nums = (45, 12, 89, 33, 67, 12)

print("len():   ", len(nums))
print("max():   ", max(nums))
print("min():   ", min(nums))
print("sum():   ", sum(nums))
print("sorted():", sorted(nums))  # Returns a sorted LIST
```

**Output:**

```text
len():    6
max():    89
min():    12
sum():    258
sorted(): [12, 12, 33, 45, 67, 89]
```

---

## 12. Common Mistakes and Best Practices

1. **Forgetting the comma in single-item tuples:**
   - Always write `item = (5,)` instead of `item = (5)`.
2. **Attempting in-place modification:**
   - Tuples do not have `.append()`, `.extend()`, `.remove()`, or `.sort()`.
   - To sort a tuple: use `sorted_tuple = tuple(sorted(my_tuple))`.
3. **Using tuples for frequently changing data:**
   - If your collection grows and shrinks dynamically during runtime, choose a `list`.
4. **Use tuples for dictionary keys:**
   - A tuple `(user_id, session_id)` makes an excellent compound dictionary key because it is hashable.

---

## 13. Practice Problems

### Problem 1: Find the Frequency and Position of an Element
Write a function that accepts a tuple and a target element, and returns a tuple containing:
- The count of occurrences
- The index of its first appearance

```python
def analyze_element(tup, target):
    if target in tup:
        return (tup.count(target), tup.index(target))
    return (0, -1)

data = (10, 25, 40, 25, 70, 25, 90)
print(analyze_element(data, 25))
print(analyze_element(data, 99))
```

**Output:**

```text
(3, 1)
(0, -1)
```

---

### Problem 2: Nested Tuple Flattening
Write a function to flatten a tuple of tuples containing numbers into a single 1D tuple.

```python
def flatten_tuple(nested_tuple):
    flat_list = []
    for item in nested_tuple:
        if isinstance(item, tuple):
            flat_list.extend(item)
        else:
            flat_list.append(item)
    return tuple(flat_list)

nested = ((1, 2), (3, 4, 5), (6,), 7)
print(flatten_tuple(nested))
```

**Output:**

```text
(1, 2, 3, 4, 5, 6, 7)
```
