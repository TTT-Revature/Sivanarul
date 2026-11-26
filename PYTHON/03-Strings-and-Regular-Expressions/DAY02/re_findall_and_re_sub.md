
# Python Regular Expressions – `re.findall()` and `re.sub()`



---

## 1. Introduction

Python provides the built-in `re` module for regular expression operations.

Two commonly used functions are:

1. `re.findall()` – Extracts all non-overlapping matches from a string.
2. `re.sub()` – Replaces matching patterns with another value.

Consider this customer message:

```text
Customer: Arun
Phone: 9876543210
Order ID: ORD12345
Email: arun@example.com
```

Suppose you want to:

- Extract the phone number.
- Extract the order ID.
- Extract the email address.
- Replace sensitive information.
- Remove unwanted characters.

These are practical situations where `re.findall()` and `re.sub()` are useful.

---

# PART 1: re.findall()

## 2. What Is `re.findall()`?

`re.findall()` searches a string for all non-overlapping occurrences of a regular expression pattern.

It returns the matching results as a Python list.

### Syntax

```python
re.findall(pattern, string, flags=0)
```

| Parameter | Description |
|---|---|
| `pattern` | Regular expression pattern |
| `string` | Input text to search |
| `flags` | Optional RegEx flags |

### Basic example

```python
import re

text = "Python 3, Java 17, Python 3.12"

result = re.findall(r"Python", text)

print(result)
```

**Output:**

```text
['Python', 'Python']
```

Explanation:

- Python searches the entire string.
- It finds two occurrences of `Python`.
- It returns both matches in a list.

---

## 3. Extracting All Numbers

One common application of `re.findall()` is extracting numbers from text.

```python
import re

text = "I have 2 laptops, 3 phones and 10 tablets"

result = re.findall(r"\d+", text)

print(result)
```

**Output:**

```text
['2', '3', '10']
```

Explanation:

- `\d` matches a digit.
- `+` matches one or more consecutive digits.
- `\d+` extracts each complete sequence of digits.

**Important:** The extracted values are strings, not integers.

If you need integers:

```python
import re

text = "I have 2 laptops, 3 phones and 10 tablets"

result = re.findall(r"\d+", text)

numbers = [int(value) for value in result]

print(numbers)
```

**Output:**

```text
[2, 3, 10]
```

---

## 4. Extracting Email Addresses

Imagine an application receives a paragraph containing multiple email addresses.

```python
import re

text = """
Contact:
admin@example.com
support@gmail.com
developer@company.in
"""

pattern = r"[\w.+-]+@[\w.-]+\.[A-Za-z]{2,}"

result = re.findall(pattern, text)

print(result)
```

**Output:**

```text
['admin@example.com', 'support@gmail.com', 'developer@company.in']
```

Pattern explanation:

| Pattern | Meaning |
|---|---|
| `[\w.+-]+` | One or more permitted characters before `@` |
| `@` | Matches the @ symbol |
| `[\w.-]+` | Matches characters in the domain portion |
| `\.` | Matches a literal dot |
| `[A-Za-z]{2,}` | Matches at least two English letters |

This is a basic email-like pattern, not a complete email validation solution.

---

## 5. Extracting Phone Numbers

Suppose you receive customer details in a text document.

```python
import re

text = """
Arun: 9876543210
Kumar: 8765432109
Siva: 9123456780
"""

result = re.findall(r"\b\d{10}\b", text)

print(result)
```

**Output:**

```text
['9876543210', '8765432109', '9123456780']
```

Explanation:

| Pattern | Meaning |
|---|---|
| `\b` | Word boundary |
| `\d` | Digit |
| `{10}` | Exactly ten digits |
| `\b` | Word boundary |

This extracts ten-digit sequences. It does not establish whether a number is active or assigned to a real person.

---

## 6. Extracting Order IDs

Suppose your application stores order IDs in the following format:

`ORD` followed by five digits.

```python
import re

text = """
ORD12345
ORD67890
ORD54321
"""

result = re.findall(r"\bORD\d{5}\b", text)

print(result)
```

**Output:**

```text
['ORD12345', 'ORD67890', 'ORD54321']
```

Explanation:

- `ORD` matches the fixed prefix.
- `\d{5}` matches exactly five digits.
- `\b` checks the word boundaries.

---

## 7. Using Capturing Groups with `re.findall()`

Capturing groups allow you to extract specific portions of a match.

### Example: Extracting dates

