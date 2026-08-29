# Day 22: Feature Scaling & Categorical Encoding

- **Date:** July 23, 2026 (Thursday)
- **Module / Focus:** Feature Standardization, Data Leakage Prevention, One-Hot Encoding, Label Encoding, and Preprocessing for Machine Learning
- **Tools Used:** Python 3, Pandas, NumPy, Scikit-Learn (`sklearn`), Jupyter Notebook

### 1. In-Depth Technical Breakdown & Theoretical Foundations

#### Feature Scaling & Standardization

- **Why Feature Scaling is Important:** Machine learning datasets often contain numerical features with very different ranges. For example, Age may range from 18–65, while Income may range from 25,000–120,000. Algorithms that rely on distances or numerical magnitudes can give excessive importance to features with larger values.

- **StandardScaler:** The `StandardScaler` from Scikit-Learn transforms numerical features so that they are centered around a mean of approximately 0 with a standard deviation of approximately 1.

- **Z-Score Standardization:** The transformation is represented as:

  $$z = \frac{x-\mu}{\sigma}$$

  where:
  - `x` = original feature value
  - `μ` = mean of the training feature
  - `σ` = standard deviation of the training feature
  - `z` = standardized value

- **Important Consideration:** Standardization does not remove the original relationships within the data. It only changes the numerical scale of the features.

#### Data Leakage Prevention

- **Understanding Data Leakage:** Data leakage occurs when information from the test dataset is unintentionally used during model training or preprocessing. This can produce overly optimistic evaluation results.

- **Correct Scaling Workflow:**
  1. Split the dataset into training and testing sets.
  2. Fit the scaler only on `X_train`.
  3. Transform `X_train` using `.fit_transform()`.
  4. Transform `X_test` using `.transform()`.
  5. Never calculate scaling parameters independently from the test dataset.

- **Why This Matters:** The test dataset should simulate completely unseen future data. Allowing its statistical information to influence preprocessing compromises the validity of model evaluation.

#### Categorical Feature Encoding

- **Why Encoding is Required:** Most machine learning algorithms require numerical input. Categorical text values such as `"Sales"`, `"Engineering"`, and `"Marketing"` therefore need to be converted into numerical representations.

- **One-Hot Encoding (`pd.get_dummies()`):** One-hot encoding creates a separate binary column for each category. It is appropriate for nominal variables where categories do not have a meaningful numerical order.

  Example:

  `Department = Sales, Engineering, Marketing`

  can become:

  `Department_Engineering`
  
  `Department_Marketing`

  with the remaining category represented by the dropped reference column when `drop_first=True` is used.

- **Label Encoding (`LabelEncoder`):** Label encoding converts categories into integer labels such as `0`, `1`, and `2`. It is most appropriate for encoding target variables or categories where numerical ordering is meaningful.

- **Important Distinction:** Arbitrarily assigning numbers such as `0 = Sales`, `1 = Engineering`, and `2 = Marketing` to a nominal feature can make some algorithms incorrectly interpret the categories as ordered. Therefore, one-hot encoding is generally safer for nominal input features.

