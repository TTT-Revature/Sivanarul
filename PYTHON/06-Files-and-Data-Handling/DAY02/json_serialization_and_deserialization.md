# Python JSON Serialization and Deserialization

---

## 1. Introduction to JSON

**JSON (JavaScript Object Notation)** is a lightweight, language-independent data-interchange format widely used in REST APIs, web services, and configuration files.

Python provides the built-in `json` module to convert between Python objects and JSON data:

- **Serialization (Dumping / Encoding):** Converting a Python object into a JSON string or file.
- **Deserialization (Loading / Decoding):** Parsing a JSON string or file into a Python object.

---

## 2. Python to JSON Type Mapping

| Python Type | JSON Equivalent |
|---|---|
| `dict` | object `{}` |
| `list`, `tuple` | array `[]` |
| `str` | string `""` |
| `int`, `float` | number |
| `True` / `False` | `true` / `false` |
| `None` | `null` |

---

## 3. Serialization: `dumps()` and `dump()`

- `json.dumps(obj)`: Serializes Python object to a JSON **string**.
- `json.dump(obj, file)`: Serializes Python object directly into a **file**.

```python
import json

employee = {
    "id": 101,
    "name": "Sivanarul",
    "is_active": True,
    "skills": ["Python", "SQL", "Docker"],
    "bonus": None
}

# dumps(): converts to formatted JSON string
json_string = json.dumps(employee, indent=2)
print(json_string)

# dump(): writes directly to a file
with open("employee.json", "w", encoding="utf-8") as f:
    json.dump(employee, f, indent=4)
```

**Output:**

```json
{
  "id": 101,
  "name": "Sivanarul",
  "is_active": true,
  "skills": [
    "Python",
    "SQL",
    "Docker"
  ],
  "bonus": null
}
```

---

## 4. Deserialization: `loads()` and `load()`

- `json.loads(string)`: Parses JSON **string** to a Python dictionary/list.
- `json.load(file)`: Reads and parses a JSON **file** into a Python object.

```python
import json

raw_json = '{"sku": "LAP-01", "price": 899.99, "in_stock": true}'

# loads(): parse from string
data = json.loads(raw_json)
print("Product SKU:", data["sku"])
print("In Stock?   ", data["in_stock"])
print("Type:       ", type(data))

# load(): parse from file
with open("employee.json", "r", encoding="utf-8") as f:
    loaded_emp = json.load(f)
print("Loaded Name:", loaded_emp["name"])
```

**Output:**

```text
Product SKU: LAP-01
In Stock?    True
Type:        <class 'dict'>
Loaded Name: Sivanarul
```

---

## 5. Handling Custom Objects

Non-serializable types (like datetime or custom classes) require a custom encoder function:

```python
import json
from datetime import datetime

class User:
    def __init__(self, username):
        self.username = username

def custom_encoder(obj):
    if isinstance(obj, User):
        return {"username": obj.username}
    if isinstance(obj, datetime):
        return obj.isoformat()
    raise TypeError("Not serializable")

payload = {"user": User("arun99"), "created_at": datetime(2026, 11, 17, 10, 0)}
print(json.dumps(payload, default=custom_encoder))
```

**Output:**

```text
{"user": {"username": "arun99"}, "created_at": "2026-11-17T10:00:00"}
```
