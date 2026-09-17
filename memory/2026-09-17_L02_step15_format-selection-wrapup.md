# Lecture 02, Step 15 — Sparse format selection and failure modes

status: **studied**
last-updated: **2026-09-17**
source_paths:
- `knowledge/depth/00-sparse-formats-operations-reorderings.md`
- `docs/LECTURE_INDEX.md`

topics covered:
- sparse storage format should be chosen according to the operation and sparsity structure rather than by habit;
- DOK/LIL are natural when entries or the sparsity pattern change frequently;
- COO is natural for triplet assembly/exchange and sorted merge-style operations;
- CSR/CSC are natural for repeated arithmetic and row/column traversal;
- MSR/MSC are useful when diagonal access deserves special treatment;
- diagonal and ELLPACK-style formats exploit additional regularity in the sparsity pattern;
- sparse input does not imply sparse factors because elimination can create fill-in;
- densifying an intermediate sparse object can change storage from O(nnz) to O(mn), or O(n^2) for square matrices;
- final organizing principle: exploit both sparsity and structural regularity while preserving sparse operations end-to-end.

mastery note:
- final Lecture 2 wrap-up delivered; no explicit mastery confirmation yet. Lecture 2 sparse-matrix block is complete at first-pass study level.
