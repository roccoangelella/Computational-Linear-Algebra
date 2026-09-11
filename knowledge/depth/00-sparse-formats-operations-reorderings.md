# Depth supplement 0 - Sparse formats, operations and reorderings

This supplement closes details from `Slides/Lecture0921-SparseMatrices.pdf` that are only summarized in Module 0. Read it after `knowledge/modules/00-large-scale-and-sparse.md`.

## 1. Sparse representation is an algorithmic choice

For `A in R^{m x n}`, let `nnz(A)` denote the number of explicitly nonzero entries. A sparse format stores values plus structural information rather than all `mn` positions. Different formats encode the same matrix but favor different operations.

### DOK - dictionary of keys

DOK stores mappings `(i,j) -> a_ij` for nonzero entries. It is convenient while entries are being inserted or modified because the sparsity pattern can change cheaply. It is not normally the fastest representation for repeated numerical kernels.

### LIL - list of lists

A row-oriented LIL representation stores, for each row, a list of nonzero column indices and corresponding values. Like DOK, it is useful during incremental matrix construction. Arithmetic is normally faster after conversion to a compressed format.

### COO - coordinate format

COO stores three arrays: row indices, column indices and values. It is natural when a matrix is assembled from triplets. Duplicate coordinates may need to be summed/canonicalized before later arithmetic.

### CSR and CSC

CSR stores nonzeros row by row using `data`, `indices` and `indptr`; CSC is the column analogue. They are designed for repeated arithmetic and structured row/column access. In particular, CSR is natural for row-wise sparse matrix-vector multiplication.

### MSR / MSC

The course also presents modified sparse row/column forms, especially for square matrices. The central idea is to treat the diagonal separately from off-diagonal entries so that diagonal access is immediate while the remaining sparse pattern is compressed.

### Diagonal and Ellpack-Itpack representations

For matrices whose nonzeros lie on a small number of diagonals, a diagonal representation can store each populated diagonal and its offset. Ellpack-Itpack uses rectangular arrays whose width is controlled by the maximum number of stored entries per row (or, in the course's diagonally structured presentation, by the limited diagonal structure). These formats trade some padding for regular memory access and predictable loops.

The correct format depends on the phase of the computation: assembly, pattern modification, row/column traversal, arithmetic, or highly regular structured kernels.

## 2. Sparse addition in COO

Suppose two COO matrices have their coordinate triples sorted lexicographically by `(row,column)`. Matrix addition can then be performed by a merge procedure analogous to merging two sorted lists:

1. compare the current coordinates from the two matrices;
2. copy the earlier coordinate if they differ;
3. if coordinates coincide, add the values and store the result if it is nonzero;
4. advance the corresponding pointer(s).

If the two matrices contain `N_z` and `N'_z` stored entries, the merge work is proportional to `O(N_z + N'_z)` once the coordinates are sorted. This is an example of how a sparse algorithm should scale with stored structure rather than with `mn`.

## 3. CSR sparse matrix-vector product

For `y=Ax`, CSR makes each row computation explicit. If row `i` occupies positions `p = indptr[i],...,indptr[i+1]-1`, then

`y_i = sum_p data[p] * x[indices[p]]`.

Only stored entries are visited, so the arithmetic is `O(nnz(A))`. The same kernel underlies many later methods: power iteration, PageRank, Arnoldi/Lanczos and stationary iterations all become practical at large scale only if the dominant operation respects sparsity.

## 4. Sparsity pattern, graph and bandwidth

For a square sparse matrix, its sparsity pattern can be represented by an adjacency graph. A matrix bandwidth can be defined as the smallest `k >= 0` such that

`a_ij = 0 whenever |i-j| > k`.

Equivalently, it is the largest distance from the main diagonal among nonzero positions. A small-bandwidth matrix has its nonzeros concentrated near the diagonal.

Why this matters: permutations do not change the abstract linear problem, but they can strongly change storage locality, fill-in during elimination, and the structure seen by direct or iterative algorithms.

If `P` is a permutation matrix, a symmetric reordering has the form

`A' = P A P^T`.

This relabels graph vertices while preserving the underlying graph.

## 5. Cuthill-McKee ordering

The Cuthill-McKee strategy traverses the adjacency graph in a breadth-first-like order, favoring neighbors of low degree, to relabel vertices so that connected vertices tend to receive nearby indices. The objective is to reduce or at least control matrix bandwidth.

A common variant reverses the produced ordering (reverse Cuthill-McKee); for many sparse problems this can reduce profile/fill behavior further, though exact improvement is problem-dependent.

The important principle is not the particular heuristic: matrix reordering is part of numerical algorithm design because the same linear operator can have very different computational behavior under different indexings.

## 6. Independent-set ordering

An independent set `S` of a graph is a set of vertices with no edges between any two vertices in `S`. Reordering the corresponding matrix so that independent-set vertices appear together can create a leading diagonal block: because those vertices are mutually nonadjacent, their off-diagonal couplings within the set are absent.

The course presents a greedy strategy for constructing such a set. The resulting block structure can be useful for parallelism, block methods and separating variables with weak direct coupling.

## 7. Format selection and failure modes

- Use DOK/LIL when the sparsity pattern changes frequently.
- Use COO for triplet assembly/exchange and simple merge-style operations.
- Use CSR/CSC for repeated arithmetic and row/column traversal.
- Use diagonal/ELL-style layouts when the pattern is sufficiently regular.
- Do not infer that a sparse input guarantees a sparse factorization: elimination can create fill-in.
- Do not densify an intermediate object merely for convenience; that can change memory from `O(nnz)` to `O(mn)` or `O(n^2)`.

## 8. Deep-understanding checkpoint

You should be able to reconstruct at least one sparse format from raw arrays; derive CSR matvec; explain why COO addition can be linear in the stored entries; define bandwidth; interpret `PAP^T` as graph relabeling; explain Cuthill-McKee qualitatively; define an independent set and explain the induced block structure; and choose a storage format based on the operation rather than by habit.

## Sources

Primary: `Slides/Lecture0921-SparseMatrices.pdf`, lectures `01Lecture0924.txt` and `02Lecture0926.txt`, and sparse examples in `Della Santa/LinAlgebra.ipynb`.
