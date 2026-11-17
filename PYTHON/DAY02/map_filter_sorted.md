
# Python: `map()`, `filter()` and `sorted(key=...)`

**Suggested filename:** `42_map_filter_sorted.md`

## 1. Introduction

When working with Python applications, we frequently need to perform three operations:

1. Transform existing data.
2. Select data based on conditions.
3. Sort data based on specific requirements.

Python provides three useful built-in functions:

| Function | Purpose |
|---|---|
| `map()` | Transforms every element in an iterable |
| `filter()` | Selects elements based on a condition |
| `sorted()` | Sorts elements and returns a new list |

These functions can work with normal functions and lambda functions.

---

# PART 1: map()

## 2. What is `map()`?

The `map()` function applies a specified function to every element in an iterable.

An iterable can be:
- List
- Tuple
- String
- Set
- Other iterable objects

### Syntax

```python
map(function, iterable)
```

Parameters:

- `function`: The function to apply to each element.
- `iterable`: The collection whose elements should be processed.

**Important:** `map()` returns a map iterator, not a list.

## 3. Basic Example Using `map()`

Imagine we have a list of numbers and want to double every number.

```python
numbers = [1, 2, 3, 4, 5]

result = map(lambda x: x * 2, numbers)

print(list(result))
```

**Output:**

```text
[2, 4, 6, 8, 10]
```

### How does it work?

| Original value | Operation | Result |
|---:|---|---:|
| 1 | 1 * 2 | 2 |
| 2 | 2 * 2 | 4 |
| 3 | 3 * 2 | 6 |
| 4 | 4 * 2 | 8 |
| 5 | 5 * 2 | 10 |

The lambda function is applied to each element.

## 4. Using `map()` with a Normal Function

We don't have to use lambda. We can also pass a function created using `def`.

```python
def square(number):
    return number * number


numbers = [1, 2, 3, 4, 5]

result = map(square, numbers)

print(list(result))
```

**Output:**

```text
[1, 4, 9, 16, 25]
```

Notice:

```python
map(square, numbers)
```

We pass `square`, not `square()`.

Why?

- `square` refers to the function itself.
- `square()` calls the function immediately.

`map()` needs the function so it can call it for each element.

## 5. Using `map()` with Strings

We can also transform strings.

### Example: Convert names to uppercase

```python
names = ["arun", "kumar", "raj"]

result = map(str.upper, names)

print(list(result))
```

**Output:**

```text
['ARUN', 'KUMAR', 'RAJ']
```

### Example: Convert strings into integers

```python
numbers = ["10", "20", "30", "40"]

result = map(int, numbers)

print(list(result))
```

**Output:**

```text
[10, 20, 30, 40]
```

This is useful when processing numeric values received as strings.

## 6. Using `map()` with Multiple Iterables

`map()` can accept more than one iterable.

The function must accept the corresponding number of arguments.

```python
numbers1 = [10, 20, 30]
numbers2 = [1, 2, 3]

result = map(lambda a, b: a + b, numbers1, numbers2)

print(list(result))
```

**Output:**

```text
[11, 22, 33]
```

Explanation:

| First iterable | Second iterable | Result |
|---:|---:|---:|
| 10 | 1 | 11 |
| 20 | 2 | 22 |
| 30 | 3 | 33 |

**Important:** When multiple iterables are provided, `map()` stops when the shortest iterable is exhausted.

Example:

```python
a = [10, 20, 30]
b = [1, 2]

result = map(lambda x, y: x + y, a, b)

print(list(result))
```

**Output:**

```text
[11, 22]
```

The third element of `a` is not processed because `b` has only two elements.

---

# PART 2: filter()

## 7. What is `filter()`?

The `filter()` function selects elements from an iterable based on a condition.

It keeps elements for which the supplied function returns a truthy value.

### Syntax

```python
filter(function, iterable)
```

Parameters:

- `function`: A function that evaluates each element.
- `iterable`: The collection to filter.

**Important:** `filter()` returns a filter iterator, not a list.

## 8. Basic Example Using `filter()`

Imagine we have numbers and want only even numbers.

