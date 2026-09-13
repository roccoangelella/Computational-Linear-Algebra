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
last-updated: **2026-09-13**
source_paths:
- `knowledge/depth/00-sparse-formats-operations-reorderings.md`

topics studied:
- symmetric sparse matrix sparsity pattern interpreted as an undirected graph;
- matrix row/column labels correspond to graph vertices and off-diagonal nonzeros correspond to graph edges;
- vertex degree as number of neighbors;
- Cuthill-McKee as a breadth-first-like ordering that favors low-degree neighbors so connected vertices tend to receive nearby positions;
- ordering `[1,3,2,4]` means: take the old row/column labels in that new order; it does not mean the matrix entries themselves become `1,3,2,4`;
- distinction between an old vertex label and its new position after permutation;
- symmetric reordering applies the same permutation to rows and columns, equivalently `A' = P A P^T`;
- explicit four-by-four example before reordering:
  `[[1,0,1,0],[0,1,1,1],[1,1,1,0],[0,1,0,1]]`;
- after ordering `(1,3,2,4)`, the matrix becomes
  `[[1,1,0,0],[1,1,1,0],[0,1,1,1],[0,0,1,1]]`;
- in that example, the bandwidth decreases from 2 to 1;
- purpose of Cuthill-McKee: reduce or control bandwidth by finding a useful ordering automatically;
- reverse Cuthill-McKee as reversed ordering, often useful for profile/fill behavior although improvement is problem-dependent.

comprehension check:
- learner initially did not understand the meaning of the graph labels / word `indices`;
- explanation was rebuilt from the matrix itself, treating `1,2,3,4` first as row/column labels and then distinguishing those old labels from new positions;
- learner then requested the matrix explicitly before and after the Cuthill-McKee ordering; that concrete example has now been recorded;
- no explicit final confirmation of mastery has yet been given after the clarification.

mastery note:
- concept has been studied and clarified, but do not assume mastery yet; verify understanding before moving beyond Cuthill-McKee if needed.

## 2026-09-13 — Lecture 02, Step 8: Independent-set ordering

status: **verified**
last-updated: **2026-09-13**
source_paths:
- `knowledge/depth/00-sparse-formats-operations-reorderings.md`

topics studied:
- independent set as a set of graph vertices with no edges between any pair in the set;
- translation to a symmetric sparse matrix: off-diagonal entries between independent-set variables are zero;
- grouping independent-set vertices by a symmetric permutation can create a diagonal leading block;
- explicit ordering `(1,3,5,2,4)` and corresponding permutation matrix `P`, its transpose `P^T`, and the meaning of `A' = P A P^T`;
- left multiplication by `P` reorders rows and right multiplication by `P^T` applies the same ordering to columns;
- permutation matrices satisfy `P^{-1}=P^T`;
- block interpretation `[[D,B],[B^T,C]]` with diagonal `D` for the independent-set variables;
- computational convenience: once the complementary variables are fixed, variables inside the independent set have no mutual dependencies and their updates can be computed independently or in parallel;
- concrete parallel-update example using variables `x_1,x_3,x_5` and conceptual assignment to separate CPU cores.

comprehension check:
- learner asked to see the explicit `P` and `P^T`, indicating the algebraic action of the permutation was important for understanding;
- learner then requested a concrete example of what 'process independently or in parallel' means;
- after the explicit block/update example, learner chose to continue.

mastery note:
- independent-set motivation and induced block structure are understood well enough to proceed; algorithm-specific parallel implementations can be revisited later when stationary iterations or sparse kernels are studied.
