# Raising and Creating Custom Exceptions in Python

---

## 1. Raising Built-in Exceptions (`raise`)

You can trigger exceptions intentionally using the `raise` keyword when inputs violate application business rules:

```python
def set_age(age):
    if not isinstance(age, int):
        raise TypeError(f"Age must be an integer, got {type(age).__name__}")
    if age < 0 or age > 150:
        raise ValueError(f"Invalid age value: {age}. Must be between 0 and 150.")
    return f"Age accepted: {age}"

try:
    print(set_age(-5))
except ValueError as err:
    print("Caught validation error:", err)
```

**Output:**

```text
Caught validation error: Invalid age value: -5. Must be between 0 and 150.
```

---

## 2. Creating Custom Exceptions

To define domain-specific exceptions, create a class that inherits from Python's built-in `Exception` (or a specific child like `ValueError`):

```python
# Custom Base Application Exception
class BankingError(Exception):
    """Base exception for banking application errors."""
    pass

class InsufficientFundsError(BankingError):
    """Raised when an account balance is insufficient for withdrawal."""
    def __init__(self, current_balance, withdrawal_amount):
        self.current_balance = current_balance
        self.withdrawal_amount = withdrawal_amount
        message = (f"Insufficient funds: Attempted to withdraw ${withdrawal_amount:.2f}, "
                   f"but current balance is only ${current_balance:.2f}.")
        super().__init__(message)
```

---

## 3. Using Custom Exceptions

```python
class BankAccount:
    def __init__(self, balance):
        self.balance = balance

    def withdraw(self, amount):
        if amount > self.balance:
            raise InsufficientFundsError(self.balance, amount)
        self.balance -= amount
        return self.balance

account = BankAccount(200.0)

try:
    account.withdraw(500.0)
except InsufficientFundsError as e:
    print("Transaction Failed!")
    print("Reason:", e)
    print("Shortfall:", e.withdrawal_amount - e.current_balance)
```

**Output:**

```text
Transaction Failed!
Reason: Insufficient funds: Attempted to withdraw $500.00, but current balance is only $200.00.
Shortfall: 300.0
```

---

## 4. Best Practices

- Always inherit from `Exception`, **never** directly from `BaseException`.
- Name custom exceptions with the `Error` suffix (e.g., `ValidationError`, `AuthError`).
- Attach contextual metadata (e.g., balance, order_id) as class attributes for rich logging.