```python
numbers = [1, 2, 3, 4, 5, 6]

result = filter(lambda x: x % 2 == 0, numbers)

print(list(result))
```

**Output:**

```text
[2, 4, 6]
```

### How does it work?

| Number | Condition | Selected? |
|---:|---|---|
| 1 | 1 % 2 == 0 | No |
| 2 | 2 % 2 == 0 | Yes |
| 3 | 3 % 2 == 0 | No |
| 4 | 4 % 2 == 0 | Yes |
| 5 | 5 % 2 == 0 | No |
| 6 | 6 % 2 == 0 | Yes |

Only elements satisfying the condition are retained.

## 9. Using `filter()` with a Normal Function

```python
def is_positive(number):
    return number > 0


numbers = [-10, 20, -5, 30, 0, 15]

result = filter(is_positive, numbers)

print(list(result))
```

**Output:**

```text
[20, 30, 15]
```

The function returns `True` for positive numbers and `False` for other numbers.

## 10. Filtering Strings

### Example: Select names starting with A

```python
names = ["Arun", "Kumar", "Anbu", "Raj", "Ajay"]

result = filter(lambda name: name.startswith("A"), names)

print(list(result))
```

**Output:**

```text
['Arun', 'Anbu', 'Ajay']
```

### Example: Select names longer than four characters

```python
names = ["Raj", "Arun", "Kumar", "Sivan", "Jo"]

result = filter(lambda name: len(name) > 4, names)

print(list(result))
```

**Output:**

```text
['Kumar', 'Sivan']
```

## 11. Understanding `filter(None, iterable)`

An interesting feature of `filter()` is that we can pass `None` as the function.

When we do this, Python retains elements that are truthy.

```python
values = [0, 10, "", "Python", None, False, True]

result = filter(None, values)

print(list(result))
```

**Output:**

```text
[10, 'Python', True]
```

Why?

| Value | Truthiness | Selected? |
|---|---|---|
| 0 | False | No |
| 10 | True | Yes |
| `""` | False | No |
| `"Python"` | True | Yes |
| `None` | False | No |
| `False` | False | No |
| `True` | True | Yes |

This is useful when removing falsy values, but be careful: valid values such as `0` and `False` will also be removed.

---

# PART 3: sorted(key=...)

## 12. What is `sorted()`?

The `sorted()` function sorts elements in an iterable and returns a new list.

### Syntax

```python
sorted(iterable, key=None, reverse=False)
```

Parameters:

- `iterable`: Collection to sort.
- `key`: Optional function that determines the sorting value.
- `reverse`: If `True`, sorts in descending order.

**Important:** `sorted()` does not modify the original collection.

## 13. Basic Sorting

```python
numbers = [40, 10, 30, 20]

result = sorted(numbers)

print(result)
```

**Output:**

```text
[10, 20, 30, 40]
```

The original list remains unchanged.

```python
print(numbers)
```

**Output:**

```text
[40, 10, 30, 20]
```

## 14. Sorting in Descending Order

```python
numbers = [40, 10, 30, 20]

result = sorted(numbers, reverse=True)

print(result)
```

**Output:**

```text
[40, 30, 20, 10]
```

## 15. Understanding the `key` Parameter

The `key` parameter is one of the most important features of `sorted()`.

It allows us to define how Python should compare elements while sorting.

### Example: Sort names by length

```python
names = ["Arun", "Sivan", "Kumar", "Raj"]

result = sorted(names, key=len)

print(result)
```

**Output:**

```text
['Raj', 'Arun', 'Sivan', 'Kumar']
```

How does it work?

Python calculates the length of each name:

| Name | Length |
|---|---:|
| Arun | 4 |
| Sivan | 5 |
| Kumar | 5 |
| Raj | 3 |

Then it sorts based on those lengths.

When two names have equal lengths, their original relative order is preserved because Python sorting is stable.

### Important

This:

```python
sorted(names, key=len)
```

is conceptually similar to:

```python
sorted(names, key=lambda name: len(name))
```

Both use the length of each name as the sorting key.

## 16. Sorting with Lambda

