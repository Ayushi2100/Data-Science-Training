# Day 14: Univariate, Bivariate & Multivariate Analysis Techniques

- **Date:** July 13, 2026 (Monday)
- **Module / Focus:** Distribution Skewness, Correlation Matrices, Covariance, Group-wise Comparisons, and Pairwise Relationships
- **Tools Used:** Python 3, Pandas, NumPy, Jupyter Notebook

### 1. In-Depth Technical Breakdown & Theoretical Foundations

#### Dimensionalities of Exploratory Analysis

- **Univariate Analysis:** Evaluates a single variable in isolation. The goal is to understand data distribution, central tendency (mean, median), dispersion (variance, standard deviation), and asymmetry (skewness).

- **Bivariate Analysis:** Examines relationships between two variables, either numerical or categorical. It can be used to assess relationships, co-movement, correlation, covariance, and group-wise differences.

- **Multivariate Analysis:** Evaluates interactions among three or more features simultaneously. It helps identify complex dependencies using correlation matrices, multi-axis groupings, and interactions among multiple variables.

#### Directionality & Magnitude Metrics

- **Covariance (Cov(X,Y)):** Measures the joint variability of two variables:

  **Cov(X,Y) = Σ[(Xi - X̄)(Yi - Ȳ)] / (n - 1)**

  A positive covariance indicates that the variables tend to move in the same direction, while a negative covariance indicates an inverse relationship. Since covariance is not standardized, its magnitude depends on the units of measurement.

- **Pearson Correlation Coefficient (r):** Standardizes covariance using the standard deviations of both variables:

  **r = Cov(X,Y) / (σX × σY)**

  The Pearson correlation coefficient ranges from **-1.0 to +1.0**:

  - **+1.0:** Perfect positive linear relationship.
  - **0.0:** No linear relationship.
  - **-1.0:** Perfect negative linear relationship.

#### Quantifying Asymmetry & Feature Relationships

- **Skewness:** Measures the asymmetry of a probability distribution:

  - **Zero Skew (≈ 0):** Approximately symmetric distribution where Mean ≈ Median.
  - **Positive Skew (> 0):** Right-tailed distribution where extreme high values pull the mean above the median.
  - **Negative Skew (< 0):** Left-tailed distribution where extreme low values pull the mean below the median.

- **Feature Correlation Matrix (`df.corr()`):** Calculates pairwise linear correlations between numerical attributes in a DataFrame. It provides a compact overview of relationships among multiple variables and can help identify strongly correlated predictors.

### 2. Comprehensive Code Implementation & Step-by-Step Execution

~~~python
import pandas as pd
import numpy as np

# ---------------------------------------------------------
# 1. Dataset Construction
# ---------------------------------------------------------
np.random.seed(42)
n_samples = 100

# Create correlated synthetic variables
marketing_spend = np.random.uniform(10, 100, n_samples)
sales_revenue = (marketing_spend * 2.5) + np.random.normal(0, 15, n_samples)
discount_rate = np.random.uniform(5, 25, n_samples)

# Create a positively skewed income distribution
customer_income = np.random.exponential(scale=50000, size=n_samples)

df = pd.DataFrame({
    'Marketing_Spend': marketing_spend,
    'Sales_Revenue': sales_revenue,
    'Discount_Rate': discount_rate,
    'Customer_Income': customer_income
})

print("--- Initial Multi-Feature Dataset ---")
print(df.head())


# ---------------------------------------------------------
# 2. Univariate Analysis: Skewness & Central Tendency
# ---------------------------------------------------------
income_mean = df['Customer_Income'].mean()
income_median = df['Customer_Income'].median()
income_skew = df['Customer_Income'].skew()

print("\n--- Univariate Profile: Customer Income ---")
print(f"Mean Income: ${income_mean:,.2f}")
print(f"Median Income: ${income_median:,.2f}")
print(f"Distribution Skewness: {income_skew:.2f} (Positive Skew)")


# ---------------------------------------------------------
# 3. Bivariate Analysis: Covariance & Correlation
# ---------------------------------------------------------
cov_val = df['Marketing_Spend'].cov(df['Sales_Revenue'])
corr_val = df['Marketing_Spend'].corr(df['Sales_Revenue'])

print("\n--- Bivariate Analysis: Spend vs. Revenue ---")
print(f"Covariance: {cov_val:.2f}")
print(f"Pearson Correlation (r): {corr_val:.4f}")


# ---------------------------------------------------------
# 4. Multivariate Analysis: Pairwise Correlation Matrix
# ---------------------------------------------------------
corr_matrix = df.corr(numeric_only=True)

print("\n--- Multivariate Correlation Matrix ---")
print(corr_matrix.round(3))
~~~

### 3. Key Takeaways & Practical Recommendations

- **Use Correlation for Standardized Comparison:** Pearson correlation (`.corr()`) is generally more useful than unscaled covariance (`.cov()`) when comparing relationships between variables with different units.

- **Compare Mean and Median to Detect Skewness:** When a distribution is positively skewed and the mean is noticeably greater than the median, the median can provide a more robust representation of central tendency.

- **Use Correlation Matrices for Multivariate Analysis:** Running `df.corr()` helps identify relationships between numerical features and can reveal highly correlated predictors.

- **Watch for Multicollinearity:** Very high absolute correlation between predictor variables (for example, `|r| > 0.8`) can indicate potential multicollinearity and may require further investigation before applying certain machine learning models.

- **Correlation Does Not Imply Causation:** A strong correlation between two variables indicates a statistical association, but it does not prove that one variable causes the other.

### 4. Key Takeaways

- Univariate analysis focuses on understanding one variable at a time.
- Bivariate analysis examines the relationship between two variables.
- Multivariate analysis studies interactions among three or more variables.
- Covariance indicates the direction of joint variation between two variables.
- Pearson correlation standardizes the relationship between variables to a range of -1 to +1.
- Skewness helps identify whether a distribution is symmetric, positively skewed, or negatively skewed.
- Comparing mean and median provides useful insight into the shape of a distribution.
- `.corr()` generates a correlation matrix for numerical features.
- High correlations between independent variables may indicate multicollinearity.
- Statistical correlation should not be interpreted as proof of causation.

### 5. Learning Outcome

By the end of Day 14, I learned how to perform univariate, bivariate, and multivariate analysis using Pandas and NumPy. I practiced measuring distribution skewness, comparing mean and median, calculating covariance and Pearson correlation, and generating correlation matrices to understand relationships between numerical features. I also learned how correlation can support exploratory analysis and help identify potential multicollinearity issues in data science workflows.
