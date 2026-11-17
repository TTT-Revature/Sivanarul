
# Return Values and Multiple Returns in Python

## 1. What is a Return Value?

A return value is the result that a function sends back to the code that called it.

We use the `return` keyword to send a value back.

Example:

```python
def calculate_total(price, quantity):
    total = price * quantity
    return total

result = calculate_total(100, 3)

print(result)
```

Output:

```text
300
```

Explanation:

1. `calculate_total(100, 3)` calls the function.
2. `price` receives 100.
3. `quantity` receives 3.
4. Python calculates `100 * 3`.
5. `return total` sends 300 back.
6. The returned value is stored in `result`.

## 2. How Does return Work?

Consider this example:

```python
def add_numbers(a, b):
    result = a + b
    return result

answer = add_numbers(10, 20)

print(answer)
```

Output:

```text
30
```

Execution flow:

```text
Function call
     |
     v
add_numbers(10, 20)
     |
     v
a = 10, b = 20
     |
     v
result = 10 + 20
     |
     v
return 30
     |
     v
answer = 30
```

The returned value goes back to the location where the function was called.

## 3. Difference Between print() and return

This is one of the most important concepts in Python functions.

### Using print()

```python
def calculate(a, b):
    print(a + b)

result = calculate(10, 20)

print("Result:", result)
```

Output:

```text
30
Result: None
```

Why?

- `print()` displays the result.
- It does not return the displayed value.
- Since the function has no explicit return statement, Python returns `None`.

### Using return

```python
def calculate(a, b):
    return a + b

result = calculate(10, 20)

print("Result:", result)
```

Output:

```text
Result: 30
```

Why?

The function sends the calculated value back to the caller.

### Comparison

| print() | return |
|---|---|
| Displays information | Sends a value back |
| Does not return the displayed value | Returns the specified value |
| Useful for output and debugging | Useful for calculations and processing |
| Function continues after print | Function exits when return executes |

Remember:

`print()` displays a value.

`return` gives a value back to the caller.

## 4. What Happens When We Don't Use return?

If a function finishes without executing an explicit return statement, Python automatically returns `None`.

Example:

```python
def greet():
    print("Welcome to Python")

result = greet()

print(result)
```

Output:

```text
Welcome to Python
None
```

Even though the function displays a message, its return value is `None`.

Another example:

```python
def display():
    pass

result = display()

print(result)
```

Output:

```text
None
```

The `pass` statement does nothing, and the function finishes normally.

## 5. The return Statement Immediately Stops Execution

Once Python executes `return`, the function terminates immediately.

Example:

```python
def check_number(number):
    if number > 0:
        return "Positive"

    print("This executes only for non-positive numbers")

    return "Non-positive"

print(check_number(10))
```

Output:

```text
Positive
```

The `print()` statement is never executed because the function already returned.

Another example:

```python
def test():
    print("First")
    return "Finished"
    print("Second")

print(test())
```

Output:

```text
First
Finished
```

The second print statement is unreachable.

## 6. Returning Different Data Types

A Python function can return different data types.

### Returning an integer

```python
def get_age():
    return 27

print(get_age())
```

Output:

```text
27
```

### Returning a string

```python
def get_name():
    return "Arun"

print(get_name())
```

Output:

```text
Arun
```

### Returning a Boolean

```python
def is_eligible(age):
    return age >= 18

print(is_eligible(25))
```

Output:

```text
True
```

### Returning a list

```python
def get_skills():
    return ["Python", "FastAPI", "SQL"]

skills = get_skills()

print(skills)
```

Output:

```text
['Python', 'FastAPI', 'SQL']
```

### Returning a dictionary

```python
def get_employee():
    return {
        "name": "Arun",
        "role": "Developer",
        "experience": 4
    }

employee = get_employee()

print(employee)
```

Output:

```text
{'name': 'Arun', 'role': 'Developer', 'experience': 4}
```

## 7. Returning Multiple Values

Python allows a function to return multiple values in a single return statement.

Example:

```python
def calculate(a, b):
    total = a + b
    difference = a - b

    return total, difference

result = calculate(20, 10)

print(result)
```

Output:

```text
(30, 10)
```

Important:

Python technically returns one object here: a tuple containing both values.

This statement:

```python
return total, difference
```

is equivalent to:

```python
return (total, difference)
```

## 8. Unpacking Multiple Return Values

We can directly assign multiple returned values to separate variables.

Example:

```python
def calculate(a, b):
    return a + b, a - b

total, difference = calculate(20, 10)

print("Total:", total)
print("Difference:", difference)
```

Output:

```text
Total: 30
Difference: 10
```

Explanation:

The function returns:

```python
(30, 10)
```

Python unpacks the tuple:

```python
total = 30
difference = 10
```

This is called tuple unpacking.

## 9. Returning Three or More Values

A function can return any number of values.

Example:

```python
def employee_details():
    name = "Arun"
    age = 27
    role = "Python Developer"

    return name, age, role

name, age, role = employee_details()

print(name)
print(age)
print(role)
```

Output:

```text
Arun
27
Python Developer
```

The function returns a tuple containing three values.

## 10. What Happens If We Unpack the Wrong Number of Values?

Example:

```python
def calculate():
    return 10, 20, 30

a, b = calculate()
```

Output:

```text
ValueError: too many values to unpack
```

Why?

The function returns three values, but we provide only two variables.

Correct:

```python
a, b, c = calculate()

print(a, b, c)
```

