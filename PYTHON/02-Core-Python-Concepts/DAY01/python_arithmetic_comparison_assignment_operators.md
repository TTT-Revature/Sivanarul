
# Python Arithmetic, Comparison and Assignment Operators

## 1. Introduction

Operators are special symbols or keywords used to perform operations on values and variables.

In Python, operators help us perform calculations, compare values, assign data, and build logical conditions.

Example:

```python
a = 10
b = 20

result = a + b

print(result)
```

Output:

```text
30
```

In this example:

- `a` and `b` are operands.
- `+` is an operator.
- `result` stores the result of the operation.

Python provides several categories of operators.

In this chapter, we will focus on:

1. Arithmetic Operators
2. Comparison Operators
3. Assignment Operators

---

# 2. Arithmetic Operators

Arithmetic operators are used to perform mathematical calculations.

Python supports the following arithmetic operators:

| Operator | Name | Description |
|---|---|---|
| `+` | Addition | Adds two values |
| `-` | Subtraction | Subtracts one value from another |
| `*` | Multiplication | Multiplies two values |
| `/` | Division | Performs division |
| `//` | Floor Division | Divides and rounds down to the nearest integer |
| `%` | Modulus | Returns the remainder |
| `**` | Exponentiation | Calculates power |

## 2.1 Addition (+)

The addition operator adds two values.

Example:

```python
a = 10
b = 20

result = a + b

print(result)
```

Output:

```text
30
```

Real-world example:

```python
product_price = 500
delivery_charge = 50

total_amount = product_price + delivery_charge

print(total_amount)
```

Output:

```text
550
```

## 2.2 Subtraction (-)

The subtraction operator subtracts one value from another.

Example:

```python
a = 50
b = 20

result = a - b

print(result)
```

Output:

```text
30
```

Real-world example:

```python
account_balance = 5000
withdrawal = 1500

remaining_balance = account_balance - withdrawal

print(remaining_balance)
```

Output:

```text
3500
```

## 2.3 Multiplication (*)

The multiplication operator multiplies two values.

Example:

```python
a = 10
b = 5

result = a * b

print(result)
```

Output:

```text
50
```

Real-world example:

```python
product_price = 250
quantity = 4

total_amount = product_price * quantity

print(total_amount)
```

Output:

```text
1000
```

## 2.4 Division (/)

The division operator divides one value by another.

Example:

```python
a = 20
b = 4

result = a / b

print(result)
print(type(result))
```

Output:

```text
5.0
<class 'float'>
```

Important:

The `/` operator produces a floating-point result for ordinary numeric operands, even when the division has no fractional remainder.

Example:

```python
print(10 / 2)
```

Output:

```text
5.0
```

### Division by Zero

```python
a = 10
b = 0

result = a / b
```

Output:

```text
ZeroDivisionError
```

Python does not allow division by zero.

## 2.5 Floor Division (//)

Floor division divides two numbers and rounds the result down to the nearest integer.

Example:

```python
a = 17
b = 5

result = a // b

print(result)
```

Output:

```text
3
```

Explanation:

```text
17 / 5 = 3.4

17 // 5 = 3
```

### Important: Negative Numbers

Floor division rounds towards negative infinity, not towards zero.

Example:

```python
print(7 // 2)
print(-7 // 2)
```

Output:

```text
3
-4
```

Explanation:

```text
7 / 2 = 3.5

-7 / 2 = -3.5
```

The floor of `-3.5` is `-4`.

## 2.6 Modulus (%)

The modulus operator returns the remainder after division.

Example:

```python
a = 17
b = 5

result = a % b

print(result)
```

Output:

```text
2
```

Explanation:

```text
17 / 5

Quotient = 3
Remainder = 2
```

### Real-World Example: Checking Even or Odd

```python
number = 10

if number % 2 == 0:
    print("Even number")
else:
    print("Odd number")
```

Output:

