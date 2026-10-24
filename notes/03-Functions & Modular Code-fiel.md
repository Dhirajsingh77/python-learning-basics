# Python Interview Notes — Phase 4 & Phase 5

# Phase 4: Functions & Modular Code

## 1. Defining and Calling Functions

A function is a reusable block of code that performs a specific task.

```python
def add(a, b):
    return a + b

result = add(10, 20)
print(result)  # 30
```

**Important points**
- `def` defines a function.
- Parameters are variables in the function definition.
- Arguments are values passed during a function call.
- `return` sends a result back to the caller.
- Without an explicit `return`, a function returns `None`.

## 2. Parameters, Arguments & Return Values

```python
def greet(name):           # Parameter
    return f"Hello, {name}"

print(greet("Dhiraj"))     # Argument
```

### `print()` vs `return`

```python
def first():
    print(10)

def second():
    return 10

x = first()   # Prints 10; x is None
y = second()  # y is 10
```

**Interview point:** `print()` displays output; `return` makes a value available to the caller.

## 3. Default and Keyword Arguments

### Default arguments

```python
def greet(name, message="Hello"):
    return f"{message}, {name}"

greet("Dhiraj")             # Hello, Dhiraj
greet("Dhiraj", "Welcome")  # Welcome, Dhiraj
```

Parameters with defaults must follow parameters without defaults.

### Keyword arguments

```python
def student(name, age):
    print(name, age)

student(age=22, name="Dhiraj")
```

Keyword arguments let you specify parameters by name.

**Common trap:** Avoid mutable default values such as `items=[]`.

```python
# Safer approach
def add_item(item, items=None):
    if items is None:
        items = []
    items.append(item)
    return items
```

## 4. `*args` and `**kwargs`

### `*args` — Variable positional arguments

Collects extra positional arguments into a tuple.

```python
def total(*args):
    return sum(args)

print(total(10, 20, 30))  # 60
```

### `**kwargs` — Variable keyword arguments

Collects extra keyword arguments into a dictionary.

```python
def show_details(**kwargs):
    print(kwargs)

show_details(name="Dhiraj", age=22)
# {'name': 'Dhiraj', 'age': 22}
```

**Remember**
- `*args` → tuple
- `**kwargs` → dictionary
- The names `args` and `kwargs` are conventions; the asterisks matter.

## 5. Variable Scope: Local vs Global

```python
x = 10  # Global variable

def show():
    x = 20  # Local variable
    print(x)

show()      # 20
print(x)    # 10
```

Use `global` when you need to reassign a module-level global variable inside a function.

```python
count = 0

def increment():
    global count
    count += 1
```

For nested functions, `nonlocal` allows reassignment of a variable in the nearest enclosing function scope.

**Interview point:** Python follows the LEGB lookup rule: Local → Enclosing → Global → Built-in.

## 6. Lambda Functions

A lambda creates a small anonymous function consisting of one expression.

```python
square = lambda x: x * x
print(square(5))  # 25
```

Common use with sorting:

```python
students = [("Aman", 80), ("Riya", 95), ("Raj", 70)]

students.sort(key=lambda student: student[1])
print(students)
```

Prefer `def` for functions with complex logic or multiple statements.

## 0. filter 
# Python `filter()` — Interview Notes

## 1. Definition
- `filter()` selects elements from an iterable that satisfy a condition.
- Returns a **filter object (iterator)**.

**Syntax:**
```python
filter(function, iterable)
```

## 2. Using a Function
```python
nums = [1, 2, 3, 4, 5, 6]

def even(n):
    return n % 2 == 0

result = list(filter(even, nums))
print(result)  # [2, 4, 6]
```

## 3. Using Lambda
```python
nums = [1, 2, 3, 4, 5, 6]

result = list(filter(lambda x: x > 3, nums))
print(result)  # [4, 5, 6]
```

## 4. Filter Strings
```python
words = ["hi", "python", "am", "code"]

result = list(filter(lambda w: len(w) > 2, words))
print(result)  # ['python', 'code']
```

## 5. Remove Falsy Values
```python
items = [0, 1, "", "hello", None, False]

print(list(filter(None, items)))
# [1, 'hello']
```

Falsy values include `0`, `False`, `None`, and empty strings.

## 6. `filter()` vs List Comprehension

```python
list(filter(lambda x: x > 2, nums))
[x for x in nums if x > 2]
```

Both filter elements; list comprehensions often offer better readability.

## Key Interview Points
- `filter()` takes a function and an iterable.
- The function should return `True` to keep an element.
- Use `list()` to convert the result into a list.
- The filter object is an iterator and is consumed as you iterate over it.
- `filter(None, iterable)` removes falsy elements.


# Python `map()` — Interview Notes

## 1. Definition
- `map()` applies a function to every element of an iterable.
- Returns a **map object (iterator)**.

**Syntax:**
```python
map(function, iterable)
```

