# Day 23: Linear Regression — Theory, Mathematical Foundation & Model Validation

- **Date:** July 24, 2026 (Friday)
- **Module / Focus:** Ordinary Least Squares (OLS), Linear Regression Mathematics, Model Coefficients, Prediction, and Model Validation
- **Tools Used:** Python 3, Pandas, NumPy, Matplotlib, Scikit-Learn (`sklearn`), Jupyter Notebook

### 1. In-Depth Technical Breakdown & Theoretical Foundations

#### Mathematical Foundation of Linear Regression

- **Purpose of Linear Regression:** Linear Regression is a supervised learning algorithm used to predict a continuous numerical target variable based on one or more input features.

- **Hypothesis Function:** The model represents the target as a linear combination of input features:

  $$\hat{y} = b + w_1x_1 + w_2x_2 + \dots + w_nx_n$$

  where:
  - `ŷ` = predicted target value
  - `b` = intercept
  - `w₁, w₂, ..., wₙ` = learned feature coefficients
  - `x₁, x₂, ..., xₙ` = input features

- **Interpretation of Coefficients:** A coefficient represents the expected change in the predicted target for a one-unit increase in that feature, while keeping the other features constant.

#### Ordinary Least Squares (OLS)

- **Objective:** Linear Regression using Ordinary Least Squares estimates the model parameters by minimizing the difference between actual and predicted values.

- **Mean Squared Error (MSE):** The basic squared-error objective can be represented as:

  $$MSE = \frac{1}{n}\sum_{i=1}^{n}(y_i-\hat{y}_i)^2$$

  Squaring the errors ensures that positive and negative errors do not cancel each other and gives greater weight to larger errors.

- **Normal Equation:** For a suitable full-rank feature matrix, the optimal coefficient vector can be expressed mathematically as:

  $$\mathbf{w} = (\mathbf{X}^T\mathbf{X})^{-1}\mathbf{X}^T\mathbf{y}$$

  Scikit-Learn's `LinearRegression` handles the underlying numerical optimization automatically.

#### Model Parameters: `coef_` and `intercept_`

- **`model.coef_`:** Stores the learned coefficient for each input feature. The sign indicates the direction of the relationship:
  - Positive coefficient → target tends to increase as the feature increases.
  - Negative coefficient → target tends to decrease as the feature increases.
  - Coefficient near zero → weak linear contribution, although interpretation depends on the scale and other features.

- **`model.intercept_`:** Represents the model's predicted baseline target when all input features are equal to zero.

#### Linearity & Model Assumptions

- **Linearity Assumption:** Linear Regression assumes that the expected target can be adequately represented as a linear combination of the input features.

- **Important Assumptions:** For reliable statistical interpretation, Linear Regression commonly relies on assumptions such as linearity, independent observations, constant error variance (homoscedasticity), and appropriately behaved residuals.

- **Important Limitation:** A high `R²` value does not automatically prove that the relationship is truly linear or that the model is appropriate. Residual analysis and domain knowledge should also be considered.

#### Model Evaluation

- **Mean Squared Error (MSE):** Measures the average squared prediction error. Lower MSE generally indicates better predictive accuracy.

- **R² Score:** Measures the proportion of variation in the target explained by the model relative to a baseline model:

  $$R^2 = 1 - \frac{\sum(y_i-\hat{y}_i)^2}{\sum(y_i-\bar{y})^2}$$

  An `R²` closer to 1 generally indicates that the model explains a larger proportion of the target variability.

