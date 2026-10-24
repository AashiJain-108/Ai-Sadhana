# Activation Function

> **Disclaimer:** Study this after the [Universal Approximation Theorem](#) for better understanding.

**What was the need of activation function in neural network (Why activation function)?**

### Intuition building:

suppose I have a **Linear Network**

Here , I have actually learned from mitesh sir to ask one simple but powerful question genuinely - **"What would happen if depth had no non-linear support?"**

That's exactly what we're going to address by taking the example of a linear network.

<img width="171" height="393" alt="image" src="https://github.com/user-attachments/assets/fc4bfe66-2c83-44e4-96da-c91d73b9c7ba" />

Hypothetically, I replace my non-linear activation function with simple linear transformation (multiplying inputs by weights)

now it is $y = (w_4 * (w_3 * (w_2 * (w_1 x))))$,

chaining of multiple linear layers together means we are just successively multiplying weights & because matrix and scalar multiplications can be combined, this entire chain simplifies into one single combined weight matrix $W$ (where $W = w_4 w_3 w_2 w_1$), resulting in $y = Wx$. 

stacking multiple layers provides no real "depth" or extra computational power. We end up with a network that is functionally no different from a basic, single-layer linear model

<img width="627" height="427" alt="image" src="https://github.com/user-attachments/assets/d01597b8-e9dd-429d-9a8c-6073b9cf7eeb" />

**Linear Decision Boundaries:** Without non-linearities, a network can only learn linear decision boundaries (like perceptrons), making it impossible to solve complex, non-linearly separable problems (such as concentric circles or separated clusters requiring curves/ellipses).
and if you ask me how I am like are you guys even understanding my discussion about linear and non linear functions

---
**linear models** can only draw **flat lines, planes, or hyperplanes to separate classes**.

and if my data as in image 2 is distributed in complex ways like concentric circles, interlaced spirals, or separated clusters , a straight line cannot possibly separate the red points from the blue points and you need a boundary that curves, bends, and wraps around the data. --Then its a **Failure Case**

for **non-linear activation functions**, the network **stretches, twists, and folds** the input space.

---
- Why Did I Give the Disclaimer About the **Universal Approximation Theorem**?

I mentioned studying the Universal Approximation Theorem (UAT) before this topic. Why?

Because the UAT provides the theoretical foundation for this capability.

It states that a feedforward neural network with a suitable non-linear activation function can approximate any continuous function on a compact domain to any desired degree of accuracy, provided it has enough neurons in its hidden layer.

In simple words, a neural network can approximate incredibly complex functions if it has the right architecture and enough neurons.

That's the mathematical guarantee behind its approximation capability.

--- 
**Conclusion:** This simply proves that depth alone is useless without non-linearities.

### Reference/Sources 

Mitesh M. Khapra Sir deep learning course freely available on youtube
(
Deep Learning(CS7015): Lec 9.3 Better activation functions)

Images used for illustration also comes from sir course only. I hold no copyright and just used for explanation remove if required
