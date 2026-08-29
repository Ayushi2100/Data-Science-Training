# Day 9: DataFrame Indexing, Slicing & Advanced Filtering

Date: July 6, 2026 (Monday)

Module / Focus: DataFrame Indexing, Slicing, Boolean Filtering and Conditional Selection

Tools Used: Python 3, Pandas, Jupyter Notebook

## 1. Topics Covered

1. DataFrame row and column selection
2. Label-based indexing using `.loc`
3. Position-based indexing using `.iloc`
4. DataFrame slicing
5. Boolean filtering
6. Multiple conditions
7. `.isin()` method
8. `.between()` method
9. Bitwise operators in Pandas

## 2. Concepts Learned

### Label-Based Indexing Using `.loc`

Learned how to select rows and columns using their labels with `.loc[]`.

Example:

```python id="locexample"
df.loc["E2":"E4", "Employee":"Salary"]
```

An important point is that `.loc[]` includes both the starting and ending labels when slicing.

### Position-Based Indexing Using `.iloc`

Learned how to select rows and columns using their numerical positions with `.iloc[]`.

Example:

```python id="ilocexample"
df.iloc[1:4, 0:3]
```

Unlike `.loc[]`, `.iloc[]` follows normal Python slicing rules, so the ending position is excluded.

### Boolean Filtering

Learned how to filter rows based on conditions.

For example:

```python id="booleanexample"
df[df["Salary"] > 65000]
```

This returns only the rows where the salary is greater than 65,000.

### Multiple Conditions

Learned how to combine multiple conditions using:

* `&` for AND
* `|` for OR
* `~` for NOT

Each condition should be enclosed in parentheses.

Example:

```python id="multipleconditions"
df[
    (df["Department"] == "IT") &
    (df["Salary"] > 65000)
]
```

### `.isin()` Method

Learned how `.isin()` can be used to filter rows matching multiple possible values.

Example:

```python id="isinexample"
df[df["Department"].isin(["HR", "Finance"])]
```

### `.between()` Method

Learned how `.between()` can be used to select values within a specified range.

Example:

```python id="betweenexample"
df[df["Experience"].between(3, 5)]
```

By default, both boundary values are included.

## 3. Practical Implementation

### Task 1: Creating a DataFrame

```python id="create_dataframe_day9"
import pandas as pd

data = {
    "Employee": ["Alice", "Bob", "Charlie", "David", "Eve", "Frank"],
    "Department": ["HR", "IT", "IT", "HR", "Finance", "Finance"],
    "Salary": [50000, 70000, 65000, 55000, 80000, 75000],
    "Experience": [2, 5, 4, 3, 7, 6]
}

df = pd.DataFrame(
    data,
    index=["E1", "E2", "E3", "E4", "E5", "E6"]
)

print("Initial DataFrame:")
print(df)
```

### Task 2: Using `.loc` and `.iloc`

```python id="loc_iloc_day9"
loc_subset = df.loc["E2":"E4", "Employee":"Salary"]

iloc_subset = df.iloc[1:4, 0:3]

print("Using .loc:")
print(loc_subset)

print("\nUsing .iloc:")
print(iloc_subset)
```

### Task 3: Filtering Using Multiple Conditions

```python id="multi_filter_day9"
it_high_salary = df[
    (df["Department"] == "IT") &
    (df["Salary"] > 65000)
]

print("IT Employees with Salary Greater Than 65,000:")
print(it_high_salary)
```

### Task 4: Filtering Using `.between()`

```python id="between_day9"
mid_level_exp = df[
    df["Experience"].between(3, 5)
]

print("Employees with 3 to 5 Years of Experience:")
print(mid_level_exp)
```

### Task 5: Filtering Using `.isin()`

```python id="isin_day9"
target_depts = df[
    df["Department"].isin(["HR", "Finance"])
]

print("Employees from HR and Finance:")
print(target_depts)
```

## 4. Key Takeaways

* `.loc[]` is used for label-based selection.
* `.iloc[]` is used for position-based selection.
* `.loc[]` includes the ending label during slicing.
* `.iloc[]` follows Python's standard slicing rule and excludes the ending position.
* Boolean conditions can be used to filter DataFrame rows.
* Use `&`, `|` and `~` for combining Pandas conditions.
* Individual conditions should be placed inside parentheses.
* `.isin()` makes membership-based filtering simple and readable.
* `.between()` provides a convenient way to filter values within a range.

## 5. Learning Outcome

By the end of Day 9, I learned how to select, slice and filter data in Pandas using both labels and positions. I also practiced applying multiple conditions and using `.isin()` and `.between()` to perform more effective data filtering.
