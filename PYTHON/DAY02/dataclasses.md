# Python Dataclasses (`@dataclass`)

---

## 1. What is a Dataclass?

Introduced in Python 3.7, the `@dataclass` decorator from the `dataclasses` module automatically generates boilerplate special methods such as `__init__()`, `__repr__()`, and `__eq__()` based on class type annotations.

---

## 2. Standard Class vs Dataclass

### Traditional Class (Boilerplate-heavy):
```python
class User:
    def __init__(self, id, name, email):
        self.id = id
        self.name = name
        self.email = email
    def __repr__(self):
        return f"User(id={self.id}, name='{self.name}', email='{self.email}')"
```

### With `@dataclass` (Clean & Pythonic):
```python
from dataclasses import dataclass

@dataclass
class User:
    id: int
    name: str
    email: str
    role: str = "Viewer"  # Default argument

u1 = User(101, "Sivanarul", "siva@example.com")
u2 = User(101, "Sivanarul", "siva@example.com")

print(u1)               # Auto-generated readable __repr__!
print("Equality test:", u1 == u2)  # Auto-generated __eq__!
```

**Output:**

```text
User(id=101, name='Sivanarul', email='siva@example.com', role='Viewer')
Equality test: True
```

---

## 3. Frozen Dataclasses (Immutability)

Setting `frozen=True` makes instances immutable and hashable (can be used as dictionary keys or set elements):

```python
from dataclasses import dataclass

@dataclass(frozen=True)
class Point:
    x: float
    y: float

p = Point(10.0, 20.0)

try:
    p.x = 15.0  # Attempting mutation raises FrozenInstanceError
except Exception as e:
    print("Cannot modify:", type(e).__name__)
```

**Output:**

```text
Cannot modify: FrozenInstanceError
```
