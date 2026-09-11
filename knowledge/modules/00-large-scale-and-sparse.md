# Module 0 - Large-scale viewpoint and sparse matrices

## 1. Why large-scale linear algebra is different

A dense `m x n` matrix stores all `mn` entries. This is appropriate when most entries matter and `mn` is moderate. Large-scale problems are often different: the dimension can be so large that storing or factoring the matrix densely is impossible, while only a small fraction of entries are nonzero. A **sparse matrix** is a matrix for which the number of stored nonzero entries, usually written `nnz(A)`, is much smaller than `mn`.

Two useful ratios are

`density(A) = nnz(A)/(mn)`,

and `sparsity(A) = 1 - density(A)`.

The decisive point is computational rather than merely visual: algorithms must preserve and exploit sparsity. An operation that converts a sparse matrix into a dense one can turn a feasible problem into an infeasible one even if its mathematical formula looks harmless.

Primary course sources: `Slides/Lecture0921-SparseMatrices.pdf`; lectures `01Lecture0924.txt`, `02Lecture0926.txt`; sparse examples in `Della Santa/LinAlgebra.ipynb`.

## 2. Sparse storage

A dense array implicitly stores zeros. Sparse formats instead store nonzero values together with enough index information to reconstruct their positions.

### Coordinate / COO format

COO represents the matrix by triples `(row, column, value)`. If `A_ij != 0`, the representation contains `(i,j,A_ij)`. It is conceptually simple and convenient when a matrix is assembled from a list of contributions. Arithmetic is usually performed after conversion to a compressed format.

### CSR: compressed sparse row

CSR stores:

- `data`: the nonzero values row by row;
- `indices`: the corresponding column indices;
- `indptr`: pointers marking where each row begins in `data`/`indices`.

The storage cost is proportional to `nnz(A)` plus the number of rows, rather than `mn`. CSR is particularly convenient for row access and sparse matrix-vector multiplication.

### CSC: compressed sparse column

CSC is the column-oriented analogue of CSR. It is useful when column access is dominant. The mathematical matrix is the same; the data structure is chosen according to the operations that need to be efficient.

The course's Python material uses SciPy sparse objects to expose these formats directly.

## 3. Sparse matrix-vector multiplication

For a dense matrix, computing `y = Ax` requires roughly `mn` scalar products/multiplications. If `A` is sparse, zero entries contribute nothing, so an implementation that iterates only over stored entries has cost approximately `O(nnz(A))`.

This observation is central to the whole course. Krylov methods, PageRank, spectral clustering and power-type eigenvalue methods can often be expressed primarily in terms of repeated matrix-vector products. If those products cost `O(nnz(A))`, very large problems can be attacked without dense factorization.

## 4. Graph interpretation

A matrix is often the numerical representation of a graph. For a graph with vertices `1,...,n`, an adjacency matrix `A` can be defined by `A_ij != 0` when an edge connects `i` and `j` (or points from one to the other in a directed graph). Real networks are typically sparse because each node connects to only a small fraction of all possible nodes.

This viewpoint reappears later:

- PageRank uses a directed web graph and a stochastic matrix derived from its links;
- spectral clustering uses adjacency/similarity matrices, degree matrices and graph Laplacians;
- sparse eigenvalue methods extract global structure from such matrices through repeated sparse operations.

## 5. Permutations and ordering

A permutation changes the ordering of rows and/or columns without changing the underlying mathematical relationships. If `P` is a permutation matrix, then expressions such as `PAP^T` reorder a square matrix. Ordering can matter enormously in sparse computation because elimination can create new nonzero entries, a phenomenon called **fill-in**. Two algebraically equivalent orderings can therefore lead to very different memory use and runtime.

The general lesson is that for sparse problems, the pattern of nonzeros is itself computational information.

## 6. Direct versus iterative thinking

A direct method such as Gaussian elimination aims, up to rounding error, to obtain the solution after a finite sequence of elimination steps. On sparse large systems, direct factorization can be expensive and can destroy sparsity through fill-in.

An iterative method instead constructs a sequence of approximations `x^(0), x^(1), ...`. If each iteration uses sparse matrix-vector products or sparse triangular operations, the method can avoid large dense intermediate matrices. This motivates the later modules on stationary iterations and Krylov methods.

## 7. SciPy sparse workflow

The laboratories distinguish NumPy dense arrays from `scipy.sparse` matrices. Typical operations are:

- construct a sparse matrix from coordinate data;
- convert between COO/CSR/CSC when useful;
- inspect shape and number of nonzeros;
- multiply a sparse matrix by a vector without converting to dense;
- explicitly request a dense representation only when the dimensions are small enough.

A common error is to write code that mathematically uses only sparse operations but accidentally calls a conversion that materializes all `mn` entries. In large-scale work, representation is part of the algorithm.

## 8. Complexity language used throughout the course

When the course says a method is suitable for large scale problems, the relevant questions are:

1. **Storage:** does memory grow like `mn`, `n^2`, or like `nnz(A)`?
2. **Arithmetic per iteration:** is the dominant operation a sparse matvec, a triangular solve, an orthogonalization against many vectors, or a dense factorization?
3. **Number of iterations:** how quickly does the method converge?
4. **Additional memory:** does the method keep a growing basis, as full Arnoldi/GMRES do, or only a few vectors, as basic power iteration does?
5. **Structure preservation:** does the method exploit symmetry, sparsity, definiteness, graph structure or low rank?

These five questions provide a useful lens for every algorithm in the program.

## 9. What you should be able to explain at the exam

You should be able to define sparsity and `nnz`; explain why sparse storage differs from dense storage; describe COO and compressed formats at a conceptual level; explain why sparse matvec costs scale with the nonzeros; connect sparse matrices to graphs; explain fill-in qualitatively; and motivate why iterative/projection methods become attractive for large sparse systems.

## 10. Source links

- Official slides: `Slides/Lecture0921-SparseMatrices.pdf`
- Lecture transcripts: `Slides/Trascrizioni/01Lecture0924.txt`, `02Lecture0926.txt`
- Computational material: `Della Santa/LinAlgebra.ipynb`
- Global routing: `docs/COURSE_MAP.md`
