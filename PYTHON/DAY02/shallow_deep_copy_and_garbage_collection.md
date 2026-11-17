# Python Shallow Copy, Deep Copy, and Garbage Collection

---

## 1. Shallow Copy vs Deep Copy

When copying objects containing nested structures:

- **Shallow Copy (`copy.copy()`):** Duplicates the top-level container, but copies references to the nested objects.
- **Deep Copy (`copy.deepcopy()`):** Recursively duplicates the container and all nested objects, creating complete independent duplicates.

```python
import copy

original = [[1, 2], [3, 4]]

# Create copies
shallow = copy.copy(original)
deep = copy.deepcopy(original)

# Modify nested element in original
original[0].append(99)

print("Original: ", original)
print("Shallow:  ", shallow)  # Affected!
print("Deep Copy:", deep)     # Completely isolated!
```

**Output:**

```text
Original:  [[1, 2, 99], [3, 4]]
Shallow:   [[1, 2, 99], [3, 4]]
Deep Copy: [[1, 2], [3, 4]]
```

---

## 2. Python Garbage Collection (GC)

Python manages memory automatically using two primary mechanisms:

1. **Reference Counting:** Every object has an internal count of how many references point to it. When an object's reference count drops to `0`, its memory is reclaimed immediately.
2. **Generational Garbage Collector (`gc` module):** Detects and cleans up **cyclic references** (e.g., Object A references Object B, and Object B references Object A).

```python
import sys
import gc

# Inspecting reference count
x = [10, 20]
print("Ref count:", sys.getrefcount(x))  # Includes argument reference

# Triggering manual collection
collected = gc.collect()
print("Garbage collector reclaimed objects:", collected)
```

**Output:**

```text
Ref count: 2
Garbage collector reclaimed objects: 0
```
