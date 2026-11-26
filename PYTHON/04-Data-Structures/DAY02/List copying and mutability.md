
# Python Lists – Copying and Mutability



---

## 1. Introduction

Python lists are mutable objects.

This means you can modify their contents after creating them.

Consider the following example:

```python
numbers = [10, 20, 30]

numbers[0] = 100

print(numbers)
```

**Output:**

```text
[100, 20, 30]
```

The original list has been modified.

However, when working with lists, an important question arises:

**What happens when you assign one list variable to another variable?**

Does Python create a new list, or do both variables refer to the same list?

To understand this, we need to learn:

- Object references.
- Variable assignment.
- Mutability.
- Aliasing.
- Shallow copying.
- Deep copying.
- Nested mutable objects.

---

## 2. Understanding Python Objects and References

In Python, variables are names that refer to objects.

When you create a list:

```python
numbers = [10, 20, 30]
```

Python creates a list object, and the variable `numbers` refers to that object.

Conceptually:

```text
numbers
   |
   v
+----------------+
| 10 | 20 | 30   |
+----------------+
   List Object
```

The variable does not contain an independent copy of the list.

It refers to the list object.

You can inspect an object's identity using `id()`.

```python
numbers = [10, 20, 30]

print(id(numbers))
```

The output will be an integer representing the object's identity during its lifetime.

The exact number can differ between executions.

### Checking object identity

```python
numbers = [10, 20, 30]

print(id(numbers))
print(id(numbers))
```

Both calls return the same identity because the variable still refers to the same object.

**Important:** `id()` provides an object identity value. Do not assume it is a physical memory address.

---

## 3. Understanding Mutability

Mutability describes whether an object can be modified after it has been created.

Python objects are commonly classified as:

1. Mutable objects.
2. Immutable objects.

### 3.1 Mutable objects

Mutable objects can be changed after creation.

Examples:

- `list`
- `dict`
- `set`
- `bytearray`

Example:

```python
numbers = [10, 20, 30]

numbers[1] = 200

print(numbers)
```

**Output:**

```text
[10, 200, 30]
```

The existing list object has been modified.

### 3.2 Immutable objects

Immutable objects cannot have their existing value changed after creation.

Examples:

- `int`
- `float`
- `complex`
- `bool`
- `str`
- `tuple`
- `frozenset`
- `bytes`

Example:

```python
name = "Python"

name = name + " Programming"

print(name)
```

**Output:**

```text
Python Programming
```

This does not modify the original string object.

Python creates a new string value and rebinds the variable `name` to it.

### Mutable vs immutable

| Feature | Mutable | Immutable |
|---|---|---|
| Can modify existing object? | Yes | No |
| Can change contents? | Yes | No |
| Examples | List, dict, set | int, str, tuple |
| Common operation | `list.append()` | Create a new value |
| Object identity | Usually remains the same during in-place modification | Rebinding may refer to a different object |

Note: A tuple is immutable, but it can contain mutable objects such as lists. Those inner objects can still be modified.

---

## 4. Variable Assignment Does Not Create a Copy

Consider:

```python
numbers = [10, 20, 30]

new_numbers = numbers

print(numbers)
print(new_numbers)
```

**Output:**

```text
[10, 20, 30]
[10, 20, 30]
```

It may appear that Python created two lists.

But that is not what happened.

Both variables refer to the same list object.

### Visual representation

```text
numbers --------+
                |
                v
          +------------+
          | 10 | 20 | 30 |
          +------------+
                ^
                |
new_numbers ----+
```

### Verify using `is`

```python
numbers = [10, 20, 30]

new_numbers = numbers

print(numbers is new_numbers)
```

**Output:**

```text
True
```

The `is` operator checks whether two variables refer to the same object.

### Verify using `id()`

```python
numbers = [10, 20, 30]

new_numbers = numbers

print(id(numbers))
print(id(new_numbers))
```

Both identity values will be the same.

---

## 5. Understanding Aliasing

Aliasing occurs when multiple variables refer to the same object.

Example:

```python
employees = ["Arun", "Kumar", "Siva"]

team = employees
```

Here:

