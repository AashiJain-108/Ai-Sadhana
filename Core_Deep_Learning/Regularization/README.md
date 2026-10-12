# Regularization

**Definition:** Regularization is a technique used to reduce overfitting by constraining a model's learning, helping it generalize to unseen data.

| Technique | How it works | Main purpose |
|---|---|---|
| L1 (Lasso) | Adds $\lambda\sum_i\|w_i\|$ to the loss | Encourages sparse weights; can perform feature selection |
| L2 (Ridge) | Adds $\lambda\sum_i w_i^2$ to the loss | Shrinks large weights |
| Elastic Net | Combines L1 and L2 | Balances sparsity and weight shrinkage |
| Dropout | Randomly drops activations during training | Reduces reliance on particular neurons |
| Early stopping | Stops when validation performance ceases to improve | Prevents excessive fitting to training data |
| Data augmentation | Creates varied training examples | Improves robustness to relevant input variations |
| Weight tying | Shares parameters across network components | Reduces independent parameters and constrains learning |

### The mathematical connection

$$
\boxed{J(\theta)=L_{\text{data}}(\theta)+\lambda R(\theta)}
$$

For L2 regularization:

$$
J(\theta)=L_{\text{recon}}+\lambda\sum_i w_i^2
$$

- $L_{\text{recon}}$: how accurately the autoencoder reconstructs its input.
- $R(\theta)$: the regularization penalty.
- $\lambda$: controls the strength of the penalty.

One distinction to remember: L1/L2 explicitly penalize parameters, whereas dropout, early stopping, and data augmentation work through different mechanisms. Batch normalization and layer normalization primarily normalize activations; any regularizing effect they provide is indirect and context-dependent.

# Regularization in Machine Learning

## 1. The basic intuition

Imagine a student preparing for an exam.

- Overfitting: The student memorizes practice questions but cannot solve new questions.
- Regularization: The student is encouraged to learn the important patterns instead of relying on overly complicated solutions.
- Generalization: The student performs well on questions they have never seen before.

Regularization adds a penalty for model complexity to the original training loss.

$$
\boxed{J(w)=L_{\text{data}}(w)+\lambda R(w)}
$$

- $L_{\text{data}}$: How wrong the model's predictions are.
- $R(w)$: Penalty that discourages certain parameter values.
- $\lambda$: Controls how strongly the penalty matters.

Remember: the model minimizes the combined objective, not just prediction error.

## 2. Three main types of regularization

### L1

**Lasso Regression**

$$
J=\text{MSE}+\lambda\sum_j|w_j|
$$

- Penalizes the absolute values of coefficients.
- Can make some coefficients exactly zero.
- Useful for feature selection.
- Analogy: removes unnecessary items from a school bag.

### L2

**Ridge Regression**

$$
J=\text{MSE}+\lambda\sum_jw_j^2
$$

- Penalizes the squares of coefficients.
- Usually shrinks coefficients toward zero, but not exactly to zero.
- Helps stabilize models, especially with correlated features.
- Analogy: reduces the volume of every item in the bag instead of removing items.

### L1 + L2

**Elastic Net**

$$
J=\text{MSE}+\lambda\left[(1-r)\sum_j|w_j|+r\sum_jw_j^2\right]
$$

- Combines L1 and L2 penalties.
- Can select features while also shrinking coefficients.
- $r=0$: Ridge-like; $r=1$: Lasso-like, using this formula's convention.
- Analogy: removes unnecessary items and reduces the size of the remaining items.

Important: In scikit-learn's `ElasticNet`, the mixing parameter is named `l1_ratio`. It corresponds to $r$ in the formula above. The overall regularization strength is called `alpha` in scikit-learn, whereas $\lambda$ is commonly used in mathematical notes.

## 3. Visual comparison of coefficients

Suppose a model learns these coefficients:

| Feature | Before regularization | Lasso | Ridge |
|---|---:|---:|---:|
| House size | 8.0 | 6.5 | 6.8 |
| Number of rooms | 3.0 | 0 | 2.2 |
| Wall colour | 0.2 | 0 | 0.1 |

Illustrative values only, not output from the article's code.

- Lasso: Can eliminate features by setting coefficients to zero.
- Ridge: Shrinks coefficients but generally retains them.
- Elastic Net: Combines both behaviours.

A zero coefficient means that feature contributes nothing through that coefficient in the fitted linear model; it does not automatically prove the feature is useless in every possible model.

- Too little regularization: Risk of overfitting.
- Too much regularization: Risk of underfitting.
- Goal: Good performance on unseen data, not merely low training error.
