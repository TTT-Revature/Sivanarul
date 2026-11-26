# Python Threads and Thread Management

---

## 1. Introduction

A **thread** is the smallest sequence of programmed instructions that can be managed independently by an operating system scheduler. Python's built-in `threading` module enables concurrent execution of multiple threads inside a single process, sharing the same address space.

---

## 2. Creating and Starting Threads

Threads can be initiated by creating `threading.Thread` instances pointing to a target callable.

```python
import threading
import time

def worker_task(task_name: str, duration: int):
    print(f"[{threading.current_thread().name}] Starting {task_name}")
    time.sleep(duration)
    print(f"[{threading.current_thread().name}] Finished {task_name}")

# Constructing threads
t1 = threading.Thread(target=worker_task, args=("Data Export", 2), name="Worker-A")
t2 = threading.Thread(target=worker_task, args=("Report Gen", 1), name="Worker-B")

# Start execution
t1.start()
t2.start()

# Wait for completion (join)
t1.join()
t2.join()

print("All worker threads completed successfully.")
```

**Output:**

```text
[Worker-A] Starting Data Export
[Worker-B] Starting Report Gen
[Worker-B] Finished Report Gen
[Worker-A] Finished Data Export
All worker threads completed successfully.
```

---

## 3. Thread Synchronization with `join()`

The `.join()` method blocks the calling thread (usually the main thread) until the target thread terminates.

```python
t = threading.Thread(target=worker_task, args=("Task-1", 1))
t.start()

# Block main thread for a maximum of 2 seconds
t.join(timeout=2.0)

if t.is_alive():
    print("Thread is still executing!")
else:
    print("Thread concluded.")
```

---

## 4. Daemon Threads

A **daemon thread** runs in the background without preventing the Python process from terminating. When all non-daemon threads finish, daemon threads are abruptly aborted by the interpreter.

```python
import threading
import time

def metrics_logger():
    while True:
        print("[Daemon] Polling telemetry metrics...")
        time.sleep(1)

# Designating daemon status
telemetry_thread = threading.Thread(target=metrics_logger, daemon=True)
telemetry_thread.start()

# Main thread continues and finishes after 2 seconds
time.sleep(2)
print("Main thread exiting. Daemon will be terminated automatically.")
```

**Output:**

```text
[Daemon] Polling telemetry metrics...
[Daemon] Polling telemetry metrics...
Main thread exiting. Daemon will be terminated automatically.
```

---

## 5. Thread Pools with `concurrent.futures`

Managing individual threads manually becomes error-prone at scale. The `ThreadPoolExecutor` context manager automates queueing, execution, and resource cleanup.

```python
from concurrent.futures import ThreadPoolExecutor
import time

def fetch_data(record_id: int) -> dict:
    time.sleep(0.5)
    return {"id": record_id, "status": "processed"}

records = [101, 102, 103, 104]

with ThreadPoolExecutor(max_workers=2) as pool:
    results = pool.map(fetch_data, records)

for res in results:
    print(res)
```

**Output:**

```text
{'id': 101, 'status': 'processed'}
{'id': 102, 'status': 'processed'}
{'id': 103, 'status': 'processed'}
{'id': 104, 'status': 'processed'}
```

---

## 6. Thread Properties and Diagnostics

| Method / Property | Description |
|---|---|
| `thread.name` | Readable name identifier for debugging |
| `thread.ident` | OS assigned integer thread ID |
| `thread.is_alive()` | Returns `True` if thread is currently active |
| `thread.daemon` | Boolean flag indicating daemon status |
| `threading.active_count()` | Total count of running native threads |
| `threading.current_thread()` | Returns the caller's thread object |

---

## 7. Best Practices

1. **Always use `join()`** on non-daemon threads to guarantee file flushes and resource completions.
2. **Favor `ThreadPoolExecutor`** over low-level manual `threading.Thread` instances.
3. **Do not perform CPU computation on threads:** The GIL prevents speedups; use threads strictly for blocking I/O calls.
4. **Guard shared memory:** Because threads share heap space, always guard concurrent read-writes using synchronization primitives (`Lock`).
