
# Python Lists – Creation, Access, Indexing and Slicing

**Suggested filename:** `31_lists_creation_access_indexing_and_slicing.md`

---

## 1. Introduction to Lists

A list is a built-in Python data structure used to store multiple values in a single variable.

Lists are:

- Ordered – elements maintain their position.
- Mutable – elements can be modified after creation.
- Indexed – each element has a position.
- Dynamic – elements can be added or removed.
- Flexible – different data types can be stored together.
- Allow duplicates – the same value can appear multiple times.

### Real-world analogy

Imagine an employee management system.

You need to store the names of employees:

```python
employee1 = "Arun"
employee2 = "Kumar"
employee3 = "Siva"
```

Managing many individual variables becomes difficult.

Instead, you can store all employee names in one list:

```python
employees = ["Arun", "Kumar", "Siva"]
```

Now you can access and manage the employees using a single variable.

---

## 2. Creating a List

Lists are created using square brackets `[]`.

### Example 1: Creating a list of strings

```python
employees = ["Arun", "Kumar", "Siva"]

print(employees)
```

**Output:**

```text
['Arun', 'Kumar', 'Siva']
```

### Example 2: Creating a list of integers

```python
ages = [25, 27, 30, 35]

print(ages)
```

**Output:**

```text
[25, 27, 30, 35]
```

### Example 3: Creating a list of mixed data types

```python
employee = ["Arun", 27, 45000.50, True]

print(employee)
```

**Output:**

```text
['Arun', 27, 45000.5, True]
```

Python allows different data types in the same list.

However, in real applications, keeping a consistent structure is usually easier to maintain.

### Example 4: Creating an empty list

```python
employees = []

print(employees)
```

**Output:**

```text
[]
```

An empty list is useful when you want to collect values later.

### Example 5: Using the `list()` constructor

You can also create a list using the built-in `list()` function.

```python
numbers = list((10, 20, 30))

print(numbers)
```

**Output:**

```text
[10, 20, 30]
```

You can convert other iterables into lists:

```python
letters = list("PYTHON")

print(letters)
```

**Output:**

```text
['P', 'Y', 'T', 'H', 'O', 'N']
```

---

## 3. Understanding List Indexing

Every element in a list has an index.

Python uses zero-based indexing.

This means the first element starts at index `0`, not index `1`.

Consider this list:

```python
languages = ["Python", "Java", "JavaScript", "C++"]
```

### Positive indexing

| Element | Positive index |
|---|---:|
| Python | 0 |
| Java | 1 |
| JavaScript | 2 |
| C++ | 3 |

### Visual representation

```text
Values:   Python    Java    JavaScript    C++
Index:       0        1          2          3
```

### Accessing elements using positive indexes

```python
languages = ["Python", "Java", "JavaScript", "C++"]

print(languages[0])
print(languages[1])
print(languages[2])
print(languages[3])
```

**Output:**

```text
Python
Java
JavaScript
C++
```

### Important

List indexing starts from zero.

If a list contains four elements, the valid positive indexes are:

```text
0, 1, 2, 3
```

Trying to access index `4` raises an `IndexError`.

---

## 4. Negative Indexing

Python also supports negative indexing.

Negative indexing starts from the end of the list.

The last element has index `-1`.

Consider:

```python
languages = ["Python", "Java", "JavaScript", "C++"]
```

| Element | Positive index | Negative index |
|---|---:|---:|
| Python | 0 | -4 |
| Java | 1 | -3 |
| JavaScript | 2 | -2 |
| C++ | 3 | -1 |

### Example

```python
languages = ["Python", "Java", "JavaScript", "C++"]

print(languages[-1])
print(languages[-2])
print(languages[-3])
print(languages[-4])
```

**Output:**

```text
C++
JavaScript
Java
Python
```

### When is negative indexing useful?

Imagine an application receives a list of recent transactions.

```python
transactions = [1000, 2500, 3000, 4500]

latest_transaction = transactions[-1]

print(latest_transaction)
```

**Output:**

```text
4500
```

You can access the last element without calculating its positive index.

