# Day 4: Mastering Control Flow Statements

Date: June 29, 2026 (Monday)

Module / Focus: Conditional Statements, Loops and Loop Control Statements

Tools Used: Python 3, Jupyter Notebook

## 1. Topics Covered

1. `if` statements
2. `if-else` statements
3. `if-elif-else` statements
4. Nested conditions
5. `for` loops
6. `while` loops
7. `range()` function
8. `break`, `continue` and `pass`

## 2. Concepts Learned

### Conditional Statements

Learned how to control program execution using:

* `if`
* `if-else`
* `if-elif-else`
* Nested `if` statements

Also practiced proper indentation for defining Python code blocks.

### For Loops

Learned how to iterate through sequences such as lists and strings using `for` loops.

Practiced the `range()` function with:

* Start and stop values
* Custom step values
* Reverse iteration

### While Loops

Learned how to execute a block of code repeatedly while a condition remains `True`.

Also understood the importance of updating loop variables to avoid infinite loops.

### Loop Control Statements

Studied three important loop control keywords:

* `break` – immediately terminates the current loop.
* `continue` – skips the current iteration and moves to the next iteration.
* `pass` – acts as a placeholder when a statement is syntactically required but no action is needed.

## 3. Practical Tasks

### Task 1: Number Classifier

```python id="9z3yq4"
num_input = float(input("Enter a number: "))

if num_input > 0:
    print("The number is Positive.")
elif num_input < 0:
    print("The number is Negative.")
else:
    print("The number is Zero.")
```

### Task 2: Multiplication Table

```python id="p8s8kx"
table_num = int(input("Enter an integer: "))

print(f"Multiplication Table for {table_num}:")

for i in range(1, 11):
    print(f"{table_num} x {i} = {table_num * i}")
```

### Task 3: Running Sum with Break

```python id="4y4jdn"
running_sum = 0
stop_number = None

for number in range(1, 51):
    if number % 2 == 0:
        running_sum += number

        if running_sum > 150:
            stop_number = number
            break

print(f"Loop stopped at number: {stop_number}")
print(f"Final Running Sum: {running_sum}")
```

### Task 4: Number Filtering Using Continue

```python id="k3o1t8"
print("Numbers not divisible by 3 or 5:")

for num in range(1, 21):
    if num % 3 == 0 or num % 5 == 0:
        continue

    print(num, end=" ")

print()
```

### Task 5: Prime and Composite Numbers

```python id="b1z8a6"
prime = []
composite = []

for i in range(2, 21):
    factors = 0

    for j in range(1, i + 1):
        if i % j == 0:
            factors += 1

            if factors > 2:
                break

    if factors == 2:
        prime.append(i)
    else:
        composite.append(i)

print("Primes (2-20):", prime)
print("Composites (2-20):", composite)
```

## 4. Key Takeaways

* Conditional statements allow programs to make decisions based on conditions.
* `for` loops are useful for iterating over sequences and ranges.
* `while` loops are useful when repetition depends on a condition.
* `break` can terminate a loop early when a required condition is reached.
* `continue` skips the current iteration and proceeds with the next one.
* Proper indentation is essential for defining Python code blocks.
* Loop variables must be updated appropriately in `while` loops to prevent infinite execution.

## 5. Learning Outcome

By the end of Day 4, I gained a better understanding of Python control flow and learned how to use conditional statements, loops and loop control statements to build programs involving decision-making, repetition and filtering.