Output:

```text
10 20 30
```

The number of unpacking targets must match the number of returned iterable elements, unless extended unpacking is used.

## 11. Extended Unpacking with *

Python supports extended unpacking.

Example:

```python
def get_numbers():
    return 10, 20, 30, 40, 50

first, *remaining = get_numbers()

print(first)
print(remaining)
```

Output:

```text
10
[20, 30, 40, 50]
```

Here:

- `first` receives the first value.
- `remaining` receives the other values as a list.

Another example:

```python
a, *middle, last = (10, 20, 30, 40, 50)

print(a)
print(middle)
print(last)
```

Output:

```text
10
[20, 30, 40]
50
```

## 12. Returning None Explicitly

Python allows us to return `None` explicitly.

Example:

```python
def find_user(user_id):
    if user_id == 1:
        return "Arun"

    return None

print(find_user(1))
print(find_user(5))
```

Output:

```text
Arun
None
```

This is useful when a function cannot find the requested data.

For example:
- A customer record does not exist.
- A database query returns no matching result.
- An optional configuration is unavailable.

Important:

There is a difference between explicitly returning `None` and reaching the end of a function without a return statement, but both produce the same returned value.

## 13. Returning Results from Another Function

A function can call another function and return its result.

Example:

```python
def calculate_total(price, quantity):
    return price * quantity

def calculate_tax(price):
    return price * 0.18

def final_amount(price, quantity):
    total = calculate_total(price, quantity)
    tax = calculate_tax(total)

    return total + tax

print(final_amount(100, 2))
```

Output:

```text
236.0
```

Explanation:

1. Calculate the total: 100 × 2 = 200.
2. Calculate tax: 200 × 0.18 = 36.
3. Add total and tax: 200 + 36 = 236.
4. Return the final amount.

This approach divides a larger problem into smaller functions.

## 14. Practical Example: Customer Validation

Imagine you receive customer data from an external API.

You want to validate the customer and return:
- Whether validation succeeded.
- A message explaining the result.

Example:

```python
def validate_customer(name, age):

    if not name or not name.strip():
        return False, "Customer name is required"

    if age < 18:
        return False, "Customer must be at least 18"

    return True, "Customer validated successfully"


status, message = validate_customer("Arun", 27)

print(status)
print(message)
```

Output:

```text
True
Customer validated successfully
```

Another call:

```python
status, message = validate_customer("", 17)

print(status)
print(message)
```

Output:

```text
False
Customer name is required
```

Notice that the function returns two values as a tuple.

In a real application, input types and missing values should also be validated carefully.

## 15. FDE Connection: Processing API Responses

Suppose an external API returns customer information.

You want to extract the customer's name and status.

Example:

```python
def process_customer(customer):

    name = customer.get("name")
    status = customer.get("status")

    return name, status


customer_data = {
    "name": "Arun",
    "status": "active"
}

name, status = process_customer(customer_data)

print("Customer:", name)
print("Status:", status)
```

Output:

```text
Customer: Arun
Status: active
```

Why is this useful?

An FDE may need to:
- Receive API responses.
- Extract relevant fields.
- Transform data.
- Return processed results.
- Pass those results to another service.

Functions with meaningful return values make these workflows easier to organize and test.

## 16. Common Mistakes

| Mistake | Explanation |
|---|---|
| Using print instead of return | The displayed value is not returned |
| Forgetting return | Function returns None if it finishes normally |
| Writing code after return | That code is unreachable on that execution path |
| Unpacking the wrong number of values | Causes ValueError |
| Assuming multiple returns are separate objects | Python packs comma-separated return values into a tuple |
| Ignoring returned values | The result may be lost if it is neither stored nor used |
| Confusing None with False | They are different Python values |

## 17. Practical Exercises

### Exercise 1: Basic Return

Create a function that accepts two numbers and returns their multiplication.

### Exercise 2: Boolean Return

Create a function that accepts an age and returns True if the person is eligible to vote; otherwise, return False.

### Exercise 3: Multiple Returns

Create a function that accepts two numbers and returns:
- Addition
- Subtraction
- Multiplication
- Division

Return all four results.

### Exercise 4: Tuple Unpacking

Call your function from Exercise 3 and unpack all four returned values into separate variables.

### Exercise 5: Customer Validation

Create a function that accepts a customer name and age.

Return:
- A Boolean indicating validation status.
- A suitable message.

### Exercise 6: Debugging

Find the problem:

```python
def calculate(a, b):
    print(a + b)

result = calculate(10, 20)

print(result * 2)
```

Explain why the code fails and correct it.

## 18. Quick Revision

| Concept | Meaning |
|---|---|
| `return` | Sends a value back to the caller |
| `print()` | Displays information |
| Implicit None | Default return value when no explicit return executes |
| Multiple return values | Comma-separated values packed into a tuple |
| Tuple unpacking | Assigns returned elements to separate variables |
| Extended unpacking | Uses `*` to collect remaining elements |
| `return None` | Explicitly returns None |
| Unreachable code | Code after an executed return statement |

## 19. Self-Assessment

You should be able to explain:

1. What is a return value?
2. What happens when a function does not have a return statement?
3. What is the difference between print and return?
4. Does return immediately terminate function execution?
5. Can Python return multiple values?
6. What data structure is used when returning comma-separated values?
7. What is tuple unpacking?
8. What happens when the number of variables does not match the returned values?
9. Can a function return a dictionary or list?
10. Can one function return the result of another function?

