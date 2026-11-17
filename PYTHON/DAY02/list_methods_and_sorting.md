
# Python Lists – List Methods and Sorting

**Suggested filename:** `32_list_methods_and_sorting.md`

---

## 1. Introduction

In the previous chapter, we learned how to create lists, access elements, use indexing, and perform slicing.

Now, we will learn how to manipulate lists using built-in list methods.

Consider this employee list:

```python
employees = ["Arun", "Kumar", "Siva"]
```

Suppose you want to:

- Add a new employee.
- Insert an employee at a specific position.
- Remove an employee.
- Delete an element using its index.
- Search for an employee.
- Sort employee names alphabetically.
- Reverse the order of elements.

Python provides built-in list methods to perform these operations.

---

# PART 1: ADDING ELEMENTS

## 2. `append()` Method

### What is `append()`?

The `append()` method adds a single element to the end of an existing list.

### Syntax

```python
list_name.append(element)
```

### Example

```python
employees = ["Arun", "Kumar", "Siva"]

employees.append("Ravi")

print(employees)
```

**Output:**

```text
['Arun', 'Kumar', 'Siva', 'Ravi']
```

### Explanation

Initially:

```text
['Arun', 'Kumar', 'Siva']
```

After `append("Ravi")`:

```text
['Arun', 'Kumar', 'Siva', 'Ravi']
```

The new element is added at the end.

### Appending different data types

```python
data = [10, 20, 30]

data.append(40)
data.append("Python")
data.append(True)

print(data)
```

**Output:**

```text
[10, 20, 30, 40, 'Python', True]
```

### Important: `append()` adds one object

```python
numbers = [10, 20, 30]

numbers.append([40, 50])

print(numbers)
```

**Output:**

```text
[10, 20, 30, [40, 50]]
```

Notice that `[40, 50]` becomes one nested list element.

---

## 3. `extend()` Method

### What is `extend()`?

The `extend()` method adds each element from an iterable to the end of an existing list.

### Syntax

```python
list_name.extend(iterable)
```

### Example

```python
numbers = [10, 20, 30]

numbers.extend([40, 50])

print(numbers)
```

**Output:**

```text
[10, 20, 30, 40, 50]
```

### Difference between `append()` and `extend()`

```python
numbers1 = [10, 20, 30]
numbers2 = [10, 20, 30]

numbers1.append([40, 50])
numbers2.extend([40, 50])

print(numbers1)
print(numbers2)
```

**Output:**

```text
[10, 20, 30, [40, 50]]
[10, 20, 30, 40, 50]
```

| Feature | `append()` | `extend()` |
|---|---|---|
| Purpose | Adds one object | Adds elements from an iterable |
| Adds a nested list? | Yes, as one element | No, adds its individual elements |
| Changes original list? | Yes | Yes |
| Return value | `None` | `None` |

### Extending with a string

```python
letters = ["A", "B"]

letters.extend("CD")

print(letters)
```

**Output:**

```text
['A', 'B', 'C', 'D']
```

A string is iterable, so Python adds its individual characters.

---

## 4. `insert()` Method

### What is `insert()`?

The `insert()` method adds an element at a specific index.

### Syntax

```python
list_name.insert(index, element)
```

### Example

```python
employees = ["Arun", "Siva", "Ravi"]

employees.insert(1, "Kumar")

print(employees)
```

**Output:**

```text
['Arun', 'Kumar', 'Siva', 'Ravi']
```

### Explanation

Before insertion:

```text
Index:    0       1       2
Value:  Arun    Siva    Ravi
```

After insertion:

```text
Index:    0       1       2       3
Value:  Arun   Kumar    Siva    Ravi
```

### Inserting at the beginning

```python
numbers = [20, 30, 40]

numbers.insert(0, 10)

print(numbers)
```

**Output:**

```text
[10, 20, 30, 40]
```

### Important

If the insertion index is larger than the list length, Python inserts the element at the end.

A negative insertion index is interpreted relative to the end, with the actual insertion position bounded by the list.

---

# PART 2: REMOVING ELEMENTS

## 5. `remove()` Method

### What is `remove()`?

The `remove()` method removes the first occurrence of a specified value.

### Syntax

