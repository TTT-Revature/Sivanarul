# Python Date Formatting and Parsing (`strftime` and `strptime`)

---

## 1. Introduction

Converting between human-readable date strings and Python `datetime` objects is essential when handling API data, logs, and databases.

- **`strftime()` (String Format Time):** Converts a `datetime` object **into** a formatted string.
- **`strptime()` (String Parse Time):** Parses a date string **into** a `datetime` object.

> **Memory aid:** `f` stands for **Format** (object to string); `p` stands for **Parse** (string to object).

---

## 2. Common Format Directives

| Directive | Meaning | Example |
|---|---|---|
| `%Y` | 4-digit Year | `2026` |
| `%y` | 2-digit Year | `26` |
| `%m` | 2-digit Month (`01`–`12`) | `11` |
| `%B` | Full Month Name | `November` |
| `%b` | Abbreviated Month Name | `Nov` |
| `%d` | 2-digit Day of Month (`01`–`31`) | `17` |
| `%H` | 24-hour format (`00`–`23`) | `14` |
| `%I` | 12-hour format (`01`–`12`) | `02` |
| `%p` | AM / PM | `PM` |
| `%M` | Minute (`00`–`59`) | `45` |
| `%S` | Second (`00`–`59`) | `30` |

---

## 3. Formatting Dates with `strftime()`

```python
from datetime import datetime

now = datetime(2026, 11, 17, 14, 30, 0)

# Format: YYYY-MM-DD
print(now.strftime("%Y-%m-%d"))

# Format: DD/MM/YYYY HH:MM:SS
print(now.strftime("%d/%m/%Y %H:%M:%S"))

# Human readable: 17 November, 2026 (02:30 PM)
print(now.strftime("%d %B, %Y (%I:%M %p)"))

# ISO 8601 standard format
print(now.isoformat())
```

**Output:**

```text
2026-11-17
17/11/2026 14:30:00
17 November, 2026 (02:30 PM)
2026-11-17T14:30:00
```

---

## 4. Parsing Dates with `strptime()`

```python
from datetime import datetime

# Parse standard date string
date_str1 = "2026-11-17"
dt1 = datetime.strptime(date_str1, "%Y-%m-%d")
print("Parsed 1:", dt1)

# Parse custom log timestamp
log_entry = "Nov 17, 2026 09:15:30 AM"
dt2 = datetime.strptime(log_entry, "%b %d, %Y %I:%M:%S %p")
print("Parsed 2:", dt2)
print("Month extracted:", dt2.month)
```

**Output:**

```text
Parsed 1: 2026-11-17 00:00:00
Parsed 2: 2026-11-17 09:15:30
Month extracted: 11
```

---

## 5. Handling `ValueError` during Parsing

If the string format does not match the directive pattern, a `ValueError` is raised:

```python
from datetime import datetime

raw_input = "17-11-2026"

try:
    dt = datetime.strptime(raw_input, "%Y/%m/%d")
except ValueError as e:
    print("Parsing failed:", e)
```

**Output:**

```text
Parsing failed: time data '17-11-2026' does not match format '%Y/%m/%d'
```
