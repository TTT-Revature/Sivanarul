
# Python Mutable and Immutable Objects

## 1. Introduction

In Python, every value is an object.

Each object has three important characteristics:

1. Identity – Identifies an object.
2. Type – Defines the kind of object.
3. Value – Represents the data stored in the object.

Example:

```python
age = 25

print(age)
print(type(age))
print(id(age))
```

Output:

```text
25
<class 'int'>
```

The `id()` function returns an object's identity during its lifetime.

**Important:** Variables in Python are names that refer to objects. They are not fixed containers that physically store values.

---

## 2. What are Mutable Objects?

Mutable objects are objects whose contents can be changed after creation.

In simple terms, we can modify the existing object without creating a completely new object.

Common mutable built-in types:

- `list`
- `dict`
- `set`
- `bytearray`

Example:

```python
numbers = [10, 20, 30]

print(numbers)
print(id(numbers))

numbers.append(40)

print(numbers)
print(id(numbers))
```

Output:

```text
[10, 20, 30]
[10, 20, 30, 40]
```

The list contents changed, but the list remained the same object.

### Real-world analogy

Imagine a shopping cart.

You can add products, remove products, or update quantities without creating a completely new shopping cart.

This is similar to a mutable object.

---

## 3. What are Immutable Objects?

Immutable objects are objects whose contents cannot be changed after creation.

If we perform an operation that appears to modify an immutable object, Python creates or uses another object and the variable may be reassigned to it.

Common immutable built-in types:

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

print(name)
print(id(name))

name = name + " Developer"

print(name)
print(id(name))
```

The second assignment creates a new string value and rebinds `name`.

**Important:** Do not assume the new object must always have a different identity from every previous object. Python may reuse objects in some situations.

### Real-world analogy

Think of a printed certificate.

You cannot change the existing printed text directly. If you need different information, you produce another certificate.

This is similar to immutable objects.

---

## 4. Mutable vs Immutable

| Feature | Mutable | Immutable |
|---|---|---|
| Modification | Contents can change | Contents cannot change |
| Object identity | Usually remains the same when modified in place | Reassignment refers to another value/object |
| Performance | Useful for repeated modifications | Useful for values that should remain unchanged |
| Examples | List, dictionary, set | Integer, string, tuple |

---

## 5. Understanding the Difference with Lists

Let's see how a mutable object behaves.

```python
a = [10, 20, 30]

b = a

b.append(40)

print(a)
print(b)
```

Output:

```text
[10, 20, 30, 40]
[10, 20, 30, 40]
```

### Why did both variables change?

Step-by-step:

1. A list object is created.
2. Variable `a` refers to that list.
3. Variable `b` is assigned the same object.
4. Both names refer to one list object.
5. `b.append(40)` modifies that object.
6. Both `a` and `b` show the updated contents.

Visual representation:

```text
        a
         \
          \
        [10, 20, 30, 40]
          /
         /
        b
```

Both variables refer to the same object.

---

## 6. Understanding the Difference with Strings

Strings are immutable.

Example:

```python
a = "Python"

b = a

b = b + " Developer"

print(a)
print(b)
```

Output:

```text
Python
Python Developer
```

### Why did only b change?

Step-by-step:

1. A string object `"Python"` is created.
2. Both `a` and `b` refer to that object.
3. `b + " Developer"` creates a new string value.
4. `b` is reassigned to the new string.
5. `a` still refers to the original string.

Visual representation:

```text
a ------> "Python"

b ------> "Python Developer"
```

The original string was not modified.

---

## 7. Understanding id() and Object Identity

Python provides the `id()` function to inspect an object's identity.

Example:

```python
numbers = [10, 20]

print(id(numbers))

numbers.append(30)

print(id(numbers))
```

The identity remains the same because the existing list was modified.

Now consider a string:

```python
name = "Python"

print(id(name))

name = name + " Developer"

print(id(name))
```

The second assignment refers to the newly constructed string value.

**Note:** Object identity values are implementation-dependent. Do not use numeric `id()` values to predict memory addresses or assume that different values always have different IDs.

---

## 8. Difference Between == and is

These two operators are very important when understanding mutable and immutable objects.

### == (Equality Operator)

Checks whether two objects have equal values.

### is (Identity Operator)

Checks whether two references point to the same object.

Example:

```python
a = [10, 20, 30]
b = [10, 20, 30]

print(a == b)
print(a is b)
```

Output:

```text
True
False
```

Explanation:

- Both lists contain the same values.
- They are two separate list objects.
- Therefore, `==` returns `True`.
- `is` returns `False`.

Another example:

```python
a = [10, 20, 30]
b = a

print(a == b)
print(a is b)
```

Output:

```text
True
True
```

Both variables refer to the same list object.

**Best practice:** Use `==` for value comparison and `is` for identity checks. Use `is None` when checking for `None`.

---

## 9. Shallow Copy and Deep Copy

Copying is an important concept when working with mutable objects.

### A. Assignment

Assignment does not create a copy.

```python
a = [10, 20, 30]

b = a

b.append(40)

print(a)
print(b)
```

Both variables refer to the same list.

### B. Shallow Copy

A shallow copy creates a new outer object but does not recursively copy nested objects.

We can use:

- `copy()`
- Slicing
- `list()`
- `copy.copy()`

Example:

```python
a = [10, 20, 30]

b = a.copy()

b.append(40)

