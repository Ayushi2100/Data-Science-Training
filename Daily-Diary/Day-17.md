# Day 17: Fundamentals of Data Visualization with Matplotlib

- **Date:** July 16, 2026 (Thursday)
- **Module / Focus:** Matplotlib Object-Oriented Interface, Canvas Setup, Axis Labeling, Bar Charts, Line Charts, and Scatter Plots
- **Tools Used:** Python 3, Matplotlib, Pandas, Jupyter Notebook

### 1. In-Depth Technical Breakdown & Theoretical Foundations

#### Matplotlib Architecture: State-Based (`pyplot`) vs. Object-Oriented (`Axes`)

- **State-Based Interface (`plt.plot`):** Uses Matplotlib's current active figure and axes automatically. It is convenient for simple visualizations but can become difficult to manage when working with multiple plots or complex layouts.

- **Object-Oriented Interface (`fig, ax = plt.subplots()`):** Explicitly creates a Figure object and one or more Axes objects. The Figure represents the complete visualization canvas, while an Axes object represents an individual plotting area containing its own axes, labels, title, ticks, and legends.

- **Advantages of the OO Approach:** The object-oriented approach provides greater control, flexibility, and maintainability, especially when creating multiple charts or reusable visualization functions.

#### Chart Types & Analytical Applications

- **Bar Charts (`ax.bar` / `ax.barh`):** Used to compare numerical values across discrete categories. They are useful for analyzing quantities such as revenue by product category.

- **Line Charts (`ax.plot`):** Used to visualize trends across an ordered or continuous dimension, particularly time-series data such as daily or monthly revenue.

- **Scatter Plots (`ax.scatter`):** Display individual observations using two numerical variables. They are useful for identifying relationships, trends, clusters, and potential outliers between variables.

#### Figure Aesthetics & Customization

- **Canvas Setup:** `plt.subplots(figsize=(width, height))` controls the dimensions of the visualization and helps produce appropriately sized charts for notebooks, reports, and presentations.

- **Axis Labels & Titles:** `ax.set_xlabel()`, `ax.set_ylabel()`, and `ax.set_title()` provide context and make visualizations easier to interpret.

- **Legends & Gridlines:** `ax.legend()` identifies plotted data series, while gridlines can make numerical comparisons easier.

- **Layout Management:** `plt.tight_layout()` automatically adjusts spacing to reduce overlapping labels and improve the final appearance of the chart.

### 2. Comprehensive Code Implementation & Step-by-Step Execution

~~~python
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np

# ---------------------------------------------------------
# 1. Dataset Initialization
# ---------------------------------------------------------

# Synthetic sales and product performance data
dates = pd.date_range(
    start='2026-07-01',
    periods=10,
    freq='D'
)

daily_revenue = [
    1200, 1500, 1100, 1800, 2100,
    1900, 2300, 2500, 2200, 2700
]

categories = [
    'Electronics',
    'Accessories',
    'Footwear',
    'Apparel',
    'Home'
]

category_revenue = [
    8500, 3200, 5400, 4100, 6300
]

prices = np.array([
    15, 25, 45, 120, 200,
    350, 500, 750, 1100, 1500
])

item_revenue = np.array([
    150, 300, 450, 1440, 2000,
    2800, 3500, 4500, 5500, 6000
])


# ---------------------------------------------------------
# 2. Line Chart: Daily Revenue Trend
# ---------------------------------------------------------

fig, ax = plt.subplots(figsize=(8, 4))

ax.plot(
    dates,
    daily_revenue,
    marker='o',
    linewidth=2,
    label='Daily Revenue'
)

ax.set_title(
    'Daily Revenue Trend (July 2026)',
    fontsize=12,
    fontweight='bold'
)

ax.set_xlabel('Date', fontsize=10)
ax.set_ylabel('Revenue ($)', fontsize=10)

ax.grid(True)
ax.legend(loc='upper left')

plt.xticks(rotation=45)
plt.tight_layout()
plt.show()


# ---------------------------------------------------------
# 3. Bar Chart: Categorical Revenue Comparison
# ---------------------------------------------------------

fig, ax = plt.subplots(figsize=(8, 4))

bars = ax.bar(
    categories,
    category_revenue,
    edgecolor='black'
)

ax.set_title(
    'Revenue Breakdown by Product Category',
    fontsize=12,
    fontweight='bold'
)

ax.set_xlabel('Product Category', fontsize=10)
ax.set_ylabel('Total Revenue ($)', fontsize=10)

ax.grid(axis='y')

# Add value labels on top of each bar
for bar in bars:
    height = bar.get_height()

    ax.annotate(
        f'${height}',
        xy=(
            bar.get_x() + bar.get_width() / 2,
            height
        ),
        xytext=(0, 3),
        textcoords='offset points',
        ha='center',
        va='bottom',
        fontsize=9
    )

plt.tight_layout()
plt.show()


# ---------------------------------------------------------
# 4. Scatter Plot: Price vs. Revenue Relationship
# ---------------------------------------------------------

fig, ax = plt.subplots(figsize=(8, 4))

ax.scatter(
    prices,
    item_revenue,
    s=60,
    alpha=0.9,
    edgecolors='k'
)

ax.set_title(
    'Price vs. Revenue Distribution',
    fontsize=12,
    fontweight='bold'
)

ax.set_xlabel('Unit Price ($)', fontsize=10)
ax.set_ylabel('Generated Revenue ($)', fontsize=10)

ax.grid(True)

plt.tight_layout()
plt.show()
~~~

### 3. Key Takeaways & Practical Recommendations

- **Adopt the Object-Oriented Approach Early:** Prefer `fig, ax = plt.subplots()` when creating structured visualizations because it provides better control over figures and axes.

- **Match Chart Type to Analytical Intent:** Use line charts for trends over ordered intervals, bar charts for categorical comparisons, and scatter plots for relationships between numerical variables.

- **Use Clear Labels:** Always provide meaningful titles, x-axis labels, and y-axis labels so that the visualization can be understood without additional explanation.

- **Use Legends When Necessary:** Legends are useful when a chart contains multiple data series or when plotted elements need identification.

- **Improve Layout with `plt.tight_layout()`:** Calling `plt.tight_layout()` helps prevent labels, titles, and tick values from overlapping or being cut off.

- **Avoid Unnecessary Decoration:** Visualization should emphasize the underlying data rather than excessive styling. A clean chart is generally easier to interpret.

### 4. Key Takeaways

- Matplotlib is a widely used Python library for creating static data visualizations.
- The object-oriented interface provides explicit control over Figure and Axes objects.
- `plt.subplots()` can be used to create a Figure and Axes for structured plotting.
- Line charts are useful for identifying trends, especially in time-series data.
- Bar charts are effective for comparing discrete categorical values.
- Scatter plots help analyze relationships between two numerical variables.
- Axis labels and titles provide essential context for interpreting charts.
- Legends help identify different data series within a visualization.
- Gridlines can improve readability when comparing numerical values.
- `plt.tight_layout()` improves chart spacing and prevents overlapping elements.
- Choosing the appropriate chart type is an important part of effective exploratory data analysis.

### 5. Learning Outcome

By the end of Day 17, I learned the fundamentals of data visualization using Matplotlib. I practiced creating line charts for time-based trends, bar charts for categorical comparisons, and scatter plots for numerical relationships. I also learned how to use the object-oriented Matplotlib interface, customize chart labels and titles, add legends and gridlines, and manage figure layouts. This session helped me understand how visualizations can convert numerical data into clear and interpretable analytical insights.
