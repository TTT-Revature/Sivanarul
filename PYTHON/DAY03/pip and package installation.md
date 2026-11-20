# Python pip and Package Installation

---

## 1. What is pip?

**`pip`** (Pip Installs Packages) is Python's standard package manager. It downloads and installs packages from the **Python Package Index (PyPI)** — a repository of over 500,000 open-source packages.

---

## 2. Common pip Commands

### Installing Packages

```bash
# Install the latest version of a package
pip install requests

# Install a specific version
pip install requests==2.31.0

# Install a minimum version
pip install "requests>=2.28"

# Install multiple packages at once
pip install flask sqlalchemy pytest
```

### Upgrading Packages

```bash
# Upgrade to the latest version
pip install --upgrade requests

# Upgrade pip itself
pip install --upgrade pip
```

### Uninstalling Packages

```bash
pip uninstall requests
```

### Listing Installed Packages

```bash
pip list
```

**Output:**

```text
Package    Version
---------- -------
Flask      3.0.0
requests   2.31.0
pip        24.0
```

### Showing Package Details

```bash
pip show requests
```

**Output:**

```text
Name: requests
Version: 2.31.0
Summary: Python HTTP for Humans.
Home-page: https://requests.readthedocs.io
Location: .venv/lib/python3.12/site-packages
Requires: charset-normalizer, idna, urllib3, certifi
```

---

## 3. Freezing and Restoring Dependencies

### Freezing (Exporting)

```bash
pip freeze > requirements.txt
```

This generates a file listing every installed package and its exact version:

```text
Flask==3.0.0
requests==2.31.0
Jinja2==3.1.3
```

### Restoring (Installing from File)

```bash
pip install -r requirements.txt
```

---

## 4. Best Practices

1. **Always work inside a virtual environment** before running `pip install`.
2. **Pin exact versions** in `requirements.txt` for production deployments (`==`).
3. **Use `pip freeze`** to capture the current state after adding or removing packages.
4. **Never run `pip install` as root/admin** unless you explicitly intend to modify the system Python.
