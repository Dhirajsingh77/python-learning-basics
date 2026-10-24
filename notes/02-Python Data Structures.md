# Python Data Structures — Interview & Placement Notes

## 1. Lists

A list is an **ordered, mutable collection** that allows duplicate elements.

```python
nums = [10, 20, 30, 20]

print(nums[0])    # 10   Positive indices → left to right {0,...,l-1}
print(nums[-1])   # 20   Negative indices → right to left  { -l,...,-1}
print(nums[1:3])  # [20, 30]
```

### Important List Methods

| Method | Purpose |
|---|---|
| `append(x)` | Add one element at the end |
| `extend(iterable)` | Add multiple elements |
| `insert(i, x)` | Insert at an index |
| `remove(x)` | Remove first matching value |
| `pop(i)` | Remove and return an element |
| `sort()` | Sort the list in place |
| `reverse()` | Reverse the list in place |
| `index(x)` | Find first matching index |
| `count(x)` | Count occurrences |
| `clear()` | Remove all elements |

```python
nums = [3, 1, 2]

nums.append(4)
nums.insert(0, 10)
nums.remove(1)
last = nums.pop()
nums.sort()

print(nums)  # [2, 3, 10]
```

### Slicing

Syntax: `list[start:stop:step]`

```python
a = [10, 20, 30, 40, 50]

a[1:4]   # [20, 30, 40]
a[:3]    # [10, 20, 30]
a[::2]   # [10, 30, 50]
a[::-1]  # [50, 40, 30, 20, 10]
```

**Interview traps**
- Indexing starts at `0`.
- Negative indices count from the end.
- The stop index is excluded.
- `sort()` modifies the list and returns `None`.
- `sorted(a)` returns a new sorted list.

### List Copying

```python
a = [1, 2, 3]
b = a
b.append(4)

print(a)  # [1, 2, 3, 4]
```

`b = a` does not copy the list; both variables refer to the same object.

```python
a = [1, 2, 3]
b = a.copy()
b.append(4)

print(a)  # [1, 2, 3]
```

`copy()` makes a shallow copy. Nested mutable objects may still be shared.

---

### LIST MERGE

```python
l1=[1,2,3,4,5]
l2=[3,4,5,6,7,8]
l3=set(l1+l2)   # order get lost , set is unordered
l3 = list(dict.fromkeys(l1 + l2))  # [1, 2, 3, 4, 5, 6, 7, 8]
```

## 2. Tuples

A tuple is an **ordered, immutable collection** that allows duplicates.

```python
t = (10, 20, 30, 20)

print(t[0])
print(t.count(20))  # 2
print(t.index(30))  # 2
```

### Important Points

```python
a = (10,)  # One-element tuple
b = (10)   # Integer, not a tuple
```

Tuple unpacking:

```python
name, age = ("Dhiraj", 22)
```

**Interview question:** Why use a tuple instead of a list?

- Tuples cannot be structurally modified after creation.
- They are useful for fixed collections of values.
- A tuple containing only hashable elements can be used as a dictionary key.

---

## 3. Sets

A set is an **unordered collection of unique elements**.

```python
nums = {1, 2, 2, 3}
print(nums)  # {1, 2, 3}
```

### Important Set Methods

```python
s = {1, 2, 3}

s.add(4)
s.update([5, 6])
s.discard(10)  # No error if absent
s.remove(2)    # Raises KeyError if absent
```

### Set Operations

```python
a = {1, 2, 3}
b = {3, 4, 5}

a | b  # Union: {1, 2, 3, 4, 5}
a & b  # Intersection: {3}
a - b  # Difference: {1, 2}
a ^ b  # Symmetric difference: {1, 2, 4, 5}
```

Remove duplicates from a list:

```python
nums = [1, 2, 2, 3, 3, 4]
unique = list(set(nums))
```

**Warning:** This does not guarantee preserving the original order.

An empty set is `set()`, not `{}`. The latter creates an empty dictionary.

---

## 4. Dictionaries

A dictionary stores data as **key-value pairs**. Keys must be unique and hashable.

```python
student = {
    "name": "Dhiraj",
    "age": 22,
    "marks": 85
}

print(student["name"])
print(student.get("grade", "Not available"))
```

### Important Dictionary Methods

| Method | Purpose |
|---|---|
| `get(key, default)` | Retrieve safely with a default |
| `keys()` | Get keys |
| `values()` | Get values |
| `items()` | Get key-value pairs |
| `update()` | Add or update entries |
| `pop(key)` | Remove and return a value |
| `setdefault(key, default)` | Get value; insert default if absent |
| `clear()` | Remove all entries |

```python
student["marks"] = 90
student["city"] = "Kolkata"

for key, value in student.items():
    print(key, value)
```

### Counting Frequency

```python
words = ["apple", "banana", "apple", "orange", "banana"]
freq = {}

for word in words:
    freq[word] = freq.get(word, 0) + 1

print(freq)
# {'apple': 2, 'banana': 2, 'orange': 1}
```

Alternative using `collections.Counter`:

```python
from collections import Counter

freq = Counter(words)
```

**Interview traps**
- `student["missing"]` raises `KeyError`.
- `student.get("missing")` returns `None` by default.
- Assigning to an existing key updates its value.
- Modern Python dictionaries preserve insertion order.

---

## 5. Nested Data Structures

Collections can contain other collections.

```python
students = [
    {"name": "Aman", "marks": 80},
    {"name": "Riya", "marks": 90},
    {"name": "Raj", "marks": 75}
]

print(students[1]["name"])  # Riya
print(students[0]["marks"]) # 80
```

Find students scoring at least 80:

```python
for student in students:
    if student["marks"] >= 80:
        print(student["name"])
```

**Common use cases:** JSON data, API responses, student records, product catalogs.

---

## 6. List Comprehensions

A concise way to create a list from an iterable.

Syntax:

```python
[expression for item in iterable if condition]
```

Examples:

```python
squares = [x * x for x in range(1, 6)]
# [1, 4, 9, 16, 25]

evens = [x for x in range(10) if x % 2 == 0]
# [0, 2, 4, 6, 8]

labels = ["Even" if x % 2 == 0 else "Odd"
          for x in range(5)]
```

Equivalent normal loop:

```python
squares = []

for x in range(1, 6):
    squares.append(x * x)
```

**Interview point:** Comprehensions are concise, but ordinary loops are often clearer for complex logic.

---

## 7. Dictionary Comprehensions

Syntax:

```python
{key_expression: value_expression for item in iterable}
```

Examples:

```python
squares = {x: x * x for x in range(1, 6)}
# {1: 1, 2: 4, 3: 9, 4: 16, 5: 25}

even_squares = {
    x: x * x for x in range(10) if x % 2 == 0
}
```

Convert two lists into a dictionary:

```python
keys = ["name", "age"]
values = ["Dhiraj", 22]

student = {k: v for k, v in zip(keys, values)}
```

---

## 8. Set Comprehensions

Syntax:

```python
{expression for item in iterable if condition}
```

Example:

```python
nums = [1, 2, 2, 3, 4, 4]
unique_squares = {x * x for x in nums}

print(unique_squares)  # {1, 4, 9, 16}
```

Repeated results are stored only once.

**Important:** `{x for x in ...}` creates a set; `{x: x for x in ...}` creates a dictionary.

---

## 9. Quick Comparison

| Feature | List | Tuple | Set | Dictionary |
|---|---|---|---|---|
| Ordered | Yes | Yes | No guaranteed order | Yes |
| Mutable | Yes | No | Yes | Yes |
| Duplicates | Yes | Yes | No | Keys: no |
| Access | Index | Index | Membership | Key |
| Syntax | `[]` | `()` | `{1, 2}` | `{"a": 1}` |

*Dictionary values can be duplicated. A tuple can contain mutable objects, even though the tuple itself is immutable.*

---

## 10. Time Complexity — Common Operations

Average-case complexities for standard Python built-in collections:

| Operation | List | Set | Dictionary |
|---|---:|---:|---:|
| Access by index/key | `O(1)` for list index / N/A for key | N/A | `O(1)` average |
| Search/membership | `O(n)` | `O(1)` average | `O(1)` average for keys |
| Append/add | `O(1)` amortized | `O(1)` average | `O(1)` average for insertion |
| Insert at front | `O(n)` | N/A | N/A |

Worst-case performance can differ, especially for hash-based collections.

---

## 11. Interview Practice Questions

### Beginner
1. Find the largest and second-largest distinct elements in a list.
2. Remove duplicates from a list.
3. Reverse a list without using `reverse()`.
4. Count even and odd numbers.
5. Find common elements between two lists.

### Intermediate
6. Count the frequency of each word in a sentence.
7. Find the first non-repeating character in a string.
8. Group students by marks using a dictionary.
9. Find elements appearing in exactly one of two lists.
10. Convert a list of tuples into a dictionary.

### Comprehension Practice
11. Create a list of squares of odd numbers from 1 to 20.
12. Create a dictionary mapping numbers 1–10 to their cubes.
13. Extract unique vowels from a string using a set comprehension.
14. Flatten a two-dimensional list using a nested list comprehension.

### Mini Projects
- **Student marks system:** Store student names and marks, calculate averages, and find the topper.
- **Contact book:** Add, search, update, and delete contacts using a dictionary.
- **Word frequency counter:** Count word occurrences, identify the most frequent word, and handle case differences.

---

## 12. Last-Minute Revision Checklist

- [ ] Explain mutable vs immutable objects.
- [ ] Know list slicing and common methods.
- [ ] Explain shallow copying vs assignment.
- [ ] Know tuple unpacking and single-element tuple syntax.
- [ ] Perform union, intersection, and difference on sets.
- [ ] Use `dict.get()` to count frequencies.
- [ ] Access nested dictionaries and lists.
- [ ] Write list, dictionary, and set comprehensions from memory.
- [ ] Explain average-case time complexity of membership checks.
- [ ] Solve at least 10 practice problems without notes.
