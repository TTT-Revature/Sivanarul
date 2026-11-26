# Algorithm Analysis – Why and How Algorithms Are Evaluated

**Language used for examples:** Python

## 1. What Is Algorithm Analysis?

Algorithm analysis is the process of evaluating an algorithm to understand how efficiently it solves a problem.

We mainly study:

- **Time complexity:** How the number of operations grows as input size increases.
- **Space complexity:** How the memory requirement grows as input size increases.

In simple terms:

> Algorithm analysis helps us understand how an algorithm behaves when the input becomes larger.

It is not just about checking whether the code produces the correct answer. We also want to know whether it does so efficiently.

## 2. Why Do We Analyse Algorithms?

Imagine two algorithms that both find an employee ID from a collection of one million employee records.

Both may return the correct employee, but one might perform far fewer operations.

We analyse algorithms to:

1. Compare different solutions to the same problem.
2. Predict performance for large inputs.
3. Avoid unnecessary processing.
4. Reduce memory consumption.
5. Build applications that can scale.
6. Make informed choices about data structures and algorithms.

### Real-world analogy

Imagine two people travelling from Chennai to Bengaluru:

- Person A takes a route with fewer delays.
- Person B takes a route with many unnecessary detours.

Both reach Bengaluru, but one route is more efficient.

Algorithm analysis is similar: we compare the resources different solutions require.

## 3. How Are Algorithms Evaluated?

We generally consider these factors:

| Factor | Meaning |
|---|---|
| Correctness | Does the algorithm produce the expected result? |
| Time complexity | How does the number of operations grow? |
| Space complexity | How does memory usage grow? |
| Scalability | Does it remain practical as input grows? |
| Readability and maintainability | Can developers understand and maintain it? |

In DSA, the main mathematical analysis focuses on time and space complexity. Correctness is essential too: a fast algorithm that gives the wrong answer is not a good solution.

## 4. Input Size – The Foundation of Analysis

Before analysing an algorithm, identify its input size.

We commonly represent input size using `n`.

Example:

```python
numbers = [10, 20, 30, 40, 50]
```

Here:

```text
n = 5
```

If the list contains 100 items:

```text
n = 100
```

When we analyse an algorithm, we ask how its work changes as `n` increases.

## 5. Time Complexity

Time complexity describes how the number of basic operations grows with input size.

It does not directly measure the exact number of seconds a program takes. Actual runtime also depends on hardware, programming language, implementation and other factors.

### 5.1 O(1) – Constant Time

The operation count stays approximately constant as input size increases.

```python
numbers = [10, 20, 30, 40, 50]

print(numbers[0])
```

We access the first item directly.

```text
Input:  5 items       -> one indexed access
Input:  100 items     -> one indexed access
Input:  1,000,000     -> one indexed access
```

<badge color="success">O(1)</badge>

### 5.2 O(n) – Linear Time

The number of operations grows proportionally with the input size.

```python
numbers = [10, 20, 30, 40, 50]

for number in numbers:
    print(number)
```

The loop visits every item once.

```text
n = 5       -> 5 visits
n = 100     -> 100 visits
n = 1,000   -> 1,000 visits
```

<badge color="info">O(n)</badge>

### 5.3 O(n²) – Quadratic Time

A nested loop can perform approximately `n × n` operations.

```python
numbers = [10, 20, 30]

for first in numbers:
    for second in numbers:
        print(first, second)
```

For each item in the outer loop, the inner loop visits every item.

```text
n = 3       -> 3 × 3 = 9 operations
n = 5       -> 5 × 5 = 25 operations
n = 10      -> 10 × 10 = 100 operations
```

<badge color="warning">O(n²)</badge>

### 5.4 O(log n) – Logarithmic Time

The amount of work grows slowly because the algorithm reduces the remaining problem size by a constant factor at each step.

Binary search is a common example. It repeatedly halves a sorted search area.

```python
def binary_search(numbers, target):
    left = 0
    right = len(numbers) - 1

    while left <= right:
        middle = (left + right) // 2

        if numbers[middle] == target:
            return middle
        elif numbers[middle] < target:
            left = middle + 1
        else:
            right = middle - 1

    return -1


values = [10, 20, 30, 40, 50, 60, 70]
print(binary_search(values, 50))  # 4
```

Visual idea:

```text
Sorted data:
[10, 20, 30, 40, 50, 60, 70]

Check middle:
[10, 20, 30, 40, 50, 60, 70]
               ^
              40

Target 50 is greater, so ignore the left half:

[50, 60, 70]
     ^
    60

Target 50 is smaller, so ignore the right side:

[50]
 ^
Found!
```

<badge color="success">O(log n)</badge>

### 5.5 O(n log n) – Linearithmic Time

This growth rate commonly appears in efficient sorting algorithms such as merge sort.

Merge sort divides the input into smaller parts, sorts those parts, and merges them.