- `employees` refers to a list.
- `team` refers to the same list.
- Both variables are aliases for the same object.

### Example: Modifying through an alias

```python
employees = ["Arun", "Kumar", "Siva"]

team = employees

team.append("Ravi")

print(employees)
print(team)
```

**Output:**

```text
['Arun', 'Kumar', 'Siva', 'Ravi']
['Arun', 'Kumar', 'Siva', 'Ravi']
```

Why did the `employees` list also change?

Because `team` and `employees` point to the same list object.

### Important distinction

Assignment creates another reference.

It does not create another independent list.

---

## 6. Modifying a List vs Reassigning a Variable

These two operations are different.

### Example 1: Modifying the existing object

```python
numbers = [10, 20, 30]

new_numbers = numbers

numbers.append(40)

print(new_numbers)
```

**Output:**

```text
[10, 20, 30, 40]
```

The original list was modified.

Both variables observe the change.

### Example 2: Reassigning the variable

```python
numbers = [10, 20, 30]

new_numbers = numbers

numbers = [100, 200, 300]

print(numbers)
print(new_numbers)
```

**Output:**

```text
[100, 200, 300]
[10, 20, 30]
```

Why?

Initially, both variables referred to the same list.

Then:

```python
numbers = [100, 200, 300]
```

Python created a new list and made `numbers` refer to it.

The variable `new_numbers` still refers to the original list.

### Visual representation

Before reassignment:

```text
numbers --------+
                |
                v
           [10, 20, 30]
                ^
                |
new_numbers ----+
```

After reassignment:

```text
numbers --------> [100, 200, 300]


new_numbers ----> [10, 20, 30]
```

This distinction is fundamental to Python programming.

---

# PART 2: COPYING LISTS

## 7. What Is List Copying?

List copying means creating another list object containing elements from an existing list.

For example:

```python
original = [10, 20, 30]

copied = original.copy()
```

Now:

- `original` refers to one list.
- `copied` refers to another list.
- Modifying the outer structure of one list does not modify the other.

There are two important types of copying:

1. Shallow copy.
2. Deep copy.

---

## 8. Shallow Copy

### What is a shallow copy?

A shallow copy creates a new outer object but does not recursively copy nested objects.

For a list containing only immutable values, a shallow copy often behaves exactly as beginners expect.

### Common ways to create a shallow copy

**Method 1: Using `copy()`**

```python
numbers = [10, 20, 30]

copied_numbers = numbers.copy()
```

**Method 2: Using slicing**

```python
numbers = [10, 20, 30]

copied_numbers = numbers[:]
```

**Method 3: Using the `list()` constructor**

```python
numbers = [10, 20, 30]

copied_numbers = list(numbers)
```

All three create a new outer list.

### Example: Modifying a shallow copy

```python
original = [10, 20, 30]

copied = original.copy()

copied.append(40)

print("Original:", original)
print("Copied:", copied)
```

**Output:**

```text
Original: [10, 20, 30]
Copied: [10, 20, 30, 40]
```

The original list remains unchanged.

### Checking object identity

```python
original = [10, 20, 30]

copied = original.copy()

print(original is copied)
```

**Output:**

```text
False
```

They are separate outer list objects.

---

## 9. The Limitation of Shallow Copying

Now consider a nested list.

```python
original = [
    [10, 20],
    [30, 40]
]

copied = original.copy()
```

At first glance, it may look like Python created two completely independent nested structures.

But that is not true.

Only the outer list was copied.

The inner lists are still shared.

### Visual representation

```text
original --------> Outer List A
                    |
                    |----> Inner List 1 [10, 20]
                    |
                    |----> Inner List 2 [30, 40]


copied ----------> Outer List B
                    |
                    |----> Inner List 1 [10, 20]
                    |
                    |----> Inner List 2 [30, 40]
```

Both outer lists refer to the same inner lists.

### Example: Modifying a nested list

```python
original = [
    [10, 20],
    [30, 40]
]

copied = original.copy()

copied[0].append(99)

print("Original:", original)
print("Copied:", copied)
```

**Output:**

```text
Original: [[10, 20, 99], [30, 40]]
Copied: [[10, 20, 99], [30, 40]]
```

