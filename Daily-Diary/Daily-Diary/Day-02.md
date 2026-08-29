# Day 2: In-Depth Exploration of Python Data Structures

Date: June 25, 2026 (Thursday)

Module / Focus: Strings, Lists, Tuples, Dictionaries, Sets, Their Methods, Built-in Functions and Slicing

Tools Used: Python 3, Jupyter Notebook

## 1. Topics Covered

1. Strings
2. Lists
3. Tuples
4. Dictionaries
5. Sets
6. Slicing and built-in functions
7. Mutable and immutable data structures

## 2. Concepts Learned

### Strings

Learned different techniques for string manipulation, including:

* String slicing using `[start:end:step]`
* Reversing strings using `[::-1]`
* Removing whitespace using `strip()`, `rstrip()` and `lstrip()`
* Changing letter case using `upper()` and `title()`
* Searching within strings using `find()`, `count()`, `startswith()` and `endswith()`
* Converting between characters and ASCII values using `ord()` and `chr()`

### Lists

Studied lists as mutable and ordered collections.

Practiced:

* `append()`
* `extend()`
* `insert()`
* `remove()`
* `pop()`
* `sort()`
* `reverse()`
* `max()`
* `min()`
* `sum()`
* `enumerate()`

### Tuples

Learned that tuples are immutable and ordered collections.

Covered:

* Tuple indexing
* Tuple methods such as `count()` and `index()`
* Single-element tuple syntax `(value,)`
* Tuple unpacking

### Dictionaries

Studied dictionaries as key-value data structures.

Practiced:

* Adding and updating key-value pairs
* `get()` for safe key retrieval
* `update()`
* `keys()`
* `values()`
* `items()`
* Iterating through dictionaries

### Sets

Learned that sets store unique elements and are useful for membership testing and removing duplicates.

Practiced:

* Creating sets
* Removing duplicate values
* Membership operators
* Union
* Intersection
* Difference
* Symmetric Difference
* Subset and disjoint checks

## 3. Practical Tasks

### Task 1: String Manipulation

```python
text = "Python Programming"

print("Step Slicing:", text[::2])
print("Reversed String:", text[::-1])

raw_data = "   data science is awesome!   "
cleaned = raw_data.strip().title()

print("Cleaned Text:", cleaned)
print("ASCII Value of 'a':", ord('a'))
print("Character for ASCII 95:", chr(95))
```

### Task 2: List Operations

```python
items = ["pen", "pencil", "eraser", "ruler", "marker"]

sliced = items[1:4]
reversed_sliced = list(reversed(sliced))

print("Extracted Slice:", sliced)
print("Reversed Sublist:", reversed_sliced)

numbers = [42, 7, 19, 88, 3]

print("Maximum Value:", max(numbers))
print("Sum:", sum(numbers))
print("Enumerated Values:", list(enumerate(numbers)))
```

### Task 3: Tuple Unpacking

```python
point = (45.2, -12.8, 100.5)

x, y, z = point

print(f"X: {x}, Y: {y}, Z: {z}")

scores = (8, 9, 8, 10, 7, 8, 9, 6)

print("Count of 8:", scores.count(8))
print("Index of 10:", scores.index(10))
```

### Task 4: Dictionary Operations

```python
book = {
    "title": "The Hobbit",
    "author": "J.R.R. Tolkien",
    "year": 1937
}

book["genre"] = "Fantasy"
book["year"] = 1938

print("Updated Book:", book)

inventory = {"apples": 15, "bananas": 8}

print("Oranges:", inventory.get("oranges", 0))

grades = {"Alice": "A", "Bob": "B", "Charlie": "A"}

for student_name, grade in grades.items():
    print(f"{student_name} scored an {grade}.")
```

### Task 5: Set Operations

```python
user_ids = ["id1", "id2", "id1", "id3", "id2", "id4"]

unique_ids = list(set(user_ids))

print("Unique IDs:", unique_ids)

alice_interests = {"reading", "cycling", "cooking"}
bob_interests = {"cooking", "gaming", "cycling"}

print("Shared Interests:", alice_interests & bob_interests)
print("All Interests:", alice_interests | bob_interests)
print("Alice's Exclusive Interests:", alice_interests - bob_interests)
```

## 4. Key Takeaways

* Strings and tuples are immutable, while lists, dictionaries and sets are mutable.
* Slicing can be used to extract portions of strings and lists.
* The `dict.get()` method allows safe retrieval of dictionary values without causing a `KeyError` when a key is missing.
* Sets are useful for removing duplicate values and performing mathematical set operations.
* Different Python data structures are suitable for different types of data and operations.

## 5. Learning Outcome

By the end of Day 2, I gained a deeper understanding of Python's major data structures and their practical applications. I also practiced manipulating strings, lists, tuples, dictionaries and sets using built-in methods and functions.
