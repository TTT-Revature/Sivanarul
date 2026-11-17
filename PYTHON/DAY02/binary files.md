
# 45. File Modes and Text/Binary Files in Python

**Suggested filename:** `45_file_modes_and_text_binary_files.md`

## 1. Introduction

In the previous chapter, we learned how to open, read, write, and append files using Python.

Now we will understand file modes in more detail.

Python files are commonly handled in two categories:

1. **Text files** – Store human-readable characters.
2. **Binary files** – Store raw bytes.

Examples:

| Text files | Binary files |
|---|---|
| `.txt` | `.jpg` |
| `.csv` | `.png` |
| `.json` | `.pdf` |
| `.xml` | `.mp3` |
| `.log` | `.mp4` |

The file extension is only a naming convention. The actual contents and the way they are encoded determine how the data should be handled.

---

## 2. Understanding File Modes

A file mode tells Python how to interact with a file.

The main modes are:

| Mode | Description |
|---|---|
| `r` | Read |
| `w` | Write and overwrite |
| `a` | Append |
| `x` | Create exclusively |
| `r+` | Read and write |
| `w+` | Write and read, overwriting existing content |
| `a+` | Append and read |

### 2.1 Read Mode – `r`

Used to read an existing file.

```python
with open("data.txt", "r") as file:
    content = file.read()
    print(content)
```

Important points:

- File must already exist.
- Raises `FileNotFoundError` if missing.
- Does not modify the file.

### 2.2 Write Mode – `w`

Used to create or overwrite a file.

```python
with open("data.txt", "w") as file:
    file.write("Hello Python")
```

Important points:

- Creates the file if it does not exist.
- Truncates an existing file to zero length when opened.
- Existing content is permanently replaced unless separately backed up.

Example:

Suppose `data.txt` initially contains:

```text
Welcome
Python Developer
```

After executing:

```python
with open("data.txt", "w") as file:
    file.write("New Content")
```

New file content:

```text
New Content
```

### 2.3 Append Mode – `a`

Used to add content at the end of a file.

```python
with open("data.txt", "a") as file:
    file.write("\nNew Employee")
```

Important points:

- Creates the file if it does not exist.
- Preserves existing content.
- Writes at the end of the file.

### 2.4 Exclusive Creation Mode – `x`

Creates a new file only if it does not already exist.

```python
with open("new_file.txt", "x") as file:
    file.write("First record")
```

If the file already exists, Python raises:

```text
FileExistsError
```

This is useful when accidentally overwriting an existing file must be avoided.

---

## 3. Understanding Combined File Modes

Python also supports modes that combine reading and writing.

### 3.1 `r+` – Read and Write

```python
with open("data.txt", "r+") as file:
    content = file.read()
    print(content)

    file.write("\nNew Line")
```

Characteristics:

- File must exist.
- Allows reading and writing.
- Does not automatically erase existing content.
- Initially positions the cursor at the beginning.
- Writing starts at the current cursor position.

**Important:** `r+` does not automatically append. If you read the entire file first, the cursor is at the end, so the next write happens there.

### 3.2 `w+` – Write and Read

```python
with open("data.txt", "w+") as file:
    file.write("Python Developer")

    file.seek(0)

    content = file.read()
    print(content)
```

Output:

```text
Python Developer
```

Characteristics:

- Creates the file if missing.
- Truncates an existing file.
- Allows both reading and writing.
- Cursor initially starts at the beginning.

### 3.3 `a+` – Append and Read

```python
with open("data.txt", "a+") as file:
    file.write("\nNew Employee")

    file.seek(0)

    content = file.read()
    print(content)
```

Characteristics:

- Creates the file if missing.
- Preserves existing content.
- Allows reading and writing.
- Writes are directed to the end of the file.
- Reading starts from the current cursor position, so `seek(0)` is useful when reading the complete file after writing.

---

## 4. Understanding Text Mode

Text mode is the default mode in Python.

Example:

```python
with open("message.txt", "r") as file:
    content = file.read()

print(type(content))
```

Output:

```text
<class 'str'>
```

Why?

Because Python decodes the file's bytes into text characters.

### Writing text

```python
with open("message.txt", "w", encoding="utf-8") as file:
    file.write("Welcome to Python")
```

Here:

- `encoding="utf-8"` specifies how characters are encoded into bytes.
- `write()` accepts a string.
- Python handles the encoding.

### Important text-mode characteristics

1. Reads data as `str`.
2. Writes data as `str`.
3. Uses an encoding for conversion between bytes and text.
4. Performs newline translation depending on the platform and `newline` setting.

---

## 5. Understanding Binary Mode

Binary mode works with bytes instead of strings.

It is commonly used for:

- Images.
- Videos.
- Audio.
- PDFs.
- Executable files.
- Other non-text data.

### Reading binary data

```python
with open("image.jpg", "rb") as file:
    content = file.read()

print(type(content))
```

Output:

```text
<class 'bytes'>
```

### Writing binary data

```python
data = b"Hello Python"

with open("sample.bin", "wb") as file:
    file.write(data)
```

The `b` prefix creates a bytes literal.

