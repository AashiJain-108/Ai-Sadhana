# Universal Approximation Theorem & Tower Functions

## Table of Contents

* [1. Overview: Universal Approximation Theorem](#1-overview-universal-approximation-theorem)
* [2. MLPs with Perceptrons vs. Sigmoid Neurons](#2-mlps-with-perceptrons-vs-sigmoid-neurons)
* [3. Intuition Behind Tower Functions](#3-intuition-behind-tower-functions)

  * [3.1 Constructing a 1D Tower Function](#31-constructing-a-1d-tower-function)
  * [3.2 Constructing a 2D Tower Function](#32-constructing-a-2d-tower-function)
* [4. Architecture of a 2D Tower Block](#4-architecture-of-a-2d-tower-block)
* [5. Approximating Continuous Functions Using Towers](#5-approximating-continuous-functions-using-towers)
* [6. Key Takeaways](#6-key-takeaways)
* [7. References](#7-references)

---

## 1. Overview: Universal Approximation Theorem

The **Universal Approximation Theorem (UAT)** establishes that a feedforward neural network with a sufficiently large hidden layer can approximate a broad class of continuous functions to any desired degree of accuracy on a compact domain.

In simple words:

> A neural network with enough hidden neurons can approximate almost any continuous curve or surface, provided the activation function and network architecture satisfy the required conditions.

For a continuous function

$$
f:\mathbb{R}^{n}\rightarrow\mathbb{R}^{m},
$$

we want a neural network \(g(x)\) such that

$$
\|f(x)-g(x)\|<\epsilon,
$$

where \(\epsilon>0\) is the desired approximation error.

More precisely, for approximation on a compact domain \(K\subset\mathbb{R}^{n}\), the objective is

$$
\sup_{x\in K}\|f(x)-g(x)\|<\epsilon.
$$

Here:

* \(f(x)\) is the target function.
* \(g(x)\) is the function represented by the neural network.
* \(\epsilon\) is the maximum permitted approximation error.
* \(K\) is the compact input domain on which the approximation is required.

### Historical Background

* **Cybenko (1989):** Established a universal approximation result for feedforward networks using sigmoid activation functions.
* **Hornik et al. (1989):** Demonstrated the approximation capabilities of multilayer feedforward networks.
* **Hornik (1991):** Further established that universal approximation is not restricted to one particular activation function, under suitable mathematical conditions.

### What Does the Theorem Actually Mean?

Imagine that we want a neural network to approximate a complicated curve.

Instead of representing the entire curve with one neuron, we combine the outputs of multiple neurons. Each neuron contributes a small part of the overall shape.

By combining enough neurons, the network can approximate the target curve increasingly accurately.

**Important:** The theorem establishes representational capability. It does not guarantee that training will find the required weights, that the network will generalize well, or that the approximation will be computationally efficient.

---

## 2. MLPs with Perceptrons vs. Sigmoid Neurons

A multilayer perceptron (MLP) can use different activation functions. The distinction below compares networks using hard-threshold perceptrons with networks using smooth sigmoid activations.

| Feature                 | Hard-Threshold Perceptrons                                  | Sigmoid Neurons                                                                   |
| ----------------------- | ----------------------------------------------------------- | --------------------------------------------------------------------------------- |
| Activation              | Hard step or threshold                                      | Smooth, continuous sigmoid                                                        |
| Output                  | Discrete, such as 0 or 1                                    | Continuous, typically between 0 and 1                                             |
| Typical application     | Boolean functions and threshold decisions                   | Smooth function approximation and differentiable learning                         |
| Approximation behavior  | Can represent Boolean functions with suitable architectures | Can approximate continuous functions on compact domains under suitable conditions |
| Hidden-layer size       | May require many neurons for certain functions              | Sufficient width provides universal approximation                                 |
| Training considerations | Hard thresholds are not ordinarily differentiable           | Sigmoid is differentiable, enabling gradient-based training                       |

### Sigmoid Activation Function

The logistic sigmoid function is defined as

$$
\sigma(z)=\frac{1}{1+e^{-z}}.
$$

For a neuron with input vector \(x\), weights \(w\), and bias \(b\),

$$
h(x)=\sigma(w^{T}x+b).
$$

The weights determine the direction and steepness of the transition, while the bias shifts its position.

As the magnitude of the weights increases, the sigmoid transition becomes steeper. Under appropriate scaling, it approaches a hard step function.

---

## 3. Intuition Behind Tower Functions

The Universal Approximation Theorem can be understood intuitively by constructing simple building blocks called **pulse functions** or **tower functions**.

The central idea is:

1. Construct a localized block using neurons.
2. Position the block in a particular region of the input space.
3. Adjust its height.
4. Combine many blocks to approximate a more complicated function.

We begin with a one-dimensional tower and then extend the construction to two dimensions.

---

### 3.1 Constructing a 1D Tower Function

Consider the sigmoid function:

$$
\sigma(wx+b)=\frac{1}{1+e^{-(wx+b)}}.
$$

#### Step 1: Make the sigmoid transition steep

When the magnitude of \(w\) becomes large, the sigmoid changes rapidly around its transition point.

The transition occurs approximately at

$$
wx+b=0.
$$

Therefore, the transition location is

$$
x=-\frac{b}{w}, \qquad w\neq 0.
$$

A sigmoid with a large positive weight approximates an upward step, while one with a large negative weight approximates a downward step.

#### Step 2: Position two transitions

Suppose we want a tower between two points \(a\) and \(b\), where \(a<b\).

We can construct an approximate pulse by subtracting two sigmoid functions:

$$
T(x)=\sigma\big(k(x-a)\big)-\sigma\big(k(x-b)\big),
$$

where \(k>0\) controls the steepness.

The first sigmoid rises near \(x=a\), while the second rises near \(x=b\).

Between the two transition points, the first sigmoid is approximately 1 and the second is approximately 0. Their difference is therefore approximately 1.

Outside the interval, both outputs are approximately equal, so their difference is approximately 0.

#### Step 3: Understand the result

The resulting function behaves approximately like a rectangular pulse:

```text
T(x)
 1 |          ┌──────────┐
   |         /            \
   |        /              \
 0 |_______/________________\________ x
           a                b
```

The smooth version has rounded transitions, while the ideal rectangular pulse has sharp edges.

As \(k\) increases, the sigmoid transitions become steeper, making the pulse more closely resemble a rectangular tower.

#### Mathematical Representation

$$
\boxed{
T(x)=\sigma\big(k(x-a)\big)
-\sigma\big(k(x-b)\big)
}
$$

Here:

* \(a\) is the approximate left boundary.
* \(b\) is the approximate right boundary.
* \(k\) controls the steepness of the edges.
* \(T(x)\) is approximately 1 inside the interval and 0 outside it.

**Intuition:** Two sigmoid transitions can work together to isolate a particular interval of the input space.

---

### 3.2 Constructing a 2D Tower Function

Now consider a function with two inputs:

$$
f:\mathbb{R}^{2}\rightarrow\mathbb{R}.
$$

The inputs are \(x_1\) and \(x_2\).

Instead of constructing a pulse along a line, we want a localized block over a rectangular region of the two-dimensional plane.

#### Step 1: Construct a pulse along each input dimension

Let the first pulse be

$$
T_1(x_1)=
\sigma\big(k(x_1-a_1)\big)
-\sigma\big(k(x_1-b_1)\big),
$$

and the second pulse be

$$
T_2(x_2)=
\sigma\big(k(x_2-a_2)\big)
-\sigma\big(k(x_2-b_2)\big).
$$

Each pulse approximately identifies an interval along one input dimension.

#### Step 2: Combine the pulses

An illustrative construction adds the two pulses:

$$
S(x_1,x_2)=T_1(x_1)+T_2(x_2).
$$

If both inputs lie inside their respective intervals, both pulses are approximately 1, producing

$$
S(x_1,x_2)\approx 2.
$$

If only one input lies inside its interval, then

$$
S(x_1,x_2)\approx 1.
$$

If neither input lies inside its interval, then

$$
S(x_1,x_2)\approx 0.
$$

This creates a high central region, lower regions around it, and a low exterior.

```text
Conceptual cross-section of the combined pulses

Height 2             ┌────────┐
                     │  Peak  │
Height 1      ───────┘        └───────
Height 0  ──────────────────────────────
```

This is an illustrative cross-section, not a complete three-dimensional rendering of the surface.

#### Step 3: Isolate the central region

An additional neuron can distinguish the central region from the lower regions by applying a threshold.

For a hard-threshold activation,

$$
H(z)=
\begin{cases}
1, & z\geq 0,\\
0, & z<0.
\end{cases}
$$

An illustrative threshold construction is

$$
B(x_1,x_2)=H\big(S(x_1,x_2)-\theta\big),
$$

where \(\theta\) is chosen between the approximate floor and peak values.

For example, choosing \(\theta=1.5\) separates the central region, where \(S\approx 2\), from the surrounding floor, where \(S\approx 1\).

The result is approximately 1 in the rectangular region where both pulses are active and 0 elsewhere.

**Important mathematical distinction:** The hard-threshold construction illustrates the geometry, but a hard threshold is not a sigmoid. To obtain a smooth approximation, the threshold can be replaced by a sufficiently steep sigmoid, with appropriate scaling and parameters.

#### Conceptual Visualization

```text
Combined pulses                    Thresholded result

      ┌──────────┐                     ┌──────────┐
      │   Peak   │                     │          │
──────┘          └──────           ─────┘          └─────
 Lower surrounding regions             Isolated tower
```

**Intuition:** Two one-dimensional pulses identify a rectangular region, and an additional nonlinear operation can isolate the region where both pulses are active.

---

## 4. Architecture of a 2D Tower Block

A simple construction based on two one-dimensional pulses uses four sigmoid neurons to create the pulses and an additional neuron to combine and threshold them.

### Architecture

```text
                    Input Layer
                  (x₁, x₂)
                      │
             ┌────────┴────────┐
             │                 │
       x₁-direction       x₂-direction
          pulse               pulse
             │                 │
        ┌────┴────┐       ┌────┴────┐
        │         │       │         │
      Sigmoid   Sigmoid  Sigmoid   Sigmoid
        │         │       │         │
        └────┬────┘       └────┬────┘
             │                 │
             └────────┬────────┘
                      │
                Combine outputs
                      │
               Output activation
                      │
                 2D Tower
```

The four sigmoid neurons construct two pulses:

* Two neurons define the pulse along \(x_1\).
* Two neurons define the pulse along \(x_2\).

The additional output neuron combines their outputs and produces an approximation of the desired localized region.

This is a conceptual architecture. Exact neuron counts and connectivity depend on the chosen activation functions and the particular mathematical construction.

### Generalization to More Dimensions

The same intuition extends to higher-dimensional inputs.

* **1D:** A pulse isolates an interval.
* **2D:** A pulse isolates a rectangular region.
* **3D:** A pulse isolates a box-shaped region.
* **Higher dimensions:** A pulse can isolate a region in a multidimensional input space.

As the dimensionality increases, constructing localized regions generally becomes more complicated and may require additional neurons or more elaborate architectures.

---

## 5. Approximating Continuous Functions Using Towers

How can small tower functions approximate a complicated curve or surface?

The key idea is to divide the input domain into small regions and approximate the target function within each region.

### Step 1: Divide the input space

Consider a continuous one-dimensional function \(f(x)\).

Divide its domain into many small intervals:

$$
[a_1,b_1], [a_2,b_2],\ldots,[a_N,b_N].
$$

Within each sufficiently small interval, the function's variation can be made small because continuous functions on compact domains are uniformly continuous.

### Step 2: Construct local building blocks

Construct a tower function for each interval.

Each tower identifies a localized region of the input space.

### Step 3: Adjust the tower heights

Assign an appropriate output weight to each tower so that its contribution approximates the target function in that region.

A simplified conceptual expression is

$$
g(x)=\sum_{i=1}^{N}c_iT_i(x),
$$

where:

* \(T_i(x)\) is the \(i\)-th tower function.
* \(c_i\) determines the contribution of that tower.
* \(N\) is the number of tower functions.

The coefficients and tower parameters are chosen to make \(g(x)\) close to \(f(x)\).

### Step 4: Combine the building blocks

The sum of the local contributions forms an approximation of the original function.

```text
Target function:
       __
      /  \       __
     /    \_____/  \
____/               \____

Tower approximation:
      ┌──┐
   ┌──┘  └─┐  ┌──┐
 ┌─┘       └──┘  └─┐
─┘                  └──
```

The diagram is conceptual: real approximations may have smooth transitions, and their quality depends on the tower construction and parameter choices.

### Step 5: Improve the approximation

We can generally improve the approximation by:

* Increasing the number of local building blocks.
* Reducing the size of the regions being approximated.
* Choosing better tower locations and heights.
* Adjusting the network's weights and biases.

For a continuous target function on a compact domain, the Universal Approximation Theorem guarantees that a suitable network exists for every desired positive approximation tolerance, under the theorem's assumptions.

### Extending the Idea to 2D Surfaces

For a two-dimensional function,

$$
f:\mathbb{R}^{2}\rightarrow\mathbb{R},
$$

the input domain can be divided into small rectangular regions.

Each localized block contributes to the approximation of the surface in its corresponding region.

Combining many such contributions can approximate complex surfaces, including hills, valleys, curved regions, and other continuous patterns.

**Important:** The individual building blocks do not need to resemble the original function. Their combined output is what approximates the target.

---

## 6. Key Takeaways

1. **Universal approximation:** A sufficiently wide feedforward network can approximate continuous functions on compact domains under suitable conditions.

2. **Sigmoid activation:** A sigmoid neuron produces a smooth transition between low and high output values.

3. **Steep transitions:** Increasing the magnitude of a sigmoid's input weight makes its transition sharper.

4. **One-dimensional towers:** Subtracting two appropriately positioned sigmoid functions creates an approximate localized pulse.

5. **Two-dimensional towers:** Combining pulses along two input dimensions can identify a rectangular region.

6. **Function approximation:** Multiple localized building blocks can be combined to approximate a more complicated function.

7. **Representation is not learning:** The theorem guarantees that suitable parameters exist; it does not guarantee that a training algorithm will find them.

8. **Width versus depth:** The theorem establishes that one hidden layer can be sufficient for approximation. It does not imply that a single hidden layer is always the most efficient architecture.

### Final Intuition

Think of a complicated function as a landscape.

A neural network does not necessarily need to learn the entire landscape as one indivisible object. It can combine many simple responses, each contributing to a different part of the input space.

The power comes from combining these simple responses into a more expressive function.

---

## 7. References

1. Cybenko, G. (1989). *Approximation by Superpositions of a Sigmoidal Function.* Mathematics of Control, Signals, and Systems, 2, 303–314.
   https://doi.org/10.1007/BF02551274

2. Hornik, K., Stinchcombe, M., & White, H. (1989). *Multilayer Feedforward Networks Are Universal Approximators.* Neural Networks, 2(5), 359–366.
   https://doi.org/10.1016/0893-6080(89)90020-8

3. https://medium.com/analytics-vidhya/neural-networks-and-the-universal-approximation-theorem-e5c387982eed

4. Hornik, K. (1991). *Approximation Capabilities of Multilayer Feedforward Networks.* Neural Networks, 4(2), 251–257.
   https://doi.org/10.1016/0893-6080(91)90009-T
