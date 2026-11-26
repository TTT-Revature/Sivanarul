
# Parameters and Arguments in Python

## 1. What are Parameters and Arguments?

Parameters and arguments are used to pass information into functions.

Example:

```python
def greet(name):
    print(f"Hello, {name}!")

greet("Arun")
```

Output:

```text
Hello, Arun!
```

In this example:

- `name` is a parameter.
- `"Arun"` is an argument.

### Parameter

A parameter is a variable declared inside the function definition.

```python
def greet(name):
    print(name)
```

Here, `name` is the parameter.

### Argument

An argument is the actual value supplied when calling the function.

```python
greet("Arun")
```

Here, `"Arun"` is the argument.

Remember:

Parameter = Variable receiving the value.

Argument = Actual value passed to the function.

---

## 2. Positional Arguments

Positional arguments are passed based on the position of parameters in the function definition.

Example:

```python
def employee(name, age, role):
    print(name)
    print(age)
    print(role)

employee("Arun", 27, "Python Developer")
```

Output:

```text
Arun
27
Python Developer
```

How Python assigns the values:

| Parameter | Argument |
|---|---|
| name | Arun |
| age | 27 |
| role | Python Developer |

Python assigns arguments according to their positions.

### Important

Changing the argument order can change the result.

```python
def employee(name, age):
    print(f"Name: {name}")
    print(f"Age: {age}")

employee(27, "Arun")
```

Output:

```text
Name: 27
Age: Arun
```

Python does not automatically understand that 27 represents age and Arun represents a name.

It follows the parameter positions.

---

## 3. Keyword Arguments

Keyword arguments pass values using parameter names.

Example:

```python
def employee(name, age, role):
    print(f"Name: {name}")
    print(f"Age: {age}")
    print(f"Role: {role}")

employee(
    role="Python Developer",
    name="Arun",
    age=27
)
```

Output:

```text
Name: Arun
Age: 27
Role: Python Developer
```

Notice that the order does not matter when all arguments are passed by keyword.

### Advantages

- Improves readability.
- Reduces mistakes caused by argument ordering.
- Makes function calls clearer.
- Useful when functions have many parameters.

---

## 4. Positional and Keyword Arguments Together

Python allows positional and keyword arguments in the same function call.

Example:

```python
def employee(name, age, role):
    print(name, age, role)

employee("Arun", age=27, role="Developer")
```

Output:

```text
Arun 27 Developer
```

Important rule:

Positional arguments must come before keyword arguments.

Correct:

```python
employee("Arun", age=27, role="Developer")
```

Incorrect:

```python
employee(name="Arun", 27, role="Developer")
```

The incorrect version raises a `SyntaxError`.

---

## 5. Default Arguments

A default argument provides a predefined value for a parameter.

If the caller does not provide a value, Python uses the default.

Example:

```python
def greet(name, country="India"):
    print(f"Hello {name} from {country}")

greet("Arun")
greet("John", "USA")
```

Output:

```text
Hello Arun from India
Hello John from USA
```

Explanation:

- First call: `country` uses its default value.
- Second call: the supplied argument overrides the default.

### Default Argument Rules

Parameters without defaults must come before parameters with defaults.

Correct:

```python
def employee(name, age, country="India"):
    print(name, age, country)
```

Incorrect:

```python
def employee(name="Arun", age):
    print(name, age)
```

The incorrect definition raises a `SyntaxError`.

---

## 6. Multiple Default Arguments

A function can have multiple default parameters.

Example:

```python
def create_account(
    username,
    role="user",
    active=True
):
    print(username)
    print(role)
    print(active)

create_account("arun")
```

Output:

```text
arun
user
True
```

We can override selected defaults using keyword arguments.

```python
create_account("arun", active=False)
```

Output:

```text
arun
user
False
```

---

## 7. Mutable Default Argument Problem

This is an important Python concept.

Consider this example:

```python
def add_item(item, items=[]):
    items.append(item)
    return items

print(add_item("Python"))
print(add_item("FastAPI"))
print(add_item("React"))
```

Output:

```text
['Python']
['Python', 'FastAPI']
['Python', 'FastAPI', 'React']
```

Why does this happen?

Python evaluates default argument expressions once when the function is defined.

Therefore, the same list object is reused across calls.

### Recommended Solution

Use `None` as the default value and create a new list inside the function.

```python
def add_item(item, items=None):

    if items is None:
        items = []

    items.append(item)

    return items

print(add_item("Python"))
print(add_item("FastAPI"))
print(add_item("React"))
```

Output:

```text
['Python']
['FastAPI']
['React']
```

Now every call creates a separate list when no list is supplied.

Important:

The mutable default argument behavior is not limited to lists. It can also affect dictionaries, sets, and other mutable objects.

---

## 8. Keyword-Only Arguments

Sometimes we want to force the caller to pass certain arguments by keyword.

Python provides `*` for this purpose.

Example:

```python
def create_user(name, *, role, active):
    print(name, role, active)

create_user("Arun", role="admin", active=True)
```

Output:

```text
Arun admin True
```

This is valid.

```python
create_user("Arun", "admin", True)
```

This raises a `TypeError`.

Why?

- `name` can be positional or keyword.
- `role` and `active` must be keyword arguments.

This improves clarity when a function has important configuration options.

---

## 9. Positional-Only Arguments

Python also supports positional-only parameters using `/`.

Example:

```python
def calculate(a, b, /):
    return a + b

print(calculate(10, 20))
```

Output:

```text
30
```

This is valid.

```python
calculate(a=10, b=20)
```

This raises a `TypeError`.

Why?

The `/` symbol means parameters before it must be supplied positionally.