### Important binary-mode characteristics

1. Reads data as `bytes`.
2. Writes data as bytes-like objects.
3. Does not perform text encoding or decoding.
4. Does not perform text newline translation.

---

## 6. Difference Between Text and Binary Modes

| Feature | Text Mode | Binary Mode |
|---|---|---|
| Main data type | `str` | `bytes` |
| Encoding | Uses encoding | No text encoding |
| Decoding | Converts bytes to text | No automatic decoding |
| Newline translation | May occur | Does not occur |
| Common modes | `r`, `w`, `a` | `rb`, `wb`, `ab` |
| Typical usage | TXT, CSV, JSON | Images, PDFs, audio |

### Practical comparison

Text mode:

```python
with open("data.txt", "w", encoding="utf-8") as file:
    file.write("Python")
```

Binary mode:

```python
with open("data.bin", "wb") as file:
    file.write(b"Python")
```

The difference is the type of data being written.

This will raise a `TypeError`:

```python
with open("data.bin", "wb") as file:
    file.write("Python")
```

Why?

Binary mode expects bytes, not a string.

Similarly, this is invalid:

```python
with open("data.txt", "w") as file:
    file.write(b"Python")
```

Text mode expects a string, not bytes.

---

## 7. Converting Between Strings and Bytes

Sometimes we need to convert text into bytes or bytes into text.

Python provides:

- `encode()` – Converts a string into bytes.
- `decode()` – Converts bytes into a string.

### String to bytes

```python
message = "Hello Python"

binary_data = message.encode("utf-8")

print(binary_data)
print(type(binary_data))
```

Output:

```text
b'Hello Python'
<class 'bytes'>
```

### Bytes to string

```python
binary_data = b"Hello Python"

message = binary_data.decode("utf-8")

print(message)
print(type(message))
```

Output:

```text
Hello Python
<class 'str'>
```

### Tamil text example

```python
message = "வணக்கம்"

binary_data = message.encode("utf-8")

print(binary_data)

decoded_message = binary_data.decode("utf-8")

print(decoded_message)
```

The encoded output is a sequence of UTF-8 bytes, and decoding with the matching encoding reconstructs the original text.

**Important:** Decoding bytes with the wrong encoding can cause `UnicodeDecodeError` or produce incorrect text.

---

## 8. Understanding Newline Handling

Different operating systems have historically used different newline representations.

| Operating system | Common newline representation |
|---|---|
| Windows | `\r\n` |
| Linux | `\n` |
| macOS (modern) | `\n` |

Python text mode normally translates platform newline representations.

### Example

```python
with open("data.txt", "w", encoding="utf-8") as file:
    file.write("First Line\n")
    file.write("Second Line\n")
```

When reading in normal text mode:

```python
with open("data.txt", "r", encoding="utf-8") as file:
    content = file.read()

print(content)
```

Python handles standard newline translation.

### The `newline` parameter

You can control newline handling using the `newline` parameter of `open()`.

For example:

```python
with open("data.txt", "r", encoding="utf-8", newline="") as file:
    content = file.read()
```

With `newline=""`, universal newline recognition is enabled, but line endings are returned untranslated.

This option is especially useful for working with CSV files.

---

## 9. File Modes with `seek()` and `tell()`

File operations use a cursor to track the current position.

### `tell()`

Returns the current stream position.

### `seek()`

Changes the stream position.

Example:

```python
with open("data.txt", "r", encoding="utf-8") as file:

    print(file.read(3))

    print(file.tell())

    file.seek(0)

    print(file.read(3))
```

Assume the file contains:

```text
Python Programming
```

Output:

```text
Pyt
3
Pyt
```

### Important points

- `seek(0)` moves to the beginning.
- `tell()` reports the current stream position.
- In text mode, positions are not necessarily simple character indexes.
- In binary mode, positions are byte offsets.

---

## 10. Working with Image Files in Binary Mode

Images should generally be copied or processed as binary data.

Example:

```python
with open("original.jpg", "rb") as source:
    image_data = source.read()

with open("copy.jpg", "wb") as destination:
    destination.write(image_data)
```

This creates a copy of the image.

Why binary mode?

An image contains binary data. Reading it as text may fail during decoding or alter how the data is interpreted.

**Real-world application:** An FDE might receive customer-uploaded images and transfer them to a storage system without changing their contents.

---

## 11. Handling File Modes Safely

Opening files in the wrong mode can cause data loss.

Consider:

```python
with open("customer_data.txt", "w") as file:
    file.write("Updated Customer")
```

If `customer_data.txt` already contains important information, its previous contents are erased.

A safer approach when creating a new file without overwriting an existing one:

```python
try:
    with open("customer_data.txt", "x", encoding="utf-8") as file:
        file.write("New Customer")

except FileExistsError:
    print("File already exists. Existing data was preserved.")
```

Output if the file exists:

```text
File already exists. Existing data was preserved.
```

Always choose the file mode based on the operation you actually need.

---

## 12. Practical Example – File Processing Application

Let's create a small program that reads customer records and appends a new record.

### Initial file: `customers.txt`

```text
101,Arun,Chennai
102,Kumar,Bangalore
```

