# Python Standard Libraries & Tools — Interview Revision Notes

## 1. `os` — Operating System Operations

Used for interacting with the operating system, directories, environment variables, and paths.

```python
import os

print(os.getcwd())            # Current working directory
print(os.listdir("."))        # Files and folders in current directory
print(os.path.exists("data.txt"))
print(os.path.isfile("data.txt"))
print(os.path.isdir("my_folder"))
```

### Create and remove directories

```python
os.makedirs("data/reports", exist_ok=True)
```

- `exist_ok=True` prevents an error if the directory already exists.
- `os.mkdir()` creates one directory level.
- `os.makedirs()` can create nested directories.

**Interview point:** `os` provides operating-system functionality; use `pathlib` for convenient path manipulation.

## 2. `sys` — Python Runtime Information

Used to access interpreter information, command-line arguments, and runtime settings.

```python
import sys

print(sys.version)
print(sys.platform)
print(sys.argv)
```

Example: `python app.py Dhiraj 22`

```python
# app.py
import sys

print(sys.argv)
# ['app.py', 'Dhiraj', '22']
```

- `sys.argv[0]` is typically the script name.
- Remaining elements are command-line arguments.
- `sys.exit()` exits the program.

**Interview point:** `sys.argv` contains strings; convert arguments to integers when numeric input is required.

## 3. `pathlib` — File and Directory Paths

An object-oriented way to work with filesystem paths.

```python
from pathlib import Path

path = Path("data.txt")

print(path.exists())
print(path.is_file())
print(path.name)
print(path.suffix)
print(path.parent)
```

### Create folders and work with files

```python
folder = Path("data/reports")
folder.mkdir(parents=True, exist_ok=True)

file = folder / "notes.txt"
file.write_text("Python revision", encoding="utf-8")

content = file.read_text(encoding="utf-8")
print(content)
```

**Important:** The `/` operator joins path components. It does not perform arithmetic here.

**Interview point:** Prefer `pathlib` for readable, cross-platform path handling.

## 4. `json` — JSON Data

JSON is a common format for exchanging structured data between applications and APIs.

### Python object to JSON string

```python
import json

student = {"name": "Dhiraj", "marks": 90}

json_string = json.dumps(student)
print(json_string)
```

### JSON string to Python object

```python
data = json.loads(json_string)
print(data["name"])
```

### Read and write JSON files

```python
with open("student.json", "w", encoding="utf-8") as file:
    json.dump(student, file, indent=4)

with open("student.json", "r", encoding="utf-8") as file:
    data = json.load(file)
```

**Remember:**

| Function | Purpose |
|---|---|
| `json.dumps()` | Python object → JSON string |
| `json.loads()` | JSON string → Python object |
| `json.dump()` | Write JSON to a file |
| `json.load()` | Read JSON from a file |

**Interview trap:** JSON objects commonly map to Python dictionaries, and JSON arrays map to Python lists. JSON `true`, `false`, and `null` map to Python `True`, `False`, and `None`.

## 5. `datetime` — Date and Time

Used for current dates, date formatting, parsing, and arithmetic.

```python
from datetime import datetime, date, timedelta

print(date.today())
print(datetime.now())

tomorrow = date.today() + timedelta(days=1)
print(tomorrow)
```

### Format and parse dates

```python
now = datetime.now()
print(now.strftime("%d-%m-%Y"))

dt = datetime.strptime("11-10-2026", "%d-%m-%Y")
print(dt)
```

- `strftime()` formats a date/time as a string.
- `strptime()` parses a string into a date/time object.
- `timedelta` represents a duration.

## 6. `collections` — Specialized Data Structures

### A. `Counter`

Counts occurrences of elements.

```python
from collections import Counter

words = ["python", "java", "python", "c++", "java", "python"]

freq = Counter(words)

print(freq["python"])       # 3
print(freq.most_common(2))  # [('python', 3), ('java', 2)]
```

Useful for frequency-counting interview problems.

### B. `defaultdict`

Provides a default value for missing keys.

```python
from collections import defaultdict

groups = defaultdict(list)

groups["CSE"].append("Dhiraj")
groups["CSE"].append("Aman")
groups["ECE"].append("Riya")

print(dict(groups))
```

Another example: counting items.

```python
counts = defaultdict(int)

for item in ["a", "b", "a"]:
    counts[item] += 1

print(dict(counts))  # {'a': 2, 'b': 1}
```

- `defaultdict(list)` creates an empty list for a missing key.
- `defaultdict(int)` creates `0` for a missing key.

### C. `namedtuple`

Creates tuple-like objects with named fields.

