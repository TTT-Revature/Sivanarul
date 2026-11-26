
# Hash Tables and Hash Functions

## 1. Introduction

A Hash Table is a data structure used to store data in **key-value pairs**.

It allows us to insert, search, and delete data efficiently using keys.

### Real-world example

Imagine a student database:

| Roll Number | Student Name |
|---|---|
| 101 | Arun |
| 102 | Kumar |
| 103 | Priya |

Instead of searching every student one by one, we can use the roll number to calculate where the information should be stored.

A Hash Table uses a Hash Function to determine the storage location.

### Basic idea

```text
       Key
        |
        v
   Hash Function
        |
        v
    Index (2)
        |
        v
   Hash Table
```

The hash function converts a key into an array index.

---

## 2. What Is a Hash Table?

A Hash Table is a data structure that stores information using key-value pairs.

Example:

```python
student = {
    101: "Arun",
    102: "Kumar",
    103: "Priya"
}
```

Here:

- 101, 102, 103 are keys.
- Arun, Kumar, Priya are values.

We can access a value using its key.

```python
print(student[102])
```

Output:

```text
Kumar
```

### Important characteristics

- Stores key-value pairs.
- Uses a hash function to calculate an index.
- Provides fast average-case lookup.
- Handles collisions using specific techniques.
- Keys must be hashable in Python dictionaries.

---

## 3. What Is a Hash Function?

A Hash Function converts a key into a numerical hash value.

That value is then used to determine the index in a hash table.

Example:

```python
def hash_function(key, table_size):

    return key % table_size
```

Suppose:

```python
key = 25
table_size = 10
```

Calculation:

```text
25 % 10 = 5
```

Therefore:

```text
Hash Index = 5
```

The key 25 will be assigned to index 5.

### Visual representation

```text
Key = 25
   |
   v
Hash Function
25 % 10
   |
   v
Index = 5

Hash Table:

Index   Value
  0       -
  1       -
  2       -
  3       -
  4       -
  5      25
  6       -
  7       -
  8       -
  9       -
```

The modulo operator (%) is commonly used in simple educational hash functions.

Real hash functions are more sophisticated, especially for strings and security-sensitive applications.

---

## 4. Properties of a Good Hash Function

A good hash function should have the following properties:

### A. Deterministic

The same key should produce the same hash value under the same hash-function configuration.

Example:

```python
hash_function(25, 10)
hash_function(25, 10)
```

Both return:

```text
5
```

### B. Uniform Distribution

Keys should be distributed across the available table positions as evenly as possible.

Poor distribution can create many collisions.

### C. Efficient Computation

The hash function should be fast to calculate.

### D. Consistent With Equality

If two keys are equal, they must have equal hash values.

In Python:

```python
a = "hello"
b = "hello"

print(a == b)
print(hash(a) == hash(b))
```

Output:

```text
True
True
```

The reverse is not guaranteed: two different keys may have the same hash value.

---

## 5. What Is a Collision?

A Collision happens when two different keys produce the same table index.

Example:

```python
def hash_function(key, table_size):
    return key % table_size
```

Consider:

```text
Key 1 = 15
Key 2 = 25
Table Size = 10
```

Calculations:

```text
15 % 10 = 5
25 % 10 = 5
```

Both keys produce index 5.

This is called a collision.

### Visual representation

```text
Key 15 ----\
            \
             Hash Function ---> Index 5
            /
Key 25 ----/
```

Both keys want to occupy the same position.

A Hash Table needs a collision-handling technique.

---

## 6. Collision Handling Techniques

Two common collision-handling approaches are:

1. Separate Chaining
2. Open Addressing

### A. Separate Chaining

In Separate Chaining, each table position stores a collection of entries, commonly a linked list.

If multiple keys produce the same index, they are stored in that position's collection.

Example:

```text
Key 15 -> Index 5
Key 25 -> Index 5
Key 35 -> Index 5
```

Visual representation:

```text
Index       Values

  0          None
  1          None
  2          None
  3          None
  4          None
  5          15 -> 25 -> 35
  6          None
  7          None
  8          None
  9          None
```

All three keys are stored in the same bucket.

Advantages:

- Simple collision handling.
- Multiple entries can occupy the same bucket.
- Table does not need an empty slot for every new entry.

Disadvantages:

- Additional memory is needed for bucket collections.
- Long chains can slow down searching.

### B. Open Addressing

In Open Addressing, all entries are stored directly inside the hash table's array.

When a collision occurs, the algorithm searches for another available position.

