# Python Nested Functions and Closures

---

## 1. Nested Functions (Inner Functions)

In Python, functions are first-class citizens: they can be defined inside other functions, passed as arguments, and returned as values.

A function defined inside another function is called a **nested (inner) function**.

```python
def outer(name):
    # Inner helper function
    def greet():
        return f"Hello, {name}!"
    
    return greet()

print(outer("Sivanarul"))
```

**Output:**

```text
Hello, Sivanarul!
```

---

## 2. What is a Closure?

A **closure** is an inner function that remembers and retains access to variables from its enclosing lexical scope, even after the outer function has finished executing and returned.

### Three Criteria for a Closure:
1. Must have a nested function.
2. The nested function must reference a variable in the enclosing scope.
3. The outer function must return the nested function object.

```python
def make_multiplier(factor):
    # factor is captured from enclosing scope
    def multiply(number):
        return number * factor
    return multiply

# Create specialized multiplier functions
double = make_multiplier(2)
triple = make_multiplier(3)

print("Double 5:", double(5))
print("Triple 5:", triple(5))
```

**Output:**

```text
Double 5: 10
Triple 5: 15
```

---

## 3. The `nonlocal` Keyword

To modify a variable from the enclosing function's scope inside the nested function, use `nonlocal`:

```python
def make_counter():
    count = 0
    def counter():
        nonlocal count
        count += 1
        return count
    return counter

c1 = make_counter()
print(c1())  # 1
print(c1())  # 2
print(c1())  # 3
```

**Output:**

```text
1
2
3
```

---

## 4. Why Use Closures?

- **Data Encapsulation:** Provides lightweight private variables without declaring full OOP classes.
- **Function Factories:** Creating customizable utility functions.
- **Foundation for Decorators:** Python decorators are built directly upon closures.