---

## 5. Accessing List Elements Using Variables

You can store an index in a variable and use it to access an element.

```python
employees = ["Arun", "Kumar", "Siva"]

index = 1

print(employees[index])
```

**Output:**

```text
Kumar
```

This is useful when the index is calculated dynamically.

### Example: Accessing the last element using `len()`

```python
employees = ["Arun", "Kumar", "Siva"]

last_index = len(employees) - 1

print(employees[last_index])
```

**Output:**

```text
Siva
```

Explanation:

- `len(employees)` returns `3`.
- The last valid positive index is `3 - 1`.
- Therefore, the last index is `2`.

---

## 6. Understanding List Slicing

Slicing allows you to extract multiple elements from a list.

Instead of accessing one element, you can retrieve a portion of the list.

### Syntax

```python
list_name[start:stop:step]
```

| Parameter | Meaning |
|---|---|
| `start` | Starting index |
| `stop` | Ending boundary, excluded |
| `step` | Number of positions to move between selected elements |

The `start` and `step` values are optional. The `stop` boundary is required in the slice syntax, although it can be omitted to use the default boundary.

Consider:

```python
numbers = [10, 20, 30, 40, 50, 60]
```

### 6.1 Basic slicing

```python
numbers = [10, 20, 30, 40, 50, 60]

print(numbers[1:4])
```

**Output:**

```text
[20, 30, 40]
```

Explanation:

- Start index = `1`
- Stop index = `4`
- Index `4` is excluded.
- Elements at indexes `1`, `2`, and `3` are returned.

### Visual representation

```text
Values:  10   20   30   40   50   60
Index:    0    1    2    3    4    5

Slice:        [---------]
              20  30  40
```

Remember: the stop index is excluded.

---

## 7. Slicing with an Omitted Start

If you omit the start index, Python starts from the beginning.

```python
numbers = [10, 20, 30, 40, 50, 60]

print(numbers[:3])
```

**Output:**

```text
[10, 20, 30]
```

This is equivalent to:

```python
print(numbers[0:3])
```

---

## 8. Slicing with an Omitted Stop

If you omit the stop index, Python continues until the end.

```python
numbers = [10, 20, 30, 40, 50, 60]

print(numbers[2:])
```

**Output:**

```text
[30, 40, 50, 60]
```

This starts from index `2` and includes the remaining elements.

---

## 9. Slicing with Both Start and Stop Omitted

You can use a colon alone to retrieve all elements.

```python
numbers = [10, 20, 30, 40, 50, 60]

result = numbers[:]

print(result)
```

**Output:**

```text
[10, 20, 30, 40, 50, 60]
```

Important: this creates a shallow copy of the list, not another reference to the same outer list.

---

## 10. Slicing with Step

The step determines how many index positions Python moves between selected elements.

### Example 1: Step of 2

```python
numbers = [10, 20, 30, 40, 50, 60]

print(numbers[::2])
```

**Output:**

```text
[10, 30, 50]
```

Explanation:

- Start at index `0`.
- Move two positions at a time.
- Select indexes `0`, `2`, and `4`.

### Example 2: Step of 3

```python
numbers = [10, 20, 30, 40, 50, 60]

print(numbers[::3])
```

**Output:**

```text
[10, 40]
```

### Example 3: Starting from a specific index

```python
numbers = [10, 20, 30, 40, 50, 60]

print(numbers[1:6:2])
```

**Output:**

```text
[20, 40, 60]
```

---

## 11. Reverse a List Using Slicing

You can reverse the order of elements using a negative step.

```python
numbers = [10, 20, 30, 40, 50]

result = numbers[::-1]

print(result)
```

**Output:**

```text
[50, 40, 30, 20, 10]
```

Explanation:

- The step is `-1`.
- Python moves backward through the list.
- All elements are selected in reverse order.

### Another example

```python
languages = ["Python", "Java", "JavaScript"]

print(languages[::-1])
```

**Output:**

```text
['JavaScript', 'Java', 'Python']
```

Note: slicing creates a new list. It does not reverse the original list in place.

---