```python
list_name.remove(value)
```

### Example

```python
numbers = [10, 20, 30, 20, 40]

numbers.remove(20)

print(numbers)
```

**Output:**

```text
[10, 30, 20, 40]
```

### Explanation

- Python searches for the value `20`.
- It finds the first occurrence.
- It removes that element.
- The second occurrence remains.

### Removing a string

```python
employees = ["Arun", "Kumar", "Siva"]

employees.remove("Kumar")

print(employees)
```

**Output:**

```text
['Arun', 'Siva']
```

### What happens if the value does not exist?

```python
numbers = [10, 20, 30]

numbers.remove(50)
```

**Error:**

```text
ValueError: list.remove(x): x not in list
```

### Safe removal

```python
numbers = [10, 20, 30]

if 50 in numbers:
    numbers.remove(50)
else:
    print("Value not found")
```

**Output:**

```text
Value not found
```

---

## 6. `pop()` Method

### What is `pop()`?

The `pop()` method removes an element from a list and returns the removed value.

### Syntax

```python
list_name.pop(index)
```

If you do not provide an index, it removes the last element.

### Example 1: Removing the last element

```python
numbers = [10, 20, 30, 40]

removed_value = numbers.pop()

print("Removed:", removed_value)
print("Updated list:", numbers)
```

**Output:**

```text
Removed: 40
Updated list: [10, 20, 30]
```

### Example 2: Removing an element by index

```python
numbers = [10, 20, 30, 40]

removed_value = numbers.pop(1)

print("Removed:", removed_value)
print("Updated list:", numbers)
```

**Output:**

```text
Removed: 20
Updated list: [10, 30, 40]
```

### Example 3: Using a negative index

```python
numbers = [10, 20, 30, 40]

removed_value = numbers.pop(-2)

print(removed_value)
print(numbers)
```

**Output:**

```text
30
[10, 20, 40]
```

### `remove()` vs `pop()`

| Feature | `remove()` | `pop()` |
|---|---|---|
| Removes based on | Value | Index |
| Returns removed element | No, returns `None` | Yes |
| Default behaviour | Requires a value | Removes last element |
| If target is missing | `ValueError` | `IndexError` for invalid index |

---

## 7. `clear()` Method

### What is `clear()`?

The `clear()` method removes all elements from a list.

### Syntax

```python
list_name.clear()
```

### Example

```python
employees = ["Arun", "Kumar", "Siva"]

employees.clear()

print(employees)
```

**Output:**

```text
[]
```

### Important: `clear()` vs assigning an empty list

```python
numbers = [10, 20, 30]
another_numbers = numbers

numbers.clear()

print(numbers)
print(another_numbers)
```

**Output:**

```text
[]
[]
```

Both variables refer to the same list object, so both observe the cleared list.

Compare with:

```python
numbers = [10, 20, 30]
another_numbers = numbers

numbers = []

print(numbers)
print(another_numbers)
```

**Output:**

```text
[]
[10, 20, 30]
```

Here, `numbers = []` rebinds the variable to a new list. It does not clear the original list.

---

# PART 3: SEARCHING AND COUNTING

## 8. `index()` Method

### What is `index()`?

The `index()` method returns the index of the first occurrence of a specified value.

### Syntax

```python
list_name.index(value)
```

You can also specify an optional start and stop range:

```python
list_name.index(value, start, stop)
```

### Example

```python
languages = ["Python", "Java", "C++", "JavaScript"]

position = languages.index("C++")

print(position)
```

**Output:**

```text
2
```

### Searching for a repeated value

```python
numbers = [10, 20, 30, 20, 40]

position = numbers.index(20)

print(position)
```

**Output:**

```text
1
```

It returns the first occurrence.

### Searching from a specific position

```python
numbers = [10, 20, 30, 20, 40]

position = numbers.index(20, 2)

print(position)
```

**Output:**

```text
3
```

Python starts searching from index `2`.

### If the value does not exist

```python
numbers = [10, 20, 30]

print(numbers.index(50))
```

This raises:

```text
ValueError: 50 is not in list
```

### Safe searching

```python
numbers = [10, 20, 30]

if 20 in numbers:
    print(numbers.index(20))
else:
    print("Value not found")
```

