# Lecture 02, Step 10: Sparse addition in COO

status: **verified**
last-updated: **2026-09-14**
source_paths:
- `knowledge/depth/00-sparse-formats-operations-reorderings.md`

topics studied:
- sparse matrix addition in COO when coordinate triples are sorted lexicographically by `(row,column)`;
- two-pointer merge procedure: compare current coordinates, copy the earlier one, add values when coordinates coincide, and advance the relevant pointer(s);
- cancellation case: coincident stored entries can sum to zero and then disappear from the sparse representation;
- complexity `O(nnz(A)+nnz(B))` once coordinates are sorted;
- lexicographic coordinate order clarified as row-first, then column: matrix positions are scanned left-to-right within each row, then row-by-row;
- notation such as `(0,0)<(0,1)` means coordinate `(0,0)` appears earlier in that ordering, not arithmetic comparison of matrix values.

comprehension check:
- learner initially did not understand comparisons such as `(0,0)<(0,1)`;
- explanation was rebuilt from a visible matrix-coordinate grid and the rule 'compare rows first; if equal, compare columns';
- learner then chose to continue.

mastery note:
- merge principle and lexicographic coordinate ordering are understood well enough to proceed; implementation details can be revisited in the Python sparse-tools lecture.
