
# Python argparse – Command-Line Argument Parsing



## 1. Introduction

In Python, command-line arguments allow users to provide information when executing a program through a terminal.

Previously, we learned about:

- `input()` – collects information while a program is running.
- `sys.argv` – receives command-line arguments as a list of strings.

However, `sys.argv` has some limitations:

- We must manually access arguments using indexes.
- We must manually validate argument counts.
- We must manually convert data types.
- We must write our own help instructions.
- Managing many arguments becomes difficult.

Python provides a built-in module called `argparse` to solve these problems.

**`argparse` is a Python standard-library module used to parse command-line arguments.**

It helps developers create user-friendly command-line applications.

---

## 2. What Is `argparse`?

`argparse` stands for argument parsing.

It allows us to define the arguments a program expects and automatically process the values supplied through the command line.

### Important Features

1. Defines positional and optional arguments.
2. Supports automatic type conversion.
3. Validates required arguments.
4. Provides automatic help messages.
5. Supports default values.
6. Supports choices and restrictions.
7. Produces useful error messages.

### Importing argparse

```python
import argparse
```

Unlike some external Python packages, `argparse` is included in Python's standard library. No additional installation is required.

---

## 3. Creating Your First Argument Parser

Let's create a simple command-line application.

### Python File: `app.py`

```python
import argparse

parser = argparse.ArgumentParser()

parser.add_argument("name")

args = parser.parse_args()

print(f"Welcome, {args.name}")
```

Let's understand the code step by step.

| Code | Explanation |
|---|---|
| `import argparse` | Imports the argument parsing module |
| `ArgumentParser()` | Creates an argument parser |
| `add_argument()` | Defines an argument |
| `parse_args()` | Reads and processes command-line arguments |
| `args.name` | Accesses the parsed argument value |

### Execute the Program

```bash
python app.py Sivanarul
```

**Output:**

```text
Welcome, Sivanarul
```

Here, `name` is a positional argument.

We must provide its value when executing the program.

---

## 4. Understanding Positional Arguments

A positional argument is an argument whose value is identified by its position in the command.

### Example

```python
import argparse

parser = argparse.ArgumentParser()

parser.add_argument("name")
parser.add_argument("city")

args = parser.parse_args()

print(f"Name: {args.name}")
print(f"City: {args.city}")
```

### Terminal Command

```bash
python app.py Sivanarul Chennai
```

**Output:**

```text
Name: Sivanarul
City: Chennai
```

The first value is assigned to `name`, and the second value is assigned to `city`.

### Important Observation

Argument order matters for positional arguments.

For example:

```bash
python app.py Chennai Sivanarul
```

The values will be assigned in the opposite order:

```text
Name: Chennai
City: Sivanarul
```

---

## 5. Understanding Optional Arguments

Optional arguments are arguments that can be identified by a flag or option name.

They usually begin with one or two hyphens.

- `-n` – short option
- `--name` – long option

### Example

```python
import argparse

parser = argparse.ArgumentParser()

parser.add_argument("--name")

args = parser.parse_args()

print(f"Name: {args.name}")
```

### Terminal Command

```bash
python app.py --name Sivanarul
```

**Output:**

```text
Name: Sivanarul
```

Unlike positional arguments, optional arguments can generally be provided in different orders.

### Example with Multiple Optional Arguments

```python
import argparse

parser = argparse.ArgumentParser()

parser.add_argument("--name")
parser.add_argument("--city")

args = parser.parse_args()

print(f"Name: {args.name}")
print(f"City: {args.city}")
```

Execution:

```bash
python app.py --city Chennai --name Sivanarul
```

**Output:**

```text
Name: Sivanarul
City: Chennai
```

---

## 6. Short and Long Argument Names

We can define both short and long names for the same argument.

### Example

```python
import argparse

parser = argparse.ArgumentParser()

parser.add_argument("-n", "--name")

args = parser.parse_args()

print(f"Name: {args.name}")
```

### Terminal Command

Using the short option:

```bash
python app.py -n Sivanarul
```

Using the long option:

```bash
python app.py --name Sivanarul
```

Both commands produce:

```text
Name: Sivanarul
```

The value is available through `args.name`.

---

## 7. Understanding `type` in argparse

By default, argument values are treated as strings.

We can specify the expected type using the `type` parameter.

### Example 1: Integer Argument

```python
import argparse

parser = argparse.ArgumentParser()

parser.add_argument("--age", type=int)

args = parser.parse_args()

print(args.age)
print(type(args.age))
```

