
# Python `sys.argv` – Command-Line Arguments


## 1. Introduction

In Python, we can provide information to a program in different ways.

So far, we have learned:

- `input()` – collects information from the user while the program is running.
- `print()` – displays information on the screen.
- f-Strings – format dynamic output.

Now, let's understand another approach: **Command-Line Arguments**.

Command-line arguments allow us to pass information to a Python program when executing it from a terminal.

Python provides the `sys` module to access command-line arguments.

The `argv` attribute inside the `sys` module stores these arguments.

---

## 2. What Is `sys.argv`?

`sys.argv` is a list containing the command-line arguments passed to a Python program.

It is available through Python's built-in `sys` module.

### Syntax

```python
import sys

sys.argv
```

### Important Points

1. `sys` is a built-in Python module.
2. `argv` stands for argument vector.
3. `sys.argv` returns a list.
4. The first element, `sys.argv[0]`, normally contains the script name or path used to execute the script.
5. Arguments supplied after the script name are stored from index `1`.
6. All command-line arguments are received as strings.

---

## 3. First Example: Understanding `sys.argv`

Create a Python file named:

```text
app.py
```

Write the following code:

```python
import sys

print(sys.argv)
```

Run the program from your terminal:

```bash
python app.py
```

**Output:**

```text
['app.py']
```

Why?

Because we did not pass any additional arguments.

The list contains only the script name.

Now execute:

```bash
python app.py Sivanarul
```

**Output:**

```text
['app.py', 'Sivanarul']
```

We passed one argument, `Sivanarul`.

Python added it to the `sys.argv` list.

---

## 4. Understanding the Index Positions

Let's pass multiple arguments.

### Python File

```python
import sys

print(sys.argv)
```

### Terminal Command

```bash
python app.py Sivanarul 27 Chennai
```

**Output:**

```text
['app.py', 'Sivanarul', '27', 'Chennai']
```

Let's understand the index positions.

| Index | Value |
|---|---|
| `sys.argv[0]` | `app.py` |
| `sys.argv[1]` | `Sivanarul` |
| `sys.argv[2]` | `27` |
| `sys.argv[3]` | `Chennai` |

We can access each argument using its index.

### Example

```python
import sys

script_name = sys.argv[0]
name = sys.argv[1]
age = sys.argv[2]
city = sys.argv[3]

print(f"Script: {script_name}")
print(f"Name: {name}")
print(f"Age: {age}")
print(f"City: {city}")
```

### Terminal Command

```bash
python app.py Sivanarul 27 Chennai
```

**Output:**

```text
Script: app.py
Name: Sivanarul
Age: 27
City: Chennai
```

---

## 5. Important Concept: `sys.argv` Stores Strings

One of the most important concepts is that every command-line argument is initially received as a string.

Even if we pass a number, Python stores it as a string.

### Example

```python
import sys

age = sys.argv[1]

print(age)
print(type(age))
```

### Terminal Command

```bash
python app.py 27
```

**Output:**

```text
27
<class 'str'>
```

Although we passed `27`, Python received it as a string.

If we want to perform mathematical operations, we need type conversion.

### Example: Converting Arguments into Integers

```python
import sys

num1 = int(sys.argv[1])
num2 = int(sys.argv[2])

result = num1 + num2

print(f"Result: {result}")
```

### Terminal Command

```bash
python app.py 10 20
```

**Output:**

```text
Result: 30
```

---

## 6. Difference Between `input()` and `sys.argv`

Both approaches collect information, but they work differently.

### Using `input()`

```python
name = input("Enter your name: ")

print(f"Welcome, {name}")
```

Execution:

```bash
python app.py
```

The program asks for the name after it starts.

### Using `sys.argv`

```python
import sys

name = sys.argv[1]

print(f"Welcome, {name}")
```

Execution:

```bash
python app.py Sivanarul
```

The name is supplied when launching the program.

### Comparison

| Feature | `input()` | `sys.argv` |
|---|---|---|
| Input method | Interactive | Command-line |
| When input is provided | During execution | When launching the program |
| Return/data type | String | List of strings |
| Requires `sys` module | No | Yes |
| Suitable for automation | Less convenient | Convenient for simple scripts |
| User interaction | Usually waits for input | Does not prompt automatically |

---

## 7. Using `len(sys.argv)`

We can use the `len()` function to determine how many items are present in the argument list.

Remember that the script name is also included.

### Example

```python
import sys

print(sys.argv)
print(f"Total arguments including script name: {len(sys.argv)}")
```

### Terminal Command

```bash
python app.py Sivanarul 27 Chennai
```

**Output:**

```text
['app.py', 'Sivanarul', '27', 'Chennai']
Total arguments including script name: 4
```

