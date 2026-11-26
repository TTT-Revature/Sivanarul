
# Python: Lambda Functions

**Suggested filename:** `41_lambda_functions.md`

## 1. Introduction

So far, we have created functions using the `def` keyword.

Example:

```python
def add(a, b):
    return a + b

print(add(10, 20))
```

**Output:**

```text
30
```

Python also provides another way to create small functions using the `lambda` keyword.

A lambda function is:
- An anonymous function (a function that does not need a declared name).
- Usually used for short operations.
- Capable of accepting multiple arguments.
- Limited to a single expression.

## 2. Lambda Function Syntax

```python
lambda arguments: expression
```

Understanding the syntax:

| Part | Meaning |
|---|---|
| `lambda` | Keyword used to create a lambda function |
| `arguments` | Inputs accepted by the function |
| `:` | Separates arguments from the expression |
| `expression` | Operation whose result becomes the return value |

Unlike a normal function, a lambda function does not use an explicit `return` statement.

The expression's result is returned automatically.

## 3. Creating Your First Lambda Function

### Example 1: Add two numbers

Using a normal function:

```python
def add(a, b):
    return a + b

print(add(10, 20))
```

Using a lambda function:

```python
add = lambda a, b: a + b

print(add(10, 20))
```

**Output:**

```text
30
```

Explanation:

- `lambda a, b` accepts two arguments.
- `a + b` is the expression.
- The result is returned automatically.
- We assign the function to the variable `add`.

**Important:** Although lambda functions are often called anonymous functions, assigning one to a variable gives us a way to refer to and call it.

## 4. Lambda Functions with Different Arguments

### Example 1: One argument

```python
square = lambda number: number * number

print(square(5))
```

**Output:**

```text
25
```

### Example 2: Two arguments

```python
multiply = lambda a, b: a * b

print(multiply(5, 4))
```

**Output:**

```text
20
```

### Example 3: Three arguments

```python
calculate_total = lambda a, b, c: a + b + c

print(calculate_total(10, 20, 30))
```

**Output:**

```text
60
```

### Example 4: No arguments

```python
greet = lambda: "Welcome to Python"

print(greet())
```

**Output:**

```text
Welcome to Python
```

A lambda function can accept zero or more arguments.

## 5. Lambda Function vs Normal Function

Let's compare both approaches.

### Normal function

```python
def square(number):
    return number * number

print(square(5))
```

### Lambda function

```python
square = lambda number: number * number

print(square(5))
```

**Output for both:**

```text
25
```

| Feature | Normal function | Lambda function |
|---|---|---|
| Keyword | `def` | `lambda` |
| Function name | Normally declared | Can be anonymous |
| Body | Multiple statements allowed | One expression |
| Return | Uses `return` or implicit `None` | Expression result returned automatically |
| Documentation | Supports docstrings | No ordinary function-body docstring |
| Best use | Reusable and complex logic | Short, simple operations |

**Practical advice:** Use `def` when the logic is complex or needs documentation. Use lambda when a small function is useful locally.

## 6. Lambda with Conditional Expressions

A lambda function can contain a conditional expression.

### Example: Check even or odd

```python
check_number = lambda number: "Even" if number % 2 == 0 else "Odd"

print(check_number(10))
print(check_number(7))
```

**Output:**

```text
Even
Odd
```

Explanation:

```python
"Even" if number % 2 == 0 else "Odd"
```

This is a conditional expression, not a normal multi-statement `if-else` block.

## 7. Lambda with `map()`

The `map()` function applies a given function to every element of an iterable.

### Syntax

```python
map(function, iterable)
```

It returns a map iterator. You can convert it into a list to see all results.

### Example: Square every number

```python
numbers = [1, 2, 3, 4, 5]

result = map(lambda number: number * number, numbers)

print(list(result))
```

**Output:**

```text
[1, 4, 9, 16, 25]
```

Understanding the execution:

1. `numbers` contains five values.
2. `map()` takes each value one by one.
3. The lambda function squares the current value.
4. `list()` consumes the map iterator and displays the results.

### Without lambda

```python
def square(number):
    return number * number

numbers = [1, 2, 3, 4, 5]

result = map(square, numbers)

print(list(result))
```

Both approaches produce the same output.

## 8. Lambda with `filter()`

The `filter()` function selects elements from an iterable based on a condition.

### Syntax

