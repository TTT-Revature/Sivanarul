
# Introduction to Regular Expressions in Python



---

## 1. What Are Regular Expressions?

A Regular Expression (RegEx) is a sequence of characters that defines a search pattern.

It helps us find, extract, validate, split, and replace specific patterns in text.

For example, imagine you receive this text:

```text
Contact us at support@example.com or call 9876543210.
```

You may want to:
- Find the email address.
- Extract the mobile number.
- Check whether a string follows a particular format.
- Remove unwanted characters.
- Identify dates, numbers, or IDs from text.

Regular expressions make these operations easier.

### Real-world analogy

Imagine searching for a particular type of vehicle in a parking area.

Instead of searching for one exact vehicle, you define a rule:

- Vehicle must start with TN.
- It must contain two digits.
- It must contain two letters.
- It must end with four digits.

A regular expression works similarly: it searches for text that follows a specified pattern.

---

## 2. The `re` Module

Python provides a built-in module called `re` for working with regular expressions.

You do not need to install an external package.

### Importing the module

```python
import re
```

### Basic example

```python
import re

text = "My employee ID is EMP123"

result = re.search("EMP", text)

print(result)
```

**Output (representative):**

```text
<re.Match object; ...>
```

The exact object representation may vary.

The result is a Match object because the pattern was found.

If the pattern is not found, `re.search()` returns `None`.

---

## 3. Understanding Raw Strings (`r""`)

Regular expressions frequently contain backslashes.

Python also uses backslashes for escape sequences.

To avoid confusion, we commonly write regular expressions using raw strings.

### Normal string

```python
pattern = "\\d+"
```

### Raw string

```python
pattern = r"\d+"
```

Both represent the same regular expression pattern in this example.

The `r` prefix tells Python to treat backslashes as ordinary characters for most string escape processing.

**Recommended practice:**

```python
pattern = r"\d+"
```

Use raw strings for most regular expression patterns.

---

## 4. Basic Regular Expression Characters

RegEx uses special characters to describe patterns.

### 4.1 Digits – `\d`

`\d` matches a digit from 0 to 9.

```python
import re

text = "Order number: 12345"

result = re.findall(r"\d", text)

print(result)
```

**Output:**

```text
['1', '2', '3', '4', '5']
```

### 4.2 Non-digits – `\D`

`\D` matches any character that is not a digit.

```python
import re

text = "ABC123"

result = re.findall(r"\D", text)

print(result)
```

**Output:**

```text
['A', 'B', 'C']
```

### 4.3 Word characters – `\w`

`\w` matches letters, digits, and underscores.

```python
import re

text = "Python_123!"

result = re.findall(r"\w", text)

print(result)
```

**Output:**

```text
['P', 'y', 't', 'h', 'o', 'n', '_', '1', '2', '3']
```

### 4.4 Non-word characters – `\W`

`\W` matches characters that are not word characters.

```python
import re

text = "Python@123!"

result = re.findall(r"\W", text)

print(result)
```

**Output:**

```text
['@', '!']
```

### 4.5 Whitespace – `\s`

`\s` matches whitespace characters, including spaces, tabs, and newlines.

```python
import re

text = "Hello World Python"

result = re.findall(r"\s", text)

print(result)
```

**Output:**

```text
[' ', ' ']
```

### 4.6 Non-whitespace – `\S`

`\S` matches any character that is not whitespace.

```python
import re

text = "Hello World"

result = re.findall(r"\S", text)

print(result)
```

**Output:**

```text
['H', 'e', 'l', 'l', 'o', 'W', 'o', 'r', 'l', 'd']
```

---

## 5. Quantifiers in Regular Expressions

Quantifiers specify how many times a character or pattern should occur.

| Quantifier | Meaning |
|---|---|
| `*` | Zero or more occurrences |
| `+` | One or more occurrences |
| `?` | Zero or one occurrence |
| `{n}` | Exactly n occurrences |
| `{n,}` | At least n occurrences |
| `{n,m}` | Between n and m occurrences |

### 5.1 Asterisk – `*`

Matches zero or more occurrences.

```python
import re

text = "ab abb abbb a"

result = re.findall(r"ab*", text)

print(result)
```

