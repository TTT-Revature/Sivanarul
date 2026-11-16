
# Python type() and Basic Object Inspection

## 1. Introduction

In Python, everything is an object.

Whether we create an integer, string, list, dictionary, function, or class, Python represents it as an object.

As developers, we frequently need to inspect objects to understand:

- What is the data type?
- What value does the object contain?
- What attributes are available?
- What methods can we use?
- Is the object callable?
- Does the object belong to a particular class?

Python provides several built-in functions and techniques to inspect objects.

Some commonly used functions are:

| Function | Purpose |
|---|---|
| `type()` | Identifies the object's type |
| `id()` | Returns the object's identity |
| `isinstance()` | Checks whether an object belongs to a class or its subclass |
| `issubclass()` | Checks whether one class inherits from another |
| `dir()` | Lists available attributes and methods |
| `getattr()` | Retrieves an attribute dynamically |
| `hasattr()` | Checks whether an attribute exists |
| `callable()` | Checks whether an object can be called |
| `vars()` | Returns an object's `__dict__`, when available |
| `repr()` | Returns a developer-oriented string representation |
| `help()` | Displays documentation about an object |

---

## 2. Understanding type()

The `type()` function is used to identify the type of an object.

### Syntax

```python
type(object)
```

### Example 1: Inspecting Basic Data Types

```python
name = "Python"
age = 25
salary = 45000.50
is_active = True

print(type(name))
print(type(age))
print(type(salary))
print(type(is_active))
```

Output:

```text
<class 'str'>
<class 'int'>
<class 'float'>
<class 'bool'>
```

### Explanation

- `name` belongs to the `str` class.
- `age` belongs to the `int` class.
- `salary` belongs to the `float` class.
- `is_active` belongs to the `bool` class.

Notice that Python displays the type in the format:

```text
<class 'data_type'>
```

This indicates that these types are also classes in Python.

### Example 2: Inspecting Collection Types

```python
numbers = [10, 20, 30]
coordinates = (10, 20)
unique_values = {10, 20, 30}
employee = {"name": "John", "age": 25}

print(type(numbers))
print(type(coordinates))
print(type(unique_values))
print(type(employee))
```

Output:

```text
<class 'list'>
<class 'tuple'>
<class 'set'>
<class 'dict'>
```

### Example 3: Inspecting None

```python
result = None

print(type(result))
```

Output:

```text
<class 'NoneType'>
```

`None` represents the absence of a value.

---

## 3. Understanding id()

The `id()` function returns the identity of an object.

### Syntax

```python
id(object)
```

### Example

```python
a = [10, 20, 30]

print(id(a))
```

Output:

```text
140123456789000
```

The number shown above is only an illustrative example. The actual output varies between executions and environments.

### Why Is id() Useful?

It helps us investigate whether two variables refer to the same object.

```python
a = [10, 20, 30]

b = a

print(id(a))
print(id(b))
```

Possible output:

```text
140123456789000
140123456789000
```

Both variables refer to the same object.

Now consider:

```python
a = [10, 20, 30]

b = [10, 20, 30]

print(id(a))
print(id(b))
```

The two objects normally have different identities because they were created separately.

### Important: id() Is Not a Value Comparison

Consider:

```python
a = [10, 20, 30]
b = [10, 20, 30]

print(a == b)
print(a is b)
```

Output:

```text
True
False
```

Explanation:

- `==` checks whether the values are equal.
- `is` checks whether both references point to the same object.
- `id()` helps us inspect object identity.

Important: Do not assume that `id()` is always a physical memory address. Python guarantees an identity value that remains constant during an object's lifetime. Its implementation details can vary.

---

## 4. Understanding isinstance()

The `isinstance()` function checks whether an object belongs to a particular class or its subclass.

### Syntax

```python
isinstance(object, classinfo)
```

### Example 1: Basic Usage

```python
age = 25

print(isinstance(age, int))
print(isinstance(age, str))
```

Output:

```text
True
False
```

### Example 2: Checking Multiple Types

We can pass a tuple of types.

```python
value = 25.5

print(isinstance(value, (int, float)))
```

Output:

```text
True
```

This checks whether the value belongs to either `int` or `float`.

### Example 3: Important Boolean Behaviour

```python
value = True

print(isinstance(value, bool))
print(isinstance(value, int))
```

Output:

```text
True
True
```

Why?

In Python, `bool` is a subclass of `int`.

Therefore:

```python
isinstance(True, int)
```

returns `True`.

If you need to check whether a value is exactly an integer and exclude Boolean values, use:

```python
value = True

print(type(value) is int)
```

Output:

```text
False
```

### type() vs isinstance()

| type() | isinstance() |
|---|---|
| Identifies the exact type | Checks class membership, including subclasses |
| Useful for inspecting exact types | Useful for validation and polymorphism |
| Does not consider subclass membership when checking exact equality | Considers inheritance |

Example:

```python
class Animal:
    pass


class Dog(Animal):
    pass


dog = Dog()

print(type(dog) is Animal)
print(isinstance(dog, Animal))
```

Output:

```text
False
True
```

`Dog` inherits from `Animal`, so the `Dog` object is also an instance of `Animal`.

---

## 5. Understanding dir()

The `dir()` function returns a list of names associated with an object.

These names can include:

- Attributes
- Methods
- Special or dunder methods

### Syntax

```python
dir(object)
```

### Example 1: Inspecting a String

```python
name = "Python"

print(dir(name))
```

The output contains many available string methods and special attributes, including:

```text
'capitalize'
'casefold'
'count'
'endswith'
'find'
'lower'
'replace'
'split'
'strip'
'upper'
```

The complete output is much longer.

### Example 2: Inspecting a List

```python
numbers = [10, 20, 30]

print(dir(numbers))
```

You will find methods such as:

```text
'append'
'clear'
'copy'
'extend'
'insert'
'pop'
'remove'
'reverse'
'sort'
```

### Why Is dir() Useful?

Imagine you receive an unfamiliar object from a third-party library.

You do not know what methods are available.

You can inspect it using:

```python
print(dir(object_name))
```

This helps you discover available attributes and methods.

Important: `dir()` is primarily an inspection aid. It does not guarantee that every listed attribute is directly usable in every situation.

---

## 6. Understanding getattr()

The `getattr()` function retrieves an attribute from an object dynamically.

### Syntax

```python
getattr(object, attribute_name)
```

We can also provide a default value:

```python
getattr(object, attribute_name, default_value)
```

### Example 1: Accessing an Attribute

```python
class Employee:
    def __init__(self):
        self.name = "John"
        self.age = 25


employee = Employee()

print(getattr(employee, "name"))
print(getattr(employee, "age"))
```

Output:

```text
John
25
```

### Example 2: Providing a Default Value

```python
class Employee:
    def __init__(self):
        self.name = "John"


employee = Employee()

print(getattr(employee, "salary", 0))
```

Output:

```text
0
```

Because `salary` does not exist, Python returns the default value `0`.

Without a default value, accessing a missing attribute through `getattr()` raises `AttributeError`.

### Practical Example

Imagine we receive a field name dynamically from an external system.

```python
class Customer:
    def __init__(self):
        self.name = "David"
        self.city = "Chennai"


customer = Customer()

field_name = "city"

value = getattr(customer, field_name, None)

print(value)
```

Output:

```text
Chennai
```

This is useful when building dynamic integrations and configuration-driven applications.

---

## 7. Understanding hasattr()

The `hasattr()` function checks whether an object has a particular attribute.

### Syntax

```python
hasattr(object, attribute_name)
```

### Example

```python
class Employee:
    def __init__(self):
        self.name = "John"
        self.age = 25


employee = Employee()

print(hasattr(employee, "name"))
print(hasattr(employee, "salary"))
```

Output:

```text
True
False
```

### Practical Example

```python
class APIResponse:
    def __init__(self):
        self.status_code = 200
        self.message = "Success"


response = APIResponse()

if hasattr(response, "status_code"):
    print("Status code:", response.status_code)
else:
    print("Status code is unavailable")
```

Output:

```text
Status code: 200
```

This is useful when working with objects whose available attributes may differ.

---

## 8. Understanding callable()

The `callable()` function checks whether an object can be called.

Examples of callable objects include:

- Functions
- Methods
- Classes
- Objects that implement `__call__()`

### Example 1: Function

```python
def greet():
    print("Hello")


print(callable(greet))
```

Output:

```text
True
```

### Example 2: Integer

```python
number = 100

print(callable(number))
```

Output:

```text
False
```

### Example 3: Class

```python
class Employee:
    pass


print(callable(Employee))
```

Output:

```text
True
```

Why?

A class can be called to create an instance.

### Example 4: Callable Object

```python
class Calculator:
    def __call__(self, a, b):
        return a + b


calculator = Calculator()

print(callable(calculator))
print(calculator(10, 20))
```

Output:

```text
True
30
```

An object becomes callable when its class implements the `__call__()` method.

---

## 9. Understanding vars()

The `vars()` function returns the `__dict__` attribute of an object when available.