### Example: Sort numbers based on their last digit

```python
numbers = [23, 15, 42, 31, 18]

result = sorted(numbers, key=lambda x: x % 10)

print(result)
```

**Output:**

```text
[31, 42, 23, 15, 18]
```

Explanation:

| Number | Last digit |
|---:|---:|
| 23 | 3 |
| 15 | 5 |
| 42 | 2 |
| 31 | 1 |
| 18 | 8 |

The numbers are sorted using their last digit.

## 17. Sorting a List of Dictionaries

This is a very important real-world use case.

Imagine receiving employee records from an API.

```python
employees = [
    {"name": "Arun", "salary": 40000},
    {"name": "Kumar", "salary": 30000},
    {"name": "Raj", "salary": 50000}
]

result = sorted(
    employees,
    key=lambda employee: employee["salary"]
)

print(result)
```

**Output:**

```text
[
    {'name': 'Kumar', 'salary': 30000},
    {'name': 'Arun', 'salary': 40000},
    {'name': 'Raj', 'salary': 50000}
]
```

Explanation:

- Each employee is a dictionary.
- `employee["salary"]` accesses the salary.
- `key` uses that salary for sorting.
- Employees are arranged in ascending salary order.

### Descending salary order

```python
result = sorted(
    employees,
    key=lambda employee: employee["salary"],
    reverse=True
)

print(result)
```

**Output:**

```text
[
    {'name': 'Raj', 'salary': 50000},
    {'name': 'Arun', 'salary': 40000},
    {'name': 'Kumar', 'salary': 30000}
]
```

## 18. Sorting Using Multiple Conditions

We can return a tuple from the key function to sort by multiple criteria.

Example: Sort employees by department first, then by salary.

```python
employees = [
    {"name": "Arun", "department": "AI", "salary": 40000},
    {"name": "Kumar", "department": "IT", "salary": 30000},
    {"name": "Raj", "department": "AI", "salary": 50000},
    {"name": "Anbu", "department": "IT", "salary": 25000}
]

result = sorted(
    employees,
    key=lambda employee: (
        employee["department"],
        employee["salary"]
    )
)

for employee in result:
    print(employee)
```

**Output:**

```text
{'name': 'Arun', 'department': 'AI', 'salary': 40000}
{'name': 'Raj', 'department': 'AI', 'salary': 50000}
{'name': 'Anbu', 'department': 'IT', 'salary': 25000}
{'name': 'Kumar', 'department': 'IT', 'salary': 30000}
```

Python compares the returned tuples in order:

1. Department.
2. Salary, when departments are equal.

This is called sorting by multiple keys.

---

# PART 4: Difference Between map(), filter(), and sorted()

## 19. Comparison

| Feature | `map()` | `filter()` | `sorted()` |
|---|---|---|---|
| Purpose | Transform elements | Select elements | Arrange elements |
| Function role | Calculates new value | Checks a condition | Produces a sorting key |
| Return type | Map iterator | Filter iterator | List |
| Original data | Not modified | Not modified | Not modified |
| Lambda commonly used? | Yes | Yes | Yes |

### Simple example

```python
numbers = [1, 2, 3, 4, 5]

# Transform
mapped = map(lambda x: x * 2, numbers)

# Filter
filtered = filter(lambda x: x % 2 == 0, numbers)

# Sort
sorted_numbers = sorted(numbers, reverse=True)

print(list(mapped))
print(list(filtered))
print(sorted_numbers)
```

**Output:**

```text
[2, 4, 6, 8, 10]
[2, 4]
[5, 4, 3, 2, 1]
```

Notice that:
- `map()` changes the values.
- `filter()` changes which elements are included.
- `sorted()` changes the order.

---

# PART 5: Combining map(), filter(), and sorted()

## 20. Practical Example: Customer Data Processing

Imagine an application receives customer records.

We need to:

1. Select customers whose age is at least 18.
2. Extract their names.
3. Sort their names alphabetically.

### Input data

```python
customers = [
    {"name": "Arun", "age": 25},
    {"name": "Kumar", "age": 16},
    {"name": "Raj", "age": 30},
    {"name": "Anbu", "age": 15},
    {"name": "Sivan", "age": 28}
]
```

