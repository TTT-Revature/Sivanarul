# Python Sets and Set Operations

---

## 1. Introduction to Sets

A **set** is an unordered collection of unique and immutable (hashable) elements. Sets in Python are based on mathematical set theory and are implemented under the hood using hash tables.

Sets have the following core characteristics:

- **Unordered:** Elements have no fixed order or index position; the order can vary between executions.
- **Unique Elements:** Duplicates are strictly not allowed. Any duplicated items are automatically eliminated.
- **Mutable Collection:** The set itself can grow or shrink; elements can be added or removed.
- **Hashable Elements:** Every individual element inside a set must be immutable (e.g., integers, floats, strings, tuples, or frozensets).
- **Unindexed:** Since elements have no fixed order, sets do not support indexing, slicing, or sequence concatenation.

### Real-World Analogy

1. **Unique Visitor IPs:** Tracking distinct IP addresses accessing a web server over a 24-hour window: `{ "192.168.1.1", "10.0.0.5" }`.
2. **Student Roll Numbers:** A registry ensuring no duplicate student ID is issued in a university department.
3. **Skill Tags:** Finding overlapping competencies between candidate skills and job requirements (e.g., Python, SQL, Docker).

---

## 2. Creating Sets

Sets are primarily created using curly braces `{}` containing comma-separated elements, or by passing an iterable to the `set()` constructor.

### Example 1: Creating Sets with Curly Braces

```python
# Set of strings
fruits = {"apple", "banana", "cherry"}
print(fruits)
print(type(fruits))

# Set of integers
numbers = {10, 20, 30, 40}
print(numbers)

# Automatic duplicate removal
tags = {"python", "django", "python", "flask", "django"}
print(tags)
```

**Output:**

```text
{'banana', 'cherry', 'apple'}
<class 'set'>
{10, 20, 30, 40}
{'django', 'flask', 'python'}
```

---

### Example 2: The Empty Set Trap

In Python, `{}` defines an empty **dictionary**, NOT an empty set. To initialize an empty set, you **must** use the `set()` constructor.

```python
# This creates a dictionary!
empty_dict = {}
print(type(empty_dict))

# Correct: Creates an empty set
empty_set = set()
print(type(empty_set))
print(empty_set)
```

**Output:**

```text
<class 'dict'>
<class 'set'>
set()
```

---

### Example 3: Creating Sets from Iterables with `set()`

```python
# From a list with duplicates (Deduplication)
raw_ids = [101, 102, 101, 103, 102, 104]
unique_ids = set(raw_ids)
print(unique_ids)

# From a string (extracts unique characters)
unique_chars = set("MISSISSIPPI")
print(unique_chars)

# From a range
num_set = set(range(1, 6))
print(num_set)
```

**Output:**

```text
{101, 102, 103, 104}
{'M', 'I', 'P', 'S'}
{1, 2, 3, 4, 5}
```

---

## 3. Set Elements and the Hashability Rule

Every item added to a set must be **hashable**, meaning its hash value must never change during its lifetime.

### Allowed (Hashable / Immutable Types):
- `int`, `float`, `complex`
- `str`
- `bool`
- `tuple` (only if all elements within the tuple are also hashable)
- `frozenset`

### Not Allowed (Unhashable / Mutable Types):
- `list`
- `dict`
- `set`

```python
# Valid: integers, strings, tuples
valid_set = {100, "Python", (1, 2, 3)}
print(valid_set)

# Invalid: attempting to add a list
try:
    invalid_set = {1, 2, [3, 4]}
except TypeError as e:
    print(f"Error: {e}")

# Invalid: tuple containing a mutable list
try:
    tuple_with_list = {1, (2, [3, 4])}
except TypeError as e:
    print(f"Error: {e}")
```

**Output:**

```text
{100, (1, 2, 3), 'Python'}
Error: unhashable type: 'list'
Error: unhashable type: 'list'
```

---

## 4. Accessing and Checking Set Elements

Because sets are unindexed, attempting to access elements via square brackets `s[0]` or slice notation `s[1:3]` results in a `TypeError`.

```python
colors = {"red", "green", "blue"}

try:
    print(colors[0])
except TypeError as e:
    print(f"Indexing error: {e}")
```

**Output:**

```text
Indexing error: 'set' object is not subscriptable
```

