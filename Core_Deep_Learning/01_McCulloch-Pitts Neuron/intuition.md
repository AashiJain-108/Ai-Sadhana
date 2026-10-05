McCulloch (neuroscientist) and Pitts (logician) proposed a highly simplified computational model of the neuron (1943)

```mermaid
graph TD
    x1["x1"] --> g
    x2["x2"] --> g
    dots1["..."] --> g
    dots2["..."] --> g
    xn["xn ∈ {0, 1}"] --> g

    subgraph Neuron ["Neuron Model"]
        g["g (Aggregation)"] --> f["f (Activation)"]
    end

    f --> y["y ∈ {0, 1}"]
```

  **g** aggregates the inputs and the function **f** takes a decision based on this aggregation

\end{tikzpicture}
\end{document}