### 2. Comprehensive Code Implementation & Step-by-Step Execution

    import pandas as pd
    import numpy as np
    from sklearn.model_selection import train_test_split
    from sklearn.preprocessing import StandardScaler, LabelEncoder

    # ---------------------------------------------------------
    # 1. Synthetic Dataset Creation
    # ---------------------------------------------------------
    np.random.seed(42)
    n_samples = 200

    data = {
        'Age': np.random.randint(18, 65, size=n_samples),
        'Income': np.random.randint(25000, 120000, size=n_samples),
        'Department': np.random.choice(
            ['Sales', 'Engineering', 'Marketing'],
            size=n_samples
        ),
        'Performance_Tier': np.random.choice(
            ['Low', 'Medium', 'High'],
            size=n_samples
        ),
        'Promoted': np.random.choice(
            ['No', 'Yes'],
            size=n_samples
        )
    }

    df = pd.DataFrame(data)

    print("--- Initial Dataset ---")
    print(df.head())


    # ---------------------------------------------------------
    # 2. One-Hot Encoding for Nominal Feature
    # ---------------------------------------------------------
    # Department has no inherent numerical ordering,
    # so one-hot encoding is appropriate.

    df_encoded = pd.get_dummies(
        df,
        columns=['Department'],
        drop_first=True
    )

    print("\n--- Dataset After One-Hot Encoding ---")
    print(df_encoded.head())


    # ---------------------------------------------------------
    # 3. Label Encoding for Target Variable
    # ---------------------------------------------------------
    # Convert Promoted values:
    # No  -> 0
    # Yes -> 1

    label_enc = LabelEncoder()

    df_encoded['Promoted'] = label_enc.fit_transform(
        df_encoded['Promoted']
    )

    print("\n--- Dataset After Label Encoding ---")
    print(df_encoded.head())


    # ---------------------------------------------------------
    # 4. Feature and Target Separation
    # ---------------------------------------------------------
    X = df_encoded.drop(
        columns=['Promoted', 'Performance_Tier']
    )

    y = df_encoded['Promoted']

    print("\nFeature Columns:")
    print(X.columns)

    print("\nTarget Preview:")
    print(y.head())


    # ---------------------------------------------------------
    # 5. Train-Test Split
    # ---------------------------------------------------------
    # Split the data BEFORE fitting the scaler
    # to prevent data leakage.

    X_train, X_test, y_train, y_test = train_test_split(
        X,
        y,
        test_size=0.20,
        random_state=42,
        stratify=y
    )

    print("\nTraining Set Shape:", X_train.shape)
    print("Testing Set Shape:", X_test.shape)


    # ---------------------------------------------------------
    # 6. Feature Standardization
    # ---------------------------------------------------------
    scaler = StandardScaler()

    numerical_cols = ['Age', 'Income']

    X_train_scaled = X_train.copy()
    X_test_scaled = X_test.copy()

    # Fit scaler ONLY on training data
    # and transform training data.

    X_train_scaled[numerical_cols] = scaler.fit_transform(
        X_train[numerical_cols]
    )

    # Use the parameters learned from X_train
    # to transform X_test.

    X_test_scaled[numerical_cols] = scaler.transform(
        X_test[numerical_cols]
    )


    # ---------------------------------------------------------
    # 7. Inspect Standardized Features
    # ---------------------------------------------------------
    print("\n--- Standardized Training Features ---")
    print(X_train_scaled[numerical_cols].head())

    print("\n--- Training Data Statistics ---")
    print(
        f"Age Mean: {X_train_scaled['Age'].mean():.2f}"
    )
    print(
        f"Age Std: {X_train_scaled['Age'].std():.2f}"
    )
    print(
        f"Income Mean: {X_train_scaled['Income'].mean():.2f}"
    )
    print(
        f"Income Std: {X_train_scaled['Income'].std():.2f}"
    )


### 3. Key Takeaways & Practical Recommendations

- **Scale Features After Splitting:** Always divide the dataset into training and testing sets before fitting `StandardScaler`. This prevents information from the test set from leaking into the training process.

- **Use `fit_transform()` Only on Training Data:** `fit_transform()` learns the mean and standard deviation from the training data and then performs the transformation.

- **Use `transform()` on Test Data:** The test dataset must be transformed using the parameters learned from the training dataset. Never fit the scaler separately on test data.

- **Use One-Hot Encoding for Nominal Features:** `pd.get_dummies()` is suitable for unordered categorical variables such as Department, City, or Product Category.

- **Use Label Encoding Carefully:** `LabelEncoder` is primarily intended for target variables. Avoid using arbitrary integer labels for nominal input features because they may introduce a false sense of ordering.

- **Scaling Depends on the Algorithm:** Algorithms such as KNN, K-Means, SVM, PCA, and many gradient-based models can be sensitive to feature scale. Tree-based algorithms such as Decision Trees and Random Forests generally do not require feature scaling.

- **Think About the Complete Preprocessing Pipeline:** In real machine learning projects, scaling and encoding should be treated as part of the preprocessing pipeline so that the same transformations are consistently applied to training, validation, and future unseen data.