Why did the original also change?

Because:

```python
copied[0]
```

and:

```python
original[0]
```

refer to the same inner list.

### Checking inner object identity

```python
original = [[10, 20], [30, 40]]

copied = original.copy()

print(original is copied)
print(original[0] is copied[0])
```

**Output:**

```text
False
True
```

Explanation:

- `original is copied` → False because the outer lists are different.
- `original[0] is copied[0]` → True because the first inner list is shared.

This is the key concept behind shallow copying.

---

## 10. Deep Copy

### What is a deep copy?

A deep copy recursively copies objects inside a collection.

It creates independent copies of nested mutable objects as well as the outer list.

Python provides the `copy` module to perform deep copying.

### Syntax

```python
import copy

copied = copy.deepcopy(original)
```

### Example

```python
import copy

original = [
    [10, 20],
    [30, 40]
]

copied = copy.deepcopy(original)

copied[0].append(99)

print("Original:", original)
print("Copied:", copied)
```

**Output:**

```text
Original: [[10, 20], [30, 40]]
Copied: [[10, 20, 99], [30, 40]]
```

The original nested list remains unchanged.

### Visual representation

```text
original --------> Outer List A
                    |
                    |----> Inner List 1 [10, 20]
                    |
                    |----> Inner List 2 [30, 40]


copied ----------> Outer List B
                    |
                    |----> Inner List 1 [10, 20]
                    |
                    |----> Inner List 2 [30, 40]
```

Unlike shallow copying, the nested lists are also independently copied.

### Verify object identity

```python
import copy

original = [[10, 20], [30, 40]]

copied = copy.deepcopy(original)

print(original is copied)
print(original[0] is copied[0])
```

**Output:**

```text
False
False
```

Both the outer list and the inner lists are different objects.

**Important:** Deep copying follows Python's object-copying rules. It does not guarantee that every object becomes an entirely independent resource. Some objects, such as external resources, may not be meaningfully deep-copyable. Deep copying can also be expensive for large structures.

---

## 11. Shallow Copy vs Deep Copy

| Feature | Shallow Copy | Deep Copy |
|---|---|---|
| Creates a new outer list | Yes | Yes |
| Copies nested mutable objects | No | Recursively |
| Inner mutable objects shared? | Yes | Normally no |
| Useful for flat lists | Yes | Usually unnecessary |
| Useful for nested structures | Depends on requirements | When independent nested data is needed |
| Performance | Usually faster | Usually more expensive |
| Python implementation | `copy()`, `[:]`, `list()` | `copy.deepcopy()` |

### Simple comparison

```python
import copy

original = [[1, 2], [3, 4]]

shallow = original.copy()
deep = copy.deepcopy(original)

shallow[0].append(99)
deep[1].append(88)

print("Original:", original)
print("Shallow:", shallow)
print("Deep:", deep)
```

**Output:**

```text
Original: [[1, 2, 99], [3, 4]]
Shallow: [[1, 2, 99], [3, 4]]
Deep: [[1, 2], [3, 4, 88]]
```

Notice:

- The shallow copy shares nested lists with the original.
- The deep copy has independent nested lists.
- Modifying the deep copy does not modify the original.

---

# PART 3: MUTABILITY IN NESTED STRUCTURES

## 12. Lists Containing Immutable Values

Consider:

```python
original = [10, 20, 30]

copied = original.copy()

copied[0] = 100

print(original)
print(copied)
```

**Output:**

```text
[10, 20, 30]
[100, 20, 30]
```

Why?

The outer lists are separate.

Assigning a new value to an element of the copied list does not modify the original list.

This works as expected because the integer objects themselves are immutable.

---

## 13. Lists Containing Mutable Objects

Now consider a list of dictionaries.

```python
original = [
    {"name": "Arun", "age": 25},
    {"name": "Kumar", "age": 28}
]

copied = original.copy()
```

The outer lists are different, but the dictionaries are shared.

### Example

```python
original = [
    {"name": "Arun", "age": 25},
    {"name": "Kumar", "age": 28}
]

copied = original.copy()

copied[0]["age"] = 30

print(original)
print(copied)
```

**Output:**

