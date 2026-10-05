McCulloch (neuroscientist) and Pitts (logician) proposed a highly simplified computational model of the neuron (1943)

```mermaid
graph TD
    %% Inputs
    x1["x₁ ∈ {0, 1}"] --> g
    x2["x₂"] --> g
    dots1["..."] --> g
    dots2["..."] --> g
    xn["xₙ ∈ {0, 1}"] --> g

    %% Central Neuron Node Split
    subgraph Neuron ["Artificial Neuron"]
        g["g (Pre-activation / Summation)"]
        f["f (Activation Function)"]
        g --> f
    end

    %% Output
    f --> y["y ∈ {0, 1}"]

    %% Styling
    style Neuron fill:none,stroke:#333,stroke-width:2px
    style f fill:#888,stroke:#333,stroke-width:1px,color:#fff
    style g fill:#fff,stroke:#333,stroke-width:1px,color:#000

```

 - **g** = aggregates the inputs 
 - **f** = takes a decision based on this aggregation

 - weight associated with communication links may be excitatory(+ve) or inhabihary(-ve)
 - In the perceptron model, excitatory inputs promote the activation of the neuron, while inhibitory inputs oppose it.
------------------------------
### Key Differences

| Feature | Excitatory Inputs | Inhibitory Inputs |
|---|---|---|
| Mathematical Sign | Positive (w > 0) | Negative (w < 0) |
| Effect on Net Input | Increases the weighted sum. | Decreases the weighted sum. |
| Effect on Activation | Pushes the neuron closer to its activation threshold. | Pulls the neuron away from its activation threshold. |
| Biological Analogy | Neurotransmitters that encourage a neuron to fire  | Neurotransmitters that prevent a neuron from firing|

### A Simple Analogy
Imagine deciding whether to go to an outdoor concert (the neuron firing).

* Excitatory input: "Your favorite band is playing" has a positive weight. It heavily pushes you toward going.
* Inhibitory input: "It is raining heavily" has a negative weight. It strongly drags down your motivation, potentially canceling out the excitement of the band and keeping you at home.

$$\theta > n w - p$$

*(where w = excitatory weight, p = inhibitory weight)*

### output
**Binary**: neuron may fire(1) or maynot fire(0)

- MP neuron -> Activation function

$$g(x_1, x_2, \dots, x_n) = g(\mathbf{x}) = \sum_{i=1}^{n} x_i$$

$$y = f(g(\mathbf{x})) = \begin{cases} 1 & \text{if } g(\mathbf{x}) \ge \theta \\ 0 & \text{if } g(\mathbf{x}) < \theta \end{cases}$$

($\theta$ is called the thresholding parameter.) 
This is called **Thresholding Logic**.