```text
Even number
```

Why?

- If a number divided by 2 produces a remainder of 0, it is even.
- Otherwise, it is odd.

### Another Example: Finding the Remainder

```python
print(10 % 3)
print(15 % 4)
print(20 % 5)
```

Output:

```text
1
3
0
```

Important: In Python, the remainder follows the sign of the divisor.

Example:

```python
print(-7 % 2)
```

Output:

```text
1
```

## 2.7 Exponentiation (**)

The exponentiation operator calculates the power of a number.

Example:

```python
a = 2
b = 3

result = a ** b

print(result)
```

Output:

```text
8
```

Explanation:

```text
2 ** 3

2 × 2 × 2 = 8
```

### Real-World Example: Square of a Number

```python
number = 5

square = number ** 2

print(square)
```

Output:

```text
25
```

### Example: Cube of a Number

```python
number = 3

cube = number ** 3

print(cube)
```

Output:

```text
27
```

---

# 3. Arithmetic Operators Summary

```python
a = 17
b = 5

print("Addition:", a + b)
print("Subtraction:", a - b)
print("Multiplication:", a * b)
print("Division:", a / b)
print("Floor Division:", a // b)
print("Modulus:", a % b)
print("Exponentiation:", a ** b)
```

Output:

```text
Addition: 22
Subtraction: 12
Multiplication: 85
Division: 3.4
Floor Division: 3
Modulus: 2
Exponentiation: 1419857
```

---

# 4. Comparison Operators

Comparison operators are used to compare two values.

The result of a comparison is a Boolean value:

- `True`
- `False`

Python provides the following comparison operators:

| Operator | Name | Description |
|---|---|---|
| `==` | Equal to | Checks whether two values are equal |
| `!=` | Not equal to | Checks whether two values are different |
| `>` | Greater than | Checks whether the left value is greater |
| `<` | Less than | Checks whether the left value is smaller |
| `>=` | Greater than or equal to | Checks whether the left value is greater than or equal |
| `<=` | Less than or equal to | Checks whether the left value is smaller than or equal |

## 4.1 Equal To (==)

Checks whether two values are equal.

Example:

```python
a = 10
b = 10

print(a == b)
```

Output:

```text
True
```

Another example:

```python
username = "admin"

print(username == "admin")
```

Output:

```text
True
```

## 4.2 Not Equal To (!=)

Checks whether two values are different.

Example:

```python
a = 10
b = 20

print(a != b)
```

Output:

```text
True
```

Another example:

```python
password = "python123"

print(password != "admin123")
```

Output:

```text
True
```

## 4.3 Greater Than (>)

Checks whether the left value is greater than the right value.

Example:

```python
a = 50
b = 30

print(a > b)
```

Output:

```text
True
```

## 4.4 Less Than (<)

Checks whether the left value is smaller than the right value.

Example:

```python
a = 10
b = 20

print(a < b)
```

Output:

```text
True
```

## 4.5 Greater Than or Equal To (>=)

Checks whether the left value is greater than or equal to the right value.

Example:

```python
age = 18

print(age >= 18)
```

Output:

```text
True
```

Real-world example:

```python
account_balance = 5000
minimum_balance = 1000

print(account_balance >= minimum_balance)
```

Output:

```text
True
```

## 4.6 Less Than or Equal To (<=)

Checks whether the left value is smaller than or equal to the right value.

Example:

```python
age = 17

print(age <= 18)
```

Output:

```text
True
```

---

# 5. Practical Example: Employee Eligibility

Imagine an application that checks whether an employee is eligible for a particular benefit.

```python
employee_age = 25
minimum_age = 18

if employee_age >= minimum_age:
    print("Employee is eligible")
else:
    print("Employee is not eligible")
```

Output:

```text
Employee is eligible
```

Here:

- `>=` compares the employee's age with the minimum age.
- The comparison produces a Boolean result.
- The `if` statement uses that result to decide which block to execute.

