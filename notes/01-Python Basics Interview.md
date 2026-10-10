# Python Basics — Interview & Placement Revision

## Phase 1: Absolute Basics

### 1. Variables and Data Types

A variable stores a reference to a value.

```python
name = "Dhiraj"     # str
age = 22            # int
height = 5.7        # float
is_student = True   # bool
result = None       # NoneType
```

**Important points**
- Python is dynamically typed; no explicit type declaration is required.
- Variable names are case-sensitive.
- Use `type()` to check a value's type.
- Python uses indentation to define code blocks.

```python
print(type(age))  # <class 'int'>
```

### 2. Input and Output

```python
name = input("Enter name: ")
age = int(input("Enter age: "))

print("Name:", name)
print(f"I am {name}, age {age}")
```

**Interview points**
- `input()` always returns a string.
- Use `int()` or `float()` when numeric input is needed.
- An f-string inserts expressions inside `{}`.

### 3. Type Conversion

```python
int("10")       # 10
float("3.14")   # 3.14
str(100)        # "100"
bool(1)         # True
```

**Important:** `int("3.5")` raises `ValueError`; use `int(float("3.5"))` if truncation is intended.

Falsy values include `0`, `0.0`, `""`, `[]`, `{}`, `None`, and `False`.

```python
bool("")    # False
bool("0")   # True
```

### 4. Operators

| Type | Operators | Example |
|---|---|---|
| Arithmetic | `+ - * / // % **` | `7 // 2` → `3` |
| Comparison | `== != > < >= <=` | `5 != 3` → `True` |
| Logical | `and or not` | `True and False` |
| Assignment | `= += -= *=` | `x += 1` |
| Membership | `in`, `not in` | `"a" in "cat"` |
| Identity | `is`, `is not` | `x is None` |

**Frequently asked differences**
- `/` performs division and returns a float.
- `//` performs floor division.
- `%` returns the remainder.
- `**` performs exponentiation.
- `==` compares values; `is` checks object identity.

```python
print(7 / 2)    # 3.5
print(7 // 2)   # 3
print(7 % 2)    # 1
print(2 ** 3)   # 8
```

### 5. Comments and Syntax

```python
# Single-line comment

"""
A string literal spanning multiple lines.
It is not technically a comment.
"""

if True:
    print("Indentation matters")
```

- Use four spaces for indentation.
- Python is case-sensitive.
- `True`, `False`, and `None` are capitalized.
- Avoid using Python keywords as variable names.

---

## Phase 2: Control Flow

### 6. if, elif, else

```python
marks = 75

if marks >= 90:
    print("A")
elif marks >= 60:
    print("B")
else:
    print("C")
```

- `if` checks the first condition.
- `elif` checks another condition if previous conditions fail.
- `else` handles all remaining cases.
- Only the first matching branch executes.

### 7. Nested Conditions

```python
age = 22
has_id = True

if age >= 18:
    if has_id:
        print("Allowed")
    else:
        print("ID required")
else:
    print("Not allowed")
```

Use `and` or `or` when appropriate to simplify nested conditions.

### 8. for Loop

A `for` loop iterates over an iterable such as a string, list, or range.

```python
for i in range(1, 6):
    print(i)
```

`range(start, stop, step)` excludes `stop`.

```python
range(5)        # 0, 1, 2, 3, 4
range(1, 6)     # 1, 2, 3, 4, 5
range(2, 10, 2) # 2, 4, 6, 8
```

### 9. while Loop

Repeats while a condition is `True`.

```python
n = 1

while n <= 5:
    print(n)
    n += 1
```

**Interview warning:** Update the loop variable properly to avoid an infinite loop.

### 10. break, continue, pass

```python
for i in range(5):
    if i == 2:
        continue
    if i == 4:
        break
    print(i)
```

- `break`: terminates the nearest loop.
- `continue`: skips the current iteration.
- `pass`: does nothing; acts as a placeholder.

### 11. Nested Loops

A loop inside another loop.

```python
for i in range(1, 4):
    for j in range(1, 4):
        print(i, j)
```

**Time complexity:** If both loops run `n` times, the total work is typically \(O(n^2)\).

### 12. Basic Pattern Printing

```python
# Right-angled triangle
for i in range(1, 5):
    print("*" * i)
```

Output:

```text
*
**
***
****
```

Number pattern:

```python
for i in range(1, 5):
    for j in range(1, i + 1):
        print(j, end=" ")
    print()
```

Output:

```text
1
1 2
1 2 3
1 2 3 4
```

---

## 13. Common Interview Programs

### Check Even or Odd

```python
n = int(input())

if n % 2 == 0:
    print("Even")
else:
    print("Odd")
```

### Find the Largest of Three Numbers

```python
a, b, c = 10, 25, 15
print(max(a, b, c))
```

Be ready to solve this again using `if-elif-else`.

### Swap Two Variables

```python
a, b = 10, 20
a, b = b, a
```

Python supports multiple assignment; a temporary variable is not required.

### Sum of First N Natural Numbers

```python
n = int(input())
total = 0

for i in range(1, n + 1):
    total += i

print(total)
```

Time complexity: \(O(n)\).

### Factorial

```python
n = int(input())
fact = 1

for i in range(1, n + 1):
    fact *= i

print(fact)
```

For non-negative integers, `0! = 1`.

### Reverse a Number

```python
n = int(input())
reverse = 0

while n > 0:
    digit = n % 10
    reverse = reverse * 10 + digit
    n //= 10

print(reverse)
```

This version assumes a non-negative integer.

### FizzBuzz

Print `Fizz` for multiples of 3, `Buzz` for multiples of 5, and `FizzBuzz` for both.

```python
for i in range(1, 101):
    if i % 15 == 0:
        print("FizzBuzz")
    elif i % 3 == 0:
        print("Fizz")
    elif i % 5 == 0:
        print("Buzz")
    else:
        print(i)
```

**Interview trap:** Check the combined condition before checking individual conditions.

---

## 14. Complexity Basics

| Code pattern | Typical time complexity |
|---|---|
| Single operation | \(O(1)\) |
| One loop over `n` items | \(O(n)\) |
| Two nested loops of size `n` | \(O(n^2)\) |
| Repeatedly halve the problem | \(O(\log n)\) |

Always explain how the number of operations grows with input size.

---

## 15. Quick Interview Questions

1. What is the difference between `/` and `//`?
2. What does `input()` return?
3. What is the difference between `==` and `is`?
4. What is the difference between `break`, `continue`, and `pass`?
5. Why does `range(1, 5)` exclude `5`?
6. What is the difference between `for` and `while`?
7. What is dynamic typing?
8. What are truthy and falsy values?
9. What causes an infinite loop?
10. What is the time complexity of two nested loops?