Common techniques:

1. Linear Probing
2. Quadratic Probing
3. Double Hashing

---

## 7. Linear Probing

Linear Probing checks the next available position when a collision occurs.

Formula:

```text
New Index = (Hash Index + i) % Table Size
```

Here, i is the number of attempts, starting from 0.

Example:

```text
Table Size = 10
Hash Function = key % 10

Keys = 15, 25, 35
```

### Step 1

Insert 15:

```text
15 % 10 = 5
```

Index 5 is empty.

Store 15 at index 5.

### Step 2

Insert 25:

```text
25 % 10 = 5
```

Index 5 is occupied.

Check the next position: index 6.

Store 25 at index 6.

### Step 3

Insert 35:

```text
35 % 10 = 5
```

Index 5 is occupied.

Check index 6: occupied.

Check index 7: empty.

Store 35 at index 7.

Final table:

```text
Index     Value

  0        -
  1        -
  2        -
  3        -
  4        -
  5       15
  6       25
  7       35
  8        -
  9        -
```

### Disadvantage

Linear Probing can cause Primary Clustering.

Primary Clustering means groups of consecutive occupied positions form, causing future insertions and searches to require more checks.

---

## 8. Quadratic Probing

Quadratic Probing checks positions using squared increments.

Formula:

```text
New Index = (Hash Index + i²) % Table Size
```

Example:

```text
Hash Index = 5
Table Size = 10
```

Possible positions:

```text
i = 0: (5 + 0²) % 10 = 5

i = 1: (5 + 1²) % 10 = 6

i = 2: (5 + 2²) % 10 = 9

i = 3: (5 + 3²) % 10 = 4
```

Instead of checking consecutive positions, it follows a quadratic pattern.

Advantages:

- Reduces primary clustering.

Disadvantages:

- May still cause secondary clustering.
- Some table-size and probing configurations may fail to visit every slot.

---

## 9. Double Hashing

Double Hashing uses two hash functions.

The first function calculates the initial index.

The second function calculates the step size.

Formula:

```text
New Index = (h1(key) + i * h2(key)) % Table Size
```

Example:

```python
def h1(key):
    return key % 10

def h2(key):
    return 7 - (key % 7)
```

The second hash function determines how far to move when a collision occurs.

Advantages:

- Reduces clustering compared with linear probing.
- Can distribute probes more effectively.

Important:

The step size must be non-zero and should be relatively prime to the table size to guarantee that every slot can be visited.

---

## 10. Load Factor

Load Factor measures how full a hash table is.

Formula:

```text
Load Factor = Number of Stored Elements / Table Size
```

Example:

```text
Stored Elements = 7
Table Size = 10
```

Calculation:

```text
Load Factor = 7 / 10

             = 0.7
```

The table is 70% full.

### Why is Load Factor important?

As the table becomes fuller:

- Collisions may increase.
- Searching may require more checks.
- Insertion may become slower.

Hash tables often resize when their load factor reaches a configured threshold.

The exact threshold depends on the implementation.

---

## 11. Rehashing

Rehashing means creating a larger hash table and inserting existing entries into their new positions.

Why is it required?

Suppose:

```text
Table Size = 5
Stored Elements = 4
Load Factor = 0.8
```

The table may become crowded.

A larger table can reduce collisions.

### Rehashing process

1. Create a new, larger table.
2. Calculate new indexes for existing keys.
3. Insert all existing entries into the new table.
4. Replace the old table with the new one.

Visual representation:

```text
Old Table:

Size = 5

[10] [20] [30] [40] [ ]

          |
          v

     Rehashing

          |

          v

New Table:

Size = 10

[ ] [10] [ ] [20] [ ] [30] [ ] [40] [ ] [ ]
```

The example illustrates redistribution; the actual positions depend on the hash function.

Rehashing is expensive for that individual operation, but when resizing is done geometrically, insertion can still have amortized O(1) complexity.

---

## 12. Implementing a Simple Hash Table in Python

Let's build a simple Hash Table using Separate Chaining.

We will support:

- Insert
- Search
- Delete