There are three user-supplied arguments, but the list contains four elements because the script name is included.

To count only the user-supplied arguments:

```python
import sys

argument_count = len(sys.argv) - 1

print(f"User-supplied arguments: {argument_count}")
```

**Output:**

```text
User-supplied arguments: 3
```

---

## 8. Handling Missing Arguments

What happens if we try to access an argument that was not provided?

Consider:

```python
import sys

name = sys.argv[1]

print(name)
```

Now execute:

```bash
python app.py
```

**Output:**

```text
IndexError: list index out of range
```

Why?

Because the list contains only one element:

```python
['app.py']
```

There is no element at index `1`.

### Solution: Validate the Argument Count

```python
import sys

if len(sys.argv) < 2:
    print("Usage: python app.py <name>")
else:
    name = sys.argv[1]
    print(f"Welcome, {name}")
```

**Execution 1:**

```bash
python app.py
```

Output:

```text
Usage: python app.py <name>
```

**Execution 2:**

```bash
python app.py Sivanarul
```

Output:

```text
Welcome, Sivanarul
```

This makes the program more reliable.

---

## 9. Practical Example: Simple Calculator Using `sys.argv`

Let's create a calculator that receives two numbers through command-line arguments.

### Python File: `calculator.py`

```python
import sys

if len(sys.argv) != 3:
    print("Usage: python calculator.py <num1> <num2>")
else:
    num1 = float(sys.argv[1])
    num2 = float(sys.argv[2])

    result = num1 + num2

    print(f"First number: {num1}")
    print(f"Second number: {num2}")
    print(f"Addition: {result}")
```

### Terminal Command

```bash
python calculator.py 10 20
```

**Output:**

```text
First number: 10.0
Second number: 20.0
Addition: 30.0
```

Note: This example validates the argument count but does not yet handle invalid numeric input.

A safer version uses `try-except`.

```python
import sys

if len(sys.argv) != 3:
    print("Usage: python calculator.py <num1> <num2>")
else:
    try:
        num1 = float(sys.argv[1])
        num2 = float(sys.argv[2])

        result = num1 + num2

        print(f"Addition: {result}")

    except ValueError:
        print("Error: Please provide valid numbers.")
```

---

## 10. Practical Example: File Processing

Command-line arguments are useful when creating scripts that process files.

Imagine that we have a Python program that reads a text file.

### Python File: `read_file.py`

```python
import sys

if len(sys.argv) != 2:
    print("Usage: python read_file.py <filename>")
else:
    filename = sys.argv[1]

    try:
        with open(filename, "r", encoding="utf-8") as file:
            content = file.read()

        print(content)

    except FileNotFoundError:
        print("Error: File not found.")
```

### Terminal Command

```bash
python read_file.py notes.txt
```

The program receives the filename through `sys.argv`, opens the file, and displays its contents.

This is a basic example of a command-line file-processing utility.

---

## 11. Practical Example: Passing AI Model Configuration

In AI engineering and FDE projects, we may need to configure scripts before execution.

For example, we might want to provide a model name when launching an AI application.

### Python File: `ai_app.py`

```python
import sys

if len(sys.argv) != 2:
    print("Usage: python ai_app.py <model_name>")
else:
    model_name = sys.argv[1]

    print("AI Application Configuration")
    print(f"Selected model: {model_name}")
    print("Application started.")
```

### Terminal Command

```bash
python ai_app.py llama3.2
```

**Output:**

```text
AI Application Configuration
Selected model: llama3.2
Application started.
```

This example only demonstrates configuration input. It does not actually load or execute an AI model.

---

## 12. Understanding the `sys` Module

`sys.argv` is one attribute of the `sys` module.

The `sys` module provides access to information and functionality related to the Python interpreter.

Some commonly used attributes and functions include:

| Attribute / Function | Purpose |
|---|---|
| `sys.argv` | Command-line arguments |
| `sys.path` | Module search paths |
| `sys.version` | Python version information |
| `sys.platform` | Platform identifier |
| `sys.executable` | Path to the Python interpreter executable |
| `sys.exit()` | Terminates the program |
| `sys.getsizeof()` | Returns the shallow size of an object in bytes |

### Example

```python
import sys

print("Python Version:", sys.version)
print("Platform:", sys.platform)
print("Interpreter:", sys.executable)
print("Arguments:", sys.argv)
```

These are useful when debugging Python environments and command-line applications.

---

## 13. Limitations of `sys.argv`

Although `sys.argv` is simple and useful, it has limitations.

1. It does not automatically validate argument types.
2. It does not automatically validate required arguments.
3. It does not provide built-in help messages.
4. It does not automatically distinguish between named and positional arguments.
5. It requires manual parsing and validation.

