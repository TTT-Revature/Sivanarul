# Python enumerate(), zip(), any(), all()

---

## 1. Introduction

Python provides versatile built-in iteration utilities that simplify loop logic and prevent cumbersome indexing code. The functions `enumerate()`, `zip()`, `any()`, and `all()` enable concise, highly readable, and idiomatic Python code.

---

## 2. enumerate()

`enumerate(iterable, start=0)` yields pairs containing a running index count and the item produced by the iterable.

### Basic Usage

```python
languages = ["Python", "Rust", "Go", "TypeScript"]

for index, language in enumerate(languages):
    print(f"Index {index}: {language}")
```

**Output:**

```text
Index 0: Python
Index 1: Rust
Index 2: Go
Index 3: TypeScript
```

### Specifying a Custom Start Index

```python
tasks = ["Setup venv", "Install packages", "Run tests"]

for step_num, task in enumerate(tasks, start=1):
    print(f"Step {step_num}: {task}")
```

**Output:**

```text
Step 1: Setup venv
Step 2: Install packages
Step 3: Run tests
```

### Why Avoid `range(len(...))`?

```python
# Unpythonic
for i in range(len(languages)):
    print(i, languages[i])

# Pythonic
for i, lang in enumerate(languages):
    print(i, lang)
```

---

## 3. zip()

`zip(*iterables)` aggregates corresponding elements from each iterable into tuples until the shortest input is exhausted.

### Combining Two Sequences

```python
names = ["Alice", "Bob", "Charlie"]
scores = [92, 85, 88]

for name, score in zip(names, scores):
    print(f"{name} -> {score}")
```

**Output:**

```text
Alice -> 92
Bob -> 85
Charlie -> 88
```

### Pairing Unequal Iterables

```python
ids = [101, 102, 103, 104]
labels = ["Red", "Green"]

paired = list(zip(ids, labels))
print(paired)
```

**Output:**

```text
[(101, 'Red'), (102, 'Green')]
```

> **Note:** To prevent truncation with mismatched lengths, use `itertools.zip_longest()`.

### Creating Dictionaries using `zip()`

```python
keys = ["username", "role", "active"]
values = ["sivanarul", "admin", True]

user_profile = dict(zip(keys, values))
print(user_profile)
```

**Output:**

```text
{'username': 'sivanarul', 'role': 'admin', 'active': True}
```

---

## 4. any()

`any(iterable)` evaluates truthiness across an iterable, returning `True` as soon as **at least one** element evaluates to true (short-circuit evaluation). It returns `False` if all elements are falsy or if the iterable is empty.

```python
flags = [False, False, True, False]
print(any(flags))

numbers = [2, 4, 6, 8, 9]
has_odd = any(n % 2 != 0 for n in numbers)
print("Contains odd number:", has_odd)
```

**Output:**

```text
True
Contains odd number: True
```

---

## 5. all()

`all(iterable)` returns `True` only if **every** element in the iterable evaluates to true. It immediately short-circuits to `False` on the first falsy element encountered.

```python
user_inputs = ["admin", "secret123", "token_val"]
all_filled = all(len(item.strip()) > 0 for item in user_inputs)
print("All inputs valid:", all_filled)

numbers = [2, 4, 6, 7]
all_even = all(n % 2 == 0 for n in numbers)
print("All even:", all_even)
```

**Output:**

```text
All inputs valid: True
All even: False
```

---

## 6. Comparison Table

| Function | Signature | Return Type | Short-Circuits? | Empty Input Value |
|---|---|---|---|---|
| `enumerate()` | `enumerate(iterable, start=0)` | Enumerator iterator | No | Empty iterator |
| `zip()` | `zip(*iterables)` | Zip iterator | Stops at shortest | Empty iterator |
| `any()` | `any(iterable)` | `bool` | Yes (on first `True`) | `False` |
| `all()` | `all(iterable)` | `bool` | Yes (on first `False`) | `True` |

---

## 7. Practical Validation Example

```python
user_record = {
    "name": "Siva",
    "email": "siva@example.com",
    "age": 28,
}

required_fields = ["name", "email", "age"]

# Verify all mandatory fields exist
is_complete = all(field in user_record for field in required_fields)

# Check if any field contains an empty string
has_blank = any(user_record.get(f) == "" for f in required_fields)

print(f"Complete: {is_complete}, Has Blank: {has_blank}")
```

**Output:**

```text
Complete: True, Has Blank: False
```

---

## 8. Best Practices

1. **Use `enumerate()`** instead of maintaining manual index counters (`i += 1`).
2. **Combine `zip()` with `dict()`** for instantaneous dictionary assembly from paired lists.
3. **Use generator expressions with `any()` and `all()`** to avoid creating temporary lists in memory.
4. **Be aware of vacuously true conditions:** `all([])` evaluates to `True`, while `any([])` evaluates to `False`.
