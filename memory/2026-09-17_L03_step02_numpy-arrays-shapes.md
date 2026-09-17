# Lecture 03 — Step 02: NumPy arrays and shapes

status: **studied**
last-updated: **2026-09-17**
source_paths:
- `knowledge/modules/01-python-and-numerical-tooling.md`
- `docs/LECTURE_INDEX.md`

topics studied:
- NumPy `ndarray` as the course's basic dense numerical-array object;
- meaning of `shape`, `ndim`, `size`, and `dtype`;
- zero-based indexing and row/column selection with `A[i,j]`, `A[i,:]`, and `A[:,j]`;
- half-open slicing convention `p:q`;
- distinction between shapes `(n,)`, `(n,1)`, and `(1,n)`;
- why transposing a one-dimensional array does not create a column/row orientation;
- matrix-vector multiplication shape tracking with `A @ x`;
- importance of checking shapes explicitly because broadcasting can otherwise hide dimensional mistakes.

comprehension check:
- learner chose to continue after the explanation; no explicit difficulty was reported.

mastery note:
- first-pass understanding is sufficient to proceed; reinforce shape semantics later in matrix multiplication, broadcasting, QR, and least-squares work.