### 2. Comprehensive Code Implementation & Step-by-Step Execution

    import pandas as pd
    import numpy as np
    import matplotlib.pyplot as plt
    from sklearn.model_selection import train_test_split
    from sklearn.linear_model import LinearRegression
    from sklearn.metrics import mean_squared_error, r2_score

    # ---------------------------------------------------------
    # 1. Dataset Generation
    # ---------------------------------------------------------
    np.random.seed(42)
    n_samples = 250

    # Generate input features
    unit_price = np.random.uniform(10, 200, size=n_samples)
    quantity = np.random.randint(1, 15, size=n_samples)

    # Generate random noise
    noise = np.random.normal(0, 15, size=n_samples)

    # Create target using a linear relationship
    # Revenue = 1.5 * Unit_Price
    #         + 25 * Quantity
    #         + 50
    #         + random noise

    revenue = (
        (1.5 * unit_price)
        + (25.0 * quantity)
        + 50.0
        + noise
    )

    df = pd.DataFrame({
        'Unit_Price': unit_price,
        'Quantity': quantity,
        'Revenue': revenue
    })

    print("--- Base Dataset Preview ---")
    print(df.head())


    # ---------------------------------------------------------
    # 2. Feature and Target Separation
    # ---------------------------------------------------------
    X = df[['Unit_Price', 'Quantity']]
    y = df['Revenue']


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
    # 4. Model Creation & Training
    # ---------------------------------------------------------
    model = LinearRegression()

    # Fit the Linear Regression model
    model.fit(X_train, y_train)

    print("\nModel training completed.")


    # ---------------------------------------------------------
    # 5. Extract Learned Parameters
    # ---------------------------------------------------------
    learned_coefs = model.coef_
    learned_intercept = model.intercept_

    print("\n--- Learned Model Parameters ---")
    print(
        f"Unit_Price Coefficient: {learned_coefs[0]:.2f}"
    )
    print(
        f"Quantity Coefficient:   {learned_coefs[1]:.2f}"
    )
    print(
        f"Intercept:              {learned_intercept:.2f}"
    )


    # ---------------------------------------------------------
    # 6. Generate Predictions
    # ---------------------------------------------------------
    y_pred = model.predict(X_test)

    print("\n--- Sample Predictions ---")
    results_df = pd.DataFrame({
        'Actual_Revenue': y_test.values,
        'Predicted_Revenue': y_pred
    })

    print(results_df.head(10))


    # ---------------------------------------------------------
    # 7. Model Evaluation
    # ---------------------------------------------------------
    mse = mean_squared_error(y_test, y_pred)
    r2 = r2_score(y_test, y_pred)

    print("\n--- Model Evaluation ---")
    print(f"Mean Squared Error (MSE): {mse:.2f}")
    print(f"R² Score: {r2:.4f}")


    # ---------------------------------------------------------
    # 8. Actual vs Predicted Visualization
    # ---------------------------------------------------------
    fig, ax = plt.subplots(figsize=(7, 5))

    ax.scatter(
        y_test,
        y_pred,
        alpha=0.7,
        edgecolors='black',
        label='Predictions'
    )

    # 45-degree reference line
    min_value = min(y_test.min(), y_pred.min())
    max_value = max(y_test.max(), y_pred.max())

    ax.plot(
        [min_value, max_value],
        [min_value, max_value],
        linestyle='--',
        linewidth=2,
        label='Perfect Prediction'
    )

    ax.set_title(
        'Actual vs Predicted Revenue',
        fontsize=12,
        fontweight='bold'
    )
    ax.set_xlabel('Actual Revenue ($)')
    ax.set_ylabel('Predicted Revenue ($)')
    ax.grid(True, linestyle='--', alpha=0.5)
    ax.legend()

    plt.tight_layout()
    plt.show()


### 3. Key Takeaways & Practical Recommendations

- **Understand the Coefficients:** Use `model.coef_` to understand the direction and magnitude of each feature's relationship with the predicted target.

- **Interpret the Intercept Carefully:** `model.intercept_` represents the predicted baseline when all features are zero, but this value may not always have practical meaning if zero is outside the realistic range of the features.

- **Evaluate with Multiple Metrics:** Use both MSE and `R²` rather than relying on a single metric. MSE focuses on prediction error, while `R²` measures explained variance relative to a baseline.

- **Check the Actual vs Predicted Plot:** Points close to the 45-degree reference line indicate accurate predictions. Systematic patterns or large deviations may indicate model limitations.

- **Do Not Assume High R² Means a Perfect Model:** A strong `R²` does not guarantee causality, correct model assumptions, or good performance on future unseen data.

- **Start with a Simple Baseline:** Linear Regression is an interpretable baseline model. More complex algorithms should be considered only when the data contains relationships that a linear model cannot adequately capture.

- **Validate on Unseen Data:** Always evaluate the final model on data that was not used during training so that its generalization ability can be estimated realistically.
