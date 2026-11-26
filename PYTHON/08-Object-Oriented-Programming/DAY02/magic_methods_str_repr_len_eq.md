# Python Special (Dunder) Methods: `__str__`, `__repr__`, `__len__`, and `__eq__`

---

## 1. Introduction to Magic / Dunder Methods

**Dunder methods** (Double Underscore methods) are special built-in methods in Python that overload standard operators and integrate user-defined classes with built-in functions.

---

## 2. `__str__` vs `__repr__`

| Method | Intended Audience | Purpose | Triggered By |
|---|---|---|---|
| `__str__` | End Users | Human-friendly, readable string representation | `print(obj)`, `str(obj)` |
| `__repr__` | Developers | Unambiguous representation, often valid Python code to recreate the object | In REPL, `repr(obj)`, logs |

---

## 3. `__len__` and `__eq__`

- `__len__`: Defines custom behavior for `len(obj)`.
- `__eq__`: Defines equality comparison `obj1 == obj2` (defaults to checking memory address `is`).

---

## 4. Comprehensive Example

```python
class Book:
    def __init__(self, title, author, pages):
        self.title = title
        self.author = author
        self.pages = pages

    # Readable string for users
    def __str__(self):
        return f"'{self.title}' by {self.author}"

    # Official developer representation
    def __repr__(self):
        return f"Book(title='{self.title}', author='{self.author}', pages={self.pages})"

    # Custom length
    def __len__(self):
        return self.pages

    # Equality check
    def __eq__(self, other):
        if isinstance(other, Book):
            return self.title == other.title and self.author == other.author
        return False

b1 = Book("Fluent Python", "Luciano Ramalho", 800)
b2 = Book("Fluent Python", "Luciano Ramalho", 800)
b3 = Book("Clean Code", "Robert C. Martin", 464)

# __str__ and __repr__
print(str(b1))   # 'Fluent Python' by Luciano Ramalho
print(repr(b1))  # Book(title='Fluent Python', author='Luciano Ramalho', pages=800)

# __len__
print(f"Book length: {len(b1)} pages")

# __eq__
print("Is b1 == b2?", b1 == b2)  # True (values match)
print("Is b1 == b3?", b1 == b3)  # False
```

**Output:**

```text
'Fluent Python' by Luciano Ramalho
Book(title='Fluent Python', author='Luciano Ramalho', pages=800)
Book length: 800 pages
Is b1 == b2? True
Is b1 == b3? False
```
