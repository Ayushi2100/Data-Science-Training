# Day 18: Advanced Visualization — Distributions, Outliers & Multi-Panel Dashboards

- **Date:** July 17, 2026 (Friday)
- **Module / Focus:** Histograms, Boxplots, Distribution Analysis, Outlier Detection, and Multi-Panel Layouts (`plt.subplots` Grid System)
- **Tools Used:** Python 3, Matplotlib, NumPy, Pandas, Jupyter Notebook

### 1. In-Depth Technical Breakdown & Theoretical Foundations

#### Distribution & Dispersion Analysis

- **Histograms (`ax.hist`):** Partition continuous numerical data into consecutive, non-overlapping intervals (bins) to visualize frequency distributions, unimodal/bimodal shapes, and skewness. Choosing an optimal bin count is critical: too few bins oversimplify the distribution, while too many create unnecessary noise.

- **Boxplots (`ax.boxplot`):** Summarize data dispersion using a five-number summary: Minimum, First Quartile (Q1 / 25th percentile), Median (Q2 / 50th percentile), Third Quartile (Q3 / 75th percentile), and Maximum.

- **Outlier Quantification:** The Interquartile Range (IQR = Q3 − Q1) sets the boundaries for detecting outliers. Data points falling beyond `Q1 − 1.5 × IQR` or `Q3 + 1.5 × IQR` are considered potential outliers and are plotted as isolated points (fliers), making boxplots an essential tool for visual quality audits.

#### Multi-Panel Executive Dashboard Design

- **Object-Oriented Grid Management (`plt.subplots(nrows, ncols)`):** Returns a Figure object along with an array of Axes objects. Indexing into this array (`axes[0, 0]`, `axes[0, 1]`, etc.) allows multiple plots to be arranged into a single layout.

- **Visual Hierarchy & Formatting:** Combining multiple subplots on a shared canvas requires clear panel titles, meaningful axis labels, consistent formatting, and appropriate spacing. `plt.tight_layout()` helps prevent axis labels and titles from overlapping.

- **Dashboard-Based Analysis:** A multi-panel dashboard allows distributions, categorical comparisons, outliers, and time-based trends to be examined simultaneously, providing a comprehensive view of the dataset.

