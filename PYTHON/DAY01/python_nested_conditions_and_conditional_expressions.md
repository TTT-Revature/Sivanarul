
# Nested Conditions and Conditional Expressions in Python

## 1. Introduction

Python allows us to make decisions using conditional statements.

Sometimes, a single condition is not enough to solve a problem.

For example, consider an application login process:

1. First, check whether the username exists.
2. If the username exists, check whether the password is correct.
3. If the password is correct, check whether the account is active.
4. If all checks pass, allow the user to log in.

Here, one condition depends on the result of another condition.

Python supports this through:

1. Nested conditional statements.
2. Conditional expressions (ternary operators).

---

# 2. Nested Conditions

## 2.1 What Are Nested Conditions?

A nested condition means placing one conditional statement inside another conditional statement.

In simple terms:

An `if` statement inside another `if`, `elif`, or `else` block is called a nested conditional statement.

### Syntax

```python
if condition1:
    if condition2:
        # Executes when both conditions are True
    else:
        # Executes when condition1 is True
        # and condition2 is False
else:
    # Executes when condition1 is False
```

Important:
- Inner conditions are evaluated only when execution reaches their block.
- Each nested block must have correct indentation.
- Nested conditions can contain `if`, `elif`, and `else`.

## 2.2 Basic Example

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

Explanation:

1. Python checks whether `age >= 18`.
2. The condition is True.
3. Python enters the outer `if` block.
4. It checks the inner condition `has_id`.
5. Since `has_id` is True, it prints "Identity verified".

## 2.3 Nested if with Multiple Levels

We can place multiple conditions inside one another.

```python
username = "admin"
password = "admin123"
is_active = True

if username == "admin":
    print("Username verified")

    if password == "admin123":
        print("Password verified")

        if is_active:
            print("Login successful")
        else:
            print("Account is inactive")

    else:
        print("Incorrect password")

else:
    print("Invalid username")
```

Output:

```text
Username verified
Password verified
Login successful
```

Execution flow:

```text
Check username
      |
      v
Username correct?
   /       \
 Yes        No
  |          |
  v          v
Check      Invalid
password   username
  |
  v
Password correct?
   /       \
 Yes        No
  |          |
  v          v
Check      Incorrect
account    password
status
  |
  v
Account active?
   /       \
 Yes        No
  |          |
  v          v
Login      Account
successful inactive
```

This is a simplified educational example. Real applications should use secure password hashing and established authentication mechanisms.

---

# 3. Nested Conditions with elif

Nested conditions can also contain `elif` statements.

### Example: Employee Role Validation

```python
department = "IT"
role = "developer"

if department == "IT":

    if role == "developer":
        print("Developer access")

    elif role == "tester":
        print("Testing access")

    else:
        print("General IT access")

else:
    print("Department not supported")
```

Output:

```text
Developer access
```

Explanation:

1. Python checks the department.
2. Since the department is IT, it enters the outer block.
3. It checks the employee's role.
4. The role is developer.
5. The corresponding block executes.

---

# 4. Nested Conditions vs Multiple Conditions

These two approaches can sometimes solve the same problem, but their structure is different.

## 4.1 Using Nested Conditions

```python
age = 25
has_id = True

if age >= 18:

    if has_id:
        print("Access granted")
    else:
        print("Identity verification required")

else:
    print("Age requirement not satisfied")
```

## 4.2 Using Logical Operators

```python
age = 25
has_id = True

if age >= 18 and has_id:
    print("Access granted")
else:
    print("Access denied")
```

### Difference

| Nested Conditions | Logical Conditions |
|---|---|
| One condition is checked inside another block | Multiple conditions are combined in one expression |
| Supports different actions at each decision level | Often simpler for straightforward combined checks |
| Useful for dependent decisions | Useful when all conditions must be satisfied |
| Can become deeply nested | Can become difficult to read if expressions are too complex |

### When Should We Use Each?

Use nested conditions when:
- One decision depends on another decision.
- Different messages or actions are required at each level.
- The application workflow has multiple stages.

Use logical operators when:
- Several conditions must be checked together.
- The conditions lead to the same action.
- The combined expression remains readable.

---

# 5. Conditional Expressions

## 5.1 What Is a Conditional Expression?

A conditional expression allows us to write a simple decision in a single line.

It is also commonly called the ternary operator.

Python uses the following structure:

```python
value_if_true if condition else value_if_false
```

It evaluates the condition and returns one of two expressions.

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

Explanation:

1. Python evaluates `age >= 18`.
2. The condition is True.
3. Python selects `"Adult"`.
4. The selected value is assigned to `status`.

## 5.2 Normal if-else vs Conditional Expression

### Using Normal if-else