```text
[{'name': 'Arun', 'age': 30}, {'name': 'Kumar', 'age': 28}]
[{'name': 'Arun', 'age': 30}, {'name': 'Kumar', 'age': 28}]
```

The dictionary is shared.

Changing the dictionary through one list is visible through the other list.

### Using deep copy

```python
import copy

original = [
    {"name": "Arun", "age": 25},
    {"name": "Kumar", "age": 28}
]

copied = copy.deepcopy(original)

copied[0]["age"] = 30

print(original)
print(copied)
```

**Output:**

```text
[{'name': 'Arun', 'age': 25}, {'name': 'Kumar', 'age': 28}]
[{'name': 'Arun', 'age': 30}, {'name': 'Kumar', 'age': 28}]
```

Now the dictionaries are independent.

---

## 14. Mutability and Function Arguments

This concept is extremely important in Python.

When a list is passed to a function, the function receives a reference to the same object.

Python uses object-reference sharing, sometimes described as call by object sharing.

### Example 1: Modifying a list inside a function

```python
def update_numbers(numbers):
    numbers.append(40)


values = [10, 20, 30]

update_numbers(values)

print(values)
```

**Output:**

```text
[10, 20, 30, 40]
```

Why?

The function receives a reference to the same list object.

When the function modifies the list, the caller can observe the change.

### Example 2: Reassigning a parameter inside a function

```python
def update_numbers(numbers):
    numbers = [100, 200, 300]


values = [10, 20, 30]

update_numbers(values)

print(values)
```

**Output:**

```text
[10, 20, 30]
```

Why?

The local parameter `numbers` is reassigned to a different list.

The caller's variable `values` still refers to the original list.

### Example 3: Returning a modified list

```python
def update_numbers(numbers):
    numbers = numbers.copy()
    numbers.append(40)

    return numbers


values = [10, 20, 30]

result = update_numbers(values)

print("Original:", values)
print("Result:", result)
```

**Output:**

```text
Original: [10, 20, 30]
Result: [10, 20, 30, 40]
```

This approach avoids modifying the caller's original outer list.

If the list contains nested mutable objects, a shallow copy may still share those objects.

---

## 15. Mutable Default Argument Problem

Python evaluates default argument expressions when a function is defined, not every time the function is called.

This can create unexpected behaviour when using a mutable default value.

### Incorrect approach

```python
def add_employee(name, employees=[]):
    employees.append(name)
    return employees


print(add_employee("Arun"))
print(add_employee("Kumar"))
print(add_employee("Siva"))
```

**Output:**

```text
['Arun']
['Arun', 'Kumar']
['Arun', 'Kumar', 'Siva']
```

Why?

The same default list is reused across function calls.

### Correct approach

Use `None` as the default value and create a new list inside the function.

```python
def add_employee(name, employees=None):
    if employees is None:
        employees = []

    employees.append(name)

    return employees


print(add_employee("Arun"))
print(add_employee("Kumar"))
print(add_employee("Siva"))
```

**Output:**

```text
['Arun']
['Kumar']
['Siva']
```

Each call creates a new list when no list is provided.

### Important distinction

If the caller explicitly passes an existing list, this function still modifies that list.

```python
def add_employee(name, employees=None):
    if employees is None:
        employees = []

    employees.append(name)
    return employees


team = ["Arun"]

add_employee("Kumar", team)

print(team)
```

**Output:**

```text
['Arun', 'Kumar']
```

If you do not want to modify the caller's list, copy it inside the function.

```python
def add_employee(name, employees=None):
    if employees is None:
        employees = []
    else:
        employees = employees.copy()

    employees.append(name)

    return employees
```

This creates a new outer list. For nested mutable structures, consider whether a deep copy is required.

---

# PART 4: PRACTICAL APPLICATIONS

## 16. FDE Example: Protecting API Response Data

Imagine an external API provides customer records.

```python
customers = [
    {"id": 101, "name": "Arun", "status": "active"},
    {"id": 102, "name": "Kumar", "status": "inactive"},
    {"id": 103, "name": "Siva", "status": "active"}
]
```

Suppose you need to create a modified version for reporting without changing the original API response.