```python
import re

text = """
17-11-2026
18-12-2026
19-01-2027
"""

pattern = r"(\d{2})-(\d{2})-(\d{4})"

result = re.findall(pattern, text)

print(result)
```

**Output:**

```text
[('17', '11', '2026'), ('18', '12', '2026'), ('19', '01', '2027')]
```

Notice something important:

When the pattern contains multiple capturing groups, `findall()` returns tuples containing the captured values.

### Extracting only the year

```python
import re

text = "17-11-2026 and 18-12-2026"

result = re.findall(r"\d{2}-\d{2}-(\d{4})", text)

print(result)
```

**Output:**

```text
['2026', '2026']
```

Because only the year is captured, the result contains only the year values.

### Important behaviour

| Pattern | `findall()` result |
|---|---|
| `r"\d+"` | List of matched strings |
| `r"(\d+)"` | List of captured strings |
| `r"(\d+)-(\w+)"` | List of tuples |
| `r"(?:\d+)"` | List of full matched strings |

A non-capturing group `(?:...)` groups part of a pattern without returning it as a separate captured value.

---

## 8. Difference Between `findall()` and `finditer()`

Both functions can find multiple matches, but their return values differ.

### Using `findall()`

```python
import re

text = "Order 101, Order 102"

result = re.findall(r"\d+", text)

print(result)
```

**Output:**

```text
['101', '102']
```

### Using `finditer()`

```python
import re

text = "Order 101, Order 102"

result = re.finditer(r"\d+", text)

for match in result:
    print(match.group())
    print(match.start())
```

**Output:**

```text
101
6
102
17
```

| Feature | `findall()` | `finditer()` |
|---|---|---|
| Return type | List | Iterator |
| Match text | Yes | Yes, using `group()` |
| Start/end positions | No | Yes |
| Capturing groups | Returns captured values | Returns Match objects |
| Best use | Collect matching values | Process matches with positions |

---

# PART 2: re.sub()

## 9. What Is `re.sub()`?

`re.sub()` replaces every non-overlapping occurrence of a matching pattern with a replacement value.

### Syntax

```python
re.sub(pattern, repl, string, count=0, flags=0)
```

| Parameter | Description |
|---|---|
| `pattern` | Pattern to search for |
| `repl` | Replacement string or function |
| `string` | Original input text |
| `count` | Maximum number of replacements; `0` means all |
| `flags` | Optional RegEx flags |

### Basic example

```python
import re

text = "Python is easy. Python is powerful."

result = re.sub(r"Python", "Java", text)

print(result)
```

**Output:**

```text
Java is easy. Java is powerful.
```

Explanation:

- Python searches for every occurrence of `Python`.
- It replaces each occurrence with `Java`.
- It returns a new string.

**Important:** `re.sub()` does not modify the original string.

---

## 10. Replacing All Digits

Imagine you want to hide numeric information in a message.

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

Explanation:

- `\d` matches each individual digit.
- `*` is the replacement string.
- Every matched digit is replaced.

### Replacing complete number sequences

```python
import re

text = "Order 12345 and Order 67890"

result = re.sub(r"\d+", "XXXXX", text)

print(result)
```

**Output:**

```text
Order XXXXX and Order XXXXX
```

Difference:

- `\d` matches one digit at a time.
- `\d+` matches a complete consecutive sequence of digits.

---

## 11. Removing Special Characters

Suppose customer data contains unwanted symbols.

```python
import re

text = "Arun@123! Developer#"

result = re.sub(r"[^A-Za-z\s]", "", text)

print(result)
```

**Output:**

```text
Arun Developer
```

Explanation:

| Pattern | Meaning |
|---|---|
| `[]` | Character class |
| `^` | Negation at the beginning of a character class |
| `A-Z` | Uppercase English letters |
| `a-z` | Lowercase English letters |
| `\s` | Whitespace |
| `""` | Replace matches with nothing |

The pattern removes everything except English letters and whitespace.

This is a simple cleaning example, not a universal method for cleaning names or multilingual customer data.

---

## 12. Removing Extra Spaces

Consider the following text:

```text
Python     is       useful
```

We want to reduce consecutive whitespace to a single space.

```python
import re

text = "Python     is       useful"

result = re.sub(r"\s+", " ", text)

print(result)
```

**Output:**

```text
Python is useful
```

Explanation:

- `\s` matches whitespace.
- `+` matches one or more consecutive whitespace characters.
- `" "` replaces each matching whitespace sequence with one space.

If you also want to remove leading and trailing spaces:

