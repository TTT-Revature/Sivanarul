
# Python f-Strings and Formatted Output

**Suggested filename:** `21_f_strings_and_formatted_output.md`

## 1. Introduction

In Python, we frequently need to combine text with dynamic values.

For example, consider displaying an employee's information:

```python
name = "Sivanarul"
age = 27
salary = 41666.50

print("Employee name:", name)
print("Employee age:", age)
print("Employee salary:", salary)
```

This works, but when we have many variables and complex output, formatting becomes difficult to manage.

Python provides several ways to format strings:

1. String concatenation
2. Comma-separated values in `print()`
3. f-Strings
4. `str.format()`
5. `%` formatting
6. Format specification mini-language

Among these methods, **f-Strings are generally the preferred approach in modern Python.**

---

## 2. What Are f-Strings?

An f-string (formatted string literal) allows us to insert variables and expressions directly inside a string.

An f-string is created by adding the letter `f` or `F` before the opening quotation mark.

### Syntax

```python
f"Text {variable}"
```

The curly braces `{}` indicate where Python should evaluate an expression and insert its result.

### Example 1: Basic f-String

```python
name = "Sivanarul"

print(f"Hello, {name}")
```

**Output:**

```text
Hello, Sivanarul
```

### Example 2: Multiple Variables

```python
name = "Sivanarul"
age = 27
city = "Chennai"

print(f"My name is {name}. I am {age} years old. I live in {city}.")
```

**Output:**

```text
My name is Sivanarul. I am 27 years old. I live in Chennai.
```

### What Happens Internally?

Consider:

```python
name = "Sivanarul"

message = f"Hello, {name}"
```

Python evaluates the expression inside `{name}` and inserts its value into the resulting string.

The final value is:

```python
"Hello, Sivanarul"
```

An f-string produces a string. It does not modify the original variable.

---

## 3. f-Strings Can Evaluate Expressions

One important advantage of f-Strings is that we can write Python expressions inside curly braces.

### Example 1: Arithmetic Expressions

```python
num1 = 10
num2 = 20

print(f"Addition: {num1 + num2}")
print(f"Subtraction: {num1 - num2}")
print(f"Multiplication: {num1 * num2}")
```

**Output:**

```text
Addition: 30
Subtraction: -10
Multiplication: 200
```

### Example 2: Calling Functions

```python
name = "sivanarul"

print(f"Uppercase name: {name.upper()}")
print(f"Name length: {len(name)}")
```

**Output:**

```text
Uppercase name: SIVANARUL
Name length: 9
```

### Example 3: Conditional Expressions

```python
age = 27

print(f"Eligibility: {'Eligible' if age >= 18 else 'Not eligible'}")
```

**Output:**

```text
Eligibility: Eligible
```

**Important:** Expressions inside f-Strings are evaluated at runtime. Avoid putting complicated business logic inside them. Calculate important values separately to keep the code readable.

---

## 4. Formatting Decimal Values

In real-world applications, we frequently work with:

- Product prices
- Employee salaries
- Tax calculations
- Payment amounts
- Financial reports

We often need to control the number of decimal places displayed.

### Example 1: Two Decimal Places

```python
price = 99.56789

print(f"Price: {price:.2f}")
```

**Output:**

```text
Price: 99.57
```

Explanation:

| Part | Meaning |
|---|---|
| `:` | Starts the format specification |
| `.2` | Displays two digits after the decimal point |
| `f` | Uses fixed-point decimal notation |

### Example 2: Different Decimal Precisions

```python
value = 123.456789

print(f"Default: {value}")
print(f"Two decimals: {value:.2f}")
print(f"Three decimals: {value:.3f}")
print(f"Four decimals: {value:.4f}")
```

**Output:**

```text
Default: 123.456789
Two decimals: 123.46
Three decimals: 123.457
Four decimals: 123.4568
```

### Important Note

Formatting controls how a number is displayed. It does not change the original numeric value.

```python
price = 99.56789

formatted_price = f"{price:.2f}"

print(formatted_price)
print(type(formatted_price))
print(price)
```

**Output:**

```text
99.57
<class 'str'>
99.56789
```

The formatted result is a string, while the original variable remains a float.

For financial calculations, do not rely on display formatting to solve floating-point precision problems. Consider using `decimal.Decimal` when exact decimal arithmetic is required.

---

## 5. Formatting Integers

We can also format integers using f-Strings.

### Example 1: Integer Width

```python
number = 25

print(f"{number:5d}")
```

**Output:**

```text
   25
```

