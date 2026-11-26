# Instance, Class, and Static Methods in Python

---

## 1. Introduction

Python classes support three distinct types of methods, each bound to a different scope and designated with different decorators:

| Method Type | Decorator | First Parameter | Access Scope |
|---|:---:|:---:|---|
| **Instance Method** | None (Default) | `self` | Accesses & modifies individual instance state. |
| **Class Method** | `@classmethod` | `cls` | Accesses & modifies class-wide state; alternative constructors. |
| **Static Method** | `@staticmethod` | None | Self-contained utility; does not touch instance (`self`) or class (`cls`). |

---

## 2. Comprehensive Code Example

```python
class Employee:
    base_salary = 50000.0  # Class attribute

    def __init__(self, name, bonus):
        self.name = name
        self.bonus = bonus

    # 1. Instance Method (acts on self)
    def calculate_total_salary(self):
        return self.base_salary + self.bonus

    # 2. Class Method (acts on cls)
    @classmethod
    def set_base_salary(cls, new_base):
        cls.base_salary = new_base

    # Alternative constructor via classmethod
    @classmethod
    def from_string(cls, emp_str):
        name, bonus_str = emp_str.split("-")
        return cls(name.strip(), float(bonus_str.strip()))

    # 3. Static Method (independent utility function)
    @staticmethod
    def is_valid_bonus(bonus):
        return bonus >= 0

# --- Demonstration ---

# Calling static method (without needing an instance)
print("Is 5000 valid bonus?", Employee.is_valid_bonus(5000))

# Creating an instance using standard __init__
emp1 = Employee("Arun", 8000.0)
print(f"{emp1.name} total: ${emp1.calculate_total_salary()}")

# Creating an instance using alternative constructor classmethod
emp2 = Employee.from_string("Sivanarul - 12000")
print(f"{emp2.name} total: ${emp2.calculate_total_salary()}")

# Modifying class attribute via classmethod
Employee.set_base_salary(60000.0)
print(f"Updated base salary: {emp1.name} now earns ${emp1.calculate_total_salary()}")
```

**Output:**

```text
Is 5000 valid bonus? True
Arun total: $58000.0
Sivanarul total: $62000.0
Updated base salary: Arun now earns $68000.0
```
