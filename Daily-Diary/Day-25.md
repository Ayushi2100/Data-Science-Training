# Day 25: Logistic Regression — Classification Theory, Probability & Model Training

- **Date:** July 28, 2026 (Tuesday)
- **Module / Focus:** Binary Classification, Sigmoid Function, Log-Odds, Decision Boundaries, Logistic Regression Training, Probability Prediction, and Classification Workflow
- **Tools Used:** Python 3, Scikit-Learn (`sklearn`), Pandas, NumPy, Matplotlib, Jupyter Notebook

---

## 1. In-Depth Technical Breakdown & Theoretical Foundations

### Understanding Logistic Regression

Despite its name, **Logistic Regression is primarily a classification algorithm**, not a regression algorithm.

It is commonly used when the target variable contains two classes, such as:

- `0` = No / Negative
- `1` = Yes / Positive

Examples include:

- Customer will purchase or not
- Employee will leave or stay
- Loan will default or not
- Email is spam or not

The model first calculates a linear combination of the input features and then passes that value through a **Sigmoid (Logistic) function** to convert it into a probability between 0 and 1.

### Linear Component

The initial linear score is:

$$
z = w_0 + w_1x_1 + w_2x_2 + \dots + w_nx_n
$$

where:

- $w_0$ = intercept
- $w_1, w_2, \dots, w_n$ = learned feature coefficients
- $x_1, x_2, \dots, x_n$ = input features

Unlike linear regression, this value is not directly treated as the final prediction.

### Sigmoid Function

The linear score is transformed using the sigmoid function:

$$
\sigma(z) = \frac{1}{1 + e^{-z}}
$$

The sigmoid function maps any real-valued input into the range:

$$
0 < \sigma(z) < 1
$$

This allows the output to be interpreted as a probability.

For example:

- Probability = `0.90` → strong likelihood of class `1`
- Probability = `0.20` → strong likelihood of class `0`
- Probability = `0.50` → boundary between the two classes

### Converting Probability into a Class

A common classification threshold is `0.5`.

$$
\hat{y} =
\begin{cases}
1 & \text{if } P(y=1|X) \geq 0.5 \\
0 & \text{if } P(y=1|X) < 0.5
\end{cases}
$$

The threshold does not have to be 0.5 in every real-world application. It can be adjusted depending on whether false positives or false negatives are more costly.

### Log-Odds Interpretation

Logistic Regression models the **log-odds** of the positive class as a linear function of the input features:

$$
\log\left(\frac{p}{1-p}\right)
=
w_0 + w_1x_1 + \dots + w_nx_n
$$

This gives the coefficients an important interpretation.

A positive coefficient generally means that increasing that feature increases the likelihood of the positive class, while a negative coefficient generally decreases it, assuming other features remain constant.

### Decision Boundary

The **decision boundary** is the point where the predicted probability is exactly 0.5.

Since:

$$
\sigma(z)=0.5
$$

when:

$$
z=0
$$

the decision boundary is:

$$
w_0+w_1x_1+w_2x_2+\dots+w_nx_n=0
$$

For two features, this boundary can be visualized as a line separating the two predicted classes.

### Model Training

Logistic Regression does not minimize ordinary Mean Squared Error like basic linear regression.

Instead, it commonly uses **log loss (cross-entropy loss)** to measure how well predicted probabilities match the actual class labels.

For binary classification:

$$
LogLoss =
-\frac{1}{n}
\sum_{i=1}^{n}
\left[
y_i\log(p_i)
+
(1-y_i)\log(1-p_i)
\right]
$$

The optimization process learns coefficients that minimize this loss.

---

