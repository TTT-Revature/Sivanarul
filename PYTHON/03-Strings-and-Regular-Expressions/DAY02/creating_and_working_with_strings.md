
# Python Strings – Creating and Working with Strings

**Suggested filename:** `24_creating_and_working_with_strings.md`

## 1. Introduction

A string is a built-in Python data type used to represent text.

In Python, strings are represented using the `str` class.

Strings can contain:

- Alphabets
- Numbers
- Special characters
- Spaces
- Symbols
- Unicode characters

Examples:

```python
name = "Sivanarul"
city = "Chennai"
message = "Welcome to Python!"
```

In real-world applications, strings are used to process:

- Usernames and passwords
- Email addresses
- API responses
- JSON data
- File contents
- Database records
- AI prompts and responses
- Application logs

---

## 2. Creating Strings in Python

Python provides different ways to create strings.

### 2.1 Single Quotes

We can create a string using single quotation marks.

```python
name = 'Sivanarul'

print(name)
print(type(name))
```

**Output:**

```text
Sivanarul
<class 'str'>
```

### 2.2 Double Quotes

We can also use double quotation marks.

```python
name = "Sivanarul"

print(name)
print(type(name))
```

**Output:**

```text
Sivanarul
<class 'str'>
```

Both single and double quotes create the same Python string type.

### 2.3 Triple Single Quotes

Triple single quotes allow us to create multiline strings.

```python
message = '''Welcome to Python.
Python is easy to learn.
Python is widely used in AI engineering.'''

print(message)
```

**Output:**

```text
Welcome to Python.
Python is easy to learn.
Python is widely used in AI engineering.
```

### 2.4 Triple Double Quotes

We can also use triple double quotes.

```python
message = """Python is a programming language.

It is widely used in:
- Web development
- Data science
- Artificial intelligence
"""

print(message)
```

**Output:**

```text
Python is a programming language.

It is widely used in:
- Web development
- Data science
- Artificial intelligence
```

### Important Note

Single quotes, double quotes, and triple quotes all create strings.

Triple-quoted strings are useful when we need multiline text.

---

## 3. Choosing Between Single and Double Quotes

Both approaches are valid.

However, we can choose the quotation style based on the text.

### Example 1: Single Quotes Inside Double Quotes

```python
message = "Python's programming features are powerful."

print(message)
```

**Output:**

```text
Python's programming features are powerful.
```

### Example 2: Double Quotes Inside Single Quotes

```python
message = 'He said "Python is interesting".'

print(message)
```

**Output:**

```text
He said "Python is interesting".
```

This avoids unnecessary escaping.

### Example 3: Escaping Quotes

If we need to use the same quotation mark inside a string, we can escape it using a backslash.

```python
message = "Python's features are \"powerful\"."

print(message)
```

**Output:**

```text
Python's features are "powerful".
```

---

## 4. Understanding String Indexing

Every character in a Python string has an index position.

Python supports two types of indexing:

1. Positive indexing
2. Negative indexing

Consider the following string:

```python
language = "PYTHON"
```

### Positive Indexing

Positive indexing starts from `0` and moves from left to right.

| Character | P | Y | T | H | O | N |
|---|---|---|---|---|---|---|
| Index | 0 | 1 | 2 | 3 | 4 | 5 |

Example:

```python
language = "PYTHON"

print(language[0])
print(language[1])
print(language[2])
print(language[3])
```

**Output:**

```text
P
Y
T
H
```

### Negative Indexing

Negative indexing starts from `-1` and moves from right to left.

| Character | P | Y | T | H | O | N |
|---|---|---|---|---|---|---|
| Index | -6 | -5 | -4 | -3 | -2 | -1 |

Example:

```python
language = "PYTHON"

print(language[-1])
print(language[-2])
print(language[-3])
```

**Output:**

```text
N
O
H
```

### Why Is Negative Indexing Useful?

Negative indexing allows us to access characters from the end without calculating the string length manually.

Example:

```python
filename = "report.pdf"

print(filename[-1])
print(filename[-3:])
```

**Output:**

```text
f
pdf
```

---

## 5. Accessing Characters Using Indexes

We can access individual characters using square brackets.

### Example

```python
name = "Sivanarul"

first_character = name[0]
last_character = name[-1]

print("First character:", first_character)
print("Last character:", last_character)
```

**Output:**

```text
First character: S
Last character: l
```

