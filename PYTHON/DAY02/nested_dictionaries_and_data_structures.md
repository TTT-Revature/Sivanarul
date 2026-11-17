# Python Nested Dictionaries and Complex Data Structures

---

## 1. Introduction to Nested Data Structures

In real-world software engineering, data rarely exists as flat, single-level collections. Modern applications frequently handle hierarchical, multi-dimensional, and relational data.

A **nested dictionary** is a dictionary where values are themselves dictionaries, lists, sets, tuples, or combinations of these data types.

Nested data structures are the foundational representation in Python for:

- **JSON Data:** REST API request and response payloads.
- **Document Databases:** MongoDB and NoSQL document representations.
- **Application Configurations:** YAML and JSON configuration settings.
- **Enterprise Entities:** Complex domain models such as users, orders, invoices, and catalog hierarchies.

### Real-World Analogy

Consider an **E-Commerce Order System**:

- An **Order** contains an `order_id`, `customer_details`, `shipping_address`, and `line_items`.
- `customer_details` is a nested dictionary with `name`, `email`, and `phone`.
- `shipping_address` is a nested dictionary with `street`, `city`, `state`, and `pincode`.
- `line_items` is a list of product dictionaries, each with `sku`, `title`, `price`, and `quantity`.

---

## 2. Creating Nested Dictionaries

### Example 1: Corporate Organizational Directory

```python
organization = {
    "engineering": {
        "team_leads": {
            "backend": "Arun Kumar",
            "frontend": "Sivanarul"
        },
        "headcount": 45,
        "active_projects": ["Cloud Migration", "AI Assistant", "Data Pipeline"]
    },
    "human_resources": {
        "manager": "Priya Sharma",
        "headcount": 8,
        "active_projects": ["Q4 Campus Hiring", "Annual Appraisal"]
    }
}

import pprint
pprint.pprint(organization)
```

**Output:**

```text
{'engineering': {'active_projects': ['Cloud Migration',
                                     'AI Assistant',
                                     'Data Pipeline'],
                 'headcount': 45,
                 'team_leads': {'backend': 'Arun Kumar',
                                'frontend': 'Sivanarul'}},
 'human_resources': {'active_projects': ['Q4 Campus Hiring',
                                         'Annual Appraisal'],
                     'headcount': 8,
                     'manager': 'Priya Sharma'}}
```

---

### Example 2: Student Academic Record

```python
students = {
    "STU101": {
        "name": "Arun",
        "courses": {
            "Python": {"quiz": 88, "midterm": 92, "final": 95},
            "Database": {"quiz": 80, "midterm": 85, "final": 90}
        },
        "attendance_pct": 96.5
    },
    "STU102": {
        "name": "Kavitha",
        "courses": {
            "Python": {"quiz": 92, "midterm": 94, "final": 98},
            "Database": {"quiz": 85, "midterm": 89, "final": 92}
        },
        "attendance_pct": 98.0
    }
}
```

---

## 3. Accessing Data in Nested Dictionaries

### 1. Chained Square Bracket Indexing

Access inner elements by cascading index keys from the outermost level to the target field:

$$\text{data}[\text{level1}][\text{level2}][\text{level3}]$$

```python
# Accessing Arun's final exam score in Python
score = students["STU101"]["courses"]["Python"]["final"]
print("STU101 Python Final Score:", score)

# Accessing engineering's backend lead
lead = organization["engineering"]["team_leads"]["backend"]
print("Backend Lead:", lead)

# Accessing the second active project in engineering
project_2 = organization["engineering"]["active_projects"][1]
print("Second Project:", project_2)
```

**Output:**

```text
STU101 Python Final Score: 95
Backend Lead: Arun Kumar
Second Project: AI Assistant
```

---

### 2. Handling Missing Intermediate Keys (`KeyError`)

If any key along the chain does not exist, standard indexing raises a `KeyError` and halts program execution.

```python
try:
    print(organization["marketing"]["headcount"])
except KeyError as e:
    print(f"KeyError encountered: {e}")
```

**Output:**

```text
KeyError encountered: 'marketing'
```

---