Explanation:

- `5` specifies a minimum field width of five characters.
- `d` represents decimal integer formatting.
- By default, the value is right-aligned.

### Example 2: Adding Leading Zeros

```python
employee_id = 42

print(f"Employee ID: {employee_id:05d}")
```

**Output:**

```text
Employee ID: 00042
```

This is useful when displaying identifiers with a fixed width.

---

## 6. Formatting Percentages

Python provides the `%` format specifier for percentage formatting.

It multiplies the value by 100 for display and adds a percentage symbol.

### Example

```python
completion = 0.8567

print(f"Completion: {completion:.2%}")
```

**Output:**

```text
Completion: 85.67%
```

Another example:

```python
success_rate = 0.95

print(f"Success Rate: {success_rate:.1%}")
```

**Output:**

```text
Success Rate: 95.0%
```

Remember:

- `0.95` becomes `95.0%`.
- `95` becomes `9500.0%`.

Use decimal ratios when formatting percentages.

---

## 7. Formatting Numbers with Commas

Large numbers can be difficult to read.

Python supports the comma separator in format specifications.

### Example

```python
salary = 1500000

print(f"Salary: {salary:,}")
```

**Output:**

```text
Salary: 1,500,000
```

### Example: Formatting Decimal Numbers

```python
revenue = 1234567.891

print(f"Revenue: {revenue:,.2f}")
```

**Output:**

```text
Revenue: 1,234,567.89
```

This is useful when generating financial reports and displaying large numerical values.

---

## 8. String Alignment and Width

Sometimes we need to align text to make output look organized.

Python supports three common alignment operators:

| Symbol | Meaning |
|---|---|
| `<` | Left alignment |
| `>` | Right alignment |
| `^` | Center alignment |

### Example 1: Left Alignment

```python
name = "Python"

print(f"{name:<15}")
```

**Output:**

```text
Python
```

The field occupies at least 15 characters, with the text aligned to the left.

### Example 2: Right Alignment

```python
name = "Python"

print(f"{name:>15}")
```

**Output:**

```text
         Python
```

### Example 3: Center Alignment

```python
name = "Python"

print(f"{name:^15}")
```

**Output:**

```text
     Python    
```

### Example 4: Custom Fill Characters

We can also specify a character to fill the remaining space.

```python
name = "Python"

print(f"{name:*^15}")
```

**Output:**

```text
*****Python****
```

This makes formatted console output easier to read.

---

## 9. Formatting Numbers with Signs

Python allows us to control how positive and negative signs are displayed.

### Example

```python
positive = 1500
negative = -1500

print(f"Positive: {positive:+}")
print(f"Negative: {negative:+}")
```

**Output:**

```text
Positive: +1500
Negative: -1500
```

Another option:

```python
number = 1500

print(f"Default: {number}")
print(f"With sign: {number:+}")
print(f"Space for positive sign: {number: }")
```

**Output:**

```text
Default: 1500
With sign: +1500
Space for positive sign:  1500
```

---

## 10. Scientific Notation

For very large or very small numbers, scientific notation can make values easier to display.

Python supports the `e` and `E` format specifiers.

### Example

```python
number = 1234567890

print(f"Scientific notation: {number:e}")
print(f"Scientific notation: {number:.2e}")
```

**Output:**

```text
Scientific notation: 1.234568e+09
Scientific notation: 1.23e+09
```

This is particularly useful in scientific computing, machine learning, and numerical analysis.

---

## 11. The `str.format()` Method

Before f-Strings became available in Python 3.6, developers frequently used the `format()` method.

It is still supported in modern Python.

### Syntax

```python
"Text {}".format(value)
```

### Example

```python
name = "Sivanarul"
age = 27

message = "My name is {} and my age is {}".format(name, age)

print(message)
```

**Output:**

```text
My name is Sivanarul and my age is 27
```

### Using Positional Indexes

```python
name = "Sivanarul"
age = 27

print("Name: {0}, Age: {1}".format(name, age))
```

**Output:**

```text
Name: Sivanarul, Age: 27
```

### Using Named Placeholders

```python
name = "Sivanarul"
salary = 41666.50

print("Name: {name}, Salary: {salary:.2f}".format(
    name=name,
    salary=salary
))
```

**Output:**

```text
Name: Sivanarul, Salary: 41666.50
```

---

## 12. Old-Style `%` Formatting

Python also supports an older string formatting technique using the `%` operator.

### Example

```python
name = "Sivanarul"
age = 27

print("Name: %s" % name)
print("Age: %d" % age)
```

