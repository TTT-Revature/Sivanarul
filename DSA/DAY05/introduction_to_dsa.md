# Introduction to DSA – Data Structures and Algorithms

**Level:** Beginner  
**Language used for examples:** Python

## 1. What is DSA?

DSA stands for **Data Structures and Algorithms**.

- **Data Structure:** A way of organising and storing data so that we can use it efficiently.
- **Algorithm:** A step-by-step procedure used to solve a problem.

In simple terms:

> Data structures organise the data. Algorithms tell us what to do with that data.

### Real-world analogy

Imagine a library:

- The books are the **data**.
- The shelves and catalogue system are the **data structures**.
- The process you follow to find a particular book is the **algorithm**.

A well-organised library makes finding a book faster. Similarly, choosing a suitable data structure and algorithm can make a program faster and more memory-efficient.

## 2. Why do we learn DSA?

We learn DSA to:

1. Solve programming problems efficiently.
2. Reduce unnecessary execution time.
3. Use memory effectively.
4. Handle large amounts of data.
5. Build scalable applications.
6. Prepare for technical interviews.

### Practical example

Suppose a list contains one million employee IDs and you need to find one ID.

- A simple linear search may check many IDs one by one.
- A binary search can eliminate half of the remaining search area at each step, but it requires the data to be sorted.

The right approach depends on the data and the problem.

## 3. Data Structures

A data structure is a method of storing and organising data.

### Common data structures

| Data structure | Basic idea | Everyday example |
|---|---|---|
| Array / List | Stores items in an ordered sequence | A row of seats |
| Linked List | Items connect to the next item | A chain |
| Stack | Last In, First Out (LIFO) | Stack of plates |
| Queue | First In, First Out (FIFO) | People waiting in a queue |
| Hash Table / Dictionary | Stores key-value pairs | Phone contacts |
| Tree | Organises data hierarchically | Folder structure |
| Graph | Represents connections between items | Road network |

### 3.1 List (Array-like structure in Python)

A Python list stores multiple items in an ordered collection.

```python
numbers = [10, 20, 30, 40]

print(numbers[0])  # 10
print(numbers[2])  # 30
```

Visual representation:

```text
Index:    0     1     2     3
        +-----+-----+-----+-----+
Value:  | 10  | 20  | 30  | 40  |
        +-----+-----+-----+-----+
```

### 3.2 Stack

A stack follows **LIFO – Last In, First Out**.

The last item added is the first item removed.

Example: A stack of plates. You normally take the top plate first.

```python
stack = []

stack.append("A")
stack.append("B")
stack.append("C")

print(stack.pop())  # C
print(stack)        # ['A', 'B']
```

```text
        TOP
      +-----+
      |  C  |  <- removed first
      +-----+
      |  B  |
      +-----+
      |  A  |
      +-----+
```

### 3.3 Queue

A queue follows **FIFO – First In, First Out**.

The first item added is the first item removed.

Example: People waiting at a ticket counter.

```python
from collections import deque

queue = deque()

queue.append("A")
queue.append("B")
queue.append("C")

print(queue.popleft())  # A
print(queue)            # deque(['B', 'C'])
```

```text
FRONT                         REAR
  |                             |
  v                             v
+-----+     +-----+     +-----+
|  A  | --> |  B  | --> |  C  |
+-----+     +-----+     +-----+
  |
  +-- leaves first
```

### 3.4 Dictionary (Hash Table)

A Python dictionary stores data as key-value pairs.

```python
employee = {
    "name": "Arun",
    "role": "Python Developer"
}

print(employee["name"])  # Arun
```

Example: A phone contact list, where a person's name is used to look up their phone number.

### 3.5 Tree

A tree stores data in a hierarchical structure.

Example: Folders and subfolders on a computer.

```text
          Company
         /       \
      HR         IT
                /  \
           Backend  Frontend
```

### 3.6 Graph

A graph represents relationships or connections between items.

Example: Cities connected by roads or people connected in a social network.

```text
Chennai ----- Bengaluru
   |              |
   |              |
Hyderabad ----- Mumbai
```

## 4. Algorithms

An algorithm is a finite sequence of steps used to solve a problem.

### Example: Find the largest number

Problem: Find the largest number in a list.

```python
numbers = [12, 45, 7, 89, 23]

largest = numbers[0]

for number in numbers:
    if number > largest:
        largest = number

print(largest)  # 89
```

How it works:

1. Assume the first number is the largest.
2. Compare each number with the current largest.
3. If a bigger number is found, update `largest`.
4. After checking every number, print the answer.

### Common algorithm categories

| Algorithm | Purpose |
|---|---|
| Searching | Find an item |
| Sorting | Arrange items in an order |
| Recursion | Solve a problem by calling the same function on a smaller problem |
| Divide and Conquer | Break a problem into smaller parts, solve them, and combine results |
| Greedy | Make the best local choice at each step |
| Dynamic Programming | Reuse results of overlapping subproblems |

## 5. Time Complexity

Time complexity describes how the number of operations an algorithm performs grows as the input size grows.

It does **not** directly tell us the exact number of seconds a program will take.

We commonly express it using **Big O notation**.

Let `n` represent the number of input items.

| Big O | Name | General behaviour |
|---|---|---|
| `O(1)` | Constant | Work stays roughly the same as input grows |
| `O(log n)` | Logarithmic | Work grows slowly as input grows |
| `O(n)` | Linear | Work grows proportionally with input |
| `O(n log n)` | Linearithmic | Common in efficient comparison sorting |
| `O(n²)` | Quadratic | Work can grow roughly with the square of input |

### Visual intuition

