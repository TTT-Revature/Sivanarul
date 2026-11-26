# Python Attributes, Methods, `__init__`, and `self`

---

## 1. The Role of `__init__` and `self`

### What is `__init__`?
`__init__` is the constructor method in Python. It automatically executes whenever a new object instance is instantiated from a class, setting up its initial state.

### What is `self`?
`self` represents the **specific instance** of the class currently being operated on. It allows methods to access and modify the attributes of that particular object.

> **Note:** `self` is explicitly passed as the first parameter in instance methods, but Python supplies it automatically upon invocation (`obj.method()` translates to `Class.method(obj)`).

---

## 2. Instance vs Class Attributes

- **Instance Attributes:** Belong exclusively to one object. Defined with `self.attribute_name` inside `__init__`.
- **Class Attributes:** Belong to the class itself and are shared across all instances.

```python
class Employee:
    # Class attribute (shared)
    company_name = "Revature"

    def __init__(self, emp_id, name, salary):
        # Instance attributes (distinct per employee)
        self.emp_id = emp_id
        self.name = name
        self.salary = salary

    def give_raise(self, percentage):
        self.salary += self.salary * (percentage / 100)
        return self.salary

# Instantiate employees
emp1 = Employee(101, "Sivanarul", 75000)
emp2 = Employee(102, "Priya", 65000)

print(f"{emp1.name} works at {emp1.company_name} earning ${emp1.salary}")
print(f"{emp2.name} works at {emp2.company_name} earning ${emp2.salary}")

# Modifying instance attribute
emp1.give_raise(10)
print(f"New salary for {emp1.name}: ${emp1.salary}")
```

**Output:**

```text
Sivanarul works at Revature earning $75000
Priya works at Revature earning $65000
New salary for Sivanarul: $82500.0
```

---

## 3. Summary

- `__init__` initializes object attributes upon creation.
- `self` binds attributes and methods to the specific object instance.