```text
             [8, 3, 6, 2]
              /       \
          [8, 3]     [6, 2]
           / \        / \
         [8] [3]    [6] [2]
           \ /        \ /
          [3, 8]     [2, 6]
              \       /
             [2, 3, 6, 8]
```

Its time complexity is `O(n log n)` in the best, average and worst cases for the standard merge sort algorithm.

## 6. Comparing Common Time Complexities

| Complexity | Name | General growth |
|---|---|---|
| `O(1)` | Constant | Stays approximately constant |
| `O(log n)` | Logarithmic | Grows slowly |
| `O(n)` | Linear | Grows proportionally |
| `O(n log n)` | Linearithmic | Faster growth than linear |
| `O(n²)` | Quadratic | Grows rapidly |
| `O(2ⁿ)` | Exponential | Grows very rapidly |
| `O(n!)` | Factorial | Grows extremely rapidly |

For many common algorithm problems, lower growth rates are more practical for large inputs. However, the best choice also depends on the problem, data and implementation.

### Growth comparison

The following values illustrate the approximate growth of common functions. They are not measured execution times.

| n | O(1) | O(log₂ n) | O(n) | O(n log₂ n) | O(n²) |
|---:|---:|---:|---:|---:|---:|
| 4 | 1 | 2 | 4 | 8 | 16 |
| 8 | 1 | 3 | 8 | 24 | 64 |
| 16 | 1 | 4 | 16 | 64 | 256 |
| 32 | 1 | 5 | 32 | 160 | 1,024 |

## 7. Best Case, Average Case and Worst Case

An algorithm may perform different amounts of work depending on the input.

Let's use linear search.

```python
def linear_search(numbers, target):
    for index, number in enumerate(numbers):
        if number == target:
            return index

    return -1
```

Suppose:

```python
numbers = [10, 20, 30, 40, 50]
```

### Best case

The target is the first item.

```text
[10, 20, 30, 40, 50]
 ^
Found immediately
```

Only one comparison is needed.

Complexity: `O(1)`

### Worst case

The target is the last item, or it is not present.

```text
[10, 20, 30, 40, 50]
                   ^
```

The algorithm may check every item.

Complexity: `O(n)`

### Average case

The target is somewhere in the middle on average, assuming possible target positions are equally likely.

The number of comparisons grows proportionally with `n`.

Complexity: `O(n)`

| Case | Meaning | Linear search |
|---|---|---|
| Best | Most favourable input | `O(1)` |
| Average | Expected behaviour under an input assumption | `O(n)` |
| Worst | Most work the algorithm may need | `O(n)` |

Important: Average-case analysis depends on assumptions about how inputs are distributed.

## 8. Space Complexity

Space complexity describes how memory requirements grow with input size.

When discussing algorithm space, we often distinguish between:

- **Input space:** Memory occupied by the input.
- **Auxiliary space:** Extra memory used by the algorithm beyond the input.

### 8.1 O(1) – Constant Auxiliary Space

```python
numbers = [10, 20, 30, 40]

total = 0

for number in numbers:
    total += number

print(total)
```

The algorithm uses a fixed number of extra variables, regardless of the number of input items.

Auxiliary space: `O(1)`

### 8.2 O(n) – Linear Auxiliary Space

```python
numbers = [10, 20, 30, 40]

squares = []

for number in numbers:
    squares.append(number * number)

print(squares)
```

The new list grows with the input size.

Auxiliary space: `O(n)`

### Time vs Space Complexity

| Time complexity | Space complexity |
|---|---|
| Measures growth in operations | Measures growth in memory |
| How much work is required? | How much extra memory is required? |
| Example: `O(n)` loop | Example: `O(n)` additional list |

## 9. How to Analyse Python Code – A Simple Method

Use this checklist when you receive a code snippet.

1. Identify the input size (`n`).
2. Count how many times each important operation runs.
3. Check whether loops are sequential or nested.
4. Check whether the input size is reduced in each iteration.
5. Identify additional data structures and variables.
6. Express the growth using Big O notation.

### Example 1: One loop

```python
def display(numbers):
    for number in numbers:
        print(number)
```

- Input size: `n`
- Loop visits each item once.
- Time complexity: `O(n)`
- Auxiliary space: `O(1)`

### Example 2: Two sequential loops

```python
def display(numbers):
    for number in numbers:
        print(number)

    for number in numbers:
        print(number)
```

First loop: `n` operations.

Second loop: `n` operations.

Total: `n + n = 2n`.

In Big O, we remove constant factors.

Time complexity: `O(n)`, not `O(2n)`.

### Example 3: Nested loops

```python
def compare(numbers):
    for first in numbers:
        for second in numbers:
            print(first, second)
```

Outer loop: `n` iterations.

Inner loop: `n` iterations for each outer iteration.

Total: `n × n = n²`.

Time complexity: `O(n²)`.