## 12. Slicing with Negative Indexes

Negative indexes can also be used in slicing.

```python
numbers = [10, 20, 30, 40, 50, 60]

print(numbers[-4:-1])
```

**Output:**

```text
[30, 40, 50]
```

Explanation:

| Element | Negative index |
|---|---:|
| 10 | -6 |
| 20 | -5 |
| 30 | -4 |
| 40 | -3 |
| 50 | -2 |
| 60 | -1 |

The slice starts at `-4` and stops before `-1`.

### Another example

```python
numbers = [10, 20, 30, 40, 50, 60]

print(numbers[-3:])
```

**Output:**

```text
[40, 50, 60]
```

---

## 13. Modifying List Elements Using Indexing

Lists are mutable.

This means you can change an element after creating the list.

```python
employees = ["Arun", "Kumar", "Siva"]

employees[1] = "Ravi"

print(employees)
```

**Output:**

```text
['Arun', 'Ravi', 'Siva']
```

Explanation:

- Index `1` originally contains `"Kumar"`.
- We assign `"Ravi"` to index `1`.
- The original list is modified.

### Modifying an element using a negative index

```python
employees = ["Arun", "Kumar", "Siva"]

employees[-1] = "Vijay"

print(employees)
```

**Output:**

```text
['Arun', 'Kumar', 'Vijay']
```

---

## 14. Modifying Multiple Elements Using Slicing

You can replace a range of elements using slice assignment.

```python
numbers = [10, 20, 30, 40, 50]

numbers[1:3] = [200, 300]

print(numbers)
```

**Output:**

```text
[10, 200, 300, 40, 50]
```

The elements at indexes `1` and `2` are replaced.

### Replacing with a different number of elements

```python
numbers = [10, 20, 30, 40, 50]

numbers[1:3] = [200, 300, 400]

print(numbers)
```

**Output:**

```text
[10, 200, 300, 400, 40, 50]
```

The list becomes longer because three elements replace two.

This is one reason Python lists are considered dynamic.

---

## 15. Accessing Nested Lists

A list can contain other lists.

This structure is called a nested list.

### Example

```python
employees = [
    ["Arun", 25, "Python Developer"],
    ["Kumar", 28, "Data Analyst"],
    ["Siva", 30, "AI Engineer"]
]

print(employees)
```

**Output:**

```text
[['Arun', 25, 'Python Developer'], ['Kumar', 28, 'Data Analyst'], ['Siva', 30, 'AI Engineer']]
```

### Accessing the first nested list

```python
print(employees[0])
```

**Output:**

```text
['Arun', 25, 'Python Developer']
```

### Accessing an element inside a nested list

```python
print(employees[0][0])
```

**Output:**

```text
Arun
```

Explanation:

- First `[0]` accesses the first employee record.
- Second `[0]` accesses the employee name.

### Accessing the employee's job role

```python
print(employees[2][2])
```

**Output:**

```text
AI Engineer
```

### Nested list structure

```text
employees
    |
    |-- Index 0 --> ["Arun", 25, "Python Developer"]
    |                    |       |          |
    |                    0       1          2
    |
    |-- Index 1 --> ["Kumar", 28, "Data Analyst"]
    |
    |-- Index 2 --> ["Siva", 30, "AI Engineer"]
```

---

## 16. Accessing List Elements Safely

Accessing an invalid index raises an `IndexError`.

### Example

```python
employees = ["Arun", "Kumar", "Siva"]

print(employees[5])
```

**Error:**

```text
IndexError: list index out of range
```

### Checking the length before accessing

```python
employees = ["Arun", "Kumar", "Siva"]

index = 5

if 0 <= index < len(employees):
    print(employees[index])
else:
    print("Invalid index")
```

**Output:**

```text
Invalid index
```

### Using try-except

```python
employees = ["Arun", "Kumar", "Siva"]

try:
    print(employees[5])
except IndexError:
    print("Employee does not exist")
```

**Output:**

```text
Employee does not exist
```

### Important difference: Indexing vs slicing

Invalid indexing raises an error:

