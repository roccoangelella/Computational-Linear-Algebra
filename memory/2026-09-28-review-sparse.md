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


## Written test checkpoint — 2026-09-28 15:52

source_paths:
- uploaded deck `Lecture2-DenseSparse(1).pdf`
- `knowledge/modules/00-large-scale-and-sparse.md`
- `knowledge/depth/00-sparse-formats-operations-reorderings.md`
- prior Lecture-02 memory files

successfully demonstrated in this checkpoint:
- sparsity understood as the fraction of zero entries and density as its complement; learner also connected sparsity to avoiding wasted storage/arithmetic on zeros;
- DOK and LIL correctly identified as construction-friendly formats, with DOK especially natural when existing entries may be updated by key;
- COO conceptual encoding correctly recalled as values plus row and column arrays, though the concrete arrays were not produced;
- CSR conceptual encoding correctly recalled as values, column indices and row-boundary pointers; equality of consecutive row pointers correctly interpreted as an all-zero row;
- MSR purpose correctly recalled: separate diagonal entries for direct/frequent access while compressing off-diagonal data;
- storage-format invariance correctly stated: changing the representation changes cost, not the represented matrix or exact mathematical result;
- bandwidth concept essentially correct and the example `a_(2,7)` correctly gives distance/bandwidth lower bound 5;
- independent-set motivation and leading diagonal block were substantially recalled, including the parallelism motivation.

precision corrections to reinforce:
- for an `m x n` matrix, `sparsity=(mn-Nz)/(mn)` and `density=Nz/(mn)`;
- the computational significance of sparsity includes both memory and arithmetic, not only multiplication/addition by zero;
- an independent-set vertex is a graph vertex / matrix row-column label, not a matrix coordinate pair `(i,j)`;
- bandwidth is `max |i-j|` over nonzero positions, not a Manhattan distance to an entry on the diagonal;
- Cuthill-McKee is not obtained by ordering nonzeros by row appearance: it is a breadth-first-like traversal of the adjacency graph, starting from low degree and sorting newly discovered neighbors by increasing degree;
- no mastery claim yet for the exact simultaneous row/column permutation formula because question 11 was left blank.

gaps exposed by this checkpoint:
- DIAG versus ELLPACK/ITPACK distinction was not retained, despite prior first-pass study;
- COO sorted-list merge addition and the term/idea of a merge procedure were not retained, despite prior first-pass study;
- CSR matrix-vector multiplication formula / exact nested traversal is not yet secure and needs re-explanation;
- Cuthill-McKee needs active re-verification;
- SciPy sparse-format selection block was intentionally skipped.

status:
- review remains **in progress**;
- do not upgrade the exposed gaps to mastery until the learner re-derives them correctly.
