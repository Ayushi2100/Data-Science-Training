# Day 20: Correlation Matrices, Heatmaps & Data Storytelling

- **Date:** July 21, 2026 (Tuesday)
- **Module / Focus:** Feature Relationship Visualization, Pearson Correlation Matrices, Heatmap Customization, and Data Storytelling
- **Tools Used:** Python 3, Seaborn, Matplotlib, Pandas, Jupyter Notebook

### 1. In-Depth Technical Breakdown & Theoretical Foundations

#### Quantifying Pairwise Feature Relationships

- **Linear Correlation Matrices (`df.corr()`):** Computes pairwise linear association scores across all numerical columns in a DataFrame. The resulting matrix is symmetric along its diagonal, where each variable has a perfect positive correlation with itself (`r = 1.0`).

- **Identifying Multicollinearity:** Strongly correlated predictor variables, commonly identified using a threshold such as `|r| > 0.8`, may indicate multicollinearity. Multicollinearity can make coefficient estimates in linear models unstable and make it difficult to determine the individual contribution of correlated features.

#### Visualizing Multi-Variable Grids (`sns.heatmap`)

- **Visualizing Correlation Grids:** Passing a correlation matrix to `sns.heatmap()` converts numerical correlation values into a visual color-coded grid, making patterns and relationships between multiple variables easier to identify.

- **Diverging Color Palettes (`cmap`):** Diverging color schemes such as `'coolwarm'`, `'vlag'`, and `'RdBu'` distinguish positive and negative correlations using contrasting tones, with the color scale centered around zero.

- **Numerical Cell Annotations:** Setting `annot=True` displays the exact correlation coefficient inside each heatmap cell. Using `fmt='.2f'` formats the values to two decimal places, improving readability.

#### Data Storytelling & Visual Communication

- **Communicating Insights:** Data storytelling transforms statistical results into understandable insights by connecting visual patterns with analytical or business questions.

- **Clear Visualization Design:** Titles, axis labels, appropriate color scales, fixed correlation limits (`vmin=-1`, `vmax=1`), and annotated values help transform a technical correlation matrix into a decision-ready visualization.

### 2. Comprehensive Code Implementation & Step-by-Step Execution

```python
import seaborn as sns
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np

# ---------------------------------------------------------
# 1. Synthetic Dataset Construction
# ---------------------------------------------------------
np.random.seed(42)
n_samples = 150

# Engineering features with known mathematical relationships
price = np.random.uniform(20, 500, n_samples)
quantity = np.random.randint(1, 10, n_samples)
discount = np.random.uniform(0, 0.3, n_samples)

# Derived feature:
# Revenue = Price * Quantity * (1 - Discount)
revenue = (
    (price * quantity) * (1 - discount)
    + np.random.normal(0, 25, n_samples)
)

customer_rating = np.random.normal(
    4.2,
    0.5,
    n_samples
).clip(1, 5)

df = pd.DataFrame({
    'Price': price,
    'Quantity': quantity,
    'Discount': discount,
    'Revenue': revenue,
    'Customer_Rating': customer_rating
})

print("--- Base Dataset Preview ---")
print(df.head())


# ---------------------------------------------------------
# 2. Pearson Correlation Matrix Computation
# ---------------------------------------------------------
corr_matrix = df.corr(numeric_only=True)

print("\n--- Correlation Matrix ---")
print(corr_matrix.round(2))


# ---------------------------------------------------------
# 3. Annotated Heatmap Visualization
#    (sns.heatmap)
# ---------------------------------------------------------
fig, ax = plt.subplots(figsize=(8, 6))

# Generate an annotated correlation heatmap
# using a diverging color palette
sns.heatmap(
    corr_matrix,
    annot=True,
    fmt='.2f',
    cmap='coolwarm',
    vmin=-1.0,
    vmax=1.0,
    linewidths=0.5,
    square=True,
    cbar_kws={"shrink": 0.8},
    ax=ax
)

ax.set_title(
    'Feature Correlation Heatmap',
    fontsize=14,
    fontweight='bold',
    pad=12
)

plt.xticks(rotation=45, ha='right')
plt.yticks(rotation=0)

plt.tight_layout()
plt.show()
```

### 3. Key Takeaways & Practical Recommendations

- **Format Matrix Cell Values Clearly:** Use `annot=True` and a precision format such as `fmt='.2f'` in `sns.heatmap()` so that the exact correlation coefficients are easy to read.

- **Use Fixed Palette Limits (`vmin` & `vmax`):** Set `vmin=-1.0` and `vmax=1.0` to ensure the heatmap represents the complete possible Pearson correlation range consistently.

- **Spot Feature Redundancy Early:** Use correlation heatmaps during exploratory data analysis to identify highly correlated or potentially redundant features before using them in predictive models.

- **Remember That Correlation Is Not Causation:** A strong correlation between two variables indicates a statistical association, not necessarily that one variable causes the other. Additional analysis is required to establish causality.

- **Focus on Strong Relationships:** Correlation values close to `+1` indicate strong positive linear association, values close to `-1` indicate strong negative linear association, and values near `0` indicate weak or no linear relationship.

- **Use Heatmaps for Data Storytelling:** A well-designed heatmap can quickly communicate which features move together, helping analysts identify important patterns and potential multicollinearity before further modeling.
