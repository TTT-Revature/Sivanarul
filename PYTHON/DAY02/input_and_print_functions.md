
# Python `input()` and `print()`

**Suggested filename:** `20_input_and_print_functions.md`

## 1. Introduction

Python programs often need to communicate with users.

There are two basic operations involved:

1. **Input:** Receiving information from the user.
2. **Output:** Displaying information to the user.

Python provides two built-in functions for these operations:

- `input()` – receives input from the user.
- `print()` – displays output on the screen.

These functions are commonly used in beginner programs, command-line applications, testing, and debugging.

---

## 2. The `print()` Function

The `print()` function displays information on the screen.

### Syntax

```python
print(value)
```

### Example 1: Printing a message

```python
print("Hello, World!")
```

**Output:**

```text
Hello, World!
```

### Example 2: Printing variables

```python
name = "Sivanarul"
age = 27

print(name)
print(age)
```

**Output:**

```text
Sivanarul
27
```

### Example 3: Printing multiple values

We can pass multiple values to the `print()` function by separating them with commas.

```python
name = "Sivanarul"
age = 27
city = "Chennai"

print(name, age, city)
```

**Output:**

```text
Sivanarul 27 Chennai
```

By default, Python separates multiple values using a space.

---

## 3. Important Parameters of `print()`

The `print()` function supports several parameters.

The most commonly used parameters are:

| Parameter | Purpose |
|---|---|
| `sep` | Defines the separator between multiple values |
| `end` | Defines what is printed at the end |
| `file` | Specifies where the output should be written |
| `flush` | Controls whether the output is forcibly flushed |

### 3.1 The `sep` Parameter

By default, Python separates multiple values using a space.

We can change this using `sep`.

**Example:**

```python
name = "Sivanarul"
age = 27
city = "Chennai"

print(name, age, city, sep=" | ")
```

**Output:**

```text
Sivanarul | 27 | Chennai
```

Another example:

```python
print("2026", "11", "17", sep="-")
```

**Output:**

```text
2026-11-17
```

### 3.2 The `end` Parameter

By default, the `print()` function moves to a new line after displaying its output.

This happens because the default value of `end` is `"\n"`.

**Example:**

```python
print("Hello")
print("Python")
```

**Output:**

```text
Hello
Python
```

We can change this behavior using `end`.

**Example:**

```python
print("Hello", end=" ")
print("Python")
```

**Output:**

```text
Hello Python
```

Another example:

```python
print("Loading", end="...")
print("Completed")
```

**Output:**

```text
Loading...Completed
```

### Difference Between `sep` and `end`

| Parameter | Purpose |
|---|---|
| `sep` | Controls the separator between multiple arguments |
| `end` | Controls what happens after the printed output |

Example:

```python
print("Python", "Developer", sep="-", end="!")
print(" Welcome")
```

**Output:**

```text
Python-Developer! Welcome
```

---

## 4. Printing Different Data Types

The `print()` function can display different Python data types.

```python
name = "Sivanarul"
age = 27
salary = 41666.50
is_developer = True
skills = ["Python", "FastAPI", "AI"]

print(name)
print(age)
print(salary)
print(is_developer)
print(skills)
```

**Output:**

```text
Sivanarul
27
41666.5
True
['Python', 'FastAPI', 'AI']
```

Python automatically converts objects into their printable string representation when displaying them.

---

## 5. The `input()` Function

The `input()` function is used to receive information from the user through the keyboard.

### Syntax

```python
variable = input("Message displayed to the user")
```

The message inside `input()` is called a prompt.

### Example 1: Getting the user's name

```python
name = input("Enter your name: ")

print("Welcome", name)
```

**Sample execution:**

```text
Enter your name: Sivanarul
Welcome Sivanarul
```

### Example 2: Getting multiple inputs

```python
name = input("Enter your name: ")
city = input("Enter your city: ")
profession = input("Enter your profession: ")

print("Name:", name)
print("City:", city)
print("Profession:", profession)
```

**Sample execution:**

```text
Enter your name: Sivanarul
Enter your city: Chennai
Enter your profession: Developer

Name: Sivanarul
City: Chennai
Profession: Developer
```

---

## 6. Important Concept: `input()` Always Returns a String

One of the most important things to understand about `input()` is that it always returns a string (`str`).

Even if the user enters a number, Python initially treats that input as a string.

### Example

```python
age = input("Enter your age: ")

print(age)
print(type(age))
```

**Sample execution:**

```text
Enter your age: 27
27
<class 'str'>
```

Although the user entered `27`, Python stores it as a string.

### Why Does This Matter?

Consider the following example:

```python
num1 = input("Enter first number: ")
num2 = input("Enter second number: ")

result = num1 + num2

print(result)
```

**Sample execution:**

```text
Enter first number: 10
Enter second number: 20
1020
```