---

# 6. Comparison Operators Summary

```python
a = 10
b = 20

print(a == b)
print(a != b)
print(a > b)
print(a < b)
print(a >= b)
print(a <= b)
```

Output:

```text
False
True
False
True
False
True
```

### Important Difference: = vs ==

These two operators have different purposes.

Assignment operator:

```python
age = 25
```

This assigns the value `25` to the variable `age`.

Comparison operator:

```python
age == 25
```

This checks whether the value of `age` is equal to `25`.

Do not confuse assignment with comparison.

---

# 7. Assignment Operators

Assignment operators are used to assign values to variables.

The basic assignment operator is:

```python
=
```

Python also provides compound assignment operators that combine an arithmetic operation with assignment.

| Operator | Example | Equivalent Expression |
|---|---|---|
| `=` | `a = 10` | Assigns 10 to a |
| `+=` | `a += 5` | `a = a + 5` |
| `-=` | `a -= 5` | `a = a - 5` |
| `*=` | `a *= 5` | `a = a * 5` |
| `/=` | `a /= 5` | `a = a / 5` |
| `//=` | `a //= 5` | `a = a // 5` |
| `%=` | `a %= 5` | `a = a % 5` |
| `**=` | `a **= 5` | `a = a ** 5` |

## 7.1 Basic Assignment (=)

The assignment operator assigns a value to a variable.

Example:

```python
name = "Python"
age = 25

print(name)
print(age)
```

Output:

```text
Python
25
```

## 7.2 Addition Assignment (+=)

Adds a value to the existing variable and assigns the result back.

Example:

```python
number = 10

number += 5

print(number)
```

Output:

```text
15
```

Equivalent expression:

```python
number = number + 5
```

### Real-World Example: Account Deposit

```python
balance = 5000

deposit = 2000

balance += deposit

print(balance)
```

Output:

```text
7000
```

## 7.3 Subtraction Assignment (-=)

Subtracts a value from the existing variable.

Example:

```python
balance = 10000

balance -= 2000

print(balance)
```

Output:

```text
8000
```

## 7.4 Multiplication Assignment (*=)

Multiplies the existing value and assigns the result.

Example:

```python
number = 10

number *= 3

print(number)
```

Output:

```text
30
```

## 7.5 Division Assignment (/=)

Divides the existing value and assigns the result.

Example:

```python
number = 20

number /= 4

print(number)
```

Output:

```text
5.0
```

Remember: `/=` produces a floating-point result for ordinary numeric operands.

## 7.6 Floor Division Assignment (//=)

Performs floor division and assigns the result.

Example:

```python
number = 17

number //= 5

print(number)
```

Output:

```text
3
```

## 7.7 Modulus Assignment (%=)

Calculates the remainder and assigns the result.

Example:

```python
number = 17

number %= 5

print(number)
```

Output:

```text
2
```

## 7.8 Exponentiation Assignment (**=)

Calculates the power and assigns the result.

Example:

```python
number = 2

number **= 3

print(number)
```

Output:

```text
8
```

---

# 8. Practical Example: Shopping Cart

Let's build a simple shopping cart calculation using arithmetic and assignment operators.

```python
cart_total = 0

product_1 = 500
product_2 = 300
product_3 = 200

cart_total += product_1
cart_total += product_2
cart_total += product_3

print("Cart Total:", cart_total)
```

Output:

```text
Cart Total: 1000
```

Now apply a discount:

```python
discount = 100

cart_total -= discount

print("Final Amount:", cart_total)
```

Output:

```text
Final Amount: 900
```

This demonstrates how assignment operators can update a variable as calculations progress.

---

# 9. Chained Comparisons

Python allows multiple comparisons in a single expression.

Example:

```python
age = 25

print(18 <= age <= 60)
```

Output:

```text
True
```

This is equivalent to:

