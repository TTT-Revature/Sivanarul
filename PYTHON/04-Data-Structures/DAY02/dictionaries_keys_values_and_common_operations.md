# Python Dictionaries – Keys, Values, and Common Operations

---

## 1. Introduction to Dictionaries

A **dictionary** is a built-in Python data structure that stores data in associative **key-value pairs**. It is classified under Python's **mapping** data type.

Key characteristics of Python dictionaries:

- **Key-Value Mapping:** Each entry consists of an associative pair: a unique `key` pointing to a `value` (`key: value`).
- **Insertion Ordered:** Since Python 3.7+, dictionaries officially maintain the insertion order of elements.
- **Mutable:** You can add, update, replace, or delete key-value pairs after creation.
- **Keys Must Be Unique and Hashable:** Duplicate keys are not permitted. Keys must be of an immutable (hashable) type such as `str`, `int`, `float`, or `tuple`.
- **Values Can Be Anything:** Values have zero restrictions; they can be duplicates, `None`, primitive numbers, strings, lists, sets, functions, or other dictionaries.
- **Fast Lookups:** Retrieval of values by key operates in average **$O(1)$ constant time** using hash tables.

### Real-World Analogy

1. **Phone Directory:** A person's name acts as the unique lookup key, and their phone number is the associated value.
2. **Employee Records:** An employee ID (`1001`) maps to a comprehensive employee profile.
3. **HTTP Headers:** An HTTP request header mapping `"Content-Type": "application/json"`.

---

## 2. Creating Dictionaries

### Example 1: Using Curly Braces `{}`

```python
# Standard dictionary
employee = {
    "id": 101,
    "name": "Sivanarul",
    "role": "Software Engineer",
    "salary": 75000.0,
    "skills": ["Python", "SQL", "Docker"]
}

print(employee)
print(type(employee))
```

**Output:**

```text
{'id': 101, 'name': 'Sivanarul', 'role': 'Software Engineer', 'salary': 75000.0, 'skills': ['Python', 'SQL', 'Docker']}
<class 'dict'>
```

---

### Example 2: Creating an Empty Dictionary

```python
# Using empty curly braces
empty_dict1 = {}
print(empty_dict1, type(empty_dict1))

# Using the dict() constructor
empty_dict2 = dict()
print(empty_dict2, type(empty_dict2))
```

**Output:**

```text
{} <class 'dict'>
{} <class 'dict'>
```

---

### Example 3: Using the `dict()` Constructor

```python
# Using keyword arguments (keys must be valid Python identifiers)
config = dict(host="localhost", port=8080, debug=True)
print(config)

# From a list of 2-item tuples or sublists
pairs = [("IN", "India"), ("US", "United States"), ("UK", "United Kingdom")]
country_codes = dict(pairs)
print(country_codes)
```

**Output:**

```text
{'host': 'localhost', 'port': 8080, 'debug': True}
{'IN': 'India', 'US': 'United States', 'UK': 'United Kingdom'}
```

---

### Example 4: Using `dict.fromkeys()`

Initializes a dictionary from a sequence of keys, assigning each key a shared default value (defaulting to `None`).

```python
keys = ["cpu", "memory", "disk"]

# Default value None
metrics = dict.fromkeys(keys)
print(metrics)

# Custom default value
status_flags = dict.fromkeys(keys, "ONLINE")
print(status_flags)
```

**Output:**

```text
{'cpu': None, 'memory': None, 'disk': None}
{'cpu': 'ONLINE', 'memory': 'ONLINE', 'disk': 'ONLINE'}
```

> **Warning with Mutable Defaults:** If you provide a mutable object like `[]` as the default in `fromkeys()`, **every key will reference the exact same list in memory**. Modifying one list modifies all of them!

---

## 3. Dictionary Keys and Hashability

A dictionary key must be **hashable**. If an object's state can change after creation (such as a `list`, `set`, or `dict`), it cannot be hashed and cannot serve as a key.

```python
# Valid keys: strings, numbers, booleans, and tuples
valid_dict = {
    "name": "Arun",
    101: "Emp ID",
    3.14: "Pi",
    True: "Flag",
    (10, 20): "Coordinates"
}
print(valid_dict[(10, 20)])

# Invalid key: list
try:
    bad_dict = {[1, 2]: "Invalid"}
except TypeError as e:
    print(f"Error: {e}")
```

**Output:**

```text
Coordinates
Error: unhashable type: 'list'
```

### Duplicate Keys (Last Key Wins)

If duplicate keys are specified during dictionary definition, the **last value overwrites** earlier values:

```python
scores = {"Alice": 80, "Bob": 90, "Alice": 95}
print(scores)
```

**Output:**

```text
{'Alice': 95, 'Bob': 90}
```

---

## 4. Accessing Dictionary Values

### 1. Square Bracket Notation (`dict[key]`)