Why did Python produce `1020` instead of `30`?

Because both inputs are strings.

The `+` operator concatenates strings instead of performing numerical addition.

---

## 7. Type Conversion with `input()`

If we want to perform mathematical operations, we must convert the input into the appropriate numeric type.

### 7.1 Converting Input into an Integer

Use `int()` when you expect a whole number.

```python
num1 = int(input("Enter first number: "))
num2 = int(input("Enter second number: "))

result = num1 + num2

print("Total:", result)
```

**Sample execution:**

```text
Enter first number: 10
Enter second number: 20
Total: 30
```

### 7.2 Converting Input into a Float

Use `float()` when you expect decimal numbers.

```python
price = float(input("Enter product price: "))

quantity = int(input("Enter quantity: "))

total = price * quantity

print("Total amount:", total)
```

**Sample execution:**

```text
Enter product price: 99.50
Enter quantity: 3
Total amount: 298.5
```

### 7.3 Converting Input into a Boolean

Be careful when converting strings into Boolean values.

```python
value = input("Enter a value: ")

result = bool(value)

print(result)
```

**Sample execution:**

```text
Enter a value: False
True
```

Why?

Because every non-empty string is truthy, including `"False"` and `"0"`.

If you need to interpret textual Boolean values, validate them explicitly.

```python
value = input("Enter True or False: ").strip().lower()

if value == "true":
    result = True
elif value == "false":
    result = False
else:
    result = None

print(result)
```

**Sample execution:**

```text
Enter True or False: False
False
```

---

## 8. Using `print()` with f-Strings

An f-string is a convenient way to insert variables and expressions into a string.

It uses the `f` prefix before the string.

### Example

```python
name = "Sivanarul"
age = 27
profession = "Python Developer"

print(f"My name is {name}")
print(f"My age is {age}")
print(f"My profession is {profession}")
```

**Output:**

```text
My name is Sivanarul
My age is 27
My profession is Python Developer
```

### Example: Displaying Calculated Values

```python
num1 = 10
num2 = 20

result = num1 + num2

print(f"The sum of {num1} and {num2} is {result}")
```

**Output:**

```text
The sum of 10 and 20 is 30
```

### Formatting Decimal Values

```python
price = 99.5678

print(f"Price: {price:.2f}")
```

**Output:**

```text
Price: 99.57
```

Here, `.2f` displays the number with two digits after the decimal point.

---

## 9. Combining `input()` and `print()`

Both functions are commonly used together to create interactive programs.

### Example 1: Simple User Profile

```python
name = input("Enter your name: ")
age = int(input("Enter your age: "))
city = input("Enter your city: ")

print("\n----- USER PROFILE -----")

print(f"Name: {name}")
print(f"Age: {age}")
print(f"City: {city}")
```

**Sample execution:**

```text
Enter your name: Sivanarul
Enter your age: 27
Enter your city: Chennai

----- USER PROFILE -----
Name: Sivanarul
Age: 27
City: Chennai
```

### Example 2: Simple Calculator

```python
num1 = float(input("Enter first number: "))
num2 = float(input("Enter second number: "))

addition = num1 + num2
subtraction = num1 - num2
multiplication = num1 * num2

print("\n----- CALCULATOR -----")

print(f"Addition: {addition}")
print(f"Subtraction: {subtraction}")
print(f"Multiplication: {multiplication}")
```

**Sample execution:**

```text
Enter first number: 20
Enter second number: 10

----- CALCULATOR -----
Addition: 30.0
Subtraction: 10.0
Multiplication: 200.0
```

---

## 10. Handling Invalid User Input

Users do not always enter the expected data.

For example, a program may expect an integer, but the user enters text.

```python
age = int(input("Enter your age: "))
```

If the user enters `twenty`, Python raises a `ValueError`.

We can handle this using `try-except`.

### Example

```python
try:
    age = int(input("Enter your age: "))

    print(f"Your age is {age}")

except ValueError:
    print("Please enter a valid whole number.")
```

**Sample execution:**

```text
Enter your age: twenty
Please enter a valid whole number.
```

This makes the program more robust.

---

## 11. The Difference Between `input()` and `print()`

| Feature | `input()` | `print()` |
|---|---|---|
| Purpose | Receives user input | Displays output |
| Direction | User to program | Program to user |
| Return value | String | `None` |
| Accepts prompt | Yes | Not as a dedicated prompt parameter |
| Common usage | Collecting information | Displaying information |

### Important Observation

The `input()` function returns a string containing the user's input, without the trailing newline used to submit it.

The `print()` function returns `None`.

Example:

```python
result = print("Hello")

print(result)
```

**Output:**

```text
Hello
None
```

---

## 12. Common Mistakes

### Mistake 1: Forgetting Type Conversion

Incorrect:

```python
num1 = input("Enter first number: ")
num2 = input("Enter second number: ")

print(num1 + num2)
```

