# Common Myths
**1. Myth:** Activation functions must be smooth and fully differentiable everywhere.

**Reality:** For a long time, researchers heavily relied on smooth, everywhere-differentiable functions like Sigmoid or Tanh so that standard gradient descent (calculating continuous derivatives) could work.Correction: ReLU (Rectified Linear Unit), $f(x) = \max(0, x)$, is not differentiable at $x = 0$. Yet, it became the standard activation function in deep learning because sub-gradient descent handles $x=0$ easily, and its simplicity drastically speeds up training.

**2. Myth:** Linear activation functions (or omitting activation) can still be useful in hidden layers if the network is deep enough.

**Reality:** People sometimes assume that stacking 50 hidden layers without activations will somehow "build up" complex representations over distance.

**Correction:** Matrix multiplication is associative. Regardless of depth, $y = W_n \dots W_2 W_1 x$ collapses into $y = W_{\text{combined}}x$. Hidden layers without non-linear activations contribute zero extra depth or expressive capacity.

**3. Myth:** Any non-linear function can act as an effective activation function.

**Reality:** Mathematically, almost any non-linear function satisfies the condition to break linearity.

**Correction:** In practice, many non-linear functions fail miserably due to training dynamics. 

For example:

<u>$f(x) = x^2$ (Quadratic):</u> Loss landscape becomes unstable, output explodes easily, and identical outputs occur for positive and negative values.

<u>$f(x) = \sin(x)$:</u> Causes chaotic loss surfaces with endless local minima (though useful in specialized fields like NeRFs/implicit neural representations, it fails in general classification/regression).

<u>Functions not defined everywhere:</u> Functions like $\ln(x)$ or $\sqrt{x}$ fail when inputs are $\le 0$.

**4. Myth:** A single hidden layer with non-linearity is all you ever need in practice.

**Reality:** The classical UAT proves that a single hidden layer with enough hidden units can approximate any function. People often ask: "Why build deep networks if 1 layer is theoretically enough?"

**Correction:** While a single-layer network can approximate any function, it may require an exponentially massive (effectively infinite) number of neurons. Deep architectures (stacking layers hierarchically) allow neural networks to represent complex functions using exponentially fewer parameters and far better generalization.
