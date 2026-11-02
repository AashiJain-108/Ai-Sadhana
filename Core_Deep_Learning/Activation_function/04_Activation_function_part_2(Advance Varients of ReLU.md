## Variants of ReLU

Based on Linear and Non-Linear structures:
* **Linear:** Leaky ReLU & Parametric ReLU
* **Non-Linear:** Exponential Linear Unit (ELU) & Scaled Exponential Linear Unit (SELU)

---

### 1. Leaky ReLU
<img width="425" height="401" alt="image" src="https://github.com/user-attachments/assets/60bda0ad-156f-4fce-9da4-261fc0a029bf" />

* **Function:** 
  `Leaky_ReLU(x) = max(α * x, x)` *(where α = 0.01)*  
  Mathematical: $\text{Leaky\_ReLU}(x) = \max(\alpha x, x)$

* **Derivative:** 
  `Derivative = α if x < 0, else 1`  
  Mathematical: $\frac{\partial \text{Leaky\_ReLU}(x)}{\partial x} = \begin{cases} \alpha & \text{if } x < 0 \\ 1 & \text{if } x > 0 \end{cases}$

* **Advantages:** Non-saturating, fast to compute, avoids the dying ReLU problem, and output is close to zero-centered.

---

### 2. Parametric ReLU (PReLU)
Same as Leaky ReLU, but $\alpha$ is not a fixed hyperparameter ($0.01$). Instead, it is treated as a learnable parameter optimized via backpropagation based on the data.

* **Function:** $\text{PReLU}(x) = \max(\alpha x, x)$

* **Derivatives:**
  * **With respect to input ($x$):** $\frac{\partial f(x)}{\partial x} = \begin{cases} \alpha & \text{if } x < 0 \\ 1 & \text{if } x > 0 \end{cases}$
  * **With respect to the learnable parameter ($\alpha$):** $\frac{\partial f(x)}{\partial \alpha} = \begin{cases} x & \text{if } x < 0 \\ 0 & \text{if } x > 0 \end{cases}$

* **Advantages:** Gives the model extra flexibility, often outperforming standard Leaky ReLU.

---

### 3. Exponential Linear Unit (ELU)
<img width="455" height="596" alt="image" src="https://github.com/user-attachments/assets/054b0f9b-70fe-4733-b9ab-c0bf0e591341" />

* **Function:** 
  $f(x) = \begin{cases} x & \text{if } x > 0 \\ \alpha(e^x - 1) & \text{if } x \le 0 \end{cases}$

* **Derivative:** 
  $\frac{\partial f(x)}{\partial x} = \begin{cases} 1 & \text{if } x > 0 \\ f(x) + \alpha & \text{if } x \le 0 \end{cases}$

* **Advantages:**
  * Smooth curve for negative inputs.
  * Pushing the mean activations closer to zero (zero-centered), which speeds up convergence.
  * Solves the Dying ReLU problem.
  * Continuous and differentiable everywhere.

* **Disadvantage:**
  * Slightly more computationally expensive due to the exponential term ($e^x$).

---

### 4. Scaled Exponential Linear Unit (SELU)
Similar to ELU, but scaled by a multiplier $\lambda$ ($\lambda > 1$):

$f(x) = \lambda \begin{cases} x & \text{if } x > 0 \\ \alpha(e^x - 1) & \text{if } x \le 0 \end{cases}$

* **Key Feature:**
  * Self-normalizing. If you use SELU, the network layers automatically normalize themselves (mean $\approx 0$, variance $\approx 1$), which leads to extremely fast training and convergence.

* **Disadvantage:**
  * Relatively new, complex mathematical proofs, and not yet widely adopted across all industry architectures.

---

### 5. Maxout Neuron
* Computes $\max(w_1^T x + b_1, w_2^T x + b_2)$, generalizing ReLU and Leaky ReLU, but doubles the number of parameters per unit.
* **Key Features:** No saturation, NO death.
