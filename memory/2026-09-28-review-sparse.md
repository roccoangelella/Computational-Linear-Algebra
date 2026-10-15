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


## Active review checkpoint — 2026-10-15: ELLPACK row encoding

source: uploaded `Lecture2-DenseSparse(2).pdf`, pages 21–25, and course depth notes.

Verified understanding:
- For the second row `[2, 1, 0, 1]` of the slide-21 matrix, learner independently produced `COEF_2=[2,1,1]` and `JCOEF_2=[1,2,4]` (slides use 1-based indices).
- Learner correctly recognized no padding is needed for this row because it has three nonzeros, the maximum row occupancy of the example matrix; other rows require padding to width three.

Unresolved for next checkpoint:
- Learner initially confused DIAG with MSR (separate main diagonal), while DIAG stores multiple populated diagonals with offsets. Need independent retrieval of DIAG offsets and values before recording mastery of DIAG.


## Active review checkpoint — 2026-10-15: DIAG offset +2

source: uploaded `Lecture2-DenseSparse(2).pdf`, slides 21–22; `knowledge/depth/00-sparse-formats-operations-reorderings.md`.

Demonstrated:
- Learner independently identified DIAG offset +2 entries `[-2,1]` and correctly reasoned that padding is required for the fixed-width rectangular `DIAG` storage.
- Correction: learner said three asterisks, but n=4 requires two, giving `[-2,1,*,*]^T`; explained the invalid hypothetical entries (3,5) and (4,6).

Assessment: DIAG positive-offset concept substantially understood; pending follow-up retrieval for negative offsets and fixed-width precision. Do not record full DIAG mastery yet.


## Active review checkpoint — 2026-10-15: COO addition conceptual rule

Source: uploaded `Lecture2-DenseSparse(2).pdf`, slides 29–31; `knowledge/depth/00-sparse-formats-operations-reorderings.md`.

Successfully demonstrated without hint:
- Learner correctly stated that COO values arrays (`AA`) cannot be added elementwise unless the corresponding `(JR, JC)` coordinate pairs agree.
- Learner correctly explained that coincident coordinates have values added, while entries present only in one input matrix must be carried into the output at their own coordinates.

Remaining precision checks:
- Verify elimination of cancelled zero entries, e.g. `5 + (-5) = 0` at `(3,2)` in the current example.
- Verify ability to derive resulting sorted `AA`, `JR`, `JC` and describe index advances/linear merge complexity.

Status: conceptual COO merge-addition rule verified; entire algorithm not yet marked mastered.


## Active review checkpoint — 2026-10-15: COO cancellation

Source: `Lecture2-DenseSparse(2).pdf`, slide 30 and COO definitions; repository `knowledge/depth/00-sparse-formats-operations-reorderings.md`.

Successfully demonstrated:
- Learner immediately recognized that COO output should not retain the explicitly cancelled entry at `(3,2)` when `5+(-5)=0`, because the intended sparse representation stores only nonzero entries.

Nuance made explicit: the lecture's displayed pseudocode copies sums without an explicit zero check; discarding cancellation zeros is an added conditional for canonical zero-free COO output. Distinguish mathematical requirement from slide pseudocode.

Next validation: learner to reconstruct final sorted COO arrays for the 3x3 addition example.


## Active review checkpoint — 2026-10-15: CSR empty first row

Source: uploaded `Lecture2-DenseSparse(2).pdf`, slides 15–16, and repository `knowledge/modules/00-large-scale-and-sparse.md`.

Question raised by learner: for a 4x4 matrix with an entirely zero first row and a nonzero element at `(2,1)`, is `IA[1]` equal to 1 or 2? Clarification: course uses 1-based indexing, so `IA[1]=1` always; an empty first row means `IA[2]=IA[1]=1`. For the concrete case with only `a_{2,1}` nonzero, `IA=[1,1,2,2,2]`. These pointers are positions in the compressed data array, NOT matrix row numbers. Python/SciPy 0-based `indptr=[0,0,1,1,1]`.

Comprehension status: explanation supplied; await independent learner recall before claiming this nuance mastered.


