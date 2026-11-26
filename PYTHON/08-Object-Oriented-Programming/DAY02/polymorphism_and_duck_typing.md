# Python Polymorphism and Duck Typing

---

## 1. What is Polymorphism?

**Polymorphism** (Greek for "many forms") is the ability of different objects to respond to the same method call in their own specific way.

---

## 2. What is Duck Typing?

Python is dynamically typed and adheres to the famous philosophy:

> *"If it walks like a duck and quacks like a duck, it's a duck."*

In Python, code does not check an object's explicit class type or inheritance tree; it checks whether the object **implements the expected behavior (methods or attributes)**.

---

## 3. Duck Typing Code Example

```python
class CreditCardProcessor:
    def process_payment(self, amount):
        return f"Charged ${amount:.2f} via Credit Card."

class PayPalProcessor:
    def process_payment(self, amount):
        return f"Redirected to PayPal: Paid ${amount:.2f}."

class CryptoProcessor:
    def process_payment(self, amount):
        return f"Transferred ${amount:.2f} equivalent in BTC."

# Notice this checkout function does NOT care about inheritance!
def checkout(payment_service, total):
    print("Initiating checkout...")
    result = payment_service.process_payment(total)
    print("Status:", result)

# Any object providing .process_payment() works seamlessly!
checkout(CreditCardProcessor(), 120.00)
checkout(PayPalProcessor(), 45.50)
checkout(CryptoProcessor(), 500.00)
```

**Output:**

```text
Initiating checkout...
Status: Charged $120.00 via Credit Card.
Initiating checkout...
Status: Redirected to PayPal: Paid $45.50.
Initiating checkout...
Status: Transferred $500.00 equivalent in BTC.
```

---

## 4. Polymorphism with Built-in Functions

Built-in functions like `len()` demonstrate polymorphism:

```python
print(len("Python"))       # 6 (String)
print(len([10, 20, 30]))   # 3 (List)
print(len({"a": 1, "b": 2})) # 2 (Dict)
```
Each object simply implements its own `__len__()` method.
