# Lecture 10 — Step 1: Classical vs Modified Gram–Schmidt

status: studied — first pass
last-updated: 2026-09-22
source_paths:
- knowledge/modules/03-orthogonality-qr-projectors-least-squares.md

topics studied:
- Classical Gram–Schmidt and Modified Gram–Schmidt have the same mathematical goal: replace linearly independent input vectors by an orthonormal basis of the same span.
- In Classical Gram–Schmidt, for a new vector a_j, all projection coefficients q_i^T a_j are formed relative to the original a_j, and the corresponding components are subtracted in one accumulated expression.
- In Modified Gram–Schmidt, a working vector v is updated immediately after each projection removal; the next coefficient is computed from the current remainder v.
- In exact arithmetic the two organizations are mathematically equivalent and produce the same subspace/factorization.
- In floating-point arithmetic, Modified Gram–Schmidt is usually more robust and better preserves orthogonality, especially for nearly dependent columns.
- Example with a1=(1,0,0)^T, a2=(1,1,0)^T, a3=(1,1,1)^T: both methods yield q1=e1, q2=e2, q3=e3; the difference is the order in which a3 is stripped of its q1 and q2 components.
- A very small norm of the remaining vector v indicates exact or numerical linear dependence; normalization must then be guarded by a tolerance.

mastery note:
- First-pass conceptual explanation delivered; learner verification still required.
