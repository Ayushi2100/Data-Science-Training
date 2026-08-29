# Day 8: Pandas Architecture, Core Structures & Data Loading

Date: July 3, 2026 (Friday)

Module / Focus: Pandas Series, DataFrames, Data Inspection and Data Loading

Tools Used: Python 3, Pandas, NumPy, Jupyter Notebook

## 1. Topics Covered

1. Introduction to Pandas
2. NumPy vs Pandas
3. Pandas Series
4. Pandas DataFrame
5. Creating Series and DataFrames
6. Indexing and label-based access
7. DataFrame structure and data types
8. `.shape`, `.dtypes`, `.size`, `.index` and `.columns`
9. Reading CSV and Excel files
10. `index_col`, `usecols` and `parse_dates`
11. `.squeeze()` method

## 2. Concepts Learned

### NumPy and Pandas

Learned the basic difference between NumPy and Pandas.

* NumPy is mainly used for numerical and array-based operations.
* Pandas provides higher-level data structures for working with structured and tabular data.
* Pandas is especially useful for handling datasets containing different types of data such as numbers, text and dates.

### Pandas Series

A Series is a one-dimensional Pandas data structure containing values along with an index.

A Series can be created with custom index labels.

It supports both:

* Position-based access using `.iloc`
* Label-based access using the index label

### Pandas DataFrame

A DataFrame is a two-dimensional tabular data structure consisting of rows and columns.

It can contain different data types in different columns and is commonly used for working with datasets.

### DataFrame Inspection

Learned how to inspect the structure of a DataFrame using:

* `.shape` – number of rows and columns
* `.dtypes` – data type of each column
* `.size` – total number of elements
* `.index` – row labels
* `.columns` – column names

These attributes help understand a dataset before performing analysis.

### Reading Data from Files

Learned about loading external datasets using:

```python
pd.read_csv()
pd.read_excel()
```

Also studied useful parameters such as:

* `index_col` – sets a column as the DataFrame index
* `usecols` – loads only selected columns
* `parse_dates` – converts date columns into datetime values

### `.squeeze()` Method

Learned how `.squeeze()` can reduce a DataFrame with a single column into a Series.

This can be useful when a one-dimensional structure is required for further processing.

## 3. Practical Implementation

### Task 1: Creating and Accessing a Series

```python
import pandas as pd
import numpy as np

subjects = ["Maths", "English", "Science", "Hindi"]
marks = [85, 92, 78, 88]

marks_series = pd.Series(
    marks,
    index=subjects,
    name="Student Marks"
)

print("Pandas Series:")
print(marks_series)

print("\nPositional Lookup:")
print(marks_series.iloc[1])

print("\nLabel Lookup:")
print(marks_series["Science"])
```

### Task 2: Creating and Inspecting a DataFrame

```python
data = {
    "Student_ID": [101, 102, 103, 104],
    "Name": ["Aman", "Ravi", "Neha", "Pooja"],
    "Score": [88.5, 75.0, 93.2, 82.0],
    "Passed": [True, True, True, True]
}

df_students = pd.DataFrame(data)

df_students.set_index("Student_ID", inplace=True)

print("DataFrame:")
print(df_students)

print("\nShape:")
print(df_students.shape)

print("\nData Types:")
print(df_students.dtypes)

print("\nTotal Elements:")
print(df_students.size)

print("\nIndex:")
print(df_students.index)

print("\nColumns:")
print(df_students.columns)
```

### Task 3: Selecting Data While Reading a File

Studied how Pandas can be used to select required columns while loading a dataset.

Example:

```python
df = pd.read_csv(
    "data.csv",
    usecols=["Name", "Score"],
    index_col="Name"
)

print(df)
```

Also learned that `parse_dates` can be used when working with date columns.

Example:

```python
df = pd.read_csv(
    "data.csv",
    parse_dates=["Order_Date"]
)
```

### Task 4: Converting a DataFrame into a Series

```python
single_col_df = pd.DataFrame({
    "Target_Metric": [10.5, 20.4, 30.1, 40.8]
})

squeezed_series = single_col_df.squeeze("columns")

print("Original Type:")
print(type(single_col_df))

print("\nAfter Squeeze:")
print(type(squeezed_series))

print("\nSeries:")
print(squeezed_series)
```

## 4. Key Takeaways

* Pandas is an important Python library for data analysis and data manipulation.
* A Series is a one-dimensional data structure, while a DataFrame is two-dimensional.
* DataFrames can contain multiple columns with different data types.
* `.shape`, `.dtypes`, `.size`, `.index` and `.columns` help inspect the structure of a dataset.
* `usecols` can be useful when only specific columns are required from a large dataset.
* `index_col` can be used to assign a meaningful column as the DataFrame index.
* `parse_dates` helps convert date columns into datetime data.
* `.squeeze()` can convert a single-column DataFrame into a Series.

## 5. Learning Outcome

By the end of Day 8, I gained a basic understanding of Pandas and learned how to create and inspect Series and DataFrames. I also practiced loading datasets and using different Pandas parameters to prepare data for further analysis.
