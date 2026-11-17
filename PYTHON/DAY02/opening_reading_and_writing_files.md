
# 44. Opening, Reading and Writing Files in Python

**Suggested filename:** `44_opening_reading_and_writing_files.md`

## 1. Introduction

So far, we have stored data in variables, lists, dictionaries, and other Python objects.

But there is one limitation:

When a Python program finishes execution, its variables normally disappear.

How can we store information permanently?

We use **files**.

Python allows us to:
- Create files.
- Open existing files.
- Read file contents.
- Write new content.
- Append content without deleting existing data.
- Close files after working with them.

File handling is important in real-world software development because applications frequently interact with text files, CSV files, JSON files, logs, and configuration files.

---

## 2. Understanding the `open()` Function

Python provides the built-in `open()` function to open a file.

### Syntax

```python
file = open("filename.txt", "mode")
```

Parameters:

- `filename`: Name or path of the file.
- `mode`: Specifies how the file should be opened.

Example:

```python
file = open("sample.txt", "r")
```

This opens `sample.txt` in read mode.

**Important:** Opening a file does not automatically read its contents.

---

## 3. File Opening Modes

Python provides different file modes.

| Mode | Description |
|---|---|
| `r` | Read an existing file |
| `w` | Write to a file; creates it or overwrites existing content |
| `a` | Append content to the end of a file |
| `x` | Create a new file; raises an error if it already exists |
| `r+` | Read and write an existing file |
| `w+` | Read and write; overwrites existing content |
| `a+` | Read and append; creates the file if necessary |

### Understanding the most important modes

**Read mode (`r`)**

```python
file = open("data.txt", "r")
```

- Opens an existing file.
- Raises `FileNotFoundError` if the file does not exist.
- Does not modify the file.

**Write mode (`w`)**

```python
file = open("data.txt", "w")
```

- Creates the file if it does not exist.
- Deletes the existing contents if the file already exists.
- Writes new content.

**Append mode (`a`)**

```python
file = open("data.txt", "a")
```

- Creates the file if it does not exist.
- Preserves existing content.
- Adds new content at the end.

**Exclusive creation mode (`x`)**

```python
file = open("data.txt", "x")
```

- Creates a new file.
- Raises `FileExistsError` if the file already exists.

---

## 4. Reading Files Using `read()`

The `read()` method reads the contents of a file.

### Example

Assume `students.txt` contains:

```text
Arun
Kumar
Sivan
```

Python code:

```python
file = open("students.txt", "r")

content = file.read()

print(content)

file.close()
```

### Output

```text
Arun
Kumar
Sivan
```

### Understanding the code

1. `open()` opens the file.
2. `read()` retrieves its contents as a string.
3. `print()` displays the contents.
4. `close()` closes the file.

### Reading a limited number of characters

```python
file = open("students.txt", "r")

content = file.read(4)

print(content)

file.close()
```

### Output

```text
Arun
```

`read(4)` reads up to four characters from the current file position.

**Important:** After reading, the file cursor moves forward. Calling `read()` again continues from the current position.

Example:

```python
file = open("students.txt", "r")

print(file.read(4))
print(file.read(3))

file.close()
```

Output:

```text
Arun

Ku
```

The second call reads the next three characters, including the newline character after `Arun`.

---

## 5. Reading Files Using `readline()`

The `readline()` method reads one line at a time.

Example:

```python
file = open("students.txt", "r")

line1 = file.readline()
line2 = file.readline()

print(line1)
print(line2)

file.close()
```

Output:

```text
Arun

Kumar
```

### Reading all lines using repeated `readline()`

```python
file = open("students.txt", "r")

while True:
    line = file.readline()

    if line == "":
        break

    print(line.strip())

file.close()
```

Output:

```text
Arun
Kumar
Sivan
```

**Explanation:**

- `readline()` returns the next line.
- At the end of the file, it returns an empty string (`""`).
- `break` stops the loop.
- `strip()` removes surrounding whitespace, including the newline character.

---

## 6. Reading Files Using `readlines()`

The `readlines()` method reads all remaining lines and returns them as a list of strings.

Example:

```python
file = open("students.txt", "r")

lines = file.readlines()

print(lines)

file.close()
```

Output:

```python
['Arun\n', 'Kumar\n', 'Sivan\n']
```

Notice:

- The result is a list.
- Each line is represented as a string.
- The newline character `\n` may be included.

### Processing the list