It is commonly used to inspect an object's instance attributes.

### Example

```python
class Employee:
    def __init__(self, name, age):
        self.name = name
        self.age = age


employee = Employee("John", 25)

print(vars(employee))
```

Output:

```text
{'name': 'John', 'age': 25}
```

### Explanation

When we create an employee object:

```python
employee = Employee("John", 25)
```

Python stores the instance attributes in the object's instance dictionary in this example.

We can inspect them using:

```python
vars(employee)
```

Important:

- `vars()` does not work for every object.
- Some objects do not have a `__dict__` attribute.
- Objects using `__slots__` may not have an instance dictionary.

---

## 10. Understanding repr()

The `repr()` function returns a developer-oriented string representation of an object.

It is useful for debugging and inspecting values.

### Example 1: String

```python
name = "Python"

print(str(name))
print(repr(name))
```

Output:

```text
Python
'Python'
```

Notice the difference:

- `str()` produces a user-friendly representation.
- `repr()` produces a representation intended to be useful for developers.

### Example 2: Custom Object

```python
class Employee:
    def __init__(self, name):
        self.name = name

    def __repr__(self):
        return f"Employee(name={self.name!r})"


employee = Employee("John")

print(repr(employee))
```

Output:

```text
Employee(name='John')
```

The `__repr__()` method allows developers to define how an object should be represented.

---

## 11. Understanding help()

The `help()` function displays documentation about Python objects, functions, classes, and modules.

### Example 1: Built-in Function

```python
help(len)
```

This displays documentation about the `len()` function.

### Example 2: String Methods

```python
help(str)
```

This displays documentation for the string class.

### Example 3: Custom Class

```python
class Employee:
    """Represents an employee."""

    def display(self):
        """Displays employee information."""
        print("Employee details")


help(Employee)
```

Python displays the available documentation for the class and its members.

You can also inspect a particular method:

```python
help(Employee.display)
```

---

## 12. Practical Example: Object Inspection Toolkit

Let's combine several inspection functions into one example.

```python
class Employee:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def display(self):
        return f"{self.name} is {self.age} years old"


employee = Employee("John", 25)

print("Type:", type(employee))

print("Identity:", id(employee))

print("Is Employee:", isinstance(employee, Employee))

print("Has name:", hasattr(employee, "name"))

print("Name:", getattr(employee, "name"))

print("Attributes:", vars(employee))

print("Callable:", callable(employee))

print("Available members:", dir(employee))
```

Possible output:

```text
Type: <class '__main__.Employee'>
Identity: 140123456789000
Is Employee: True
Has name: True
Name: John
Attributes: {'name': 'John', 'age': 25}
Callable: False
Available members: [...]
```

The identity value and complete `dir()` output vary between executions and environments.

### What Did We Learn?

| Function | What We Inspected |
|---|---|
| `type()` | Object type |
| `id()` | Object identity |
| `isinstance()` | Class membership |
| `hasattr()` | Attribute existence |
| `getattr()` | Attribute value |
| `vars()` | Instance attributes |
| `callable()` | Whether the object can be called |
| `dir()` | Available names |

---

## 13. Object Inspection in Forward-Deployed Engineering

As an FDE, you may need to integrate unfamiliar libraries, APIs, SDKs, and third-party systems.

You cannot always assume that an object contains the attributes you expect.

Object inspection helps you understand the structure of unfamiliar objects.

### Example: Inspecting an API Client Object

Imagine a third-party library provides a client object.

```python
class APIClient:
    def __init__(self):
        self.base_url = "https://api.example.com"
        self.timeout = 30

    def connect(self):
        print("Connecting to API")


client = APIClient()

print(type(client))

print(dir(client))

print(vars(client))

if hasattr(client, "base_url"):
    print(getattr(client, "base_url"))
```

Output includes:

```text
<class '__main__.APIClient'>
{'base_url': 'https://api.example.com', 'timeout': 30}
https://api.example.com
```

The `dir()` output contains the available names, including methods and special attributes.

### Why Does This Matter?

Suppose you integrate a new AI SDK.

You may need to investigate:

- What type of object does the SDK return?
- Does the response contain a `status` attribute?
- Does the object have a `content` attribute?
- Which methods are available?
- Is the returned object callable?
- What information is stored inside it?

These inspection techniques help you understand unfamiliar objects before writing integration logic.

Important: Object inspection is useful during development and debugging, but production code should rely on documented interfaces and explicit validation rather than depending blindly on implementation details.

---

## 14. Common Mistakes

