
# Python while Loops

## 1. Introduction to while Loops

A `while` loop is used to execute a block of code repeatedly as long as a given condition evaluates to `True`.

In simple terms:

**A while loop continues executing until its condition becomes False.**

### Real-world analogy

Imagine an ATM withdrawal process.

1. The ATM asks for the withdrawal amount.
2. It checks whether the account has sufficient balance.
3. If the balance is sufficient, the transaction continues.
4. If the balance is insufficient, the transaction is rejected.

A similar condition-based approach can be implemented using a while loop.

### Syntax

```python
while condition:
    # Code to execute
```

Explanation:

| Component | Description |
|---|---|
| `while` | Starts the loop |
| `condition` | Expression evaluated before every iteration |
| `:` | Marks the beginning of the loop block |
| Indented code | Executes while the condition is True |

---

## 2. Basic while Loop

### Example 1: Print Numbers from 1 to 5

```python
number = 1

while number <= 5:
    print(number)
    number = number + 1
```

Output:

```text
1
2
3
4
5
```

### How does it work?

Initially:

```python
number = 1
```

Python checks:

```python
while number <= 5:
```

Execution:

| Iteration | number | Condition | Action |
|---|---:|---|---|
| 1 | 1 | True | Print 1 |
| 2 | 2 | True | Print 2 |
| 3 | 3 | True | Print 3 |
| 4 | 4 | True | Print 4 |
| 5 | 5 | True | Print 5 |
| 6 | 6 | False | Stop |

Once `number` becomes 6, the condition becomes False, and the loop terminates.

**Important:** The variable must be updated so that the condition can eventually become False.

---

## 3. Understanding How a while Loop Executes

A while loop follows this execution process:

1. Initialize a variable if required.
2. Evaluate the condition.
3. If the condition is True, execute the loop body.
4. Update relevant variables.
5. Return to the condition.
6. Stop when the condition becomes False.

### Flow of Execution

```text
       Start
         |
         v
   Check condition
         |
      True?
      /   \
    Yes    No
     |      |
     v      v
 Execute   Exit loop
 code
     |
     v
 Update variable
     |
     +------> Check condition again
```

Unlike a `for` loop, a `while` loop does not automatically move through a sequence. The programmer controls the condition and any required updates.

---

## 4. Increment and Decrement in while Loops

### Example 1: Increment

Increment means increasing a variable's value.

```python
count = 1

while count <= 5:
    print(count)
    count += 1
```

Output:

```text
1
2
3
4
5
```

### Example 2: Decrement

Decrement means decreasing a variable's value.

```python
count = 5

while count >= 1:
    print(count)
    count -= 1
```

Output:

```text
5
4
3
2
1
```

### Example 3: Print Even Numbers

```python
number = 2

while number <= 20:
    print(number)
    number += 2
```

Output:

```text
2
4
6
8
10
12
14
16
18
20
```

---

## 5. Infinite while Loops

An infinite loop is a loop that continues executing without reaching a termination condition.

### Example

```python
number = 1

while number <= 5:
    print(number)
```

This program continuously prints `1`.

Why?

Because the value of `number` is never updated.

The condition:

```python
number <= 5
```

always remains True.

### Corrected Example

```python
number = 1

while number <= 5:
    print(number)
    number += 1
```

Now the loop terminates after five iterations.

### Important Note

Infinite loops are not always mistakes.

Sometimes they are intentional.

For example:

- Continuously monitoring a system.
- Waiting for user input.
- Running a background worker.
- Listening for incoming events.

However, production applications need an appropriate exit condition, cancellation mechanism, or shutdown strategy.

---

## 6. Using while True

Python allows us to create a loop using:

```python
while True:
    # Code
```

Since `True` never becomes False, the loop continues until something explicitly terminates it, typically using `break`.

### Example: Simple Menu Application

```python
while True:
    print("\n1. View Profile")
    print("2. View Settings")
    print("3. Exit")

    choice = input("Enter your choice: ")

    if choice == "1":
        print("Displaying Profile")

    elif choice == "2":
        print("Displaying Settings")

    elif choice == "3":
        print("Application Closed")
        break

    else:
        print("Invalid Choice")
```

The application continues displaying the menu until the user enters `3`.

---

## 7. Using break in while Loops

The `break` statement immediately terminates the nearest enclosing loop.

### Example

```python
number = 1

while number <= 10:

    if number == 5:
        break

    print(number)
    number += 1
```

Output:

```text
1
2
3
4
```

When `number` becomes 5, the `break` statement terminates the loop.

