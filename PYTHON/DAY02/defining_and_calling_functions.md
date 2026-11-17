
# Defining and Calling Functions in Python

## 1. What is a Function?

A function is a reusable block of code designed to perform a specific task.

For example, imagine you are building an application that calculates an employee's salary.

Instead of writing the salary calculation repeatedly, you can define a function once and call it whenever required.

Real-world analogy:

A coffee machine performs a specific task:
- You provide coffee powder and water.
- The machine processes them.
- It produces coffee.

Similarly, a Python function can receive input, process it, and return an output.

## 2. Why Do We Need Functions?

Without functions:

```python
price = 1000
tax = price * 0.18
print(price + tax)

price = 2000
tax = price * 0.18
print(price + tax)
```

The same calculation is repeated.

With functions:

```python
def calculate_price(price):
    tax = price * 0.18
    return price + tax

print(calculate_price(1000))
print(calculate_price(2000))
```

Output:

```text
1180.0
2360.0
```

Advantages:
- Code reusability.
- Better organization.
- Easier debugging.
- Easier testing.
- Reduced code duplication.
- Better maintainability.

## 3. Defining a Function

We use the `def` keyword to define a function.

Syntax:

```python
def function_name():
    # Function body
    statement
```

Example:

```python
def greet():
    print("Hello, Python!")

```

Important:

Defining a function does not execute its body.

It only creates the function.

## 4. Calling a Function

To execute a function, we need to call it using its name followed by parentheses.

Example:

```python
def greet():
    print("Hello, Python!")

greet()
```

Output:

```text
Hello, Python!
```

Execution flow:

1. Python encounters the function definition.
2. Python creates the function object.
3. Python encounters `greet()`.
4. The function body executes.
5. Execution continues after the function call.

## 5. Functions Without Parameters

A function does not always need input.

Example:

```python
def display_message():
    print("Welcome to our application")

display_message()
display_message()
```

Output:

```text
Welcome to our application
Welcome to our application
```

The same function can be called multiple times.

## 6. Functions With Parameters

Parameters allow us to pass information into a function.

Example:

```python
def greet(name):
    print(f"Hello, {name}!")

greet("Arun")
greet("Priya")
```

Output:

```text
Hello, Arun!
Hello, Priya!
```

Here:
- `name` is a parameter.
- `"Arun"` and `"Priya"` are arguments.

Parameter: Variable declared in the function definition.

Argument: Actual value supplied during the function call.

## 7. Multiple Parameters

A function can accept multiple parameters.

Example:

```python
def employee_details(name, age, role):
    print(f"Name: {name}")
    print(f"Age: {age}")
    print(f"Role: {role}")

employee_details("Arun", 27, "Python Developer")
```

Output:

```text
Name: Arun
Age: 27
Role: Python Developer
```

The arguments are assigned to parameters based on their positions.

## 8. The return Statement

The `return` statement sends a result back to the caller.

Example:

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

What happens?

1. `add_numbers(10, 20)` is called.
2. `a` receives 10.
3. `b` receives 20.
4. Python calculates the sum.
5. `return` sends 30 to the caller.
6. The returned value is stored in `answer`.

## 9. Difference Between print() and return

This is an important concept.

Using print():

```python
def add_numbers(a, b):
    print(a + b)

result = add_numbers(10, 20)

print(result)
```

Output:

```text
30
None
```

Using return:

```python
def add_numbers(a, b):
    return a + b

result = add_numbers(10, 20)

print(result)
```

Output:

```text
30
```

Difference:

| print() | return |
|---|---|
| Displays information | Sends a value back |
| Does not return the displayed value | Returns the specified value |
| Useful for displaying output | Useful for further processing |
| Function continues after print | Function exits when return executes |

Important:

If a function does not explicitly return a value, Python returns `None`.

## 10. The return Statement Stops Function Execution

Example:

```python
def check_age(age):
    if age >= 18:
        return "Eligible"

    return "Not eligible"

    print("This statement will not execute")

print(check_age(25))
```

Output:

```text
Eligible
```

Once Python executes `return`, the function immediately exits.

## 11. Functions Returning Multiple Values