**Output:**

```text
['ab', 'abb', 'abbb', 'a']
```

Explanation:

- `a` is required.
- `b*` means zero or more `b` characters.

Therefore, even `a` alone matches.

### 5.2 Plus – `+`

Matches one or more occurrences.

```python
import re

text = "ab abb abbb a"

result = re.findall(r"ab+", text)

print(result)
```

**Output:**

```text
['ab', 'abb', 'abbb']
```

The final `a` does not match because at least one `b` is required.

### 5.3 Question mark – `?`

Matches zero or one occurrence.

```python
import re

text = "color colour"

result = re.findall(r"colou?r", text)

print(result)
```

**Output:**

```text
['color', 'colour']
```

The `u?` means the letter `u` is optional.

### 5.4 Exact count – `{n}`

```python
import re

text = "12 123 1234 12345"

result = re.findall(r"\d{3}", text)

print(result)
```

**Output:**

```text
['123', '123', '123']
```

This finds non-overlapping groups of exactly three digits.

### 5.5 Range – `{n,m}`

```python
import re

text = "12 123 1234 12345"

result = re.findall(r"\d{2,4}", text)

print(result)
```

**Output:**

```text
['12', '123', '1234', '1234', '5']
```

The pattern matches between two and four digits. Because matching is non-overlapping and the quantifier is greedy, the five-digit sequence is split into `1234` and `5`.

---

## 6. Character Classes – `[]`

Square brackets define a character class.

They match one character from the specified set.

### Example 1: Match selected characters

```python
import re

text = "apple banana orange"

result = re.findall(r"[aeiou]", text)

print(result)
```

**Output:**

```text
['a', 'a', 'a', 'a', 'o', 'a', 'e']
```

This pattern finds vowels.

### Example 2: Match a range of digits

```python
import re

text = "A1 B2 C3 D4"

result = re.findall(r"[0-9]", text)

print(result)
```

**Output:**

```text
['1', '2', '3', '4']
```

### Example 3: Match uppercase letters

```python
import re

text = "Python FDE 2026"

result = re.findall(r"[A-Z]", text)

print(result)
```

**Output:**

```text
['P', 'F', 'D', 'E']
```

### Common character classes

| Pattern | Meaning |
|---|---|
| `[abc]` | a, b, or c |
| `[a-z]` | Lowercase English letters |
| `[A-Z]` | Uppercase English letters |
| `[0-9]` | Digits |
| `[a-zA-Z]` | English letters |
| `[a-zA-Z0-9]` | English letters and digits |
| `[^0-9]` | Any character except digits |

**Important:** Inside a character class, `^` at the beginning means negation.

---

## 7. Anchors – `^` and `$`

Anchors match positions rather than ordinary characters.

### 7.1 Start of string – `^`

```python
import re

text = "Python Developer"

result = re.search(r"^Python", text)

print(result is not None)
```

**Output:**

```text
True
```

The pattern matches only if `Python` occurs at the beginning.

### 7.2 End of string – `$`

```python
import re

text = "Python Developer"

result = re.search(r"Developer$", text)

print(result is not None)
```

**Output:**

```text
True
```

The pattern matches only if `Developer` occurs at the end.

### 7.3 Combining both anchors

```python
import re

text = "12345"

result = re.fullmatch(r"\d+", text)

print(result is not None)
```

**Output:**

```text
True
```

`re.fullmatch()` is another way to check whether the entire string matches a pattern.

Compare:

- `re.search()` finds a match anywhere.
- `re.match()` checks from the beginning.
- `re.fullmatch()` requires the entire string to match.

---

## 8. Important Functions in Python's `re` Module

Python provides several functions for regular expression operations.

| Function | Purpose |
|---|---|
| `re.search()` | Finds the first match anywhere in the string |
| `re.match()` | Checks for a match at the beginning |
| `re.fullmatch()` | Checks whether the entire string matches |
| `re.findall()` | Returns all non-overlapping matches as a list |
| `re.finditer()` | Returns an iterator of match objects |
| `re.sub()` | Replaces matching text |
| `re.split()` | Splits a string using a pattern |
| `re.compile()` | Compiles a pattern for reuse |