**Output:**

```text
1
```

---

## 9. `count()` Method

### What is `count()`?

The `count()` method returns the number of times a particular value appears in a list.

### Syntax

```python
list_name.count(value)
```

### Example

```python
numbers = [10, 20, 30, 20, 40, 20]

result = numbers.count(20)

print(result)
```

**Output:**

```text
3
```

### Counting strings

```python
languages = [
    "Python",
    "Java",
    "Python",
    "JavaScript",
    "Python"
]

print(languages.count("Python"))
```

**Output:**

```text
3
```

### Counting Boolean values: an important Python detail

```python
values = [True, 1, False, 0, True]

print(values.count(1))
```

**Output:**

```text
2
```

Why?

In Python:

```python
True == 1
False == 0
```

List methods that compare values using equality can therefore treat these values as equal.

---

# PART 4: SORTING AND REVERSING

## 10. `sort()` Method

### What is `sort()`?

The `sort()` method sorts the elements of a list in place.

By default, it sorts in ascending order.

### Syntax

```python
list_name.sort()
```

### Example 1: Sorting numbers

```python
numbers = [50, 10, 40, 20, 30]

numbers.sort()

print(numbers)
```

**Output:**

```text
[10, 20, 30, 40, 50]
```

### Example 2: Sorting strings

```python
languages = ["Python", "Java", "C++", "JavaScript"]

languages.sort()

print(languages)
```

**Output:**

```text
['C++', 'Java', 'JavaScript', 'Python']
```

Strings are sorted lexicographically, based on their character values.

### Example 3: Descending order

Use `reverse=True`.

```python
numbers = [50, 10, 40, 20, 30]

numbers.sort(reverse=True)

print(numbers)
```

**Output:**

```text
[50, 40, 30, 20, 10]
```

### Example 4: Sorting with mixed case

```python
names = ["arun", "Kumar", "siva", "Ravi"]

names.sort()

print(names)
```

**Output:**

```text
['Kumar', 'Ravi', 'arun', 'siva']
```

By default, string sorting is case-sensitive because uppercase and lowercase characters have different Unicode code points.

To sort without considering case:

```python
names = ["arun", "Kumar", "siva", "Ravi"]

names.sort(key=str.lower)

print(names)
```

**Output:**

```text
['arun', 'Kumar', 'Ravi', 'siva']
```

### Important: `sort()` returns `None`

```python
numbers = [30, 10, 20]

result = numbers.sort()

print(result)
print(numbers)
```

**Output:**

```text
None
[10, 20, 30]
```

Do not write:

```python
numbers = numbers.sort()
```

That would assign `None` to `numbers`.

---

## 11. `sorted()` Function

### What is `sorted()`?

`sorted()` is a built-in Python function that returns a new sorted list without modifying the original iterable.

### Syntax

```python
sorted(iterable, key=None, reverse=False)
```

### Example

```python
numbers = [50, 10, 40, 20, 30]

result = sorted(numbers)

print("Original:", numbers)
print("Sorted:", result)
```

**Output:**

```text
Original: [50, 10, 40, 20, 30]
Sorted: [10, 20, 30, 40, 50]
```

### Descending order

```python
numbers = [50, 10, 40, 20, 30]

result = sorted(numbers, reverse=True)

print(result)
```

**Output:**

```text
[50, 40, 30, 20, 10]
```

### Difference between `sort()` and `sorted()`

| Feature | `sort()` | `sorted()` |
|---|---|---|
| Type | List method | Built-in function |
| Modifies original list | Yes | No |
| Returns | `None` | New sorted list |
| Works with | Lists | Any iterable |
| Supports descending order | Yes | Yes |
| Supports `key` | Yes | Yes |

### When should you use each?

Use `sort()` when:

- You want to change the original list.
- You do not need to preserve the original order.

Use `sorted()` when:

- You want to preserve the original iterable.
- You need a separate sorted result.
- You want to sort tuples, strings, or other iterables into a list.

---

## 12. Sorting with the `key` Parameter

The `key` parameter allows you to define how Python should compare elements.

### Example 1: Sorting strings by length

```python
names = ["Arun", "Kumar", "Siva", "Christopher"]

names.sort(key=len)

print(names)
```