### Checking Membership (`in` and `not in`)

Sets use a hash table for element storage, allowing membership tests to complete in average **$O(1)$ constant time**, compared to $O(n)$ linear scanning in lists.

```python
active_users = {"arun99", "siva_k", "priya_dev"}

print("siva_k" in active_users)
print("john_doe" in active_users)
print("guest" not in active_users)
```

**Output:**

```text
True
False
True
```

### Iterating Over a Set

You can iterate through each item using a `for` loop:

```python
frameworks = {"Django", "FastAPI", "Flask"}

for framework in frameworks:
    print(f"Framework: {framework}")
```

**Output:**

```text
Framework: Django
Framework: Flask
Framework: FastAPI
```

---

## 5. Adding and Updating Elements

### 1. `add(element)`
Adds a single element to the set. If the element is already present, the set remains unchanged without error.

```python
languages = {"Python", "Java"}

languages.add("Go")
languages.add("Python")  # Duplicate ignored

print(languages)
```

**Output:**

```text
{'Python', 'Java', 'Go'}
```

---

### 2. `update(iterable)`
Adds multiple elements from any iterable (list, tuple, another set, dictionary keys, etc.) to the existing set.

```python
languages = {"Python", "Java"}

# Update with a list and another set
languages.update(["C++", "Rust"], {"Kotlin", "Go"})

print(languages)
```

**Output:**

```text
{'Python', 'Kotlin', 'Go', 'Rust', 'Java', 'C++'}
```

---

## 6. Removing Elements from a Set

Python provides multiple methods to remove elements, each handling missing values differently:

### 1. `remove(element)`
Removes the specified element. If the element does not exist, it raises a `KeyError`.

```python
tech = {"Python", "Docker", "Kubernetes"}

tech.remove("Docker")
print(tech)

try:
    tech.remove("AWS")  # Not present
except KeyError as e:
    print(f"KeyError: Element {e} not found")
```

**Output:**

```text
{'Kubernetes', 'Python'}
KeyError: Element 'AWS' not found
```

---

### 2. `discard(element)`
Removes the specified element if present. If the element does not exist, **no error is raised** (silent operation).

```python
tech = {"Python", "Docker", "Kubernetes"}

tech.discard("Docker")
tech.discard("AWS")  # No error raised!

print(tech)
```

**Output:**

```text
{'Kubernetes', 'Python'}
```

---

### 3. `pop()`
Removes and returns an **arbitrary** element from the set. Since sets are unordered, you cannot predict which element will be popped. If the set is empty, it raises a `KeyError`.

```python
letters = {'A', 'B', 'C', 'D'}

removed_item = letters.pop()
print(f"Popped item: {removed_item}")
print(f"Remaining:   {letters}")
```

**Output:**

```text
Popped item: A
Remaining:   {'B', 'C', 'D'}
```

---

### 4. `clear()`
Removes all elements from the set, leaving it completely empty.

```python
data = {1, 2, 3, 4}
data.clear()

print(data)
print(len(data))
```

**Output:**

```text
set()
0
```

---

### 5. `del`
Deletes the set variable from memory entirely.

```python
sample = {10, 20}
del sample

try:
    print(sample)
except NameError as e:
    print(f"NameError: {e}")
```

**Output:**

```text
NameError: name 'sample' is not defined
```

---

## 7. Mathematical Set Operations

Python provides mathematical set operations via both **operators** and **methods**.

- **Operators** (e.g., `|`, `&`, `-`, `^`) require both operands to be sets.
- **Methods** (e.g., `.union()`, `.intersection()`) accept any iterable as arguments.

```python
team_backend = {"Python", "Java", "SQL", "Docker"}
team_frontend = {"JavaScript", "React", "HTML", "Docker"}
```

---

### 1. Union (`|` or `union()`)

Combines all distinct elements present in either set $A \cup B$.

```python
# Operator
all_skills = team_backend | team_frontend
print("Union (|):       ", all_skills)

# Method
all_skills_m = team_backend.union(team_frontend)
print("Union (.union()):", all_skills_m)
```

**Output:**

```text
Union (|):        {'Python', 'Java', 'HTML', 'SQL', 'React', 'Docker', 'JavaScript'}
Union (.union()): {'Python', 'Java', 'HTML', 'SQL', 'React', 'Docker', 'JavaScript'}
```