Provides direct lookup by key. If the key does not exist, Python raises a `KeyError`.

```python
user = {"username": "siva99", "role": "admin"}

print(user["username"])

try:
    print(user["email"])
except KeyError as e:
    print(f"KeyError: Key {e} does not exist")
```

**Output:**

```text
siva99
KeyError: Key 'email' does not exist
```

---

### 2. The `.get(key, default=None)` Method (Safe Access)

Returns the value if `key` exists; otherwise returns `None` (or a specified default value) without raising an exception.

```python
user = {"username": "siva99", "role": "admin"}

# Key exists
print(user.get("role"))

# Key does not exist: returns None
print(user.get("email"))

# Key does not exist: returns custom fallback
print(user.get("email", "not_provided@example.com"))
```

**Output:**

```text
admin
None
not_provided@example.com
```

---

## 5. Adding, Updating, and Modifying Entries

### 1. Direct Assignment

If the key exists, its value is updated. If the key does not exist, a new key-value pair is added.

```python
product = {"name": "Laptop", "price": 1200}

# Update existing key
product["price"] = 1100

# Add new key
product["brand"] = "Dell"

print(product)
```

**Output:**

```text
{'name': 'Laptop', 'price': 1100, 'brand': 'Dell'}
```

---

### 2. The `.update()` Method

Updates a dictionary with elements from another dictionary or from an iterable of key-value pairs.

```python
device = {"type": "Server", "status": "idle"}

# Update with dictionary
device.update({"status": "running", "uptime": "99.9%"})
print(device)

# Update using keyword arguments
device.update(memory="64GB", location="Datacenter 1")
print(device)
```

**Output:**

```text
{'type': 'Server', 'status': 'running', 'uptime': '99.9%'}
{'type': 'Server', 'status': 'running', 'uptime': '99.9%', 'memory': '64GB', 'location': 'Datacenter 1'}
```

---

### 3. The `.setdefault(key, default=None)` Method

- If `key` is in the dictionary, returns its existing value.
- If `key` is **not** in the dictionary, inserts `key` with value `default` and returns `default`.

```python
settings = {"theme": "dark"}

# Key exists: returns existing value, no change
t = settings.setdefault("theme", "light")
print("Theme:", t)

# Key absent: inserts new key with default value
lang = settings.setdefault("language", "English")
print("Language:", lang)

print(settings)
```

**Output:**

```text
Theme: dark
Language: English
{'theme': 'dark', 'language': 'English'}
```

---

## 6. Removing Items from a Dictionary

### 1. `.pop(key, [default])`
Removes the specified key and returns its value. If the key is not found and no default is provided, it raises a `KeyError`.

```python
server = {"host": "10.0.0.1", "port": 80, "ssl": False}

# Remove existing key
removed_val = server.pop("ssl")
print(f"Removed ssl: {removed_val}")

# Safe removal with fallback
removed_missing = server.pop("auth_token", "Not Found")
print(f"Removed auth_token: {removed_missing}")

print(server)
```

**Output:**

```text
Removed ssl: False
Removed auth_token: Not Found
{'host': '10.0.0.1', 'port': 80}
```

---

### 2. `.popitem()`
Removes and returns the **last inserted** `(key, value)` pair as a tuple (LIFO order). Raises `KeyError` if the dictionary is empty.

```python
cache = {"a": 1, "b": 2, "c": 3}

last_item = cache.popitem()
print("Popped item:", last_item)
print("Remaining:  ", cache)
```

**Output:**

```text
Popped item: ('c', 3)
Remaining:   {'a': 1, 'b': 2}
```

---

### 3. The `del` Statement
Deletes an item by key. Raises `KeyError` if the key is missing.

```python
car = {"brand": "Tesla", "model": "Model 3", "year": 2022}

del car["year"]
print(car)
```

**Output:**

```text
{'brand': 'Tesla', 'model': 'Model 3'}
```

---

### 4. `.clear()`
Empties the dictionary completely.

```python
session = {"user": "admin", "token": "abc123xyz"}
session.clear()

print(session)
print(len(session))
```

**Output:**

```text
{}
0
```

---

## 7. Iterating Through Dictionaries & Dictionary Views

Python dictionaries provide three dynamic view objects:

- `.keys()`: View of all dictionary keys.
- `.values()`: View of all dictionary values.
- `.items()`: View of all `(key, value)` pairs as tuples.

> **Dynamic Views:** Views reflect changes made to the underlying dictionary immediately.

```python
inventory = {"apples": 50, "bananas": 100, "oranges": 75}
```

### Iterating Over Keys (Default Behavior)

```python
for item in inventory:
    print(f"Key: {item} -> Value: {inventory[item]}")
```

**Output:**

```text
Key: apples -> Value: 50
Key: bananas -> Value: 100
Key: oranges -> Value: 75
```

