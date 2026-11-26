
# Operator Precedence in Python

## 1. Introduction

Operator precedence determines the order in which Python evaluates operators in an expression.

When an expression contains multiple operators, Python follows a predefined order of priority.

### Example

```python
result = 10 + 5 * 2

print(result)
```

Output:

```text
20
```

Why?

Python evaluates multiplication before addition.

Step-by-step:

```text
10 + 5 * 2

10 + 10

20
```

If Python evaluated from left to right without considering precedence, the result would be different:

```text
(10 + 5) * 2

15 * 2

30
```

Therefore, operator precedence determines which operation happens first.

---

## 2. Why Do We Need Operator Precedence?

Consider a real-world calculation:

```python
total_amount = 1000 + 500 * 2

print(total_amount)
```

Output:

```text
2000
```

Explanation:

- Product price = 1000
- Additional item price = 500
- Quantity = 2

Python calculates multiplication first:

```text
1000 + (500 * 2)

1000 + 1000

2000
```

Understanding precedence helps prevent incorrect calculations in financial applications, business logic, API validations, and data-processing systems.

---

## 3. Python Operator Precedence Table

The following table lists common Python operators from highest precedence to lowest precedence.

| Priority | Operators | Description |
|---|---|---|
| 1 | `()` | Parentheses / grouping |
| 2 | `**` | Exponentiation |
| 3 | `+x`, `-x`, `~x` | Unary plus, minus, bitwise NOT |
| 4 | `*`, `/`, `//`, `%`, `@` | Multiplication, division, floor division, modulus, matrix multiplication |
| 5 | `+`, `-` | Addition and subtraction |
| 6 | `<<`, `>>` | Bitwise shifts |
| 7 | `&` | Bitwise AND |
| 8 | `^` | Bitwise XOR |
| 9 | `|` | Bitwise OR |
| 10 | `==`, `!=`, `<`, `>`, `<=`, `>=`, `is`, `is not`, `in`, `not in` | Comparisons, identity and membership |
| 11 | `not` | Logical NOT |
| 12 | `and` | Logical AND |
| 13 | `or` | Logical OR |
| 14 | `if ... else` | Conditional expression |
| 15 | `lambda` | Lambda expression |
| 16 | `:=` | Assignment expression |

Note:
- Operators with the same precedence generally follow their associativity rules.
- This is a simplified reference table of commonly encountered operators, not every Python expression rule.
- Parentheses can be used to make the intended evaluation order explicit.

---

## 4. Understanding Operator Precedence Step by Step

### Example 1: Multiplication and Addition

```python
result = 10 + 5 * 2

print(result)
```

Output:

```text
20
```

Evaluation:

```text
10 + 5 * 2

10 + 10

20
```

Multiplication has higher precedence than addition.

### Example 2: Division and Subtraction

```python
result = 20 - 10 / 2

print(result)
```

Output:

```text
15.0
```

Evaluation:

```text
20 - 10 / 2

20 - 5.0

15.0
```

Division is evaluated before subtraction.

### Example 3: Multiple Arithmetic Operators

```python
result = 10 + 20 * 3 - 5

print(result)
```

Output:

```text
65
```

Evaluation:

```text
10 + 20 * 3 - 5

10 + 60 - 5

70 - 5

65
```

Multiplication is performed before addition and subtraction.

When operators have the same precedence, their associativity determines the order.

---

## 5. Parentheses and Operator Precedence

Parentheses allow us to control the evaluation order.

### Without Parentheses

```python
result = 10 + 5 * 2

print(result)
```

Output:

```text
20
```

### With Parentheses

```python
result = (10 + 5) * 2

print(result)
```

Output:

```text
30
```

Explanation:

Without parentheses:
- Multiplication happens first.

With parentheses:
- The expression inside parentheses is evaluated first.

Important:

Parentheses are useful for making complex expressions easier to understand and maintain.

---

## 6. Associativity

Associativity determines the evaluation order when operators have the same precedence.

Most arithmetic operators with the same precedence are evaluated from left to right.

### Example 1: Left-to-Right Associativity

```python
result = 20 - 5 - 3

print(result)
```

Output:

```text
12
```

Evaluation:

```text
(20 - 5) - 3

15 - 3

12
```

### Example 2: Exponentiation

Exponentiation (`**`) is evaluated from right to left.

```python
result = 2 ** 3 ** 2

print(result)
```

Output:

```text
512
```

Evaluation:

```text
2 ** (3 ** 2)

2 ** 9

512
```

Important:

Exponentiation is right-associative, unlike most arithmetic operators.

### Example 3: Parentheses Change Associativity

```python
result = (2 ** 3) ** 2

print(result)
```

Output:

```text
64
```

Evaluation:

```text
8 ** 2

64
```

---

## 7. Operator Precedence with Comparison Operators

Comparison operators have lower precedence than arithmetic operators.

Example:

```python
age = 25

result = age + 5 > 20

print(result)
```

Output:

```text
True
```

Evaluation:

```text
25 + 5 > 20

30 > 20

True
```

Another example:

```python
a = 10
b = 20
c = 30

print(a < b and b < c)
```

Output:

```text
True
```

Explanation:

1. `a < b` evaluates to `True`.
2. `b < c` evaluates to `True`.
3. `and` combines both results.

### Chained Comparisons

Python also supports chained comparisons.

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
18 <= age and age <= 60
```

Chained comparisons are useful for checking ranges.

---

## 8. Operator Precedence with Logical Operators

Logical operators have different precedence levels:

```text
not
and
or
```

`not` has higher precedence than `and`, and `and` has higher precedence than `or`.

### Example

```python
result = True or False and False

