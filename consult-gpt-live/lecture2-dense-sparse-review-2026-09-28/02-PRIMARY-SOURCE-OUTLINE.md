# Primary source outline - Lecture 2: Dense and Sparse Matrices

Requested basis: the attached **59-page** deck `Lecture2-DenseSparse.pdf`, dated 2026-09-27.

Use the attached deck itself as the primary source during the session.

## Page routing

- pp. 2-5: large-matrix motivation; sparse/dense; sparsity and density; structured vs unstructured sparsity.
- pp. 7-26: storage schemes: DOK, LIL, COO, CSR/CSC, MSR/MSC, DIAG, ELLPACK/ITPACK.
- pp. 27-34: operations: COO addition and CSR matrix-vector multiplication.
- pp. 35-54: reorderings: sparsity pattern, permutations, adjacency graph, bandwidth, Cuthill-McKee / reverse Cuthill-McKee, independent-set ordering.
- pp. 55-59: `scipy.sparse` formats, basic functions, and format-specific operation advice.

## Source rule

When a slide-specific convention differs from generic textbook or SciPy conventions, follow the lecture for the course claim and explicitly distinguish implementation conventions.