Python allows us to return multiple values.

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

Technically, Python packs these values into a tuple.

We can unpack them:

```python
def calculate(a, b):
    return a + b, a - b

total, difference = calculate(20, 10)

print(total)
print(difference)
```

Output:

```text
30
10
```

## 12. Functions and Type Hints

Type hints help communicate the expected types of parameters and return values.

Example:

```python
def calculate_total(price: float, quantity: int) -> float:
    return price * quantity

result = calculate_total(100.0, 3)

print(result)
```

Output:

```text
300.0
```

Explanation:

- `price: float` indicates the expected parameter type.
- `quantity: int` indicates the expected parameter type.
- `-> float` indicates the expected return type.

Important:

Python does not automatically enforce these type hints at runtime.

## 13. Function Execution Order

Example:

```python
def first():
    print("First function")

def second():
    print("Second function")

print("Program started")

second()
first()

print("Program completed")
```

Output:

```text
Program started
Second function
First function
Program completed
```

Remember:

Functions execute when called, not simply when defined.

A function can also call another function, provided the called function has been defined before that call is executed.

## 14. Practical Example: Customer Data Validation

Imagine you receive customer information from an external API.

You want to validate whether the customer has a valid name.

```python
def validate_customer(name):
    if not name or not name.strip():
        return False

    return True

customer_1 = validate_customer("Arun")
customer_2 = validate_customer("   ")

print(customer_1)
print(customer_2)
```

Output:

```text
True
False
```

This is a simple example of reusable validation logic.

## 15. Common Mistakes

### Mistake 1: Forgetting parentheses

Incorrect:

```python
def greet():
    print("Hello")

greet
```

Correct:

```python
greet()
```

Without parentheses, you are referencing the function rather than calling it.

### Mistake 2: Forgetting indentation

Incorrect:

```python
def greet():
print("Hello")
```

Correct:

```python
def greet():
    print("Hello")
```

### Mistake 3: Using print instead of return

Incorrect when a result is needed elsewhere:

```python
def multiply(a, b):
    print(a * b)

result = multiply(5, 4)
```

Here, `result` becomes `None`.

Correct:

```python
def multiply(a, b):
    return a * b

result = multiply(5, 4)
```

### Mistake 4: Incorrect number of arguments

```python
def greet(name):
    print(f"Hello {name}")

greet()
```

Output:

```text
TypeError
```

The function requires one argument, but none was supplied.

## 16. FDE Connection

Functions are fundamental when building production integrations.

For example, an FDE might create separate functions for:

```python
def fetch_customer_data():
    pass

def validate_customer_data():
    pass

def transform_customer_data():
    pass

def send_customer_data():
    pass
```

Each function handles one responsibility.

This makes it easier to:
- Integrate external APIs.
- Validate incoming JSON data.
- Transform customer records.
- Connect AI model responses to business systems.
- Test individual components.

These are placeholder functions because `pass` does not implement the actual operations.

## 17. Practical Exercises

### Exercise 1
Create a function called `greet()` that displays:

```text
Welcome to Python
```

### Exercise 2
Create a function that accepts two numbers and returns their multiplication.

### Exercise 3
Create a function that accepts a person's age and returns whether they are eligible to vote.

### Exercise 4
Create a function that accepts three numbers and returns their average.

### Exercise 5
Create a function that accepts a customer's name and email and returns both values as a tuple.

## 18. Quick Revision

| Concept | Meaning |
|---|---|
| `def` | Defines a function |
| Function call | Executes a function |
| Parameter | Variable in a function definition |
| Argument | Value passed during a function call |
| `return` | Sends a value back and exits the function |
| `print()` | Displays information |
| Type hints | Communicate expected types |
| `pass` | Placeholder statement |
| `None` | Default return value when no explicit return is executed |

## 19. Self-Assessment

You should be able to explain:

1. What is a function?
2. Why do we use functions?
3. What is the difference between defining and calling a function?
4. What is the difference between a parameter and an argument?
5. What is the difference between `print()` and `return`?
6. What happens when a function has no return statement?
7. Can a function return multiple values?
8. Are type hints enforced automatically by Python?


