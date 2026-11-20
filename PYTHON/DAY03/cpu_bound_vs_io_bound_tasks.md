# CPU-bound vs I/O-bound Tasks

---

## 1. Introduction

Determining whether an application bottleneck stems from CPU computations or external input/output operations is the fundamental decision point when architecting concurrent Python programs.

---

## 2. Core Comparison

| Metric | CPU-Bound Tasks | I/O-Bound Tasks |
|---|---|---|
| **Primary Limiter** | Clock frequency, CPU core saturation | Network latency, disk I/O, database response |
| **Typical Operations** | Math crunching, hashing, matrix algebra, image encoding | Web scraping, REST API requests, disk reads/writes |
| **CPU Utilization** | Sits near 100% per active core | Hovers near 0-5% while awaiting external responses |
| **Optimal Python Solution**| `multiprocessing`, `concurrent.futures.ProcessPoolExecutor` | `threading`, `asyncio`, `concurrent.futures.ThreadPoolExecutor` |

---

## 3. Code Example: CPU-Bound Task

A CPU-bound task keeps the processor actively calculating.

```python
import time

def calculate_factors(number: int) -> list:
    """CPU intensive: computes all integer factors."""
    return [i for i in range(1, number + 1) if number % i == 0]

start = time.time()
result = [calculate_factors(5_000_000 + i) for i in range(3)]
elapsed = time.time() - start

print(f"Computed factors sequentially in: {elapsed:.2f}s")
```

**Output:**

```text
Computed factors sequentially in: 1.15s
```

> **Optimization:** To speed this up, use `multiprocessing.Pool` across multiple cores to calculate factor sets in parallel.

---

## 4. Code Example: I/O-Bound Task

An I/O-bound task spends the majority of its lifetime in a non-operational wait state.

```python
import time

def simulate_http_download(endpoint: str) -> str:
    """I/O intensive: simulated network request delay."""
    time.sleep(1.0)  # Emulates waiting for server payload
    return f"Response from {endpoint}"

endpoints = ["/users", "/invoices", "/products"]

# Sequential Execution
start = time.time()
responses = [simulate_http_download(ep) for ep in endpoints]
elapsed = time.time() - start

print(f"Sequential I/O completed in: {elapsed:.2f}s")
```

**Output:**

```text
Sequential I/O completed in: 3.01s
```

---

## 5. Solving I/O-Bound with ThreadPoolExecutor

Threads allow the operating system to sleep the waiting thread and immediately run other threads without sequential stalling:

```python
import time
from concurrent.futures import ThreadPoolExecutor

start = time.time()
with ThreadPoolExecutor(max_workers=3) as executor:
    results = list(executor.map(simulate_http_download, endpoints))
elapsed = time.time() - start

print(f"Concurrent ThreadPool I/O completed in: {elapsed:.2f}s")
```

**Output:**

```text
Concurrent ThreadPool I/O completed in: 1.01s
```

---

## 6. How to Identify the Bottleneck

```text
Step 1: Inspect system metrics (Task Manager / top / htop)
├── Is CPU usage hovering near 100%?
│   └── YES -> It is CPU-bound!
│              Solution: Use multiprocessing, vectorize with NumPy, or compile with Cython/Numba.
└── NO -> CPU is idle while script is slow?
    └── YES -> It is I/O-bound!
               Solution: Use asyncio or ThreadPoolExecutor.
```

---

## 7. Best Practices

1. **Profile before optimizing:** Use `time.perf_counter()`, `cProfile`, or `tracemalloc` to pinpoint true latency sources.
2. **Never use `multiprocessing` for pure I/O:** Process spawning incurs substantial memory overhead and IPC serialization costs compared to lightweight threads.
3. **Never rely on `threading` for CPU-heavy algorithms:** In CPython, the GIL will serialize thread execution, adding context-switching overhead and making it slower than pure single-threaded execution.