```python
file = open("students.txt", "r")

lines = file.readlines()

for line in lines:
    print(line.strip())

file.close()
```

Output:

```text
Arun
Kumar
Sivan
```

**Important:** `readlines()` loads all remaining lines into memory. For very large files, iterating directly over the file is generally more memory-efficient.

---

## 7. Writing Files Using `write()`

The `write()` method writes a string into a file.

Example:

```python
file = open("employee.txt", "w")

file.write("Employee Name: Arun")

file.close()
```

The file will contain:

```text
Employee Name: Arun
```

### Writing multiple lines

```python
file = open("employee.txt", "w")

file.write("Employee Name: Arun\n")
file.write("Department: Python Development\n")
file.write("Experience: 4 Years\n")

file.close()
```

File content:

```text
Employee Name: Arun
Department: Python Development
Experience: 4 Years
```

**Important:** `write()` does not automatically add a newline. Use `\n` when you want a new line.

### Writing a list of strings using `writelines()`

```python
file = open("employees.txt", "w")

employees = [
    "Arun\n",
    "Kumar\n",
    "Sivan\n"
]

file.writelines(employees)

file.close()
```

File content:

```text
Arun
Kumar
Sivan
```

**Remember:** `writelines()` does not automatically insert newline characters between strings.

---

## 8. Appending Data Using `a`

Append mode adds new content without deleting existing content.

Assume `employees.txt` contains:

```text
Arun
Kumar
```

Python code:

```python
file = open("employees.txt", "a")

file.write("\nSivan")

file.close()
```

Updated file content:

```text
Arun
Kumar
Sivan
```

### Difference between `w` and `a`

| Feature | `w` mode | `a` mode |
|---|---|---|
| Creates missing file | Yes | Yes |
| Preserves old content | No | Yes |
| Adds content at the end | Not necessarily | Yes |
| Overwrites existing content | Yes | No |

This distinction is extremely important when working with logs and records.

---

## 9. Closing Files Using `close()`

After completing file operations, close the file.

```python
file = open("data.txt", "r")

content = file.read()

print(content)

file.close()
```

Why close files?

- Releases operating-system resources.
- Helps ensure buffered data is flushed.
- Prevents unnecessary open file handles.

You can check whether a file is closed:

```python
file = open("data.txt", "r")

print(file.closed)

file.close()

print(file.closed)
```

Output:

```text
False
True
```

**Problem with manually closing files:**

If an error occurs before `close()` executes, the file might remain open longer than expected.

Python provides a better solution: the `with` statement.

---

## 10. Using `with open()` – Recommended Approach

The `with` statement automatically closes the file when the block finishes, including when an exception occurs.

### Syntax

```python
with open("filename.txt", "mode") as file:
    # File operations
```

Example:

```python
with open("students.txt", "r") as file:
    content = file.read()
    print(content)
```

There is no need to call `file.close()` manually.

### Writing using `with`

```python
with open("students.txt", "w") as file:
    file.write("Arun\n")
    file.write("Kumar\n")
    file.write("Sivan\n")
```

### Checking whether the file is closed

```python
with open("students.txt", "r") as file:
    print(file.closed)

print(file.closed)
```

Output:

```text
False
True
```

**Best practice:** Prefer `with open()` for normal file handling.

---

## 11. Reading Large Files Efficiently

Suppose a log file contains millions of lines.

Using `read()` loads the entire remaining file into memory.

A more efficient approach is to process one line at a time.

Example:

```python
with open("server.log", "r") as file:

    for line in file:
        if "ERROR" in line:
            print(line.strip())
```

This processes each line individually rather than loading the entire file into a list or string.

**Real-world application:** Finding errors in application logs.

---

## 12. File Paths and Working Directories

A file can be opened using:

1. Relative path.
2. Absolute path.

### Relative path

```python
with open("data.txt", "r") as file:
    print(file.read())
```

Python looks for the file relative to the current working directory.

### Absolute path

Windows example:

```python
with open("C:/Users/Developer/Documents/data.txt", "r") as file:
    print(file.read())
```

Linux example:

```python
with open("/home/developer/data.txt", "r") as file:
    print(file.read())
```

### Checking the current working directory

```python
import os

print(os.getcwd())
```

This displays the directory from which relative paths are resolved.

### Working with paths using `pathlib`

`pathlib` is a modern standard-library module for handling filesystem paths.

```python
from pathlib import Path

file_path = Path("data") / "students.txt"

print(file_path)
```

Output (typical on Windows):

```text
data\students.txt
```

