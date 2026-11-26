# Python Inheritance and Method Overriding

---

## 1. What is Inheritance?

**Inheritance** allows a child class (subclass) to inherit attributes and methods from a parent class (superclass), promoting code reuse and establishing an *is-a* relationship.

```text
       [Employee]          <-- Superclass / Parent
           |
     +-----+-----+
     |           |
[Developer]  [Manager]     <-- Subclasses / Children
```

---

## 2. Basic Inheritance

```python
class Employee:
    def __init__(self, name, emp_id):
        self.name = name
        self.emp_id = emp_id

    def get_role(self):
        return "General Employee"

class Developer(Employee):
    pass

dev = Developer("Sivanarul", 101)
print(f"Employee: {dev.name}, Role: {dev.get_role()}")
```

**Output:**

```text
Employee: Sivanarul, Role: General Employee
```

---

## 3. Method Overriding

**Method overriding** occurs when a subclass provides its own specific implementation of a method that is already defined in its parent class.

```python
class Employee:
    def __init__(self, name, base_salary):
        self.name = name
        self.base_salary = base_salary

    def calculate_pay(self):
        return self.base_salary

class Developer(Employee):
    def __init__(self, name, base_salary, overtime_hours):
        super().__init__(name, base_salary)
        self.overtime_hours = overtime_hours

    # Overriding parent's calculate_pay method
    def calculate_pay(self):
        overtime_pay = self.overtime_hours * 50.0
        return self.base_salary + overtime_pay

class Manager(Employee):
    def __init__(self, name, base_salary, team_bonus):
        super().__init__(name, base_salary)
        self.team_bonus = team_bonus

    # Overriding parent's calculate_pay method
    def calculate_pay(self):
        return self.base_salary + self.team_bonus

dev = Developer("Siva", 75000, 10)
mgr = Manager("Priya", 85000, 15000)

print(f"Developer Pay: ${dev.calculate_pay()}")
print(f"Manager Pay:   ${mgr.calculate_pay()}")
```

**Output:**

```text
Developer Pay: $75500.0
Manager Pay:   $100000
```
