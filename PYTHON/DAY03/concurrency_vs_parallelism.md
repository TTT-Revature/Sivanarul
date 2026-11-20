# Concurrency vs Parallelism

---

## 1. Introduction

Although often used interchangeably, **concurrency** and **parallelism** denote two distinct operational paradigms in system design and software architecture.

### Real-World Analogy

- **Concurrency (One Person, Multiple Tasks):** A single chef juggling an order: boiling pasta, chopping vegetables, and checking the timer. Only one task is physically handled at any given microsecond, but all make forward progress through rapid context switching.
- **Parallelism (Multiple People, Simultaneous Tasks):** Two distinct chefs working side-by-side: Chef A chops onions while Chef B prepares the broth at the exact same physical instant.

---

## 2. Core Definitions

| Concept | Definition | Underlying Hardware Requirement |
|---|---|---|
| **Concurrency** | Structuring a system to handle multiple tasks by interleaving their execution. | Can run on a single CPU core. |
| **Parallelism** | Executing multiple computations simultaneously at the exact same physical clock cycle. | Requires multi-core processors or multi-CPU hardware. |

---

## 3. Visual Execution Models

### Concurrent Execution (Single CPU Core)

```text
Time  --------------------------------------------------->
Core 1: [ Task A ] -> [ Task B ] -> [ Task A ] -> [ Task C ]
         (Interleaved progress via rapid context switching)
```

### Parallel Execution (Multi-Core CPU)

```text
Time  --------------------------------------------------->
Core 1: [ ================== Task A =================== ]
Core 2: [ ================== Task B =================== ]
         (True simultaneous execution at the exact same instant)
```

---

## 4. Python Concurrency and Parallelism Toolkit

Python provides three distinct standard library mechanisms to solve concurrency and parallelism:

| Model | Module | Execution Unit | Best For | GIL Impact |
|---|---|---|---|---|
| **Preemptive Multithreading** | `threading` | OS Thread | I/O-bound operations | Constrained by GIL |
| **Cooperative Multitasking** | `asyncio` | Coroutine | High-concurrency network I/O | Single thread (No GIL contention) |
| **Multiprocessing** | `multiprocessing` | OS Process | CPU-bound calculations | Completely bypasses the GIL |

---

## 5. The Python GIL (Global Interpreter Lock)

In standard CPython, the **GIL** is a mutual exclusion lock that ensures only **one native thread executes Python bytecode at any given time**.

```text
Thread 1: [ Python Code ] --- (Holds GIL) --->
Thread 2:                 --- (Blocked, waiting for GIL) --->
```

### Consequences of the GIL:
1. **CPU-bound threads cannot scale across multiple CPU cores** in CPython.
2. **I/O-bound threads run concurrently and efficiently** because Python automatically releases the GIL during file, socket, and sleep I/O operations.
3. To achieve true parallel speedup on multi-core chips for mathematical or heavy calculations, developers must spawn separate OS processes via `multiprocessing`.

---

## 6. Demonstration: Concurrent Threads vs Parallel Processes

```python
import time
import threading
from multiprocessing import Process

def io_simulation(task_id: int):
    """Simulates waiting for an external network response."""
    time.sleep(1)

# Concurrency with Threads (I/O-bound)
start_time = time.time()
threads = [threading.Thread(target=io_simulation, args=(i,)) for i in range(4)]
for t in threads:
    t.start()
for t in threads:
    t.join()
print(f"4 I/O threads finished in: {time.time() - start_time:.2f}s")
```

**Output:**

```text
4 I/O threads finished in: 1.01s
```

All 4 operations finished in ~1 second concurrently because threads release the GIL while sleeping.

---

## 7. Best Practices

1. **Diagnose the bottleneck first:** Profile whether the workload is spending time waiting on I/O or saturating CPU execution units.
2. **For network/web scraping/database tasks:** Use `asyncio` or `threading`.
3. **For data science, cryptography, image processing:** Use `multiprocessing` or native C-extensions (NumPy, Polars).
4. **Use high-level abstractions:** Prefer `concurrent.futures.ThreadPoolExecutor` and `ProcessPoolExecutor` over manual thread/process coordination.
