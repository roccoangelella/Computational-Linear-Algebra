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

## 2026-09-11 — Lecture 01, Step 2: COO

status: **verified**
last-updated: **2026-09-11**
source_paths:
- `knowledge/depth/00-sparse-formats-operations-reorderings.md`

topics studied:
- COO/coordinate sparse representation;
- one stored triplet `(row, column, value)` per nonzero entry;
- structural positions are retained while explicit zero values are omitted;
- zero-based indexing convention for computational arrays;
- COO is natural for assembly/exchange from triplets.

comprehension check:
- learner indicated the representation is clear and can reconstruct rows directly from `(row, col, data)`;
- one sign/value slip was corrected in the example: row 0 ended with `-2`, not `4`.

mastery note:
- basic COO representation considered understood; no further elementary reconstruction drills are needed unless later confusion appears.

## 2026-09-11 — Lecture 01, Step 3: CSR and `indptr`

status: **verified**
last-updated: **2026-09-11**
source_paths:
- `knowledge/depth/00-sparse-formats-operations-reorderings.md`

topics studied:
- CSR stores nonzeros row by row using `data`, `indices`, and `indptr`;
- `data` contains nonzero values, `indices` their column indices;
- `indptr` stores row-boundary positions in the flattened `data`/`indices` arrays;
- row `i` is obtained from the slice `indptr[i]:indptr[i+1]`;
- the number of nonzeros in row `i` is `indptr[i+1]-indptr[i]`;
- equal consecutive `indptr` entries represent an empty row;
- CSR is natural for row-wise sparse matrix-vector multiplication.

comprehension check:
- learner initially found `indptr` unclear;
- after reframing it as the positions of separators between concatenated rows, learner confirmed understanding.

mastery note:
- CSR row-boundary semantics are understood; proceed without further elementary `indptr` drills unless needed later.

## 2026-09-11 — Lecture 01, Step 4: CSC

status: **verified**
last-updated: **2026-09-11**
source_paths:
- `knowledge/depth/00-sparse-formats-operations-reorderings.md`

topics studied:
- CSC is the column-oriented analogue of CSR;
- `data` stores nonzeros column by column;
- `indices` stores row indices;
- `indptr` marks column boundaries;
- distinction between CSR and CSC semantics.

comprehension check:
- learner correctly constructed CSC `data` and `indptr` for the running matrix example;
- one correction was made: CSC `indices` are row indices, yielding `[0,2,1,2,0]` for the example.

mastery note:
- CSC representation is understood well enough to proceed to structural sparse-matrix issues.

## 2026-09-12 — Lecture 01, Step 5: Fill-in

status: **verified**
last-updated: **2026-09-12**
source_paths:
- `knowledge/modules/00-large-scale-and-sparse.md`
- `knowledge/depth/00-sparse-formats-operations-reorderings.md`
- `knowledge/modules/02-linear-algebra-and-direct-methods.md`

topics studied:
- fill-in as creation of new nonzero entries during Gaussian elimination/factorization;
- elimination update can turn an originally zero position into a nonzero one;
- a sparse input matrix does not guarantee sparse LU factors;
- fill-in increases both memory and arithmetic cost;
- sparsity pattern, not only `nnz(A)`, influences factorization cost;
- pivot in Gaussian/Gauss-Jordan elimination recalled as the leading entry used as the elimination anchor.

comprehension check:
- learner requested and received a quick pivot recap, then chose to continue the sparse-matrix lecture.

mastery note:
- first-pass conceptual understanding recorded; later reordering examples will reinforce the link between sparsity pattern and fill-in.

## 2026-09-12 — Lecture 02, Step 6: Bandwidth and symmetric permutation

status: **verified**
last-updated: **2026-09-12**
source_paths:
- `docs/LECTURE_INDEX.md`
- `knowledge/depth/00-sparse-formats-operations-reorderings.md`

topics studied:
- bandwidth as `max |i-j|` over nonzero positions under the course convention;
- distinction between number of nonzeros and spatial distribution of nonzeros;
- simultaneous row/column reordering `A' = P A P^T`;
- permutation as relabeling of variables/graph vertices rather than changing the underlying relationships;
- explicit example reducing bandwidth from 2 to 1 by reordering `(1,2,3,4)` to `(1,3,2,4)`.

comprehension check:
- learner requested an explicit bandwidth-reducing permutation example and then chose to continue.

mastery note:
- first-pass bandwidth/reordering concept considered clear enough to proceed to algorithmic reorderings.

## 2026-09-12 — Lecture 02, Step 7: Graph viewpoint and Cuthill-McKee

status: **verified**
last-updated: **2026-09-12**
source_paths:
- `knowledge/depth/00-sparse-formats-operations-reorderings.md`

topics studied:
- symmetric sparse matrix sparsity pattern interpreted as an undirected graph;
- vertices correspond to matrix indices and off-diagonal nonzeros correspond to graph edges;
- vertex degree as number of neighbors;
- Cuthill-McKee as a breadth-first-like ordering that favors low-degree neighbors so connected vertices tend to receive nearby indices;
- purpose: reduce or control bandwidth and improve sparse computational structure;
- reverse Cuthill-McKee as reversed ordering, often useful for profile/fill behavior although improvement is problem-dependent.

mastery note:
- conceptual algorithm introduced with the same four-vertex path example used for manual permutation; no implementation-level mastery claimed yet.