```python
import re

text = "   Python     is       useful   "

result = re.sub(r"\s+", " ", text).strip()

print(result)
```

**Output:**

```text
Python is useful
```

---

## 13. Using the `count` Parameter

The `count` parameter controls how many replacements are performed.

### Example

```python
import re

text = "Python Python Python Python"

result = re.sub(r"Python", "Java", text, count=2)

print(result)
```

**Output:**

```text
Java Java Python Python
```

Explanation:

- `count=2` replaces only the first two matches.
- The remaining matches stay unchanged.
- `count=0` replaces all matches.

---

## 14. Using Capturing Groups in `re.sub()`

Capturing groups can be reused in the replacement string.

### Example: Changing date format

Original format:

```text
17-11-2026
```

Required format:

```text
2026/11/17
```

Code:

```python
import re

text = "17-11-2026"

result = re.sub(
    r"(\d{2})-(\d{2})-(\d{4})",
    r"\3/\2/\1",
    text
)

print(result)
```

**Output:**

```text
2026/11/17
```

Explanation:

| Group | Value |
|---|---|
| `\1` | Day |
| `\2` | Month |
| `\3` | Year |

The replacement string rearranges the captured groups.

This changes the text format; it does not verify whether the date is a valid calendar date.

---

## 15. Using a Function as the Replacement

`re.sub()` can accept a function instead of a replacement string.

This is useful when replacement logic depends on the matched value.

### Example: Replacing numbers with their doubled values

```python
import re

text = "Numbers: 10, 20, 30"

def double_number(match):
    number = int(match.group())
    return str(number * 2)

result = re.sub(r"\d+", double_number, text)

print(result)
```

**Output:**

```text
Numbers: 20, 40, 60
```

Explanation:

1. `re.sub()` finds a number.
2. It passes the Match object to `double_number()`.
3. `match.group()` extracts the matched number.
4. The function doubles it.
5. The returned string replaces the original match.

This technique is useful for dynamic text transformations.

---

## 16. Practical Example: Customer Data Processing

Imagine an application receives customer information in an unstructured format.

### Input

```python
import re

customer_message = """
Name: Arun@123
Phone: 9876543210
Order: ORD12345
Email: arun@example.com
"""
```

### Step 1: Extract customer information

```python
name = re.search(r"Name:\s*(.+)", customer_message)
phone = re.search(r"Phone:\s*(\d{10})", customer_message)
order = re.search(r"Order:\s*(ORD\d+)", customer_message)
email = re.search(
    r"Email:\s*([\w.+-]+@[\w.-]+\.[A-Za-z]{2,})",
    customer_message
)
```

### Step 2: Clean the customer name

```python
if name:
    clean_name = re.sub(r"[^A-Za-z\s]", "", name.group(1))
    print("Name:", clean_name.strip())
```

### Step 3: Display extracted information

```python
print("Phone:", phone.group(1) if phone else "Not found")
print("Order:", order.group(1) if order else "Not found")
print("Email:", email.group(1) if email else "Not found")
```

**Output:**

```text
Name: Arun
Phone: 9876543210
Order: ORD12345
Email: arun@example.com
```

This is a demonstration of pattern-based extraction and cleaning. In a production integration, validate the input format, handle missing or repeated fields, and avoid assuming that the input always follows this exact layout.

---

## 17. Practical Example: Log Processing

Applications generate logs that may contain large amounts of information.

An FDE may need to extract error codes and clean sensitive information.

### Input

```python
import re

logs = """
INFO: Application started
ERROR: 500 Internal Server Error
WARNING: High memory usage
ERROR: 404 Resource Not Found
INFO: User logged in
"""
```

### Extract error codes

```python
error_codes = re.findall(r"ERROR:\s*(\d+)", logs)

print(error_codes)
```

**Output:**

```text
['500', '404']
```

### Replace error codes

```python
cleaned_logs = re.sub(r"ERROR:\s*\d+", "ERROR: CODE_HIDDEN", logs)

print(cleaned_logs)
```

**Output:**

```text
INFO: Application started
ERROR: CODE_HIDDEN Internal Server Error
WARNING: High memory usage
ERROR: CODE_HIDDEN Resource Not Found
INFO: User logged in
```

This demonstrates how RegEx can support basic log analysis and text transformation.

---

## 18. `re.findall()` vs `re.sub()`

