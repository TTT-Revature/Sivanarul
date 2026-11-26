# The `super()` Function in Python

---

## 1. What is `super()`?

The built-in **`super()`** function returns a proxy object that delegates method calls to a parent or sibling class in the inheritance hierarchy.

It is most commonly used in:
1. Subclass constructors (`__init__`) to invoke the parent constructor without hardcoding the parent's class name.
2. Extending inherited methods rather than replacing them entirely.

---

## 2. Using `super()` in Subclass Initialization

```python
class Vehicle:
    def __init__(self, make, model):
        self.make = make
        self.model = model
        print("-> Vehicle initialized")

class ElectricCar(Vehicle):
    def __init__(self, make, model, battery_kwh):
        # Delegate make and model initialization to Vehicle
        super().__init__(make, model)
        self.battery_kwh = battery_kwh
        print("-> ElectricCar initialized")

car = ElectricCar("Tesla", "Model Y", 75)
print(f"Details: {car.make} {car.model} with {car.battery_kwh}kWh battery")
```

**Output:**

```text
-> Vehicle initialized
-> ElectricCar initialized
Details: Tesla Model Y with 75kWh battery
```

---

## 3. Extending Methods with `super()`

```python
class Logger:
    def log(self, message):
        print(f"[LOG]: {message}")

class TimestampLogger(Logger):
    def log(self, message):
        from datetime import datetime
        timestamp = datetime.now().strftime("%H:%M:%S")
        # Call original parent implementation
        super().log(f"{timestamp} - {message}")

ts_logger = TimestampLogger()
ts_logger.log("System startup completed.")
```

**Output:**

```text
[LOG]: 15:35:00 - System startup completed.
```

---

## 4. Method Resolution Order (MRO)

Python uses the C3 Linearization algorithm to determine the Method Resolution Order (MRO) in multiple inheritance:

```python
print(ElectricCar.__mro__)
```
