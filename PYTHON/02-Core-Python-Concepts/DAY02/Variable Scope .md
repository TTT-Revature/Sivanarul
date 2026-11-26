
# Variable Scope in Python

## 1. What is Variable Scope?

Variable scope defines the region of a program where a variable can be accessed.

Consider this example:

```python
name = "Arun"

def greet():
    print(name)

greet()
print(name)
```

Output:

```text
Arun
Arun
```

Here, `name` is defined outside the function.

Therefore, it can be accessed both inside the function and outside it.

But what happens when we define a variable inside a function?

Let's understand.

## 2. Local Scope

A variable created inside a function is called a local variable.

It is generally accessible only within that function.

Example:

```python
def greet():
    message = "Hello Python"
    print(message)

greet()
```

Output:

```text
Hello Python
```

Here:
- `message` is a local variable.
- It is created inside `greet()`.
- It can be accessed inside that function.

### Accessing a Local Variable Outside the Function

```python
def greet():
    message = "Hello Python"

greet()

print(message)
```

Output:

```text
NameError: name 'message' is not defined
```

Why?

The variable `message` belongs to the function's local scope.

It cannot be accessed directly from the global scope.

Important:

A local variable's name is not available outside its scope, although objects it references can continue to exist if another reference keeps them alive.

## 3. Global Scope

A variable defined at the top level of a module is called a global variable.

It can be accessed throughout that module, including inside functions, provided it is not shadowed by another local or enclosing variable.

Example:

```python
company = "OpenAI"

def display_company():
    print(company)

display_company()
print(company)
```

Output:

```text
OpenAI
OpenAI
```

Here:
- `company` is a global variable.
- The function can read it.
- The variable can also be accessed outside the function.

### Modifying a Global Variable

Consider this example:

```python
count = 10

def update_count():
    count = 20
    print(count)

update_count()

print(count)
```

Output:

```text
20
10
```

Why?

Inside the function, Python creates a new local variable named `count`.

It does not modify the global variable.

This is called variable shadowing.

The local variable temporarily hides the global variable when resolving the name inside the function.

## 4. The global Keyword

If you want to reassign a global variable inside a function, use the `global` keyword.

Example:

```python
count = 10

def update_count():
    global count
    count = 20

update_count()

print(count)
```

Output:

```text
20
```

Explanation:

```python
global count
```

This tells Python that assignments to `count` inside this function should refer to the module-level global variable.

### Without global

```python
count = 10

def update_count():
    count = 50

update_count()

print(count)
```

Output:

```text
10
```

### With global

```python
count = 10

def update_count():
    global count
    count = 50

update_count()

print(count)
```

Output:

```text
50
```

Important:

Use `global` carefully. Excessive modification of global variables makes applications harder to test, debug and maintain.

## 5. Enclosing Scope

Enclosing scope occurs when one function is defined inside another function.

Example:

```python
def outer_function():

    message = "Hello from outer function"

    def inner_function():
        print(message)

    inner_function()

outer_function()
```

Output:

```text
Hello from outer function
```

Here:
- `outer_function()` is the outer function.
- `inner_function()` is the inner function.
- `message` belongs to the enclosing scope of `inner_function()`.

The inner function can access variables defined in its enclosing function.

### Another Example

```python
def outer():
    name = "Arun"

    def inner():
        age = 27
        print(name)
        print(age)

    inner()

outer()
```

Output:

```text
Arun
27
```

The inner function can access both:
- `name` from the enclosing scope.
- `age` from its own local scope.

But the outer function cannot directly access the inner function's local variable.

## 6. The nonlocal Keyword

What if you want to modify a variable belonging to an enclosing function?

Python provides the `nonlocal` keyword.

Example:

```python
def outer():

    count = 10

    def inner():
        nonlocal count
        count = 20

    inner()

    print(count)

outer()
```

Output:

```text
20
```

Explanation:

- `count` belongs to `outer()`.
- `inner()` accesses the enclosing variable.
- `nonlocal count` tells Python to modify that enclosing variable instead of creating a new local variable.

### Without nonlocal

```python
def outer():

    count = 10

    def inner():
        count = 20

    inner()

    print(count)

outer()
```

Output:

```text
10
```

Why?

The assignment creates a local variable inside `inner()`.

The enclosing variable remains unchanged.

### global vs nonlocal

| global | nonlocal |
|---|---|
| Refers to a module-level variable | Refers to a variable in an enclosing function |
| Used for global scope | Used for enclosing function scope |
| Can reassign a global variable | Can reassign an enclosing variable |
| Cannot create a reference to an arbitrary local variable | Requires an existing binding in an enclosing function scope |

## 7. LEGB Rule

Python follows the LEGB rule when resolving variable names.

LEGB represents four scopes:

1. Local
2. Enclosing
3. Global
4. Built-in

Python searches these scopes in this order.

### L – Local

The current function's local scope.

### E – Enclosing

The scope of an outer function containing the current function.

### G – Global

The module-level scope.

### B – Built-in

Names provided by Python itself, such as:
- `print()`
- `len()`
- `sum()`
- `range()`
- `type()`

### LEGB Example

```python
name = "Global"

def outer():

    name = "Enclosing"

    def inner():

        name = "Local"

        print(name)

    inner()

outer()
```

Output:

```text
Local
```

Why?

Python finds `name` in the local scope first.

It does not need to search the enclosing or global scope.

### Demonstrating the Full LEGB Search

```python
name = "Global"

def outer():

    name = "Enclosing"

    def inner():
        print(name)

    inner()

outer()
```

Output:

```text
Enclosing
```

Python does not find `name` in the local scope of `inner()`.