### Python program

```python
def read_customers():
    with open("customers.txt", "r", encoding="utf-8") as file:
        for line in file:
            print(line.strip())


def add_customer(customer_id, name, city):
    with open("customers.txt", "a", encoding="utf-8") as file:
        file.write(f"{customer_id},{name},{city}\n")


add_customer(103, "Sivan", "Coimbatore")

read_customers()
```

Output:

```text
101,Arun,Chennai
102,Kumar,Bangalore
103,Sivan,Coimbatore
```

This demonstrates:

- Reading using `r`.
- Appending using `a`.
- Text-mode file operations.
- Functions.
- String formatting.
- Context managers.

**Production note:** This is a learning example. For real CSV data, use Python's `csv` module to handle commas, quotes, and special characters correctly.

---

## 13. FDE Connection – Choosing the Correct File Mode

An FDE often integrates systems that exchange files.

Consider these scenarios:

| Scenario | Suitable mode |
|---|---|
| Read customer configuration | `r` |
| Create a new report | `w` |
| Add new application log entries | `a` |
| Create a report only if it does not exist | `x` |
| Read and update an existing text file | `r+` |
| Read an uploaded image | `rb` |
| Save a generated PDF or image | `wb` |
| Append binary data | `ab` |

### Example: Processing an uploaded customer file

```python
def process_customer_file(file_path):

    try:
        with open(file_path, "r", encoding="utf-8") as file:

            for line in file:
                customer_data = line.strip()
                print(customer_data)

    except FileNotFoundError:
        print("Customer file not found.")

    except UnicodeDecodeError:
        print("The file could not be decoded as UTF-8.")
```

In a production application, you would also validate the file format, size, content, and access permissions.

---

## 14. Common Mistakes

| Mistake | Explanation |
|---|---|
| Using `w` instead of `a` | Existing content is erased |
| Using `r` for a missing file | Raises `FileNotFoundError` |
| Writing strings in `wb` mode | Binary mode expects bytes |
| Writing bytes in `w` mode | Text mode expects strings |
| Assuming `r+` means append | It starts at the beginning |
| Forgetting `seek(0)` in `a+` | Reading may start from the end |
| Using text mode for image copying | Can cause decoding problems |
| Assuming `.jpg` always means valid image data | File extensions do not guarantee content format |
| Ignoring encoding | May cause decoding errors |

---

## 15. Practice Exercises

### Beginner Level

**Exercise 1:** Create a file using `w` mode and write three lines.

**Exercise 2:** Open the same file using `r` mode and display its contents.

**Exercise 3:** Add a fourth line using `a` mode.

### Intermediate Level

**Exercise 4:** Write a program using `x` mode. Handle `FileExistsError` if the file already exists.

**Exercise 5:** Open a file using `r+`, read its contents, move the cursor to the beginning, and write a replacement string. Observe what happens to the remaining old content.

**Exercise 6:** Open a file using `a+`, append a new record, move the cursor to the beginning, and read the complete file.

### Advanced Level

**Exercise 7:** Create a program that reads a text file and counts the number of lines containing `ERROR`.

**Exercise 8:** Copy an image using `rb` and `wb` modes.

**Exercise 9:** Convert a string into UTF-8 bytes, save it in binary mode, read it back, and decode it.

**Exercise 10 – FDE Scenario:**

A customer provides two files:

- `customer.txt`
- `customer_image.jpg`

Write a program that:
1. Reads the text file using text mode.
2. Reads the image using binary mode.
3. Creates a backup of both files.
4. Handles missing-file errors.
5. Does not modify the original files.

---

## 16. Quick Revision

| Concept | Key Point |
|---|---|
| `r` | Read existing file |
| `w` | Create or overwrite |
| `a` | Append at the end |
| `x` | Create only if absent |
| `r+` | Read and write existing file |
| `w+` | Read and write after truncating |
| `a+` | Read and append |
| `rb` | Read bytes |
| `wb` | Write bytes |
| `ab` | Append bytes |
| Text mode | Works with `str` |
| Binary mode | Works with `bytes` |
| `encode()` | String to bytes |
| `decode()` | Bytes to string |
| `seek()` | Move file cursor |
| `tell()` | Get file position |
| `encoding` | Specifies text encoding |

---

## 17. Self-Assessment

1. What is the difference between `r`, `w`, and `a`?
2. What happens when an existing file is opened in `w` mode?
3. What is the difference between `r+` and `a+`?
4. Why do we use binary mode for images?
5. What is the difference between `str` and `bytes`?
6. What does `encode()` do?
7. What does `decode()` do?
8. Why is UTF-8 commonly used?
9. What is the purpose of `seek()`?
10. Which mode should you use to create a new file without overwriting an existing one?

---

## 18. Learning Outcome

After completing this chapter, you should be able to:

- Select appropriate file modes.
- Understand read, write, append, and exclusive creation.
- Work with combined reading and writing modes.
- Explain text files versus binary files.
- Convert strings into bytes and bytes into strings.
- Handle encoding and newline behavior.
- Read and write binary files.
- Choose safe file operations for real-world applications.


