# Python asyncio and Basic Asynchronous Tasks

---

## 1. Introduction

The **`asyncio`** library provides the foundational infrastructure for writing concurrent applications using the async/await syntax. At its heart lies the **Event Loop**, a single-threaded execution manager that dispatches tasks, handles network socket events, and switches coroutine contexts seamlessly.

---

## 2. The Event Loop Architecture

```text
+-------------------------------------------------------+
|                      Event Loop                       |
|                                                       |
|  [ Ready Task Queue ] ----> Executes bytecode         |
|                                     |                 |
|                                     v                 |
|  [ Polling / I/O Sockets ] <---- Awaits I/O completion|
+-------------------------------------------------------+
```

`asyncio.run(coroutine)` creates a fresh event loop, executes the passed coroutine to completion, and guarantees clean teardown of lingering tasks and executors.

---

## 3. Creating Tasks with `asyncio.create_task()`

Wrapping a coroutine in `asyncio.create_task()` schedules it for immediate background execution on the event loop without awaiting it immediately.

```python
import asyncio
import time

async def monitor_service(service_name: str, interval: float):
    print(f"Monitoring [{service_name}] started")
    await asyncio.sleep(interval)
    print(f"Monitoring [{service_name}] ping successful")
    return f"{service_name}: OK"

async def main():
    # Schedule background tasks
    task_auth = asyncio.create_task(monitor_service("Auth Service", 1.5))
    task_db = asyncio.create_task(monitor_service("Database", 1.0))

    print("Main coordinator performing other operations...")
    await asyncio.sleep(0.5)

    # Await resolution
    res_auth = await task_auth
    res_db = await task_db
    print("Health Status:", res_auth, res_db)

asyncio.run(main())
```

**Output:**

```text
Monitoring [Auth Service] started
Monitoring [Database] started
Main coordinator performing other operations...
Monitoring [Database] ping successful
Monitoring [Auth Service] ping successful
Health Status: Auth Service: OK Database: OK
```

---

## 4. Handling Timeouts with `asyncio.wait_for()`

To avoid operations hanging indefinitely, wrap awaitables with timeout limits:

```python
import asyncio

async def long_query():
    await asyncio.sleep(5)
    return "Database result"

async def main():
    try:
        result = await asyncio.wait_for(long_query(), timeout=2.0)
        print(result)
    except asyncio.TimeoutError:
        print("Query aborted: Operation timed out after 2.0s")

asyncio.run(main())
```

**Output:**

```text
Query aborted: Operation timed out after 2.0s
```

---

## 5. Task Management Utilities

| Function | Purpose |
|---|---|
| `asyncio.create_task(coro)` | Schedules coroutine execution on the loop, returning a `Task` |
| `asyncio.gather(*coros)` | Executes awaitables concurrently and aggregates return values in order |
| `asyncio.wait_for(aw, timeout)` | Imposes strict execution timeout on awaitable |
| `asyncio.shield(aw)` | Protects an awaitable from being cancelled |
| `asyncio.sleep(delay)` | Non-blocking sleep yielding loop control |

---

## 6. Asynchronous Queues (`asyncio.Queue`)

For coordinating workflows between asynchronous producers and consumers without locks:

```python
import asyncio

async def producer(queue: asyncio.Queue):
    for order_id in [101, 102, 103]:
        await asyncio.sleep(0.5)
        await queue.put(order_id)
        print(f"Enqueued order: {order_id}")
    await queue.put(None)  # Sentinel to stop consumer

async def consumer(queue: asyncio.Queue):
    while True:
        order_id = await queue.get()
        if order_id is None:
            queue.task_done()
            break
        print(f"Processing order: {order_id}")
        await asyncio.sleep(1.0)
        queue.task_done()

async def main():
    queue = asyncio.Queue()
    await asyncio.gather(producer(queue), consumer(queue))

asyncio.run(main())
```

**Output:**

```text
Enqueued order: 101
Processing order: 101
Enqueued order: 102
Enqueued order: 103
Processing order: 102
Processing order: 103
```

---

## 7. Best Practices

1. **Always handle exceptions in `gather()`:** Use `return_exceptions=True` if you do not want one failing coroutine to cancel remaining peers.
2. **Apply `asyncio.wait_for()`** to external network requests to prevent infinite hangs.
3. **Avoid creating manual loops:** Use `asyncio.run()` instead of `get_event_loop()` / `run_until_complete()`.
4. **Use `asyncio.Queue`** for asynchronous pipelines to balance ingestion and consumption rates.
