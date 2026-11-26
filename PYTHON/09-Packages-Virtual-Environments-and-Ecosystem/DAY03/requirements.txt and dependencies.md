# Python requirements.txt and Dependency Management

---

## 1. What is `requirements.txt`?

`requirements.txt` is a plain-text file that lists the Python packages required by a project, along with their version constraints. It serves as the **dependency manifest** for reproducible installations.

---

## 2. File Format and Version Specifiers

```text
# Exact version pinning (recommended for production)
Flask==3.0.0
requests==2.31.0
SQLAlchemy==2.0.25

# Minimum version
pytest>=7.0

# Compatible release (allows patch updates only)
numpy~=1.26.0

# Version range
pandas>=2.0,<2.2

# No version constraint (installs latest — risky!)
black
```

### Version Specifier Reference

| Specifier | Meaning | Example |
|---|---|---|
| `==` | Exact match | `requests==2.31.0` |
| `>=` | Minimum version | `pytest>=7.0` |
| `<=` | Maximum version | `numpy<=1.26.4` |
| `~=` | Compatible release (same major.minor) | `flask~=3.0.0` → allows `3.0.x` |
| `!=` | Exclude specific version | `urllib3!=2.0.0` |

---

## 3. Generating `requirements.txt`

```bash
# Activate your virtual environment first!
pip freeze > requirements.txt
```

---

## 4. Installing from `requirements.txt`

```bash
# On a new machine or fresh virtual environment
python -m venv .venv
source .venv/bin/activate      # or .venv\Scripts\Activate.ps1 on Windows
pip install -r requirements.txt
```

---

## 5. Development vs Production Dependencies

Many projects maintain separate files:

```text
project/
├── requirements.txt          # Production dependencies
├── requirements-dev.txt      # Development/testing tools
└── ...
```

**`requirements-dev.txt`:**

```text
-r requirements.txt       # Include all production deps
pytest==8.0.0
black==24.1.0
mypy==1.8.0
```

Install dev dependencies: `pip install -r requirements-dev.txt`

---

## 6. Best Practices

1. **Always pin exact versions** (`==`) in production `requirements.txt` for deterministic builds.
2. **Regenerate** after adding or removing packages: `pip freeze > requirements.txt`.
3. **Commit `requirements.txt` to Git** — it is a critical project artifact.
4. **Never commit `.venv/`** — only the requirements file.
