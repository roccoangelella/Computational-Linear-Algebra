# Study progress

This file records topics that have actually been studied in conversation. It is episodic study memory, not a replacement for the semantic course notes.

## 2026-09-11 — Lecture 01, Step 1

status: **verified**
last-updated: **2026-09-11**
source_paths:
- `docs/LECTURE_INDEX.md`
- `docs/COURSE_MAP.md`
- `knowledge/modules/00-large-scale-and-sparse.md`
- `knowledge/depth/00-sparse-formats-operations-reorderings.md`

topics studied:
- meaning of a large-scale linear-algebra problem;
- dense versus sparse matrices;
- `nnz(A)`, density and sparsity;
- why representation is part of the numerical algorithm;
- dense storage cost `O(mn)` versus sparse storage scaling with the number of stored nonzeros;
- motivation for sparse matrix-vector products and iterative methods.

comprehension check:
- learner correctly explained why `nnz(A) << mn` can yield major savings and why the positions of nonzeros must still be encoded;
- precision correction made: `nnz(A)` is a count, not a complexity class; operations that visit each stored nonzero are `O(nnz(A))`;
- `O(mn)` becomes quadratic only in the square/comparable-dimension case, e.g. `m=n`, where it is `O(n^2)`.

mastery note:
- conceptual checkpoint passed after the above precision correction; implementation-level mastery will be tested while reconstructing sparse formats and sparse kernels.
