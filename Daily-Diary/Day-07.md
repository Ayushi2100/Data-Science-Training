# Day 7: Advanced NumPy Operations, Random Sampling and Statistical Foundations

Date: July 2, 2026 (Thursday)

Module / Focus: NumPy Arrays, Reshaping, Flattening, Random Sampling, Outlier Detection and Missing Values

Tools Used: Python 3, NumPy, Jupyter Notebook

## 1. Topics Covered

1. NumPy multidimensional arrays
2. Array reshaping
3. `reshape()` and the `-1` parameter
4. `flatten()` and `ravel()`
5. Random number generation
6. Random seeds
7. Quartiles and IQR
8. Outlier detection
9. Handling `NaN` values
10. NaN-safe statistical functions

## 2. Concepts Learned

### Array Reshaping

Learned how to change the dimensions of a NumPy array using `reshape()` without changing the total number of elements.

Also learned that `-1` can be used to allow NumPy to automatically calculate one dimension.

For example:

```python
array.reshape(3, -1)
```

automatically determines the second dimension based on the number of elements.

### `flatten()` and `ravel()`

Studied two methods for converting multidimensional arrays into one-dimensional arrays.

* `flatten()` returns a copy of the array.
* `ravel()` returns a flattened view when possible, making it more memory-efficient.

### Random Number Generation

Practiced generating random values using:

* `np.random.rand()`
* `np.random.randn()`
* `np.random.randint()`
* `np.random.choice()`

Also learned how `np.random.seed()` can be used to produce reproducible random results.

### Outlier Detection Using IQR

Learned how the Interquartile Range (IQR) can be used to identify potential outliers.

The main concepts covered were:

* Q1: 25th percentile
* Q2: Median
* Q3: 75th percentile
* IQR = Q3 - Q1

Outlier boundaries can be calculated using:

**Lower Bound = Q1 - 1.5 × IQR**

**Upper Bound = Q3 + 1.5 × IQR**

Values outside these boundaries can be considered potential outliers.

### Handling Missing Values

Learned about `np.nan` and how missing numerical values can affect statistical calculations.

Practiced NaN-safe functions such as:

* `np.nanmean()`
* `np.nansum()`
* `np.nanmedian()`

Also practiced replacing missing values with the mean of the available data.

## 3. Practical Implementation

### Task 1: Array Reshaping and Flattening

```python id="6c5m2r"
import numpy as np

base_arr = np.arange(1, 13)

print("Original Array:")
print(base_arr)

reshaped_2d = base_arr.reshape(3, -1)

print("\nReshaped Array:")
print(reshaped_2d)

flattened = reshaped_2d.flatten()
raveled = reshaped_2d.ravel()

raveled[0] = 999

print("\nModified Raveled Array:")
print(raveled)

print("\nOriginal Array After Ravel Modification:")
print(reshaped_2d)

print("\nFlattened Array:")
print(flattened)
```

### Task 2: Random Sampling

```python id="y7h4p2"
np.random.seed(42)

rand_floats = np.random.rand(3)
rand_normal = np.random.randn(3)
rand_ints = np.random.randint(10, 100, size=5)

print("Random Floats:")
print(rand_floats)

print("\nRandom Normal Values:")
print(rand_normal)

print("\nRandom Integers:")
print(rand_ints)
```

### Task 3: Outlier Detection Using IQR

```python id="m2q8v5"
scores = np.array([
    55, 60, 62, 65, 68, 70,
    72, 75, 78, 80, 5, 150
])

q1, q3 = np.percentile(scores, [25, 75])

iqr = q3 - q1

lower_bound = q1 - (1.5 * iqr)
upper_bound = q3 + (1.5 * iqr)

outlier_mask = (
    (scores < lower_bound) |
    (scores > upper_bound)
)

clean_mask = (
    (scores >= lower_bound) &
    (scores <= upper_bound)
)

print("Q1:", q1)
print("Q3:", q3)
print("IQR:", iqr)

print("Lower Bound:", lower_bound)
print("Upper Bound:", upper_bound)

print("Detected Outliers:", scores[outlier_mask])
print("Clean Dataset:", scores[clean_mask])
```

### Task 4: Handling Missing Values

```python id="k9s3w1"
raw_metrics = np.array([
    85.0, np.nan, 72.0,
    np.nan, 91.0, 60.0
])

print("Mean using np.mean():", np.mean(raw_metrics))
print("Mean using np.nanmean():", np.nanmean(raw_metrics))

mean_value = np.nanmean(raw_metrics)

imputed_metrics = np.where(
    np.isnan(raw_metrics),
    mean_value,
    raw_metrics
)

print("Array after Imputation:")
print(imputed_metrics)
```

## 4. Key Takeaways

* NumPy provides efficient tools for numerical and array-based data processing.
* `reshape()` changes the dimensions of an array while preserving the number of elements.
* `flatten()` creates a copy, while `ravel()` can provide a view when possible.
* Random seeds help make random experiments reproducible.
* The IQR method can be used to identify potential outliers.
* Missing values represented by `NaN` can affect statistical calculations.
* NaN-safe functions such as `np.nanmean()` are useful when working with incomplete numerical data.

## 5. Learning Outcome

By the end of Day 7, I gained practical experience with NumPy arrays and learned how to reshape and flatten data, generate random samples, detect potential outliers using IQR, and handle missing numerical values.