### 3. Safe Lookup with Chained `.get()`

To avoid runtime exceptions, you can chain `.get()` calls by passing an empty dictionary `{}` as the fallback for intermediate levels:

```python
# Safe navigation
marketing_headcount = organization.get("marketing", {}).get("headcount", "Not Found")
print("Marketing Headcount:", marketing_headcount)
```

**Output:**

```text
Marketing Headcount: Not Found
```

---

### 4. Enterprise Best Practice: A Reusable `deep_get` Helper

In production systems, deep nested lookups are best handled with a robust utility function that traverses arbitrary key paths:

```python
def deep_get(dictionary, keys, default=None):
    """
    Safely retrieves a value from a nested dictionary given a list of keys.
    """
    current = dictionary
    for key in keys:
        if isinstance(current, dict) and key in current:
            current = current[key]
        else:
            return default
    return current

# Test lookups
res1 = deep_get(students, ["STU102", "courses", "Python", "final"])
print("Found score:   ", res1)

res2 = deep_get(students, ["STU999", "courses", "Python", "final"], default="N/A")
print("Missing student:", res2)
```

**Output:**

```text
Found score:    98
Missing student: N/A
```

---

## 4. Modifying and Adding to Nested Dictionaries

### 1. Adding a New Nested Level

```python
# Add a new department
organization["finance"] = {
    "manager": "Ramesh Patel",
    "headcount": 12,
    "active_projects": ["Q4 Budgeting"]
}

# Add a new team lead in engineering
organization["engineering"]["team_leads"]["devops"] = "Karan Singh"

print("Updated Team Leads:", organization["engineering"]["team_leads"])
```

**Output:**

```text
Updated Team Leads: {'backend': 'Arun Kumar', 'frontend': 'Sivanarul', 'devops': 'Karan Singh'}
```

---

### 2. Updating Existing Values

```python
# Increment headcount
organization["engineering"]["headcount"] += 5
print("New Engineering Headcount:", organization["engineering"]["headcount"])
```

**Output:**

```text
New Engineering Headcount: 50
```

---

### 3. Mutating Nested Collections (Lists / Sets)

```python
# Append a new project to the list inside the dictionary
organization["engineering"]["active_projects"].append("Security Hardening")

print("Engineering Projects:", organization["engineering"]["active_projects"])
```

**Output:**

```text
Engineering Projects: ['Cloud Migration', 'AI Assistant', 'Data Pipeline', 'Security Hardening']
```

---

## 5. Deleting Elements from Nested Structures

### 1. Using `del`
Deletes a nested field by exact key reference.

```python
# Remove devops lead
del organization["engineering"]["team_leads"]["devops"]
print(organization["engineering"]["team_leads"])
```

**Output:**

```text
{'backend': 'Arun Kumar', 'frontend': 'Sivanarul'}
```

---

### 2. Using `.pop()`
Removes a nested field and returns its value safely.

```python
# Pop frontend lead safely
removed_lead = organization["engineering"]["team_leads"].pop("frontend", "None")
print("Removed:", removed_lead)
print("Remaining:", organization["engineering"]["team_leads"])
```

**Output:**

```text
Removed: Sivanarul
Remaining: {'backend': 'Arun Kumar'}
```

---

## 6. Combining Compound Data Structures

In Python enterprise development, different data structures are combined to represent real-world entities:

| Data Structure Pattern | Typical Use Case | Example Structure |
| :--- | :--- | :--- |
| **List of Dictionaries** | Relational database rows / API query results | `[{"id": 1, "name": "A"}, {"id": 2, "name": "B"}]` |
| **Dictionary of Lists** | Grouping items under categories | `{"fruits": ["apple", "mango"], "veggies": ["carrot"]}` |
| **Dictionary of Sets** | Graph adjacency lists / Unique tag catalogs | `{"user_1": {"admin", "editor"}, "user_2": {"viewer"}}` |
| **Tuples as Keys** | Multi-dimensional coordinates / Grid lookups | `{(0, 0): "Origin", (1, 5): "Checkpoint"}` |

### Example: Processing a List of Dictionaries