### 8.1 `re.search()`

```python
import re

text = "My employee ID is EMP123"

result = re.search(r"EMP\d+", text)

if result:
    print(result.group())
else:
    print("No match found")
```

**Output:**

```text
EMP123
```

`group()` returns the matched text.

### 8.2 `re.match()`

```python
import re

text = "EMP123 is my employee ID"

result = re.match(r"EMP\d+", text)

if result:
    print(result.group())
else:
    print("No match found")
```

**Output:**

```text
EMP123
```

Now consider:

```python
import re

text = "My ID is EMP123"

result = re.match(r"EMP\d+", text)

print(result)
```

**Output:**

```text
None
```

The pattern does not begin at the start of the string.

### 8.3 `re.fullmatch()`

```python
import re

employee_id = "EMP123"

result = re.fullmatch(r"EMP\d{3}", employee_id)

print(result is not None)
```

**Output:**

```text
True
```

Try changing the input to:

```python
employee_id = "My ID is EMP123"
```

The result will be `False` because the entire input does not match the pattern.

### 8.4 `re.findall()`

Finds all non-overlapping matches.

```python
import re

text = "Order 101, Order 102, Order 103"

result = re.findall(r"\d+", text)

print(result)
```

**Output:**

```text
['101', '102', '103']
```

### 8.5 `re.finditer()`

Returns an iterator containing match objects.

```python
import re

text = "Order 101, Order 102"

matches = re.finditer(r"\d+", text)

for match in matches:
    print(match.group())
    print(match.start())
    print(match.end())
```

**Output:**

```text
101
6
9
102
17
20
```

Here:

- `group()` returns the matched text.
- `start()` returns the starting index.
- `end()` returns the ending index (exclusive).

### 8.6 `re.sub()`

Replaces matched text.

```python
import re

text = "My phone number is 9876543210"

result = re.sub(r"\d", "*", text)

print(result)
```

**Output:**

```text
My phone number is **********
```

You can also replace multiple digits together:

```python
import re

text = "Order ID: 12345"

result = re.sub(r"\d+", "XXXXX", text)

print(result)
```

**Output:**

```text
Order ID: XXXXX
```

### 8.7 `re.split()`

Splits a string using a regular expression.

```python
import re

text = "Python,Java;JavaScript|C++"

result = re.split(r"[,;|]", text)

print(result)
```

**Output:**

```text
['Python', 'Java', 'JavaScript', 'C++']
```

The pattern matches a comma, semicolon, or vertical bar.

### 8.8 `re.compile()`

Compiles a pattern so it can be reused.

```python
import re

pattern = re.compile(r"\d+")

text1 = "Order 101"
text2 = "Order 202"

print(pattern.findall(text1))
print(pattern.findall(text2))
```

**Output:**

```text
['101']
['202']
```

---

## 9. Groups in Regular Expressions

Parentheses `()` create capturing groups.

They allow us to extract specific parts of a match.

### Example: Extracting date components

```python
import re

text = "Date: 17-11-2026"

pattern = r"(\d{2})-(\d{2})-(\d{4})"

result = re.search(pattern, text)

if result:
    print(result.group(0))
    print(result.group(1))
    print(result.group(2))
    print(result.group(3))
```

**Output:**

```text
17-11-2026
17
11
2026
```

Explanation:

| Expression | Meaning |
|---|---|
| `group(0)` | Entire match |
| `group(1)` | First capturing group |
| `group(2)` | Second capturing group |
| `group(3)` | Third capturing group |

### Named groups

Named groups make patterns easier to understand.

```python
import re

text = "Date: 17-11-2026"

pattern = r"(?P<day>\d{2})-(?P<month>\d{2})-(?P<year>\d{4})"

result = re.search(pattern, text)

if result:
    print(result.group("day"))
    print(result.group("month"))
    print(result.group("year"))
```

**Output:**

```text
17
11
2026
```

---

## 10. Greedy and Non-Greedy Matching

By default, quantifiers such as `*` and `+` are greedy.

They try to match as much text as possible while still allowing the overall pattern to succeed.

### Greedy example