**Output:**

```text
['Arun', 'Siva', 'Kumar', 'Christopher']
```

Explanation:

Python calculates the length of each string and sorts based on that length.

### Example 2: Sorting by length in descending order

```python
names = ["Arun", "Kumar", "Siva", "Christopher"]

names.sort(key=len, reverse=True)

print(names)
```

**Output:**

```text
['Christopher', 'Kumar', 'Arun', 'Siva']
```

### Example 3: Sorting without case sensitivity

```python
names = ["python", "Java", "c++", "React"]

result = sorted(names, key=str.lower)

print(result)
```

**Output:**

```text
['c++', 'Java', 'python', 'React']
```

---

## 13. Sorting a List of Dictionaries

In real-world applications, data is often represented as a list of dictionaries.

For example:

```python
employees = [
    {"name": "Arun", "salary": 45000},
    {"name": "Kumar", "salary": 60000},
    {"name": "Siva", "salary": 50000}
]
```

### Sorting employees by salary

```python
employees.sort(key=lambda employee: employee["salary"])

print(employees)
```

**Output:**

```text
[
    {'name': 'Arun', 'salary': 45000},
    {'name': 'Siva', 'salary': 50000},
    {'name': 'Kumar', 'salary': 60000}
]
```

### Sorting by salary in descending order

```python
employees.sort(
    key=lambda employee: employee["salary"],
    reverse=True
)

print(employees)
```

**Output:**

```text
[
    {'name': 'Kumar', 'salary': 60000},
    {'name': 'Siva', 'salary': 50000},
    {'name': 'Arun', 'salary': 45000}
]
```

### Understanding the lambda function

```python
lambda employee: employee["salary"]
```

This tells Python to use the salary value as the sorting key for each employee dictionary.

You will learn lambda functions in detail in a later chapter.

---

## 14. `reverse()` Method

### What is `reverse()`?

The `reverse()` method reverses the order of elements in the original list.

### Syntax

```python
list_name.reverse()
```

### Example

```python
numbers = [10, 20, 30, 40, 50]

numbers.reverse()

print(numbers)
```

**Output:**

```text
[50, 40, 30, 20, 10]
```

### Important: `reverse()` is not the same as sorting descending

```python
numbers = [30, 10, 40, 20]

numbers.reverse()

print(numbers)
```

**Output:**

```text
[20, 40, 10, 30]
```

It simply reverses the existing order. It does not arrange the numbers from largest to smallest.

For descending sorting:

```python
numbers = [30, 10, 40, 20]

numbers.sort(reverse=True)

print(numbers)
```

**Output:**

```text
[40, 30, 20, 10]
```

---

## 15. `copy()` Method

### What is `copy()`?

The `copy()` method creates a shallow copy of a list.

### Syntax

```python
new_list = original_list.copy()
```

### Example

```python
numbers = [10, 20, 30]

new_numbers = numbers.copy()

new_numbers.append(40)

print(numbers)
print(new_numbers)
```

**Output:**

```text
[10, 20, 30]
[10, 20, 30, 40]
```

The two outer lists are separate objects.

### Important: Shallow copy

Consider a nested list:

```python
original = [[10, 20], [30, 40]]

copied = original.copy()

copied[0].append(99)

print(original)
print(copied)
```

**Output:**

```text
[[10, 20, 99], [30, 40]]
[[10, 20, 99], [30, 40]]
```

Why?

`copy()` creates a new outer list, but the inner lists are still shared.

For an independent deep copy of nested mutable structures, Python provides the `copy` module:

```python
import copy

original = [[10, 20], [30, 40]]

copied = copy.deepcopy(original)

copied[0].append(99)

print(original)
print(copied)
```

**Output:**

```text
[[10, 20], [30, 40]]
[[10, 20, 99], [30, 40]]
```

---

# PART 5: COMPLETE LIST METHODS REFERENCE

## 16. Important List Methods