```python
filter(function, iterable)
```

The function should return a truthy or falsy result for each element.

### Example: Filter even numbers

```python
numbers = [1, 2, 3, 4, 5, 6]

result = filter(lambda number: number % 2 == 0, numbers)

print(list(result))
```

**Output:**

```text
[2, 4, 6]
```

Explanation:

- `number % 2 == 0` checks whether a number is even.
- If the result is `True`, the element is retained.
- If the result is `False`, the element is excluded.

### Example: Filter numbers greater than 10

```python
numbers = [5, 12, 8, 20, 3, 15]

result = filter(lambda number: number > 10, numbers)

print(list(result))
```

**Output:**

```text
[12, 20, 15]
```

## 9. Lambda with `sorted()`

The `sorted()` function sorts an iterable and returns a new list.

Its `key` parameter allows us to specify how elements should be compared.

Lambda functions are commonly used with this parameter.

### Example 1: Sort numbers in ascending order

```python
numbers = [40, 10, 30, 20]

result = sorted(numbers, key=lambda number: number)

print(result)
```

**Output:**

```text
[10, 20, 30, 40]
```

Here, the lambda returns each number itself, so the sorting order is based on the number.

This particular lambda is unnecessary because `sorted(numbers)` already sorts numbers directly. It is included to demonstrate the `key` parameter.

### Example 2: Sort strings by length

```python
names = ["Arun", "Sivan", "Kumar", "Raj"]

result = sorted(names, key=lambda name: len(name))

print(result)
```

**Output:**

```text
['Raj', 'Arun', 'Sivan', 'Kumar']
```

Explanation:

- `len(name)` calculates the length of each name.
- `sorted()` uses that length for comparison.
- Shorter names appear first.
- Names with equal lengths retain their original relative order because Python sorting is stable.

### Example 3: Sort employees by salary

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

This is a practical example of using lambda functions to sort structured data.

## 10. Lambda with `reduce()`

The `reduce()` function repeatedly combines elements of an iterable into a single result.

It is available in the `functools` module.

### Syntax

```python
from functools import reduce

reduce(function, iterable)
```

### Example: Calculate the sum

```python
from functools import reduce

numbers = [10, 20, 30, 40]

result = reduce(lambda a, b: a + b, numbers)

print(result)
```

**Output:**

```text
100
```

Understanding the execution:

```text
Step 1: 10 + 20 = 30
Step 2: 30 + 30 = 60
Step 3: 60 + 40 = 100
```

The final result is `100`.

**Important:** `reduce()` is useful for some aggregation operations, but for simple addition, Python's built-in `sum()` is clearer.

## 11. Lambda Functions as Arguments

A function can accept another function as an argument.

This is possible because functions are first-class objects in Python.

### Example

```python
def execute_operation(a, b, operation):
    return operation(a, b)


result = execute_operation(
    10,
    20,
    lambda x, y: x + y
)

print(result)
```

**Output:**

```text
30
```

We passed a lambda function directly into another function.

We can change the operation without changing `execute_operation()`.

```python
print(execute_operation(10, 20, lambda x, y: x - y))
print(execute_operation(10, 20, lambda x, y: x * y))
```

**Output:**

```text
-10
200
```

This pattern is useful when a function needs to receive behavior as an argument.

## 12. Important Limitations of Lambda Functions

Lambda functions have some limitations.

### Limitation 1: Only one expression

Valid:

```python
square = lambda number: number * number
```

Invalid:

```python
# A lambda cannot contain multiple statements like this:
# lambda number:
#     result = number * number
#     return result
```

Use `def` when multiple statements are required.

### Limitation 2: No normal function-body docstring

Lambda functions do not have the usual function body in which to write a docstring.

Use a named function with `def` when meaningful documentation is needed.

### Limitation 3: Avoid complicated expressions

Not recommended:

```python
result = lambda x: "A" if x > 100 else "B" if x > 50 else "C" if x > 10 else "D"
```

A normal function is easier to read when the logic becomes complicated.

## 13. Common Mistakes

### Mistake 1: Forgetting to call the lambda function

```python
square = lambda x: x * x

print(square)
```

This displays a function representation, not the calculated result.

Correct:

```python
print(square(5))
```

Output:

```text
25
```

### Mistake 2: Using `return` inside lambda

Incorrect:

```python
# square = lambda x: return x * x
```

Correct:

```python
square = lambda x: x * x
```

The expression's result is returned automatically.

### Mistake 3: Forgetting to consume the `map()` iterator

```python
numbers = [1, 2, 3]

result = map(lambda x: x * 2, numbers)

print(result)
```

This prints a map object representation, not the calculated values.

Correct:

```python
print(list(result))
```

Output:

```text
[2, 4, 6]
```

Remember that map and filter return iterators, which are consumed when iterated over.

## 14. FDE Connection

As a Forward-Deployed Engineer, you may receive data from different customer systems.

You may need to:

- Transform data.
- Filter invalid records.
- Sort customer information.
- Apply simple business rules.
- Pass custom behavior into reusable functions.

### Practical example: Process customer records

```python
customers = [
    {"name": "Arun", "age": 25, "active": True},
    {"name": "Kumar", "age": 30, "active": False},
    {"name": "Raj", "age": 22, "active": True}
]

active_customers = filter(
    lambda customer: customer["active"],
    customers
)

sorted_customers = sorted(
    active_customers,
    key=lambda customer: customer["age"]
)

print(list(sorted_customers))
```

**Output:**

```text
[
    {'name': 'Raj', 'age': 22, 'active': True},
    {'name': 'Arun', 'age': 25, 'active': True}
]
```

Here:
- `filter()` selects active customers.
- `sorted()` sorts them by age.
- Lambda provides the small conditions used by both operations.

In real production systems, validate external data before processing it. Lambda functions do not replace validation or error handling.

## 15. Practice Exercises

### Exercise 1: Square a number

Create a lambda function that accepts a number and returns its square.

Expected:

```python
print(square(6))
```

Output:

```text
36
```

### Exercise 2: Add two numbers

Create a lambda function that accepts two numbers and returns their sum.

### Exercise 3: Even number filter

Given:

```python
numbers = [10, 15, 20, 25, 30, 35]
```

Use `filter()` and lambda to select only even numbers.

Expected output:

```text
[10, 20, 30]
```

### Exercise 4: Double every number

Given:

```python
numbers = [1, 2, 3, 4, 5]
```

Use `map()` and lambda to double every number.

Expected output:

```text
[2, 4, 6, 8, 10]
```

### Exercise 5: Sort employees

Given:

```python
employees = [
    {"name": "Arun", "salary": 40000},
    {"name": "Kumar", "salary": 25000},
    {"name": "Raj", "salary": 50000}
]
```

Use `sorted()` and lambda to sort employees by salary in descending order.

### Exercise 6: Pass a lambda into a function

Create a function called `calculate()` that accepts two numbers and an operation function.

Pass lambda functions to perform addition and multiplication.

### Exercise 7: Understand the output

Predict the output before running this code:

```python
numbers = [2, 4, 6, 8]

result = map(lambda x: x + 10, numbers)

print(list(result))
```

## 16. Quick Revision

| Concept | Meaning |
|---|---|
| `lambda` | Creates a small anonymous function |
| `lambda x: x * 2` | Function accepting one argument |
| Multiple arguments | `lambda x, y: x + y` |
| No arguments | `lambda: "Hello"` |
| Conditional expression | `lambda x: "Even" if x % 2 == 0 else "Odd"` |
| `map()` | Applies a function to every element |
| `filter()` | Selects elements based on a condition |
| `sorted()` | Sorts an iterable and returns a new list |
| `reduce()` | Combines iterable elements into one result |
| `key=` | Specifies the value used for sorting |

## 17. Self-Assessment

Before moving to the next topic, make sure you can answer:

1. What is a lambda function?
2. What is the difference between `def` and `lambda`?
3. Can a lambda function accept multiple arguments?
4. Can a lambda function contain multiple statements?
5. Does a lambda function need an explicit `return`?
6. What is the purpose of `map()`?
7. What is the purpose of `filter()`?
8. How can lambda be used with `sorted()`?
9. What does `reduce()` do?
10. Why might we choose a normal function instead of a lambda function?

## 18. Learning Outcome

After completing this chapter, you should be able to:

- Create lambda functions.
- Pass arguments to lambda functions.
- Use conditional expressions inside lambda functions.
- Apply lambda with `map()`, `filter()`, and `sorted()`.
- Understand the purpose of `reduce()`.
- Pass functions as arguments to other functions.
- Identify when lambda is appropriate and when `def` is better.