### Problem: Shallow copy

```python
customers_copy = customers.copy()

customers_copy[0]["status"] = "inactive"

print(customers[0])
```

**Output:**

```text
{'id': 101, 'name': 'Arun', 'status': 'inactive'}
```

The original record was modified because the dictionary is shared.

### Solution: Deep copy

```python
import copy

customers_copy = copy.deepcopy(customers)

customers_copy[0]["status"] = "inactive"

print("Original:", customers[0])
print("Copy:", customers_copy[0])
```

**Output:**

```text
Original: {'id': 101, 'name': 'Arun', 'status': 'active'}
Copy: {'id': 101, 'name': 'Arun', 'status': 'inactive'}
```

Now the original customer records remain unchanged.

### Why this matters in FDE development

You may work with:

- API responses from customer systems.
- Configuration objects.
- Nested JSON data.
- AI model inputs and outputs.
- Data transformation pipelines.
- Multi-step business workflows.

Unexpected mutations can cause incorrect reports, altered payloads, and difficult-to-debug application behaviour.

However, do not deep-copy every API response automatically. Copy only when independent data is required. Deep copying large objects can consume additional memory and processing time.

---

## 17. FDE Example: Creating Independent AI Prompt Data

Imagine an application maintains a base prompt configuration.

```python
base_prompt = {
    "model": "llama3.2",
    "temperature": 0.2,
    "messages": [
        {"role": "system", "content": "You are a helpful assistant."}
    ]
}
```

You want to create a separate prompt configuration for another workflow.

### Incorrect approach

```python
prompt_a = base_prompt

prompt_a["messages"].append(
    {"role": "user", "content": "Explain Python lists."}
)

print(base_prompt)
```

The original configuration is also modified because both variables refer to the same dictionary.

### Using a shallow copy

```python
prompt_a = base_prompt.copy()

prompt_a["messages"].append(
    {"role": "user", "content": "Explain Python lists."}
)

print(base_prompt)
```

The original is still affected because the nested `messages` list is shared.

### Using a deep copy

```python
import copy

prompt_a = copy.deepcopy(base_prompt)

prompt_a["messages"].append(
    {"role": "user", "content": "Explain Python lists."}
)

print("Base:", base_prompt)
print("Workflow:", prompt_a)
```

**Output:**

```text
Base: {
    'model': 'llama3.2',
    'temperature': 0.2,
    'messages': [
        {'role': 'system', 'content': 'You are a helpful assistant.'}
    ]
}

Workflow: {
    'model': 'llama3.2',
    'temperature': 0.2,
    'messages': [
        {'role': 'system', 'content': 'You are a helpful assistant.'},
        {'role': 'user', 'content': 'Explain Python lists.'}
    ]
}
```

The base configuration remains unchanged.

---

## 18. Choosing the Correct Copying Strategy

| Situation | Recommended approach |
|---|---|
| Another variable should refer to the same list | `new = original` |
| Independent copy of a flat list | `original.copy()` |
| Independent outer list | `original[:]` |
| Convert another iterable into a list | `list(iterable)` |
| Independent copy of nested mutable structures | `copy.deepcopy(original)` |
| Modify the original intentionally | Use the original reference |
| Avoid changing a caller's flat list | Make a shallow copy |

The correct strategy depends on whether you want to share or isolate the underlying data.

---

## 19. Common Mistakes

### Mistake 1: Assuming assignment creates a copy

```python
a = [10, 20, 30]
b = a

b.append(40)

print(a)
```

Output:

```text
[10, 20, 30, 40]
```

Both variables refer to the same object.

### Mistake 2: Assuming a shallow copy copies nested lists

```python
a = [[10, 20], [30, 40]]
b = a.copy()

b[0].append(99)

print(a)
```

Output:

```text
[[10, 20, 99], [30, 40]]
```

The inner list is shared.

### Mistake 3: Using deep copy unnecessarily

For a simple list of integers:

```python
import copy

numbers = [10, 20, 30]

copied = copy.deepcopy(numbers)
```

A normal shallow copy is sufficient for this flat list.

### Mistake 4: Confusing modification with reassignment