| Method | Purpose | Example |
|---|---|---|
| `append()` | Add one element at the end | `items.append(10)` |
| `extend()` | Add elements from an iterable | `items.extend([10, 20])` |
| `insert()` | Insert an element at an index | `items.insert(1, 10)` |
| `remove()` | Remove the first matching value | `items.remove(10)` |
| `pop()` | Remove and return an element | `items.pop()` |
| `clear()` | Remove all elements | `items.clear()` |
| `index()` | Find the first matching index | `items.index(10)` |
| `count()` | Count occurrences | `items.count(10)` |
| `sort()` | Sort the original list | `items.sort()` |
| `reverse()` | Reverse the original list | `items.reverse()` |
| `copy()` | Create a shallow copy | `items.copy()` |

### Important distinction

Most list methods that modify the list return `None`.

Examples:

- `append()`
- `extend()`
- `insert()`
- `remove()`
- `sort()`
- `reverse()`
- `clear()`

Methods such as `pop()`, `index()`, and `count()` return useful values.

---

## 17. Time Complexity of Common List Operations

Understanding performance is important when working with large datasets.

Let `n` represent the number of elements in a list.

| Operation | Typical time complexity |
|---|---|
| Access by index | O(1) |
| Update by index | O(1) |
| Append | O(1) amortized |
| Extend by k elements | O(k) amortized |
| Insert at beginning | O(n) |
| Remove by value | O(n) |
| Pop last element | O(1) |
| Pop from beginning | O(n) |
| Search using `in` | O(n) |
| Index search | O(n) |
| Count | O(n) |
| Sort | O(n log n) |
| Reverse | O(n) |
| Copy | O(n) |

**Note:** These are typical complexity characteristics for Python lists. Append is amortized O(1), meaning occasional resizing operations can take longer.

Python's built-in sorting algorithm is Timsort. Its performance can be close to O(n) on already ordered data and O(n log n) in the general worst case.

---

## 18. Practical FDE Example: Processing Customer Records

Imagine you receive customer records from an external API.

```python
customers = [
    {"id": 101, "name": "Arun", "age": 25, "city": "Chennai"},
    {"id": 102, "name": "Kumar", "age": 30, "city": "Bangalore"},
    {"id": 103, "name": "Siva", "age": 28, "city": "Chennai"},
    {"id": 104, "name": "Ravi", "age": 24, "city": "Coimbatore"}
]
```

### Task 1: Add a new customer

```python
new_customer = {
    "id": 105,
    "name": "Vijay",
    "age": 27,
    "city": "Chennai"
}

customers.append(new_customer)

print(len(customers))
```

**Output:**

```text
5
```

### Task 2: Find the customer with ID 103

```python
customer = next(
    (item for item in customers if item["id"] == 103),
    None
)

print(customer)
```

**Output:**

```text
{'id': 103, 'name': 'Siva', 'age': 28, 'city': 'Chennai'}
```

### Task 3: Sort customers by age

```python
customers.sort(key=lambda customer: customer["age"])

for customer in customers:
    print(customer["name"], customer["age"])
```

**Output:**

```text
Ravi 24
Arun 25
Vijay 27
Siva 28
Kumar 30
```

### Task 4: Create a separate sorted result

```python
sorted_customers = sorted(
    customers,
    key=lambda customer: customer["name"]
)

for customer in sorted_customers:
    print(customer["name"])
```

**Output:**

```text
Arun
Kumar
Ravi
Siva
Vijay
```

### FDE relevance

These operations are commonly used when:

- Integrating customer data from APIs.
- Combining records from multiple systems.
- Preparing data before sending it to an AI model.
- Sorting search results.
- Removing duplicate or unwanted records.
- Building data transformation pipelines.

For large-scale production systems, consider database queries, pagination, streaming, and efficient data structures rather than loading and manipulating every record in memory.

---

## 19. Common Mistakes

### Mistake 1: Confusing `append()` and `extend()`

```python
numbers = [1, 2, 3]

numbers.append([4, 5])

print(numbers)
```

Output:

```text
[1, 2, 3, [4, 5]]
```

Use `extend()` if you want individual elements.

### Mistake 2: Expecting `remove()` to remove all duplicates

```python
numbers = [10, 20, 20, 30]

numbers.remove(20)

print(numbers)
```

Output:

```text
[10, 20, 30]
```

Only the first matching value is removed.

### Mistake 3: Confusing `remove()` and `pop()`