The remaining iterations are not executed.

---

## 8. Using continue in while Loops

The `continue` statement skips the remaining statements in the current iteration and moves to the next condition check.

### Example: Skip Number 3

```python
number = 0

while number < 5:

    number += 1

    if number == 3:
        continue

    print(number)
```

Output:

```text
1
2
4
5
```

When the value becomes 3, Python skips the `print()` statement and checks the loop condition again.

**Important:** In a while loop, ensure that the variable update happens before `continue` when necessary. Otherwise, the loop may become infinite.

---

## 9. Using pass in while Loops

The `pass` statement does nothing.

It acts as a placeholder when Python requires a statement but the implementation is not ready.

### Example

```python
number = 1

while number <= 3:
    pass
```

This example creates an infinite loop because `number` is never updated.

A safer placeholder example is:

```python
number = 1

while number <= 3:
    # Implementation will be added later
    pass

    number += 1
```

`pass` does not terminate or skip an iteration. It simply performs no operation.

### Difference Between break, continue and pass

| Statement | Purpose |
|---|---|
| `break` | Terminates the nearest enclosing loop |
| `continue` | Skips the remaining current iteration |
| `pass` | Does nothing; acts as a placeholder |

---

## 10. Using else with while Loops

Python supports an `else` block with while loops.

The `else` block executes when the loop condition becomes False through normal completion.

It does not execute when the loop is terminated by `break`.

### Example 1: Normal Completion

```python
number = 1

while number <= 3:
    print(number)
    number += 1

else:
    print("Loop completed")
```

Output:

```text
1
2
3
Loop completed
```

### Example 2: Loop Terminated by break

```python
number = 1

while number <= 5:

    if number == 3:
        break

    print(number)
    number += 1

else:
    print("Loop completed")
```

Output:

```text
1
2
```

The else block does not execute because the loop was terminated by `break`.

---

## 11. Nested while Loops

A nested while loop means placing one while loop inside another while loop.

### Example

```python
row = 1

while row <= 3:

    column = 1

    while column <= 2:
        print("Row:", row, "Column:", column)
        column += 1

    row += 1
```

Output:

```text
Row: 1 Column: 1
Row: 1 Column: 2
Row: 2 Column: 1
Row: 2 Column: 2
Row: 3 Column: 1
Row: 3 Column: 2
```

### How does it work?

- The outer loop controls the rows.
- The inner loop controls the columns.
- The inner loop completes its iterations for every outer loop iteration.

**Important:** Initialize the inner loop variable inside the outer loop when it needs to restart for every outer iteration.

---

## 12. Practical Example: User Login Attempts

Imagine a login system that allows a user to enter a password up to three times.

```python
correct_password = "python123"
attempts = 0
maximum_attempts = 3

while attempts < maximum_attempts:

    password = input("Enter password: ")

    if password == correct_password:
        print("Login successful")
        break

    else:
        attempts += 1
        print("Incorrect password")

else:
    print("Maximum attempts reached")
```

Explanation:

1. The user gets a maximum of three attempts.
2. The loop checks whether attempts are below three.
3. If the password is correct, `break` terminates the loop.
4. Otherwise, the attempt count increases.
5. If all attempts are used without success, the loop's `else` block executes.

This is an educational example. Real authentication systems should use secure password hashing, proper session management, and server-side rate limiting.

---

## 13. Practical FDE Application: Retry Mechanism

When integrating external APIs, temporary failures may occur.

For example:

- Network interruptions.
- Temporary service unavailability.
- Rate limiting.
- Server errors.

A retry mechanism can attempt an operation again.

### Example: Simulated API Retry

```python
attempts = 0
maximum_attempts = 3

while attempts < maximum_attempts:

    attempts += 1

    print("API request attempt:", attempts)

    api_success = False

    if attempts == 3:
        api_success = True

    if api_success:
        print("API request successful")
        break

    print("API request failed")

else:
    print("API request failed after all attempts")
```

Output:

```text
API request attempt: 1
API request failed
API request attempt: 2
API request failed
API request attempt: 3
API request successful
```

This is a simulation, not a real HTTP request.

In a production integration, you would typically use:

- HTTP client libraries such as `requests` or `httpx`.
- Exception handling.
- Request timeouts.
- Bounded retries.
- Exponential backoff.
- Appropriate handling for retryable HTTP status codes.
- Idempotency protection where required.

---

## 14. Difference Between for and while Loops

Both loops execute code repeatedly, but their typical use cases differ.