### Mistake 1: Confusing type() and isinstance()

```python
class Animal:
    pass


class Dog(Animal):
    pass


dog = Dog()

print(type(dog) is Animal)
print(isinstance(dog, Animal))
```

Output:

```text
False
True
```

Reason: `Dog` inherits from `Animal`.

### Mistake 2: Using is Instead of ==

Incorrect:

```python
a = [10, 20]
b = [10, 20]

print(a is b)
```

Output:

```text
False
```

Correct for comparing values:

```python
print(a == b)
```

Output:

```text
True
```

### Mistake 3: Assuming dir() Returns Only Methods

```python
numbers = [10, 20, 30]

print(dir(numbers))
```

`dir()` returns attribute names and methods, including special methods. It is not limited to callable methods.

### Mistake 4: Assuming vars() Works on Everything

```python
number = 100

print(vars(number))
```

This raises `TypeError` because an integer does not have an instance `__dict__`.

### Mistake 5: Assuming callable() Guarantees Successful Execution

```python
def greet(name):
    print("Hello", name)


print(callable(greet))
```

Output:

```text
True
```

However, calling `greet()` without the required argument still raises `TypeError`.

`callable()` only checks whether an object is callable. It does not validate the arguments required by that object.

---

## 15. Quick Revision

| Function | Purpose | Example |
|---|---|---|
| `type()` | Identify object type | `type(100)` |
| `id()` | Inspect object identity | `id(name)` |
| `isinstance()` | Check class membership | `isinstance(10, int)` |
| `issubclass()` | Check inheritance relationship | `issubclass(Dog, Animal)` |
| `dir()` | List available names | `dir(list)` |
| `getattr()` | Retrieve an attribute | `getattr(obj, "name")` |
| `hasattr()` | Check attribute existence | `hasattr(obj, "name")` |
| `callable()` | Check whether object is callable | `callable(print)` |
| `vars()` | Inspect instance dictionary | `vars(obj)` |
| `repr()` | Get developer-oriented representation | `repr(obj)` |
| `help()` | Display documentation | `help(str)` |

---

## 16. Practice Exercises

Try solving these exercises without looking at the examples.

### Exercise 1: Basic Type Inspection

Create variables containing:

- An integer
- A float
- A string
- A list
- A dictionary
- A Boolean

Use `type()` to inspect every variable.

### Exercise 2: Object Identity

Create two variables that refer to the same list.

Use:

- `id()`
- `==`
- `is`

Explain the output.

### Exercise 3: isinstance()

Create a variable containing `True`.

Check whether it belongs to:

- `bool`
- `int`
- `str`

Explain why the results are different.

### Exercise 4: dir()

Create a string variable.

Use `dir()` to inspect its available methods.

Identify five methods and try using them.

### Exercise 5: getattr() and hasattr()

Create an Employee class containing:

- name
- age
- department

Check whether the employee has a salary attribute.

Retrieve the salary using `getattr()` with a default value.

### Exercise 6: callable()

Create a normal function and a class.

Use `callable()` to inspect both.

Then create an object with a `__call__()` method and inspect it.

### Exercise 7: Object Inspection Toolkit

Create a Customer class with:

- customer_id
- name
- city

Create an object and inspect it using:

- `type()`
- `id()`
- `isinstance()`
- `dir()`
- `vars()`
- `hasattr()`
- `getattr()`

---

## 17. Self-Assessment Questions

1. What is an object in Python?
2. What does the `type()` function return?
3. What is the difference between `type()` and `isinstance()`?
4. What does the `id()` function represent?
5. What is the difference between `==` and `is`?
6. What information does `dir()` provide?
7. What is the purpose of `getattr()`?
8. How is `hasattr()` different from `getattr()`?
9. What does `callable()` check?
10. What does `vars()` return?
11. What is the difference between `str()` and `repr()`?
12. Why are object inspection techniques useful when integrating third-party libraries?

---

## 18. Key Takeaways

- Everything in Python is an object.
- Every object has a type, identity, and value.
- `type()` identifies the object's type.
- `id()` returns the object's identity.
- `isinstance()` checks class membership, including inheritance.
- `dir()` helps discover available attributes and methods.
- `getattr()` retrieves attributes dynamically.
- `hasattr()` checks whether an attribute exists.
- `callable()` checks whether an object can be called.
- `vars()` helps inspect an object's instance dictionary.
- `repr()` provides a developer-oriented representation.
- `help()` provides documentation.

---

## 19. Learning Progress

**Completed Topic:** Python type() and Basic Object Inspection

**Suggested Next Topic:** Python Operators