| Feature | `re.findall()` | `re.sub()` |
|---|---|---|
| Main purpose | Extract matches | Replace matches |
| Returns | List | String |
| Changes original string? | No | No |
| Uses a pattern? | Yes | Yes |
| Supports capturing groups? | Yes | Yes |
| Supports replacement functions? | No | Yes |
| Common application | Extract IDs and numbers | Mask or clean text |

### Remember

```python
re.findall(pattern, text)
```

Use this when you want to collect matching values.

```python
re.sub(pattern, replacement, text)
```

Use this when you want to transform matching text.

---

## 19. Common Mistakes

### Mistake 1: Expecting `findall()` to return integers

```python
result = re.findall(r"\d+", "Age 25")
print(result)
```

Output:

```text
['25']
```

Convert explicitly if integers are required:

```python
numbers = [int(value) for value in result]
```

### Mistake 2: Confusing `\d` and `\d+`

```python
re.findall(r"\d", "12345")
```

Output:

```text
['1', '2', '3', '4', '5']
```

But:

```python
re.findall(r"\d+", "12345")
```

Output:

```text
['12345']
```

### Mistake 3: Forgetting that `re.sub()` returns a new string

```python
text = "Python 123"

re.sub(r"\d+", "", text)

print(text)
```

Output:

```text
Python 123
```

Correct:

```python
text = re.sub(r"\d+", "", text)
```

### Mistake 4: Misunderstanding capturing groups

```python
re.findall(r"(\d+)-(\w+)", "123-ABC")
```

Output:

```text
[('123', 'ABC')]
```

Multiple capturing groups produce tuples.

### Mistake 5: Using an incorrect replacement group reference

For captured groups in a replacement string, use references such as `\1`, `\2`, or the unambiguous form `\g<1>`.

For example:

```python
re.sub(r"(\d+)", r"ID-\g<1>", "123")
```

Output:

```text
ID-123
```

---

## 20. Practice Exercises

### Beginner Level

1. Extract all numbers from `"Python 3, Java 17, React 19"`.
2. Extract all words from a sentence.
3. Extract all email-like values from a paragraph.
4. Replace all digits with `*`.
5. Replace every occurrence of `"Python"` with `"AI"`.

### Intermediate Level

6. Extract all ten-digit sequences from a text.
7. Extract order IDs following the pattern `ORD` plus five digits.
8. Replace multiple spaces with one space.
9. Remove special characters while preserving spaces.
10. Extract day, month, and year using capturing groups.
11. Change the date format from `DD-MM-YYYY` to `YYYY/MM/DD`.
12. Use `count=2` to replace only the first two matching words.

### FDE Practical Level

13. Extract HTTP status codes from application logs.
14. Mask phone numbers by replacing their digits with `*`.
15. Extract customer IDs from an unstructured support message.
16. Remove unwanted characters from customer data.
17. Build a small program that extracts error codes and replaces sensitive information in logs.

---

## 21. Quick Revision

| Function / Pattern | Purpose |
|---|---|
| `re.findall()` | Extract all non-overlapping matches |
| `re.sub()` | Replace matching patterns |
| `\d+` | One or more digits |
| `\w+` | One or more word characters |
| `\s+` | One or more whitespace characters |
| `\d{10}` | Exactly ten digits |
| `()` | Capturing group |
| `(?:...)` | Non-capturing group |
| `\1` | Reference first captured group in a replacement |
| `count=0` | Replace all occurrences |
| `count=2` | Replace at most two occurrences |
| `match.group()` | Get matched text |

---

## 22. Self-Assessment

1. What is the purpose of `re.findall()`?
2. What type of value does `re.findall()` return?
3. What happens when a pattern contains two capturing groups?
4. What is the difference between `\d` and `\d+`?
5. What is the purpose of `re.sub()`?
6. Does `re.sub()` modify the original string?
7. What does the `count` parameter control?
8. How can you replace all digits with `*`?
9. How can you use captured groups inside a replacement string?
10. Can `re.sub()` accept a function as its replacement argument?
11. What is the difference between extraction and transformation?
12. How can these functions help process application logs?

---

## 23. Learning Outcome

After completing this chapter, you should be able to:

- Extract multiple matching values using `re.findall()`.
- Understand the effect of capturing groups on returned values.
- Convert extracted numeric strings into integers.
- Replace matching patterns using `re.sub()`.
- Clean and mask text.
- Use replacement counts and dynamic replacement functions.
- Apply RegEx to basic customer-data and log-processing tasks.

**Next recommended topic:** Regular Expression Groups, Lookahead, Lookbehind, and Backreferences.
