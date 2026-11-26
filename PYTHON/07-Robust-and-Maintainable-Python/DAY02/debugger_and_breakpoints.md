# Python Debugger and Breakpoints (`breakpoint()` and `pdb`)

---

## 1. Introduction

Python includes a built-in interactive source code debugger called **`pdb`**.

Since Python 3.7, the easiest way to invoke the debugger is the built-in **`breakpoint()`** function. Calling `breakpoint()` suspends execution and drops you directly into an interactive debugging prompt.

---

## 2. Setting a Breakpoint

```python
def calculate_grade(scores):
    total = sum(scores)
    count = len(scores)
    
    breakpoint()  # <--- Execution pauses right here!
    
    average = total / count
    return average

calculate_grade([88, 92, 79, 95])
```

When this code runs in a terminal, Python pauses and displays:

```text
> app.py(7)calculate_grade()
-> average = total / count
(Pdb) 
```

---

## 3. Essential `pdb` Commands

| Command | Shortcut | Description |
|---|:---:|---|
| `next` | `n` | Execute the current line and advance to the next line. |
| `step` | `s` | Step **into** the function called on the current line. |
| `continue` | `c` | Continue execution until the next breakpoint or program completion. |
| `print` | `p expr` | Evaluate and print expression (e.g., `p total`). |
| `where` | `w` | Show the stack trace and current frame position. |
| `list` | `l` | Show surrounding lines of code. |
| `quit` | `q` | Immediately abort execution and quit debugger. |

---

## 4. Post-Mortem Debugging with `pdb.pm()`

If an application crashes unhandled, you can inspect the state at the point of failure:

```python
import pdb

try:
    1 / 0
except Exception:
    pdb.pm()  # Drops directly into the crashed state
```