```python
import re

text = "<h1>Hello</h1><h1>World</h1>"

result = re.findall(r"<h1>.*</h1>", text)

print(result)
```

**Output:**

```text
['<h1>Hello</h1><h1>World</h1>']
```

The `.*` matches as much as possible.

### Non-greedy example

Add `?` after the quantifier:

```python
import re

text = "<h1>Hello</h1><h1>World</h1>"

result = re.findall(r"<h1>.*?</h1>", text)

print(result)
```

**Output:**

```text
['<h1>Hello</h1>', '<h1>World</h1>']
```

The `.*?` matches as little as possible while allowing the pattern to succeed.

**Important:** Regular expressions are useful for simple text extraction, but they are not a reliable replacement for an HTML parser when processing complex HTML documents.

---

## 11. Flags in Regular Expressions

Flags modify how a pattern behaves.

### 11.1 Ignore case – `re.IGNORECASE`

```python
import re

text = "Python PYTHON python"

result = re.findall(r"python", text, re.IGNORECASE)

print(result)
```

**Output:**

```text
['Python', 'PYTHON', 'python']
```

### 11.2 Multiline – `re.MULTILINE`

Makes `^` and `$` operate at the beginning and end of each line.

```python
import re

text = """Python
Java
Python Developer"""

result = re.findall(r"^Python", text, re.MULTILINE)

print(result)
```

**Output:**

```text
['Python', 'Python']
```

### 11.3 Dot-all – `re.DOTALL`

Allows `.` to match newline characters as well.

```python
import re

text = "Hello\nWorld"

result = re.findall(r"Hello.*World", text, re.DOTALL)

print(result)
```

**Output:**

```text
['Hello\nWorld']
```

---

## 12. Practical Example: Extracting Information from Text

Imagine an application receives a customer message.

```python
import re

message = """
Customer: Arun
Email: arun@example.com
Phone: 9876543210
Order ID: ORD12345
"""

email = re.search(r"[\w.+-]+@[\w.-]+\.[A-Za-z]{2,}", message)
phone = re.search(r"\b\d{10}\b", message)
order_id = re.search(r"\bORD\d+\b", message)

print("Email:", email.group() if email else "Not found")
print("Phone:", phone.group() if phone else "Not found")
print("Order ID:", order_id.group() if order_id else "Not found")
```

**Output:**

```text
Email: arun@example.com
Phone: 9876543210
Order ID: ORD12345
```

This is a basic extraction example.

The email pattern is not a complete implementation of email-address validation. Real systems should apply appropriate validation and verification.

---

## 13. Regular Expressions in FDE Work

Regular expressions are valuable for Forward-Deployed Engineers because they frequently work with data coming from different systems.

### Common FDE use cases

| Use case | RegEx application |
|---|---|
| API response processing | Extract IDs and values from text |
| Log analysis | Identify error codes and timestamps |
| Data cleaning | Remove unwanted characters |
| Document processing | Extract dates and reference numbers |
| Customer data integration | Identify email addresses and phone-like values |
| AI pipelines | Extract structured fields from generated or unstructured text |
| CLI tools | Validate simple input formats |

### Example: Extracting error codes from logs

```python
import re

logs = """
INFO: Application started
ERROR: 500 Internal Server Error
WARNING: High memory usage
ERROR: 404 Resource Not Found
"""

errors = re.findall(r"ERROR:\s*(\d+)", logs)

print(errors)
```

**Output:**

```text
['500', '404']
```

### Example: Cleaning unwanted symbols

```python
import re

customer_name = "Arun@123!"

cleaned_name = re.sub(r"[^A-Za-z\s]", "", customer_name)

print(cleaned_name)
```

**Output:**

```text
Arun
```

This example keeps English letters and spaces only. It is not suitable for every language or every name.

---

## 14. Common Mistakes

### Mistake 1: Forgetting the raw string prefix

```python
pattern = "\d+"
```

This may work in Python, but Python can issue an invalid-escape warning.

Prefer:

```python
pattern = r"\d+"
```

### Mistake 2: Confusing `search()` and `match()`

```python
text = "My ID is EMP123"

print(re.search(r"EMP", text))
print(re.match(r"EMP", text))
```