### Combined Example

Python supports positional-only, normal, and keyword-only parameters together.

```python
def example(a, b, /, c, *, d):
    print(a, b, c, d)

example(10, 20, 30, d=40)
```

Output:

```text
10 20 30 40
```

Explanation:

- `a`, `b`: positional-only.
- `c`: positional or keyword.
- `d`: keyword-only.

---

## 10. Argument Unpacking

Python allows us to unpack collections when passing arguments.

### Using * for Positional Unpacking

Example:

```python
def add(a, b, c):
    return a + b + c

numbers = [10, 20, 30]

result = add(*numbers)

print(result)
```

Output:

```text
60
```

The `*` operator unpacks the list into separate positional arguments.

Equivalent call:

```python
add(10, 20, 30)
```

### Using ** for Keyword Unpacking

Example:

```python
def employee(name, age, role):
    print(name, age, role)

data = {
    "name": "Arun",
    "age": 27,
    "role": "Developer"
}

employee(**data)
```

Output:

```text
Arun 27 Developer
```

The `**` operator unpacks dictionary entries into keyword arguments.

The dictionary keys must match the function's parameter names, and there must not be duplicate values supplied for the same parameter.

---

## 11. Argument Passing and Mutable Objects

Python uses object-reference sharing (also called call-by-object-sharing).

Consider this example:

```python
def update_list(values):
    values.append(100)

numbers = [10, 20, 30]

update_list(numbers)

print(numbers)
```

Output:

```text
[10, 20, 30, 100]
```

Why?

The parameter `values` refers to the same list object as `numbers`.

Modifying that list is visible to the caller.

### Reassigning the Parameter

```python
def update_list(values):
    values = [100, 200]

numbers = [10, 20, 30]

update_list(numbers)

print(numbers)
```

Output:

```text
[10, 20, 30]
```

Why?

Reassigning the local parameter does not change which object the caller's variable references.

Remember:

- Mutating a shared object can affect the caller.
- Rebinding a local parameter does not rebind the caller's variable.

---

## 12. FDE Practical Example: API Configuration

Imagine you are integrating an external customer API.

You may need:
- A required API endpoint.
- A required API key.
- An optional timeout.
- An optional retry count.

Example:

```python
def connect_api(
    endpoint,
    api_key,
    timeout=30,
    retries=3
):
    print(f"Endpoint: {endpoint}")
    print(f"Timeout: {timeout}")
    print(f"Retries: {retries}")

connect_api(
    "https://api.example.com/customers",
    "sample-key",
    timeout=60
)
```

Output:

```text
Endpoint: https://api.example.com/customers
Timeout: 60
Retries: 3
```

This demonstrates how parameters and arguments make integrations configurable.

Note: The API key here is only a placeholder. Real credentials should be stored securely, not hardcoded.

---

## 13. Common Mistakes

| Mistake | Explanation |
|---|---|
| Passing too few arguments | Required parameters are missing |
| Passing too many arguments | Function does not accept that many positional arguments |
| Incorrect positional order | Values may be assigned to the wrong parameters |
| Positional argument after keyword argument | Invalid call syntax |
| Default before non-default parameter | Invalid function definition |
| Mutable default list | Same list can be reused across calls |
| Incorrect keyword name | Keyword does not match a parameter |
| Duplicate argument value | Same parameter receives more than one value |

---

## 14. Practical Exercises

### Exercise 1: Positional Arguments

Create a function that accepts:
- Employee name
- Employee age
- Employee department

Display all three values.

### Exercise 2: Keyword Arguments

Call the same function using keyword arguments in a different order.

### Exercise 3: Default Arguments

Create a function called `calculate_discount()`.

Requirements:
- Accept product price.
- Accept discount percentage.
- Set the default discount to 10%.
- Return the final price.

### Exercise 4: Keyword-Only Arguments

Create a function called `create_user()`.

Requirements:
- `name` can be positional.
- `role` must be keyword-only.
- `active` must be keyword-only and default to `True`.

### Exercise 5: Argument Unpacking

Create a function that accepts three numbers and returns their sum.

Pass the numbers using a list and the `*` operator.

### Exercise 6: Mutable Default Arguments

Write a function that adds values to a list.

Demonstrate the mutable default argument problem and correct it using `None`.

---

## 15. Quick Revision

| Concept | Meaning |
|---|---|
| Parameter | Variable declared in function definition |
| Argument | Actual value passed during function call |
| Positional argument | Value assigned based on position |
| Keyword argument | Value assigned using parameter name |
| Default argument | Value used when no argument is supplied |
| Keyword-only | Must be supplied using its parameter name |
| Positional-only | Must be supplied by position |
| `*args` | Collects extra positional arguments |
| `**kwargs` | Collects extra keyword arguments |
| `*` | Can unpack an iterable or mark keyword-only parameters |
| `**` | Can unpack a mapping into keyword arguments |
| Mutable default | A mutable object reused across calls |

## 16. Self-Assessment

You should be able to explain:

1. What is the difference between parameters and arguments?
2. What are positional arguments?
3. What are keyword arguments?
4. Can positional and keyword arguments be combined?
5. What are default arguments?
6. Why are mutable default arguments dangerous?
7. What is the purpose of `/` in a function definition?
8. What is the purpose of `*` in a function definition?
9. What is the difference between `*` and `**` when unpacking?
10. What happens when a mutable object is modified inside a function?

## Learning Outcome

After completing this chapter, you should understand how Python functions receive input, how arguments are assigned to parameters, and how to design flexible and reusable function interfaces.

**Next topic:** Variable-Length Arguments – `*args` and `**kwargs`.
