## Types of Activation Funtion

1. **Sigmoid Activation Function**

Graph & Range: Squashes inputs into a range between 0 and 1.

<img width="437" height="331" alt="image" src="https://github.com/user-attachments/assets/d275bf93-ae41-4eb2-aa3a-a90387eea60d" />

**input range = [0,1]**
<img width="192" height="78" alt="image" src="https://github.com/user-attachments/assets/b3b9e618-2af6-4c8a-8d22-beca7e3f3077" />

* **Function:**
  $$\sigma(x) = \frac{1}{1 + e^{-x}}$$

* **Derivative:**
  $$\frac{\partial \sigma(x)}{\partial x} = \sigma(x)(1 - \sigma(x))$$
  
**Key Properties**

- **Output Range:** Between 0 and 1 (ideal for Binary Classification based probabilities (yes/no) or(0/1)).
- **Shape:** Continuous, smooth, and S-shaped.
- **Midpoint:** At $x = 0 $, the function outputs 0.5.
- **Derivative:** $\(\sigma'(x) = \sigma(x) \cdot (1 - \sigma(x))\)$

  <u>*Problems with Sigmoid Function:*</u>

**A. Vanishing Gradient Problem due to Saturation:**
 - **Saturation:** When a neuron's input is very large (positive or negative), the sigmoid function flattens out near $0$ or $1$, where its gradient $\sigma(x)(1 - \sigma(x))$ drops close to $0$.
 - **Stalled Training:** During backpropagation, if neurons saturate, their gradients vanish to zero. This means weights stop updating, and training completely stalls.
   i.e $$w = w - \eta \Delta w$$ here $Delta w$ stops updating and remains 0 ie no new learning
- **Cause:** High weight initialization causes weighted sums to become very large right from the start so when they are backpropagated and derivative is found it comes smaller and smaller nearly to 0 causing neurons to saturate and stop learning.

- *Question that might have raised :* why only high weights considered cause not high inputs
- *Answer :* because inputs are normalized from the start its assumed
  
**B. Not Zero Centered**

  <img width="903" height="765" alt="image" src="https://github.com/user-attachments/assets/a4fc1a74-5a7b-4c94-8618-ec427265a86a" />
  
- Consider the gradient wrt w1 & w2: 
- $$\nabla w_1 = \frac{\partial \mathcal{L}(\mathbf{w})}{\partial y} \cdot \frac{\partial y}{\partial h_3} \cdot \frac{\partial h_3}{\partial a_3} \cdot h_{21}$$
- $$\nabla w_2 = \frac{\partial \mathcal{L}(\mathbf{w})}{\partial y} \cdot \frac{\partial y}{\partial h_3} \cdot \frac{\partial h_3}{\partial a_3} \cdot h_{22}$$

- here h21 & h22 are between [0,1] (both positive)
- so as h21 & h22 are always positive delta w1 and delta w2 sign depends on common part  $$\frac{\partial \mathcal{L}(\mathbf{w})}{\partial y} \cdot \frac{\partial y}{\partial h_3} \cdot \frac{\partial h_3}{\partial a_3}$$
- so if common term is positive (negative) then $delta w1$ and $delta w2$ are positive(negative) ie all gradients at a given layer tend to have the same sign (all positive or all negative)

**Restricted Updates:** This forces weight updates to follow a constrained "zigzag" path rather than moving directly toward the optimal weights, leading to slower convergence.

 <img width="491" height="426" alt="image" src="https://github.com/user-attachments/assets/2142f94f-ea2e-43cf-b0ad-2a949711e95e" />
 <img width="500" height="396" alt="image" src="https://github.com/user-attachments/assets/8b3cbd1b-e85e-42ee-9a61-adb296d2c50d" />

 **it slows things down:** Because of these zigzag movements ,in a neural network, weights can't update in a direct, straight line toward the optimal values. Weight bounce back and forth in a zigzag motion, wasting computational steps and making the overall training process much slower. ultimately leading to slower convergence.

**C. Computationally Expensive**

Computing exponentials $\exp(x)$ makes sigmoid operations slow.  

2. **tanh Activation Function**

 Graph & Range: Squashes inputs into a range between -1 and 1.
 
<img width="965" height="925" alt="image" src="https://github.com/user-attachments/assets/5fb11766-37c0-4b19-80fc-9da3ed3590d5" />

**input range = [-1,1]**

* **Function:**
  $$\tanh(x) = \frac{e^x - e^{-x}}{e^x + e^{-x}}$$

* **Derivative:**
  $$\frac{\partial \tanh(x)}{\partial x} = 1 - \tanh^2(x)$$

*Advantages:*

**Zero-Centered:** Because its range spans from -1 to 1, its outputs are zero-centered, fixing the directional update problem of Sigmoid and leading to faster training.

<img width="563" height="283" alt="image" src="https://github.com/user-attachments/assets/3ea03239-a326-4f57-9ce4-273c7f2195ef" />

*Disadvantages:*

**Still Saturates:** Like Sigmoid, it flattens out at extremes, meaning it still suffers from the vanishing gradient problem.

Computationally expensive due to exponential calculations.

3. **Rectified Linear Unit (ReLU) Activation Function**

Graph & Range: Outputs $0$ for negative inputs and passes $x$ directly for positive inputs.

<img width="262" height="291" alt="image" src="https://github.com/user-attachments/assets/fbaaa6f1-f8a6-48f5-9bcb-356fafc285d7" />

Non-linearity: Even though it looks like straight lines, combining ReLU units can approximate complex non-linear shapes (like sigmoids).

<img width="497" height="331" alt="image" src="https://github.com/user-attachments/assets/4f58615e-097e-4635-8931-17d458b7ee12" />

*Advantages:*
- Does not saturate in the positive region.  
- Computationally very efficient (just a threshold check). 
- Converges much faster in practice and became the standard for Convolutional Neural Networks (CNNs).

 *Disadvantages:*
 - Not differentiable at $x = 0$ (though handled programmatically in code).
 - Not zero-centered (though techniques like Batch Normalization help resolve this).
 - dying ReLU problem

* **Function:**
  $$\text{ReLU}(x) = \max(0, x)$$

* **Derivative:**
$$\frac{\partial \text{ReLU}(x)}{\partial x}=\begin{cases}0,&\text{if } x < 0 \\ 1, & \text{if } x > 0 \end{cases}$$

  (Note: The derivative at $x = 0$ is technically undefined, but in practice, it is conventionally set to either $0$ or $1$).

### Dying ReLU Problem

**The Dying ReLU problem occurs when a ReLU neuron stops learning because its gradient becomes zero for all training inputs.**

Let's understand why this happens, starting from the weight update formula.

#### 1. Start with Gradient Descent

During training, gradient descent updates a neuron's weight using:

$$
w \leftarrow w - \eta \frac{\partial \mathcal{L}}{\partial w}
$$

Where:
- $w$ = current weight
- $\eta$ = learning rate
- $\frac{\partial \mathcal{L}}{\partial w}$ = gradient of the loss with respect to the weight

**What happens if the gradient becomes zero?**

$$
w_{\text{new}} = w_{\text{old}} - \eta(0)
$$

$$
w_{\text{new}} = w_{\text{old}}
$$

The weight does not change. Gradient descent cannot update it through this gradient.

But why would a neuron's gradient become zero?

#### 2. Trace the Gradient Backward

During backpropagation, the chain rule calculates the gradient by multiplying the derivatives along the computational path.

For a neuron with:

$$
z = wx+b, \qquad f(z)=\max(0,z)
$$

The gradient of the loss with respect to its weight is:

$$
\frac{\partial \mathcal{L}}{\partial w}
=
\frac{\partial \mathcal{L}}{\partial f}
\cdot
\frac{\partial f(z)}{\partial z}
\cdot
\frac{\partial z}{\partial w}
$$

Notice that the gradient is a product of three terms.

**If even one of these terms is zero, the entire product becomes zero.**

This is where ReLU becomes important.

#### 3. The Zero Multiplier: ReLU's Derivative

The ReLU activation function is defined as:

$$
f(z)=\max(0,z)
$$

Its derivative is:

$$
\frac{\partial f(z)}{\partial z}
=
\begin{cases}
0 & \text{if } z<0\\
1 & \text{if } z>0
\end{cases}
$$

At $z=0$, the derivative is undefined mathematically; implementations typically use a derivative of zero.

When $z<0$, ReLU outputs zero and its derivative is also zero.

Substituting this into the backpropagation formula:

$$
\frac{\partial \mathcal{L}}{\partial w}
=
\frac{\partial \mathcal{L}}{\partial f}
\cdot 0 \cdot
\frac{\partial z}{\partial w}
=0
$$

The gradient reaching the neuron's weight becomes zero.

**The result:** Gradient descent cannot update that neuron's weights through this path. Its bias also receives a zero gradient from this neuron for that input.

#### 4. When Does a Neuron Die?

A neuron computes its weighted input as:

$$
z=w_1x_1+w_2x_2+\cdots+w_nx_n+b
$$

The value of $z$ depends on the input, weights, and bias.

If $z<0$, the neuron outputs zero. This is normal behaviour for ReLU and does not, by itself, mean the neuron is dead.

The problem arises when the neuron produces a negative $z$ **for every training input**.

In that case:
- Its ReLU output remains zero.
- Its ReLU derivative remains zero.
- Its gradients with respect to its weights and bias remain zero.
- Gradient descent cannot revive it through ordinary backpropagation.

The neuron has become a *dead ReLU*.

This can happen when weight updates and bias changes push the neuron into a state where its weighted input stays negative across the training data.

#### 5. Why Is This a Problem?

A dead neuron contributes no activation to the next layer for any training input. It also stops learning through the usual gradient-based updates.

Consequently, the network loses a unit that could otherwise learn useful patterns.

If many neurons die, the network's effective capacity to learn can decrease.

However, **there is no universal 50% threshold** beyond which a network stops learning. The impact depends on the network architecture, which neurons have died, and how much useful capacity remains.

#### Key Takeaway

**A ReLU neuron dies when its input stays in the negative region for all training examples, causing its gradient to remain zero and preventing it from learning through ordinary backpropagation.**