```python
print(18 <= age and age <= 60)
```

Another example:

```python
marks = 75

if 50 <= marks <= 100:
    print("Valid marks")
```

Output:

```text
Valid marks
```

Chained comparisons are useful when checking ranges.

---

# 10. Operator Precedence

When an expression contains multiple operators, Python follows operator precedence rules.

Example:

```python
result = 10 + 5 * 2

print(result)
```

Output:

```text
20
```

Why?

Multiplication is evaluated before addition.

```text
10 + 5 * 2

10 + 10

20
```

### Common Arithmetic Precedence

From higher precedence to lower precedence:

| Priority | Operators | Description |
|---|---|---|
| 1 | `**` | Exponentiation |
| 2 | `+x`, `-x` | Unary positive and negative |
| 3 | `*`, `/`, `//`, `%` | Multiplication, division, floor division, modulus |
| 4 | `+`, `-` | Addition and subtraction |
| 5 | Comparisons | `==`, `!=`, `>`, `<`, `>=`, `<=` |

Parentheses can be used to control the order of evaluation.

Example:

```python
result = (10 + 5) * 2

print(result)
```

Output:

```text
30
```

Important: This is a simplified precedence table for the operators covered here. Python has additional precedence rules for other operator categories.

---

# 11. Important Concepts and Common Mistakes

## Mistake 1: Confusing / and //

```python
print(10 / 2)
print(10 // 2)
```

Output:

```text
5.0
5
```

`/` performs division.

`//` performs floor division.

## Mistake 2: Confusing % and /

```python
print(17 / 5)
print(17 % 5)
```

Output:

```text
3.4
2
```

`/` returns the division result.

`%` returns the remainder.

## Mistake 3: Confusing = and ==

```python
age = 25

print(age == 25)
```

Output:

```text
True
```

`=` assigns a value.

`==` compares values.

## Mistake 4: Incorrectly Updating a Variable

```python
number = 10

number += 5

print(number)
```

Output:

```text
15
```

Remember that `+=` updates the variable. It does not create a separate result variable.

## Mistake 5: Division by Zero

```python
result = 10 / 0
```

This raises:

```text
ZeroDivisionError
```

Always consider whether the denominator can be zero when processing external data.

## Mistake 6: Floating-Point Precision

```python
print(0.1 + 0.2)
```

Output:

```text
0.30000000000000004
```

This happens because many decimal fractions cannot be represented exactly using binary floating-point.

For financial calculations, consider using Python's `decimal.Decimal` instead of relying on ordinary floating-point arithmetic.

---

# 12. FDE Practical Application

As a Forward-Deployed Engineer, you will frequently implement business logic based on customer requirements.

Let's consider three simple examples.

## Example 1: Payment Calculation

```python
product_price = 1500
quantity = 3

total_amount = product_price * quantity

discount = 500

total_amount -= discount

print("Final Payment:", total_amount)
```

Output:

```text
4000
```

## Example 2: Account Eligibility

```python
account_balance = 5000
minimum_balance = 1000

if account_balance >= minimum_balance:
    print("Transaction allowed")
else:
    print("Insufficient balance")
```

Output:

```text
Transaction allowed
```

## Example 3: API Request Validation

```python
request_amount = 2500
minimum_amount = 100
maximum_amount = 10000

if minimum_amount <= request_amount <= maximum_amount:
    print("Request is valid")
else:
    print("Invalid request amount")
```

Output:

```text
Request is valid
```

These examples demonstrate how operators help translate business requirements into executable Python logic.

In production applications, additional validation, authentication, authorization, and error handling may also be required.

---

# 13. Practice Exercises

Try solving these exercises without looking at the examples.

## Exercise 1: Arithmetic Operators

Create two variables:

```python
a = 25
b = 4
```

Calculate:

1. Addition
2. Subtraction
3. Multiplication
4. Division
5. Floor division
6. Modulus
7. Exponentiation