The exact separator depends on the operating system.

---

## 13. Handling File Errors

File operations can fail for several reasons.

Common exceptions:

| Exception | Meaning |
|---|---|
| `FileNotFoundError` | File does not exist |
| `PermissionError` | Insufficient access permission |
| `IsADirectoryError` | A directory was used where a file was expected |
| `FileExistsError` | File already exists when using `x` mode |
| `UnicodeDecodeError` | File bytes cannot be decoded using the selected encoding |

### Example: Handling a missing file

```python
try:
    with open("unknown.txt", "r") as file:
        content = file.read()
        print(content)

except FileNotFoundError:
    print("File not found.")
```

Output:

```text
File not found.
```

### Handling multiple exceptions

```python
try:
    with open("data.txt", "r", encoding="utf-8") as file:
        print(file.read())

except FileNotFoundError:
    print("The requested file does not exist.")

except PermissionError:
    print("You do not have permission to read this file.")

except UnicodeDecodeError:
    print("Unable to decode the file.")
```

**Best practice:** Catch exceptions you can handle meaningfully. Avoid using a broad `except:` that hides unexpected programming errors.

---

## 14. Understanding File Encoding

Text files store bytes. Python must decode those bytes into characters when reading and encode characters into bytes when writing.

Use the `encoding` parameter to specify the expected encoding.

Example:

```python
with open("data.txt", "r", encoding="utf-8") as file:
    content = file.read()
    print(content)
```

Writing:

```python
with open("data.txt", "w", encoding="utf-8") as file:
    file.write("வணக்கம் Python")
```

UTF-8 is a widely used encoding that supports English, Tamil, and many other languages.

**Important:** Specifying UTF-8 is good practice, but it does not automatically convert incorrectly encoded existing files into UTF-8.

---

## 15. Understanding the File Cursor

A file cursor represents the current position from which the next read or write operation takes place.

### Example

```python
with open("data.txt", "r") as file:

    print(file.read(5))
    print(file.tell())

    file.seek(0)

    print(file.read(5))
```

Assume `data.txt` contains:

```text
Python Programming
```

Output:

```text
Pytho
5
Pytho
```

Explanation:

- `read(5)` reads five characters.
- `tell()` returns the current stream position.
- `seek(0)` moves the cursor back to the beginning.
- The next `read(5)` reads the same first five characters.

For text files, `tell()` returns a position suitable for restoring with `seek()`. It should not always be interpreted as a simple character count, especially with multibyte encodings.

---

## 16. Reading and Writing in Binary Mode

Text mode works with strings.

Binary mode works with bytes.

Common binary file examples:
- Images.
- PDFs.
- Audio files.
- Video files.
- Other non-text data.

### Reading binary files

```python
with open("image.jpg", "rb") as file:
    content = file.read()

print(type(content))
```

Output:

```text
<class 'bytes'>
```

### Writing binary files

```python
data = b"Hello Python"

with open("sample.bin", "wb") as file:
    file.write(data)
```

Common binary modes:

| Mode | Meaning |
|---|---|
| `rb` | Read binary |
| `wb` | Write binary |
| `ab` | Append binary |

**Important:** Binary mode does not perform text encoding or decoding. The data is handled as bytes.

---

## 17. Practical Example: Employee Record Management

Let's build a small program that stores employee records in a text file.

```python
def add_employee(name, department):
    with open("employees.txt", "a", encoding="utf-8") as file:
        file.write(f"{name},{department}\n")


def display_employees():
    try:
        with open("employees.txt", "r", encoding="utf-8") as file:
            for line in file:
                print(line.strip())

    except FileNotFoundError:
        print("No employee records found.")


add_employee("Arun", "Python")
add_employee("Kumar", "AI")
add_employee("Sivan", "Data Engineering")

display_employees()
```

Possible output:

```text
Arun,Python
Kumar,AI
Sivan,Data Engineering
```

This example demonstrates:
- Function creation.
- File opening.
- Appending records.
- Reading records.
- Exception handling.
- Context managers.

**Production note:** This simple comma-separated format is only for learning. If fields can contain commas, quotes, or newlines, use Python's `csv` module instead of manually constructing records.

---

## 18. FDE Connection – Why File Handling Matters

Forward-Deployed Engineers frequently work with customer data, logs, configurations, and integrations.

File handling is a foundational skill for these tasks.

### Scenario 1: Processing application logs

A customer provides a large application log file.

You need to find all error messages.