## 2026-10-15 — CSR matrix-vector operation explanation (pending recall)

Basis: `Lecture2-DenseSparse(2).pdf`, slides 32–34; `knowledge/depth/00-sparse-formats-operations-reorderings.md`.

Teaching presented after user's question about performing operations with CSR (not yet independently verified):
- 0-based `data`, `indices`, `indptr` and row slice `[indptr[i], indptr[i+1])`.
- Example A with rows `[0,0,0,0]`, `[7,0,2,0]`, `[0,-1,0,3]`, `[4,0,0,5]`, v=`[2,3,4,1]`; data=`[7,2,-1,3,4,5]`, indices=`[0,2,1,3,0,3]`, indptr=`[0,0,2,4,6]`.
- Detailed row-by-row calculation yields `Av=[0,22,0,13]`; formula `w[i] += data[k]*v[indices[k]]` over row pointer interval.
- Explained cost as O(m+nnz) for 0-based row loop including empty rows.

Status: explanation given; NO new mastery claim until learner independently derives or applies a step.


## 2026-10-15 — Bandwidth active check

Source: course notes `knowledge/depth/00-sparse-formats-operations-reorderings.md`, Lecture 2 slide 43. For the example A with nonzeros at (1,4)/(4,1), BW(A)=3; reordered A' tridiagonal has BW(A')=1. On being asked both bandwidths and computational purpose, learner answered `2!!!!!` alone, insufficient/incorrect for the example's maximum-distance bandwidth; explain maximum over all nonzeros and test with one short follow-up. Do not claim concept mastered until correct independent recall.


## 2026-10-15 — Bandwidth recall, first matrix

Source: uploaded `Lecture2-DenseSparse(2).pdf`, slides 43–47; `knowledge/depth/00-sparse-formats-operations-reorderings.md`.

Successfully demonstrated:
- For the review example `A=[[2,0,0,1],[0,2,1,1],[0,1,2,0],[1,1,0,2]]`, learner answered `Bw(A)=3` without a hint. This is correct because nonzero positions `(1,4)` and `(4,1)` have `|i-j|=3`.

Pending:
- Independently identify `Bw(A')` after symmetric row/column permutation `[1,4,2,3]` and explain why reduced bandwidth matters computationally. Do not claim completed mastery of reordering until checked.


## 2026-10-15 — Bandwidth recall, permuted matrix

Sources: uploaded `Lecture2-DenseSparse(2).pdf` slides 43–47; `knowledge/depth/00-sparse-formats-operations-reorderings.md`.

Successfully demonstrated: learner independently answered `Bw(A')=1` after earlier correctly answering `Bw(A)=3`, for reordering `[1,4,2,3]` of `A=[[2,0,0,1],[0,2,1,1],[0,1,2,0],[1,1,0,2]]`. The permuted matrix is tridiagonal, so maximum index distance of any nonzero is 1. Numeric understanding of bandwidth in both arrangements is verified. Computational motivation of bandwidth reduction and Cuthill–McKee method still require independent explanation; do not claim mastery yet.


## 2026-10-15 — Cuthill–McKee objective vs algorithm distinction

Source: uploaded `Lecture2-DenseSparse(2).pdf`, slides 43–48; `knowledge/depth/00-sparse-formats-operations-reorderings.md`.

Learner response: "The algorithm consists of finding among the various combinations of rows and columns the one that minimizes bandwidth." This shows correct identification of *objective*, but NOT mastery of the mechanism.

Clarification provided: Cuthill–McKee is a heuristic, not an exhaustive optimizer. It starts from a minimum-degree vertex, visits/discovers its unvisited neighbors ordered by ascending degree, and processes the accumulated traversal breadth-first-like; resulting graph-vertex order gives simultaneous row/column permutation. Illustrated on previously studied graph path 1–4–2–3; starting at vertex 1 obtains [1,4,2,3] and reduces bandwidth 3→1.

Next: independently test retrieval of degree-based neighbor sorting and queue-like visit ordering. Do not mark full mastery until learner produces algorithm steps.