---

### Iterating Over Values

```python
total_stock = 0
for quantity in inventory.values():
    total_stock += quantity

print(f"Total Stock: {total_stock}")
```

**Output:**

```text
Total Stock: 225
```

---

### Iterating Over Key-Value Pairs (`.items()`)

```python
for item, qty in inventory.items():
    print(f"Product: {item:<10} | In Stock: {qty:>4}")
```

**Output:**

```text
Product: apples     | In Stock:   50
Product: bananas    | In Stock:  100
Product: oranges    | In Stock:   75
```

---

## 8. Checking Membership

- `key in dict`: Checks if a key exists in the dictionary in average **$O(1)$ time**.
- `val in dict.values()`: Scans all values in linear **$O(n)$ time**.

```python
credentials = {"admin": "pass123", "editor": "pass456"}

print("admin" in credentials)
print("guest" in credentials)

# Checking values
print("pass123" in credentials.values())
```

**Output:**

```text
True
False
True
```

---

## 9. Dictionary Merging and Copying (Python 3.9+)

### The Merge (`|`) and Update (`|=`) Operators

Python 3.9 introduced the union operators for dictionaries:

- `d1 | d2`: Creates a new merged dictionary. If keys overlap, values from the right operand (`d2`) take precedence.
- `d1 |= d2`: Merges `d2` into `d1` in-place.

```python
default_config = {"host": "localhost", "port": 8000, "debug": True}
user_config = {"port": 5000, "workers": 4}

# New merged dictionary
merged = default_config | user_config
print("Merged:", merged)

# In-place update
default_config |= user_config
print("Updated default_config:", default_config)
```

**Output:**

```text
Merged: {'host': 'localhost', 'port': 5000, 'debug': True, 'workers': 4}
Updated default_config: {'host': 'localhost', 'port': 5000, 'debug': True, 'workers': 4}
```

---

### Shallow Copy vs Deep Copy

```python
import copy

original = {"name": "Team A", "members": ["Arun", "Siva"]}

# Shallow copy
shallow = original.copy()

# Deep copy
deep = copy.deepcopy(original)

# Modify nested list in original
original["members"].append("Kumar")

print("Original:", original["members"])
print("Shallow: ", shallow["members"])  # Affected by nested change!
print("Deep:    ", deep["members"])     # Completely isolated!
```

**Output:**

```text
Original: ['Arun', 'Siva', 'Kumar']
Shallow:  ['Arun', 'Siva', 'Kumar']
Deep:     ['Arun', 'Siva']
```

---

## 10. Summary Table of Built-in Dictionary Methods

| Method | Syntax | Description |
| :--- | :--- | :--- |
| `get()` | `d.get(k, [def])` | Returns value for key `k`, or `def` if absent. |
| `keys()` | `d.keys()` | Returns a dynamic view of all keys. |
| `values()` | `d.values()` | Returns a dynamic view of all values. |
| `items()` | `d.items()` | Returns a dynamic view of all `(key, value)` pairs. |
| `pop()` | `d.pop(k, [def])` | Removes key `k` and returns its value. |
| `popitem()` | `d.popitem()` | Removes and returns the last inserted `(k, v)` pair. |
| `update()` | `d.update(other)` | Updates dictionary with key-value pairs from `other`. |
| `setdefault()` | `d.setdefault(k, [def])` | Inserts key with default value if not already present. |
| `clear()` | `d.clear()` | Removes all elements from the dictionary. |
| `copy()` | `d.copy()` | Returns a shallow copy. |
| `fromkeys()` | `dict.fromkeys(keys, [v])` | Class method returning a new dict with given keys. |

---

## 11. Practice Problems

### Problem 1: Word Frequency Counter
Write a function that counts how many times each word appears in a given sentence, ignoring punctuation and case.

```python
def count_words(text):
    words = text.lower().replace(",", "").replace(".", "").split()
    counts = {}
    for word in words:
        counts[word] = counts.get(word, 0) + 1
    return counts

sentence = "Python is powerful and Python is readable. Learning Python is fun."
print(count_words(sentence))
```

**Output:**

```text
{'python': 3, 'is': 3, 'powerful': 1, 'and': 1, 'readable': 1, 'learning': 1, 'fun': 1}
```

---

### Problem 2: Inverting a Dictionary
Given a dictionary mapping student names to grades, invert it so that each grade maps to a list of student names who earned that grade.

```python
def invert_grades(grades):
    inverted = {}
    for student, grade in grades.items():
        inverted.setdefault(grade, []).append(student)
    return inverted

students = {"Arun": "A", "Siva": "B", "Priya": "A", "Karan": "C", "Deepa": "B"}
print(invert_grades(students))
```

**Output:**

```text
{'A': ['Arun', 'Priya'], 'B': ['Siva', 'Deepa'], 'C': ['Karan']}
```
