# Prior study state - Lecture 2 sparse/dense block

This is a **review snapshot**, not a new mastery claim.

## Already studied in conversation

Repository study memory records prior work on:
- large-scale motivation; dense vs sparse; `nnz`, density and sparsity;
- COO, CSR, CSC, including CSR `indptr` semantics;
- fill-in;
- bandwidth and symmetric permutation `P A P^T`;
- graph viewpoint and Cuthill-McKee / reverse Cuthill-McKee;
- independent-set ordering, diagonal leading block, and parallel-update motivation;
- CSR sparse matrix-vector multiplication;
- sorted COO addition and lexicographic coordinate ordering;
- DOK and LIL;
- MSR / MSC conceptual purpose;
- diagonal storage;
- ELLPACK / ITPACK and padding trade-offs;
- format-selection principles and failure modes.

## Recorded cautions

### Cuthill-McKee
The graph-label / new-position distinction initially needed a concrete matrix-before/matrix-after explanation. Study memory explicitly says **do not assume full mastery**.

### COO ordering
Coordinate comparisons such as `(0,0) < (0,1)` initially caused confusion. The row-first, then column ordering was later clarified.

### Final format selection
The wrap-up was completed at first-pass study level, but no explicit final mastery confirmation was recorded.

### MSR / MSC
Previous work emphasized the **conceptual role** of separating diagonal from off-diagonal storage. The current deck contains a more exact array-packing convention.

## Review objective

Target **retrieval plus transfer**: can the learner explain purpose, trade-offs, algorithmic consequences, and relationships without being walked through the material again?
