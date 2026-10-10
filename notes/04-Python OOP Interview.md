# Python OOP — Interview & Placement Revision Notes

## 1. Classes and Objects

**Class:** A blueprint that defines attributes and behavior.

**Object:** An instance of a class.

```python
class Student:
    def study(self):
        print("Student is studying")

s1 = Student()
s1.study()
```

- `Student` is the class.
- `s1` is an object.
- `study()` is an instance method.

## 2. The `__init__()` Method

`__init__()` initializes an object's attributes when an instance is created.

```python
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age

s1 = Student("Dhiraj", 22)

print(s1.name)  # Dhiraj
print(s1.age)   # 22
```

**Important interview points**
- `self` refers to the current instance.
- `self` is a convention, not a reserved keyword.
- `__init__()` is an initializer, not the method that creates the object.
- Python calls `__new__()` to create an instance before calling `__init__()`.

## 3. Instance Variables vs Class Variables

### Instance variables

Belong to individual objects.

### Class variables

Shared through the class unless shadowed by an instance attribute.

```python
class Student:
    college = "IIIT Kalyani"  # Class variable

    def __init__(self, name):
        self.name = name       # Instance variable

s1 = Student("Dhiraj")
s2 = Student("Aman")

print(s1.name)       # Dhiraj
print(s2.name)       # Aman
print(s1.college)    # IIIT Kalyani
```

Changing an instance attribute does not change the class variable:

```python
s1.college = "Other College"

print(s1.college)       # Other College
print(s2.college)       # IIIT Kalyani
print(Student.college)  # IIIT Kalyani
```

**Common trap:** Avoid mutable class variables for data that should belong to each object.

```python
class Example:
    items = []  # Shared list across instances
```

If each object needs its own list, initialize `self.items = []` inside `__init__()`.

## 4. Instance, Class and Static Methods

### Instance method

Works with an individual instance through `self`.

### Class method

Receives the class through `cls`. Use `@classmethod`.

### Static method

Does not automatically receive `self` or `cls`. Use `@staticmethod`.

```python
class Student:
    college = "IIIT Kalyani"

    def __init__(self, name):
        self.name = name

    def introduce(self):
        return f"I am {self.name}"

    @classmethod
    def change_college(cls, name):
        cls.college = name

    @staticmethod
    def is_adult(age):
        return age >= 18
```

```python
s1 = Student("Dhiraj")

print(s1.introduce())
print(Student.is_adult(22))
Student.change_college("New College")
```

**Interview question:** When should you use a class method instead of a static method?

- Use a class method when you need the class (`cls`) or want a class-aware alternative constructor.
- Use a static method for a related utility that needs neither the instance nor the class.

## 5. Inheritance

Inheritance allows a child class to reuse and extend a parent class.

```python
class Animal:
    def speak(self):
        print("Animal makes a sound")

class Dog(Animal):
    def bark(self):
        print("Dog barks")

d = Dog()
d.speak()  # Inherited method
d.bark()
```

### Types of inheritance

- Single: One child inherits from one parent.
- Multilevel: A class inherits from a child class in a chain.
- Multiple: One class inherits from multiple parent classes.
- Hierarchical: Multiple child classes inherit from one parent.
- Hybrid: A combination of inheritance types.

### Using `super()`

Calls the next implementation in the method resolution order (MRO).

```python
class Animal:
    def __init__(self, name):
        self.name = name

class Dog(Animal):
    def __init__(self, name, breed):
        super().__init__(name)
        self.breed = breed

d = Dog("Bruno", "Labrador")
print(d.name, d.breed)
```

**Important:** `super()` is not simply another name for the parent class. It follows the MRO, which matters in multiple inheritance.

## 6. Encapsulation

Encapsulation groups data and behavior together and controls how an object's state is accessed or changed.

Python naming conventions:

- `name`: Public attribute.
- `_name`: Non-public by convention.
- `__name`: Name-mangled attribute; not truly private.

Example:

```python
class BankAccount:
    def __init__(self, balance):
        self.__balance = balance

    def deposit(self, amount):
        if amount <= 0:
            raise ValueError("Amount must be positive")
        self.__balance += amount

    def get_balance(self):
        return self.__balance

account = BankAccount(1000)
account.deposit(500)

print(account.get_balance())  # 1500
```

