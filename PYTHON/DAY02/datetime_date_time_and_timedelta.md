# Python datetime, date, time, and timedelta

---

## 1. Introduction to the datetime Module

Python's built-in `datetime` module provides classes for manipulating dates, times, and time intervals.

Main classes:
- `date`: Represents idealized calendar date (year, month, day).
- `time`: Represents time of day independent of date (hour, minute, second, microsecond).
- `datetime`: Combines date and time into a single object.
- `timedelta`: Represents a duration or difference between two dates/times.

---

## 2. Working with `date`, `time`, and `datetime`

```python
from datetime import date, time, datetime

# Current date and current date-time
today = date.today()
now = datetime.now()

print("Today's Date:   ", today)
print("Current DateTime:", now)

# Individual attributes
print(f"Year: {today.year}, Month: {today.month}, Day: {today.day}")
print(f"Hour: {now.hour}, Minute: {now.minute}, Second: {now.second}")

# Creating specific instances
specific_date = date(2026, 12, 25)
specific_time = time(14, 30, 45)
combined = datetime(2026, 12, 25, 14, 30, 45)

print("Specific Event:", combined)
```

**Output:**

```text
Today's Date:    2026-11-17
Current DateTime: 2026-11-17 15:35:00.123456
Year: 2026, Month: 11, Day: 17
Hour: 15, Minute: 35, Second: 0
Specific Event: 2026-12-25 14:30:45
```

---

## 3. Date Arithmetic with `timedelta`

`timedelta` represents a duration: days, seconds, microseconds, milliseconds, minutes, hours, or weeks.

```python
from datetime import datetime, timedelta

start_time = datetime(2026, 11, 1, 9, 0, 0)

# Add 14 days and 3 hours
deadline = start_time + timedelta(days=14, hours=3)
print("Project Deadline:", deadline)

# Subtract 30 minutes
reminder = deadline - timedelta(minutes=30)
print("Meeting Reminder:", reminder)

# Difference between two datetime objects produces a timedelta
duration = deadline - start_time
print("Duration in Days:   ", duration.days)
print("Total Duration (sec):", duration.total_seconds())
```

**Output:**

```text
Project Deadline: 2026-11-15 12:00:00
Meeting Reminder: 2026-11-15 11:30:00
Duration in Days:    14
Total Duration (sec): 1220400.0
```

---

## 4. Comparing Dates and Times

Standard comparison operators (`<`, `<=`, `>`, `>=`, `==`) work directly on date and datetime objects:

```python
from datetime import date

d1 = date(2026, 5, 10)
d2 = date(2026, 8, 20)

print("Is d1 earlier than d2?", d1 < d2)
```

**Output:**

```text
Is d1 earlier than d2? True
```
