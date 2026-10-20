# What is Machine Learning(ML)?
Machine learning is a branch of artificial intelligence (AI) that gives computers the ability to learn from data and improve their performance without being explicitly programmed. It allows machines to identify patterns, make decisions, even predict future trends-all by learning from experience, much like humans do.

# Typical Machine Learning Workflow

A typical ML project can be thought of as a sequence of stages:

1. **Define the problem**
   Understand what problem needs to be solved and what value an ML solution could provide.

2. **Collect the data**
  Identify sources of data(both primary and seconday data sources) and create a data lake(an integrated dataset from different resources)

4. **Prepare the data**
   Pre-process or Clean data for missing or incorrect data, Generate derived variable through feature engineering, and transform the data when necessary.

5. **Split the data**
   Divide the available dataset into appropriate subsets, such as training and validation data.

6. **Train and evaluate models**
   Build different ML models and compare their performance on validation data to determine which approach works well.

7. **Deploy the solution**
   Put the selected model into practical use, such as integrating it into a product, application, or decision-making system.

# How Machines Learn

## A Different Way to Think About "Learning"

To understand how machines learn, we first need to understand how data, algorithms, and models come together to make machine learning possible.

> "Machines don't learn. What a typical 'learning machine' does is find a mathematical formula which, when applied to a collection of inputs (called 'training data'), produces the desired output."

— Andriy Burkov, *The Hundred-Page Machine Learning Book*

### What does this actually mean?

The word **"learning"** can make machine learning sound similar to human learning. But technically, an ML model does something much
more specific.

A learning algorithm takes training data and uses it to determine or adjust the parameters of a mathematical model.

In simplified form:

**Training Data → Learning Algorithm → Parameter Adjustment → Trained Model → Prediction on New Data**

### Source

Andriy Burkov, *The Hundred-Page Machine Learning Book*

# Instance-Based Learning vs. Model-Based Learning

## 1. Introduction

Machine Learning algorithms can be categorized according to how they learn from training data and use that knowledge to make predictions on unseen data.

Two important approaches are:

1. **Instance-Based Learning**
2. **Model-Based Learning**

The fundamental difference lies in how each approach represents the knowledge acquired from data.

- **Instance-Based Learning** retains training examples and uses their similarity to make predictions.
- **Model-Based Learning** learns a generalized representation, such as a mathematical function, a set of rules, or a decision structure, and uses it to make predictions.

Both approaches aim to generalize beyond the training data. However, they differ in their learning process, storage requirements, computational costs, and prediction mechanisms.

---

## 2. Instance-Based Learning

### Definition

Instance-Based Learning is a machine learning approach in which an algorithm retains training examples and uses their similarity to previously observed examples to predict the output of a new input.

Instead of explicitly fitting a single global function during training, it typically postpones much of the computation until a prediction is required.

It is also known as **memory-based learning** and is commonly associated with **lazy learning**.

### How Does It Work?

The general workflow is:

1. Collect and preprocess the training dataset.
2. Store the training examples, possibly using a suitable indexing structure.
3. Receive a new input instance.
4. Measure its similarity or distance from stored examples.
5. Select relevant examples and use them to generate a prediction.

### Example: K-Nearest Neighbors (KNN)

Suppose a college wants to predict whether a student will get placed using two features:

- IQ
- CGPA

The training dataset contains students whose placement outcomes are already known.

When a new student arrives, KNN calculates the distances between the new student and the stored examples. It selects the \(k\) nearest neighbors and predicts the class using their labels, commonly through majority voting.

For example, if \(k=5\) and three of the five nearest students were placed, KNN predicts that the new student belongs to the placement class.

For numerical features, Euclidean distance is one possible distance measure:
$$
\[
d(x,z)=\sqrt{\sum_{j=1}^{m}(x_j-z_j)^2}
\]
$$

Here:

- $$\(x\)$$ is the new input.
- $$\(z\)$$ is a stored training instance.
- $$\(m\)$$ is the number of features.
- $$\(d(x,z)\)$$ measures the distance between the two instances.

The choice of distance measure and feature scaling can significantly influence the result.

### Characteristics

- Training often requires relatively little computation beyond storing or indexing examples.
- Prediction involves retrieving and comparing relevant training instances.
- The training data, or a suitable subset of it, generally remains part of the predictive system.
- Predictions can adapt to local patterns in the dataset.
- Memory requirements can increase as the training dataset grows.
- Prediction can become expensive when many examples must be examined.