### Accessing an Invalid Index

```python
name = "Python"

print(name[10])
```

**Output:**

```text
IndexError: string index out of range
```

The string contains only six characters, so index `10` does not exist.

---

## 6. Understanding String Slicing

Slicing allows us to extract a portion of a string.

### Syntax

```python
string[start:stop:step]
```

| Parameter | Meaning |
|---|---|
| `start` | Starting index, included |
| `stop` | Ending index, excluded |
| `step` | Number of positions to move |

### Example 1: Basic Slicing

```python
language = "PYTHON"

print(language[0:3])
```

**Output:**

```text
PYT
```

Explanation:

- Starts at index `0`.
- Stops before index `3`.
- Extracts characters at indexes `0`, `1`, and `2`.

### Example 2: Omitting the Starting Index

```python
language = "PYTHON"

print(language[:3])
```

**Output:**

```text
PYT
```

If the starting index is omitted, Python starts from the beginning.

### Example 3: Omitting the Ending Index

```python
language = "PYTHON"

print(language[2:])
```

**Output:**

```text
THON
```

If the ending index is omitted, Python continues until the end.

### Example 4: Negative Slicing

```python
language = "PYTHON"

print(language[-3:])
```

**Output:**

```text
HON
```

### Example 5: Using Step

```python
language = "PYTHON"

print(language[::2])
```

**Output:**

```text
PTO
```

Here, Python selects every second character.

### Example 6: Reversing a String

```python
language = "PYTHON"

print(language[::-1])
```

**Output:**

```text
NOHTYP
```

A step of `-1` moves through the string in reverse order.

---

## 7. String Concatenation

Concatenation means joining two or more strings.

Python uses the `+` operator for string concatenation.

### Example 1: Joining Two Strings

```python
first_name = "Sivanarul"
last_name = "Anbu"

full_name = first_name + " " + last_name

print(full_name)
```

**Output:**

```text
Sivanarul Anbu
```

### Example 2: Concatenating Multiple Strings

```python
first = "Python"
second = "is"
third = "powerful"

message = first + " " + second + " " + third

print(message)
```

**Output:**

```text
Python is powerful
```

### Important Note

The `+` operator concatenates strings.

However, we cannot directly concatenate a string and an integer.

Incorrect:

```python
age = 27

message = "My age is " + age
```

This raises a `TypeError`.

Correct:

```python
age = 27

message = "My age is " + str(age)

print(message)
```

**Output:**

```text
My age is 27
```

For readable dynamic strings, f-Strings are generally preferred.

---

## 8. String Repetition

Python allows us to repeat a string using the `*` operator.

### Example 1

```python
message = "Python "

print(message * 3)
```

**Output:**

```text
Python Python Python
```

### Example 2: Creating Separators

```python
print("=" * 30)
print("EMPLOYEE REPORT")
print("=" * 30)
```

**Output:**

```text
==============================
EMPLOYEE REPORT
==============================
```

### Important Note

String repetition requires an integer multiplier.

```python
print("Hello" * 3)
```

This produces:

```text
HelloHelloHello
```

---

## 9. Finding the Length of a String

Python provides the built-in `len()` function to find the number of characters in a string.

### Syntax

```python
len(string)
```

### Example

```python
message = "Python Developer"

print(len(message))
```

**Output:**

```text
16
```

Spaces are also counted as characters.

### Example: Username Length

```python
username = "sivanarul"

length = len(username)

print(f"Username: {username}")
print(f"Length: {length}")
```

**Output:**

```text
Username: sivanarul
Length: 9
```

### Important Note About Unicode

Python string length counts Unicode code points, not necessarily the number of visible characters.

For example, some emojis and combined characters may contain multiple code points even though they appear as one visible character.

---

## 10. Checking Whether a Substring Exists

We can use the membership operator `in` to check whether a string contains another string.

### Example

```python
message = "Python is powerful"

print("Python" in message)
print("Java" in message)
```

**Output:**

```text
True
False
```

### Using `not in`

```python
message = "Python is powerful"

print("Java" not in message)
```

**Output:**

```text
True
```

### Important Note

String membership checks are case-sensitive.

```python
message = "Python Developer"

print("python" in message)
print("Python" in message)
```

**Output:**

```text
False
True
```

If we need case-insensitive matching, we can normalize both strings using `.lower()` or `.casefold()`.

---

## 11. Strings Are Immutable