```python
age = 16

if age >= 18:
    status = "Adult"
else:
    status = "Minor"

print(status)
```

Output:

```text
Minor
```

### Using Conditional Expression

```python
age = 16

status = "Adult" if age >= 18 else "Minor"

print(status)
```

Output:

```text
Minor
```

Both approaches produce the same result.

The conditional expression is shorter, but normal `if-else` is often easier to read when the logic becomes complex.

---

# 6. Conditional Expressions with Different Data Types

A conditional expression can return values of different data types.

### Example 1: Integer Values

```python
number = 10

result = 100 if number > 0 else -100

print(result)
```

Output:

```text
100
```

### Example 2: Boolean Values

```python
age = 20

is_adult = True if age >= 18 else False

print(is_adult)
```

Output:

```text
True
```

A simpler and more direct approach is:

```python
is_adult = age >= 18
```

### Example 3: List Values

```python
is_active = True

result = ["Python", "SQL"] if is_active else []

print(result)
```

Output:

```text
['Python', 'SQL']
```

### Example 4: None as a Default Value

```python
user_input = ""

username = user_input if user_input else None

print(username)
```

Output:

```text
None
```

This checks whether the input is truthy. An empty string is falsy, so the result is `None`.

---

# 7. Nested Conditional Expressions

A conditional expression can contain another conditional expression.

This is sometimes called a nested ternary expression.

### Example: Grade Classification

```python
marks = 85

grade = (
    "A" if marks >= 90
    else "B" if marks >= 75
    else "C" if marks >= 50
    else "Fail"
)

print(grade)
```

Output:

```text
B
```

Explanation:

1. Is marks greater than or equal to 90? No.
2. Is marks greater than or equal to 75? Yes.
3. Therefore, the result is `"B"`.

Equivalent normal conditional statements:

```python
marks = 85

if marks >= 90:
    grade = "A"

elif marks >= 75:
    grade = "B"

elif marks >= 50:
    grade = "C"

else:
    grade = "Fail"

print(grade)
```

Recommendation:

Avoid deeply nested conditional expressions. They can make code difficult to understand and debug.

For multiple business rules, prefer normal `if-elif-else` statements.

---

# 8. Conditional Expressions with Logical Operators

We can combine conditional expressions with logical operators.

### Example: Access Validation

```python
age = 25
is_active = True

message = (
    "Access granted"
    if age >= 18 and is_active
    else "Access denied"
)

print(message)
```

Output:

```text
Access granted
```

Explanation:

Both conditions must be satisfied:
- Age must be at least 18.
- Account must be active.

If both conditions are True, the expression returns `"Access granted"`.

Otherwise, it returns `"Access denied"`.

---

# 9. Practical FDE Use Cases

Nested conditions and conditional expressions are useful when translating business requirements into application logic.

## Use Case 1: Subscription Validation

Business requirement:

Only active users with a premium subscription can access a premium feature.

```python
user = {
    "name": "Arun",
    "is_active": True,
    "subscription": "premium"
}

if user is not None:

    if user["is_active"]:

        if user["subscription"] == "premium":
            print("Premium feature available")
        else:
            print("Upgrade your subscription")

    else:
        print("Account is inactive")

else:
    print("User not found")
```

Output:

```text
Premium feature available
```

## Use Case 2: API Response Message

```python
response_status = 200

message = (
    "Request successful"
    if response_status == 200
    else "Request failed"
)

print(message)
```

Output:

```text
Request successful
```

## Use Case 3: AI Model Response Handling

Imagine an AI application that receives a model response.

```python
response = {
    "status": "success",
    "answer": "Python is a programming language"
}

if response["status"] == "success":

    if response["answer"]:
        print(response["answer"])
    else:
        print("The model returned an empty answer")

else:
    print("Unable to generate a response")
```

Output:

```text
Python is a programming language
```

This structure can be used when integrating AI model APIs and handling different response states.

## Use Case 4: Feature Access

```python
user_role = "admin"
is_active = True

access_message = (
    "Access granted"
    if user_role == "admin" and is_active
    else "Access denied"
)

print(access_message)
```

Output:

```text
Access granted
```

Note: These examples demonstrate business logic only. Production authorization must be enforced on the server using trusted identity and permission data.

---

# 10. Common Mistakes

## Mistake 1: Incorrect Indentation

Incorrect:

```python
age = 20

if age >= 18:
if age < 60:
    print("Adult")
```

Correct:

```python
age = 20

if age >= 18:
    if age < 60:
        print("Adult")
```

Each nested block requires another indentation level.

## Mistake 2: Forgetting the else Part of a Conditional Expression

Incorrect:

```python
status = "Adult" if age >= 18
```