| Feature | for Loop | while Loop |
|---|---|---|
| Main purpose | Iterate over an iterable | Repeat while a condition is True |
| Iteration | Gets elements from an iterable | Depends on a Boolean condition |
| Initialization | Often handled by the iterable | Usually initialized separately |
| Updating | Iteration advances automatically | Programmer updates relevant state |
| Common use | Lists, strings, ranges | Retry systems, menus, monitoring |
| Infinite loop risk | Usually less common | Higher if condition never changes |

### Example: for Loop

```python
for number in range(1, 6):
    print(number)
```

### Example: while Loop

```python
number = 1

while number <= 5:
    print(number)
    number += 1
```

Both examples produce:

```text
1
2
3
4
5
```

Use a `for` loop when iterating over an iterable. Use a `while` loop when repetition depends on a condition.

---

## 15. Common Mistakes

### Mistake 1: Forgetting to Update the Variable

Incorrect:

```python
count = 1

while count <= 5:
    print(count)
```

Problem: The loop never terminates.

Correction:

```python
count = 1

while count <= 5:
    print(count)
    count += 1
```

### Mistake 2: Incorrect Condition

```python
count = 1

while count >= 5:
    print(count)
    count += 1
```

The loop body never executes because the initial condition is False.

### Mistake 3: Incorrect Placement of Increment

Incorrect:

```python
count = 1

while count <= 5:

    if count == 3:
        continue

    print(count)
    count += 1
```

Problem: When `count` becomes 3, `continue` skips the increment. The loop becomes infinite.

Correction:

```python
count = 1

while count <= 5:

    current = count
    count += 1

    if current == 3:
        continue

    print(current)
```

### Mistake 4: Confusing break and continue

- `break` stops the entire nearest enclosing loop.
- `continue` skips only the current iteration.

### Mistake 5: Incorrect Indentation

Incorrect:

```python
count = 1

while count <= 5:
print(count)
count += 1
```

Correct:

```python
count = 1

while count <= 5:
    print(count)
    count += 1
```

---

## 16. Practice Exercises

Try solving these exercises without looking at the examples.

### Beginner Level

1. Print numbers from 1 to 10 using a while loop.
2. Print numbers from 10 to 1 in reverse order.
3. Print even numbers between 1 and 50.
4. Print odd numbers between 1 and 50.
5. Calculate the sum of numbers from 1 to 100.

### Intermediate Level

6. Find the factorial of a number using a while loop.
7. Count the number of digits in an integer.
8. Reverse a number using a while loop.
9. Find the sum of the digits of a number.
10. Create a multiplication table using a while loop.

### Practical FDE Exercises

11. Create a menu-driven application using `while True`.
12. Build a login attempt simulation with a maximum of three attempts.
13. Create a retry mechanism that stops after five attempts.
14. Simulate monitoring a service until its status becomes `"healthy"`.
15. Create a program that repeatedly accepts customer records until the user enters `"exit"`.

---

## 17. Quick Revision

| Concept | Description |
|---|---|
| `while` | Repeats code while a condition is True |
| Condition | Controls whether the loop continues |
| Increment | Increases a variable's value |
| Decrement | Decreases a variable's value |
| Infinite loop | Loop that does not terminate normally |
| `while True` | Creates a loop with an always-True condition |
| `break` | Terminates the nearest enclosing loop |
| `continue` | Skips the current iteration |
| `pass` | Does nothing |
| `else` | Executes when the loop completes without break |
| Nested while | A while loop inside another while loop |

---

## 18. Self-Assessment Questions

Before moving forward, make sure you can answer:

1. What is a while loop?
2. How does Python evaluate a while loop condition?
3. Why is variable initialization important?
4. Why should we update variables inside a while loop?
5. What is an infinite loop?
6. What is the purpose of `while True`?
7. What is the difference between `break` and `continue`?
8. What is the purpose of `pass`?
9. When does the else block execute in a while loop?
10. What is a nested while loop?
11. What is the difference between for and while loops?
12. How can while loops help implement API retry mechanisms?

---

## 19. Learning Outcome

After completing this chapter, you should be able to:

- Understand condition-based repetition.
- Write while loops.
- Control loop execution using increment and decrement.
- Identify and prevent unintended infinite loops.
- Use `break`, `continue`, and `pass`.
- Implement nested while loops.
- Understand the loop else clause.
- Build simple retry mechanisms and menu-driven applications.

### Next Topic

**Loop Control Statements: break, continue, and pass**

We have introduced these statements in this chapter. The next chapter will explore their execution flow, nested-loop behavior, and practical applications in greater detail.