**Output:**

```text
Name: Sivanarul
Age: 27
```

### Common Format Specifiers

| Specifier | Purpose |
|---|---|
| `%s` | String representation |
| `%d` | Integer |
| `%f` | Floating-point number |
| `%.2f` | Floating-point number with two decimal places |
| `%e` | Scientific notation |

### Example

```python
price = 99.567

print("Price: %.2f" % price)
```

**Output:**

```text
Price: 99.57
```

This method is still encountered in older Python codebases, but f-Strings are generally easier to read for new code.

---

## 13. Comparison of String Formatting Methods

| Method | Example | Usage |
|---|---|---|
| Concatenation | `"Hello " + name` | Basic string joining |
| `print()` arguments | `print("Hello", name)` | Simple output |
| f-Strings | `f"Hello {name}"` | Preferred modern formatting |
| `str.format()` | `"Hello {}".format(name)` | Existing and compatible code |
| `%` formatting | `"Hello %s" % name` | Legacy Python code |

### Recommendation

For new Python applications, prefer f-Strings when formatting values into strings.

---

## 14. Debugging with f-Strings

Python 3.8 introduced the f-string debug syntax using `=`.

It displays both the expression and its value.

### Example

```python
name = "Sivanarul"
age = 27

print(f"{name=}")
print(f"{age=}")
```

**Output:**

```text
name='Sivanarul'
age=27
```

### Example: Debugging an Expression

```python
num1 = 10
num2 = 20

print(f"{num1 + num2=}")
```

**Output:**

```text
num1 + num2=30
```

This feature is helpful when debugging variables and calculations.

Note: Debug f-Strings are useful during development, but avoid exposing sensitive values such as passwords, access tokens, or personal data in logs.

---

## 15. Practical Example: Employee Salary Report

Let's combine different formatting techniques in one practical example.

```python
employee_name = "Sivanarul"
employee_id = 42
basic_salary = 35000.50
bonus = 5000.75

total_salary = basic_salary + bonus

print("=" * 40)
print(f"{'EMPLOYEE SALARY REPORT':^40}")
print("=" * 40)

print(f"Employee Name : {employee_name}")
print(f"Employee ID   : {employee_id:05d}")
print(f"Basic Salary  : ₹{basic_salary:,.2f}")
print(f"Bonus         : ₹{bonus:,.2f}")
print("-" * 40)
print(f"Total Salary  : ₹{total_salary:,.2f}")
print("=" * 40)
```

**Output:**

```text
========================================
        EMPLOYEE SALARY REPORT
========================================
Employee Name : Sivanarul
Employee ID   : 00042
Basic Salary  : ₹35,000.50
Bonus         : ₹5,000.75
----------------------------------------
Total Salary  : ₹40,001.25
========================================
```

This example combines:

- f-Strings
- Decimal formatting
- Integer formatting
- Thousands separators
- Text alignment
- String repetition

---

## 16. Practical Example: AI Model Performance Report

Formatted output is also useful when displaying AI model evaluation results.

```python
model_name = "Random Forest"
accuracy = 0.9567
precision = 0.9425
recall = 0.9312
execution_time = 2.45678

print("=" * 45)
print(f"{'MODEL PERFORMANCE REPORT':^45}")
print("=" * 45)

print(f"Model Name       : {model_name}")
print(f"Accuracy         : {accuracy:.2%}")
print(f"Precision        : {precision:.2%}")
print(f"Recall           : {recall:.2%}")
print(f"Execution Time   : {execution_time:.3f} seconds")

print("=" * 45)
```

**Output:**

```text
=============================================
         MODEL PERFORMANCE REPORT
=============================================
Model Name       : Random Forest
Accuracy         : 95.67%
Precision        : 94.25%
Recall           : 93.12%
Execution Time   : 2.457 seconds
=============================================
```

In real FDE applications, the same information might be returned through an API, displayed in a dashboard, or recorded in structured logs.

---

## 17. Advanced Note: f-String Limitations and Safety

### 17.1 Curly Braces

If we want to display literal curly braces, we must escape them by doubling them.

```python
name = "Python"

print(f"{{name}}")
print(f"{{{name}}}")
```

**Output:**

```text
{name}
{Python}
```

### 17.2 Expressions and Python Versions

f-Strings were introduced in Python 3.6.

Some newer f-string capabilities were added in later versions.

For example:

- Debug syntax (`f"{value=}"`) was introduced in Python 3.8.
- Python 3.12 improved f-string expression parsing and removed several earlier restrictions.

