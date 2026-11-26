
# Python: `*args` and `**kwargs`

**Suggested filename:** `39_args_and_kwargs.md`

## 1. Introduction

So far, we have learned how to pass arguments to Python functions:

- Positional arguments
- Keyword arguments
- Default arguments

But what if we don't know in advance how many arguments a function will receive?

For example:

```python
def add(a, b):
    return a + b

print(add(10, 20))
```

This function accepts only two arguments.

What if we want to add three, four, or even ten numbers without changing the function definition every time?

Python provides:

- `*args` – collects extra positional arguments.
- `**kwargs` – collects extra keyword arguments.

These features make functions more flexible.

---

## 2. Understanding `*args`

`*args` allows a function to accept any number of additional positional arguments.

### Syntax

```python
def function_name(*args):
    # function body
    pass
```

Here:
- `*` collects additional positional arguments.
- `args` is the conventional parameter name.
- Python stores the collected arguments in a tuple.

**Important:** The name `args` is not mandatory. The `*` symbol provides the behavior.

### Example 1: Accepting multiple arguments

```python
def display_names(*args):
    print(args)

display_names("Arun", "Bala", "Kumar")
```

**Output:**

```text
('Arun', 'Bala', 'Kumar')
```

Notice that the arguments are stored as a tuple.

### Example 2: Iterating through `*args`

```python
def display_names(*args):
    for name in args:
        print(name)

display_names("Arun", "Bala", "Kumar")
```

**Output:**

```text
Arun
Bala
Kumar
```

### Example 3: Calculating the total

```python
def calculate_total(*numbers):
    total = 0

    for number in numbers:
        total += number

    return total

result = calculate_total(10, 20, 30, 40)

print(result)
```

**Output:**

```text
100
```

Here, `numbers` is a tuple containing all the supplied positional arguments.

### Example 4: Combining normal parameters and `*args`

```python
def calculate_total(customer_name, *prices):
    total = sum(prices)

    print("Customer:", customer_name)
    print("Total:", total)

calculate_total("Arun", 100, 200, 300)
```

**Output:**

```text
Customer: Arun
Total: 600
```

The first positional argument is assigned to `customer_name`. Remaining positional arguments are collected in `prices`.

**Remember:** A normal positional parameter can appear before `*args`.

---

## 3. Understanding `**kwargs`

`**kwargs` allows a function to accept any number of additional keyword arguments.

### Syntax

```python
def function_name(**kwargs):
    # function body
    pass
```

Here:
- `**` collects additional keyword arguments.
- `kwargs` is the conventional parameter name.
- Python stores the collected arguments in a dictionary.

### Example 1: Accepting multiple keyword arguments

```python
def display_details(**kwargs):
    print(kwargs)

display_details(
    name="Arun",
    age=25,
    city="Chennai"
)
```

**Output:**

```text
{'name': 'Arun', 'age': 25, 'city': 'Chennai'}
```

Notice that Python stores the keyword arguments as key-value pairs in a dictionary.

### Example 2: Iterating through `**kwargs`

```python
def display_details(**kwargs):
    for key, value in kwargs.items():
        print(key, ":", value)

display_details(
    name="Arun",
    age=25,
    city="Chennai"
)
```

**Output:**

```text
name : Arun
age : 25
city : Chennai
```

### Example 3: Building a user profile

```python
def create_profile(**details):
    print("User Profile")

    for key, value in details.items():
        print(f"{key}: {value}")

create_profile(
    name="Arun",
    role="Python Developer",
    experience=4,
    location="Chennai"
)
```

**Output:**

```text
User Profile
name: Arun
role: Python Developer
experience: 4
location: Chennai
```

This is useful when a function needs to accept optional details without defining every possible parameter separately.

---

## 4. Difference Between `*args` and `**kwargs`

| Feature | `*args` | `**kwargs` |
|---|---|---|
| Purpose | Collect extra positional arguments | Collect extra keyword arguments |
| Data type | Tuple | Dictionary |
| Argument format | `10, 20, 30` | `name="Arun"` |
| Access | Indexing and iteration | Keys and values |
| Symbol | Single `*` | Double `**` |