Terminal command:

```bash
python app.py --age 27
```

**Output:**

```text
27
<class 'int'>
```

Here, `argparse` automatically converts the supplied value into an integer.

### Example 2: Float Argument

```python
import argparse

parser = argparse.ArgumentParser()

parser.add_argument("--temperature", type=float)

args = parser.parse_args()

print(args.temperature)
print(type(args.temperature))
```

Terminal command:

```bash
python app.py --temperature 0.7
```

**Output:**

```text
0.7
<class 'float'>
```

### Example 3: Multiple Data Types

```python
import argparse

parser = argparse.ArgumentParser()

parser.add_argument("--name", type=str)
parser.add_argument("--age", type=int)
parser.add_argument("--salary", type=float)

args = parser.parse_args()

print(f"Name: {args.name}")
print(f"Age: {args.age}")
print(f"Salary: {args.salary}")
```

Terminal command:

```bash
python app.py --name Sivanarul --age 27 --salary 41666.50
```

**Output:**

```text
Name: Sivanarul
Age: 27
Salary: 41666.5
```

If a supplied value cannot be converted into the specified type, `argparse` displays an error and exits.

---

## 8. Required Arguments

Sometimes an application cannot run without certain information.

We can use `required=True` to make an optional argument mandatory.

### Example

```python
import argparse

parser = argparse.ArgumentParser()

parser.add_argument(
    "--name",
    required=True
)

args = parser.parse_args()

print(f"Welcome, {args.name}")
```

### Execution 1: Without the Argument

```bash
python app.py
```

**Output:**

```text
usage: app.py [-h] --name NAME
app.py: error: the following arguments are required: --name
```

### Execution 2: With the Argument

```bash
python app.py --name Sivanarul
```

**Output:**

```text
Welcome, Sivanarul
```

**Important:** Positional arguments are already required by default unless configured otherwise. The `required=True` parameter is mainly used with optional arguments.

---

## 9. Default Values

We can assign default values to optional arguments using `default`.

If the user does not provide an argument, the default value is used.

### Example

```python
import argparse

parser = argparse.ArgumentParser()

parser.add_argument(
    "--city",
    default="Chennai"
)

args = parser.parse_args()

print(f"City: {args.city}")
```

### Execution 1: Without Supplying a Value

```bash
python app.py
```

**Output:**

```text
City: Chennai
```

### Execution 2: Supplying a Value

```bash
python app.py --city Bangalore
```

**Output:**

```text
City: Bangalore
```

Default values are useful when applications have standard configurations.

---

## 10. Help Messages and Descriptions

One of the most useful features of `argparse` is its automatic help generation.

We can provide descriptions using the `description` and `help` parameters.

### Example

```python
import argparse

parser = argparse.ArgumentParser(
    description="Employee information management application"
)

parser.add_argument(
    "--name",
    required=True,
    help="Enter employee name"
)

parser.add_argument(
    "--age",
    type=int,
    required=True,
    help="Enter employee age"
)

args = parser.parse_args()

print(f"Employee Name: {args.name}")
print(f"Employee Age: {args.age}")
```

### Terminal Command

```bash
python app.py --help
```

**Example Output:**

```text
usage: app.py [-h] --name NAME --age AGE

Employee information management application

options:
  -h, --help   show this help message and exit
  --name NAME  Enter employee name
  --age AGE    Enter employee age
```

We did not write a separate help function.

`argparse` generated the help message automatically.

---

## 11. Restricting Values Using `choices`

Sometimes we want to allow only specific values.

For example, an application may support only:

- Development
- Testing
- Production

We can use the `choices` parameter.

### Example

```python
import argparse

parser = argparse.ArgumentParser()

parser.add_argument(
    "--environment",
    choices=["development", "testing", "production"],
    required=True
)

args = parser.parse_args()

print(f"Environment: {args.environment}")
```

### Valid Execution

```bash
python app.py --environment development
```

**Output:**

```text
Environment: development
```

### Invalid Execution

```bash
python app.py --environment staging
```

**Output:**

```text
app.py: error: argument --environment: invalid choice: 'staging'
```

This helps restrict command-line values to an approved set.

---

## 12. Boolean Flags Using `action`

Some arguments do not require a separate value.

For example, we may want to enable debugging by passing a flag.

We can use `action="store_true"`.

### Example

```python
import argparse

parser = argparse.ArgumentParser()

parser.add_argument(
    "--debug",
    action="store_true"
)

args = parser.parse_args()

print(f"Debug Mode: {args.debug}")
```

