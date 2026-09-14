# Lecture 02, Step 13 — Diagonal sparse storage

status: **verified**
last-updated: **2026-09-14**
source_paths:
- `knowledge/depth/00-sparse-formats-operations-reorderings.md`

Topics studied:
- diagonal sparse storage for matrices whose nonzeros lie on a small number of diagonals;
- diagonal offset defined by `j-i`;
- main diagonal offset `0`, upper diagonal offset `+1`, lower diagonal offset `-1`;
- tridiagonal example with offsets `[-1,0,+1]`;
- position information is partly encoded by the regular diagonal structure itself;
- matrix-vector product can exploit offsets directly, e.g. interior tridiagonal row `y_i = 2 x_{i-1} + 4 x_i + x_{i+1}`;
- distinction between generic sparsity and structured sparsity;
- limitation: diagonal storage is advantageous only when nonzeros are concentrated on relatively few diagonals.

Comprehension check:
- learner chose to continue after the tridiagonal/offset explanation.

Mastery note:
- first-pass concept considered understood well enough to proceed to ELLPACK/ITPACK.