For small scripts, `sys.argv` is sufficient.

For larger command-line applications, Python provides the `argparse` module.

### Example: Introducing `argparse`

```python
import argparse

parser = argparse.ArgumentParser(
    description="Simple employee information program"
)

parser.add_argument(
    "--name",
    required=True,
    help="Employee name"
)

parser.add_argument(
    "--age",
    type=int,
    required=True,
    help="Employee age"
)

args = parser.parse_args()

print(f"Employee Name: {args.name}")
print(f"Employee Age: {args.age}")
```

### Terminal Command

```bash
python app.py --name Sivanarul --age 27
```

**Output:**

```text
Employee Name: Sivanarul
Employee Age: 27
```

Here, `argparse` handles argument parsing and provides useful features such as validation and automatic help messages.

We will study command-line argument parsing in more detail separately.

---

## 14. Common Mistakes

| Mistake | Explanation |
|---|---|
| Forgetting `import sys` | Python cannot access `sys.argv` without importing the module |
| Accessing a missing index | Causes `IndexError` |
| Assuming arguments are integers | All command-line arguments are initially strings |
| Forgetting `int()` or `float()` | Mathematical operations may perform string concatenation or fail |
| Miscounting arguments | `sys.argv[0]` is included in the list |
| Ignoring invalid input | Conversion may raise `ValueError` |
| Assuming `sys.argv` is a function | It is a list attribute of the `sys` module |

---

## 15. Practice Exercises

### Beginner Level

**Exercise 1: Display Arguments**

Create a Python program that displays the complete `sys.argv` list.

Run it with three arguments.

**Exercise 2: Personal Information**

Pass the following details through the terminal:

- Name
- Age
- City

Display the details using f-Strings.

**Exercise 3: Argument Counter**

Write a program that displays the number of user-supplied arguments, excluding the script name.

### Intermediate Level

**Exercise 4: Calculator**

Create a program that accepts two numbers through `sys.argv` and displays:

- Addition
- Subtraction
- Multiplication
- Division

Handle division by zero and invalid numeric values.

**Exercise 5: Employee Salary Calculator**

Pass the following values through the command line:

- Employee name
- Basic salary
- Bonus

Calculate and display the total salary.

**Exercise 6: File Reader**

Create a program that receives a filename and displays its contents.

Handle the case where the file does not exist.

### FDE-Oriented Practical Exercise

**Exercise 7: AI Application Configuration**

Create a Python program that receives:

- Model name
- Temperature
- Maximum token count

Example execution:

```bash
python ai_app.py llama3.2 0.7 2048
```

Expected output:

```text
AI Application Configuration
Model: llama3.2
Temperature: 0.7
Maximum Tokens: 2048
```

Requirements:

1. Use `sys.argv`.
2. Validate the argument count.
3. Convert temperature into a float.
4. Convert maximum tokens into an integer.
5. Handle invalid values using `try-except`.

This exercise introduces the idea of configuring an AI application from the command line.

---

## 16. Quick Revision

| Concept | Explanation |
|---|---|
| `sys` | Built-in Python module |
| `sys.argv` | List of command-line arguments |
| `sys.argv[0]` | Script name or execution path |
| `sys.argv[1]` | First user-supplied argument |
| `len(sys.argv)` | Total number of list elements, including the script |
| `len(sys.argv) - 1` | Number of user-supplied arguments |
| `int()` | Converts suitable argument strings into integers |
| `float()` | Converts suitable argument strings into floats |
| `IndexError` | Occurs when accessing an unavailable list index |
| `ValueError` | Can occur when converting invalid input |
| `argparse` | More advanced command-line argument parsing module |

---

## 17. Self-Assessment Questions

1. What is `sys.argv`?
2. What does `argv` stand for?
3. Why do we import the `sys` module?
4. What is stored at index `0`?
5. Why are command-line arguments initially strings?
6. What happens when we access a missing argument?
7. What is the difference between `input()` and `sys.argv`?
8. Why do we use `len(sys.argv)`?
9. What is the purpose of the `argparse` module?
10. Why is command-line configuration useful for automation?
11. What is the difference between `sys.argv` and `sys.path`?
12. How can command-line arguments help configure an AI application?

---

## 18. Learning Outcome

After completing this topic, you should understand:

- What command-line arguments are.
- How to use `sys.argv`.
- How to access arguments using list indexes.
- Why command-line arguments are strings.
- How to perform type conversion.
- How to validate argument counts.
- How to handle missing and invalid arguments.
- How to use command-line inputs in automation and AI application configuration.
- When to use `sys.argv` and when to use `argparse`.

**Next Suggested Topic:** Python Strings – Creation, Indexing and Basic Operations