print(a)
print(b)
```

Output:

```text
[10, 20, 30]
[10, 20, 30, 40]
```

Here, the two outer lists are separate objects.

### Nested List Example

```python
import copy

a = [[10, 20], [30, 40]]

b = copy.copy(a)

b[0].append(50)

print(a)
print(b)
```

Output:

```text
[[10, 20, 50], [30, 40]]
[[10, 20, 50], [30, 40]]
```

Why?

The outer list is copied, but the inner lists are shared.

### C. Deep Copy

A deep copy recursively copies nested objects.

Example:

```python
import copy

a = [[10, 20], [30, 40]]

b = copy.deepcopy(a)

b[0].append(50)

print(a)
print(b)
```

Output:

```text
[[10, 20], [30, 40]]
[[10, 20, 50], [30, 40]]
```

Now the nested lists are independent copies.

---

## 10. Mutable Default Argument Problem

This is a common Python interview question.

Consider:

```python
def add_item(item, items=[]):
    items.append(item)
    return items

print(add_item(10))
print(add_item(20))
print(add_item(30))
```

Output:

```text
[10]
[10, 20]
[10, 20, 30]
```

### Why does this happen?

The default list is created once when Python executes the function definition.

The same list is reused across calls that omit the `items` argument.

### Correct Approach

Use `None` as the default value and create a new list inside the function.

```python
def add_item(item, items=None):
    if items is None:
        items = []

    items.append(item)
    return items

print(add_item(10))
print(add_item(20))
print(add_item(30))
```

Output:

```text
[10]
[20]
[30]
```

Each call gets a new list.

---

## 11. Mutable and Immutable Objects in Functions

When passing an object to a function, Python passes an object reference.

Let's understand this with two examples.

### Mutable Object

```python
def update_list(numbers):
    numbers.append(100)

my_numbers = [10, 20, 30]

update_list(my_numbers)

print(my_numbers)
```

Output:

```text
[10, 20, 30, 100]
```

The function modifies the same list object.

### Immutable Object

```python
def update_number(number):
    number = number + 100

my_number = 10

update_number(my_number)

print(my_number)
```

Output:

```text
10
```

The function reassigns its local variable. It does not change the original integer object or the caller's variable.

---

## 12. FDE Connection: Why Does This Matter?

As a Forward-Deployed Engineer, you may build:

- API integrations
- Customer data processing systems
- Automation scripts
- AI agents
- RAG pipelines
- Data transformation applications

Mutable and immutable objects can affect how data is shared and modified.

### Example: Customer Data Processing

```python
customer = {
    "name": "Arun",
    "orders": [101, 102]
}

def add_order(customer_data):
    customer_data["orders"].append(103)

add_order(customer)

print(customer)
```

Output:

```text
{
    'name': 'Arun',
    'orders': [101, 102, 103]
}
```

The function modified the original dictionary and its nested list.

### Potential Integration Problem

Imagine two application components share the same customer dictionary.

If one component modifies it unexpectedly, another component may receive changed data.

To avoid this:

1. Understand whether objects are shared.
2. Use shallow or deep copies when appropriate.
3. Avoid unintended mutation.
4. Validate data before modifying it.
5. Be careful when passing mutable objects between functions.

---

## 13. Practice Tasks

### Beginner Level

**Task 1:** Create a list and modify it using `append()`.

**Task 2:** Create a string and attempt to change one of its characters.

**Task 3:** Create two variables pointing to the same list and modify the list through one variable.

**Task 4:** Create two independent lists with identical values. Compare them using `==` and `is`.

### Intermediate Level

**Task 5:** Demonstrate the difference between assignment and shallow copying.

**Task 6:** Create a nested list and demonstrate shallow copy behavior.

**Task 7:** Use `copy.deepcopy()` to create an independent nested list.

**Task 8:** Fix the mutable default argument problem in a function.

### FDE-Oriented Practice

**Task 9:** Create a customer dictionary with a nested orders list. Pass it to a function and add an order.

**Task 10:** Create a copy of customer data and modify the copy without affecting the original.

**Task 11:** Build a function that receives a list of customer records and returns a new list without modifying the original.

---

## 14. Quick Revision

| Concept | Meaning |
|---|---|
| Mutable | Contents can be changed after creation |
| Immutable | Contents cannot be changed after creation |
| `id()` | Returns object identity |
| `==` | Compares values |
| `is` | Compares object identity |
| Assignment | Creates another reference to an object |
| Shallow Copy | Copies the outer object, shares nested objects |
| Deep Copy | Recursively copies nested objects |
| `append()` | Adds an element to an existing list |
| `copy()` | Creates a shallow copy of a list |

### Common Mutable Types

- List
- Dictionary
- Set
- Bytearray

### Common Immutable Types

- Integer
- Float
- Complex
- Boolean
- String
- Tuple
- Frozenset
- Bytes

---

## 15. Self-Assessment

Try answering these questions without referring to the notes.

1. What is a mutable object?
2. What is an immutable object?
3. Give four examples of mutable types.
4. Give four examples of immutable types.
5. Why can a list be modified but a string cannot?
6. What is the difference between `==` and `is`?
7. What happens when two variables refer to the same list?
8. Does assignment create a copy of an object?
9. What is a shallow copy?
10. What is a deep copy?
11. Why is a mutable default argument dangerous?
12. Why does modifying a list inside a function affect the original list?
13. Why does reassigning an integer inside a function not change the caller's variable?
14. How can unexpected mutation affect a customer integration?

---


