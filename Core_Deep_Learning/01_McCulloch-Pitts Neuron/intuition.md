McCulloch (neuroscientist) and Pitts (logician) proposed a highly simplified computational model of the neuron (1943)

\documentclass{standalone}
\usepackage{tikz}
\usepackage{amsmath,amssymb}

\begin{document}
\begin{tikzpicture}[>=stealth, scale=1.2]

  % Semi-circle top (gray fill)
  \fill[gray!60] (0,0) arc (180:0:1cm) -- cycle;
  % Semi-circle bottom (white fill with thin border)
  \draw[gray!50] (0,0) arc (180:360:1cm) -- cycle;
  % Top semi-circle outline
  \draw[gray!50] (0,0) arc (180:0:1cm);

  % Function Labels inside the circle
  \node at (1, 0.45) {\large $f$};
  \node at (1, -0.45) {\large $g$};

  % Output Arrow and Label
  \draw[->] (1, 1) -- (1, 1.8);
  \node[above] at (1, 1.8) {\large $y \in \{0, 1\}$};

  % Input Nodes & Arrows pointing to the bottom arc
  \draw[->] (-0.3, -1.2) -- (0.45, -0.45);
  \draw[->] (0.3, -1.2) -- (0.75, -0.65);
  \draw[->] (1.0, -1.2) -- (1.0, -0.7);
  \draw[->] (1.7, -1.2) -- (1.25, -0.65);
  \draw[->] (3.0, -1.1) -- (1.55, -0.45);

  % Input Labels
  \node[below left] at (-0.3, -1.2) {\large $x_1$};
  \node[below left] at (0.3, -1.2) {\large $x_2$};
  \node[below] at (1.0, -1.2) {\large $\cdot\cdot$};
  \node[below] at (1.7, -1.2) {\large $\cdot\cdot$};
  \node[below right] at (2.4, -1.1) {\large $x_n \in \{0, 1\}$};

  **g** aggregates the inputs and the function **f** takes a decision based on this aggregation

\end{tikzpicture}
\end{document}
