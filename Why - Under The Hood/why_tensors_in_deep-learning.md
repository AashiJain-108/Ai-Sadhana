## Why do we use Tensors in deep Learning ?

So When I was studying the subjects some question actually came to my mind which I thought were worth sharing.
**why did deep learning move past NumPy to Tensors (in PyTorch, TensorFlow, or JAX)?**

**Numpy:** 
- uses contiguous blocks of memory (homogeneous C arrays) and vectorized CPU instructions, making it blazing fast for linear algebra.
- NumPy is incredible for **general numerical computing**

 *2 bottlenecks of using numpy for training deep neural network :*
  **1. Hardware Acceleration (CPU vs. GPU/TPU)**:
 -  NumPy Limitation: NumPy is hardcoded to run strictly on the CPU. Even though NumPy operations are written in fast C/Fortran, they rely on CPU cores (which are optimized for sequential, heavy-duty logic tasks).
 -  Tensor Solution: Deep learning involves millions/billions of matrix multiplications happening simultaneously (e.g., forward and backward passes in a transformer).
 -  Tensors can seamlessly allocate memory and execute operations on GPUs (Graphics Processing Units) and TPUs.
 -  A GPU has thousands of smaller cores designed to process parallel matrix math simultaneously, cutting training time from weeks to hours.
In PyTorch, shifting a tensor to a GPU is literally just adding .to('cuda') or .to('mps').

**2. Automatic Differentiation (Autograd / The Backprop Engine):**
This is the most critical theoretical difference.
- **How NumPy Works (Stateless):** If you compute $y = Wx + b$ in NumPy, NumPy calculates the output matrix and forgets everything else. It has no memory of the operation history. If you want to update your weights ($W$) using backpropagation, you have to manually derive the calculus chain rule for every single layer and write out the gradient equations by hand.
- **How Tensors Work (Dynamic Computational Graphs):** Deep learning frameworks treat Tensors as nodes in a Directed Acyclic Graph (DAG) (often called the Autograd engine). As you perform operations on tensors (addition, multiplication, activations), PyTorch records every single step behind the scenes in a hidden graph. When you call .backward(), the tensor automatically traverses backward through this graph, applying the chain rule to compute gradients for every parameter instantly.
