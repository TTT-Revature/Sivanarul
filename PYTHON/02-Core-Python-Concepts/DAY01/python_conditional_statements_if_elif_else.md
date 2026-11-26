
# Conditional Statements in Python (if, elif and else)

## 1. Introduction

In Python, conditional statements are used to execute different blocks of code depending on whether a condition is True or False.

In real-world applications, we constantly make decisions.

For example:

- If a user enters the correct password, allow login.
- If the payment is successful, confirm the order.
- If the payment fails, show an error.
- If a user has administrator privileges, allow access to the admin dashboard.

Python provides three main conditional keywords:

1. `if`
2. `elif`
3. `else`

---

# 2. The if Statement

## 2.1 What is an if Statement?

The `if` statement executes a block of code only when a given condition evaluates to True.

### Syntax

```python
if condition:
    # Code executes when condition is True
```

Important:
- The condition must be followed by a colon (`:`).
- The code inside the condition must be indented.
- Python uses indentation to identify the code block.

### Example

```python
age = 25

if age >= 18:
    print("You are eligible to vote")
```

Output:

```text
You are eligible to vote
```

Explanation:

1. The variable `age` contains `25`.
2. Python evaluates `age >= 18`.
3. The condition evaluates to `True`.
4. Therefore, Python executes the indented statement.

### Another Example

```python
temperature = 40

if temperature > 35:
    print("It is a hot day")

print("Program completed")
```

Output:

```text
It is a hot day
Program completed
```

Notice:

The second print statement is outside the `if` block, so it executes regardless of whether the condition is True or False.

---

# 3. The else Statement

## 3.1 What is an else Statement?

The `else` statement executes when the preceding `if` condition is False.

It provides an alternative execution path.

### Syntax

```python
if condition:
    # Executes when condition is True
else:
    # Executes when condition is False
```

### Example

```python
age = 16

if age >= 18:
    print("Eligible")
else:
    print("Not eligible")
```

Output:

```text
Not eligible
```

Explanation:

1. Python checks whether `age >= 18`.
2. The condition evaluates to False.
3. Python skips the `if` block.
4. Python executes the `else` block.

### Real-World Example: Login Validation

```python
password = "python123"
correct_password = "admin123"

if password == correct_password:
    print("Login successful")
else:
    print("Invalid password")
```

Output:

```text
Invalid password
```

---

# 4. The elif Statement

## 4.1 What is elif?

`elif` stands for "else if".

It allows us to check multiple conditions in sequence.

When the `if` condition is False, Python checks the next `elif` condition.

Python executes the first matching block and skips the remaining conditions.

### Syntax

```python
if condition1:
    # First condition
elif condition2:
    # Second condition
elif condition3:
    # Third condition
else:
    # Executes when all conditions are False
```

### Example

```python
marks = 75

if marks >= 90:
    print("Grade A")

elif marks >= 75:
    print("Grade B")

elif marks >= 50:
    print("Grade C")

else:
    print("Fail")
```

Output:

```text
Grade B
```

Explanation:

1. `marks >= 90` → False.
2. `marks >= 75` → True.
3. Python executes the Grade B block.
4. The remaining conditions are skipped.

Important:

Python does not execute every matching `elif` condition. It executes only the first matching branch.

---

# 5. Difference Between if, elif and else

| Keyword | Purpose | Condition |
|---|---|---|
| `if` | Checks the first condition | Required |
| `elif` | Checks additional conditions | Required |
| `else` | Executes when no previous condition matches | No condition |

Example:

```python
age = 25

if age < 18:
    print("Minor")

elif age >= 18 and age < 60:
    print("Adult")

else:
    print("Senior citizen")
```

Output:

```text
Adult
```

---

# 6. Understanding Execution Flow

Consider the following example:

```python
number = 10

if number > 20:
    print("Greater than 20")

elif number > 5:
    print("Greater than 5")

else:
    print("Less than or equal to 5")
```

Output:

```text
Greater than 5
```

### Execution Flow

```text
              Start
                |
                v
        number > 20 ?
           /       \
        True       False
         |            |
         v            v
   Print greater   number > 5 ?
      than 20       /      \
                 True      False
                  |          |
                  v          v
             Print > 5    Print <= 5
                  \          /
                   \        /
                    End
```

The program checks conditions from top to bottom.

Once a matching condition is found, the corresponding block executes and the remaining branches are skipped.

---

# 7. Multiple Conditions Inside if Statements

We can combine multiple conditions using logical operators.

Common logical operators:

- `and`
- `or`
- `not`

## 7.1 Using AND

Both conditions must be truthy.

```python
age = 25
salary = 40000

if age >= 18 and salary >= 30000:
    print("Eligible for the program")
else:
    print("Not eligible")
```

Output:

```text
Eligible for the program
```

## 7.2 Using OR

At least one condition must be truthy.

```python
is_admin = False
is_manager = True

if is_admin or is_manager:
    print("Access granted")
else:
    print("Access denied")
```

