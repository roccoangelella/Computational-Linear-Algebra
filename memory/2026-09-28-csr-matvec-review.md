# 2026-09-28 — CSR matrix-vector product review

status: **reviewed; exact indexing being reinforced**

source_paths:
- `knowledge/depth/00-sparse-formats-operations-reorderings.md`

successfully studied:
- CSR stores nonzeros row by row; `indptr`/`IA` marks the row boundaries, while `indices`/`JA` gives the column associated with each stored value.
- For row `i`, the matrix-vector product uses the stored positions between `IA[i]` and `IA[i+1]-1` and computes `w_i = sum_h AA[h] * v[JA[h]]`.
- The learner correctly explained why `JA[h]` identifies the component of the vector that must multiply `AA[h]`: it is the column index of that matrix entry.
- CSR makes row-wise matrix-vector multiplication natural because row membership is already encoded by contiguous ranges of the stored arrays.

precision point still being reinforced:
- One does not multiply by or iterate over the `IA` values themselves as matrix entries. `IA` only supplies the start/end positions for the inner traversal through `AA` and `JA`.
