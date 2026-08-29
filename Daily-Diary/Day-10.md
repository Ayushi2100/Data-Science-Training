# Day 10: Aggregations, Grouping & Multi-Table Operations

Date: July 7, 2026 (Tuesday)

Module / Focus: Grouping, Aggregation, Pivot Tables, Cross-Tabulation, Merging and Concatenation

Tools Used: Python 3, Pandas, Jupyter Notebook

## 1. Topics Covered

1. `groupby()`
2. Aggregation functions
3. `.agg()` method
4. Pivot tables
5. Cross-tabulation
6. Merging DataFrames
7. Concatenating DataFrames
8. Split-Apply-Combine approach

## 2. Concepts Learned

### Grouping Data Using `groupby()`

Learned how to divide data into groups based on the values of a particular column and perform calculations on each group.

For example, employee data can be grouped according to department to calculate the average salary of each department.

The `groupby()` process can be understood as:

**Split → Apply → Combine**

* Split the data into groups.
* Apply a calculation to each group.
* Combine the results into a summary.

### Aggregation Using `.agg()`

Learned how `.agg()` can be used to perform different calculations on different columns.

Common aggregation functions include:

* `mean()`
* `sum()`
* `min()`
* `max()`
* `count()`

For example, average and total salary can be calculated while also finding the highest performance score.

### Pivot Tables

Learned how to create summary tables using `pivot_table()`.

Pivot tables are useful for analyzing numerical data based on one or more categories.

Example:

```python id="pivotexample"
df.pivot_table(
    values="Salary",
    index="Department",
    aggfunc="mean"
)
```

### Cross-Tabulation

Learned how `pd.crosstab()` can be used to calculate frequency counts between categorical variables.

For example, it can show the number of employees who are bonus-eligible or not within each department.

### Merging DataFrames

Learned how to combine related DataFrames using `pd.merge()`.

The merge operation is similar to joining tables in SQL.

Common types of joins include:

* Inner join
* Left join
* Right join
* Outer join

### Concatenating DataFrames

Learned how `pd.concat()` can be used to combine DataFrames.

* `axis=0` combines DataFrames row-wise.
* `axis=1` combines DataFrames column-wise.

## 3. Practical Implementation

### Task 1: Creating the Dataset

```python id="dataset_day10"
import pandas as pd

df = pd.DataFrame({
    "Department": ["HR", "IT", "IT", "HR", "Finance", "Finance"],
    "Salary": [50000, 70000, 65000, 55000, 80000, 75000],
    "Performance_Score": [85, 92, 88, 75, 95, 80],
    "Bonus_Eligible": ["Yes", "Yes", "No", "No", "Yes", "No"]
})

print("Base Dataset:")
print(df)
```

### Task 2: Grouping and Aggregation

```python id="groupby_day10"
grouped_summary = df.groupby("Department").agg({
    "Salary": ["mean", "sum"],
    "Performance_Score": "max"
})

print("Grouped Summary:")
print(grouped_summary)
```

This calculates:

* Average salary for each department
* Total salary for each department
* Highest performance score for each department

### Task 3: Creating a Pivot Table

```python id="pivot_day10"
pivot_df = df.pivot_table(
    values="Salary",
    index="Department",
    aggfunc="mean"
)

print("Pivot Table:")
print(pivot_df)
```

### Task 4: Creating a Cross-Tabulation

```python id="crosstab_day10"
cross_tab = pd.crosstab(
    df["Department"],
    df["Bonus_Eligible"]
)

print("Cross-Tabulation:")
print(cross_tab)
```

### Task 5: Merging DataFrames

Created a second DataFrame containing department and floor information.

```python id="merge_day10"
locations = pd.DataFrame({
    "Department": ["HR", "IT", "Finance"],
    "Floor": [1, 3, 2]
})

merged_df = pd.merge(
    df,
    locations,
    on="Department",
    how="inner"
)

print("Merged DataFrame:")
print(merged_df)
```

### Task 6: Concatenating DataFrames

```python id="concat_day10"
df_part1 = pd.DataFrame({
    "Name": ["Aman", "Ravi"],
    "Score": [85, 90]
})

df_part2 = pd.DataFrame({
    "Name": ["Neha", "Pooja"],
    "Score": [88, 92]
})

combined_df = pd.concat(
    [df_part1, df_part2],
    ignore_index=True
)

print("Concatenated DataFrame:")
print(combined_df)
```

## 4. Key Takeaways

* `groupby()` is useful for analyzing data category-wise.
* The Split-Apply-Combine approach helps organize grouped data analysis.
* `.agg()` allows multiple aggregation operations to be performed together.
* `pivot_table()` creates summarized views of numerical data.
* `pd.crosstab()` is useful for analyzing relationships between categorical variables.
* `pd.merge()` combines related DataFrames based on common columns.
* `pd.concat()` combines DataFrames along rows or columns.
* Grouping and aggregation are important techniques in exploratory data analysis.

## 5. Learning Outcome

By the end of Day 10, I learned how to summarize and analyze datasets using grouping and aggregation. I also gained practical experience with pivot tables, cross-tabulation, merging and concatenating DataFrames, which are important operations in data analysis.
