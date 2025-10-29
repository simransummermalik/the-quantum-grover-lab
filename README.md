# 🧠 Grover’s Escape Room: Quantum vs. Classical Search

### “If you can find the code faster, you escape the box. Classical brute force checks every key. Quantum amplifies the right one.”

---

## Overview

This repository hosts an interactive, classroom-ready **Grover’s Algorithm demonstration** built in Python with [PennyLane](https://pennylane.ai/).  
It’s designed to **visually and conceptually showcase how quantum search achieves a quadratic speedup** over classical brute force, framed as a “code-breaking escape room.”

Participants try to find a hidden bitstring (the lock code).  
- The **classical team** iterates through all combinations — `O(N)` steps.  
- The **quantum circuit** uses amplitude amplification — `O(√N)` steps.  

The result isn’t just “quantum is faster”; it’s *why* it’s faster — and where that advantage actually applies in the real world.

---

## Core Idea

Most machine learning problems hide a painful truth: **they’re search problems in disguise**.  
Finding the best parameters, weights, or architectures is fundamentally a hunt through a massive configuration space.

Classical methods use:
- gradient descent,
- heuristics,
- random restarts,  
but fundamentally, they move through that search space one clue at a time.

Grover’s algorithm instead operates like a **probabilistic magnet** — amplifying the amplitude of correct answers and suppressing the rest.  
Even in a completely unstructured search (no gradients, no priors, just “find the key”), it converges in roughly √N iterations instead of N.

That is not marketing — it’s mathematically provable.

---

## Notebook Structure

| Section | Purpose |
|----------|----------|
| **1. Setup** | Initialize dependencies, seed randomness, and import PennyLane |
| **2. The Classical Baseline** | Brute-force enumeration of all candidate bitstrings |
| **3. The Grover Circuit** | Build oracle, diffusion operator, and measure amplitudes |
| **4. Quantum vs. Classical Race** | Run both, visualize probabilities, and compare outcomes |
| **5. Interpretation** | Step-by-step breakdown of amplitude amplification |
| **6. Discussion: Does Quantum Beat Everything?** | Detailed reasoning why Grover ≠ Deep Learning |
| **7. Where This Connects to QML** | Conceptual link between unstructured search and variational optimization |
| **Appendix (A1–A6)** | Extended cells: scaling, probabilistic behavior, multi-solution search, GPU/TPU FAQ, noise models, and honest limitations |

The notebook is heavily annotated and written to sound like an **interactive seminar**, not a static paper.

---

## Key Concepts Demonstrated

### Quadratic Speedup
Grover’s algorithm solves unstructured search in O(√N) queries versus classical O(N).  
For small N, it’s symbolic. For large N, it’s decisive.

### Amplitude Amplification
Each iteration of the Grover operator rotates the system’s state vector toward the marked state in Hilbert space.  
The number of required rotations scales with √N because each oracle-diffusion pair doubles the probability amplitude of the correct answer in expectation.

### Relation to Machine Learning
Deep learning doesn’t brute-force. It exploits structure.  
But *inside* every ML pipeline are subroutines that look like unstructured searches —  
hyperparameter tuning, neural architecture search, feature selection, combinatorial routing, etc.

That’s where quantum can plug in — not to replace networks, but to accelerate the ugly parts of optimization that classical solvers choke on.

---

## Results Snapshot

| Metric | Classical | Quantum (Grover) |
|:-------:|:-----------|:----------------|
| Search Space Size (N) | 16 (4-bit lock) | 16 |
| Required Evaluations | 16 | ≈ 3 |
| Probability of Success | 1 (after full enumeration) | > 0.9 (after 3 iterations) |
| Scaling Trend | O(N) | O(√N) |

Each iteration of Grover amplifies the marked state’s probability, visible as a sharp spike in the histogram of measured outcomes.

---

## Why This Demo Works

Unlike static graphs, this notebook **lets you race classical and quantum strategies live.**

It’s designed to:
- make amplitude amplification *visually intuitive* (probability bars growing),
- anchor every quantum operation to a clear classical analogue,
- and debunk the common myths (“quantum beats neural networks” or “quantum is magic”).

It’s grounded in rigorous math but built for engagement — part lecture, part experiment, part revelation.

---

## Hardware Note

By default, the notebook uses:
```python
qml.device("default.qubit", wires=n_qubits)