## 2. Using a Function
```python
nums = [1, 2, 3, 4]

def square(n):
    return n ** 2

result = list(map(square, nums))
print(result)  # [1, 4, 9, 16]
```

## 3. Using Lambda
```python
nums = [1, 2, 3, 4]

result = list(map(lambda x: x * 2, nums))
print(result)  # [2, 4, 6, 8]
```

## 4. Convert Strings to Integers
```python
nums = ["10", "20", "30"]

result = list(map(int, nums))
print(result)  # [10, 20, 30]
```

## 5. Map Multiple Iterables
`map()` passes corresponding elements from each iterable to the function. It stops when the shortest iterable is exhausted.

```python
a = [1, 2, 3]
b = [10, 20, 30]

result = list(map(lambda x, y: x + y, a, b))
print(result)  # [11, 22, 33]
```

## 6. `map()` vs `filter()`

| `map()` | `filter()` |
|---|---|
| Transforms elements | Selects elements |
| Applies a function to each element | Keeps elements where the function returns truthy |
| Usually preserves the number of elements for one iterable | May return fewer elements |

## Key Interview Points
- `map()` returns an iterator, not a list.
- Use `list()` to materialize the results.
- It supports multiple iterables.
- The function's output becomes the corresponding output element.
- List comprehension alternative: `[x * 2 for x in nums]`.



## 7. Modules and Imports

A module is a Python file containing reusable code.

```python
import math

print(math.sqrt(25))
print(math.pi)
```

Other import styles:

```python
import math as m
from math import sqrt

print(m.pi)
print(sqrt(16))
```

Avoid `from module import *` in production code because it can cause naming conflicts.

## 8. Creating Your Own Module

**math_utils.py**

```python
def add(a, b):
    return a + b

def square(n):
    return n * n
```

**main.py**

```python
import math_utils

print(math_utils.add(5, 3))
print(math_utils.square(4))
```

Keep both files in the same directory for this simple example.

### `if __name__ == "__main__"`

```python
def main():
    print("Program started")

if __name__ == "__main__":
    main()
```

This block runs when the file is executed directly, not when it is imported as a normal module.

**Why use it?** To prevent test code or program execution from running unintentionally when another file imports the module.

---

# Phase 5: Intermediate Python

## 1. File Handling

Use `with open()` to manage files safely. It closes the file automatically.

### Read a file

```python
with open("notes.txt", "r", encoding="utf-8") as file:
    content = file.read()
    print(content)
```

### Write to a file

```python
with open("notes.txt", "w", encoding="utf-8") as file:
    file.write("Python revision notes")
```

### Append to a file

```python
with open("notes.txt", "a", encoding="utf-8") as file:
    file.write("\nFunctions and modules")
```

| Mode | Purpose |
|---|---|
| `r` | Read; file must exist |
| `w` | Write; overwrites existing content or creates file |
| `a` | Append; creates file if needed |
| `x` | Create a new file; fails if it exists |
| `b` | Binary mode, e.g. `rb` |
| `+` | Read and write, e.g. `r+` |

### Read line by line

```python
with open("notes.txt", "r", encoding="utf-8") as file:
    for line in file:
        print(line.strip())
```

**Interview point:** `read()` reads all content into memory, while iterating over the file is usually more memory-efficient for large text files.

## 2. CSV File Handling

CSV stores tabular data as rows and columns.

```python
import csv

with open("students.csv", "w", newline="", encoding="utf-8") as file:
    writer = csv.writer(file)
    writer.writerow(["Name", "Marks"])
    writer.writerow(["Dhiraj", 90])
```

Read CSV:

```python
import csv

with open("students.csv", "r", newline="", encoding="utf-8") as file:
    reader = csv.reader(file)

    for row in reader:
        print(row)
```

For CSV files with headers, use `csv.DictReader` and `csv.DictWriter` when dictionary-style access is useful.

## 3. Exception Handling

Exceptions are runtime errors that interrupt normal program execution unless handled.

```python
try:
    n = int(input("Enter a number: "))
    print(100 / n)

except ValueError:
    print("Enter a valid integer")

except ZeroDivisionError:
    print("Cannot divide by zero")

finally:
    print("Execution completed")
```

### Keywords

- `try`: Code that might raise an exception.
- `except`: Handles a matching exception.
- `else`: Runs if the `try` block finishes without an exception.
- `finally`: Runs during normal or exceptional exit from the construct.
- `raise`: Explicitly raises an exception.

### Raising an exception

```python
def withdraw(balance, amount):
    if amount <= 0:
        raise ValueError("Amount must be positive")

    if amount > balance:
        raise ValueError("Insufficient balance")

    return balance - amount
```

**Interview traps**
- Catch specific exceptions rather than using a bare `except`.
- `finally` is useful for cleanup.
- Don't use exceptions to silently hide unexpected bugs.

## 4. String Methods and Formatting

Strings are **immutable**: methods that transform strings return new strings.