```python
a = [10, 20, 30]
b = a

a = [100, 200, 300]

print(b)
```

Output:

```text
[10, 20, 30]
```

Reassigning `a` does not change the object referenced by `b`.

### Mistake 5: Assuming function arguments are automatically copied

```python
def update(items):
    items.append(100)


numbers = [10, 20, 30]

update(numbers)

print(numbers)
```

Output:

```text
[10, 20, 30, 100]
```

The function modifies the shared list object.

### Mistake 6: Using mutable default arguments

Avoid:

```python
def process(items=[]):
    items.append(10)
    return items
```

Prefer:

```python
def process(items=None):
    if items is None:
        items = []

    items.append(10)
    return items
```

---

# PART 5: PRACTICE AND REVISION

## 20. Practice Exercises

### Beginner Level

1. Create a list containing five integers.
2. Assign the list to another variable.
3. Modify the second variable and observe the original.
4. Check whether two variables refer to the same object using `is`.
5. Create a shallow copy using `copy()`.
6. Create a shallow copy using slicing.
7. Modify the copied list and compare both lists.

### Intermediate Level

8. Create a nested list and perform a shallow copy.
9. Modify an inner list through the copied list.
10. Observe the changes in the original list.
11. Create a deep copy using `copy.deepcopy()`.
12. Modify a nested list inside the deep copy.
13. Compare the original, shallow copy, and deep copy.
14. Pass a list to a function and modify it.
15. Reassign a function parameter and observe the caller's list.

### FDE Practical Level

16. Create a list of customer dictionaries.
17. Create a shallow copy and update a nested customer field.
18. Explain why the original data changes.
19. Create a deep copy and repeat the update.
20. Build two independent AI prompt configurations from one base configuration.
21. Write a function that accepts a list and returns an updated copy without changing the original.
22. Demonstrate the mutable default argument problem and correct it.

---

## 21. Quick Revision

| Concept | Meaning |
|---|---|
| Mutability | Ability to modify an existing object |
| Mutable object | An object whose contents can change |
| Immutable object | An object whose value cannot be changed after creation |
| Reference | A way to access an object |
| Aliasing | Multiple variables referring to the same object |
| Assignment | Binds another variable name to an object |
| Shallow copy | Creates a new outer object but shares nested objects |
| Deep copy | Recursively copies nested objects |
| `id()` | Returns an object's identity value |
| `is` | Checks whether two references point to the same object |
| `==` | Checks value equality |
| `copy()` | Creates a shallow list copy |
| `copy.deepcopy()` | Creates a deep copy |

### Important syntax

```python
# Assignment: same object
b = a

# Shallow copy
b = a.copy()

# Shallow copy using slicing
b = a[:]

# Shallow copy using list()
b = list(a)

# Deep copy
import copy
b = copy.deepcopy(a)

# Identity comparison
print(a is b)

# Equality comparison
print(a == b)
```

---

## 22. Self-Assessment

Try answering these questions without referring to the notes.

1. What is mutability in Python?
2. Why are lists called mutable objects?
3. What is an object reference?
4. What is aliasing?
5. Does `b = a` create a new list?
6. What is the difference between modifying a list and reassigning a variable?
7. What is a shallow copy?
8. What is a deep copy?
9. Why can modifying a nested list affect a shallow copy's original list?
10. What is the purpose of `copy.deepcopy()`?
11. What is the difference between `is` and `==`?
12. How are lists passed to functions?
13. Why can modifying a function argument affect the caller's list?
14. Why should mutable default arguments be avoided?
15. When would you use deep copying in an FDE application?

---

## 23. Learning Outcome

After completing this chapter, you should be able to:

- Explain mutable and immutable objects.
- Understand Python object references.
- Differentiate assignment from copying.
- Explain aliasing.
- Create shallow copies using `copy()`, slicing, and `list()`.
- Understand why shallow copying shares nested objects.
- Create deep copies using `copy.deepcopy()`.
- Understand mutability when passing lists to functions.
- Avoid mutable default argument problems.
- Choose an appropriate copying strategy for API and AI application data.

**Next recommended topic:** List Iteration – `for` loops, `enumerate()`, and iterating over nested lists.