```python
from collections import namedtuple

Student = namedtuple("Student", ["name", "marks"])

s = Student("Dhiraj", 90)

print(s.name)
print(s.marks)
```

Named tuples are immutable. For many new projects requiring typed records or default values, consider `dataclasses` as well.

## 7. `random` — Random Values

```python
import random

print(random.randint(1, 10))        # Includes 1 and 10
print(random.choice(["A", "B", "C"]))
print(random.random())              # Float in [0.0, 1.0)
```

### Shuffle a list

```python
nums = [1, 2, 3, 4, 5]
random.shuffle(nums)

print(nums)
```

`shuffle()` modifies the list in place and returns `None`.

**Interview point:** Use `random` for games and simulations, not security-sensitive tokens. For security-sensitive randomness, use the `secrets` module.

## 8. `math` — Mathematical Operations

```python
import math

print(math.sqrt(25))      # 5.0
print(math.ceil(4.2))     # 5
print(math.floor(4.8))    # 4
print(math.factorial(5))  # 120
print(math.gcd(12, 18))   # 6
print(math.pi)
```

**Common distinctions:**

- `ceil(x)` rounds toward positive infinity.
- `floor(x)` rounds toward negative infinity.
- `sqrt(x)` calculates the square root.
- `factorial(n)` calculates \(n!\) for non-negative integers.

## 9. `csv` — Tabular Data

CSV files store data in rows and columns.

### Write CSV

```python
import csv

with open("students.csv", "w", newline="", encoding="utf-8") as file:
    writer = csv.writer(file)
    writer.writerow(["Name", "Marks"])
    writer.writerow(["Dhiraj", 90])
    writer.writerow(["Aman", 85])
```

### Read CSV

```python
with open("students.csv", "r", newline="", encoding="utf-8") as file:
    reader = csv.DictReader(file)

    for row in reader:
        print(row["Name"], row["Marks"])
```

**Interview point:** Values read from CSV are generally strings. Convert them to `int` or `float` when numerical operations are required.

## 10. `requests` — Working with APIs

`requests` is an external package, not part of Python's standard library. Install it with:

```bash
python -m pip install requests
```

### Send a GET request

```python
import requests

url = "https://jsonplaceholder.typicode.com/todos/1"

try:
    response = requests.get(url, timeout=10)
    response.raise_for_status()

    data = response.json()
    print(data["title"])

except requests.RequestException as error:
    print("Request failed:", error)
```

### Important methods and attributes

| Method / Attribute | Purpose |
|---|---|
| `requests.get(url)` | Retrieve a resource |
| `requests.post(url, json=data)` | Send JSON data |
| `response.status_code` | HTTP status code |
| `response.json()` | Parse JSON response |
| `response.text` | Response body as text |
| `response.raise_for_status()` | Raise an error for HTTP 4xx/5xx |
| `timeout=10` | Set a timeout in seconds |

**Interview points**
- `200` commonly means success.
- `404` means the resource was not found.
- `500` indicates a server-side error.
- Handle connection failures and timeouts.
- Never hardcode API secrets into source code.

---

## 11. Quick Library Selection Guide

| Requirement | Use |
|---|---|
| List files or inspect environment | `os` |
| Handle file paths cleanly | `pathlib` |
| Access command-line arguments | `sys` |
| Store or exchange JSON | `json` |
| Parse or calculate dates | `datetime` |
| Count frequencies | `Counter` |
| Group data by keys | `defaultdict` |
| Represent tuple records with named fields | `namedtuple` |
| Generate random game values | `random` |
| Mathematical functions | `math` |
| Read or write CSV | `csv` |
| Call a web API | `requests` |

## 12. Placement Practice Tasks

### Beginner
1. List all `.py` files in a directory using `pathlib`.
2. Save a student dictionary to JSON and read it back.
3. Count word frequency using `Counter`.
4. Generate a random number guessing game.
5. Calculate the number of days between two dates.

### Intermediate
6. Read a CSV of student marks and find the topper.
7. Group students by department using `defaultdict(list)`.
8. Accept a filename from `sys.argv` and check whether it exists.
9. Call a public API using `requests` and handle errors.
10. Convert API JSON data into a clean list of dictionaries.

## 13. Interview Self-Test

- [ ] Difference between `os` and `pathlib`.
- [ ] Difference between `json.dump()` and `json.dumps()`.
- [ ] Difference between `Counter` and `defaultdict`.
- [ ] Difference between `random.randint()` and `random.random()`.
- [ ] Difference between `strftime()` and `strptime()`.
- [ ] How to read CSV rows as dictionaries.
- [ ] Why API requests need timeouts and error handling.
- [ ] Difference between standard libraries and third-party packages.