---

### 2. Intersection (`&` or `intersection()`)

Finds only the common elements present in both sets $A \cap B$.

```python
# Operator
shared_skills = team_backend & team_frontend
print("Intersection (&):             ", shared_skills)

# Method
shared_skills_m = team_backend.intersection(team_frontend)
print("Intersection (.intersection()):", shared_skills_m)
```

**Output:**

```text
Intersection (&):              {'Docker'}
Intersection (.intersection()): {'Docker'}
```

---

### 3. Difference (`-` or `difference()`)

Returns elements present in the first set but absent from the second set $A \setminus B$.

```python
# Skills unique to backend
only_backend = team_backend - team_frontend
print("Only Backend (-):", only_backend)

# Skills unique to frontend
only_frontend = team_frontend.difference(team_backend)
print("Only Frontend:   ", only_frontend)
```

**Output:**

```text
Only Backend (-): {'Python', 'Java', 'SQL'}
Only Frontend:    {'JavaScript', 'React', 'HTML'}
```

---

### 4. Symmetric Difference (`^` or `symmetric_difference()`)

Returns elements present in either set, but **not in both** $(A \cup B) \setminus (A \cap B)$.

```python
# Skills not shared between teams
non_shared = team_backend ^ team_frontend
print("Symmetric Difference (^):", non_shared)
```

**Output:**

```text
Symmetric Difference (^): {'Python', 'Java', 'HTML', 'SQL', 'React', 'JavaScript'}
```

---

### In-Place Modification Operations

These methods modify the target set directly without returning a new set:

| Operation | In-Place Operator | In-Place Method | Description |
| :--- | :---: | :--- | :--- |
| **Union Update** | `|=` | `s1.update(s2)` | Adds all elements from `s2` into `s1`. |
| **Intersection Update** | `&=` | `s1.intersection_update(s2)` | Keeps only elements found in both `s1` and `s2`. |
| **Difference Update** | `-=` | `s1.difference_update(s2)` | Removes all elements of `s2` from `s1`. |
| **Symmetric Diff Update**| `^=` | `s1.symmetric_difference_update(s2)` | Keeps only elements unique to either set. |

```python
nums = {1, 2, 3, 4, 5}
other = {4, 5, 6, 7}

nums.intersection_update(other)
print("After intersection_update:", nums)
```

**Output:**

```text
After intersection_update: {4, 5}
```

---

## 8. Set Relationships and Comparisons

```python
A = {1, 2, 3}
B = {1, 2, 3, 4, 5}
C = {6, 7, 8}
```

### 1. Subset (`issubset()` or `<=`)
Checks if every element of set $A$ is present in set $B$.

```python
print(A.issubset(B))  # True
print(A <= B)         # True
print(B.issubset(A))  # False
```

---

### 2. Superset (`issuperset()` or `>=`)
Checks if set $B$ contains every element of set $A$.

```python
print(B.issuperset(A))  # True
print(B >= A)           # True
```

---

### 3. Proper Subset (`<`) and Proper Superset (`>`)
A is a proper subset of B if $A \subseteq B$ and $A \neq B$.

```python
print(A < B)     # True
print(A < {1, 2, 3})  # False (equal sets are not proper subsets)
```

---

### 4. Disjoint (`isdisjoint()`)
Checks if two sets have **no common elements** ($A \cap B = \emptyset$).

```python
print(A.isdisjoint(C))  # True (no elements in common)
print(A.isdisjoint(B))  # False (1, 2, 3 are in common)
```

**Output:**

```text
True
True
False
True
True
True
False
True
False
```

---

## 9. Immutable Sets: `frozenset`

A **`frozenset`** is an immutable version of a Python set. Once created, its elements cannot be added, removed, or modified.

### Why Use `frozenset`?
1. **Dictionary Keys:** Because a `frozenset` is immutable, it is hashable and can be used as a key in a dictionary.
2. **Set of Sets:** A standard `set` cannot contain another `set`, but it **can** contain a `frozenset`.
3. **Data Integrity:** Protects critical lookup sets from accidental modification.

