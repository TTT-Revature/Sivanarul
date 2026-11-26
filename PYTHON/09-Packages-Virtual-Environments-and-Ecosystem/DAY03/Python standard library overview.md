# Python Standard Library Overview

---

## 1. Introduction

The **Python Standard Library** is a vast collection of modules and packages that ship with every Python installation — no `pip install` required. It provides ready-to-use tools for file I/O, networking, data processing, testing, concurrency, and much more.

> *"Python comes with batteries included."*

---

## 2. Key Standard Library Modules by Category

### File and OS Operations

| Module | Purpose |
|---|---|
| `os` | Operating system interface (env vars, process management) |
| `os.path` | Legacy path manipulation (string-based) |
| `pathlib` | Modern object-oriented path handling |
| `shutil` | High-level file operations (copy, move, delete trees) |
| `glob` | Unix-style pathname pattern matching |
| `tempfile` | Create temporary files and directories |

### Data Handling

| Module | Purpose |
|---|---|
| `json` | JSON serialization and deserialization |
| `csv` | Read and write CSV tabular data |
| `sqlite3` | Embedded SQLite database interface |
| `xml.etree.ElementTree` | Parse and create XML documents |
| `configparser` | Read `.ini` configuration files |

### Date, Time, and Math

| Module | Purpose |
|---|---|
| `datetime` | Date, time, and timedelta operations |
| `time` | Low-level time access and conversions |
| `calendar` | Calendar-related functions |
| `math` | Mathematical functions (sqrt, sin, log, pi) |
| `random` | Generate pseudo-random numbers |
| `statistics` | Mean, median, standard deviation |

### Text Processing

| Module | Purpose |
|---|---|
| `re` | Regular expressions |
| `string` | String constants and templates |
| `textwrap` | Text wrapping and formatting |

### Testing and Debugging

| Module | Purpose |
|---|---|
| `unittest` | Unit testing framework |
| `doctest` | Test interactive examples embedded in docstrings |
| `pdb` | Interactive debugger |
| `logging` | Flexible logging system |

### Networking and Web

| Module | Purpose |
|---|---|
| `http.server` | Simple HTTP server |
| `urllib.request` | URL handling and HTTP requests |
| `socket` | Low-level network interface |
| `email` | Email message handling |

### Concurrency

| Module | Purpose |
|---|---|
| `threading` | Thread-based parallelism |
| `multiprocessing` | Process-based parallelism |
| `asyncio` | Asynchronous I/O framework |
| `concurrent.futures` | High-level interface for async execution |

### Data Structures

| Module | Purpose |
|---|---|
| `collections` | Specialized containers (Counter, defaultdict, deque, namedtuple) |
| `itertools` | Iterator building blocks (chain, cycle, combinations) |
| `functools` | Higher-order functions (reduce, lru_cache, partial) |
| `heapq` | Heap queue (priority queue) algorithm |

---

## 3. Quick Usage Example

```python
import os
import json
import random
from datetime import datetime
from collections import Counter
from pathlib import Path

# os: Get current working directory
print("CWD:", os.getcwd())

# json: Serialize data
data = {"user": "Sivanarul", "score": 95}
print("JSON:", json.dumps(data))

# random: Generate random number
print("Random:", random.randint(1, 100))

# datetime: Current timestamp
print("Now:", datetime.now().isoformat())

# collections: Count word frequency
words = "python java python go python java".split()
print("Counts:", Counter(words))

# pathlib: Check if file exists
print("Exists:", Path("requirements.txt").exists())
```

---

## 4. Best Practice

Before installing a third-party package via `pip`, always check whether the standard library already provides the functionality you need. This reduces external dependencies and simplifies deployment.
