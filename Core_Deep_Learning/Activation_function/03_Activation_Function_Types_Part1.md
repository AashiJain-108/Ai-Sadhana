## Types of Activation Funtion

1. **Sigmoid Activation Function**

Graph & Range: Squashes inputs into a range between 0 and 1.

<img width="437" height="331" alt="image" src="https://github.com/user-attachments/assets/d275bf93-ae41-4eb2-aa3a-a90387eea60d" />

**input range = [0,1]**
<img width="192" height="78" alt="image" src="https://github.com/user-attachments/assets/b3b9e618-2af6-4c8a-8d22-beca7e3f3077" />


**Key Properties**

- **Output Range:** Between 0 and 1 (ideal for Binary Classification based probabilities (yes/no) or(0/1)).
- **Shape:** Continuous, smooth, and S-shaped.
- **Midpoint:** At $x = 0 $, the function outputs 0.5.
- **Derivative:** $\(\sigma'(x) = \sigma(x) \cdot (1 - \sigma(x))\)$

- **Problems with Sigmoid Function:**

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

**C. Computationally Expensive**
Computing exponentials ($\exp(x)$) makes sigmoid operations slow.  
