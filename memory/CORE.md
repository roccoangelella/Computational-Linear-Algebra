# Core course memory

Status: **derived and source-indexed**. This file is a compact orientation layer, not a replacement for the official material.

## Course identity and assessment

The course is **Computational Linear Algebra for Large Scale Problems**. The 2025/2026 material is organized around large/sparse matrix computation, numerical linear-system methods, eigenvalue/singular-value computation, and data-analysis applications. The assessment material in the supplied archive specifies two mandatory projects: **PageRank** and **Principal Component Analysis (PCA)**, plus one non-mandatory project. The exam is an oral presentation/discussion of the work with questions on the mathematical content. Always re-check `docs/ASSESSMENT.md` and the official homework documents before giving procedural advice.

## Global conceptual spine

1. **Sparse matrices** — why large matrices must be stored and multiplied without materializing zeros; storage formats and graph/permutation viewpoints.
2. **Linear algebra foundations** — matrices, linear systems, vector spaces, linear maps, rank, determinant, norms, eigenvalues, conditioning.
3. **Direct transformations and orthogonality** — Gaussian elimination; Gram–Schmidt and modified Gram–Schmidt; Givens rotations; Householder reflections; QR-type reasoning; projectors and least squares.
4. **Stationary iterative solvers** — fixed-point/matrix-splitting view, Jacobi and Gauss–Seidel, iteration matrix, spectral-radius convergence, residuals versus true error and conditioning.
5. **Approximation** — interpolation/regression viewpoint and least-squares problems; normal equations/QR connections.
6. **Krylov subspaces** — polynomial-in-`A` approximation spaces, Arnoldi orthogonalization, projected systems, FOM and the GMRES viewpoint; finite-dimensional termination in exact arithmetic and the practical large-sparse setting.
7. **Spectral graph methods** — graph Laplacian, eigenvectors/eigenvalues and spectral clustering.
8. **Eigenvalue computation** — power/inverse-power ideas, Rayleigh quotient, shifts, deflation, Gershgorin localization, Lanczos for symmetric problems, and the QR eigenvalue method.
9. **Singular value decomposition** — singular values/vectors, relationship to eigenproblems, computation, low-rank approximation, image/data compression, pseudoinverse and least squares.
10. **PCA and clustering** — covariance/statistics background, PCA as an eigen/SVD-based dimensionality reduction, explained variance/loadings/scores, preprocessing, interpretation, then k-means and cluster evaluation.
11. **PageRank** — stochastic/link matrices and the dominant eigenvector interpretation, serving as one mandatory project.

## Cross-topic dependencies that matter most

- Sparse matrices motivate iterative/Krylov/eigenvalue methods because dense factorizations or dense storage are often unaffordable.
- Orthogonality is a numerical tool, not only a geometric concept: it powers QR, Arnoldi/Lanczos, projections, least squares, eigensolvers and SVD.
- Projectors and least squares are the conceptual bridge from orthogonality to approximation, Krylov projection methods, regression and SVD pseudoinverses.
- Eigenvalue methods reappear in spectral clustering, PageRank and PCA.
- SVD is both an eigenvalue-related factorization and the foundation of optimal low-rank approximation; PCA can be computed through covariance eigendecomposition or directly through SVD of centered/scaled data.
- Conditioning controls how residuals translate into forward error; a small residual does not automatically imply an accurate solution for an ill-conditioned system.

## Primary navigation

- Full module map: `docs/COURSE_MAP.md`
- Lecture chronology: `docs/LECTURE_INDEX.md`
- Concept dependencies and aliases: `docs/CONCEPT_GRAPH.md`
- Exam/homework rules: `docs/ASSESSMENT.md`
- Source hierarchy and provenance rules: `docs/SOURCE_POLICY.md`
- Why this knowledge architecture is structured this way: `docs/KNOWLEDGE_ARCHITECTURE.md`
