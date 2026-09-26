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

> "Machines don't learn. What a typical 'learning machine' does is find a mathematical formula which, when applied to a collection of inputs (called 'training data'), produces the desired output."

— Andriy Burkov, *The Hundred-Page Machine Learning Book*

### What does this actually mean?

The word **"learning"** can make machine learning sound similar to human learning. But technically, an ML model does something much
more specific.

A learning algorithm takes training data and uses it to determine or adjust the parameters of a mathematical model.

In simplified form:

Training Data
      ↓
Learning Algorithm
      ↓
Parameter Adjustment
      ↓
Trained Model
      ↓
Prediction on New Data

**Data → Algorithm → Learned Parameters/Structure → Model → Prediction**

### Source

Andriy Burkov, *The Hundred-Page Machine Learning Book*
