# Working with CSV Files in Python

---

## 1. Introduction to CSV

A **CSV (Comma-Separated Values)** file is a plain-text file that stores tabular data. Each line represents a record, and fields are separated by delimiters (typically commas).

Python provides the built-in `csv` module for reading and writing CSV files safely, managing quotation, commas within text, and platform line-endings.

---

## 2. Writing CSV Files

### 1. Using `csv.writer` (List-based)

```python
import csv

employees = [
    ["ID", "Name", "Department", "Salary"],
    [101, "Sivanarul", "Engineering", 75000],
    [102, "Priya", "HR", 62000],
    [103, "Karan", "Finance", 68000]
]

# newline="" is essential to prevent blank lines on Windows
with open("employees.csv", mode="w", newline="", encoding="utf-8") as f:
    writer = csv.writer(f)
    writer.writerows(employees)

print("employees.csv created successfully.")
```

---

### 2. Using `csv.DictWriter` (Dictionary-based)

```python
import csv

data = [
    {"id": 1, "product": "Keyboard", "price": 45.0},
    {"id": 2, "product": "Mouse", "price": 25.0}
]

fields = ["id", "product", "price"]

with open("products.csv", mode="w", newline="", encoding="utf-8") as f:
    writer = csv.DictWriter(f, fieldnames=fields)
    writer.writeheader()
    writer.writerows(data)
```

---

## 3. Reading CSV Files

### 1. Using `csv.reader` (Row-by-Row as Lists)

```python
import csv

with open("employees.csv", mode="r", encoding="utf-8") as f:
    reader = csv.reader(f)
    header = next(reader)  # Extract header row
    print("Header:", header)
    for row in reader:
        print(f"ID: {row[0]}, Name: {row[1]}, Salary: ${row[3]}")
```

**Output:**

```text
Header: ['ID', 'Name', 'Department', 'Salary']
ID: 101, Name: Sivanarul, Salary: $75000
ID: 102, Name: Priya, Salary: $62000
ID: 103, Name: Karan, Salary: $68000
```

---

### 2. Using `csv.DictReader` (Rows as Dictionaries)

`csv.DictReader` maps each row directly to a dictionary where keys are the header names:

```python
import csv

with open("products.csv", mode="r", encoding="utf-8") as f:
    reader = csv.DictReader(f)
    for row in reader:
        print(f"Product: {row['product']:<10} | Price: ${row['price']}")
```

**Output:**

```text
Product: Keyboard   | Price: $45.0
Product: Mouse      | Price: $25.0
```

---

## 4. Custom Delimiters (TSV and Semicolons)

You can specify different delimiters (such as tabs `\t` or pipes `|`):

```python
import csv

# Reading pipe-delimited file
with open("data.pipe", mode="r", encoding="utf-8") as f:
    reader = csv.reader(f, delimiter="|")
```

---

## 5. Best Practices

1. **Always specify `newline=""`** when opening files for writing to prevent extra blank rows on Windows.
2. **Specify `encoding="utf-8"`** to prevent character encoding issues across operating systems.
3. **Prefer `DictReader` and `DictWriter`** over index-based readers to keep code readable and immune to column reordering.
