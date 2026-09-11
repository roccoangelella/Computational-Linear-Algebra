# Core course memory

Status: **derived, source-indexed, and backed by the study-complete semantic corpus in `knowledge/`**. This file is deliberately compact: it keeps the whole program visible, while detailed mathematics belongs in the module documents and their depth supplements.

## Course identity and assessment

The course is **Computational Linear Algebra for Large Scale Problems**. The 2025/2026 corpus centers on large/sparse matrix computation, numerical linear-system methods, eigenvalue/singular-value computation, and data-analysis applications. The supplied assessment material specifies two mandatory projects: **PageRank** and **Principal Component Analysis (PCA)**, plus one non-mandatory project. Always re-check `docs/ASSESSMENT.md` for current procedural advice.

## Global conceptual spine

1. **Sparse matrices and large-scale thinking** — store/process nonzeros, understand sparse matvec cost and graph structure, and avoid algorithms that destroy useful sparsity. Detailed: `knowledge/modules/00-large-scale-and-sparse.md`.
2. **Python/numerical tooling** — Jupyter, NumPy arrays, shapes/dtypes, SciPy sparse structures, tolerances, pandas/scikit-learn workflow. Detailed: `knowledge/modules/01-python-and-numerical-tooling.md`.
3. **Linear algebra foundations/direct methods** — vector spaces, rank, determinant, norms, Gaussian elimination, REF/RREF, conditioning, residual versus error. Detailed: `knowledge/modules/02-linear-algebra-and-direct-methods.md`.
4. **Orthogonality and projections** — Gram-Schmidt/MGS, Givens, Householder, QR, orthogonal projectors and least-squares geometry. Detailed: `knowledge/modules/03-orthogonality-qr-projectors-least-squares.md`.
5. **Stationary iterative solvers** — matrix splittings, Jacobi, Gauss-Seidel, iteration matrix, spectral-radius convergence and stopping criteria. Detailed: `knowledge/modules/04-stationary-iterative-methods.md`.
6. **Approximation/least squares** — polynomial interpolation plus design matrices, overdetermined systems, normal equations versus QR, conditioning and projection interpretation. Detailed: `knowledge/modules/05-approximation-and-least-squares.md`.
7. **Krylov methods** — `K_m(A,b)`, minimal polynomials, Arnoldi, Hessenberg projection, FOM, GMRES and large-sparse cost/memory logic. Detailed: `knowledge/modules/06-krylov-arnoldi-fom-gmres.md`.
8. **Spectral clustering** — similarity graph, degree/Laplacian matrices, connected components, Fiedler/eigenvector embeddings and k-means. Detailed: `knowledge/modules/07-spectral-clustering.md`.
9. **Power-type eigenvalue methods** — power/inverse/shifted inverse iteration, Rayleigh quotient, spectral separation, the course's symmetric rank-one **shifting**, and Householder similarity **deflation** with recursive dimension reduction. Detailed: `knowledge/modules/08-power-inverse-shifts-deflation.md`; depth: `knowledge/depth/08-power-shifting-householder-deflation.md`.
10. **PCA and k-means** — covariance eigendecomposition/SVD viewpoint, scores/loadings, explained variance, preprocessing, interpretation, clustering and the current PCA project. Detailed: `knowledge/modules/09-pca-and-kmeans.md`.
11. **Advanced eigenvalue computation** — Gershgorin localization/conditioning, Rayleigh/Ritz ideas, Lanczos, Hessenberg/tridiagonal structure and QR iteration with shifts/deflation. Detailed: `knowledge/modules/10-gershgorin-lanczos-qr-eigenvalues.md`.
12. **Singular value decomposition** — existence/uniqueness structure, singular vectors/values, four fundamental subspaces, norms/conditioning, truncated-SVD optimality, pseudoinverse, least squares and computation by orthogonal reductions. Detailed: `knowledge/modules/11-singular-value-decomposition.md`.
13. **PageRank** — stochastic web matrices, damping/teleportation, positivity/uniqueness, sparse power iteration and the mandatory project. Detailed: `knowledge/modules/12-pagerank-project.md`.

## Cross-topic dependencies that matter most

- Sparse storage makes repeated matrix-vector products feasible, motivating stationary, Krylov, PageRank and sparse eigenvalue methods.
- Orthogonality is both geometry and a numerical-stability device: QR, projections, Arnoldi/Lanczos, Householder deflation, eigensolvers, SVD and PCA all depend on it.
- Least squares is the bridge from projectors to approximation, GMRES and the SVD pseudoinverse.
- Spectral information controls convergence in stationary iterations and power methods and provides structure in PageRank, spectral clustering and PCA.
- Arnoldi projects a general matrix to Hessenberg form; symmetry reduces this structure to Lanczos/tridiagonal form.
- Householder transformations recur because orthogonal transformations preserve Euclidean geometry while creating useful matrix structure: QR, course eigenpair deflation, Hessenberg/tridiagonal/bidiagonal reductions.
- SVD closes several loops at once: `||A||_2`, conditioning, rank, least squares/minimum norm, optimal low-rank approximation and PCA.
- Conditioning controls how residuals relate to forward error; a small residual alone is not an accuracy certificate for an ill-conditioned problem.

## Retrieval anchors

- Detailed program: `knowledge/README.md`
- Depth-supplement routing: `knowledge/depth/README.md`
- Full module map: `docs/COURSE_MAP.md`
- Deep-coverage audit: `docs/DEEP_COVERAGE_AUDIT.md`
- File-by-file corpus audit: `docs/SOURCE_COVERAGE.md`
- Lecture chronology: `docs/LECTURE_INDEX.md`
- Labs/notebooks: `docs/LAB_INDEX.md`
- Concept dependencies: `docs/CONCEPT_GRAPH.md`
- Exam/homework rules: `docs/ASSESSMENT.md`
- Provenance/source policy: `docs/SOURCE_POLICY.md`
- Raw-ingestion versus semantic-study status: `sources/INGESTION_STATUS.md`