## 2. Comprehensive Code Implementation & Step-by-Step Execution

    import pandas as pd
    import numpy as np
    import matplotlib.pyplot as plt

    from sklearn.model_selection import train_test_split
    from sklearn.linear_model import LogisticRegression
    from sklearn.metrics import accuracy_score

    # ---------------------------------------------------------
    # 1. Dataset Generation
    # ---------------------------------------------------------
    np.random.seed(42)
    n_samples = 300

    # Generate customer-related features
    age = np.random.randint(18, 65, size=n_samples)
    income = np.random.randint(20000, 120000, size=n_samples)

    # Generate a probability influenced by age and income
    score = (
        0.05 * age
        + 0.00002 * income
        - 2.0
    )

    probability = 1 / (1 + np.exp(-score))

    # Generate binary target
    # 1 = Purchased
    # 0 = Not Purchased
    purchased = (
        np.random.rand(n_samples) < probability
    ).astype(int)

    df = pd.DataFrame({
        'Age': age,
        'Income': income,
        'Purchased': purchased
    })

    print("--- Dataset Preview ---")
    print(df.head())

    print("\n--- Target Distribution ---")
    print(df['Purchased'].value_counts())


    # ---------------------------------------------------------
    # 2. Feature and Target Separation
    # ---------------------------------------------------------
    X = df[['Age', 'Income']]
    y = df['Purchased']


    # ---------------------------------------------------------
    # 3. Train-Test Partitioning
    # ---------------------------------------------------------
    X_train, X_test, y_train, y_test = train_test_split(
        X,
        y,
        test_size=0.20,
        random_state=42,
        stratify=y
    )

    print("\nTraining Set Shape:", X_train.shape)
    print("Testing Set Shape: ", X_test.shape)


    # ---------------------------------------------------------
    # 4. Logistic Regression Model Training
    # ---------------------------------------------------------
    model = LogisticRegression(random_state=42)

    # Train the classifier
    model.fit(X_train, y_train)

    print("\nModel training completed.")


    # ---------------------------------------------------------
    # 5. Extract Model Parameters
    # ---------------------------------------------------------
    print("\n--- Learned Model Parameters ---")
    print("Coefficients:", model.coef_)
    print("Intercept:", model.intercept_)


    # ---------------------------------------------------------
    # 6. Class Prediction
    # ---------------------------------------------------------
    y_pred = model.predict(X_test)

    accuracy = accuracy_score(y_test, y_pred)

    print("\n--- Classification Performance ---")
    print(f"Accuracy: {accuracy * 100:.2f}%")


    # ---------------------------------------------------------
    # 7. Probability Prediction
    # ---------------------------------------------------------
    y_probability = model.predict_proba(X_test)

    results_df = pd.DataFrame({
        'Actual': y_test.values,
        'Predicted': y_pred,
        'Probability_Class_0': y_probability[:, 0],
        'Probability_Class_1': y_probability[:, 1]
    })

    print("\n--- Sample Probability Predictions ---")
    print(results_df.head(10))


    # ---------------------------------------------------------
    # 8. Visualizing Actual vs Predicted Classes
    # ---------------------------------------------------------
    fig, ax = plt.subplots(figsize=(8, 5))

    ax.scatter(
        X_test['Age'],
        y_test,
        alpha=0.6,
        label='Actual'
    )

    ax.scatter(
        X_test['Age'],
        y_pred,
        marker='x',
        alpha=0.7,
        label='Predicted'
    )

    ax.set_title(
        'Logistic Regression: Actual vs Predicted Classes',
        fontsize=12,
        fontweight='bold'
    )

    ax.set_xlabel('Age', fontsize=10)
    ax.set_ylabel('Purchased Class', fontsize=10)

    ax.set_yticks([0, 1])
    ax.set_yticklabels([
        'Not Purchased (0)',
        'Purchased (1)'
    ])

    ax.legend()
    ax.grid(True, linestyle='--', alpha=0.5)

    plt.tight_layout()
    plt.show()

## 3. Key Takeaways & Practical Recommendations

- **Remember that Logistic Regression is a classification algorithm:** It predicts class probabilities and converts them into class labels.

- **Understand the Sigmoid Function:** The sigmoid function converts the model's linear output into a probability between 0 and 1.

- **Use `predict_proba()` when probabilities matter:** `predict()` returns class labels, while `predict_proba()` provides the probability of belonging to each class.

- **Understand the classification threshold:** A default threshold of 0.5 is common, but real-world applications may require a different threshold depending on the cost of false positives and false negatives.

- **Interpret coefficients carefully:** Positive coefficients generally increase the log-odds of the positive class, while negative coefficients decrease them, holding other features constant.

- **Use `stratify=y` during splitting:** This helps preserve the proportion of each class in both training and testing datasets.

- **Do not evaluate only with accuracy:** Accuracy is useful as a basic metric, but Precision, Recall, F1-score, and the Confusion Matrix provide a much more complete picture of classification performance.

- **Logistic Regression is an important baseline model:** It is relatively simple, interpretable, and often provides a strong starting point before moving to more complex classification algorithms.
