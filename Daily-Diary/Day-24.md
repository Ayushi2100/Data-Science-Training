# Day 24: Regression Model Evaluation Metrics

- **Date:** July 27, 2026 (Monday)
- **Module / Focus:** Regression Model Evaluation, Residual Analysis, MAE, MSE, RMSE, R² Score, and Model Diagnostics
- **Tools Used:** Python 3, Pandas, NumPy, Matplotlib, Scikit-Learn (`sklearn.metrics`), Jupyter Notebook

### 1. In-Depth Technical Breakdown & Theoretical Foundations

#### Understanding Residual Errors

- **Residual Error:** A residual represents the difference between the actual target value and the value predicted by the regression model.

  $$e_i = y_i - \hat{y}_i$$

  where:
  - `eᵢ` = residual error
  - `yᵢ` = actual value
  - `ŷᵢ` = predicted value

- A positive residual means the model **underestimated** the actual value, while a negative residual means the model **overestimated** it.

#### Mean Absolute Error (MAE)

- **Definition:** MAE calculates the average absolute difference between actual and predicted values.

  $$MAE = \frac{1}{n}\sum_{i=1}^{n}|y_i-\hat{y}_i|$$

- **Characteristics:**
  - Easy to interpret.
  - Expressed in the same units as the target variable.
  - Gives equal linear importance to each prediction error.
  - Less sensitive to extreme outliers than MSE and RMSE.

- **Example:** If MAE is `8`, the model's predictions are off by approximately 8 target units on average.

#### Mean Squared Error (MSE)

- **Definition:** MSE calculates the average squared difference between actual and predicted values.

  $$MSE = \frac{1}{n}\sum_{i=1}^{n}(y_i-\hat{y}_i)^2$$

- **Characteristics:**
  - Penalizes large errors more heavily because residuals are squared.
  - Useful when large prediction errors are particularly undesirable.
  - Its units are squared compared with the original target units.
  - Highly sensitive to outliers.

#### Root Mean Squared Error (RMSE)

- **Definition:** RMSE is the square root of MSE.

  $$RMSE = \sqrt{\frac{1}{n}\sum_{i=1}^{n}(y_i-\hat{y}_i)^2}$$

- **Characteristics:**
  - Retains the outlier sensitivity of MSE.
  - Returns the metric to the original target units.
  - Often easier to communicate to stakeholders than MSE.
  - Lower RMSE generally indicates better predictive performance.

#### Coefficient of Determination (R² Score)

- **Definition:** R² measures how much of the variation in the target variable is explained by the regression model compared with a baseline that always predicts the mean.

  $$R^2 = 1-\frac{\sum(y_i-\hat{y}_i)^2}{\sum(y_i-\bar{y})^2}$$

  where:
  - `ŷᵢ` = predicted value
  - `yᵢ` = actual value
  - `ȳ` = mean of actual target values

- **Interpretation:**
  - `R² = 1.0` → Perfect predictions.
  - `R² = 0.0` → Model performs like the mean-prediction baseline.
  - `R² < 0` → Model performs worse than the mean baseline on the evaluated data.

- **Important:** R² should not be interpreted as a percentage of predictions that are correct. It measures explained variation relative to a baseline.

#### Comparing Regression Metrics

- **MAE:** Best when straightforward average error in target units is important.
- **MSE:** Useful when large errors need to be penalized strongly.
- **RMSE:** Useful when large errors matter and the result should remain in the original target units.
- **R²:** Useful for understanding how much target variation the model explains.

