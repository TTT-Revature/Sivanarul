# Python pathlib Module

---

## 1. Introduction to pathlib

The `pathlib` module (introduced in Python 3.4) offers an object-oriented approach to working with filesystem paths. Instead of manipulating file paths as raw strings with `os.path`, `pathlib` provides intuitive classes representing paths across different operating systems.

### Why pathlib over os.path?

- **Object-Oriented:** Paths are objects with helpful properties and methods.
- **Cross-Platform:** Automatically handles Windows `\` and Unix `/` separators.
- **Cleaner Syntax:** Uses the `/` operator to construct paths cleanly.

---

## 2. Creating and Inspecting Paths

```python
from pathlib import Path

# Current working directory and home directory
cwd = Path.cwd()
home = Path.home()
print("Current Directory:", cwd)
print("Home Directory:   ", home)

# Constructing a path using the / operator
file_path = cwd / "data" / "reports" / "summary.txt"
print("Constructed Path:", file_path)

# Path components
print("Name:     ", file_path.name)       # summary.txt
print("Stem:     ", file_path.stem)       # summary
print("Suffix:   ", file_path.suffix)     # .txt
print("Parent:   ", file_path.parent)     # data/reports
```

**Output:**

```text
Current Directory: C:\Users\SivanarulA\Desktop\FDE
Home Directory:    C:\Users\SivanarulA
Constructed Path: C:\Users\SivanarulA\Desktop\FDE\data\reports\summary.txt
Name:      summary.txt
Stem:      summary
Suffix:    .txt
Parent:    C:\Users\SivanarulA\Desktop\FDE\data\reports
```

---

## 3. Common Filesystem Operations

```python
from pathlib import Path

# Create a directory safely (parents=True creates intermediate dirs, exist_ok=True prevents errors)
docs_dir = Path("my_workspace") / "notes"
docs_dir.mkdir(parents=True, exist_ok=True)

# Write and read text directly without open() boilerplate
note_file = docs_dir / "todo.txt"
note_file.write_text("1. Learn Pathlib\n2. Build project", encoding="utf-8")

# Read file content
content = note_file.read_text(encoding="utf-8")
print("Content:\n" + content)

# Check file existence and type
print("Exists? ", note_file.exists())
print("Is File?", note_file.is_file())
print("Is Dir? ", docs_dir.is_dir())
```

**Output:**

```text
Content:
1. Learn Pathlib
2. Build project
Exists?  True
Is File? True
Is Dir?  True
```

---

## 4. Searching and Iterating Directories

```python
from pathlib import Path

base = Path("my_workspace")

# Iterate over all direct items
for item in base.iterdir():
    print("Item:", item.name)

# Glob pattern matching (recursive search with **/*)
for txt_file in base.glob("**/*.txt"):
    print("Found text file:", txt_file.name)
```

**Output:**

```text
Item: notes
Found text file: todo.txt
```

---

## 5. Summary Table

| Method / Property | Description |
|---|---|
| `Path.cwd()` | Returns current working directory |
| `p.exists()` | Checks if path exists |
| `p.is_file()` / `p.is_dir()` | Checks if path is a file or directory |
| `p.mkdir(parents=True, exist_ok=True)` | Creates directory tree safely |
| `p.read_text()` / `p.write_text()` | Reads or writes string data directly |
| `p.glob(pattern)` | Finds matching files using wildcards |
