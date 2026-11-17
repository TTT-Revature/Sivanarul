# Python Environment Variables

---

## 1. Introduction

**Environment variables** are dynamic values configured at the operating system level outside application code. They are essential for:

- **Security:** Keeping secrets (API keys, database passwords, tokens) out of source control.
- **Configurability:** Configuring environment-specific parameters (development vs production hosts).

Python accesses environment variables through the built-in `os` module.

---

## 2. Accessing Environment Variables

### 1. `os.environ` Dictionary

`os.environ` behaves like a Python dictionary of all current environment variables. Accessing a missing key via `[]` raises a `KeyError`.

```python
import os

# Accessing existing variable
user_path = os.environ["PATH"]
print("PATH exists:", len(user_path) > 0)

# Missing key raises KeyError
try:
    secret = os.environ["API_SECRET_KEY"]
except KeyError:
    print("API_SECRET_KEY is not defined!")
```

---

### 2. `os.environ.get()` (Recommended)

Returns a fallback default value instead of raising an error:

```python
import os

# Safe lookup with default fallback
db_host = os.environ.get("DB_HOST", "localhost")
db_port = int(os.environ.get("DB_PORT", 5432))
debug_mode = os.environ.get("DEBUG", "False").lower() in ("true", "1")

print(f"Host: {db_host}, Port: {db_port}, Debug: {debug_mode}")
```

**Output:**

```text
Host: localhost, Port: 5432, Debug: False
```

---

## 3. Setting Environment Variables in Python

You can modify or add environment variables within the current process lifetime using `os.environ`:

```python
import os

os.environ["APP_ENV"] = "production"
print("Environment:", os.environ.get("APP_ENV"))
```

> **Note:** Changes made via `os.environ` only affect the current Python process and its child processes; they do **not** permanently modify the host operating system.

---

## 4. Best Practices

1. **Never commit `.env` files** or hardcoded credentials to Git. Add `.env` to `.gitignore`.
2. **Always provide sensible defaults** using `os.environ.get(key, default)` for non-sensitive values.
3. **Parse types explicitly:** Environment variables are always retrieved as strings; cast numbers with `int()` or booleans with `.lower() == 'true'`.
