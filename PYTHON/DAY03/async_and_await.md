# Python async and await

---

## 1. Introduction

The `async` and `await` keywords introduced in Python 3.5 establish native syntax for writing **cooperative asynchronous code**. Asynchronous routines can yield execution back to an event loop while waiting for non-blocking I/O, allowing thousands of operations to progress concurrently on a single thread.

---

## 2. Coroutines and `async def`

Declaring a function with `async def` marks it as a **coroutine function**. Calling a coroutine function does not immediately run its body; instead, it returns a **coroutine object**.

```python
import asyncio

async def fetch_status():
    print("Fetching server status...")
    await asyncio.sleep(1)  # Non-blocking pause
    print("Status: 200 OK")
    return {"status": 200}

# Execution entry point
result = asyncio.run(fetch_status())
print(result)
```

**Output:**

```text
Fetching server status...
Status: 200 OK
{'status': 200}
```

---

## 3. The `await` Expression

The `await` keyword yields execution back to the event loop until the awaited awaitable (coroutine, Task, or Future) finishes:

```python
import asyncio

async def compute_subtotal(price: float, qty: int) -> float:
    await asyncio.sleep(0.5)
    return price * qty

async def checkout():
    print("Processing checkout...")
    total = await compute_subtotal(24.50, 2)
    print(f"Checkout total: ${total:.2f}")

asyncio.run(checkout())
```

**Output:**

```text
Processing checkout...
Checkout total: $49.00
```

> **Rule:** `await` can only be invoked from within functions defined with `async def`.

---

## 4. Concurrent Execution with `asyncio.gather()`

Running asynchronous operations sequentially defeats the purpose of async programming. Use `asyncio.gather()` to launch operations concurrently.

```python
import asyncio
import time

async def download_file(filename: str, delay: float):
    print(f"Starting {filename}...")
    await asyncio.sleep(delay)
    print(f"Finished {filename} ({delay}s)")
    return f"{filename} data"

async def main():
    start = time.perf_counter()

    # Dispatch downloads concurrently
    results = await asyncio.gather(
        download_file("file1.zip", 2.0),
        download_file("file2.zip", 1.0),
        download_file("file3.zip", 1.5)
    )

    elapsed = time.perf_counter() - start
    print(f"All files fetched in: {elapsed:.2f}s")
    print("Payloads:", results)

asyncio.run(main())
```

**Output:**

```text
Starting file1.zip...
Starting file2.zip...
Starting file3.zip...
Finished file2.zip (1.0s)
Finished file3.zip (1.5s)
Finished file1.zip (2.0s)
All files fetched in: 2.01s
Payloads: ['file1.zip data', 'file2.zip data', 'file3.zip data']
```

The total duration is determined by the slowest task (2.0s), not their sum (4.5s).

---

## 5. Sequential vs Concurrent Execution

| Model | Code Pattern | Wall-Clock Time (3 × 1s tasks) |
|---|---|---|
| **Sequential** | `await t1; await t2; await t3` | ~3.0 seconds |
| **Concurrent** | `await asyncio.gather(t1, t2, t3)` | ~1.0 second |

---

## 6. Common Pitfalls

### Blocking the Event Loop with Synchronous Code

```python
# ANTI-PATTERN: Blocks the entire thread, halting all coroutines
import time
async def bad_worker():
    time.sleep(2)  # NEVER DO THIS in async code!

# CORRECT: Yields control cooperatively
import asyncio
async def good_worker():
    await asyncio.sleep(2)  # Non-blocking
```

---

## 7. Best Practices

1. **Use `asyncio.run()`** as the single entry point for the root coroutine.
2. **Never invoke blocking calls** (`time.sleep()`, synchronous `requests.get()`, standard file I/O) directly inside async functions.
3. **Use asynchronous client libraries:** Use `httpx` or `aiohttp` for HTTP, and `aiofiles` for file interactions.
4. **Run CPU-bound logic in an executor:** If computation is necessary, offload it using `loop.run_in_executor()`.
