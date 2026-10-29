## Qualities of Ideal Activation Function

An ideal activation function should have the following five key characteristics:

**Non-Linear:** Essential for capturing non-linear patterns in data.

**Differentiable:** Must allow derivative calculation so that Gradient Descent and Backpropagation can update weights.

**Computationally Inexpensive:** Fast to compute to ensure training does not become slow.

**Zero-Centered:** Outputs should ideally have a mean around zero (or be normalized), which helps speed up training convergence.

**Non-Saturating:** Should not "squash" inputs into a narrow, flat range (like 0 to 1), which causes vanishing gradients.