```python
class HashTable:

    def __init__(self, size):

        self.size = size
        self.table = [[] for _ in range(size)]

    def hash_function(self, key):

        return hash(key) % self.size

    def insert(self, key, value):

        index = self.hash_function(key)

        for i, (existing_key, existing_value) in enumerate(self.table[index]):

            if existing_key == key:

                self.table[index][i] = (key, value)
                return

        self.table[index].append((key, value))

    def search(self, key):

        index = self.hash_function(key)

        for existing_key, value in self.table[index]:

            if existing_key == key:
                return value

        return None

    def delete(self, key):

        index = self.hash_function(key)

        for i, (existing_key, value) in enumerate(self.table[index]):

            if existing_key == key:

                del self.table[index][i]
                return True

        return False


ht = HashTable(10)

ht.insert("name", "Arun")
ht.insert("age", 25)
ht.insert("city", "Chennai")

print(ht.search("name"))
print(ht.search("age"))

print(ht.delete("city"))

print(ht.search("city"))
```

Output:

```text
Arun
25
True
None
```

Explanation:

- `insert()` stores a key-value pair.
- `search()` retrieves the value using its key.
- `delete()` removes the matching key-value pair.
- If a key already exists, `insert()` updates its value.

Note: This is a learning implementation. It does not include resizing or production-level optimizations.

---

## 13. Python Dictionary and Hash Tables

Python provides a built-in dictionary (`dict`).

A dictionary uses hashing internally to support efficient key-based lookup.

Example:

```python
employee = {
    "id": 101,
    "name": "Arun",
    "department": "AI"
}

print(employee["name"])
```

Output:

```text
Arun
```

Common dictionary operations:

### Insert

```python
employee["salary"] = 50000
```

### Update

```python
employee["department"] = "Engineering"
```

### Search

```python
print(employee.get("name"))
```

### Delete

```python
del employee["id"]
```

### Check Key

```python
print("name" in employee)
```

Output:

```text
True
```

Python dictionaries handle collisions internally. You generally do not need to implement collision handling yourself.

---

## 14. Hashable and Unhashable Objects in Python

Python dictionary keys must be hashable.

An object is hashable when:

- It has a hash value that remains stable during its lifetime.
- It can be compared for equality consistently.
- Equal objects have equal hash values.

Common hashable types:

```python
name = "Arun"
age = 25
price = 99.5
status = True
```

These can be used as dictionary keys.

Tuples can also be hashable if all their elements are hashable.

Example:

```python
data = {
    (10, 20): "Point A"
}
```

Common unhashable types:

```python
list
dict
set
```

Example:

```python
data = {}

data[[1, 2, 3]] = "Numbers"
```

This produces:

```text
TypeError: unhashable type: 'list'
```

Why?

A list is mutable. Its contents can change, so it cannot safely be used as a dictionary key.

Important: A tuple containing a list is also unhashable.

---

## 15. Python's hash() Function

Python provides a built-in `hash()` function.

It returns the hash value of a hashable object.

Example:

```python
print(hash(100))
print(hash("python"))
print(hash((10, 20)))
```

The exact output for strings and tuples containing strings may vary between Python processes because Python uses hash randomization for certain types.

Important points:

- Equal objects must have equal hash values.
- Different objects can have the same hash value.
- Hash values are not guaranteed to be unique.
- Do not use Python's built-in hash() as a permanent ID or persistent database identifier.
- Hashing is not the same as encryption.

---

## 16. Hash Table Time Complexity

Let n represent the number of stored elements.

| Operation | Average Case | Worst Case |
|---|---:|---:|
| Insert | O(1) | O(n) |
| Search | O(1) | O(n) |
| Delete | O(1) | O(n) |

Why can the worst case be O(n)?

If many keys collide and are placed in the same bucket, searching may require checking every entry in that bucket.

Space Complexity:

```text
O(n + m)
```

For a chained hash table:

- n = number of stored entries.
- m = number of buckets.

For typical dynamically resized hash tables, space is proportional to the number of entries, subject to capacity and implementation overhead.

Important:

O(1) is an average-case expectation, not a guarantee for every operation.

---

## 17. Hash Table vs Other Data Structures

| Feature | Array | Linked List | Hash Table |
|---|---|---|---|
| Access by index | O(1) | O(n) | Not its main purpose |
| Search by value | O(n) | O(n) | O(1) average by key |
| Insert | Depends on position | O(1) at head | O(1) average |
| Delete | Depends on position | O(1) after locating node | O(1) average by key |
| Key-value storage | Not built-in | Can be implemented | Yes |

Hash Tables are useful when we need fast access through unique keys.

---

## 18. Applications of Hash Tables

### A. Database Indexing

Hash-based indexes can support equality lookups.

Example:

```text
Employee ID -> Employee Record
```

Note: Databases also commonly use B-tree or B+ tree indexes, especially when range queries are needed.