If the inputs are `10` and `20`, the output is `1020`.

Correct:

```python
num1 = int(input("Enter first number: "))
num2 = int(input("Enter second number: "))

print(num1 + num2)
```

### Mistake 2: Using `int()` for Decimal Input

Incorrect:

```python
price = int(input("Enter price: "))
```

This raises `ValueError` if the user enters `99.50`.

Correct:

```python
price = float(input("Enter price: "))
```

### Mistake 3: Assuming `"False"` Becomes `False`

Incorrect:

```python
value = bool(input("Enter value: "))
```

Entering `"False"` produces `True` because the string is non-empty.

Correct:

```python
value = input("Enter value: ").strip().lower()

if value == "true":
    result = True
elif value == "false":
    result = False
else:
    result = None
```

### Mistake 4: Confusing `sep` and `end`

- `sep` separates multiple arguments.
- `end` controls the ending of a print operation.

### Mistake 5: Forgetting That `print()` Returns `None`

`print()` displays information; it is not intended to return that information for further processing.

---

## 13. Real-World Relevance to Forward-Deployed Engineering (FDE)

In real-world FDE projects, applications frequently collect information and return results.

However, `input()` and `print()` are primarily associated with command-line programs.

In production systems, input and output may come from:

- REST API requests and responses.
- Web application forms.
- Database records.
- Configuration files.
- Message queues.
- AI model responses.

### Example: Simulating an API Input and Output

```python
customer_name = input("Enter customer name: ")
purchase_amount = float(input("Enter purchase amount: "))

customer_data = {
    "customer_name": customer_name,
    "purchase_amount": purchase_amount,
    "status": "processed"
}

print("\nCustomer Processing Result")
print(f"Customer: {customer_data['customer_name']}")
print(f"Amount: {customer_data['purchase_amount']}")
print(f"Status: {customer_data['status']}")
```

This example introduces a simple data collection and processing flow.

In a real FastAPI application:

- API endpoints receive request data.
- Python processes that data.
- API endpoints return structured responses, often JSON.
- Logging systems record application events instead of relying on `print()` for production monitoring.

### Why Should an FDE Understand This?

An FDE must understand how data enters a system, how it is processed, and how results are communicated.

These basic concepts provide the foundation for understanding API request-response cycles and application workflows.

---

## 14. Practice Exercises

### Beginner Level

**Exercise 1: Personal Information**

Write a program that collects:

- Name
- Age
- City
- Profession

Display all information using `print()`.

**Exercise 2: Addition**

Get two integer values from the user and display their sum.

**Exercise 3: Rectangle Area**

Get the length and width from the user and calculate the area.

Formula:

```text
Area = Length × Width
```

### Intermediate Level

**Exercise 4: Employee Salary**

Get the following information:

- Employee name
- Basic salary
- Bonus

Calculate and display the total salary.

**Exercise 5: Temperature Conversion**

Get the temperature in Celsius and convert it into Fahrenheit.

Formula:

```text
Fahrenheit = (Celsius × 9/5) + 32
```

**Exercise 6: Shopping Bill**

Get:

- Product name
- Product price
- Quantity

Calculate and display the total bill using an f-string.

### FDE-Oriented Practical Exercise

**Exercise 7: Customer Data Collection**

Build a simple command-line program that collects:

- Customer ID
- Customer name
- Email address
- Purchase amount

Store the information in a dictionary and display a formatted customer report.

Try handling invalid purchase amounts using `try-except`.

---

## 15. Quick Revision

| Concept | Explanation |
|---|---|
| `input()` | Receives information from the user |
| `print()` | Displays information |
| `int()` | Converts suitable input into an integer |
| `float()` | Converts suitable input into a floating-point number |
| `str()` | Converts an object into a string representation |
| `sep` | Separates multiple printed values |
| `end` | Controls what is printed at the end |
| `f-string` | Inserts values and expressions into strings |
| `try-except` | Handles exceptions such as invalid numeric input |
| `\n` | Represents a newline character |

---

## 16. Self-Assessment Questions

Try answering these without looking at the explanations.

1. What is the purpose of the `input()` function?
2. What is the return type of `input()`?
3. Why does `input() + input()` perform string concatenation?
4. What is the difference between `sep` and `end`?
5. What happens when we execute `int("hello")`?
6. What is an f-string?
7. Why does `bool("False")` return `True`?
8. What does the `print()` function return?
9. How can we handle invalid numeric input?
10. Why might production applications use logging instead of `print()`?

---

## 17. Learning Outcome

After completing this topic, you should understand:

- How to collect information using `input()`.
- How to display information using `print()`.
- How to work with `sep` and `end`.
- Why input values need type conversion.
- How to format output using f-strings.
- How to handle invalid user input.
- How basic input and output concepts relate to application workflows.


