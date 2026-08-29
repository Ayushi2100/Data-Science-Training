# Day 13: Data Cleaning & Preprocessing Strategies

- **Date:** July 10, 2026 (Friday)
- **Module / Focus:** Missing Value Imputation, Record Deduplication, Datetime Standardization, and String Cleaning
- **Tools Used:** Python 3, Pandas, Jupyter Notebook

## 1. In-Depth Technical Breakdown & Theoretical Foundations

### Selective Imputation vs. Row Deletion Mechanics

- **Targeted Row Deletion (`.dropna()`):** Used when essential identification fields such as primary keys or timestamps are missing. Removing rows using `subset=['Transaction_ID', 'Date']` clears unidentifiable records without unnecessarily removing rows that only contain missing numerical attributes.

- **Numerical Imputation Strategies:** Missing numerical values can be replaced using central tendency measures. Median imputation using `.fillna(df['Price'].median())` is useful when the data contains extreme values or outliers because the median is less affected by them than the mean.

- **Categorical Imputation:** Missing categorical values can be replaced using mode imputation with `.fillna(df['Category'].mode()[0])`. The `.mode()` method returns a Pandas Series, so `[0]` is used to extract the first mode as a scalar value.

### String Standardization & Formatting Normalization

- **Whitespace Elimination (`.str.strip()`):** Removes leading and trailing spaces from string values. This prevents logically identical values from being treated as different categories.

- **Casing Normalization (`.str.title()` / `.str.lower()`):** Standardizes the capitalization of categorical values. For example, `"laptop"`, `"LAPTOP"`, and `"Laptop "` can be converted into a consistent representation such as `"Laptop"`.

### Order of Execution for Deduplication

- **Sequence Dependency:** Text standardization should be performed before `.drop_duplicates()`.

- If duplicate records contain differences only in capitalization or whitespace, deduplicating before cleaning may fail to identify them as duplicates.

- Therefore, the recommended sequence is:

  **String Cleaning → Missing Value Handling → Deduplication → Datetime Conversion**

### Datetime Standardization & Type Casting

- **String-to-Timestamp Conversion (`pd.to_datetime()`):** Converts date strings into Pandas datetime values.

- Standardizing dates enables chronological sorting, date-based filtering, time-series analysis, and extraction of features such as year, month, and day.

## 2. Data Cleaning & Preprocessing Workflow

The following workflow was followed during the practical session:

1. Load the raw dataset.
2. Inspect the uncleaned values.
3. Remove unnecessary whitespace from text columns.
4. Standardize text capitalization.
5. Remove rows missing essential identifiers.
6. Impute missing categorical values using the mode.
7. Impute missing numerical values using the median.
8. Remove duplicate records.
9. Convert date columns into standardized datetime format.
10. Inspect the final cleaned dataset and its data types.

## 3. Comprehensive Code Implementation & Step-by-Step Execution

```python
import pandas as pd
import numpy as np

# ---------------------------------------------------------
# 1. Dataset Setup
# ---------------------------------------------------------
# Simulating raw and uncleaned data

raw_data = {
    'Transaction_ID': [' T101 ', 'T102', 'T103', 'T103 ', 'T105', None],
    'Date': ['2026-07-01', '2026-07-02', '2026-07-03', '2026-07-03', '2026-07-05', '2026-07-06'],
    'Product': ['laptop ', ' Mouse', 'MONITOR', 'Monitor', None, 'Keyboard'],
    'Category': ['electronics', 'Accessories', 'Electronics', 'Electronics', 'Accessories', None],
    'Price': [1200.0, 25.0, 300.0, 300.0, np.nan, 45.0],
    'Quantity': [1, 3, 2, 2, 4, 1]
}

df = pd.DataFrame(raw_data)

print("--- Uncleaned Raw Dataset ---")
print(df)


# ---------------------------------------------------------
# 2. Text Cleaning & Whitespace Elimination
# ---------------------------------------------------------

# Remove leading and trailing whitespace
df['Transaction_ID'] = df['Transaction_ID'].str.strip()
df['Product'] = df['Product'].str.strip()
df['Category'] = df['Category'].str.strip()

# Standardize text capitalization
df['Product'] = df['Product'].str.title()
df['Category'] = df['Category'].str.title()

print("\n--- After String Standardization ---")
print(df[['Transaction_ID', 'Product', 'Category']])


# ---------------------------------------------------------
# 3. Selective Null Dropping
# ---------------------------------------------------------

# Drop rows missing essential identification fields
df = df.dropna(
    subset=['Transaction_ID', 'Date']
)


# ---------------------------------------------------------
# 4. Categorical Imputation Using Mode
# ---------------------------------------------------------

# Fill missing Category values using the most frequent category
category_mode = df['Category'].mode()[0]
df['Category'] = df['Category'].fillna(category_mode)

# Fill missing Product values using the most frequent product
product_mode = df['Product'].mode()[0]
df['Product'] = df['Product'].fillna(product_mode)


# ---------------------------------------------------------
# 5. Numerical Imputation Using Median
# ---------------------------------------------------------

# Calculate median price
price_median = df['Price'].median()

# Replace missing prices with the median
df['Price'] = df['Price'].fillna(price_median)

print("\n--- After Selective Imputation ---")
print(df)


# ---------------------------------------------------------
# 6. Deduplication
# ---------------------------------------------------------

# Remove duplicate rows after text standardization
df = df.drop_duplicates()


# ---------------------------------------------------------
# 7. Datetime Standardization
# ---------------------------------------------------------

# Convert Date column from string to datetime
df['Date'] = pd.to_datetime(df['Date'])

print("\n--- Final Cleaned Dataset ---")
print(df)

print("\n--- Final Data Types ---")
print(df.dtypes)
```

