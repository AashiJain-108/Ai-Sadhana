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
 **g** = aggregates the inputs 
 **f** = takes a decision based on this aggregation of function **g**
