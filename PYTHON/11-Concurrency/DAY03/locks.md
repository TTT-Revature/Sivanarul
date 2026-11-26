# Python Locks

---

## 1. Introduction

A **Lock** (also known as a mutex or mutual exclusion primitive) is a synchronization tool used to protect a **critical section** — a region of code that accesses shared mutable resources — guaranteeing that only one thread can execute that block at any given instant.

---

## 2. Using `threading.Lock`

A lock exists in one of two states: **locked** or **unlocked**.
- Calling `.acquire()` on an unlocked lock locks it and allows the thread to proceed.
- Calling `.acquire()` on an already locked lock blocks the calling thread until another thread invokes `.release()`.

### Resolving Race Conditions with a Lock

```python
import threading

shared_counter = 0
counter_lock = threading.Lock()

def safe_increment(iterations: int):
    global shared_counter
    for _ in range(iterations):
        counter_lock.acquire()
        try:
            shared_counter += 1
        finally:
            counter_lock.release()

threads = [threading.Thread(target=safe_increment, args=(100_000,)) for _ in range(5)]
for t in threads:
    t.start()
for t in threads:
    t.join()

print(f"Final Count: {shared_counter}")
```

**Output:**

```text
Final Count: 500000
```

---

## 3. The `with` Context Manager (Recommended)

Python locks natively support the context management protocol. The `with lock:` statement automatically acquires the lock on entry and guarantees its release on exit, even if exceptions are raised.

```python
import threading

account_balance = 1000
balance_lock = threading.Lock()

def safe_withdrawal(amount: int):
    global account_balance
    with balance_lock:  # Automatically acquires and releases
        if account_balance >= amount:
            account_balance -= amount
            print(f"Debited ${amount}. Balance: ${account_balance}")
        else:
            print(f"Failed to debit ${amount}. Insufficient funds.")

t1 = threading.Thread(target=safe_withdrawal, args=(600,))
t2 = threading.Thread(target=safe_withdrawal, args=(600,))

t1.start()
t2.start()
t1.join()
t2.join()
```

**Output:**

```text
Debited $600. Balance: $400
Failed to debit $600. Insufficient funds.
```

---

## 4. Reentrant Locks: `threading.RLock`

A standard `Lock` cannot be acquired twice by the same thread; attempting to do so results in a self-deadlock. An **`RLock`** (Reentrant Lock) tracks which thread owns it and can be acquired multiple times by the owning thread.

```python
import threading

reentrant_lock = threading.RLock()

def inner_operation():
    with reentrant_lock:
        print("Inner operation holds RLock")

def outer_operation():
    with reentrant_lock:
        print("Outer operation holds RLock")
        inner_operation()  # Re-acquires without deadlocking

thread = threading.Thread(target=outer_operation)
thread.start()
thread.join()
```

**Output:**

```text
Outer operation holds RLock
Inner operation holds RLock
```

---

## 5. Deadlocks and Prevention

A **deadlock** happens when two or more threads are permanently blocked, each holding a lock that the other needs.

```python
# Deadlock Scenario:
# Thread 1: Acquires Lock A, waits for Lock B
# Thread 2: Acquires Lock B, waits for Lock A
```

### Deadlock Prevention Rules:

| Rule | Implementation |
|---|---|
| **Lock Ordering** | Always acquire multiple locks in the exact same global order across all threads. |
| **Lock Timeouts** | Use `lock.acquire(timeout=2.0)` to abort if lock acquisition stalls. |
| **Minimize Critical Section** | Never execute long-running I/O or network requests inside a lock. |

---

## 6. Comparison: `Lock` vs `RLock`

| Characteristic | `threading.Lock` | `threading.RLock` |
|---|---|---|
| **Can re-acquire by same thread?** | No (causes immediate deadlock) | Yes (increments internal counter) |
| **Performance overhead** | Lower | Slightly higher bookkeeping |
| **Best Used For** | General mutual exclusion | Recursive routines, helper method cascades |

---

## 7. Best Practices

1. **Always use the `with lock:` idiom** rather than manually pairing `.acquire()` and `.release()`.
2. **Keep the critical section narrow:** Perform data parsing and formatting outside the lock; keep only state mutations inside.
3. **Never perform blocking I/O while holding a lock.**
4. **Use timeouts** when acquiring locks in complex distributed or concurrent systems.