## 4. Practical Tasks & Their Purpose

### Task 1: String Cleaning

```python
df['Transaction_ID'] = df['Transaction_ID'].str.strip()
df['Product'] = df['Product'].str.strip().str.title()
df['Category'] = df['Category'].str.strip().str.title()
```

This removes unnecessary whitespace and standardizes text capitalization.

### Task 2: Removing Rows with Missing Essential Fields

```python
df = df.dropna(
    subset=['Transaction_ID', 'Date']
)
```

This removes records that cannot be reliably identified because essential fields are missing.

### Task 3: Categorical Imputation

```python
category_mode = df['Category'].mode()[0]
df['Category'] = df['Category'].fillna(category_mode)
```

The most frequently occurring category is used to replace missing categorical values.

### Task 4: Numerical Imputation

```python
price_median = df['Price'].median()
df['Price'] = df['Price'].fillna(price_median)
```

The median price is used to replace missing numerical values.

### Task 5: Deduplication

```python
df = df.drop_duplicates()
```

This removes completely duplicated rows after text values have been standardized.

### Task 6: Datetime Conversion

```python
df['Date'] = pd.to_datetime(df['Date'])
```

This converts date strings into Pandas datetime values for easier temporal analysis.

## 5. Importance of Cleaning Order

The order of preprocessing operations can affect the final dataset.

For example, consider:

```text
"T103"
"T103 "
```

Before string cleaning, these values are technically different because the second value contains an extra space.

After applying:

```python
df['Transaction_ID'] = df['Transaction_ID'].str.strip()
```

both values become:

```text
"T103"
"T103"
```

They can then be recognized as duplicates.

Therefore, text standardization should be performed **before deduplication**.

## 6. Data Cleaning Techniques Summary

| Cleaning Task | Pandas Method | Purpose |
|---|---|---|
| Remove whitespace | `.str.strip()` | Standardize text values |
| Change text case | `.str.title()` / `.str.lower()` | Normalize categorical values |
| Remove incomplete key records | `.dropna(subset=...)` | Preserve reliable records |
| Mode imputation | `.mode()[0]` + `.fillna()` | Fill missing categorical values |
| Median imputation | `.median()` + `.fillna()` | Fill missing numerical values |
| Remove duplicates | `.drop_duplicates()` | Eliminate repeated records |
| Convert dates | `pd.to_datetime()` | Standardize datetime values |

## 7. Key Takeaways

- Data cleaning is an essential preprocessing step before performing analysis or building machine learning models.
- Text values should be standardized before duplicate detection.
- `.str.strip()` removes unnecessary leading and trailing whitespace.
- `.str.title()` and `.str.lower()` can standardize text capitalization.
- `.dropna(subset=...)` allows selective removal of rows with missing essential fields.
- Mode imputation is useful for filling missing categorical values.
- `.mode()` returns a Series, so `[0]` can be used to extract the first mode.
- Median imputation is useful for numerical data when outliers or skewed distributions are present.
- `.drop_duplicates()` removes completely duplicated records.
- `pd.to_datetime()` converts date strings into standardized datetime values.
- The order of preprocessing operations matters because earlier transformations can affect the results of later cleaning steps.

## 8. Learning Outcome

By the end of Day 13, I learned how to clean and preprocess raw datasets using Pandas. I practiced standardizing text values, handling missing values through selective deletion and imputation, removing duplicate records, and converting date strings into proper datetime formats.

These preprocessing techniques help transform messy raw data into a cleaner and more consistent dataset that can be used for Exploratory Data Analysis and further data science workflows.
