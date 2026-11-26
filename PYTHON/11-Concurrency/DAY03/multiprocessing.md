# Python Multiprocessing

---

## 1. Introduction

The `multiprocessing` module side-steps Python's Global Interpreter Lock (GIL) by spawning separate operating system processes, each containing its own isolated Python interpreter, memory space, and GIL. This unlocks true multi-core parallel processing for computationally heavy (CPU-bound) workloads.

---

## 2. Spawning Processes

Creating a process mirrors the `threading` API using `multiprocessing.Process`.

> **Important:** Always guard process startup code with `if __name__ == '__main__':` to prevent infinite recursive child process spawning on Windows and macOS.

```python
from multiprocessing import Process
import os

def process_worker(label: str):
    print(f"Child process [{label}] PID: {os.getpid()} (Parent PID: {os.getppid()})")

if __name__ == "__main__":
    print(f"Main Process PID: {os.getpid()}")

    p1 = Process(target=process_worker, args=("Alpha",))
    p2 = Process(target=process_worker, args=("Beta",))

    p1.start()
    p2.start()

    p1.join()
    p2.join()
```

**Output:**

```text
Main Process PID: 4510
Child process [Alpha] PID: 4511 (Parent PID: 4510)
Child process [Beta] PID: 4512 (Parent PID: 4510)
```

---

## 3. Parallel Processing with `multiprocessing.Pool`

`Pool` manages a worker pool of processes, seamlessly partitioning data and distributing task chunks across CPU cores.

```python
from multiprocessing import Pool
import time

def compute_heavy_square(n: int) -> int:
    return n * n

if __name__ == "__main__":
    numbers = [10, 20, 30, 40, 50, 60]

    # Spawn worker pool equal to machine CPU core count
    with Pool() as pool:
        results = pool.map(compute_heavy_square, numbers)

    print("Computed squares:", results)
```

**Output:**

```text
Computed squares: [100, 400, 900, 1600, 2500, 3600]
```

---

## 4. Inter-Process Communication (IPC)

Because processes do not share virtual memory address space, sharing data requires dedicated IPC primitives such as **Queues** or **Pipes**.

```python
from multiprocessing import Process, Queue

def producer(q: Queue):
    for product in ["Laptop", "Monitor", "Keyboard"]:
        q.put(product)
    q.put(None)  # Sentinel value signaling stop

def consumer(q: Queue):
    while True:
        item = q.get()
        if item is None:
            break
        print(f"Consumed package: {item}")

if __name__ == "__main__":
    shared_queue = Queue()

    p_prod = Process(target=producer, args=(shared_queue,))
    p_cons = Process(target=consumer, args=(shared_queue,))

    p_prod.start()
    p_cons.start()

    p_prod.join()
    p_cons.join()
```

**Output:**

```text
Consumed package: Laptop
Consumed package: Monitor
Consumed package: Keyboard
```

---

## 5. Threading vs Multiprocessing

| Feature | `threading` | `multiprocessing` |
|---|---|---|
| **Memory Architecture** | Shared memory address space | Independent memory per process |
| **GIL Status** | Subject to GIL constraints | Completely bypasses the GIL |
| **Creation Cost** | Lightweight, low memory overhead | Heavier; incurs process initialization |
| **IPC Mechanism** | Direct variable access (needs Lock) | Pickled serialization (Queues, Pipes) |
| **Optimal Use Case** | Web scraping, disk I/O, network APIs | Data science, cryptography, image processing |

---

## 6. High-Level: `ProcessPoolExecutor`

The modern, standardized way to dispatch tasks across processes is `concurrent.futures.ProcessPoolExecutor`:

```python
from concurrent.futures import ProcessPoolExecutor

def is_prime(n: int) -> bool:
    if n < 2:
        return False
    return all(n % i != 0 for i in range(2, int(n ** 0.5) + 1))

if __name__ == "__main__":
    candidates = [1000000007, 1000000009, 1000000011]
    with ProcessPoolExecutor() as executor:
        for num, prime_status in zip(candidates, executor.map(is_prime, candidates)):
            print(f"{num} is prime: {prime_status}")
```

**Output:**

```text
1000000007 is prime: True
1000000009 is prime: True
1000000011 is prime: False
```

---

## 7. Best Practices

1. **Always wrap execution in `if __name__ == '__main__':`** to support cross-platform compatibility.
2. **Keep arguments serializable:** Data passed between processes must be pickleable.
3. **Size pools appropriately:** Default worker count should equal `os.cpu_count()` to avoid CPU thrashing.
4. **Avoid excessive IPC for tiny tasks:** IPC serialization and deserialization overhead can outweigh parallel computational gains.