### Advantages

- Simple to understand and implement.
- Can represent complex, nonlinear decision boundaries.
- Does not require fitting a specific global parametric function.
- New examples can sometimes be incorporated without retraining a global model.

### Limitations

- May require substantial memory.
- Prediction can be slow for large datasets.
- Performance depends on the distance or similarity measure.
- Irrelevant features, inconsistent feature scales, noise, and high dimensionality can reduce effectiveness.
- Retaining more examples does not automatically guarantee better predictions.

### Common Examples

- K-Nearest Neighbors (KNN)
- Case-Based Reasoning
- Locally Weighted Regression

---

## 3. Model-Based Learning

### Definition

Model-Based Learning is a machine learning approach in which an algorithm learns a representation of patterns or relationships from training data and uses that learned representation to make predictions on unseen inputs.

The representation may be a mathematical function, a decision tree, a set of rules, or a more complex model.

The objective is to learn a model that captures useful regularities in the training data and generalizes to new examples.

This approach is commonly associated with **eager learning**, because the algorithm constructs or fits a model before using it for prediction.

### How Does It Work?

The general workflow is:

1. Collect and preprocess the training dataset.
2. Select a suitable model family and learning algorithm.
3. Train the algorithm on the available data.
4. Learn the model's parameters or structure.
5. Evaluate the model on suitable validation or test data.
6. Use the trained model to predict outcomes for new inputs.

### Example: Logistic Regression

Consider the same student placement problem, using IQ and CGPA to predict whether a student will get placed.

Logistic Regression learns coefficients from the training data and uses them to estimate the probability of a binary outcome.

A simplified mathematical representation is:
$$\[
z=w_1x_1+w_2x_2+b
\]$$

$$\[
P(y=1\mid x)]=\frac{1}{1+e^{-z}}
\$$
Here:

- $$\(x_1,x_2\)$$ are input features.
- $$\(w_1,w_2\)$$ are learned weights.
- $$\(b\)$$ is the bias or intercept.
- $$\(P(y=1\mid x)\)$$ is the estimated probability of the positive class.

A decision threshold can then convert the probability into a class prediction.

After training, the system can use the learned coefficients to predict outcomes without needing to search through every original training example.

The original data may still be retained for auditing, retraining, or monitoring, but it is not ordinarily required for each prediction by a standard logistic regression model.

### Characteristics

- Requires a training procedure to learn the model.
- Stores a learned representation of the training data.
- Prediction uses the learned model rather than necessarily comparing the input with stored examples.
- Can provide fast predictions when the trained model is compact.
- Performance depends on the model family, its assumptions, training procedure, and data quality.
- May require retraining or updating when the underlying data distribution changes.

### Advantages

- Often supports efficient predictions after training.
- Can provide a compact representation of learned knowledge.
- Can scale well to large numbers of predictions, depending on the model.
- Some models provide interpretable coefficients or decision rules.
- Can learn reusable patterns that apply across many unseen inputs.

### Limitations

- Training may require considerable time and computational resources.
- An unsuitable model family may fail to capture important patterns.
- Model complexity and regularization must be managed to avoid underfitting or overfitting.
- Changes in the underlying data distribution may require model updates or retraining.
- A compact model is not guaranteed; some trained models can be large and expensive to run.

### Common Examples

- Linear Regression
- Logistic Regression
- Decision Trees
- Neural Networks

Support Vector Machines can also be model-based, although kernel SVMs may retain training examples or support vectors for prediction. Therefore, not every algorithm fits a simple storage-based distinction perfectly.

---

## 4. Fundamental Differences

| Basis | Instance-Based Learning | Model-Based Learning |
|---|---|---|
| Core idea | Uses stored training examples | Uses a learned model or representation |
| Learning objective | Relies on relationships between a query and relevant examples | Learns a reusable representation of patterns in the data |
| Training phase | Often relatively inexpensive | Fits parameters or model structure |
| Prediction phase | Compares the query with stored examples | Evaluates the trained model |
| Computation | Often shifts more computation to prediction time | Often performs more computation during training |
| Storage | May retain many or all training examples | Stores the learned model; may be compact or large |
| Prediction speed | Can be slow for large datasets | Often fast for compact models |
| Generalization | Often local and query-dependent | Encoded in the learned representation |
| Model updates | May incorporate new examples directly, depending on the algorithm | May require parameter updates or retraining |
| Interpretability | Depends on the examples, similarity measure, and prediction method | Depends on the model family |
| Main challenge | Efficient retrieval, memory, and meaningful similarity | Learning a suitable model that generalizes well |
| Example | K-Nearest Neighbors | Logistic Regression |

