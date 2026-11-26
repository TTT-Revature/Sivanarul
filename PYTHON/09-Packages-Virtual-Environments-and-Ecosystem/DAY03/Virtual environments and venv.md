# Python Virtual Environments and `venv`

---

## 1. What is a Virtual Environment?

A **virtual environment** is an isolated, self-contained Python installation that maintains its own set of installed packages independently from the system-wide Python installation.

### Why Use Virtual Environments?

- **Dependency Isolation:** Project A may require `requests==2.28`, while Project B needs `requests==2.31`. Without isolation, one project's dependencies overwrite the other's.
- **Reproducibility:** Ensures every team member and deployment server uses the exact same package versions.
- **Clean System Python:** Prevents polluting the global Python installation with project-specific packages.

---

## 2. Creating a Virtual Environment with `venv`

Python 3.3+ includes the built-in `venv` module (no installation required):

```bash
# Create a virtual environment named ".venv"
python -m venv .venv
```

This creates a `.venv/` directory containing:
- A copy of the Python interpreter.
- A local `pip` executable.
- An empty `site-packages/` directory for installed packages.

---

## 3. Activating and Deactivating

### Activation

| Operating System | Command |
|---|---|
| **Windows (PowerShell)** | `.venv\Scripts\Activate.ps1` |
| **Windows (CMD)** | `.venv\Scripts\activate.bat` |
| **macOS / Linux** | `source .venv/bin/activate` |

After activation, the terminal prompt changes to show the environment name:

```text
(.venv) PS C:\Users\SivanarulA\Desktop\project>
```

### Deactivation

```bash
deactivate
```

---

## 4. Installing Packages Inside a Virtual Environment

With the environment activated, `pip install` installs packages only into `.venv/`:

```bash
(.venv) $ pip install requests flask
(.venv) $ pip list
```

**Output:**

```text
Package    Version
---------- -------
Flask      3.0.0
requests   2.31.0
pip        24.0
```

---

## 5. Best Practices

1. **Always add `.venv/` to `.gitignore`** — never commit the virtual environment directory to version control.
2. **Create one virtual environment per project** in the project root.
3. **Name it `.venv`** (the convention recognized by most IDEs and tools).
4. **Freeze dependencies** after installing: `pip freeze > requirements.txt`.
5. **Recreate** on a new machine: `python -m venv .venv && pip install -r requirements.txt`.