Correct:

```python
status = "Adult" if age >= 18 else "Minor"
```

A conditional expression requires both the true and false alternatives.

## Mistake 3: Using Nested Ternary Expressions for Complex Logic

Difficult to read:

```python
result = "A" if marks >= 90 else "B" if marks >= 75 else "C" if marks >= 50 else "Fail"
```

More readable:

```python
if marks >= 90:
    result = "A"
elif marks >= 75:
    result = "B"
elif marks >= 50:
    result = "C"
else:
    result = "Fail"
```

## Mistake 4: Confusing a Conditional Expression with a Normal if Statement

Normal conditional statement:

```python
if age >= 18:
    print("Adult")
```

Conditional expression:

```python
status = "Adult" if age >= 18 else "Minor"
```

The first controls which statements execute. The second evaluates to a value that can be assigned or used in another expression.

## Mistake 5: Accessing Data Before Checking Whether It Exists

Unsafe:

```python
user = None

if user["name"]:
    print(user["name"])
```

This raises an error because `user` is `None`.

Safer:

```python
user = None

if user is not None:
    if user["name"]:
        print(user["name"])
else:
    print("User not found")
```

For production applications, also validate that the expected dictionary key exists before accessing it.

---

# 11. Quick Revision

| Concept | Meaning |
|---|---|
| Nested condition | A conditional statement inside another conditional block |
| Nested if | An `if` statement inside another block |
| Nested elif | An `elif` statement inside an outer conditional block |
| Conditional expression | A compact expression that selects one of two values |
| Ternary expression | Another name for a conditional expression |
| Nested ternary | A conditional expression inside another conditional expression |

### Important Syntax

Nested condition:

```python
if condition1:
    if condition2:
        print("Both conditions satisfied")
```

Conditional expression:

```python
result = "Yes" if condition else "No"
```

Nested conditional expression:

```python
result = "A" if condition1 else "B" if condition2 else "C"
```

---

# 12. Practice Exercises

Try solving these exercises independently.

## Exercise 1: Nested Age Validation

Create a program with the following requirements:

- Check whether the user is at least 18.
- If the user is an adult, check whether they have a valid identity document.
- If both conditions are satisfied, print "Registration allowed".
- Otherwise, print an appropriate message.

Use nested `if` statements.

## Exercise 2: Employee Access

Create an employee access system.

Requirements:

- Check whether the employee belongs to the IT department.
- If yes, check the employee role.
- Developer: Developer dashboard.
- Tester: Testing dashboard.
- Other roles: General IT access.
- Other departments: Access unavailable.

Use nested `if`, `elif`, and `else`.

## Exercise 3: Conditional Expression

Write a program that checks whether a number is even or odd using a conditional expression.

Expected format:

```python
result = "Even" if condition else "Odd"
```

## Exercise 4: Grade Calculation

Write a program using a conditional expression to classify marks:

- 90 and above: A
- 75 and above: B
- 50 and above: C
- Below 50: Fail

Then rewrite the same program using `if-elif-else`.

## Exercise 5: Subscription Validation

Create a program with these conditions:

- User must exist.
- Account must be active.
- Subscription must be premium.

Use nested conditions to determine whether the user can access a premium feature.

## Exercise 6: FDE Business Requirement

Build a simple feature-access decision system.

Input:

```python
user_role = "admin"
is_active = True
feature_name = "analytics"
enabled_features = ["analytics", "reports"]
```

Requirements:

1. Check whether the account is active.
2. Check whether the role is admin or manager.
3. Check whether the requested feature exists in the enabled features.
4. Grant access only when all requirements are satisfied.

Use nested conditions and membership operators.

---

# 13. Self-Assessment

Before moving to the next topic, make sure you can explain:

1. What are nested conditional statements?
2. Can an `if` statement contain another `if` statement?
3. Can we use `elif` inside a nested conditional?
4. What is a conditional expression?
5. Why is a conditional expression also called a ternary expression?
6. What is the difference between a normal `if-else` and a conditional expression?
7. Can we nest conditional expressions?
8. When should we avoid nested ternary expressions?
9. How do nested conditions help implement business workflows?
10. When should we use logical operators instead of nested conditions?

---

# 14. Connection to Forward Deployed Engineering

Forward Deployed Engineers frequently translate business requirements into application workflows.

Consider this requirement:

"Only active premium customers with analytics enabled should access the analytics dashboard."

You must convert that requirement into executable application logic.

This requires understanding:

- Conditional statements.
- Nested conditions.
- Logical operators.
- Membership operators.
- Data validation.
- Application states.

These concepts form the foundation for developing API endpoints, integrating external services, and implementing business workflows.

---

