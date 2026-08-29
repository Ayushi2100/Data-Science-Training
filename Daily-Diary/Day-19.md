# Day 19: Statistical Data Visualization with Seaborn

- **Date:** July 20, 2026 (Monday)
- **Module / Focus:** Seaborn Global Styling, Categorical Frequency Counts (`countplot`), Distribution Profiling (`histplot` with KDE), and Aggregate Comparisons (`barplot` with Error Bars)
- **Tools Used:** Python 3, Seaborn, Matplotlib, Pandas, Jupyter Notebook

### 1. In-Depth Technical Breakdown & Theoretical Foundations

#### High-Level Visual Themes & Global Styling (`sns.set_theme`)

- **Declarative API Architecture:** Built on top of Matplotlib, Seaborn provides a high-level interface for creating statistical visualizations and integrates naturally with Pandas DataFrames. It can automatically perform statistical aggregations and map categorical variables to visual properties.

- **Global Theme Configuration (`sns.set_theme()`):** Controls the overall appearance of Seaborn plots, including grid styles, color palettes, and font scaling. This provides consistent styling across multiple visualizations without manually configuring every axis.

#### Categorical Frequency & Distribution Modeling

- **Frequency Counting (`sns.countplot`):** Displays the number of observations belonging to each categorical value. Unlike a basic Matplotlib bar chart, `countplot()` can calculate category frequencies directly from raw DataFrame data without requiring a separate `.value_counts()` operation.

- **Kernel Density Estimation (`sns.histplot(..., kde=True)`):** Combines a histogram with a smooth Kernel Density Estimation (KDE) curve. KDE provides an approximation of the underlying probability density of a continuous variable and helps identify distribution characteristics such as skewness, peaks, and overall shape.

#### Statistical Aggregations & Error Bars

- **Automated Statistical Aggregation (`sns.barplot`):** Seaborn's `barplot()` can automatically calculate an aggregation such as the mean for each categorical group and display the result visually.

- **Error Bar Interpretations (`errorbar` Parameter):**
  - `errorbar='sd'`: Displays standard deviation around the estimated group mean, representing the variability of observations within each category.
  - `errorbar=('ci', 95)`: Displays a 95% confidence interval for the estimated statistic, commonly calculated using bootstrapping.

### 2. Comprehensive Code Implementation & Step-by-Step Execution

```python
import seaborn as sns
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np

# ---------------------------------------------------------
# 1. Global Styling & Dataset Construction
# ---------------------------------------------------------
# Apply Seaborn default aesthetic theme
sns.set_theme(style="whitegrid", palette="muted")

np.random.seed(42)
n_samples = 200

data = {
    'Category': np.random.choice(
        ['Electronics', 'Accessories', 'Apparel', 'Home'],
        size=n_samples,
        p=[0.4, 0.25, 0.2, 0.15]
    ),
    'Revenue': np.random.exponential(scale=250, size=n_samples) + 20,
    'Customer_Rating': np.random.normal(
        loc=4.2,
        scale=0.6,
        size=n_samples
    ).clip(1, 5)
}

df = pd.DataFrame(data)

print("--- Base Dataset Preview ---")
print(df.head())


# ---------------------------------------------------------
# 2. Categorical Frequency Analysis (sns.countplot)
# ---------------------------------------------------------
fig, ax = plt.subplots(figsize=(8, 4))

sns.countplot(
    data=df,
    x='Category',
    order=df['Category'].value_counts().index,
    ax=ax
)

ax.set_title(
    'Transaction Volume by Product Category',
    fontsize=12,
    fontweight='bold'
)
ax.set_xlabel('Category', fontsize=10)
ax.set_ylabel('Transaction Count', fontsize=10)

plt.tight_layout()
plt.show()


# ---------------------------------------------------------
# 3. Distribution & Density Estimation
#    (sns.histplot + KDE)
# ---------------------------------------------------------
fig, ax = plt.subplots(figsize=(8, 4))

sns.histplot(
    data=df,
    x='Revenue',
    kde=True,
    bins=20,
    color='teal',
    ax=ax
)

ax.set_title(
    'Revenue Distribution with Kernel Density Estimation (KDE)',
    fontsize=12,
    fontweight='bold'
)
ax.set_xlabel('Revenue ($)', fontsize=10)
ax.set_ylabel('Frequency Density', fontsize=10)

plt.tight_layout()
plt.show()


# ---------------------------------------------------------
# 4. Aggregated Comparisons with Standard Deviation
#    (sns.barplot)
# ---------------------------------------------------------
fig, ax = plt.subplots(figsize=(8, 4))

sns.barplot(
    data=df,
    x='Category',
    y='Revenue',
    estimator=np.mean,
    errorbar='sd',
    capsize=0.1,
    ax=ax
)

ax.set_title(
    'Mean Revenue by Category (with Standard Deviation Error Bars)',
    fontsize=12,
    fontweight='bold'
)
ax.set_xlabel('Category', fontsize=10)
ax.set_ylabel('Mean Revenue ($)', fontsize=10)

plt.tight_layout()
plt.show()
```

### 3. Key Takeaways & Practical Recommendations

- **Pass Raw DataFrames Directly:** Use Seaborn's `data`, `x`, and `y` parameters to provide raw DataFrames directly. Seaborn can perform frequency calculations and statistical aggregations internally.

- **Use KDE for Distribution Analysis:** Enable `kde=True` with `histplot()` to understand the shape of continuous variables and identify characteristics such as skewness, concentration, and multiple peaks.

- **Specify Error Bars Explicitly:** Use `errorbar='sd'` when the objective is to visualize variability within groups. Use confidence intervals such as `errorbar=('ci', 95)` when the objective is to communicate uncertainty around an estimated statistic.

- **Use Seaborn for Statistical Visualization:** Seaborn is particularly useful for EDA because it combines attractive visual defaults with built-in statistical functionality and direct DataFrame integration.

- **Choose Visualization Based on the Question:** Use `countplot()` for categorical frequencies, `histplot()` with KDE for distributions, and `barplot()` for comparing aggregated numerical values across categories.

- **Interpret Error Bars Carefully:** Error bars represent a specific statistical quantity and should not automatically be interpreted as proof of statistical significance. Always check what the selected error-bar method represents before drawing conclusions.
