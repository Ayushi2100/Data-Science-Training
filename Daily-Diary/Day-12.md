# Day 12: Data Quality Assessment & Validation

- **Date:** July 9, 2026 (Thursday)
- **Module / Focus:** Missing Value Auditing, Duplicate Record Detection, Data Type Verification, and Logical Consistency Checks
- **Tools Used:** Python 3, Pandas, NumPy, Jupyter Notebook

## 1. In-Depth Technical Breakdown & Theoretical Foundations

### Missing Value Auditing & Null Quantification

- **Identifying Null States:** Missing values such as `NaN` and `None` can affect statistical calculations, data analysis, and machine learning workflows. Therefore, identifying missing values is an important first step in data quality assessment.

- **Null Masking (`df.isnull()` / `df.isna()`):** These methods generate a Boolean DataFrame with the same shape as the original dataset. Missing values are represented as `True`, while non-missing values are represented as `False`.

- **Aggregated Missingness Audit:** Combining `df.isnull().sum()` calculates the total number of missing values in each column. The percentage of missing values can also be calculated using `(df.isnull().sum() / len(df)) * 100`.

- **Missing Value Analysis:** The percentage of missing values helps determine whether a column should be dropped, imputed, or retained for further analysis.

### Duplicate Record Detection & Primary Key Auditing

- **Row-Level Duplicate Identification:** Duplicate records can lead to incorrect statistical summaries and may introduce bias into data analysis and machine learning workflows.

- **Evaluating Duplicates (`df.duplicated()`):** The `duplicated()` method returns a Boolean Series indicating whether each row is a duplicate of a previous row.

- **The `keep` Parameter:** The `keep` parameter controls which duplicate record is considered the original:
  - `keep='first'` keeps the first occurrence unmarked.
  - `keep='last'` keeps the last occurrence unmarked.
  - `keep=False` marks all duplicate occurrences as `True`.

- **Primary Key Uniqueness Verification:** Duplicate values in important identifier columns can indicate data integrity problems. For example, `df.duplicated(subset=['Transaction_ID'], keep=False)` can be used to identify repeated transaction IDs.

### Data Type Verification

- **Type Alignment Audit:** Each column should have an appropriate data type according to the meaning of the data.

- Numerical values such as `Price`, `Quantity`, and `Revenue` should generally be stored using numeric data types.

- Identifiers such as `Transaction_ID` can be stored as strings.

- Incorrectly stored values, such as prices represented as strings like `"₹1,200"`, can prevent mathematical operations and require preprocessing.

- The `.dtypes` attribute can be used to inspect the data type of every column.

### Business Logic & Logical Consistency Checks

- **Cross-Column Validation:** Data quality checks should also verify whether relationships between different columns follow expected business rules.

- For example, if the business rule states that:

  **Revenue = Price × Quantity**

  then the calculated revenue can be compared with the recorded revenue.

- Records where the calculated value differs from the recorded value can be flagged for further investigation.

## 2. Data Quality Assessment Workflow

A systematic data quality assessment can be performed using the following steps:

1. Inspect the dataset structure.
2. Identify missing values.
3. Calculate missing value counts and percentages.
4. Detect completely duplicated rows.
5. Check duplicate values in important identifier columns.
6. Verify the data types of all columns.
7. Validate relationships between related columns.
8. Identify inconsistent records requiring further investigation.

## 3. Comprehensive Code Implementation & Step-by-Step Execution

