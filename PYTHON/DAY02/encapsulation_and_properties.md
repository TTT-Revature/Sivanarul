# Python Encapsulation and Properties (`@property`)

---

## 1. What is Encapsulation?

**Encapsulation** is the OOP principle of restricting direct access to an object's internal data, preventing accidental or unauthorized modification.

Python convention uses underscores to signal visibility:
- **Public:** `self.name` (accessible anywhere).
- **Protected:** `self._balance` (intended for internal/subclass use only).
- **Private (Name Mangling):** `self.__secret` (Python transforms name to `_ClassName__secret`).

---

## 2. Pythonic Getters and Setters with `@property`

Instead of verbose Java-style `getBalance()` and `setBalance()` methods, Python uses the `@property` decorator to expose methods as clean attributes with transparent validation.

```python
class BankAccount:
    def __init__(self, owner, balance):
        self.owner = owner
        self._balance = balance  # Protected attribute

    # Getter property
    @property
    def balance(self):
        """Retrieve account balance."""
        return self._balance

    # Setter property with validation
    @balance.setter
    def balance(self, value):
        if value < 0:
            raise ValueError("Balance cannot be negative!")
        self._balance = value

account = BankAccount("Sivanarul", 1000.0)

# Access balance like a regular attribute
print("Current Balance: $", account.balance)

# Update balance cleanly
account.balance = 1500.0
print("Updated Balance: $", account.balance)

# Validation triggers on invalid value
try:
    account.balance = -200
except ValueError as e:
    print("Update blocked:", e)
```

**Output:**

```text
Current Balance: $ 1000.0
Updated Balance: $ 1500.0
Update blocked: Balance cannot be negative!
```

---

## 3. Read-Only Properties

If you define `@property` without a corresponding `@setter`, the attribute becomes strictly **read-only**:

```python
class Circle:
    def __init__(self, radius):
        self.radius = radius

    @property
    def area(self):
        import math
        return math.pi * (self.radius ** 2)

c = Circle(5)
print(f"Area: {c.area:.2f}")

try:
    c.area = 50  # Attempting to assign raises AttributeError
except AttributeError as e:
    print("Error:", e)
```

**Output:**

```text
Area: 78.54
Error: property 'area' of 'Circle' object has no setter
```