**Important:** These are typical tendencies rather than universal rules. For example, an instance-based system can use efficient indexing, and a large neural network can require substantial memory and computation during inference.

---

## 5. Lazy Learning vs. Eager Learning

These terms are closely associated with the two approaches.

### Lazy Learning

A lazy learner postpones much of its learning or computation until a query needs to be answered.

For example, a basic KNN implementation can store the training data and calculate distances when a new instance arrives.

### Eager Learning

An eager learner constructs a predictive model from the training data before it receives a prediction request.

For example, Logistic Regression estimates its coefficients during training and subsequently uses those coefficients to make predictions.

| Aspect | Lazy Learning | Eager Learning |
|---|---|---|
| Typical association | Instance-based | Model-based |
| When much of the work occurs | At prediction time | During training |
| Stored knowledge | Training examples | Learned representation |
| Example | KNN | Logistic Regression |

The terms describe common learning strategies, not strict definitions that apply to every algorithm.

---

## 6. Understanding the Difference Through an Analogy

Imagine two students preparing for a mathematics examination.

**Student A: Memorization**

Student A remembers many solved problems. When encountering a new problem, they search for a similar example and use it as a guide.

This resembles Instance-Based Learning: the prediction depends on relevant stored examples.

**Student B: Understanding the principles**

Student B studies the underlying mathematical relationships and learns how to apply them. When a new problem appears, they use those principles to solve it.

This resembles Model-Based Learning: the prediction uses a learned representation of the underlying relationships.

This analogy illustrates the central idea, although actual machine learning algorithms do not understand concepts in the same way humans do.

---

## 7. When Should Each Approach Be Used?

### Instance-Based Learning Can Be Suitable When:

- Local similarity is informative for the task.
- The dataset is manageable in terms of memory and prediction cost.
- A flexible, non-parametric method is desirable.
- New examples need to be incorporated without repeatedly fitting a global model.

### Model-Based Learning Can Be Suitable When:

- Predictions must be made efficiently at scale.
- A reusable predictive function is desirable.
- The training data contains patterns that a suitable model can capture.
- A compact representation is beneficial for deployment.

Neither approach is universally superior. The appropriate choice depends on dataset size, data quality, feature representation, computational constraints, prediction latency, and the evaluation results.

---

## 8. Important Clarifications

1. **Instance-based learning is not simply copying answers.** Algorithms such as KNN use a defined similarity measure and an aggregation rule to make predictions.

2. **Model-based learning does not always mean learning a straight line.** Models can be linear, nonlinear, rule-based, tree-based, or neural.

3. **Instance-based learning can generalize.** It generalizes using similarities between unseen inputs and stored examples.

4. **Model-based learning does not always use less memory.** Compact regression models may use little storage, whereas large neural networks can require substantial resources.

5. **Training-data retention is not the same as data preprocessing.** Both approaches may need missing-value handling, encoding, feature selection, and scaling.

6. **These approaches are not the same as supervised versus unsupervised learning.** Supervision describes the kind of learning signal available; instance-based versus model-based learning describes how knowledge is represented and used. The categories address different aspects of machine learning.

---
## References

1. [Scikit-learn: Nearest Neighbors](https://scikit-learn.org/stable/modules/neighbors.html) — documentation on instance-based nearest-neighbor methods.
2. [Tom M. Mitchell, *Machine Learning*, Chapter 8: Instance-Based Learning](https://nkapila.me/masters/mitchell) — foundational discussion of instance-based learning and delayed generalization.
3. https://medium.com/@mahendrakumar24325/instance-based-learning-vs-model-based-learning-a-clear-and-practical-guide-c0445ee81fab
4. https://www.kaggle.com/discussions/getting-started/179177
5. Gpt-5 (OpenAI product for refining thoughts into structure)

# Types of Machine Learning 
<img width="802" height="337" alt="image" src="https://github.com/user-attachments/assets/a1ff8831-c492-41ce-bb0e-f3697f281303" />

<img width="822" height="472" alt="image" src="https://github.com/user-attachments/assets/7c099c21-dcb5-474c-8b25-a251298b9f97" />

### Reference/Sources
CBSE XI Artificial Intelligence Student Handbook