`search()` finds the pattern anywhere; `match()` checks only from the beginning.

### Mistake 3: Forgetting that `findall()` returns a list

```python
result = re.findall(r"\d+", "Order 123")
print(result)
```

Output:

```text
['123']
```

It does not return a single Match object.

### Mistake 4: Using `*` when at least one character is required

```python
r"\d*"
```

This allows zero digits and can produce empty matches.

Use:

```python
r"\d+"
```

when at least one digit is required.

### Mistake 5: Assuming RegEx validates all business rules

For example:

```python
r"\d{10}"
```

checks for ten digits, but does not prove that the number is a valid, active mobile number.

Pattern matching and real-world validation are different tasks.

### Mistake 6: Using RegEx for every text-processing task

Use the right tool for the problem:

- Simple exact text operations: string methods.
- Pattern matching: `re`.
- Structured JSON: `json`.
- HTML documents: an HTML parser.
- CSV files: Python's `csv` module or Pandas.

---

## 15. Practice Exercises

### Beginner Level

1. Extract all digits from `"Python 3 is released in 2026"`.
2. Find all lowercase letters from `"Hello PYTHON World"`.
3. Extract all words from `"Python is useful for AI"`.
4. Find all spaces in a sentence.
5. Check whether a string starts with `"EMP"` using `re.match()`.

### Intermediate Level

6. Extract all 10-digit sequences from a text.
7. Extract all email-like strings from a paragraph.
8. Replace all digits with `*`.
9. Split a string using commas, spaces, or semicolons.
10. Extract dates in the format `DD-MM-YYYY`.
11. Find all words that start with an uppercase letter.
12. Use capturing groups to extract day, month, and year.

### FDE Practical Level

13. Extract HTTP status codes from application logs.
14. Extract order IDs that follow the format `ORD` followed by five digits.
15. Clean customer names by removing unwanted punctuation.
16. Extract email addresses and phone-like values from a customer support message.
17. Build a small log-processing program that counts how many `ERROR`, `WARNING`, and `INFO` entries exist.

---

## 16. Quick Revision

| Concept | Syntax | Purpose |
|---|---|---|
| Digit | `\d` | Match a digit |
| Non-digit | `\D` | Match a non-digit |
| Word character | `\w` | Match a letter, digit, or underscore |
| Non-word | `\W` | Match a non-word character |
| Whitespace | `\s` | Match whitespace |
| Non-whitespace | `\S` | Match non-whitespace |
| Zero or more | `*` | Match zero or more |
| One or more | `+` | Match one or more |
| Optional | `?` | Match zero or one |
| Exact count | `{n}` | Match exactly n |
| Character class | `[]` | Match one selected character |
| Start anchor | `^` | Match at the beginning |
| End anchor | `$` | Match at the end |
| Capturing group | `()` | Capture part of a match |
| Search | `re.search()` | Find first match anywhere |
| Match | `re.match()` | Match at the beginning |
| Full match | `re.fullmatch()` | Match the entire string |
| Find all | `re.findall()` | Return all matches |
| Replace | `re.sub()` | Replace matching text |
| Split | `re.split()` | Split using a pattern |
| Compile | `re.compile()` | Reuse a compiled pattern |

---

## 17. Self-Assessment

Try answering without referring to the notes.

1. What is a regular expression?
2. Why do we commonly use raw strings for RegEx patterns?
3. What is the difference between `\d` and `\D`?
4. What is the difference between `*` and `+`?
5. What is the purpose of `{3,5}`?
6. What is the difference between `re.search()` and `re.match()`?
7. What does `re.fullmatch()` check?
8. What does `re.findall()` return?
9. What is the purpose of capturing groups?
10. What is the difference between greedy and non-greedy matching?
11. How can you replace all digits in a string?
12. Why should we not use RegEx as a complete substitute for structured-data parsers?

---

## 18. Learning Outcome

After completing this chapter, you should be able to:

- Explain what regular expressions are.
- Import and use Python's `re` module.
- Understand common RegEx symbols and quantifiers.
- Search, extract, replace, and split text.
- Use capturing groups and flags.
- Perform basic pattern-based data cleaning.
- Identify practical applications of RegEx in FDE projects.


