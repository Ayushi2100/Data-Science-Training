# Day 3: Comprehensive Study of Python Operators

Date: June 26, 2026 (Friday)

Module / Focus: Arithmetic, Comparison, Logical, Assignment, Identity and Membership Operators

Tools Used: Python 3, Jupyter Notebook

## 1. Topics Covered

1. Arithmetic operators
2. Comparison operators
3. Logical operators
4. Assignment and compound assignment operators
5. Identity operators
6. Membership operators
7. Boolean expressions and conditional evaluation

## 2. Concepts Learned

### Arithmetic Operators

Practiced mathematical operations using:

* Addition (`+`)
* Subtraction (`-`)
* Multiplication (`*`)
* Division (`/`)
* Floor division (`//`)
* Modulus (`%`)
* Exponentiation (`**`)

Understood that `/` returns a floating-point result, while `//` performs floor division.

### Comparison Operators

Learned to compare values using:

* `==`
* `!=`
* `>`
* `<`
* `>=`
* `<=`

These operators return Boolean values: `True` or `False`.

### Logical Operators

Practiced combining Boolean expressions using:

* `and`
* `or`
* `not`

Also learned about short-circuit evaluation in logical expressions.

### Assignment Operators

Practiced assignment and compound assignment operators:

* `=`
* `+=`
* `-=`
* `*=`
* `/=`
* `%=`
* `//=`
* `**=`

### Identity Operators

Learned the difference between equality and identity:

* `==` checks whether values are equal.
* `is` checks whether two references point to the same object.
* `is not` checks whether they refer to different objects.

The `id()` function was used to inspect object identities.

### Membership Operators

Practiced:

* `in`
* `not in`

Learned that membership testing behaves differently depending on the data structure. For dictionaries, `in` checks keys by default.

## 3. Practical Tasks

### Task 1: Leap Year and Parity Verification

```python
year = 2024

is_leap_year = (year % 4 == 0 and year % 100 != 0) or (year % 400 == 0)
is_even = year % 2 == 0

print(f"Year {year} is a leap year: {is_leap_year}")
print(f"Year {year} is an even number: {is_even}")
```

### Task 2: Email Domain Verification

```python
allowed_domains = ["gmail.com", "yahoo.com", "outlook.com"]
user_email = "john.doe@gmail.com"

domain = user_email.split("@")[-1]

if domain in allowed_domains:
    print(f"Valid domain: {domain}")
else:
    print(f"Invalid domain: {domain}")
```

### Task 3: Equality vs Identity

```python
x = [10, 20]
y = [10, 20]
z = x

print("x == y:", x == y)
print("x is y:", x is y)
print("x is z:", x is z)

print("id(x):", id(x))
print("id(y):", id(y))
print("id(z):", id(z))
```

### Task 4: Eligibility and Conditional Evaluation

```python
homework_score = 85
exam_score = 72

has_passed = (homework_score >= 80 and exam_score >= 70) or (exam_score == 100)

if has_passed:
    print("Student Status: Passed")
else:
    print("Student Status: Failed")
```

### Task 5: Dictionary Membership

```python
student_scores = {
    "Alice": 95,
    "Bob": 88,
    "Charlie": 92
}

print("Alice in dictionary:", "Alice" in student_scores)
print("95 in dictionary:", 95 in student_scores)
print("95 in dictionary values:", 95 in student_scores.values())
```

## 4. Key Takeaways

* Arithmetic operators are used for mathematical calculations.
* Comparison and logical operators are useful for building conditional expressions.
* Compound assignment operators simplify variable updates.
* `==` compares values, while `is` checks object identity.
* The `in` operator checks membership, and dictionary membership checks keys by default.
* Understanding operators is essential for writing conditions, calculations and data-processing logic in Python.

## 5. Learning Outcome

By the end of Day 3, I developed a better understanding of Python operators and practiced using them in mathematical calculations, conditional statements, membership checks, email validation and object identity comparisons.
