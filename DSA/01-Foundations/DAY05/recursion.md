# Recursion

---

## 1. What is Recursion?

A function that **calls itself** with a smaller version of the same problem until it hits a **base case**.

```mermaid
graph TD
    Call["factorial(4)"] --> C2["4 × factorial(3)"]
    C2 --> C3["3 × factorial(2)"]
    C3 --> C4["2 × factorial(1)"]
    C4 --> Base["1 → BASE CASE returns 1"]
    Base --> R1["Returns 1×1 = 1"]
    R1 --> R2["Returns 2×1 = 2"]
    R2 --> R3["Returns 3×2 = 6"]
    R3 --> R4["Returns 4×6 = 24 ✅"]
```

---

## 2. The 2 Laws of Recursion

1. **Must have a base case** — the stopping condition.
2. **Must move toward the base case** — each call reduces the problem.

```python
def factorial(n):
    # Base case
    if n == 0 or n == 1:
        return 1
    # Recursive case — moves toward base (n decreases)
    return n * factorial(n - 1)

print(factorial(5))   # 120
```

**Output:**

```text
120
```

---

## 3. The Call Stack

Each call creates a **stack frame**. Frames stack up → then unwind on return.

```mermaid
sequenceDiagram
    participant M as main
    participant F3 as factorial(3)
    participant F2 as factorial(2)
    participant F1 as factorial(1)
    M->>F3: call factorial(3)
    F3->>F2: call factorial(2)
    F2->>F1: call factorial(1)
    F1-->>F2: return 1 (base)
    F2-->>F3: return 2×1 = 2
    F3-->>M: return 3×2 = 6
```

---

## 4. Classic Examples

### Sum of List

```python
def sum_list(arr):
    if not arr:              # Base case: empty list
        return 0
    return arr[0] + sum_list(arr[1:])   # Shrinks list each call

print(sum_list([1, 2, 3, 4]))   # 10
```

### Fibonacci (Naive)

```python
def fib(n):
    if n <= 1: return n                 # Base cases
    return fib(n-1) + fib(n-2)         # Two recursive branches

print(fib(6))   # 8
```

---

## 5. Recursion vs Iteration

| Feature | Recursion | Iteration |
|---|---|---|
| **Readability** | Often cleaner for tree/graph problems | Cleaner for simple loops |
| **Memory** | O(n) stack frames | O(1) extra space |
| **Risk** | Stack overflow on deep input | No stack overflow risk |
| **Best for** | Trees, divide-and-conquer, backtracking | Linear scans, simple accumulation |

---

## 6. Tail Recursion

The recursive call is the **last** operation — some compilers optimize this to avoid extra stack frames.

```python
def factorial_tail(n, accumulator=1):
    if n == 0: return accumulator
    return factorial_tail(n - 1, n * accumulator)   # Last op = recursive call

print(factorial_tail(5))   # 120
```

---

## 7. Avoiding Redundant Work — Memoization

```python
from functools import lru_cache

@lru_cache(maxsize=None)
def fib_memo(n):
    if n <= 1: return n
    return fib_memo(n-1) + fib_memo(n-2)

print(fib_memo(40))   # Very fast — O(n) time and space
```

---

## 8. Common Recursion Pitfalls

```mermaid
flowchart TD
    P1["Missing base case → Infinite recursion → Stack Overflow"]
    P2["Not reducing problem → Never reaches base case"]
    P3["Recomputing subproblems → Exponential time"]
    P1 --> Fix1["Add if n <= 0: return"]
    P2 --> Fix2["Ensure each call shrinks n"]
    P3 --> Fix3["Use @lru_cache or memoization"]
```