```python
numbers = [10, 20, 30]

print(numbers[10])
```

But an out-of-range slice boundary is normally adjusted automatically:

```python
numbers = [10, 20, 30]

print(numbers[0:10])
```

**Output:**

```text
[10, 20, 30]
```

---

## 17. Lists and Object References

Python variables refer to objects.

Consider:

```python
numbers = [10, 20, 30]

another_numbers = numbers

another_numbers[0] = 100

print(numbers)
print(another_numbers)
```

**Output:**

```text
[100, 20, 30]
[100, 20, 30]
```

Why?

Both variables refer to the same list object.

### Creating a separate shallow copy

```python
numbers = [10, 20, 30]

another_numbers = numbers[:]

another_numbers[0] = 100

print(numbers)
print(another_numbers)
```

**Output:**

```text
[10, 20, 30]
[100, 20, 30]
```

The outer lists are now separate objects.

**Important:** Slicing creates a shallow copy. If the list contains nested mutable objects, those inner objects are still shared.

---

## 18. List Operations – A Quick Preview

This chapter focuses on creation, access, indexing, and slicing.

You will study list methods in detail in the next chapters.

For now, understand these common operations:

| Operation | Example | Purpose |
|---|---|---|
| Length | `len(numbers)` | Get number of elements |
| Membership | `20 in numbers` | Check whether a value exists |
| Concatenation | `list1 + list2` | Combine lists into a new list |
| Repetition | `numbers * 2` | Repeat list elements |
| Minimum | `min(numbers)` | Find smallest comparable value |
| Maximum | `max(numbers)` | Find largest comparable value |
| Sum | `sum(numbers)` | Calculate numeric total |

Example:

```python
numbers = [10, 20, 30]

print(len(numbers))
print(20 in numbers)
print(numbers + [40, 50])
print(numbers * 2)
```

**Output:**

```text
3
True
[10, 20, 30, 40, 50]
[10, 20, 30, 10, 20, 30]
```

---

## 19. Practical FDE Example: Processing API Records

Imagine an API returns multiple customer records.

For this learning example, assume the API response has already been converted into a Python list.

```python
customers = [
    {"id": 101, "name": "Arun", "city": "Chennai"},
    {"id": 102, "name": "Kumar", "city": "Bangalore"},
    {"id": 103, "name": "Siva", "city": "Coimbatore"},
    {"id": 104, "name": "Ravi", "city": "Chennai"}
]
```

### Accessing the first customer

```python
print(customers[0])
```

**Output:**

```text
{'id': 101, 'name': 'Arun', 'city': 'Chennai'}
```

### Accessing a specific customer's name

```python
print(customers[1]["name"])
```

**Output:**

```text
Kumar
```

### Getting the first two customers

```python
first_two_customers = customers[:2]

print(first_two_customers)
```

**Output:**

```text
[{'id': 101, 'name': 'Arun', 'city': 'Chennai'}, {'id': 102, 'name': 'Kumar', 'city': 'Bangalore'}]
```

### Getting the last two customers

```python
last_two_customers = customers[-2:]

print(last_two_customers)
```

**Output:**

```text
[{'id': 103, 'name': 'Siva', 'city': 'Coimbatore'}, {'id': 104, 'name': 'Ravi', 'city': 'Chennai'}]
```

### Why is this useful in FDE work?

Forward-Deployed Engineers often integrate multiple systems.

API responses commonly contain collections of records.

Understanding lists helps you:

- Access individual API records.
- Retrieve selected records.
- Process customer information.
- Work with nested JSON-like structures.
- Prepare data for AI pipelines.
- Implement basic pagination and batch processing.

In production systems, large datasets should generally be paginated or processed in batches at the API or database layer instead of downloading everything and slicing locally.

---

## 20. Common Mistakes

### Mistake 1: Forgetting that indexing starts at zero

```python
numbers = [10, 20, 30]

print(numbers[1])
```

Output:

```text
20
```

Index `1` is the second element.

### Mistake 2: Using an invalid index

```python
numbers = [10, 20, 30]

print(numbers[3])
```