```python
employees = [
    {"id": 101, "name": "Arun", "dept": "Engineering", "salary": 80000},
    {"id": 102, "name": "Priya", "dept": "HR", "salary": 65000},
    {"id": 103, "name": "Siva", "dept": "Engineering", "salary": 92000},
    {"id": 104, "name": "Deepa", "dept": "Finance", "salary": 72000}
]

# Calculate total salary for Engineering department
eng_total_salary = sum(emp["salary"] for emp in employees if emp["dept"] == "Engineering")
print(f"Total Engineering Payroll: ${eng_total_salary}")

# Group employee names by department
dept_group = {}
for emp in employees:
    dept_group.setdefault(emp["dept"], []).append(emp["name"])

print("Employees by Department:", dept_group)
```

**Output:**

```text
Total Engineering Payroll: $172000
Employees by Department: {'Engineering': ['Arun', 'Siva'], 'HR': ['Priya'], 'Finance': ['Deepa']}
```

---

## 7. Iterating Over Nested Dictionaries

### 1. Iterating Two-Level Dictionaries

```python
user_permissions = {
    "admin": {"read": True, "write": True, "delete": True},
    "editor": {"read": True, "write": True, "delete": False},
    "guest": {"read": True, "write": False, "delete": False}
}

for role, perms in user_permissions.items():
    print(f"\nRole: {role.upper()}")
    for action, is_allowed in perms.items():
        status = "ALLOWED" if is_allowed else "DENIED"
        print(f"  - {action:<8}: {status}")
```

**Output:**

```text
Role: ADMIN
  - read    : ALLOWED
  - write   : ALLOWED
  - delete  : ALLOWED

Role: EDITOR
  - read    : ALLOWED
  - write   : ALLOWED
  - delete  : DENIED

Role: GUEST
  - read    : ALLOWED
  - write   : DENIED
  - delete  : DENIED
```

---

### 2. Flattening a Nested Dictionary

Converting a hierarchical dictionary into a single-level dictionary with dot-delimited compound keys (e.g., `"user.address.city"`):

```python
def flatten_dict(nested_dict, parent_key='', sep='.'):
    items = []
    for k, v in nested_dict.items():
        new_key = f"{parent_key}{sep}{k}" if parent_key else k
        if isinstance(v, dict):
            items.extend(flatten_dict(v, new_key, sep=sep).items())
        else:
            items.append((new_key, v))
    return dict(items)

config = {
    "database": {
        "host": "localhost",
        "auth": {
            "user": "root",
            "password": "secret_password"
        }
    },
    "server": {
        "port": 8080
    }
}

flat = flatten_dict(config)
for key, val in flat.items():
    print(f"{key:<25} = {val}")
```

**Output:**

```text
database.host             = localhost
database.auth.user        = root
database.auth.password    = secret_password
server.port               = 8080
```

---

## 8. Deep Copying vs Shallow Copying

A shallow copy (`dict.copy()`) duplicates only the top-level dictionary references. The nested dictionaries or lists still point to the exact same objects in memory.

To completely isolate a nested structure, use `copy.deepcopy()`.

```python
import copy

system_cfg = {
    "app": "API Gateway",
    "ports": {"http": 80, "https": 443}
}

# Shallow copy
shallow_cfg = system_cfg.copy()

# Deep copy
deep_cfg = copy.deepcopy(system_cfg)

# Mutate nested dictionary in original
system_cfg["ports"]["http"] = 8080

print("Original:   ", system_cfg["ports"])
print("Shallow:    ", shallow_cfg["ports"])  # Unintentionally corrupted!
print("Deep Copy:  ", deep_cfg["ports"])     # Preserved original value!
```

**Output:**

```text
Original:    {'http': 8080, 'https': 443}
Shallow:     {'http': 8080, 'https': 443}
Deep Copy:   {'http': 80, 'https': 443}
```

---

## 9. Serialization: Working with JSON

Python's built-in `json` module seamlessly converts nested dictionaries to and from JSON formatted strings.