### 2. Comprehensive Code Implementation & Step-by-Step Execution

    import pandas as pd
    import numpy as np
    import matplotlib.pyplot as plt
    from sklearn.model_selection import train_test_split
    from sklearn.linear_model import LinearRegression
    from sklearn.metrics import (
        mean_squared_error,
        mean_absolute_error,
        r2_score
    )

    # ---------------------------------------------------------
    # 1. Dataset Generation
    # ---------------------------------------------------------
    np.random.seed(42)
    n_samples = 300

    advertising = np.random.uniform(5, 100, size=n_samples)
    store_locations = np.random.randint(1, 10, size=n_samples)

    # Generate random noise
    noise = np.random.normal(0, 12, size=n_samples)

    # Generate continuous target variable
    sales = (
        (2.4 * advertising)
        + (15.8 * store_locations)
        + 100
        + noise
    )

    df = pd.DataFrame({
        'Advertising_Spend': advertising,
        'Store_Locations': store_locations,
        'Sales': sales
    })

    print("--- Base Dataset Preview ---")
    print(df.head())


    # ---------------------------------------------------------
    # 2. Feature and Target Separation
    # ---------------------------------------------------------
    X = df[['Advertising_Spend', 'Store_Locations']]
    y = df['Sales']


    # ---------------------------------------------------------
    # 3. Train-Test Partitioning
    # ---------------------------------------------------------
    X_train, X_test, y_train, y_test = train_test_split(
        X,
        y,
        test_size=0.20,
        random_state=42
    )

    print("\nTraining Set Shape:", X_train.shape)
    print("Testing Set Shape:", X_test.shape)


    # ---------------------------------------------------------
    # 4. Model Training
    # ---------------------------------------------------------
    model = LinearRegression()

    model.fit(X_train, y_train)

    print("\nLinear Regression model training completed.")


    # ---------------------------------------------------------
    # 5. Generate Predictions
    # ---------------------------------------------------------
    y_pred = model.predict(X_test)

    print("\n--- Sample Actual vs Predicted Values ---")

    results_df = pd.DataFrame({
        'Actual_Sales': y_test.values,
        'Predicted_Sales': y_pred
    })

    print(results_df.head(10))


    # ---------------------------------------------------------
    # 6. Calculate Regression Evaluation Metrics
    # ---------------------------------------------------------
    mae = mean_absolute_error(y_test, y_pred)

    mse = mean_squared_error(y_test, y_pred)

    rmse = np.sqrt(mse)

    r2 = r2_score(y_test, y_pred)

    print("\n--- Regression Performance Diagnostics ---")
    print(f"Mean Absolute Error (MAE):      {mae:.2f}")
    print(f"Mean Squared Error (MSE):       {mse:.2f}")
    print(f"Root Mean Squared Error (RMSE): {rmse:.2f}")
    print(f"R² Score:                       {r2:.4f}")


    # ---------------------------------------------------------
    # 7. Residual Error Calculation
    # ---------------------------------------------------------
    residuals = y_test - y_pred

    print("\n--- Residual Statistics ---")
    print(f"Mean Residual: {residuals.mean():.2f}")
    print(f"Minimum Residual: {residuals.min():.2f}")
    print(f"Maximum Residual: {residuals.max():.2f}")


    # ---------------------------------------------------------
    # 8. Residual Distribution Visualization
    # ---------------------------------------------------------
    fig, ax = plt.subplots(figsize=(7, 4.5))

    ax.hist(
        residuals,
        bins=20,
        edgecolor='black',
        alpha=0.7
    )

    # Reference line at zero residual
    ax.axvline(
        0,
        linestyle='--',
        linewidth=1.5,
        label='Zero Error Line'
    )

    ax.set_title(
        'Residual Error Distribution',
        fontsize=12,
        fontweight='bold'
    )

    ax.set_xlabel('Residual Error (Actual - Predicted)')
    ax.set_ylabel('Frequency')

    ax.grid(
        True,
        linestyle=':',
        alpha=0.6
    )

    ax.legend()

    plt.tight_layout()
    plt.show()


### 3. Key Takeaways & Practical Recommendations

- **Understand Residuals First:** Residuals represent the prediction errors of a regression model. Analyzing them helps identify systematic problems that a single performance score may hide.

- **Use MAE for Easy Interpretation:** MAE expresses the average prediction error directly in the same units as the target variable and is relatively robust to individual extreme errors.

- **Use RMSE When Large Errors Matter:** RMSE penalizes large residuals more strongly than MAE while remaining in the original target units.

- **Compare MAE and RMSE:** If RMSE is substantially larger than MAE, the model may contain some unusually large prediction errors or outliers.

- **Use R² Alongside Error Metrics:** R² provides information about explained variation, while MAE, MSE, and RMSE describe prediction error. No single metric provides a complete picture.

- **Inspect Residual Distributions:** Ideally, residuals should be reasonably centered around zero without strong systematic patterns. Noticeable skewness, extreme values, or structure can indicate model limitations.

- **Do Not Rely Only on R²:** A high R² does not necessarily mean the model is suitable for every business or prediction task. Always consider the magnitude and practical consequences of prediction errors.

- **Evaluate on Unseen Data:** Regression metrics should be calculated on a test set that was not used to train the model so that the reported performance better reflects its expected generalization.
