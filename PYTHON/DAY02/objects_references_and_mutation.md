# Python Objects, References, and Mutation

---

## 1. Everything is an Object

In Python, variables do not store values directly; they store **references (pointers)** to objects allocated in memory.

### Memory Address Inspection (`id()`):
The built-in `id(obj)` function returns the unique integer representing an object's memory address.

```python
a = [1, 2, 3]
b = a  # Copies reference, NOT the object!

print("id(a):", id(a))
print("id(b):", id(b))
print("a is b:", a is b)
```

**Output:**

```text
id(a): 2154388373440
id(b): 2154388373440
a is b: True
```

---

## 2. Mutability in Shared References

Because `a` and `b` point to the identical list in memory, mutating through `b` alters `a`:

```python
b.append(99)
print("a:", a)
print("b:", b)
```

**Output:**

```text
a: [1, 2, 3, 99]
b: [1, 2, 3, 99]
```

---

## 3. Function Arguments: Call by Object Reference

Python uses **Call by Object Reference** (or Call by Assignment).
- Reassigning parameter names inside a function does not affect the outer variable.
- Mutating a mutable object passed into a function alters the caller's object!

```python
def add_item(target_list):
    target_list.append("NEW")

fruits = ["apple", "banana"]
add_item(fruits)
print("fruits after function call:", fruits)
```

**Output:**

```text
fruits after function call: ['apple', 'banana', 'NEW']
```
