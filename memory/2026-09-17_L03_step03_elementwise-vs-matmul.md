# Lecture 03 — Step 03: Elementwise vs matrix multiplication

status: **studied**
last-updated: **2026-09-17**
source_paths:
- `knowledge/modules/01-python-and-numerical-tooling.md`

topics studied:
- `A * B` in NumPy as elementwise multiplication of compatible arrays;
- `A @ B` as algebraic matrix multiplication;
- matrix-product compatibility rule: inner dimensions must match;
- result shape rule `(m,n) @ (n,p) -> (m,p)`;
- worked 2x2 example contrasting the numerical outputs of elementwise and matrix multiplication;
- interpretation of each matrix-product entry as a row-column dot product;
- role of `A.T` as transpose for two-dimensional real arrays;
- vectorization as expressing numerical operations through NumPy array primitives rather than explicit Python loops when possible.

comprehension check:
- concept presented with explicit arithmetic comparison; learner confirmation to be checked before advancing if confusion appears.

mastery note:
- first-pass exposure recorded; subsequent examples will reinforce matrix multiplication and shape compatibility.