```python
with open("application.log", "r", encoding="utf-8") as file:

    for line in file:
        if "ERROR" in line:
            print(line.strip())
```

### Scenario 2: Reading configuration data

An application stores configuration information in a text file.

```python
with open("config.txt", "r", encoding="utf-8") as file:
    settings = file.read()

print(settings)
```

For structured configuration, JSON, TOML, or other suitable formats are preferable.

### Scenario 3: Saving AI-generated output

An AI application generates a response that needs to be saved.

```python
ai_response = "The customer request has been processed successfully."

with open("ai_output.txt", "w", encoding="utf-8") as file:
    file.write(ai_response)
```

### Scenario 4: Processing customer-provided files

An FDE may receive:
- Customer CSV exports.
- JSON files.
- Application logs.
- Text documents.
- Configuration files.

Python file handling provides the foundation for reading and processing these inputs.

---

## 19. Common Mistakes

| Mistake | Why it is a problem |
|---|---|
| Using `r` for a missing file | Raises `FileNotFoundError` |
| Using `w` accidentally | Deletes existing content |
| Forgetting `\n` | Multiple records may appear on one line |
| Not closing files | Resources may remain open |
| Using `read()` for huge files | Can consume excessive memory |
| Assuming `write()` accepts integers | It expects a string in text mode |
| Ignoring file encoding | May cause decoding errors or incorrect text |
| Using `readlines()` unnecessarily | Loads all remaining lines into memory |
| Catching every exception | Can hide programming mistakes |

---

## 20. Practice Exercises

### Beginner Level

**Exercise 1:** Create a file named `welcome.txt` and write:

```text
Welcome to Python File Handling
```

**Exercise 2:** Read the contents of `welcome.txt` and display them.

**Exercise 3:** Create a file containing three student names, with each name on a separate line.

### Intermediate Level

**Exercise 4:** Append a fourth student name without deleting the existing names.

**Exercise 5:** Read a file line by line and display only lines containing the word `Python`.

**Exercise 6:** Write a program that handles `FileNotFoundError` when opening a missing file.

### Advanced Level

**Exercise 7:** Create an employee file containing employee names and departments. Write separate functions to add and display employees.

**Exercise 8:** Read a large log file line by line and count how many lines contain `ERROR`.

**Exercise 9:** Read a text file, count the total number of lines, and print the count.

**Exercise 10 – FDE Scenario:**

A customer provides a text file containing:

```text
Arun,Python
Kumar,AI
Sivan,Data Engineering
```

Write a program that:
1. Reads the file.
2. Splits each line into employee name and department.
3. Stores each employee as a dictionary.
4. Prints the resulting list of dictionaries.

Expected output:

```python
[
    {'name': 'Arun', 'department': 'Python'},
    {'name': 'Kumar', 'department': 'AI'},
    {'name': 'Sivan', 'department': 'Data Engineering'}
]
```

---

## 21. Quick Revision

| Concept | Purpose |
|---|---|
| `open()` | Opens a file |
| `read()` | Reads file contents |
| `readline()` | Reads one line |
| `readlines()` | Reads remaining lines into a list |
| `write()` | Writes a string |
| `writelines()` | Writes multiple strings |
| `close()` | Closes a file |
| `with open()` | Automatically closes a file |
| `r` | Read mode |
| `w` | Write mode |
| `a` | Append mode |
| `x` | Exclusive file creation |
| `tell()` | Gets current stream position |
| `seek()` | Changes stream position |
| `rb` | Reads binary data |
| `wb` | Writes binary data |
| `encoding="utf-8"` | Specifies text encoding |

---

## 22. Self-Assessment

Before moving to the next topic, make sure you can answer these questions:

1. What is the purpose of the `open()` function?
2. What is the difference between `w` and `a`?
3. What happens when you open a missing file in `r` mode?
4. What is the difference between `read()`, `readline()`, and `readlines()`?
5. Why should we use `with open()`?
6. Does `write()` automatically add a newline?
7. What does `encoding="utf-8"` mean?
8. What is the difference between text mode and binary mode?
9. What are `seek()` and `tell()` used for?
10. Why is line-by-line reading useful for large files?

---

## 23. Learning Outcome

After completing this chapter, you should be able to:

- Open files in different modes.
- Read complete files and individual lines.
- Write and append data.
- Use context managers safely.
- Handle common file-related exceptions.
- Work with file paths and encodings.
- Process large files efficiently.
- Build simple file-based data-processing applications.