### Example

```python
def example(*args, **kwargs):
    print("Arguments:", args)
    print("Keyword arguments:", kwargs)

example(10, 20, 30, name="Arun", city="Chennai")
```

**Output:**

```text
Arguments: (10, 20, 30)
Keyword arguments: {'name': 'Arun', 'city': 'Chennai'}
```

---

## 5. Combining Normal Parameters, `*args`, and `**kwargs`

We can use all three in one function.

### Example

```python
def employee_details(employee_id, *skills, **details):
    print("Employee ID:", employee_id)

    print("Skills:")
    for skill in skills:
        print("-", skill)

    print("Additional Details:")
    for key, value in details.items():
        print(key, ":", value)


employee_details(
    101,
    "Python",
    "FastAPI",
    "SQL",
    department="AI",
    location="Chennai"
)
```

**Output:**

```text
Employee ID: 101
Skills:
- Python
- FastAPI
- SQL
Additional Details:
department : AI
location : Chennai
```

### Parameter order

A common function parameter order is:

```python
def example(normal_parameter, *args, **kwargs):
    pass
```

Python also supports keyword-only parameters using `*`:

```python
def create_user(name, *skills, active=True):
    print(name)
    print(skills)
    print(active)

create_user("Arun", "Python", "SQL", active=False)
```

**Output:**

```text
Arun
('Python', 'SQL')
False
```

Here, `active` is keyword-only because it appears after `*skills`.

---

## 6. Argument Unpacking: `*` and `**` at the Function Call

So far, we have used `*args` and `**kwargs` in function definitions.

But `*` and `**` can also unpack existing collections when calling a function.

### Example 1: Unpacking a list using `*`

```python
def add(a, b, c):
    return a + b + c

numbers = [10, 20, 30]

result = add(*numbers)

print(result)
```

**Output:**

```text
60
```

What happens?

```python
add(*numbers)
```

is equivalent to:

```python
add(10, 20, 30)
```

The list elements are unpacked into positional arguments.

### Example 2: Unpacking a dictionary using `**`

```python
def employee(name, age, city):
    print(name, age, city)

details = {
    "name": "Arun",
    "age": 25,
    "city": "Chennai"
}

employee(**details)
```

**Output:**

```text
Arun 25 Chennai
```

The dictionary keys must match the function's parameter names.

This:

```python
employee(**details)
```

is equivalent to:

```python
employee(
    name="Arun",
    age=25,
    city="Chennai"
)
```

---

## 7. Important Rules and Common Mistakes

### Mistake 1: Thinking `args` is a list

```python
def example(*args):
    print(type(args))

example(10, 20, 30)
```

**Output:**

```text
<class 'tuple'>
```

`*args` collects arguments into a tuple, not a list.

### Mistake 2: Thinking `kwargs` is a tuple

```python
def example(**kwargs):
    print(type(kwargs))

example(name="Arun", age=25)
```

**Output:**

```text
<class 'dict'>
```

`**kwargs` collects arguments into a dictionary.

### Mistake 3: Passing keyword arguments without names

Incorrect:

```python
def display(**kwargs):
    print(kwargs)

display("Arun", 25)
```

This raises a `TypeError` because `**kwargs` accepts keyword arguments, not ordinary positional arguments.

Correct:

```python
display(name="Arun", age=25)
```

### Mistake 4: Unexpected dictionary keys

```python
def employee(name, age):
    print(name, age)

details = {
    "name": "Arun",
    "salary": 50000
}

employee(**details)
```

This raises a `TypeError` because `salary` is not a parameter of the function, and the required `age` argument is missing.

### Mistake 5: Duplicate argument values

```python
def employee(name):
    print(name)

employee("Arun", name="Kumar")
```

This raises a `TypeError` because `name` receives two values.

---

## 8. Practical Example: Flexible API Configuration

Imagine building a Python application that connects to different external services.

Each service may require different configuration details.

