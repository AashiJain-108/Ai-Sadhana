A **feature** is an **input variable(x) or input column** in a machine learning dataset that helps predict the target variable(y).

**Feature Selection** is the process of selecting the most relevant and important features from the available input features while removing unnecessary or less useful ones.

**Why Do We Need Feature Selection?**
| Reason | Benefit |
| :--- | :--- |
| **Curse of Dimensionality** | Avoids unnecessary high-dimensional data |
| **Computational Complexity** | Reduces computation and memory requirements |
| **Interpretability** | Makes model decisions easier to understand |

curse of dimensionity reason : data sparsity

Consider representing data points in different dimensions:
- 1D: Points lie on a line.
- 2D: Points occupy a plane.
- 3D: Points occupy a volume.
- 100D: Data occupies a very high-dimensional space.
If the number of observations remains limited while dimensions increase, the data becomes increasingly sparse.

This creates problems such as:
- Distance measurements becoming less informative.
- Difficulty identifying meaningful patterns.
- Increased complexity in learning relationships.
- Greater requirements for training data.
Important: High-dimensional data can make distance-based algorithms particularly difficult to use effectively.


Interpretability means understanding why a machine learning model produces a particular prediction.

There are two important concepts:
Concept	Meaning	Example
Prediction	Predicting an outcome for new data	Predicting tomorrow's stock price
Inference	Understanding relationships and factors behind an outcome	Understanding why a customer's loan was rejected

### Types of Feature Selection Techniques

1. Filter Methods

Use statistical measures to evaluate features independently of a machine learning model.

2. Wrapper Methods

Evaluate different feature subsets by training and testing a machine learning model.

3. Embedded Methods

Perform feature selection as part of the model training process.

| Technique | Purpose |
| :--- | :--- |
| **Variance Threshold** | Removes features with very low variance |
| **Correlation** | Identifies highly correlated features |
| **ANOVA** | Evaluates differences between feature means across target classes |
| **Chi-Square Test** | Evaluates relationships between categorical variables |
| **Mutual Information** | Measures statistical dependence between features and target |

## Feature Selection vs Feature Extraction
| Feature Selection | Feature Extraction |
| :--- | :--- |
| Selects existing features | Creates new transformed features |
| Original feature meanings are retained | New features may be harder to interpret |
| Removes unnecessary columns | Transforms original information |
| **Example:** Variance Threshold | **Example:** PCA |

Feature selection chooses the best existing features, whereas feature extraction generates new features from the existing data.


**Why Must Feature Selection Be Applied Only on Training Data?**

Data leakage occurs when information from the testing dataset influences the training process.

If we calculate feature-selection statistics using the complete dataset before splitting, information from the test set indirectly influences which features are selected.

This can result in overly optimistic model evaluation.
