# 2026-09-21 — Voice review scope snapshot

status: **derived review snapshot — no new mastery claim**
last-updated: **2026-09-21**

purpose:
- consolidate the course topics already recorded as studied in repository memory;
- define the scope for a GPT Live / Voice review session;
- preserve weak spots and mastery uncertainty without upgrading them.

source_paths:
- `memory/STUDY_PROGRESS.md`
- dated study-memory files from 2026-09-12, 2026-09-13, 2026-09-14, 2026-09-17, 2026-09-18
- `knowledge/modules/00-large-scale-and-sparse.md`
- `knowledge/depth/00-sparse-formats-operations-reorderings.md`
- `knowledge/modules/01-python-and-numerical-tooling.md`
- `knowledge/modules/02-linear-algebra-and-direct-methods.md`

review scope:

## Sparse / large-scale block
- large-scale motivation; dense vs sparse; nnz, density, sparsity;
- COO, CSR, CSC and CSR indptr semantics;
- fill-in;
- bandwidth and symmetric permutation;
- graph viewpoint; degree; Cuthill-McKee / reverse Cuthill-McKee;
- independent-set ordering and parallel-update motivation;
- CSR sparse matrix-vector product;
- sorted COO addition;
- DOK/LIL;
- MSR/MSC;
- diagonal storage;
- ELLPACK/ITPACK;
- format-selection trade-offs and failure modes.

## Gauss-Jordan review already performed
- augmented matrices; elementary row operations;
- pivots and pivot columns;
- REF vs RREF;
- Gaussian vs Gauss-Jordan;
- row swaps / partial-pivoting motivation.
Independent execution on a fresh problem had not yet been verified in the dedicated review memory.

## Python / Jupyter block actually studied
- Jupyter execution state and fresh-kernel reproducibility;
- NumPy ndarray shape/ndim/size/dtype;
- zero-based indexing and half-open slicing;
- distinctions among (n,), (n,1), (1,n);
- elementwise multiplication vs matrix multiplication;
- matrix-product shape compatibility and row-column dot-product interpretation;
- basic vectorization.

## Linear-algebra foundations / direct methods
- Ax=b and column-combination interpretation;
- linear combinations and span;
- geometry of span in R^2;
- linear independence;
- basis and dimension;
- image / column space and kernel / null space;
- rank and rank-nullity;
- minors, cofactors and Laplace expansion;
- elementary row operations;
- REF, RREF and pivots;
- Gaussian elimination and back substitution;
- pivoting;
- numerical zero and tolerance;
- vector and matrix norms;
- conditioning and condition number;
- residual vs forward error.

mastery cautions:
- Cuthill-McKee was clarified but repository memory explicitly says not to assume full mastery.
- COO lexicographic-coordinate comparisons initially caused confusion and were later clarified.
- span geometry in R^2 required clarification of ambient dimension vs subspace dimension.
- sparse format-selection wrap-up and much of Lecture 04 are marked studied/first-pass rather than fully verified.
- no dedicated Step 7 memory was found for the determinant/invertibility bridge; test the square-matrix equivalences explicitly instead of assuming mastery.

voice-session setting:
- Study shape.
- Default Level 2: verify + small hints.
- Escalate to Level 3 only after repeated failed attempts, then require re-derivation from a different angle.
- One question at a time.
- No automatic praise and no passive lecture-first review.

This file records no newly studied topic; it is only a consolidated retrieval aid for the review session.