One of the most important characteristics of Python strings is immutability.

**Immutable means that the original string cannot be modified after it has been created.**

### Example

```python
name = "Python"

name[0] = "J"
```

**Output:**

```text
TypeError: 'str' object does not support item assignment
```

We cannot directly replace an individual character.

### How Can We Create a Modified String?

We can create a new string instead.

```python
name = "Python"

new_name = "J" + name[1:]

print(name)
print(new_name)
```

**Output:**

```text
Python
Jython
```

The original string remains unchanged.

The variable `new_name` refers to a newly created string.

### Important Understanding

String immutability helps Python manage string objects consistently and makes strings safe to share without unexpected in-place modifications.

---

## 12. Iterating Through a String

A string is an iterable object.

This means we can use loops to access its characters one by one.

### Example 1: Using a `for` Loop

```python
language = "PYTHON"

for character in language:
    print(character)
```

**Output:**

```text
P
Y
T
H
O
N
```

### Example 2: Using Index Positions

```python
language = "PYTHON"

for index in range(len(language)):
    print(index, language[index])
```

**Output:**

```text
0 P
1 Y
2 T
3 H
4 O
5 N
```

### Example 3: Counting Characters

```python
message = "Hello Python"

count = 0

for character in message:
    count += 1

print(f"Total characters: {count}")
```

**Output:**

```text
Total characters: 12
```

---

## 13. Working with Special Characters and Escape Sequences

Strings can contain special characters.

Python uses escape sequences to represent certain characters.

