# Day 1: Introduction to Data Science, Environment Setup & Python Basics

* **Date:** June 24, 2026 (Wednesday)
* **Module / Focus:** Data Science Overview, Environment Configuration, Variables, I/O Operations, Core Data Types, and Operators
* **Tools Used:** Python 3, Jupyter Notebook, VS Code, Google Colab

## 1. Objectives & Concepts Learned

### Data Science & Its Lifecycle

Explored the fundamentals of Data Science, data-driven decision-making, and real-world applications across industries such as:

* Healthcare
* Finance
* E-commerce
* Sports
* Social Media

Studied the **8-stage Data Science Lifecycle**:

**Business Problem → Data Collection → Data Cleaning → EDA → Modeling → Evaluation → Deployment → Monitoring**

### Development Environment

Configured programming environments for Data Science using:

* Jupyter Notebook
* VS Code with Python and Jupyter extensions
* Google Colab

### Variables & Input/Output Operations

Learned about:

* Variable declaration and assignment
* `snake_case` naming conventions
* Formatted strings using **f-strings**
* Taking user input using `input()`
* Type conversion using `int()`, `float()`, and `str()`

### Core Data Types & Mutability

Studied the difference between **mutable** and **immutable** Python objects.

**Mutable:** `list`, `dict`, `set`

**Immutable:** `int`, `float`, `str`, `tuple`

### Operators

Practiced different types of Python operators, including:

* Arithmetic operators
* Floor division (`//`)
* Exponentiation (`**`)
* Membership operators (`in`, `not in`)
* Equality operator (`==`)
* Identity operator (`is`)

## 2. Data Structures & Core Types Covered

### Integer and Float — `int`, `float`

Immutable numeric data types used for calculations, including:

* `abs()`
* `pow()`
* `round()`

### String — `str`

An immutable and ordered sequence of characters.

Practiced:

* Indexing
* Slicing (`[start:end]`)
* `.upper()`
* `.lower()`
* `.replace()`
* `.startswith()`

### List — `list`

A mutable and ordered collection that allows duplicate elements.

Practiced:

* `.append()`
* `.insert()`
* `.remove()`
* `.sort()`

### Dictionary — `dict`

A mutable collection of key-value pairs with unique keys.

Practiced:

* `.get()`
* `.keys()`
* `.values()`
* Adding new key-value pairs

### Tuple — `tuple`

An immutable and ordered collection that supports:

* Indexing
* `.count()`
* `.index()`

### Set — `set`

A mutable collection of unique elements.

Studied set operations such as:

* Union
* Intersection
* Difference

## 3. Practical Tasks & Code Implementation

### Task 1: Student Information Form

```python
name = input("Enter Name: ")
age = int(input("Enter Age: "))
city = input("Enter City: ")

print(f"My name is {name}")
print(f"My age is {age}")
print(f"My city is {city}")
```

### Task 2: Mathematical Operations

```python
num1 = int(input("Enter First Number: "))
num2 = int(input("Enter Second Number: "))

print("Addition:", num1 + num2)
print("Subtraction:", num1 - num2)
print("Multiplication:", num1 * num2)
print("Division:", num1 / num2)
print("Floor Division:", num1 // num2)
print("Power:", num1 ** num2)
```

### Task 3: String Slicing & Case Manipulation

```python
name = input("Enter Name: ")

print("Length of Name:", len(name))
print("Uppercase Name:", name.upper())
print("Lowercase Name:", name.lower())
print("First 3 Characters:", name[0:3])
```

### Task 4: List Manipulation & Mutability

```python
fruits = ["Apple", "Mango", "Banana"]

fruits.append("Orange")
fruits.insert(1, "Kiwi")
fruits.remove("Banana")
fruits.sort()

print("Final List:", fruits)
```

### Task 5: Dictionary & Identity Verification

```python
student = {
    "name": "Rahul",
    "age": 22
}

student["city"] = "Delhi"

print("Keys:", list(student.keys()))
print("Values:", list(student.values()))
print("Name:", student.get("name"))

# Identity vs Equality check
list1 = [10, 20, 30]
list2 = [10, 20, 30]

print("Equality (list1 == list2):", list1 == list2)  # True
print("Identity (list1 is list2):", list1 is list2)  # False
```

## 4. Key Takeaways

* User input received through `input()` is stored as a string by default and may require type conversion for numerical operations.
* The equality operator (`==`) compares the values of objects, while the identity operator (`is`) checks whether two references point to the same object.
* Mutable data structures such as lists, dictionaries, and sets can be modified after creation.
* Immutable data types cannot be modified after creation.
* Understanding Python's core data types and operators provides a strong foundation for Data Science and data analysis.

## 5. Learning Outcome

By the end of Day 1, I gained a foundational understanding of **Data Science, its lifecycle, Python programming basics, core data structures, mutability, operators, and development environments**. I also practiced implementing basic Python programs using user input and built-in data structures.