### Solution

```python
# Step 1: Filter eligible customers
eligible_customers = filter(
    lambda customer: customer["age"] >= 18,
    customers
)

# Step 2: Extract customer names
customer_names = map(
    lambda customer: customer["name"],
    eligible_customers
)

# Step 3: Sort names
result = sorted(customer_names)

print(result)
```

**Output:**

```text
['Arun', 'Raj', 'Sivan']
```

### Understanding the workflow

```text
Original Customer Records
          |
          v
       filter()
          |
          v
   Eligible Customers
          |
          v
        map()
          |
          v
    Customer Names
          |
          v
       sorted()
          |
          v
     Final Result
```

This is a simple example of a data transformation pipeline.

---

# PART 6: Important Concepts

## 21. Lazy Evaluation

`map()` and `filter()` return iterators.

They do not calculate and store all results immediately.

Example:

```python
numbers = [1, 2, 3, 4]

result = map(lambda x: x * 2, numbers)

print(result)
```

Output will be similar to:

```text
<map object at ...>
```

The exact memory address or representation may vary.

To obtain the values:

```python
print(list(result))
```

Output:

```text
[2, 4, 6, 8]
```

### Important: Iterators are consumed

```python
numbers = [1, 2, 3]

result = map(lambda x: x * 2, numbers)

print(list(result))
print(list(result))
```

**Output:**

```text
[2, 4, 6]
[]
```

Why?

The first `list()` consumes the iterator. There are no remaining elements for the second call.

If you need to reuse the results, store them in a list:

```python
result = list(map(lambda x: x * 2, numbers))

print(result)
print(result)
```

## 22. Difference Between sorted() and list.sort()

Both are used for sorting, but they behave differently.

### Using sorted()

```python
numbers = [30, 10, 20]

result = sorted(numbers)

print(result)
print(numbers)
```

**Output:**

```text
[10, 20, 30]
[30, 10, 20]
```

`sorted()` returns a new list.

### Using list.sort()

```python
numbers = [30, 10, 20]

result = numbers.sort()

print(numbers)
print(result)
```

**Output:**

```text
[10, 20, 30]
None
```

`sort()` modifies the original list and returns `None`.

---

# PART 7: Common Mistakes

## 23. Mistake 1: Forgetting list() with map()

```python
numbers = [1, 2, 3]

result = map(lambda x: x * 2, numbers)

print(result)
```

This displays an iterator representation, not the actual values.

Correct:

```python
print(list(result))
```

## 24. Mistake 2: Using filter() when you want transformation

Suppose we want to double every number.

Incorrect:

```python
numbers = [1, 2, 3]

result = filter(lambda x: x * 2, numbers)

print(list(result))
```

Output:

```text
[1, 2, 3]
```

Why?

`filter()` checks whether the returned value is truthy. It does not replace each element with that value.

Correct:

```python
result = map(lambda x: x * 2, numbers)

print(list(result))
```

Output:

```text
[2, 4, 6]
```

## 25. Mistake 3: Confusing key with the original value

```python
names = ["Arun", "Sivan", "Raj"]

result = sorted(names, key=len)

print(result)
```

The `key` function determines the comparison value. It does not replace the original elements in the resulting list.

Output:

```text
['Raj', 'Arun', 'Sivan']
```

The result still contains strings, not their lengths.

## 26. Mistake 4: Assuming sorted() modifies the original list

```python
numbers = [30, 10, 20]

sorted(numbers)

print(numbers)
```

Output:

```text
[30, 10, 20]
```

To keep the sorted result:

```python
numbers = sorted(numbers)
```

---

# PART 8: FDE Connection

## 27. Real-World Example: Processing API Records

As a Forward-Deployed Engineer, you may receive records from customer APIs.

For example:

```python
orders = [
    {"order_id": 101, "amount": 5000, "status": "completed"},
    {"order_id": 102, "amount": 2000, "status": "pending"},
    {"order_id": 103, "amount": 8000, "status": "completed"},
    {"order_id": 104, "amount": 1000, "status": "cancelled"}
]
```

