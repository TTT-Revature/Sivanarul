# Python Logging and Log Levels

---

## 1. Why Logging instead of `print()`?

While `print()` outputs transient text to the console, the built-in `logging` module offers:

- **Configurable Log Levels:** Filter messages by severity.
- **Contextual Metadata:** Timestamps, line numbers, module names, thread IDs.
- **Destination Flexibility:** Write simultaneously to console, files, and remote log aggregators.
- **Zero Code Modification:** Toggle verbosity across production vs development via configuration.

---

## 2. The 5 Standard Log Levels

| Level | Numeric Value | When to Use |
|---|:---:|---|
| `DEBUG` | 10 | Detailed diagnostic information for diagnosing bugs. |
| `INFO` | 20 | Confirmation that systems are functioning as expected. |
| `WARNING` | 30 | Indication that something unexpected happened (default level). |
| `ERROR` | 40 | Serious issue; application unable to perform a function. |
| `CRITICAL` | 50 | Fatal error; application may abort execution immediately. |

---

## 3. Basic Configuration Example

```python
import logging

# Configure root logger format and minimum threshold
logging.basicConfig(
    level=logging.INFO,
    format="%(asctime)s [%(levelname)s] %(name)s: %(message)s",
    datefmt="%Y-%m-%d %H:%M:%S"
)

logger = logging.getLogger("AppService")

# Logging messages at various levels
logger.debug("Parsing payload parameters...")       # Skipped (below INFO)
logger.info("Database connection established.")      # Emitted
logger.warning("Cache miss for user_id=412.")        # Emitted
logger.error("Failed to query payment gateway.")     # Emitted
logger.critical("Primary disk storage full!")        # Emitted
```

**Output:**

```text
2026-11-17 15:35:10 [INFO] AppService: Database connection established.
2026-11-17 15:35:10 [WARNING] AppService: Cache miss for user_id=412.
2026-11-17 15:35:10 [ERROR] AppService: Failed to query payment gateway.
2026-11-17 15:35:10 [CRITICAL] AppService: Primary disk storage full!
```

---

## 4. Logging Exceptions (`logger.exception`)

When an exception occurs inside a `try-except` block, `logger.exception()` automatically captures the entire stack trace:

```python
try:
    val = 1 / 0
except ZeroDivisionError:
    logger.exception("An unhandled math error occurred:")
```