### Execution 1: Without the Flag

```bash
python app.py
```

**Output:**

```text
Debug Mode: False
```

### Execution 2: With the Flag

```bash
python app.py --debug
```

**Output:**

```text
Debug Mode: True
```

### Understanding `store_true`

| User command | Result |
|---|---|
| No `--debug` | `False` |
| With `--debug` | `True` |

For the opposite behavior, Python also provides `action="store_false"`.

---

## 13. Accepting Multiple Values Using `nargs`

Sometimes an application needs more than one value for a single argument.

We can use `nargs` to specify how many values should be accepted.

### Example 1: Fixed Number of Values

```python
import argparse

parser = argparse.ArgumentParser()

parser.add_argument(
    "--numbers",
    nargs=3,
    type=int
)

args = parser.parse_args()

print(args.numbers)
```

Terminal command:

```bash
python app.py --numbers 10 20 30
```

**Output:**

```text
[10, 20, 30]
```

### Example 2: One or More Values

```python
import argparse

parser = argparse.ArgumentParser()

parser.add_argument(
    "--skills",
    nargs="+"
)

args = parser.parse_args()

print(args.skills)
```

Terminal command:

```bash
python app.py --skills Python FastAPI SQL
```

**Output:**

```text
['Python', 'FastAPI', 'SQL']
```

### Common `nargs` Values

| Value | Meaning |
|---|---|
| `1` | Exactly one value |
| `2` | Exactly two values |
| `+` | One or more values |
| `*` | Zero or more values |
| `?` | Zero or one value |

---

## 14. Argument Groups

When an application has many arguments, we can organize them into groups.

This improves the help message and makes the CLI easier to understand.

### Example

```python
import argparse

parser = argparse.ArgumentParser(
    description="AI application configuration"
)

model_group = parser.add_argument_group("Model Configuration")

model_group.add_argument(
    "--model",
    default="llama3.2",
    help="AI model name"
)

model_group.add_argument(
    "--temperature",
    type=float,
    default=0.7,
    help="Model temperature"
)

runtime_group = parser.add_argument_group("Runtime Configuration")

runtime_group.add_argument(
    "--debug",
    action="store_true",
    help="Enable debug mode"
)

args = parser.parse_args()

print(f"Model: {args.model}")
print(f"Temperature: {args.temperature}")
print(f"Debug: {args.debug}")
```

Terminal command:

```bash
python ai_app.py --model llama3.2 --temperature 0.5 --debug
```

**Output:**

```text
Model: llama3.2
Temperature: 0.5
Debug: True
```

Argument groups help organize larger command-line applications.

---

## 15. Practical Example: AI Application Configuration

Let's combine several `argparse` concepts into one practical example.

Imagine that we are building an AI application that accepts model configuration through the command line.

### Python File: `ai_app.py`

```python
import argparse

parser = argparse.ArgumentParser(
    description="AI Model Configuration Tool"
)

parser.add_argument(
    "--model",
    type=str,
    default="llama3.2",
    help="AI model name"
)

parser.add_argument(
    "--temperature",
    type=float,
    default=0.7,
    help="Model temperature"
)

parser.add_argument(
    "--max-tokens",
    type=int,
    default=2048,
    help="Maximum output token count"
)

parser.add_argument(
    "--debug",
    action="store_true",
    help="Enable debug mode"
)

args = parser.parse_args()

print("=" * 40)
print("AI APPLICATION CONFIGURATION")
print("=" * 40)

print(f"Model       : {args.model}")
print(f"Temperature : {args.temperature}")
print(f"Max Tokens  : {args.max_tokens}")
print(f"Debug Mode  : {args.debug}")

print("=" * 40)
```

### Terminal Command

```bash
python ai_app.py --model llama3.2 --temperature 0.5 --max-tokens 4096 --debug
```

**Output:**

```text
========================================
AI APPLICATION CONFIGURATION
========================================
Model       : llama3.2
Temperature : 0.5
Max Tokens  : 4096
Debug Mode  : True
========================================
```

This example demonstrates command-line configuration for an AI application.

It does not actually load or execute the AI model.

---

## 16. Understanding the Difference Between `sys.argv` and `argparse`

Both approaches work with command-line arguments, but their responsibilities are different.