**Interview point:** Python does not enforce strict private access like some languages. Double underscores trigger name mangling to reduce accidental name conflicts.

## 7. Polymorphism

Polymorphism means the same interface can produce different behavior for different objects.

### Method overriding

A child class provides its own implementation of an inherited method.

```python
class Animal:
    def speak(self):
        print("Some sound")

class Dog(Animal):
    def speak(self):
        print("Bark")

class Cat(Animal):
    def speak(self):
        print("Meow")

for animal in [Dog(), Cat()]:
    animal.speak()
```

Output:

```text
Bark
Meow
```

### Duck typing

Python focuses on whether an object supports the required behavior, rather than requiring a particular class.

```python
class PDF:
    def open(self):
        print("Opening PDF")

class Image:
    def open(self):
        print("Opening image")

def open_file(file):
    file.open()
```

Both objects work with `open_file()` because both provide an `open()` method.

**Interview trap:** Python supports overriding and duck typing. It does not support traditional signature-based method overloading in the same way as Java or C++.

## 8. Special (Dunder) Methods

Dunder means *double underscore*.

| Method | Purpose |
|---|---|
| `__init__()` | Initialize an instance |
| `__str__()` | Human-readable string representation |
| `__repr__()` | Developer-oriented representation |
| `__len__()` | Behavior for `len(obj)` |
| `__eq__()` | Behavior for `obj1 == obj2` |
| `__add__()` | Behavior for `obj1 + obj2` |
| `__del__()` | Finalization hook; timing is not guaranteed |

### `__str__()` vs `__repr__()`

```python
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def __str__(self):
        return f"{self.name}, age {self.age}"

    def __repr__(self):
        return f"Student({self.name!r}, {self.age!r})"

s = Student("Dhiraj", 22)

print(str(s))   # Dhiraj, age 22
print(repr(s))  # Student('Dhiraj', 22)
```

- `__str__()` is intended for a readable display.
- `__repr__()` is intended to be unambiguous and useful for debugging.
- If `__str__()` is absent, `str(obj)` can fall back to `__repr__()`.

**Interview note:** Avoid relying on `__del__()` for essential cleanup. Prefer context managers, such as `with open(...)`, for predictable resource management.

## 9. Abstraction — Basic Understanding

Abstraction exposes essential behavior while hiding implementation details.

Python supports abstract base classes through the `abc` module.

```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self):
        pass

class Square(Shape):
    def __init__(self, side):
        self.side = side

    def area(self):
        return self.side ** 2

s = Square(4)
print(s.area())  # 16
```

You cannot instantiate `Shape` while its abstract methods remain unimplemented.

## 10. The Four Pillars of OOP

| Pillar | Meaning |
|---|---|
| Encapsulation | Group data and methods; control access to state |
| Abstraction | Expose essential features and hide implementation details |
| Inheritance | Reuse and extend behavior from another class |
| Polymorphism | Use a common interface with different implementations |

## 11. Interview Practice Programs

### Beginner
1. Create a `Student` class with name, roll number and marks.
2. Create a `Rectangle` class with `area()` and `perimeter()`.
3. Create an `Employee` class with a class variable for company name.
4. Demonstrate method overriding using `Animal`, `Dog` and `Cat`.

### Intermediate
5. Build a `BankAccount` with deposit, withdrawal and balance-check methods.
6. Create a `Library` class to add, issue and return books.
7. Implement an abstract `Shape` class with `Circle` and `Rectangle`.
8. Implement `__str__()` and `__eq__()` for a custom class.
9. Demonstrate multiple inheritance and inspect the MRO.
10. Create a game with a base `Character` class and child classes such as `Warrior` and `Mage`.

## 12. Last-Minute Checklist

- [ ] Explain class vs object.
- [ ] Explain `self` and `__init__()`.
- [ ] Differentiate instance and class variables.
- [ ] Explain instance, class and static methods.
- [ ] Demonstrate inheritance and `super()`.
- [ ] Explain encapsulation and name mangling.
- [ ] Demonstrate polymorphism through overriding.
- [ ] Explain abstraction and abstract classes.
- [ ] Differentiate `__str__()` and `__repr__()`.
- [ ] Write a bank account program without looking at notes.