### 2. Comprehensive Code Implementation & Step-by-Step Execution

    import matplotlib.pyplot as plt
    import pandas as pd
    import numpy as np

    # ---------------------------------------------------------
    # 1. Dataset Setup (Simulating Sales Metrics & Outliers)
    # ---------------------------------------------------------
    np.random.seed(42)

    # Continuous distribution metrics
    customer_ages = np.random.normal(
        loc=35,
        scale=10,
        size=250
    ).astype(int)

    order_values = np.random.exponential(
        scale=150,
        size=250
    ) + 20

    # Add artificial outliers to order values
    order_values = np.append(
        order_values,
        [1200, 1450, 1600, 1800]
    )

    categories = [
        'Electronics',
        'Accessories',
        'Apparel',
        'Home'
    ]

    category_revenue = [
        12500,
        4300,
        6800,
        8900
    ]

    dates = pd.date_range(
        start='2026-07-01',
        periods=10,
        freq='D'
    )

    daily_sales = [
        1200,
        1500,
        1100,
        1800,
        2100,
        1900,
        2300,
        2500,
        2200,
        2700
    ]


    # ---------------------------------------------------------
    # 2. Multi-Panel Executive Dashboard Setup (2x2 Grid)
    # ---------------------------------------------------------
    fig, axes = plt.subplots(
        nrows=2,
        ncols=2,
        figsize=(14, 10)
    )

    fig.suptitle(
        'Executive Sales & Customer Performance Dashboard',
        fontsize=16,
        fontweight='bold'
    )


    # ---------------------------------------------------------
    # Panel 1: Histogram — Customer Age Distribution
    # ---------------------------------------------------------
    axes[0, 0].hist(
        customer_ages,
        bins=15,
        color='#3498db',
        edgecolor='black',
        alpha=0.7
    )

    axes[0, 0].set_title(
        'Customer Age Distribution',
        fontsize=11,
        fontweight='bold'
    )

    axes[0, 0].set_xlabel('Age', fontsize=9)
    axes[0, 0].set_ylabel('Frequency', fontsize=9)

    axes[0, 0].grid(
        axis='y',
        linestyle='--',
        alpha=0.5
    )


    # ---------------------------------------------------------
    # Panel 2: Boxplot — Order Value & Outlier Analysis
    # ---------------------------------------------------------
    axes[0, 1].boxplot(
        order_values,
        vert=False,
        patch_artist=True,
        boxprops=dict(
            facecolor='#9b59b6',
            color='black'
        ),
        flierprops=dict(
            marker='o',
            markerfacecolor='red',
            markersize=6
        )
    )

    axes[0, 1].set_title(
        'Order Value Dispersion & Outliers',
        fontsize=11,
        fontweight='bold'
    )

    axes[0, 1].set_xlabel(
        'Order Value ($)',
        fontsize=9
    )

    axes[0, 1].grid(
        axis='x',
        linestyle='--',
        alpha=0.5
    )


    # ---------------------------------------------------------
    # Panel 3: Bar Chart — Categorical Revenue Breakdown
    # ---------------------------------------------------------
    bars = axes[1, 0].bar(
        categories,
        category_revenue,
        color='#2ecc71',
        edgecolor='black',
        alpha=0.8
    )

    axes[1, 0].set_title(
        'Revenue by Product Category',
        fontsize=11,
        fontweight='bold'
    )

    axes[1, 0].set_xlabel(
        'Category',
        fontsize=9
    )

    axes[1, 0].set_ylabel(
        'Revenue ($)',
        fontsize=9
    )

    axes[1, 0].grid(
        axis='y',
        linestyle='--',
        alpha=0.5
    )

    # Add value labels on bars
    for bar in bars:
        height = bar.get_height()

        axes[1, 0].annotate(
            f'${height}',
            xy=(
                bar.get_x() + bar.get_width() / 2,
                height
            ),
            xytext=(0, 3),
            textcoords="offset points",
            ha='center',
            va='bottom',
            fontsize=8
        )


    # ---------------------------------------------------------
    # Panel 4: Line Chart — Daily Sales Trend
    # ---------------------------------------------------------
    axes[1, 1].plot(
        dates,
        daily_sales,
        marker='s',
        color='#e74c3c',
        linewidth=2,
        label='Trend'
    )

    axes[1, 1].set_title(
        'Daily Revenue Trend',
        fontsize=11,
        fontweight='bold'
    )

    axes[1, 1].set_xlabel(
        'Date',
        fontsize=9
    )

    axes[1, 1].set_ylabel(
        'Sales ($)',
        fontsize=9
    )

    axes[1, 1].grid(
        True,
        linestyle='--',
        alpha=0.5
    )

    axes[1, 1].tick_params(
        axis='x',
        rotation=30
    )


    # ---------------------------------------------------------
    # 3. Finalize Layout Alignment
    # ---------------------------------------------------------
    plt.tight_layout(
        rect=[0, 0, 1, 0.96]
    )

    plt.show()

### 3. Key Takeaways & Practical Recommendations

- **Spot Extreme Values with Boxplots:** Use boxplots to quickly detect skewed data, unusual dispersion, and potential outliers before training machine learning models.

- **Choose the Appropriate Visualization:** Use histograms for understanding numerical distributions, boxplots for dispersion and outlier detection, bar charts for categorical comparisons, and line charts for time-based trends.

- **Structure Layouts with `nrows` and `ncols`:** Using `plt.subplots(2, 2)` creates a clean matrix of subplots, allowing multiple complementary metrics to be displayed in a single dashboard.

- **Highlight Outliers Explicitly:** Customizing `flierprops` helps make extreme observations visually distinguishable during data quality and exploratory analysis.

- **Improve Readability with `plt.tight_layout()`:** Calling `plt.tight_layout()` helps prevent axis labels, titles, and subplot contents from overlapping.

- **Use Dashboards for Decision-Making:** Combining multiple visualization techniques into a single dashboard provides a broader perspective and makes it easier to identify important patterns and relationships.

- **Match Visualization to Analytical Objective:** Selecting the correct chart type is essential for communicating insights effectively and avoiding misleading interpretations.
