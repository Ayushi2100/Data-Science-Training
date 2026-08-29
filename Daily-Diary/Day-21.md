# Day 21: Introduction to Machine Learning with Scikit-Learn

- **Date:** July 22, 2026 (Wednesday)
- **Module / Focus:** Machine Learning Workflow Fundamentals, Scikit-Learn Estimator API, Dataset Splitting, Decision Tree Classification, and Model Evaluation
- **Tools Used:** Python 3, Scikit-Learn (`sklearn`), Pandas, NumPy, Jupyter Notebook

### 1. In-Depth Technical Breakdown & Theoretical Foundations

#### Machine Learning Taxonomy & Workflow Pipeline

- **Supervised Learning Paradigms:** Supervised learning trains models using labeled data `(X, y)` to learn the relationship between input features (`X`) and a target variable (`y`). Classification predicts discrete categories or class labels, while regression predicts continuous numerical values.

- **Typical Machine Learning Workflow:** A basic supervised learning workflow consists of data preparation, feature-target separation, train-test splitting, model selection, model training, prediction, and performance evaluation.

- **Dataset Partitioning (`train_test_split`):** Splits the available dataset into a training set and a testing set. The training data (`X_train`, `y_train`) is used to learn patterns, while the testing data (`X_test`, `y_test`) evaluates how well the trained model generalizes to unseen observations.

- **Reproducibility with `random_state`:** Setting a fixed `random_state` ensures that the same random partition is generated each time the code is executed, making experiments reproducible.

#### The Scikit-Learn Estimator API Design

- **Consistent Object-Oriented Interface:** Scikit-Learn provides a standardized API that makes different machine learning algorithms work in a similar manner.

- **Model Instantiation:** A model object is created by selecting an estimator and specifying its hyperparameters. For example:
  `DecisionTreeClassifier(max_depth=3)`

- **Model Fitting (`.fit(X, y)`):** The `.fit()` method trains the model using the provided training features and corresponding target values.

- **Inference / Prediction (`.predict(X)`):** After training, `.predict()` generates predictions for new or unseen feature observations.

- **Hyperparameters vs. Learned Parameters:** Hyperparameters such as `max_depth` are specified before training, while the model learns its internal parameters from the training data during `.fit()`.

#### Decision Tree Classifier Mechanics

- **Recursive Feature Splitting:** A Decision Tree divides the feature space into smaller regions using a sequence of decision rules. Each internal node represents a condition on a feature, while leaf nodes represent the final predicted class.

- **Splitting Criteria:** Decision Trees commonly use measures such as **Gini Impurity** or **Entropy / Information Gain** to determine which feature and threshold provide the most useful split.

- **Overfitting Control:** A tree with unlimited depth can continue splitting until it memorizes the training data, resulting in poor generalization. Hyperparameters such as `max_depth` restrict tree complexity and help reduce overfitting.

#### Classification Accuracy

- **Accuracy (`accuracy_score`):** Measures the proportion of correctly classified observations out of all observations:

  **Accuracy = Number of Correct Predictions / Total Number of Predictions**

- Accuracy is useful when the classes are reasonably balanced. For highly imbalanced datasets, additional metrics such as precision, recall, F1-score, and the confusion matrix should also be considered.

### 2. Comprehensive Code Implementation & Step-by-Step Execution

```python
import pandas as pd
import numpy as np

from sklearn.model_selection import train_test_split
from sklearn.tree import DecisionTreeClassifier
from sklearn.metrics import accuracy_score


# ---------------------------------------------------------
# 1. Dataset Generation
#    Synthetic Classification Data
# ---------------------------------------------------------
np.random.seed(42)
n_samples = 300

# Synthetic customer purchase decision dataset
age = np.random.randint(18, 65, size=n_samples)

income = np.random.randint(
    20000,
    120000,
    size=n_samples
)

browsing_score = np.random.uniform(
    1.0,
    10.0,
    size=n_samples
)

# Rule-based target variable:
# Purchased = 1
# Not Purchased = 0
target = (
    ((age > 30) & (income > 50000))
    | (browsing_score > 7.0)
).astype(int)

df = pd.DataFrame({
    'Age': age,
    'Income': income,
    'Browsing_Score': browsing_score,
    'Purchased': target
})

print("--- Initial Dataset Preview ---")
print(df.head())


# ---------------------------------------------------------
# 2. Feature/Target Separation
#    & Train-Test Partitioning
# ---------------------------------------------------------
X = df[['Age', 'Income', 'Browsing_Score']]
y = df['Purchased']

# Split dataset into:
# 80% training data
# 20% testing data
X_train, X_test, y_train, y_test = train_test_split(
    X,
    y,
    test_size=0.20,
    random_state=42,
    stratify=y
)

print(f"\nTraining set shape: {X_train.shape}")
print(f"Testing set shape:  {X_test.shape}")


# ---------------------------------------------------------
# 3. Model Instantiation & Training
# ---------------------------------------------------------
# Create a Decision Tree Classifier
# max_depth limits the complexity of the tree
model = DecisionTreeClassifier(
    max_depth=3,
    random_state=42
)

# Train the model using training data
model.fit(X_train, y_train)

print("\nModel fitting complete.")


# ---------------------------------------------------------
# 4. Prediction & Performance Evaluation
# ---------------------------------------------------------
# Generate predictions on unseen test data
y_pred = model.predict(X_test)

# Calculate classification accuracy
accuracy = accuracy_score(
    y_test,
    y_pred
)

print("\n--- Baseline Model Evaluation ---")
print(f"Test Accuracy Score: {accuracy * 100:.2f}%")


# ---------------------------------------------------------
# 5. Actual vs Predicted Values
# ---------------------------------------------------------
results_df = pd.DataFrame({
    'Actual': y_test.values,
    'Predicted': y_pred
})

print("\n--- Sample Predictions vs Ground Truth ---")
print(results_df.head(10))
```

### 3. Key Takeaways & Practical Recommendations

- **Always Partition Data Before Training:** Use `train_test_split()` before fitting the model so that the testing data remains unseen during training. This helps provide a more realistic estimate of model performance.

- **Use `random_state` for Reproducibility:** Setting a fixed random seed ensures that experiments can be repeated with the same train-test partition and model configuration.

- **Control Decision Tree Complexity:** Hyperparameters such as `max_depth` help prevent decision trees from becoming unnecessarily complex and overfitting the training data.

- **Use `stratify=y` for Classification:** Passing `stratify=y` preserves approximately the same target-class proportions in both the training and testing datasets.

- **Understand the Scikit-Learn Workflow:** Most Scikit-Learn estimators follow a simple pattern: instantiate the model, call `.fit()` for training, and call `.predict()` for inference.

- **Do Not Rely Only on Accuracy:** Accuracy alone may be misleading when classes are imbalanced. For real-world classification problems, evaluate additional metrics such as precision, recall, F1-score, and the confusion matrix.

- **Treat the Test Set as Unseen Data:** The test dataset should not influence model training or hyperparameter decisions. Keeping it isolated helps prevent data leakage and provides a more reliable estimate of generalization performance.
