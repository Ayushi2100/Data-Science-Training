# Day 5: Functions, Modular Design and Variable Scope

Date: June 30, 2026 (Tuesday)

Module / Focus: Functions, Arguments, Return Values, Lambda Functions and Variable Scope

Tools Used: Python 3, Jupyter Notebook

## 1. Topics Covered

1. Function definition using `def`
2. Positional and keyword arguments
3. Default arguments
4. Variable-length arguments using `*args` and `**kwargs`
5. Return values
6. Multiple return values
7. Lambda functions
8. `map()`, `filter()` and `sorted()`
9. LEGB scope rule
10. `global` and `nonlocal` keywords

## 2. Concepts Learned

### Functions

Learned how to create reusable blocks of code using the `def` keyword.

Also practiced:

* Parameters and arguments
* Function calls
* Return statements
* Docstrings
* Default parameters

### Function Arguments

Learned different ways of passing arguments:

* Positional arguments
* Keyword arguments
* Default arguments
* Variable-length positional arguments using `*args`
* Variable-length keyword arguments using `**kwargs`

`*args` collects additional positional arguments into a tuple, while `**kwargs` collects additional keyword arguments into a dictionary.

### Return Values

Learned that functions can return values using the `return` statement.

Also practiced returning multiple values from a function and unpacking them into separate variables.

A function without an explicit `return` statement returns `None`.

### Lambda Functions

Learned how to create small anonymous functions using the `lambda` keyword.

Practiced using lambda functions with:

* `filter()`
* `map()`
* `sorted()`

### Variable Scope and LEGB Rule

Learned how Python searches for variables using the LEGB rule:

**Local → Enclosing → Global → Built-in**

Also studied:

* `global` for modifying variables defined at the global level
* `nonlocal` for modifying variables from an enclosing function scope

## 3. Practical Tasks

### Task 1: Leap Year Function

```python id="u1b7h3"
def is_leap_year(year):
    return (year % 4 == 0 and year % 100 != 0) or (year % 400 == 0)

print("Is 2000 a leap year?:", is_leap_year(2000))
print("Is 1900 a leap year?:", is_leap_year(1900))
print("Is 2024 a leap year?:", is_leap_year(2024))
```

### Task 2: Calculate Statistics

```python id="j7w8np"
def calculate_stats(numbers):
    if not numbers:
        return 0, 0.0, 0

    total_sum = sum(numbers)
    count = len(numbers)
    average = total_sum / count

    return total_sum, average, count


total, mean, n_items = calculate_stats([10, 20, 30, 40, 50])

print(f"Total: {total}")
print(f"Mean: {mean}")
print(f"Count: {n_items}")
```

### Task 3: Using `*args` and `**kwargs`

```python id="5g7m3x"
def build_employee_profile(emp_id, name, *certifications, **details):
    profile = {
        "id": emp_id,
        "name": name,
        "certifications": list(certifications)
    }

    profile.update(details)

    return profile


user_record = build_employee_profile(
    101,
    "Amit Sharma",
    "Python",
    "Data Science",
    department="Analytics",
    city="Mumbai",
    experience_years=4
)

print("Employee Profile:", user_record)
```

### Task 4: Filtering and Sorting Using Lambda

```python id="z8q6k2"
employees = [
    {"name": "Amit", "age": 28, "salary": 50000},
    {"name": "Neha", "age": 35, "salary": 75000},
    {"name": "Raj", "age": 24, "salary": 45000},
    {"name": "Pooja", "age": 31, "salary": 80000}
]

high_earners = list(
    filter(lambda emp: emp["salary"] > 50000, employees)
)

sorted_high_earners = sorted(
    high_earners,
    key=lambda emp: emp["age"]
)

print("Filtered and Sorted Employees:", sorted_high_earners)
```

### Task 5: Global and Nonlocal Scope

```python id="n4v2rs"
runs_count = 0

def update_count():
    global runs_count
    runs_count += 1
    print(f"Global run counter: {runs_count}")


update_count()
update_count()


def outer_pipeline():
    status = "Pending"

    def inner_step():
        nonlocal status
        status = "Completed"

    inner_step()

    return status


print("Pipeline Result:", outer_pipeline())
```

## 4. Key Takeaways

* Functions help make programs reusable, organized and easier to maintain.
* `*args` allows a function to accept multiple positional arguments.
* `**kwargs` allows a function to accept multiple keyword arguments.
* Functions can return one or multiple values.
* Lambda functions are useful for short operations such as filtering and sorting.
* Python follows the LEGB rule when searching for variables.
* The `global` and `nonlocal` keywords allow controlled modification of variables outside the current local scope.

## 5. Learning Outcome

By the end of Day 5, I gained a better understanding of Python functions, argument handling, return values, lambda functions and variable scope. I also practiced building reusable functions and applying functional programming concepts to data processing tasks.