Requirement:

- Select completed orders.
- Extract their amounts.
- Sort amounts from highest to lowest.

### Solution

```python
completed_orders = filter(
    lambda order: order["status"] == "completed",
    orders
)

order_amounts = map(
    lambda order: order["amount"],
    completed_orders
)

result = sorted(order_amounts, reverse=True)

print(result)
```

**Output:**

```text
[8000, 5000]
```

This demonstrates a simple data-processing workflow.

In real applications, also consider:
- Missing dictionary keys.
- Invalid data types.
- Null values.
- Data validation.
- Large datasets and memory usage.

---

# PART 9: Practice Exercises

## 28. Exercise 1: Using map()

Given:

```python
numbers = [2, 4, 6, 8, 10]
```

Use `map()` to multiply every number by 5.

Expected output:

```text
[10, 20, 30, 40, 50]
```

## 29. Exercise 2: Using filter()

Given:

```python
numbers = [5, 12, 18, 23, 30, 41]
```

Use `filter()` to select numbers greater than 20.

Expected output:

```text
[23, 30, 41]
```

## 30. Exercise 3: Using sorted()

Given:

```python
names = ["Sivan", "Raj", "Arun", "Kumar"]
```

Sort names based on their length.

Expected output:

```text
['Raj', 'Arun', 'Sivan', 'Kumar']
```

## 31. Exercise 4: Sort dictionaries

Given:

```python
students = [
    {"name": "Arun", "marks": 80},
    {"name": "Kumar", "marks": 95},
    {"name": "Raj", "marks": 70}
]
```

Sort students by marks in descending order.

## 32. Exercise 5: Combine all three

Given:

```python
employees = [
    {"name": "Arun", "salary": 40000, "active": True},
    {"name": "Kumar", "salary": 25000, "active": False},
    {"name": "Raj", "salary": 50000, "active": True},
    {"name": "Anbu", "salary": 30000, "active": True}
]
```

Perform these operations:

1. Filter active employees.
2. Extract their salaries.
3. Sort salaries in descending order.

Expected output:

```text
[50000, 40000, 30000]
```

## 33. Exercise 6: Predict the output

Without executing the code, predict the output:

```python
numbers = [1, 2, 3, 4, 5]

result = filter(lambda x: x > 2, numbers)

result = map(lambda x: x * 10, result)

print(list(result))
```

---

# PART 10: Quick Revision

## 34. Summary

| Function | Main purpose | Example |
|---|---|---|
| `map()` | Transform each element | `map(lambda x: x * 2, numbers)` |
| `filter()` | Select elements | `filter(lambda x: x > 10, numbers)` |
| `sorted()` | Sort elements | `sorted(numbers, reverse=True)` |
| `sorted(key=...)` | Sort using a custom value | `sorted(names, key=len)` |

### Remember these three points

- `map()` → Transform.
- `filter()` → Select.
- `sorted()` → Organize.

### Return types

| Function | Return type |
|---|---|
| `map()` | Map iterator |
| `filter()` | Filter iterator |
| `sorted()` | List |

## 35. Self-Assessment

Before moving to the next topic, make sure you can answer:

1. What is the purpose of `map()`?
2. What is the purpose of `filter()`?
3. What is the difference between `map()` and `filter()`?
4. What does `sorted()` return?
5. What is the purpose of the `key` parameter?
6. Can we pass a normal function to `map()`?
7. What happens when multiple iterables are passed to `map()`?
8. Why does `map()` return an iterator?
9. What happens when we consume the same iterator twice?
10. What is the difference between `sorted()` and `list.sort()`?

## 36. Learning Outcome

After completing this chapter, you should be able to:

- Transform data using `map()`.
- Filter data using `filter()`.
- Sort data using `sorted()`.
- Customize sorting with `key=`.
- Use lambda functions with these built-in functions.
- Process lists of dictionaries.
- Combine multiple operations into a simple data-processing pipeline.
- Understand iterators and lazy evaluation.

**Next recommended topic:** Python List Comprehensions.