Output:

```text
Access granted
```

## 7.3 Using NOT

The `not` operator reverses a condition's truth value.

```python
is_blocked = False

if not is_blocked:
    print("User can continue")
else:
    print("User is blocked")
```

Output:

```text
User can continue
```

---

# 8. Nested if Statements

## 8.1 What is a Nested if?

A nested `if` means placing one conditional statement inside another conditional block.

It is useful when one decision depends on another decision.

### Example

```python
age = 25
has_id = True

if age >= 18:
    print("Age requirement satisfied")

    if has_id:
        print("Identity verified")
    else:
        print("Identity document required")

else:
    print("Age requirement not satisfied")
```

Output:

```text
Age requirement satisfied
Identity verified
```

### Real-World Example: Application Login

```python
username = "admin"
password = "admin123"
is_active = True

if username == "admin":
    if password == "admin123":
        if is_active:
            print("Login successful")
        else:
            print("Account is inactive")
    else:
        print("Incorrect password")
else:
    print("User not found")
```

Output:

```text
Login successful
```

Explanation:

1. Check whether the username exists.
2. Check whether the password is correct.
3. Check whether the account is active.
4. Execute the successful login path only when all checks pass.

Note: This is a learning example. Real authentication systems should use securely hashed passwords and established authentication mechanisms rather than hardcoded credentials.

---

# 9. Multiple if Statements vs if-elif-else

This is an important difference.

## 9.1 Multiple Independent if Statements

Each `if` condition is evaluated independently.

```python
number = 10

if number > 0:
    print("Positive")

if number > 5:
    print("Greater than 5")

if number < 20:
    print("Less than 20")
```

Output:

```text
Positive
Greater than 5
Less than 20
```

All three conditions are True, so all three blocks execute.

## 9.2 Using if-elif-else

```python
number = 10

if number > 0:
    print("Positive")

elif number > 5:
    print("Greater than 5")

elif number < 20:
    print("Less than 20")

else:
    print("No condition matched")
```

Output:

```text
Positive
```

Why?

The first condition is True.

Python executes that block and skips all remaining `elif` and `else` branches.

### Difference Summary

| Multiple if | if-elif-else |
|---|---|
| Conditions are evaluated independently | Conditions are checked in sequence |
| Multiple blocks can execute | Only one branch executes |
| Useful for independent checks | Useful for mutually exclusive decisions |

---

# 10. Conditional Statements with User Input

The `input()` function allows users to provide information while a program is running.

Remember: `input()` returns a string.

If you want to perform numeric comparisons, convert the input into the required numeric type.

### Example: Age Validation

```python
age = int(input("Enter your age: "))

if age >= 18:
    print("You are an adult")
else:
    print("You are a minor")
```

Example execution:

```text
Enter your age: 22
You are an adult
```

### Example: Grade Calculation

```python
marks = int(input("Enter your marks: "))

if marks < 0 or marks > 100:
    print("Invalid marks")

elif marks >= 90:
    print("Grade A")

elif marks >= 75:
    print("Grade B")

elif marks >= 50:
    print("Grade C")

else:
    print("Fail")
```

Example execution:

```text
Enter your marks: 85
Grade B
```

The first condition validates the input range before calculating the grade.

Note: `int()` raises a `ValueError` if the user enters non-numeric text. Robust applications should handle that error using exception handling.

---

# 11. Conditional Expressions (Ternary Operator)

Python also supports a shorter way to write simple conditional assignments.

It is called a conditional expression or ternary expression.

### Syntax

```python
value_if_true if condition else value_if_false
```

### Example

```python
age = 20

status = "Adult" if age >= 18 else "Minor"

print(status)
```

Output:

```text
Adult
```

This is equivalent to:

```python
age = 20

if age >= 18:
    status = "Adult"
else:
    status = "Minor"

print(status)
```

Use conditional expressions for simple decisions. For complicated business logic, normal `if-elif-else` statements are usually easier to read.

---

# 12. Common Mistakes

## Mistake 1: Forgetting the Colon

Incorrect:

```python
if age >= 18
    print("Adult")
```

Correct:

```python
if age >= 18:
    print("Adult")
```

## Mistake 2: Incorrect Indentation

Incorrect:

```python
if age >= 18:
print("Adult")
```

Correct:

```python
if age >= 18:
    print("Adult")
```

Python uses indentation to identify code blocks.

## Mistake 3: Using Assignment Instead of Comparison

Incorrect:

```python
if age = 18:
    print("Adult")
```

Correct:

```python
if age == 18:
    print("Adult")
```

- `=` assigns a value.
- `==` compares two values.

## Mistake 4: Incorrect Condition Ordering

Incorrect:

```python
marks = 95

if marks >= 50:
    print("Grade C")

elif marks >= 90:
    print("Grade A")
```

Output:

```text
Grade C
```

Why?

The first condition is already True. Python never reaches the second condition.

Correct:

```python
marks = 95

if marks >= 90:
    print("Grade A")

elif marks >= 50:
    print("Grade C")
```

Output:

```text
Grade A
```

Always arrange overlapping conditions carefully, usually from the most restrictive or highest threshold to the least restrictive.

## Mistake 5: Using Multiple else Blocks at the Same Level

Incorrect:

```python
if age >= 18:
    print("Adult")
else:
    print("Minor")
else:
    print("Unknown")
```

A single `if` statement can have only one `else` branch at that level.

Use `elif` for additional conditions.

---

# 13. Practical FDE Use Cases

Conditional statements are used in almost every application.

## Use Case 1: API Request Validation

```python
request_data = {
    "username": "Arun",
    "email": "arun@example.com"
}

if "username" not in request_data:
    print("Username is required")

elif "email" not in request_data:
    print("Email is required")

else:
    print("Request data is valid")
```

## Use Case 2: Payment Processing

```python
payment_status = "success"

if payment_status == "success":
    print("Order confirmed")

elif payment_status == "pending":
    print("Payment is processing")

elif payment_status == "failed":
    print("Payment failed")

else:
    print("Unknown payment status")
```

## Use Case 3: User Role Validation

```python
user_role = "manager"

if user_role == "admin":
    print("Admin dashboard")

elif user_role == "manager":
    print("Manager dashboard")

elif user_role == "developer":
    print("Developer dashboard")

else:
    print("Access restricted")
```

## Use Case 4: AI Application Response Handling

Imagine an AI application that checks the result returned by an AI model.

```python
response = {
    "status": "success",
    "answer": "Python is a programming language"
}

if response["status"] == "success":
    print(response["answer"])

elif response["status"] == "error":
    print("Unable to generate an answer")

else:
    print("Unknown response status")
```

This type of logic is useful when integrating external AI services, APIs, and automated workflows.

---

# 14. Quick Revision

| Concept | Purpose |
|---|---|
| `if` | Executes code when a condition is True |
| `elif` | Checks another condition when earlier conditions are False |
| `else` | Executes when no preceding condition matches |
| Nested if | Places one conditional block inside another |
| Multiple if | Evaluates independent conditions |
| Ternary expression | Writes a simple conditional assignment in one expression |
| `and` | Requires both operands to be truthy |
| `or` | Requires at least one operand to be truthy |
| `not` | Reverses a truth value |

Important rules:

- A condition must be followed by a colon.
- Indentation defines the code block.
- `elif` can be used multiple times.
- `else` is optional.
- Only one branch of an `if-elif-else` chain executes.
- Independent `if` statements can execute multiple blocks.
- Conditions are checked from top to bottom.
- Correct condition ordering is important.

---

# 15. Practice Exercises

Try solving these exercises independently.

## Exercise 1: Age Classification

Write a program that checks a person's age.

Requirements:

- Below 13: Child
- 13 to 19: Teenager
- 20 to 59: Adult
- 60 and above: Senior citizen

## Exercise 2: Number Classification

Write a program to identify whether a number is:

- Positive
- Negative
- Zero

## Exercise 3: Even or Odd

Write a program to check whether a number is even or odd.

Hint: Use the modulus operator `%`.

## Exercise 4: Grade Calculator

Create a program that accepts marks from the user.

Requirements:

- 90–100: Grade A
- 75–89: Grade B
- 50–74: Grade C
- 0–49: Fail
- Outside 0–100: Invalid marks

## Exercise 5: Login Validation

Create a simple login program.

Requirements:

- Check username.
- Check password.
- Check whether the account is active.
- Display the appropriate message.

## Exercise 6: FDE Business Rule

Create a program for an online service.

Requirements:

- The user must be active.
- The user must have a valid subscription.
- The requested feature must be available.
- If all conditions are satisfied, allow access.
- Otherwise, display an appropriate message.

Use:
- `if`
- `elif`
- `else`
- `and`
- `in`

---

# 16. Self-Assessment

Before moving to the next topic, make sure you can explain:

1. What is a conditional statement?
2. What is the difference between `if` and `elif`?
3. Why do we use `else`?
4. Can we use multiple `elif` statements?
5. Can we write multiple independent `if` statements?
6. What is a nested `if` statement?
7. What happens when the first `if` condition is True?
8. Why does condition ordering matter?
9. What is a ternary expression?
10. How are conditional statements useful in API development?

---

# 17. Connection to Forward Deployed Engineering

As a Forward Deployed Engineer, you will use conditional statements when:

- Validating incoming API requests.
- Implementing business requirements.
- Checking authentication and authorization.
- Handling payment responses.
- Integrating third-party services.
- Managing AI model responses.
- Building automated workflows.
- Handling different application states.

For example, when a customer explains a business requirement such as:

"Only active premium users should be allowed to access the analytics feature."

You should be able to translate that requirement into Python conditions.

That ability to convert business requirements into reliable application logic is an important FDE skill.

---