An escape sequence begins with a backslash (`\`).

### Common Escape Sequences

| Escape Sequence | Meaning |
|---|---|
| `\n` | New line |
| `\t` | Horizontal tab |
| `\\` | Backslash |
| `\'` | Single quotation mark |
| `\"` | Double quotation mark |
| `\r` | Carriage return |
| `\b` | Backspace |
| `\0` | Null character |

### Example 1: New Line

```python
message = "Hello\nPython"

print(message)
```

**Output:**

```text
Hello
Python
```

### Example 2: Tab

```python
message = "Name:\tSivanarul"

print(message)
```

**Output:**

```text
Name:   Sivanarul
```

The exact visual spacing depends on the terminal's tab stops.

### Example 3: Backslash

```python
path = "C:\\Users\\Python"

print(path)
```

**Output:**

```text
C:\Users\Python
```

---

## 14. Raw Strings

A raw string treats backslashes as ordinary characters for most escape-sequence processing.

We create a raw string using the `r` or `R` prefix.

### Example

```python
path = r"C:\Users\Python\Documents"

print(path)
```

**Output:**

```text
C:\Users\Python\Documents
```

Raw strings are particularly useful when working with:

- Windows file paths
- Regular expressions
- Text patterns

### Important Note

A raw string cannot end with an odd number of consecutive backslashes because the final backslash would escape the closing quotation mark.

---

## 15. Combining Strings with f-Strings

We can combine the string concepts learned so far with f-Strings.

### Example: User Profile

```python
name = "Sivanarul"
city = "Chennai"
profession = "Python Developer"

profile = f"""
USER PROFILE
-------------------------
Name       : {name}
City       : {city}
Profession : {profession}
-------------------------
"""

print(profile)
```

**Output:**

```text
USER PROFILE
-------------------------
Name       : Sivanarul
City       : Chennai
Profession : Python Developer
-------------------------
```

This approach is useful when generating readable reports and messages.

---

## 16. Practical Example: Email Address Processing

Let's create a simple program that receives an email address and extracts some information.

```python
email = "sivanarul@example.com"

username = email[:email.index("@")]
domain = email[email.index("@") + 1:]

print(f"Email: {email}")
print(f"Username: {username}")
print(f"Domain: {domain}")
```

**Output:**

```text
Email: sivanarul@example.com
Username: sivanarul
Domain: example.com
```

This demonstrates:

- String indexing
- String slicing
- Finding a substring
- f-String formatting

**Important:** This is only a basic string-processing demonstration. Real email validation requires more comprehensive validation rules.

---

## 17. Practical Example: Processing AI Model Responses

AI applications frequently receive textual responses that need to be inspected or processed.

```python
response = "  The AI model generated a successful response.  "

clean_response = response.strip()

print(f"Original length: {len(response)}")
print(f"Cleaned response: {clean_response}")
print(f"Cleaned length: {len(clean_response)}")
```

**Output:**

```text
Original length: 55
Cleaned response: The AI model generated a successful response.
Cleaned length: 49
```

This example introduces a common real-world requirement: removing unnecessary whitespace from text.

We will study string methods such as `strip()`, `replace()`, `split()`, and `join()` in a separate topic.

---

## 18. Common Mistakes

| Mistake | Explanation |
|---|---|
| Using mismatched quotation marks | Can cause a `SyntaxError` |
| Accessing an invalid index | Raises `IndexError` |
| Confusing indexing and slicing | Indexing retrieves one character; slicing extracts a portion |
| Assuming the ending slice index is included | The stop position is excluded |
| Directly modifying a string character | Strings are immutable |
| Concatenating strings and integers directly | Can raise `TypeError` |
| Forgetting that spaces count toward length | `len()` includes spaces |
| Ignoring case sensitivity | `"Python"` and `"python"` are different strings |
| Misunderstanding escape sequences | Backslashes can introduce special characters |

---

## 19. Practice Exercises

### Beginner Level

**Exercise 1: Create a String**

Create strings using:

- Single quotes
- Double quotes
- Triple single quotes
- Triple double quotes

Display each string.

**Exercise 2: Character Access**

Given:

```python
language = "PYTHON"
```

Display:

- First character
- Last character
- Third character
- Second-last character

**Exercise 3: String Slicing**

Given:

```python
message = "Forward Deployed Engineer"
```

Extract:

- `Forward`
- `Deployed`
- `Engineer`

**Exercise 4: String Repetition**

Print the word `Python` five times using the multiplication operator.

### Intermediate Level

**Exercise 5: Reverse a String**

Get a string from the user and reverse it using slicing.

**Exercise 6: String Concatenation**

Get first name and last name from the user.

Combine them into a full name.

**Exercise 7: Character Counter**

Get a sentence from the user and count its total characters using `len()`.

Compare the result with a manual loop-based count.

**Exercise 8: Search for a Word**

Get a sentence and a search word.

Check whether the word exists using `in`.

### FDE-Oriented Practical Exercises

**Exercise 9: Email Information Extractor**

Get an email address from the user.

Extract:

- Username
- Domain

Handle the case where `@` is missing.

**Exercise 10: AI Response Inspector**

Given an AI-generated response:

1. Display the original response.
2. Display the total string length.
3. Extract the first 20 characters.
4. Extract the last 20 characters.
5. Check whether a specific keyword exists.
6. Display the reversed string.

**Exercise 11: File Extension Extractor**

Given a filename such as:

```python
filename = "customer_report.csv"
```

Extract the filename and extension separately.

---

## 20. Quick Revision

| Concept | Explanation |
|---|---|
| `str` | Python string data type |
| `'text'` | Single-quoted string |
| `"text"` | Double-quoted string |
| `'''text'''` | Triple single-quoted string |
| `"""text"""` | Triple double-quoted string |
| Positive indexing | Access characters from left to right |
| Negative indexing | Access characters from right to left |
| Slicing | Extract a portion of a string |
| `+` | Concatenate strings |
| `*` | Repeat strings |
| `len()` | Returns the number of Unicode code points |
| `in` | Checks substring membership |
| `[::-1]` | Reverses a string |
| Immutable | Original string cannot be changed in place |
| `\n` | Newline |
| `\t` | Tab |
| `r""` | Raw string literal |

---

## 21. Self-Assessment Questions

1. What is a string in Python?
2. Which Python class represents strings?
3. What is the difference between single and double quotes?
4. Why do we use triple quotes?
5. What is positive indexing?
6. What is negative indexing?
7. What is the difference between indexing and slicing?
8. Why is the ending index excluded in slicing?
9. What does `[::-1]` do?
10. What is string concatenation?
11. Why are strings immutable?
12. What happens when we try to modify a string using an index?
13. What does `len()` return?
14. What is the purpose of escape sequences?
15. What is a raw string?
16. Why is string processing important in AI and FDE applications?

---

## 22. Learning Outcome

After completing this topic, you should understand:

- How to create strings using different quotation styles.
- How to access individual characters.
- How positive and negative indexing work.
- How to extract substrings using slicing.
- How to concatenate and repeat strings.
- How to find string length.
- How to check substring membership.
- Why strings are immutable.
- How to iterate through strings.
- How to use escape sequences and raw strings.
- How string processing applies to API data and AI-generated text.