```python
import pandas as pd
import numpy as np

# ---------------------------------------------------------
# 1. Dataset Setup
# ---------------------------------------------------------
# Simulating a messy raw sales dataset

raw_data = {
    'Transaction_ID': ['T101', 'T102', 'T103', 'T103', 'T105', 'T106', 'T107'],
    'Product': ['Laptop', 'Mouse', None, 'Mouse', 'Keyboard', 'Monitor', 'Laptop'],
    'Price': [1200.0, 25.0, 300.0, 25.0, 45.0, np.nan, 1200.0],
    'Quantity': [1, 3, 2, 3, 4, 2, 1],
    'Revenue': [1200.0, 75.0, 600.0, 75.0, 200.0, 500.0, 1200.0]
}

df = pd.DataFrame(raw_data)

print("--- Initial Dataset ---")
print(df)


# ---------------------------------------------------------
# 2. Missing Value Quantification Audit
# ---------------------------------------------------------

missing_count = df.isnull().sum()

missing_percent = (
    df.isnull().sum() / len(df) * 100
).round(2)

missing_audit_df = pd.DataFrame({
    'Missing Count': missing_count,
    'Missing %': missing_percent
})

print("\n--- Missing Value Audit ---")
print(missing_audit_df)


# ---------------------------------------------------------
# 3. Duplicate Record Inspection
# ---------------------------------------------------------

# Check for completely duplicated rows
full_duplicates = df[df.duplicated()]

print("\n--- Fully Duplicate Rows ---")
print(full_duplicates)


# ---------------------------------------------------------
# 4. Primary Key Duplicate Detection
# ---------------------------------------------------------

# Check for duplicate Transaction_ID values
key_duplicates = df[
    df.duplicated(
        subset=['Transaction_ID'],
        keep=False
    )
]

print("\n--- Duplicate Transaction IDs ---")
print(key_duplicates)


# ---------------------------------------------------------
# 5. Data Type Verification
# ---------------------------------------------------------

print("\n--- Data Types ---")
print(df.dtypes)


# ---------------------------------------------------------
# 6. Business Logic Validation
# ---------------------------------------------------------

# Business rule:
# Revenue should equal Price multiplied by Quantity

expected_revenue = df['Price'] * df['Quantity']

logic_mismatches = df[
    df['Revenue'] != expected_revenue
]

print("\n--- Revenue Mismatches ---")
print(logic_mismatches)
```

## 4. Practical Tasks & Their Purpose

### Task 1: Missing Value Audit

```python
missing_count = df.isnull().sum()

missing_percent = (
    df.isnull().sum() / len(df) * 100
).round(2)
```

This identifies the number and percentage of missing values in each column.

### Task 2: Full Duplicate Detection

```python
full_duplicates = df[df.duplicated()]
```

This checks whether complete rows have been repeated in the dataset.

### Task 3: Duplicate Transaction ID Detection

```python
key_duplicates = df[
    df.duplicated(
        subset=['Transaction_ID'],
        keep=False
    )
]
```

This identifies all records having the same transaction ID.

### Task 4: Data Type Inspection

```python
print(df.dtypes)
```

This verifies whether the columns have appropriate data types for their intended operations.

### Task 5: Logical Consistency Validation

```python
expected_revenue = df['Price'] * df['Quantity']

logic_mismatches = df[
    df['Revenue'] != expected_revenue
]
```

This compares the recorded revenue with the expected revenue and identifies inconsistent records.

## 5. Difference Between Full Duplicates and Duplicate Keys

A **full duplicate** occurs when all values in two or more rows are identical.

A **duplicate key** occurs when an important identifier, such as `Transaction_ID`, appears more than once, even if the remaining column values are different.

For example:

```python
df.duplicated()
```

checks for completely duplicated rows.

Whereas:

```python
df.duplicated(
    subset=['Transaction_ID'],
    keep=False
)
```

checks for duplicate transaction IDs.

Therefore, a dataset can contain duplicate keys without containing completely duplicate rows.

## 6. Data Quality Checks Summary

| Quality Check | Pandas Method | Purpose |
|---|---|---|
| Missing values | `isnull()` / `isna()` | Identify missing data |
| Missing value count | `isnull().sum()` | Count missing values per column |
| Missing percentage | `isnull().sum() / len(df) * 100` | Measure missing data proportion |
| Duplicate rows | `duplicated()` | Detect repeated complete records |
| Duplicate keys | `duplicated(subset=...)` | Check identifier uniqueness |
| Data types | `dtypes` | Verify column data types |
| Business rules | Boolean conditions | Detect logical inconsistencies |

## 7. Key Takeaways

- Data quality assessment should be performed before detailed analysis or machine learning.
- Missing values can affect calculations and statistical analysis and should be identified early.
- `isnull()` and `isna()` are useful for detecting missing values.
- `isnull().sum()` can be used to calculate the number of missing values in each column.
- Missing value percentages help determine the appropriate handling strategy.
- `duplicated()` helps identify repeated records.
- Full duplicate rows and duplicate identifier values represent different data quality problems.
- The `subset` parameter can be used to check duplicates in specific columns.
- The `.dtypes` attribute helps verify whether columns have appropriate data types.
- Business rules can be used to identify logically inconsistent records.
- Validating relationships between columns helps detect incorrect or corrupted data before further analysis.

## 8. Learning Outcome

By the end of Day 12, I learned how to systematically assess the quality of a dataset using Pandas and NumPy. I practiced identifying missing values, measuring missing data percentages, detecting duplicate records and duplicate identifiers, verifying data types, and validating business rules between related columns.

These techniques provide an important foundation for preparing reliable and accurate datasets for Exploratory Data Analysis and future machine learning workflows.
