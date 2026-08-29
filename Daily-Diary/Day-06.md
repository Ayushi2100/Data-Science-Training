# Day 6: Python Basics Assessment & Practical Evaluation

Date: July 1, 2026 (Wednesday)

Module / Focus: Practical Assessment on Core Python, Data Structures, Control Flow, Functions and Dynamic Arguments

Tools Used: Python 3, Jupyter Notebook

## 1. Assessment Overview

Day 6 focused on a practical assessment covering the Python concepts learned during the first week of training.

The assessment tested my ability to:

* Apply Python fundamentals to practical problems
* Use functions to create modular solutions
* Work with lists and numerical data
* Apply conditional statements and loops
* Use default arguments
* Work with `*args` and `**kwargs`
* Perform calculations and data analysis using Python

## 2. Topics Tested

1. Lists and numerical data
2. `sum()`, `max()` and `min()`
3. Average and statistical calculations
4. Conditional statements
5. Discount calculations
6. Functions and default arguments
7. `*args`
8. `**kwargs`
9. Dictionary processing
10. List filtering and comprehensions

## 3. Practical Assessment Tasks

### Question 1: Student Result Analyzer

Created a function to calculate the total, average, highest and lowest marks, and the number of students who passed.

```python id="a2f7k9"
def analyze_results(marks):
    total_marks = sum(marks)
    avg_marks = round(total_marks / len(marks), 2)
    highest_marks = max(marks)
    lowest_marks = min(marks)
    passed_students = sum(1 for m in marks if m >= 40)

    print(f"Total Marks: {total_marks}")
    print(f"Average Marks: {avg_marks}")
    print(f"Highest Marks: {highest_marks}")
    print(f"Lowest Marks: {lowest_marks}")
    print(f"Passed Students: {passed_students}")

    return total_marks, avg_marks, highest_marks, lowest_marks, passed_students


marks_list = [78, 45, 32, 91, 67, 39]

analyze_results(marks_list)
```

### Question 2: Shopping Cart Calculator

Created a function using a default discount and applied an additional discount when the bill crossed a specified amount.

```python id="r8m3q1"
def calculate_bill(prices, discount=10):
    original_bill = sum(prices)
    discounted_bill = original_bill * (1 - discount / 100)

    extra_discount_applied = False

    if discounted_bill > 5000:
        discounted_bill *= 0.95
        extra_discount_applied = True

    final_amount = round(discounted_bill)

    print(f"Original Bill: {original_bill}")
    print(f"Discount Applied: {discount}%")
    print(f"Extra Discount: {'Yes' if extra_discount_applied else 'No'}")
    print(f"Final Amount: {final_amount}")

    return final_amount


item_prices = [1200, 800, 1500, 2500]

calculate_bill(item_prices)
```

### Question 3: Employee Information System

Created a function using `**kwargs` to accept employee information dynamically and classify the salary.

```python id="v5n2s8"
def employee(**kwargs):
    for key, value in kwargs.items():
        print(f"{key.capitalize()}: {value}")

    salary = kwargs.get("salary", 0)

    if salary > 50000:
        print("High Salary")
    else:
        print("Normal Salary")

    total_details = len(kwargs)

    print(f"Total Details: {total_details}")

    return total_details


employee(
    name="Rahul",
    age=25,
    department="IT",
    salary=60000
)
```

### Question 4: Number Analysis Tool

Created a function using `*args` to analyze a variable number of numerical values.

```python id="q6k1p4"
def analyze_numbers(*args):
    largest = max(args)
    smallest = min(args)

    even_count = sum(1 for n in args if n % 2 == 0)
    odd_count = sum(1 for n in args if n % 2 != 0)

    total_sum = sum(args)
    average = round(total_sum / len(args), 2)

    divisible_by_3_and_5 = [
        n for n in args
        if n % 3 == 0 and n % 5 == 0
    ]

    print(f"Largest Number: {largest}")
    print(f"Smallest Number: {smallest}")
    print(f"Even Numbers: {even_count}")
    print(f"Odd Numbers: {odd_count}")
    print(f"Sum: {total_sum}")
    print(f"Average: {average}")
    print(f"Divisible by both 3 and 5: {divisible_by_3_and_5}")

    return (
        largest,
        smallest,
        even_count,
        odd_count,
        total_sum,
        average,
        divisible_by_3_and_5
    )


analyze_numbers(12, 15, 20, 9, 30, 7, 4)
```

## 4. Key Takeaways

* Practiced applying Python concepts to real-world problem-solving scenarios.
* Used built-in functions such as `sum()`, `max()` and `min()` for data calculations.
* Practiced creating reusable functions with default arguments.
* Applied `*args` to handle a variable number of inputs.
* Applied `**kwargs` to process dynamic employee information.
* Used conditional logic and list comprehensions for data filtering.
* Improved problem-solving and practical Python programming skills.

## 5. Learning Outcome

The Day 6 assessment helped me evaluate my understanding of the Python concepts covered during the first week. It provided practical experience in solving problems involving calculations, functions, conditional logic, lists and dynamic arguments.