print(result)
```

Output:

```text
True
```

Evaluation:

```text
True or (False and False)

True or False

True
```

### Another Example

```python
result = not True or False

print(result)
```

Output:

```text
False
```

Evaluation:

```text
(not True) or False

False or False

False
```

Recommendation:

Use parentheses when combining multiple logical conditions.

```python
result = (True or False) and False

print(result)
```

Output:

```text
False
```

---

## 9. Unary Operator Precedence and Exponentiation

One important Python detail is that exponentiation interacts with unary minus in a special way.

Example:

```python
result = -2 ** 2

print(result)
```

Output:

```text
-4
```

Why?

Python evaluates this as:

```python
-(2 ** 2)
```

Therefore:

```text
-(4)

-4
```

If you want to square negative two, use parentheses:

```python
result = (-2) ** 2

print(result)
```

Output:

```text
4
```

This is a common interview question.

---

## 10. Practical FDE Example

Imagine developing a service that checks whether a user qualifies for a discount.

Requirements:

- The user must be at least 18 years old.
- The purchase amount must be at least 5,000.
- The user must be either a premium member or have a valid coupon.

```python
age = 25
purchase_amount = 6000
is_premium = True
has_coupon = False

eligible = (
    age >= 18
    and purchase_amount >= 5000
    and (is_premium or has_coupon)
)

print(eligible)
```

Output:

```text
True
```

Explanation:

1. `age >= 18` evaluates to `True`.
2. `purchase_amount >= 5000` evaluates to `True`.
3. `is_premium or has_coupon` evaluates to `True`.
4. The three conditions are combined using `and`.

All requirements are satisfied.

This type of conditional logic appears in:
- Business rule engines.
- API request validation.
- Pricing systems.
- User eligibility checks.
- Feature access control.

---

## 11. Common Mistakes

### Mistake 1: Assuming Python Always Evaluates from Left to Right

Incorrect assumption:

```python
result = 10 + 5 * 2
```

Python does not simply evaluate this from left to right.

Correct result:

```text
20
```

### Mistake 2: Forgetting Parentheses

```python
result = 10 + 5 * 2
```

This is different from:

```python
result = (10 + 5) * 2
```

Outputs:

```text
20
30
```

### Mistake 3: Misunderstanding Exponentiation

```python
print(2 ** 3 ** 2)
```

Output:

```text
512
```

Remember that exponentiation is right-associative.

### Mistake 4: Misunderstanding Logical Precedence

```python
print(True or False and False)
```

Output:

```text
True
```

Because `and` has higher precedence than `or`.

### Mistake 5: Ignoring Unary Minus

```python
print(-3 ** 2)
```

Output:

```text
-9
```

To get positive nine:

```python
print((-3) ** 2)
```

Output:

```text
9
```

---

## 12. Quick Revision

| Concept | Important Rule |
|---|---|
| Operator precedence | Determines which operator is evaluated first |
| Parentheses | Highest priority for grouping expressions |
| Multiplication and division | Higher precedence than addition and subtraction |
| Comparison operators | Lower precedence than arithmetic operators |
| `not` | Higher precedence than `and` and `or` |
| `and` | Higher precedence than `or` |
| Associativity | Determines order among operators with equal precedence |
| Exponentiation | Right-associative |
| Most arithmetic operators | Generally left-associative |

### Important Expressions to Remember

| Expression | Result |
|---|---:|
| `10 + 5 * 2` | `20` |
| `(10 + 5) * 2` | `30` |
| `2 ** 3 ** 2` | `512` |
| `(2 ** 3) ** 2` | `64` |
| `-2 ** 2` | `-4` |
| `(-2) ** 2` | `4` |
| `True or False and False` | `True` |

---

## 13. Practice Exercises

Try predicting the output before running each program.

### Exercise 1: Arithmetic Precedence

```python
result = 10 + 20 * 2 - 5

print(result)
```

### Exercise 2: Parentheses

```python
result = (10 + 20) * (5 - 2)

print(result)
```

### Exercise 3: Exponentiation

```python
result = 3 ** 2 ** 2

print(result)
```

### Exercise 4: Unary Minus

```python
print(-5 ** 2)
print((-5) ** 2)
```

### Exercise 5: Logical Precedence

```python
a = True
b = False
c = True

print(a or b and c)
print((a or b) and c)
```

### Exercise 6: Combined Conditions

```python
age = 25
salary = 40000
is_active = True

result = age >= 18 and salary > 30000 or is_active

print(result)
```

Explain the order of evaluation.

---

## 14. Self-Assessment

Before moving to the next topic, make sure you can explain:

1. What is operator precedence?
2. Why does multiplication happen before addition?
3. What is the purpose of parentheses?
4. What is associativity?
5. Why is `2 ** 3 ** 2` equal to `512`?
6. Why is `-2 ** 2` equal to `-4`?
7. What is the precedence order of `not`, `and`, and `or`?
8. How does operator precedence affect complex business conditions?

---

## 15. Connection to Forward Deployed Engineering

Operator precedence is not just a Python theory concept.

As a Forward Deployed Engineer, you will write conditions involving:

- API validations.
- Authentication and authorization.
- Business rules.
- Financial calculations.
- Data filtering.
- Feature flags.
- Conditional workflows.

Incorrect operator precedence can produce incorrect business decisions.

A good engineering practice is to use parentheses to make complex expressions clear, even when Python's precedence rules already determine the result.

**Completed Topic:** Operator Precedence

**Suggested Next Topic:** Conditional Statements in Python (`if`, `elif`, and `else`).
