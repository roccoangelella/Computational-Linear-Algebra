# Lecture 13 bridge — Stability diagnostics for QR and orthogonalization

status: studied — first pass
last-updated: 2026-10-01
source_paths:
- knowledge/modules/03-orthogonality-qr-projectors-least-squares.md
- knowledge/depth/03-qr-construction-details.md
- docs/LECTURE_INDEX.md

topics studied:
- Distinction between exact-algebra correctness and floating-point numerical quality of a computed QR factorization.
- A computed factorization should be checked using two different diagnostics:
  1. reconstruction error ||A-QR||, which measures how well the factors reproduce A;
  2. orthogonality error ||Q^T Q-I||, which measures how close the computed columns of Q are to an orthonormal set.
- A small reconstruction error alone does not guarantee good orthogonality.
- Classical Gram-Schmidt can lose orthogonality for nearly dependent columns because subtraction of nearly equal quantities causes cancellation and accumulated roundoff.
- Modified Gram-Schmidt changes the computational order and generally preserves orthogonality better than Classical Gram-Schmidt.
- Householder QR is normally the robust dense choice because it is built from orthogonal reflections and zeros a whole column tail at once.
- Givens rotations are also orthogonal and can be preferable for selective, sparse, or structured elimination.
- Numerical stability describes the behavior of the algorithm, whereas conditioning describes the sensitivity of the underlying mathematical problem.

mastery note:
- first-pass conceptual explanation delivered; learner verification still required, especially why both reconstruction and orthogonality diagnostics are needed.