## Exercise 2: Even or Odd

Write a program that:

1. Accepts an integer.
2. Checks whether the number is even or odd.
3. Displays the result.

Hint: Use the modulus operator.

## Exercise 3: Comparison Operators

Create two variables:

```python
a = 100
b = 200
```

Check:

1. Whether a is equal to b.
2. Whether a is greater than b.
3. Whether a is less than b.
4. Whether a is not equal to b.

## Exercise 4: Assignment Operators

Start with:

```python
balance = 10000
```

Perform the following operations:

1. Add 2000.
2. Subtract 1500.
3. Multiply by 2.
4. Divide by 5.

Print the balance after each operation.

## Exercise 5: Shopping Cart

Create a shopping cart with:

- Laptop price: 50000
- Mouse price: 1000
- Keyboard price: 2000

Calculate the total price.

Apply a discount of 3000.

Print the final amount.

## Exercise 6: Eligibility Validation

Write a program that checks whether a person is eligible for an application.

Conditions:

- Minimum age: 18
- Maximum age: 60

Use comparison operators.

## Exercise 7: Floor Division and Modulus

Predict the output before executing:

```python
print(17 // 5)
print(17 % 5)

print(-7 // 2)
print(-7 % 2)
```

Explain why negative floor division produces `-4`.

## Exercise 8: Operator Precedence

Predict the output:

```python
result = 10 + 5 * 2 ** 2

print(result)
```

Then use parentheses to change the result.

---

# 14. Self-Assessment Questions

1. What are operators and operands?
2. What is the difference between `/` and `//`?
3. What does the modulus operator return?
4. What is the purpose of the exponentiation operator?
5. Why does `10 / 2` return `5.0`?
6. What is the difference between `=` and `==`?
7. What is the output of `10 % 3`?
8. What is the difference between `+=` and `+`?
9. What does `>=` check?
10. What is operator precedence?
11. Why does `-7 // 2` return `-4`?
12. How are operators useful in API request validation?

---

# 15. Quick Revision

| Category | Operator | Purpose |
|---|---|---|
| Arithmetic | `+` | Addition |
| Arithmetic | `-` | Subtraction |
| Arithmetic | `*` | Multiplication |
| Arithmetic | `/` | Division |
| Arithmetic | `//` | Floor division |
| Arithmetic | `%` | Remainder |
| Arithmetic | `**` | Power |
| Comparison | `==` | Equal to |
| Comparison | `!=` | Not equal to |
| Comparison | `>` | Greater than |
| Comparison | `<` | Less than |
| Comparison | `>=` | Greater than or equal |
| Comparison | `<=` | Less than or equal |
| Assignment | `=` | Assign value |
| Assignment | `+=` | Add and assign |
| Assignment | `-=` | Subtract and assign |
| Assignment | `*=` | Multiply and assign |
| Assignment | `/=` | Divide and assign |
| Assignment | `//=` | Floor divide and assign |
| Assignment | `%=` | Modulus and assign |
| Assignment | `**=` | Power and assign |

---

# 16. Key Takeaways

- Arithmetic operators perform mathematical calculations.
- Comparison operators compare values and return Boolean results.
- Assignment operators assign or update variable values.
- `/` performs division, while `//` performs floor division.
- `%` returns the remainder.
- `**` calculates powers.
- `==` compares values, while `=` assigns values.
- Compound assignment operators simplify variable updates.
- Operator precedence determines the order of evaluation.
- Parentheses make complex expressions easier to understand.
- Operators are fundamental to implementing business logic and validating application data.

---

# 17. Learning Progress

**Completed Topic:** Arithmetic, Comparison and Assignment Operators

**Suggested Next Topic:** Logical Operators

The next chapter will cover:

- `and`
- `or`
- `not`
- Truthy and falsy values
- Short-circuit evaluation
- Combining multiple conditions
- Practical authentication and API validation examples
