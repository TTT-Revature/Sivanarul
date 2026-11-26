# Python Classes and Objects (OOP Basics)

---

## 1. What are Classes and Objects?

Python is an Object-Oriented Programming (OOP) language:

- **Class:** A user-defined blueprint or template that defines attributes and behaviors.
- **Object (Instance):** A concrete instance created from that class blueprint.

### Real-World Analogy:
A **Blueprint** of a house defines the structure (doors, windows, rooms). The **House** built on a specific lot is the actual object.

---

## 2. Defining a Class and Instantiating Objects

```python
class Car:
    # Class attribute (shared by all instances)
    wheels = 4

    # Initializer method (constructor)
    def __init__(self, brand, model, year):
        # Instance attributes (unique to each instance)
        self.brand = brand
        self.model = model
        self.year = year

    # Instance method
    def start_engine(self):
        return f"{self.brand} {self.model}'s engine is running!"

# Creating instances (objects)
car1 = Car("Toyota", "Corolla", 2022)
car2 = Car("Tesla", "Model 3", 2024)

# Accessing attributes
print(f"Car 1: {car1.brand} {car1.model} ({car1.year})")
print(f"Car 2: {car2.brand} {car2.model} ({car2.year})")

# Calling methods
print(car1.start_engine())
print(car2.start_engine())
```

**Output:**

```text
Car 1: Toyota Corolla (2022)
Car 2: Tesla Model 3 (2024)
Toyota Corolla's engine is running!
Tesla Model 3's engine is running!
```

---

## 3. Checking Types and Instances

Use `isinstance()` and `type()` to inspect objects:

```python
print("Is car1 a Car?", isinstance(car1, Car))
print("Is car1 an object?", isinstance(car1, object))
```

**Output:**

```text
Is car1 a Car? True
Is car1 an object? True
```
