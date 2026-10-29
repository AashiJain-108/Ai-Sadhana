## Types of Activation Funtion

1. **Sigmoid Activation Function**

Graph & Range: Squashes inputs into a range between 0 and 1.

<img width="437" height="331" alt="image" src="https://github.com/user-attachments/assets/d275bf93-ae41-4eb2-aa3a-a90387eea60d" />

**input range = [0,1]**
<img width="192" height="78" alt="image" src="https://github.com/user-attachments/assets/b3b9e618-2af6-4c8a-8d22-beca7e3f3077" />


**Key Properties**

• **Output Range:** Between 0 and 1 (ideal for Binary Classification based probabilities (yes/no) or(0/1)).
• **Shape:** Continuous, smooth, and S-shaped.
• **Midpoint:** At $x = 0 $, the function outputs 0.5.
• **Derivative:** $\(\sigma'(x) = \sigma(x) \cdot (1 - \sigma(x))\)$

- **Problems with Sigmoid Function:**
**A. Vanishing Gradient Problem due to Saturation:**
 - **Saturation:** When a neuron's input is very large (positive or negative), the sigmoid function flattens out near $0$ or $1$, where its gradient $\sigma(x)(1 - \sigma(x))$ drops close to $0$.
 - **Stalled Training:** During backpropagation, if neurons saturate, their gradients vanish to zero. This means weights stop updating, and training completely stalls.
   i.e $$w = w - \eta \Delta w$$ here $$Delta w$$ stops updating and remains 0 ie no new learning
- **Cause:** High weight initialization causes weighted sums to become very large right from the start so when they are backpropagated and derivative is found it comes smaller and smaller nearly to 0 causing neurons to saturate and stop learning.

- *Question that might have raised :* why only high weights considered cause not high inputs
- *Answer :* because inputs are normalized from the start its assumed 
- **B. Not Zero Centered**