```python
def connect_service(service_name, **config):
    print("Connecting to:", service_name)

    for key, value in config.items():
        print(f"{key}: {value}")


connect_service(
    "Payment API",
    base_url="https://example.com",
    timeout=30,
    retry_count=3
)
```

**Output:**

```text
Connecting to: Payment API
base_url: https://example.com
timeout: 30
retry_count: 3
```

Why is this useful?

Different services may need different optional configuration values. Using `**config` lets us accept those values flexibly.

**Production note:** Flexible arguments do not replace input validation. A real application should validate configuration names, types, required values, and security-sensitive settings. Never print API keys or passwords in production logs.

---

## 9. FDE Connection

As a Forward-Deployed Engineer, you may work with:

- APIs from multiple vendors.
- Different customer configurations.
- Integration tools.
- Reusable Python utilities.
- Data processing pipelines.

`*args` and `**kwargs` help build flexible interfaces.

For example:

```python
def process_customer(customer_id, *records, **options):
    print("Customer:", customer_id)
    print("Records:", records)
    print("Options:", options)


process_customer(
    101,
    {"name": "Arun"},
    {"name": "Kumar"},
    validate=True,
    source="CRM"
)
```

**Output:**

```text
Customer: 101
Records: ({'name': 'Arun'}, {'name': 'Kumar'})
Options: {'validate': True, 'source': 'CRM'}
```

This is a simple illustration of how a reusable function can receive variable records and optional processing settings.

---

## 10. Practice Exercises

### Exercise 1: Basic `*args`

Create a function that accepts any number of numbers and prints each number.

### Exercise 2: Sum of numbers

Create a function using `*args` that calculates the sum of all supplied numbers.

Expected:

```python
calculate_sum(10, 20, 30)
```

Output:

```text
60
```

### Exercise 3: Basic `**kwargs`

Create a function that accepts a person's name, age, and city using `**kwargs` and displays them.

### Exercise 4: Combine both

Create a function that accepts:
- Employee ID as a normal parameter.
- Any number of skills using `*args`.
- Additional employee information using `**kwargs`.

### Exercise 5: Argument unpacking

Given:

```python
numbers = [10, 20, 30]
```

Pass these values to a function that accepts three positional parameters using `*`.

### Exercise 6: Dictionary unpacking

Given:

```python
employee = {
    "name": "Arun",
    "age": 25,
    "city": "Chennai"
}
```

Pass the dictionary values to a function using `**`.

---

## 11. Quick Revision

| Concept | Meaning |
|---|---|
| `*args` | Collects extra positional arguments |
| `**kwargs` | Collects extra keyword arguments |
| `args` type | Tuple |
| `kwargs` type | Dictionary |
| `*list` | Unpacks iterable elements into positional arguments |
| `**dict` | Unpacks dictionary entries into keyword arguments |
| `*` in definition | Can introduce keyword-only parameters |
| `**kwargs` in definition | Collects additional named arguments |

### Remember

```python
def example(*args, **kwargs):
    print(args)
    print(kwargs)
```

- `*args` → Tuple
- `**kwargs` → Dictionary

## 12. Self-Assessment

Before moving to the next topic, make sure you can answer:

1. Why do we use `*args`?
2. Why do we use `**kwargs`?
3. What is the difference between a tuple and a dictionary in this context?
4. Can we use normal parameters with `*args`?
5. What happens when we pass a list using `*`?
6. What happens when we pass a dictionary using `**`?
7. Why must dictionary keys match parameter names when unpacking into a function?
8. What is the difference between `*args` in a function definition and `*values` in a function call?

## 13. Learning Outcome

After completing this chapter, you should be able to:

- Accept a flexible number of positional arguments.
- Accept a flexible number of keyword arguments.
- Understand how Python collects arguments into tuples and dictionaries.
- Combine normal parameters, `*args`, and `**kwargs`.
- Unpack lists and dictionaries into function calls.
- Use flexible function arguments in reusable Python applications.

**Next recommended topic:** Python Lambda Functions.