### 17.3 Avoid Evaluating Untrusted Expressions

f-Strings evaluate Python expressions written directly in source code.

Never take arbitrary user input and pass it to `eval()` to generate dynamic f-Strings.

For example, this is unsafe:

```python
user_input = input("Enter an expression: ")

# Avoid:
# result = eval(user_input)
```

Use explicit validation and controlled formatting instead.

---

## 18. Common Mistakes

| Mistake | Explanation |
|---|---|
| Forgetting `f` before a string | Variables inside `{}` are not evaluated |
| Using parentheses instead of curly braces | f-Strings use `{}` for expressions |
| Confusing `.2f` with rounding the original variable | Formatting changes the displayed representation, not the original value |
| Using `%` as a percentage without understanding it | The `%` format specifier scales the value by 100 |
| Putting complex business logic inside an f-String | Makes code harder to read and maintain |
| Printing sensitive values | Can expose credentials or personal information |
| Assuming formatted output is numeric | The result of an f-String is always a string |

---

## 19. Practice Exercises

### Beginner Level

**Exercise 1: Personal Introduction**

Create variables for:

- Name
- Age
- City
- Profession

Display them using a single f-String.

**Exercise 2: Arithmetic Report**

Get two numbers and display:

- Addition
- Subtraction
- Multiplication
- Division

Use f-Strings for every output.

**Exercise 3: Decimal Formatting**

Given:

```python
price = 1234.56789
```

Display the price with:

- Two decimal places
- Three decimal places
- Thousands separator

### Intermediate Level

**Exercise 4: Employee Salary Slip**

Create a salary report containing:

- Employee name
- Employee ID
- Basic salary
- Bonus
- Total salary

Format the salary values with two decimal places and thousands separators.

**Exercise 5: Product Invoice**

Create a product invoice with:

- Product name
- Unit price
- Quantity
- Total amount

Display the invoice in a neatly aligned format.

**Exercise 6: Student Performance Report**

Display:

- Student name
- Subject
- Marks
- Maximum marks
- Percentage

Display the percentage using `.2%` formatting. Convert the marks ratio into a decimal before formatting it as a percentage.

### FDE-Oriented Practical Exercise

**Exercise 7: AI Model Evaluation Report**

Create a report for an AI model containing:

- Model name
- Accuracy
- Precision
- Recall
- F1-score
- Execution time

Requirements:

1. Display evaluation metrics as percentages.
2. Display execution time with three decimal places.
3. Align the report neatly.
4. Use f-Strings for all formatted output.

---

## 20. Quick Revision

| Concept | Syntax | Purpose |
|---|---|---|
| Basic f-String | `f"{name}"` | Insert variables |
| Expression | `f"{a + b}"` | Evaluate expressions |
| Decimal formatting | `f"{price:.2f}"` | Two decimal places |
| Integer formatting | `f"{number:05d}"` | Leading zeros |
| Percentage | `f"{value:.2%}"` | Percentage display |
| Thousands separator | `f"{number:,}"` | Readable large numbers |
| Left alignment | `f"{name:<15}"` | Left-align text |
| Right alignment | `f"{name:>15}"` | Right-align text |
| Center alignment | `f"{name:^15}"` | Center-align text |
| Scientific notation | `f"{number:.2e}"` | Scientific representation |
| Debug syntax | `f"{value=}"` | Display expression and value |
| `str.format()` | `"{}".format(value)` | Alternative formatting |
| `%` formatting | `"%s" % value` | Legacy formatting |

---

## 21. Self-Assessment Questions

1. What is an f-String?
2. Why do we use the `f` prefix?
3. What happens when we write `f"{10 + 20}"`?
4. What is the meaning of `.2f`?
5. What is the difference between `:5d` and `:05d`?
6. What does `:.2%` do?
7. What is the difference between `<`, `>` and `^`?
8. Does f-String formatting modify the original variable?
9. What is the difference between f-Strings and `str.format()`?
10. What is the purpose of the debug syntax `f"{variable=}"`?
11. Why should we avoid using `eval()` with untrusted user input?
12. Why are f-Strings useful when generating AI model performance reports?

---

## 22. Learning Outcome

After completing this topic, you should understand:

- How f-Strings work.
- How to insert variables and expressions into strings.
- How to control decimal precision.
- How to format integers and percentages.
- How to align text and format large numbers.
- How `str.format()` and `%` formatting work.
- How to generate readable reports.
- How formatted output helps in debugging and application development.

**Next Suggested Topic:** String Fundamentals in Python