```python
text = "  Hello Python  "

text.strip()                  # "Hello Python"
text.lower()                  # "  hello python  "
text.upper()                  # "  HELLO PYTHON  "
text.replace("Python", "JS")  # "  Hello JS  "
text.split()                  # ["Hello", "Python"]
```

### Joining strings

```python
words = ["Learn", "Python"]
sentence = " ".join(words)

print(sentence)  # Learn Python
```

### Checking strings

```python
"123".isdigit()       # True
"hello".isalpha()     # True
"hello123".isalnum()  # True
"python".startswith("py")  # True
```

### F-strings

```python
name = "Dhiraj"
marks = 89.456

print(f"{name} scored {marks:.2f}")
# Dhiraj scored 89.46
```

Use f-strings for readable string interpolation and formatting.

## 5. Dates and Time

Use `datetime` for dates, times, and formatting.

```python
from datetime import datetime, date, timedelta

today = date.today()
now = datetime.now()

print(today)
print(now)
```

### Formatting a date

```python
now = datetime.now()

print(now.strftime("%d-%m-%Y"))
```

### Convert a string into a date/time

```python
dt = datetime.strptime("11-10-2026", "%d-%m-%Y")
print(dt)
```

### Add days

```python
tomorrow = date.today() + timedelta(days=1)
```

Common format codes:

| Code | Meaning |
|---|---|
| `%d` | Day |
| `%m` | Month |
| `%Y` | Four-digit year |
| `%H` | Hour, 24-hour clock |
| `%M` | Minute |
| `%S` | Second |

**Interview point:** `strftime()` formats a date/time as a string; `strptime()` parses a string into a date/time object.

For production systems involving different time zones, prefer timezone-aware datetimes.

## 6. Regular Expressions (Regex)

Regex searches for patterns in strings using Python's `re` module.

```python
import re

text = "My number is 9876543210"

match = re.search(r"\d{10}", text)

if match:
    print(match.group())
```

### Common patterns

| Pattern | Meaning |
|---|---|
| `\d` | Digit |
| `\w` | Word character |
| `\s` | Whitespace |
| `.` | Any character except newline by default |
| `+` | One or more |
| `*` | Zero or more |
| `?` | Zero or one |
| `^` | Start of string/line |
| `$` | End of string/line |
| `{n}` | Exactly n repetitions |

### Common functions

```python
re.search(r"cat", text)       # First match anywhere
re.match(r"cat", text)        # Match at the start
re.findall(r"\d+", text)      # All non-overlapping matches
re.sub(r"\d+", "X", text)     # Replace matches
```

Use raw strings such as `r"\d+"` to avoid most backslash-escaping issues.

**Important:** A regex match is not automatically full validation. Use `re.fullmatch()` when the entire input must follow a pattern.

## 7. Virtual Environments (`venv`)

A virtual environment isolates a project's installed Python packages from other projects.

### Create one

```bash
python3 -m venv .venv
```

### Activate on Linux/macOS

```bash
source .venv/bin/activate
```

### Activate on Windows CMD

```bat
.venv\Scripts\activate.bat
```

### Deactivate

```bash
deactivate
```

**Why use it?** Different projects may require different package versions.

Usually, add `.venv/` to `.gitignore` instead of committing the environment directory.

## 8. Package Management with pip

`pip` installs and manages Python packages.

```bash
python -m pip install requests
python -m pip show requests
python -m pip list
python -m pip uninstall requests
```

### Save dependencies

```bash
python -m pip freeze > requirements.txt
```

### Install dependencies

```bash
python -m pip install -r requirements.txt
```

Run these commands with the intended virtual environment activated.

**Best practice:** Use `python -m pip` so pip runs under the Python interpreter you intend to use.

---

# Interview Quick Questions

1. What is the difference between parameters and arguments?
2. What is the difference between `print()` and `return`?
3. What are `*args` and `**kwargs`?
4. Explain Python's LEGB scope rule.
5. What does `if __name__ == "__main__"` do?
6. What happens when you open a file in `w` mode?
7. What is the difference between `read()`, `readline()`, and `readlines()`?
8. Explain `try`, `except`, `else`, and `finally`.
9. Why are Python strings immutable?
10. What is the difference between `strftime()` and `strptime()`?
11. What is the difference between `re.match()` and `re.search()`?
12. Why do we use virtual environments?
13. What is `requirements.txt` used for?
14. Why should you avoid mutable default arguments?
15. What is the difference between a module and a package?

# Practice Tasks

## Functions
- Build a calculator using separate functions.
- Write a function accepting any number of numeric arguments and returning their sum.
- Create a module containing reusable string utilities.

## Files and Exceptions
- Count lines, words, and characters in a text file.
- Read student marks from a CSV and calculate the average.
- Handle invalid input and division by zero.

## Intermediate Python
- Validate a date string using `datetime`.
- Extract all numbers from a text file using regex.
- Create a virtual environment and install a package.
- Export installed dependencies to `requirements.txt`.