```python
numbers = [10, 20, 30]

numbers.remove(20)
```

Removes a value.

```python
numbers = [10, 20, 30]

numbers.pop(1)
```

Removes an element at an index.

### Mistake 4: Assigning the result of `sort()`

Incorrect:

```python
numbers = [30, 10, 20]

numbers = numbers.sort()

print(numbers)
```

Output:

```text
None
```

Correct:

```python
numbers = [30, 10, 20]

numbers.sort()

print(numbers)
```

### Mistake 5: Assuming `reverse()` sorts descending

`reverse()` reverses the current order. Use `sort(reverse=True)` for descending sorting.

### Mistake 6: Assuming `copy()` creates a deep copy

`copy()` creates a shallow copy. Nested mutable elements remain shared.

### Mistake 7: Modifying a list while iterating over it

This can cause elements to be skipped or unexpected results.

Instead, create a new list when filtering:

```python
numbers = [10, 20, 30, 40, 50]

filtered_numbers = [
    number for number in numbers
    if number != 30
]

print(filtered_numbers)
```

**Output:**

```text
[10, 20, 40, 50]
```

List comprehensions will be covered in a later chapter.

---

## 20. Practice Exercises

### Beginner Level

1. Create a list of five programming languages and append another language.
2. Extend a list with three additional numbers.
3. Insert an employee name at index 2.
4. Remove a particular value from a list.
5. Remove the last element using `pop()`.
6. Clear all elements from a list.
7. Count how many times `10` occurs in a list.
8. Find the index of `"Python"` in a language list.

### Intermediate Level

9. Sort a list of integers in ascending order.
10. Sort the same list in descending order.
11. Sort a list of names alphabetically without considering case.
12. Sort names based on their length.
13. Reverse a list without sorting it.
14. Create a shallow copy and modify the copied list.
15. Sort a list of dictionaries based on employee salary.
16. Find the first occurrence of a value starting from a specified index.

### FDE Practical Level

17. Create a list of customer dictionaries.
18. Add a new customer record.
19. Remove a customer using their ID.
20. Sort customer records based on age.
21. Sort customer records based on salary in descending order.
22. Create a separate sorted copy without modifying the original records.
23. Build a small employee management program using `append()`, `remove()`, `pop()`, `sort()`, and `copy()`.

---

## 21. Quick Revision

| Method / Function | What it does |
|---|---|
| `append(x)` | Adds one element |
| `extend(iterable)` | Adds multiple elements |
| `insert(i, x)` | Inserts at a position |
| `remove(x)` | Removes first matching value |
| `pop(i)` | Removes and returns an element |
| `clear()` | Removes all elements |
| `index(x)` | Returns the first matching index |
| `count(x)` | Counts occurrences |
| `sort()` | Sorts the original list |
| `sorted()` | Returns a new sorted list |
| `reverse()` | Reverses the original list |
| `copy()` | Creates a shallow copy |

---

## 22. Self-Assessment

1. What is the difference between `append()` and `extend()`?
2. What is the purpose of `insert()`?
3. Does `remove()` delete all duplicate values?
4. What does `pop()` return?
5. What is the difference between `remove()` and `pop()`?
6. What happens when you call `clear()`?
7. What is the purpose of `index()`?
8. How is `count()` different from `index()`?
9. What is the difference between `sort()` and `sorted()`?
10. Why does `sort()` return `None`?
11. What is the purpose of the `key` parameter?
12. What is the difference between `reverse()` and descending sorting?
13. What is a shallow copy?
14. What is the time complexity of searching for an element in a list?
15. Why should we avoid repeatedly inserting elements at the beginning of a large list?

---

## 23. Learning Outcome

After completing this chapter, you should be able to:

- Add elements using `append()`, `extend()`, and `insert()`.
- Remove elements using `remove()`, `pop()`, and `clear()`.
- Search and count values using `index()` and `count()`.
- Sort lists using `sort()` and `sorted()`.
- Use `key` and `reverse` parameters.
- Sort lists containing dictionaries.
- Reverse lists using `reverse()`.
- Create shallow copies using `copy()`.
- Understand the time complexity of common list operations.
- Apply list methods to basic API and customer-data processing.


