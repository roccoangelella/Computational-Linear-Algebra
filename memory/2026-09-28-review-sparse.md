# 2026-09-28 — Lecture 2 sparse-matrix review

status: **in progress**
source_paths:
- `knowledge/depth/00-sparse-formats-operations-reorderings.md`
- uploaded deck `Lecture2-DenseSparse.pdf`

topics successfully reviewed:
- COO representation as three arrays of nonzero values, row indices, and column indices;
- CSR representation as nonzero values, column indices, and row-boundary pointers;
- in the course's 1-based notation, row `i` occupies positions `IA[i]` through `IA[i+1]-1`, while `IA[i+1]` is the start of the next row;
- CSR is natural for sparse matrix-vector multiplication because the nonzeros of each row are contiguous and the row boundaries are explicit.

comprehension check:
- learner correctly explained that matrix-vector multiplication is fundamentally row-by-column and that CSR makes the relevant nonzeros directly available row by row;
- precision to reinforce next: COO can still perform matrix-vector multiplication by scanning triplets and accumulating into the appropriate output row; it is not impossible, just less directly row-structured than CSR.
