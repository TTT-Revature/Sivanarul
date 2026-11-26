# Python Project Structure

---

## 1. Introduction

A well-organized project structure makes code easier to navigate, test, and maintain. As projects grow beyond a single script, following standard conventions helps every developer on the team find things quickly.

---

## 2. Minimal Script Project

For small utility scripts:

```text
my_script/
├── main.py
├── requirements.txt
└── README.md
```

---

## 3. Standard Package Layout

For production applications and libraries:

```text
my_project/
├── src/
│   └── my_project/
│       ├── __init__.py
│       ├── core.py
│       ├── utils.py
│       └── models/
│           ├── __init__.py
│           └── user.py
├── tests/
│   ├── __init__.py
│   ├── test_core.py
│   └── test_utils.py
├── docs/
│   └── usage.md
├── .gitignore
├── README.md
├── requirements.txt
├── requirements-dev.txt
└── setup.py  # or pyproject.toml
```

### Key Directories

| Directory | Purpose |
|---|---|
| `src/my_project/` | Main application source code |
| `tests/` | Unit and integration tests |
| `docs/` | Documentation files |

### Key Files

| File | Purpose |
|---|---|
| `__init__.py` | Marks a directory as a Python package |
| `README.md` | Project description and setup instructions |
| `requirements.txt` | Production dependencies |
| `requirements-dev.txt` | Development/test dependencies |
| `.gitignore` | Files and directories to exclude from Git |
| `setup.py` / `pyproject.toml` | Package metadata and build config |

---

## 4. The `src/` Layout vs Flat Layout

### Flat Layout

```text
my_project/
├── my_project/
│   ├── __init__.py
│   └── core.py
└── tests/
```

### `src/` Layout (Recommended)

```text
my_project/
├── src/
│   └── my_project/
│       ├── __init__.py
│       └── core.py
└── tests/
```

**Why prefer `src/`?**
- Prevents accidentally importing the local package instead of the installed one during testing.
- Forces you to install the package (`pip install -e .`) before running tests, catching packaging issues early.

---

## 5. Example: `__init__.py`

```python
# src/my_project/__init__.py
"""My Project - A demo application."""

__version__ = "1.0.0"

from .core import process_data
from .utils import format_output
```

**Usage:**

```python
from my_project import process_data, __version__

print(__version__)
process_data("sample.csv")
```

**Output:**

```text
1.0.0
Processing sample.csv...
```

---

## 6. The `pyproject.toml` (Modern Standard)

```toml
[build-system]
requires = ["setuptools>=68.0"]
build-backend = "setuptools.backends._legacy:_Backend"

[project]
name = "my_project"
version = "1.0.0"
description = "A demo project"
requires-python = ">=3.10"
dependencies = [
    "requests>=2.31",
    "click>=8.0",
]

[project.optional-dependencies]
dev = ["pytest>=8.0", "black>=24.0"]
```

---

## 7. Best Practices

1. **Follow the `src/` layout** for anything beyond a simple script.
2. **Keep `tests/` at the project root**, not inside `src/`.
3. **One module = one responsibility.** Split large modules into focused files.
4. **Always include** `README.md`, `requirements.txt`, and `.gitignore`.
5. **Use `pyproject.toml`** instead of `setup.py` for new projects (PEP 621).