| Feature | `sys.argv` | `argparse` |
|---|---|---|
| Type | List of strings | Argument parsing framework |
| Manual indexing | Required | Not required |
| Automatic type conversion | No | Yes, using `type` |
| Required arguments | Manual validation | Built-in support |
| Default values | Manual implementation | Built-in support |
| Help messages | Manual implementation | Automatic |
| Choices validation | Manual implementation | Built-in support |
| Multiple values | Manual processing | Supports `nargs` |
| Best suited for | Small scripts | Structured CLI applications |

### Important Understanding

`argparse` uses the command-line arguments supplied to the Python process. By default, it reads from `sys.argv`.

We can also provide a custom list to `parse_args()` when testing or processing arguments programmatically.

---

## 17. Common Mistakes

| Mistake | Explanation |
|---|---|
| Forgetting `import argparse` | The module must be imported |
| Forgetting `parse_args()` | Arguments are not parsed until this method is called |
| Using incorrect argument names | The attribute name is normally derived from the argument name |
| Forgetting `type=int` | Values remain strings by default |
| Using `required=True` unnecessarily for positional arguments | Positional arguments are required by default |
| Incorrect `choices` values | Supplied values must match an allowed choice |
| Passing a value to `store_true` | The flag itself enables the Boolean value |
| Forgetting the `--` prefix | Optional arguments must be called using their defined option strings |

---

## 18. Practice Exercises

### Beginner Level

**Exercise 1: Personal Information**

Create a program that accepts:

- Name
- Age
- City

Use `argparse` and display the values.

**Exercise 2: Calculator**

Accept two integer arguments and display their sum.

**Exercise 3: Default Values**

Create a program that accepts a city argument with a default value of Chennai.

Display the default when no value is provided.

### Intermediate Level

**Exercise 4: Employee Salary Calculator**

Accept:

- Employee name
- Basic salary
- Bonus

Calculate and display the total salary.

Use appropriate argument types.

**Exercise 5: Environment Configuration**

Create an application that accepts an environment value.

Allowed choices:

- development
- testing
- production

Reject all other values.

**Exercise 6: Multiple Skills**

Accept multiple skills using `nargs="+"`.

Example:

```bash
python app.py --skills Python SQL FastAPI Docker
```

Display all supplied skills.

### FDE-Oriented Practical Exercises

**Exercise 7: AI Model Configuration**

Build a CLI tool that accepts:

- Model name
- Temperature
- Maximum tokens
- Debug mode

Use default values and appropriate data types.

**Exercise 8: Data Processing CLI**

Create a program that accepts:

- Input filename
- Output filename
- Processing mode

Allowed processing modes:

- clean
- validate
- transform

Requirements:

1. Input filename is required.
2. Output filename is optional.
3. Processing mode must use `choices`.
4. Provide meaningful help messages.
5. Display the selected configuration.

---

## 19. Quick Revision

| Concept | Purpose |
|---|---|
| `argparse` | Command-line argument parsing |
| `ArgumentParser()` | Creates an argument parser |
| `add_argument()` | Defines an argument |
| `parse_args()` | Parses supplied arguments |
| Positional argument | Argument identified by position |
| Optional argument | Argument identified by a flag |
| `type` | Specifies the expected argument type |
| `required` | Makes an optional argument mandatory |
| `default` | Defines a default value |
| `choices` | Restricts accepted values |
| `help` | Adds argument documentation |
| `description` | Describes the application |
| `action="store_true"` | Creates a Boolean flag |
| `nargs` | Controls the number of accepted values |
| `add_argument_group()` | Organizes arguments into groups |

---

## 20. Self-Assessment Questions

1. What is `argparse`?
2. Why do we use `argparse` instead of manually accessing `sys.argv`?
3. What is the purpose of `ArgumentParser()`?
4. What does `add_argument()` do?
5. What happens when we call `parse_args()`?
6. What is the difference between positional and optional arguments?
7. What is the purpose of the `type` parameter?
8. How do we define a mandatory optional argument?
9. What is the purpose of `default`?
10. How does `choices` work?
11. What is the difference between `store_true` and `store_false`?
12. What does `nargs="+"` mean?
13. How does `argparse` generate help messages?
14. Where does `argparse` normally obtain its command-line arguments?
15. In which situations would an FDE use `argparse`?

---

## 21. Learning Outcome

After completing this topic, you should understand:

- What command-line argument parsing means.
- How to create an argument parser.
- How to define positional and optional arguments.
- How to use short and long argument names.
- How to perform automatic type conversion.
- How to configure required and default values.
- How to validate inputs using `choices`.
- How to create Boolean flags.
- How to accept multiple values.
- How to organize arguments using groups.
- How to build a basic configuration CLI for an AI application.