It finds the variable in the enclosing scope.

If we remove the enclosing variable, Python searches the global scope.

If no matching name exists in any of these scopes, Python raises `NameError`.

## 8. Variable Shadowing

Variable shadowing occurs when a variable in an inner scope has the same name as a variable in an outer scope.

Example:

```python
name = "Global Name"

def greet():
    name = "Local Name"
    print(name)

greet()

print(name)
```

Output:

```text
Local Name
Global Name
```

The local variable shadows the global variable inside the function.

The global variable remains unchanged.

## 9. Scope and Mutable Objects

An important distinction:

You can modify a mutable global object inside a function without using `global`, as long as you are not rebinding the variable itself.

Example:

```python
employees = ["Arun", "Priya"]

def add_employee():
    employees.append("Kumar")

add_employee()

print(employees)
```

Output:

```text
['Arun', 'Priya', 'Kumar']
```

Why?

The function accesses the global list and modifies the same list object.

Now consider reassignment:

```python
employees = ["Arun", "Priya"]

def replace_employees():
    employees = ["Kumar", "John"]

replace_employees()

print(employees)
```

Output:

```text
['Arun', 'Priya']
```

Why?

The assignment creates a local variable named `employees`.

It does not replace the global list.

Remember:

- Mutating a shared object does not require `global`.
- Reassigning a global variable requires `global`.

## 10. Scope and Functions

Functions also have names that follow scope rules.

Example:

```python
def greet():
    print("Hello")

greet()
```

Here, `greet` is a name defined in the module's global scope.

You can also define a function inside another function.

```python
def outer():

    def inner():
        print("Inside inner function")

    inner()

outer()
```

Output:

```text
Inside inner function
```

The name `inner` is local to `outer()` and cannot normally be accessed directly outside it.

## 11. Practical Example: API Configuration

Imagine you are building an API integration.

You have a global configuration value.

```python
API_TIMEOUT = 30

def fetch_customer():
    print(f"API timeout: {API_TIMEOUT} seconds")

fetch_customer()
```

Output:

```text
API timeout: 30 seconds
```

The function can read the global configuration.

However, a more maintainable approach for reusable application code is often to pass configuration explicitly.

```python
def fetch_customer(timeout):
    print(f"API timeout: {timeout} seconds")

fetch_customer(30)
fetch_customer(60)
```

Output:

```text
API timeout: 30 seconds
API timeout: 60 seconds
```

Why is this approach useful?

- The function is easier to test.
- Different API calls can use different timeouts.
- Hidden dependencies are reduced.
- Configuration is explicit.

## 12. Common Mistakes

| Mistake | Explanation |
|---|---|
| Accessing a local variable outside its function | Causes NameError |
| Assuming local assignment modifies a global variable | Creates a local variable instead |
| Forgetting global before global reassignment | Can cause UnboundLocalError |
| Using nonlocal without an enclosing binding | Causes SyntaxError |
| Confusing mutation with reassignment | They have different scope behavior |
| Assuming inner functions can be accessed everywhere | Their names belong to their defining scope |

### Important: UnboundLocalError

Consider:

```python
count = 10

def update():
    print(count)
    count = 20

update()
```

Output:

```text
UnboundLocalError
```

Why?

Python determines that `count` is local to `update()` because it is assigned there.

The function tries to read this local variable before assigning a value to it.

Correct version:

```python
count = 10

def update():
    global count
    print(count)
    count = 20

update()
```

Output:

```text
10
```

## 13. Practical Exercises

### Exercise 1: Local Scope

Create a function that defines a variable called `message` and prints it.

Try accessing that variable outside the function. Observe the error.

### Exercise 2: Global Scope

Create a global variable called `company`.

Access it inside a function without using `global`.

### Exercise 3: global Keyword

Create a global variable called `counter = 0`.

Write a function that increases the counter by 1 using `global`.

Call the function three times.

Expected output:

```text
3
```

### Exercise 4: Enclosing Scope

Create an outer function with a variable called `username`.

Create an inner function that prints the username.

### Exercise 5: nonlocal Keyword

Create an outer function with `balance = 1000`.

Create an inner function that updates the balance to 1500 using `nonlocal`.

Print the updated balance from the outer function.

### Exercise 6: LEGB

Predict the output:

```python
name = "Global"

def outer():
    name = "Enclosing"

    def inner():
        print(name)

    inner()

outer()
```

### Exercise 7: Debugging

Find the problem:

```python
total = 100

def update_total():
    total = total + 50

update_total()

print(total)
```

Explain why it raises an error and correct it.

## 14. Quick Revision

| Concept | Meaning |
|---|---|
| Local scope | Variable defined inside a function |
| Global scope | Variable defined at module level |
| Enclosing scope | Variable defined in an outer function |
| Built-in scope | Python's built-in names |
| `global` | Allows reassignment of a module-level variable |
| `nonlocal` | Allows reassignment of an enclosing function variable |
| LEGB | Local, Enclosing, Global, Built-in |
| Shadowing | Inner variable hides an outer variable with the same name |

## 15. Self-Assessment

You should be able to answer:

1. What is variable scope?
2. What is local scope?
3. What is global scope?
4. Can a function read a global variable?
5. Why do we use the `global` keyword?
6. What is enclosing scope?
7. Why do we use `nonlocal`?
8. What does LEGB stand for?
9. What is variable shadowing?
10. What is the difference between modifying and reassigning a global list?

## Learning Outcome

After completing this chapter, you should understand how Python resolves variable names, how local and global variables behave, and how to use `global`, `nonlocal`, and the LEGB rule.

**Next topic:** Python Closures.