```python
# Creating a frozenset
fs1 = frozenset([1, 2, 3, 4, 5])
fs2 = frozenset([4, 5, 6, 7, 8])

print(fs1)
print(type(fs1))

# Set operations work normally and return a new frozenset
print("Intersection:", fs1 & fs2)

# Mutation attempts raise an AttributeError
try:
    fs1.add(10)
except AttributeError as e:
    print(f"Error: {e}")

# Using frozenset as a dictionary key
group_permissions = {
    frozenset({"admin", "root"}): "Full Access",
    frozenset({"guest"}): "Read-Only Access"
}

user_role = frozenset({"admin", "root"})
print(f"Access Level: {group_permissions[user_role]}")
```

**Output:**

```text
frozenset({1, 2, 3, 4, 5})
<class 'frozenset'>
Intersection: frozenset({4, 5})
Error: 'frozenset' object has no attribute 'add'
Access Level: Full Access
```

---

## 10. Set Performance and Time Complexity

Python sets are built using hash tables, giving them exceptional lookup and modification performance:

| Operation | Average Case | Worst Case (Hash Collisions) |
| :--- | :---: | :---: |
| **Add element** (`add`) | $O(1)$ | $O(n)$ |
| **Remove element** (`remove` / `discard`) | $O(1)$ | $O(n)$ |
| **Check membership** (`in`) | $O(1)$ | $O(n)$ |
| **Union** ($A \cup B$) | $O(\text{len}(A) + \text{len}(B))$ | $O(\text{len}(A) \times \text{len}(B))$ |
| **Intersection** ($A \cap B$) | $O(\min(\text{len}(A), \text{len}(B)))$ | $O(\text{len}(A) \times \text{len}(B))$ |
| **Difference** ($A \setminus B$) | $O(\text{len}(A))$ | $O(\text{len}(A) \times \text{len}(B))$ |

---

## 11. Summary Table of Built-in Set Methods

| Method | Syntax | Description |
| :--- | :--- | :--- |
| `add()` | `s.add(x)` | Adds item `x` to set `s`. |
| `update()` | `s.update(iter)` | Adds all items from iterable `iter`. |
| `remove()` | `s.remove(x)` | Removes item `x`; raises `KeyError` if absent. |
| `discard()` | `s.discard(x)` | Removes item `x` safely without error if absent. |
| `pop()` | `s.pop()` | Removes and returns an arbitrary element. |
| `clear()` | `s.clear()` | Removes all elements from the set. |
| `union()` | `s.union(iter)` | Returns the union of sets. |
| `intersection()` | `s.intersection(iter)` | Returns the intersection of sets. |
| `difference()` | `s.difference(iter)` | Returns elements unique to `s`. |
| `symmetric_difference()` | `s.symmetric_difference(iter)` | Returns elements in either set but not both. |
| `issubset()` | `s.issubset(other)` | Returns `True` if `s` is a subset of `other`. |
| `issuperset()` | `s.issuperset(other)` | Returns `True` if `s` is a superset of `other`. |
| `isdisjoint()` | `s.isdisjoint(other)` | Returns `True` if sets share no common elements. |
| `copy()` | `s.copy()` | Returns a shallow copy of the set. |

---

## 12. Practice Problems

### Problem 1: Remove Duplicate Customer Emails Preserving Unique Entries
Given a raw list of customer email submissions that contains duplicates with inconsistent casing, write a function to return a clean set of lowercased emails.

```python
def sanitize_emails(email_list):
    return {email.strip().lower() for email in email_list}

submissions = [
    "User1@Example.com ",
    "admin@revature.com",
    "user1@example.com",
    " ADMIN@REVATURE.COM "
]

clean_emails = sanitize_emails(submissions)
print(clean_emails)
```

**Output:**

```text
{'user1@example.com', 'admin@revature.com'}
```

---

### Problem 2: Find Common and Missing Course Enrollees
You are given two sets of student IDs: enrolled in Python and enrolled in Java. Compute:
1. Students enrolled in both courses.
2. Students enrolled only in Python.
3. Total unique students across both courses.

```python
python_students = {101, 102, 105, 108, 110}
java_students = {102, 103, 105, 109, 112}

both = python_students & java_students
only_python = python_students - java_students
all_unique = python_students | java_students

print("Both courses: ", both)
print("Only Python:  ", only_python)
print("Total unique: ", all_unique)
```

**Output:**

```text
Both courses:  {102, 105}
Only Python:   {101, 108, 110}
Total unique:  {101, 102, 103, 105, 108, 109, 110, 112}
```