- `json.dumps(obj, indent=4)`: Serializes Python dictionary to a formatted JSON string.
- `json.loads(json_string)`: Deserializes JSON string back to a Python nested dictionary.

```python
import json

order = {
    "order_id": "ORD-2026-9921",
    "customer": {
        "id": "CUST-412",
        "name": "Sivanarul",
        "email": "sivanarul@example.com"
    },
    "items": [
        {"sku": "LAPTOP-01", "name": "Dev Laptop", "qty": 1, "unit_price": 1200.00},
        {"sku": "MOUSE-02", "name": "Wireless Mouse", "qty": 2, "unit_price": 25.50}
    ],
    "is_paid": True
}

# Serialize to JSON formatted string
json_str = json.dumps(order, indent=2)
print("Serialized JSON:\n", json_str)

# Deserialize back to Python object
parsed_order = json.loads(json_str)
print("\nParsed customer name:", parsed_order["customer"]["name"])
```

**Output:**

```text
Serialized JSON:
 {
  "order_id": "ORD-2026-9921",
  "customer": {
    "id": "CUST-412",
    "name": "Sivanarul",
    "email": "sivanarul@example.com"
  },
  "items": [
    {
      "sku": "LAPTOP-01",
      "name": "Dev Laptop",
      "qty": 1,
      "unit_price": 1200.0
    },
    {
      "sku": "MOUSE-02",
      "name": "Wireless Mouse",
      "qty": 2,
      "unit_price": 25.5
    }
  ],
  "is_paid": true
}

Parsed customer name: Sivanarul
```

---

## 10. Real-World Case Study: Calculating Order Total and Invoice Summary

```python
def generate_invoice(order_data):
    customer_name = order_data["customer"]["name"]
    order_id = order_data["order_id"]
    
    subtotal = 0.0
    print(f"INVOICE FOR: {customer_name.upper()} | ORDER: {order_id}")
    print("-" * 55)
    print(f"{'SKU':<12} {'Item Name':<20} {'Qty':<5} {'Total Price':>12}")
    print("-" * 55)
    
    for item in order_data["items"]:
        line_total = item["qty"] * item["unit_price"]
        subtotal += line_total
        print(f"{item['sku']:<12} {item['name']:<20} {item['qty']:<5} ${line_total:>11.2f}")
    
    tax = subtotal * 0.08  # 8% Tax
    grand_total = subtotal + tax
    
    print("-" * 55)
    print(f"{'Subtotal:':<38} ${subtotal:>11.2f}")
    print(f"{'Tax (8%):':<38} ${tax:>11.2f}")
    print(f"{'Grand Total:':<38} ${grand_total:>11.2f}")
    print("-" * 55)

generate_invoice(order)
```

**Output:**

```text
INVOICE FOR: SIVANARUL | ORDER: ORD-2026-9921
-------------------------------------------------------
SKU          Item Name            Qty     Total Price
-------------------------------------------------------
LAPTOP-01    Dev Laptop           1       $    1200.00
MOUSE-02     Wireless Mouse       2       $      51.00
-------------------------------------------------------
Subtotal:                              $    1251.00
Tax (8%):                              $     100.08
Grand Total:                           $    1351.08
-------------------------------------------------------
```

---

## 11. Practice Problems

### Problem 1: Calculate Average Subject Score Across All Students
Given a nested dictionary of student exam marks, calculate the class average for each subject.

```python
exam_results = {
    "Arun": {"Math": 85, "Science": 90, "English": 78},
    "Priya": {"Math": 95, "Science": 88, "English": 92},
    "Siva": {"Math": 75, "Science": 82, "English": 80}
}

def subject_averages(results):
    subject_totals = {}
    subject_counts = {}
    
    for student, subjects in results.items():
        for subject, mark in subjects.items():
            subject_totals[subject] = subject_totals.get(subject, 0) + mark
            subject_counts[subject] = subject_counts.get(subject, 0) + 1
            
    return {sub: round(subject_totals[sub] / subject_counts[sub], 2) for sub in subject_totals}

print(subject_averages(exam_results))
```

**Output:**

```text
{'Math': 85.0, 'Science': 86.67, 'English': 83.33}
```