### B. Caching

Store previously calculated results.

```text
API Request -> Cached Response
```

A cache can use a hash table to retrieve stored responses quickly.

### C. Counting Frequency

Count how many times each element appears.

```python
numbers = [1, 2, 2, 3, 3, 3]

frequency = {}

for num in numbers:

    if num in frequency:
        frequency[num] += 1

    else:
        frequency[num] = 1

print(frequency)
```

Output:

```text
{1: 1, 2: 2, 3: 3}
```

### D. Duplicate Detection

A set or dictionary can help identify repeated values efficiently.

### E. Compiler Symbol Tables

Compilers use symbol tables to associate variable names with information such as types, scopes, and memory locations.

### F. Fast Lookup Systems

Hash tables are useful for:

- User ID lookup.
- Session management.
- Configuration lookup.
- API response caching.
- Mapping identifiers to objects.

---

## 19. Hash Tables in an FDE Scenario

Imagine an AI-powered enterprise application processing employee requests.

Each request has a unique request ID.

```text
Request ID -> Request Details
```

Example:

```python
requests = {
    "REQ101": "Leave request",
    "REQ102": "Expense approval",
    "REQ103": "Access request"
}
```

When a user asks for a request's status, the application can retrieve the corresponding record by its ID.

Other FDE use cases:

- Caching API responses.
- Mapping external IDs to internal IDs.
- Storing configuration values.
- Tracking processed event IDs.
- Quickly checking whether a document has already been processed.

Hash tables are especially useful for applications that perform many key-based lookups.

---

## 20. Common Mistakes

1. **Assuming collisions never happen**
   - Different keys can produce the same hash index.

2. **Assuming hash values are unique**
   - Hash collisions are possible.

3. **Confusing hashing with encryption**
   - Hashing is not encryption and is not automatically reversible or secure.

4. **Assuming all operations are always O(1)**
   - O(1) is the average-case expectation; worst case can be O(n).

5. **Using mutable objects as dictionary keys**
   - Lists, dictionaries, and sets are unhashable.

6. **Assuming Python hash() returns the same value across runs**
   - Hash randomization can change values for strings and related objects between processes.

7. **Confusing a hash table with a normal array**
   - A hash table uses a hash function to determine where keys are stored.

---

## 21. Practice Exercises

### Beginner

1. What is a Hash Table?
2. What is a Hash Function?
3. What is a Collision?
4. What is the purpose of the modulo operator in a simple hash function?
5. What is Load Factor?

### Intermediate

6. Given:

```python
def hash_function(key):
    return key % 10
```

Find the indexes for:

```text
15, 25, 32, 42
```

7. What happens when two keys generate the same index?
8. Explain Separate Chaining.
9. What is the difference between Linear Probing and Quadratic Probing?
10. Why is Rehashing required?

### Advanced

11. Why can a hash table have O(n) worst-case search complexity?
12. Why does Python prevent lists from being used as dictionary keys?
13. What is the difference between a hash value and a hash table index?
14. How does Path Compression differ from collision handling in Union-Find and Hash Tables?
15. Why is a hash table generally unsuitable for range queries?

---

## 22. Quick Revision

| Concept | Meaning |
|---|---|
| Hash Table | Stores key-value pairs |
| Hash Function | Converts a key into a hash value |
| Hash Index | Position calculated for storage |
| Collision | Two keys map to the same index |
| Separate Chaining | Stores colliding entries in a bucket collection |
| Open Addressing | Finds another available table position |
| Linear Probing | Checks consecutive positions |
| Quadratic Probing | Checks positions using squared increments |
| Double Hashing | Uses two hash functions |
| Load Factor | Number of entries / table capacity |
| Rehashing | Resizing and redistributing entries |
| Python Dictionary | Built-in hash-based key-value structure |
| Average Lookup | O(1) |
| Worst-case Lookup | O(n) |

---

## 23. Learning Outcome

After completing this topic, you should be able to:

- Explain Hash Tables and Hash Functions.
- Calculate hash indexes.
- Understand and identify collisions.
- Implement Separate Chaining.
- Explain Linear Probing, Quadratic Probing, and Double Hashing.
- Calculate Load Factor.
- Understand Rehashing.
- Use Python dictionaries effectively.
- Explain average-case and worst-case complexity.
- Identify practical applications of hashing.

### Recommended Next Topic

**Hashing Problems – Frequency Counting, Duplicate Detection, and Two Sum**

These problems will help you apply hash tables to real programming and interview questions.
