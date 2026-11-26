# Python Race Conditions and Shared Data

---

## 1. Introduction

A **race condition** is an undesirable situation that occurs when two or more concurrent execution threads access shared mutable data and attempt to alter it simultaneously. Because thread scheduling is non-deterministic, the final outcome depends on the arbitrary timing of CPU context switches.

---

## 2. Anatomy of a Race Condition

Consider the deceptively simple operation: `counter += 1`. This single line in Python translates to multiple lower-level bytecode instructions:

```text
1. LOAD_GLOBAL    (Read value into thread CPU register)
2. LOAD_CONST     (Read literal 1)
3. BINARY_ADD     (Perform arithmetic in register)
4. STORE_GLOBAL   (Write result back to shared memory)
```

If another thread interrupts between step 1 and step 4, one thread's update is overwritten and permanently lost.

---

## 3. Demonstrating a Race Condition

```python
import threading

shared_counter = 0

def increment_many(iterations: int):
    global shared_counter
    for _ in range(iterations):
        shared_counter += 1

# Launch 5 concurrent threads each adding 100,000
threads = [threading.Thread(target=increment_many, args=(100_000,)) for _ in range(5)]

for t in threads:
    t.start()
for t in threads:
    t.join()

print(f"Expected count: 500000")
print(f"Actual count:   {shared_counter}")
```

**Output (sample run):**

```text
Expected count: 500000
Actual count:   364219
```

The count is significantly below the expected 500,000 due to race condition update collisions.

---

## 4. The Check-Then-Act Hazard

Another common manifestation is **Check-Then-Act**, where a conditional branch evaluates a condition that invalidates prior to action:

```python
import threading

bank_account = {"balance": 100}

def withdraw_money(amount: int):
    # Check
    if bank_account["balance"] >= amount:
        # Context switch occurs here!
        bank_account["balance"] -= amount
        print(f"Withdrawn {amount}. Remaining: {bank_account['balance']}")
    else:
        print("Declined: Insufficient balance")

t1 = threading.Thread(target=withdraw_money, args=(80,))
t2 = threading.Thread(target=withdraw_money, args=(80,))

t1.start()
t2.start()
t1.join()
t2.join()
```

**Output (race condition triggered):**

```text
Withdrawn 80. Remaining: 20
Withdrawn 80. Remaining: -60
```

Both threads checked when balance was 100, causing an illegal negative balance.

---

## 5. Identifying Symptoms of Shared State Bugs

| Symptom | Cause |
|---|---|
| **Intermittent test failures** | Timing-dependent race condition |
| **Heisenbugs** | Bug disappears when running inside a debugger due to slow execution |
| **Corrupted data structures** | Simultaneous modifications on dictionaries or trees |
| **Unexplained negative balances** | Check-Then-Act race condition |

---

## 6. How to Eliminate Race Conditions

| Technique | Description |
|---|---|
| **Mutual Exclusion (Lock)** | Enforces that only one thread enters the critical section |
| **Thread-Safe Queues (`queue.Queue`)** | Thread communication via message passing instead of shared state |
| **Immutable Data Structures** | Passing frozen copies (tuples, frozen dataclasses) |
| **Thread-Local Storage (`threading.local`)** | Giving each thread its own independent variable instance |

---

## 7. Best Practices

1. **Avoid shared mutable state entirely** where possible — favor passing data via message queues.
2. **Protect all critical sections** modifying shared state with synchronization locks.
3. **Keep critical sections as small as possible** to avoid thread contention bottlenecks.
4. **Use thread-safe data structures:** `queue.Queue` has built-in locking for thread-safe operations.