```text
Input size increases  -------------------->

O(1)       ─────────────  nearly constant
O(log n)   ____/          grows slowly
O(n)       ____/          grows proportionally
O(n log n) ____/          grows faster than linear
O(n²)      ____/          grows rapidly
```

### Simple code examples

**O(1) – Constant time**

```python
numbers = [10, 20, 30, 40]
print(numbers[0])
```

Accessing an item by list index takes constant time in the usual Python list model.

**O(n) – Linear time**

```python
numbers = [10, 20, 30, 40]

for number in numbers:
    print(number)
```

The loop visits each item once. If the number of items doubles, the number of visits roughly doubles.

**O(n²) – Quadratic time**

```python
numbers = [10, 20, 30]

for first in numbers:
    for second in numbers:
        print(first, second)
```

For each item, the inner loop visits all items. With `n` items, there are `n × n` iterations.

**O(log n) – Logarithmic time**

Binary search repeatedly halves the search area. It works on sorted data.

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

Each step discards approximately half of the remaining elements.

## 6. Space Complexity

Space complexity describes how the memory requirement of an algorithm grows as the input size grows.

It can include extra memory used by the algorithm. In some analyses, the input storage is also counted; always check which convention is being used.

### Examples

**O(1) – Constant extra space**

```python
numbers = [10, 20, 30, 40]

total = 0

for number in numbers:
    total += number

print(total)  # 100
```

The algorithm uses one additional variable, `total`, regardless of the list length.

**O(n) – Linear extra space**

```python
numbers = [10, 20, 30, 40]

squares = []

for number in numbers:
    squares.append(number * number)

print(squares)  # [100, 400, 900, 1600]
```

The new list grows as the input list grows.

### Time vs Space Complexity

| Complexity | What it measures | Main question |
|---|---|---|
| Time complexity | Growth in operations | How does the work grow? |
| Space complexity | Growth in memory usage | How does the memory grow? |

## 7. Searching: Linear Search vs Binary Search

| Feature | Linear Search | Binary Search |
|---|---|---|
| Approach | Check items one by one | Repeatedly halve the search area |
| Requires sorted data? | No | Yes |
| Time complexity | `O(n)` | `O(log n)` |
| Beginner example | Search through an unsorted list | Search a sorted list |

Remember: Binary search is not automatically the right choice. The data must be sorted, and sorting itself may have a cost.

## 8. How Data Structures and Algorithms Work Together

Consider an employee management application.

- A list can hold employee records.
- A dictionary can find an employee using an ID.
- A sorting algorithm can arrange employees by salary.
- A searching algorithm can find a particular employee.
- A tree can represent an organisation hierarchy.

The data structure determines how data is organised. The algorithm determines how we process it.

## 9. Where DSA Is Used in Real Applications

| Application | DSA concepts |
|---|---|
| Search engines | Searching, ranking, graphs |
| Maps and navigation | Graphs, shortest-path algorithms |
| Social networks | Graphs |
| Browser history | Stack |
| Printer job management | Queue |
| Database indexing | Trees and hash-based structures |
| File systems | Trees |
| Scheduling systems | Queues and priority queues |

## 10. Beginner Learning Roadmap

Study the topics in this order:

1. Complexity analysis – Big O, time and space complexity
2. Arrays and Python lists
3. Strings
4. Searching – linear and binary search
5. Sorting – bubble, selection, insertion, merge and quick sort
6. Linked lists
7. Stacks and queues
8. Hash tables and sets
9. Recursion and backtracking
10. Trees and binary search trees
11. Heaps and priority queues
12. Graphs
13. Greedy algorithms
14. Dynamic programming

## 11. Practice Tasks

Try these without looking at a solution first.

1. Find the largest number in a list.
2. Find the smallest number in a list.
3. Count how many even numbers are in a list.
4. Search for a target using linear search.
5. Search for a target using binary search on a sorted list.
6. Explain the difference between a stack and a queue.
7. Identify the time complexity of a loop that visits every item once.
8. Identify the extra space complexity of an algorithm that creates a second list containing `n` items.

## 12. Quick Revision

- **DSA:** Data Structures and Algorithms.
- **Data Structure:** Organises and stores data.
- **Algorithm:** Steps used to solve a problem.
- **Time Complexity:** How operation count grows with input size.
- **Space Complexity:** How memory usage grows with input size.
- **Big O:** A way to describe growth rate.
- **`O(1)`:** Constant growth.
- **`O(log n)`:** Logarithmic growth.
- **`O(n)`:** Linear growth.
- **`O(n log n)`:** Linearithmic growth.
- **`O(n²)`:** Quadratic growth.
- **Stack:** LIFO – Last In, First Out.
- **Queue:** FIFO – First In, First Out.
- **Binary Search:** Repeatedly halves a sorted search space.

## 13. Knowledge Check

**Question 1:** What is the main purpose of a data structure?

A. To increase the number of lines in a program  
B. To organise and store data  
C. To replace programming languages  
D. To execute code automatically

**Question 2:** Which data structure follows LIFO?

A. Queue  
B. Graph  
C. Stack  
D. Tree

**Question 3:** Which search algorithm requires sorted data?

A. Linear Search  
B. Binary Search  
C. Both  
D. Neither

**Question 4:** What does `O(n)` usually mean?

A. The work grows proportionally with the input size  
B. The work is always constant  
C. The work grows with the square of the input size  
D. The algorithm uses no memory

**Question 5:** What does space complexity measure?

A. The number of lines of code  
B. The time taken by the CPU clock  
C. How memory usage grows with input size  
D. The internet speed of an application

---

**Learning note:** Understand the purpose of each structure before memorising its operations or complexity. Practise each concept with small Python examples, then move to problem-solving.