This raises `IndexError`.

The last valid positive index is `2`.

### Mistake 3: Assuming the stop index is included

```python
numbers = [10, 20, 30, 40, 50]

print(numbers[1:4])
```

Output:

```text
[20, 30, 40]
```

Index `4` is excluded.

### Mistake 4: Using zero as the slicing step

```python
numbers = [10, 20, 30]

print(numbers[::0])
```

This raises:

```text
ValueError: slice step cannot be zero
```

### Mistake 5: Thinking slicing modifies the original list

```python
numbers = [10, 20, 30, 40]

result = numbers[1:3]

print(numbers)
print(result)
```

Output:

```text
[10, 20, 30, 40]
[20, 30]
```

Slicing returns a new list.

### Mistake 6: Confusing assignment with copying

```python
numbers = [10, 20, 30]

new_numbers = numbers

new_numbers[0] = 100

print(numbers)
```

Output:

```text
[100, 20, 30]
```

Assignment does not create a copy. Both names refer to the same list.

---

## 21. Practice Exercises

### Beginner Level

1. Create a list containing five programming languages.
2. Create a list containing five integer values.
3. Access the first and last elements.
4. Access the third element using positive indexing.
5. Access the second-last element using negative indexing.
6. Find the length of a list using `len()`.

### Intermediate Level

7. Extract the first three elements using slicing.
8. Extract the last three elements using slicing.
9. Retrieve elements between index `2` and index `5`.
10. Retrieve every second element using step.
11. Reverse a list using slicing.
12. Replace the second element with a new value.
13. Replace multiple elements using slice assignment.
14. Create a nested list containing employee details and access one employee's job role.
15. Create a separate shallow copy of a list and modify it.

### FDE Practical Level

16. Create a list containing five customer records.
17. Access the third customer record.
18. Extract the first two records.
19. Extract the last two records.
20. Access the email or name field inside a nested customer record.
21. Simulate processing a batch of API records by extracting a selected slice.

---

## 22. Quick Revision

| Concept | Syntax | Purpose |
|---|---|---|
| Create list | `items = [10, 20, 30]` | Store multiple values |
| Empty list | `items = []` | Create an empty list |
| List constructor | `list(iterable)` | Convert an iterable to a list |
| Positive indexing | `items[0]` | Access from the beginning |
| Negative indexing | `items[-1]` | Access from the end |
| Length | `len(items)` | Count elements |
| Basic slicing | `items[1:4]` | Extract a portion |
| Start omitted | `items[:3]` | Start from beginning |
| Stop omitted | `items[2:]` | Continue to the end |
| Step | `items[::2]` | Select every second element |
| Reverse | `items[::-1]` | Return elements in reverse order |
| Modify element | `items[0] = 100` | Change an element |
| Slice assignment | `items[1:3] = [20, 30]` | Replace a portion |
| Nested access | `items[0][1]` | Access an inner element |
| Shallow copy | `items[:]` | Copy the outer list |

---

## 23. Self-Assessment

Try answering these questions without referring to the notes.

1. What is a list in Python?
2. What are the main characteristics of lists?
3. Why does Python use zero-based indexing?
4. What is the difference between positive and negative indexing?
5. What happens when you access an invalid index?
6. Explain the syntax `list[start:stop:step]`.
7. Why is the stop index excluded in slicing?
8. What does `numbers[::-1]` do?
9. What happens when the slicing step is zero?
10. How can you modify an element in a list?
11. What is a nested list?
12. What is the difference between `new_list = old_list` and `new_list = old_list[:]`?
13. Is slicing a deep copy or a shallow copy?
14. How can list slicing help process API records?

---

## 24. Learning Outcome

After completing this chapter, you should be able to:

- Create lists using square brackets and the `list()` constructor.
- Understand list characteristics.
- Access elements using positive and negative indexes.
- Extract portions of lists using slicing.
- Use start, stop, and step parameters.
- Reverse lists using slicing.
- Modify individual and multiple elements.
- Access nested list elements.
- Understand list references and shallow copying.
- Apply lists to basic API record-processing scenarios.


