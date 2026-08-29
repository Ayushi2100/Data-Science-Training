# Day 11: Exploratory Data Analysis (EDA) Fundamentals

Date: July 8, 2026 (Wednesday)

Module / Focus: Dataset Profiling, Data Inspection, Summary Statistics and Value Distribution

Tools Used: Python 3, Pandas, Jupyter Notebook

## 1. Topics Covered

1. Introduction to Exploratory Data Analysis (EDA)
2. Understanding dataset dimensions
3. DataFrame structure and schema inspection
4. Checking data types
5. Summary statistics
6. Categorical data analysis
7. Frequency distribution
8. Percentage distribution
9. Sorting DataFrames

## 2. Concepts Learned

### Introduction to EDA

Learned that Exploratory Data Analysis is an important step in the data analysis process used to understand a dataset before performing further analysis or building models.

EDA helps identify:

* Dataset structure
* Data types
* Missing values
* Numerical distributions
* Categorical distributions
* Possible unusual values
* Relationships and patterns in the data

### Dataset Dimensions Using `.shape`

Learned how `.shape` provides the number of rows and columns in a DataFrame.

Example:

```python id="shape_day11"
print(df.shape)
```

This gives the dataset dimensions in the form:

```text
(rows, columns)
```

### Dataset Information Using `.info()`

Learned how `.info()` provides an overview of the DataFrame, including:

* Number of entries
* Column names
* Non-null values
* Data types
* Memory usage

This is useful for getting an initial understanding of a dataset.

### Checking Data Types

Used `.dtypes` to check the data type of each column.

This helps determine whether a column contains:

* Integers
* Floating-point numbers
* Strings
* Boolean values
* Other data types

### Summary Statistics Using `.describe()`

Learned how `.describe()` provides statistical information about numerical columns.

It includes:

* Count
* Mean
* Standard deviation
* Minimum
* 25th percentile
* Median
* 75th percentile
* Maximum

Also learned that:

```python id="describe_all_day11"
df.describe(include="all")
```

can be used to obtain descriptive information for both numerical and categorical columns.

### Frequency Analysis Using `.value_counts()`

Learned how `.value_counts()` can be used to count how frequently each unique value occurs in a column.

For example:

```python id="valuecounts_day11"
df["Product"].value_counts()
```

Using:

```python id="normalize_day11"
df["Category"].value_counts(normalize=True)
```

returns proportions instead of raw counts.

Multiplying by 100 converts these proportions into percentages.

### Sorting Data Using `.sort_values()`

Learned how to arrange DataFrame rows according to one or more columns.

For example:

```python id="sort_day11"
df.sort_values(
    by=["Price", "Quantity"],
    ascending=[False, True]
)
```

This sorts the data by:

* Price in descending order
* Quantity in ascending order when prices are equal

## 3. Practical Implementation

### Task 1: Creating the Dataset

```python id="dataset_day11"
import pandas as pd

data = {
    "Transaction_ID": [
        "T101", "T102", "T103",
        "T104", "T105", "T106"
    ],
    "Product": [
        "Laptop", "Mouse", "Monitor",
        "Mouse", "Laptop", "Keyboard"
    ],
    "Category": [
        "Electronics", "Accessories",
        "Electronics", "Accessories",
        "Electronics", "Accessories"
    ],
    "Price": [1200, 25, 300, 25, 1200, 45],
    "Quantity": [1, 3, 2, 5, 2, 4],
    "Revenue": [1200, 75, 600, 125, 2400, 180]
}

df = pd.DataFrame(data)

print(df)
```

### Task 2: Structural Inspection

```python id="inspection_day11"
print("Dataset Shape:")
print(df.shape)

print("\nData Types:")
print(df.dtypes)

print("\nDataset Information:")
df.info()
```

### Task 3: Numerical Summary

```python id="summary_day11"
print("Numerical Summary:")
print(df.describe())
```

### Task 4: Complete Dataset Summary

```python id="fullsummary_day11"
print("Complete Dataset Summary:")
print(df.describe(include="all"))
```

### Task 5: Product Frequency Analysis

```python id="frequency_day11"
print("Product Frequencies:")
print(df["Product"].value_counts())

print("\nCategory Percentage Distribution:")
print(
    df["Category"].value_counts(normalize=True) * 100
)
```

### Task 6: Sorting the Dataset

```python id="sorting_day11"
sorted_df = df.sort_values(
    by=["Price", "Quantity"],
    ascending=[False, True]
)

print("Sorted DataFrame:")
print(sorted_df)
```

## 4. Key Takeaways

* EDA helps understand a dataset before performing detailed analysis.
* `.shape` provides the number of rows and columns.
* `.info()` provides useful information about columns, non-null values and data types.
* `.dtypes` helps verify the data type of each column.
* `.describe()` provides important statistical summaries for numerical data.
* `.value_counts()` helps analyze the frequency of categorical values.
* `value_counts(normalize=True)` can be used to calculate proportions.
* `.sort_values()` allows data to be sorted using one or multiple columns.

## 5. Learning Outcome

By the end of Day 11, I learned the fundamentals of Exploratory Data Analysis and practiced inspecting, summarizing, sorting and understanding the distribution of values in a dataset using Pandas.
