# SQL Data Types

## 1. Why Choosing the Correct Data Type Matters

Every column in a relational table must be assigned an explicit **Data Type**. Choosing the correct data type is critical for:
1. **Data Accuracy**: Enforces domain integrity at the hardware level.
2. **Storage Efficiency**: Smaller types require fewer bytes per row, allowing more rows to fit into cache memory (RAM).
3. **Query Performance**: Indexing and sorting on integer keys is significantly faster than on variable-length text strings.
4. **Calculations**: Prevents roundoff floating-point bugs in financial ledgers.

---

## 2. Core SQL Data Type Categories

```text
+--------------------------------------------------------------------------+
|                             SQL DATA TYPES                               |
+--------------------------------------------------------------------------+
       |                  |                |             |            |
       v                  v                v             v            v
+--------------+   +--------------+  +-----------+  +---------+  +---------+
|   NUMERIC    |   |  CHARACTER/  |  | DATE/TIME |  | BOOLEAN |  | SEMI-   |
|              |   |    STRING    |  |           |  |         |  |STRUCT'D |
+--------------+   +--------------+  +-----------+  +---------+  +---------+
| INT, BIGINT  |   | CHAR(n)      |  | DATE      |  | BOOLEAN |  | JSON    |
| SMALLINT     |   | VARCHAR(n)   |  | TIME      |  | (TRUE/  |  | JSONB   |
| DECIMAL(p,s) |   | TEXT         |  | TIMESTAMP |  |  FALSE) |  | XML     |
| FLOAT, DOUBLE|   +--------------+  | INTERVAL  |  +---------+  +---------+
+--------------+                     +-----------+
```

---

## 3. Numeric Types

### A. Integers (Exact Whole Numbers)
- **`SMALLINT`**: 2 bytes (-32,768 to 32,767). Best for small counts, status codes.
- **`INT` / `INTEGER`**: 4 bytes (-2.14 billion to 2.14 billion). Standard choice for IDs.
- **`BIGINT`**: 8 bytes (-9 quintillion to 9 quintillion). Essential for high-volume logs, analytics IDs.

### B. Fixed-Point Exact Decimals
- **`DECIMAL(p, s)` / `NUMERIC(p, s)`**:
  - `p` (Precision): Total number of digits (before and after the decimal point).
  - `s` (Scale): Number of digits to the right of the decimal point.
  - *Example*: `DECIMAL(10, 2)` can store up to `99,999,999.99`.
  - **Rule of Thumb**: ALWAYS use `DECIMAL` for currency, pricing, taxes, and accounting.

### C. Floating-Point Numbers (Approximate)
- **`REAL` / `FLOAT`**: 4 bytes (6 decimal digits precision).
- **`DOUBLE PRECISION`**: 8 bytes (15 decimal digits precision).
- Best for scientific measurements, physics simulations, GPS coordinates where slight precision variations are acceptable.

---

## 4. Character & String Types

### A. `CHAR(n)` (Fixed Length)
Allocates exactly `n` characters of storage. If the inserted string is shorter, it is right-padded with whitespace.
- *Best for*: Predictable fixed-size strings like ISO country codes (`US`, `IN`), state codes (`NY`, `CA`), MD5 hashes.

### B. `VARCHAR(n)` (Variable Length)
Stores only the characters provided plus 1 or 2 bytes of length overhead (up to `n`).
- *Best for*: Names, emails, street addresses, titles.

### C. `TEXT` (Unlimited / Large Variable Length)
Stores very large text strings without arbitrary maximum limits (up to 1GB in PostgreSQL).
- *Best for*: Blog posts, user bios, markdown documents, comments.

---

## 5. Date and Time Types

| Data Type | What It Stores | Example | Typical Use Case |
| :--- | :--- | :--- | :--- |
| **`DATE`** | Year, Month, Day | `2026-11-27` | Birthdates, due dates |
| **`TIME`** | Hour, Minute, Second | `14:30:00` | Store opening hours |
| **`TIMESTAMP`** | Date and Time (no timezone) | `2026-11-27 14:30:00` | Local system events |
| **`TIMESTAMPTZ`** | Date, Time with UTC Timezone | `2026-11-27 09:00:00+00` | Global audits, orders |

---

## 6. Decision Guide: "Which Data Type Should I Pick?"

```text
Do you need to store numbers?
 ├── Whole numbers only?
 │    ├── < 32,000  ---------> SMALLINT
 │    ├── < 2 Billion -------> INT
 │    └── Huge scale / Log --> BIGINT
 └── Decimals / Fractions?
      ├── Money / Finance ---> DECIMAL(12, 2)
      └── Scientific data ---> DOUBLE PRECISION

Do you need to store text?
 ├── Fixed length (e.g., country code 'US') --> CHAR(2)
 ├── Normal strings with limit --------------> VARCHAR(100)
 └── Free-form long paragraphs --------------> TEXT
```