## 10. Asymptotic Notations: Big O, Omega and Theta

These notations describe how an algorithm's resource usage grows as input size becomes large.

| Notation | Meaning | Informal interpretation |
|---|---|---|
| Big O – `O(g(n))` | Asymptotic upper bound | Does not grow faster than this bound, eventually |
| Omega – `Ω(g(n))` | Asymptotic lower bound | Grows at least as fast as this bound, eventually |
| Theta – `Θ(g(n))` | Asymptotically tight bound | Grows at the same order as this function |

For example, if an algorithm always performs work proportional to `n`, its tight bound is `Θ(n)`. It is also correct to say it is `O(n)` and `Ω(n)`.

Beginner note: Big O is commonly used to communicate an algorithm's upper growth bound. In interview discussions, people often use it to describe worst-case time complexity, but these are not exactly the same definition.

## 11. Important Rules for Simplifying Big O

### Rule 1: Ignore constant factors

```text
O(2n)  -> O(n)
O(5n)  -> O(n)
O(100) -> O(1)
```

### Rule 2: Keep the fastest-growing term

```text
O(n² + n)       -> O(n²)
O(n² + 10n + 5) -> O(n²)
O(n log n + n)  -> O(n log n)
```

### Rule 3: Sequential loops are added

```python
for item in items:
    print(item)

for item in items:
    print(item)
```

`O(n + n)` simplifies to `O(n)`.

### Rule 4: Nested loops are often multiplied

```python
for first in items:
    for second in items:
        print(first, second)
```

`O(n × n)` becomes `O(n²)`.

These are common patterns, not automatic rules for every program. Always inspect loop bounds and how the input changes.

## 12. Algorithm Analysis in Real Applications

| Application | Why analysis matters |
|---|---|
| Search engines | Efficiently retrieve relevant results |
| E-commerce | Search and sort large product catalogues |
| Maps | Find efficient routes |
| Banking | Process large numbers of transactions |
| Social networks | Analyse connections between users |
| Databases | Retrieve records efficiently |
| AI applications | Process large datasets and manage memory |

## 13. Practice Tasks

Try to identify the time and auxiliary space complexity.

### Task 1

```python
numbers = [10, 20, 30, 40]

print(numbers[2])
```

### Task 2

```python
numbers = [10, 20, 30, 40]

for number in numbers:
    print(number)
```

### Task 3

```python
numbers = [10, 20, 30, 40]

for first in numbers:
    for second in numbers:
        print(first, second)
```

### Task 4

```python
numbers = [10, 20, 30, 40]

result = []

for number in numbers:
    result.append(number)
```

### Task 5

Two loops run one after another. Each loop visits all `n` items. What is the simplified time complexity?

## 14. Quick Revision

- **Algorithm analysis:** Evaluating an algorithm's efficiency.
- **Input size (`n`):** The amount of data given to an algorithm.
- **Time complexity:** Growth in the number of operations.
- **Space complexity:** Growth in memory requirements.
- **Correctness:** Whether the algorithm gives the expected result.
- **Scalability:** How well an approach handles increasing input sizes.
- **Best case:** The most favourable input.
- **Average case:** Expected behaviour under stated assumptions.
- **Worst case:** The input requiring the most work.
- **Big O:** Asymptotic upper bound.
- **Omega:** Asymptotic lower bound.
- **Theta:** Asymptotically tight bound.
- **Auxiliary space:** Extra memory used beyond the input.
- **Sequential loops:** Their operation counts are added.
- **Nested loops:** Their operation counts are often multiplied.

## 15. Knowledge Check

**Question 1:** Why do we analyse algorithms?

A. To increase code length  
B. To understand efficiency and resource usage  
C. To avoid using variables  
D. To remove functions

**Question 2:** What does `n` usually represent in complexity analysis?

A. Number of functions  
B. Input size  
C. CPU speed  
D. Number of files

**Question 3:** What is the time complexity of a loop that visits every item once?

A. `O(1)`  
B. `O(log n)`  
C. `O(n)`  
D. `O(n²)`

**Question 4:** What is the time complexity of two nested loops, each iterating over `n` items?

A. `O(n)`  
B. `O(n²)`  
C. `O(log n)`  
D. `O(1)`

**Question 5:** What is the simplified form of `O(3n + 10)`?

A. `O(n²)`  
B. `O(3n)`  
C. `O(n)`  
D. `O(10)`

**Question 6:** Which case describes the maximum amount of work an algorithm may need for an input of size `n`?

A. Best case  
B. Average case  
C. Worst case  
D. Constant case

**Question 7:** An algorithm creates a second list containing one item for every input item. What is its auxiliary space complexity?

A. `O(1)`  
B. `O(log n)`  
C. `O(n)`  
D. `O(n²)`

---

**Learning note:** Do not memorise Big O values alone. Practise counting operations in small Python programs and explain why the complexity has that growth rate.
