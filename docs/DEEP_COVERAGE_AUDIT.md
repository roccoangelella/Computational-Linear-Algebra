# Deep coverage audit

Date: 2026-09-11

## Purpose

This is a stricter second-pass audit of whether the GitHub repository is sufficient to support a **deep understanding of the entire taught Computational Linear Algebra program**, not merely whether every topic name appears somewhere.

The audit compared the repository's study layer against the complete supplied 91-file corpus already catalogued in `docs/SOURCE_COVERAGE.md` and `sources/MANIFEST.tsv`. Official slides/homework material were treated as highest-authority course evidence; labs/notebooks were checked for implementation detail; transcripts were used to recover lecture explanations and handwritten-slide content; supplied external references were treated as secondary depth material.

## Audit standard

A topic counts as deeply covered only if the repository contains, at the level relevant to this course:

1. definitions and dimensions/assumptions of the mathematical objects;
2. derivation or justification of the central formulas/theorems rather than only their names;
3. algorithm steps and what problem they solve;
4. convergence/existence/uniqueness/stability conditions when applicable;
5. numerical caveats, conditioning and failure modes;
6. computational/storage cost and large-scale implications when relevant;
7. links to implementation/lab logic and connections to prerequisite/application topics.

This standard is deliberately stronger than syllabus coverage.

## Result before remediation

The 13-module semantic corpus had strong breadth and several genuinely deep sections, especially Krylov/Arnoldi/FOM/GMRES, spectral clustering, power methods, PCA, Lanczos/QR, SVD and PageRank. However, the strict comparison found real omissions. Therefore the pre-audit claim of deep-study completeness was too strong without qualification.

The largest missing block was polynomial interpolation: the official approximation slides include Lagrange interpolation, interpolation-error analysis, the Lebesgue constant, Weierstrass approximation, Chebyshev nodes and the Runge phenomenon, while the original Module 5 moved too quickly from interpolation to least squares.

Additional depth gaps were found in sparse formats/reorderings; `PA=LU`, morphism matrices and change of basis; explicit Householder/Givens QR construction; sharper Jacobi/Gauss-Seidel convergence theorems; restarted/practical GMRES; PCA cluster-validation metrics; QR eigensolver convergence assumptions; and SVD bidiagonalization details.

## Remediation

The following source-indexed supplements were added under `knowledge/depth/`:

- `00-sparse-formats-operations-reorderings.md`
- `02-foundations-lu-morphisms-change-of-basis.md`
- `03-qr-construction-details.md`
- `04-stationary-convergence-details.md`
- `05-polynomial-interpolation-and-convergence.md`
- `06-krylov-projection-and-gmres-implementation.md`
- `09-pca-preprocessing-and-cluster-validation.md`
- `10-eigenvalue-convergence-details.md`
- `11-svd-computation-details.md`

`knowledge/depth/README.md` routes these supplements from their corresponding base modules.

## Module-by-module status after remediation

| Module | Strict-depth status | Evidence/reason |
|---|---|---|
| 0 Large-scale/sparse | PASS with supplement | storage taxonomy, sparse kernels, graph/bandwidth/reordering and large-scale cost model are represented |
| 1 Python/tooling | PASS | arrays/shapes/dtypes, vectorization, sparse objects, floating point/tolerances, pandas/sklearn workflow and reproducibility are represented |
| 2 Foundations/direct methods | PASS with supplement | spaces/rank/norms/conditioning/elimination plus solvability, `PA=LU`, linear-map matrices, change of basis, similarity and Cayley-Hamilton |
| 3 Orthogonality/QR/projectors | PASS with supplement | GS/MGS, projectors/least squares plus explicit stable Householder and Givens QR construction |
| 4 Stationary iterations | PASS with supplement | splitting/error recurrence/spectral-radius criterion/residuals plus diagonal-dominance, SPD, Stein-Rosenberg and tridiagonal comparison results |
| 5 Approximation | PASS with supplement | polynomial interpolation/convergence/node choice plus least-squares geometry and QR/SVD connections |
| 6 Krylov methods | PASS with supplement | Krylov/minimal polynomial, Arnoldi/FOM/GMRES plus general projection spaces, restart, complexity and practical Hessenberg QR updates |
| 7 Spectral clustering | PASS | Laplacian quadratic form/PSD, connected components, Fiedler/Rayleigh view, normalized variants, cut relaxation, spectral embedding and computational issues |
| 8 Power/shifts/deflation | PASS | eigenstructure, power convergence derivation, inverse/shifted/Rayleigh iterations, residuals, symmetric deflation and PageRank connection |
| 9 PCA/k-means | PASS with supplement | PCA derivation/SVD/reconstruction/current homework plus preprocessing and internal/external clustering evaluation formulas |
| 10 Gershgorin/Lanczos/QR | PASS with supplement | localization proof, Ritz/Lanczos recurrence, finite-precision issues plus QR convergence conditions, Hessenberg reduction, shifts and deflation |
| 11 SVD | PASS with supplement | existence/geometry/subspaces/norms/Eckart-Young/pseudoinverse/least squares plus bidiagonalization and structured computation |
| 12 PageRank | PASS | stochastic construction, failure modes, teleportation/uniqueness, power iteration, convergence, sparse implementation, dataset parsing and validation |

## Cross-topic coherence check

The repository now contains the prerequisite chains needed to reason across modules rather than memorize isolated algorithms. Examples:

- sparse representation -> cheap matvec -> stationary/Krylov/power/Lanczos/PageRank;
- basis/change-of-basis -> similarity -> eigenvalue algorithms;
- orthogonality -> QR/projectors -> least squares -> Arnoldi/GMRES -> QR eigensolver/SVD;
- polynomial approximation -> least squares -> projection methods;
- spectral radius -> stationary convergence and power-method convergence;
- Rayleigh quotient -> power methods, spectral clustering, Lanczos and PCA;
- SVD -> conditioning, pseudoinverse, low-rank approximation and PCA.

`docs/CONCEPT_GRAPH.md` remains the global routing layer; the depth supplements ensure those edges lead to enough mathematical detail.

## What this audit can and cannot certify

**Certified:** the repository now contains enough source-indexed mathematical and computational material to support a deep study of the full taught program without routinely reopening the original binary PDFs. A student can use it to derive the main algorithms, state their assumptions, explain convergence/numerical behavior, connect implementations to theory and prepare for the mathematical oral discussion described in the assessment material.

**Not certified:** merely reading the repository guarantees mastery or a particular grade. Deep understanding is a property of the learner, not of a document collection. It requires solving problems, reproducing derivations without looking, implementing/debugging algorithms, interpreting numerical experiments and answering oral questions. The repository is now sufficient material for that process; it cannot replace the process.

## Residual reasons to consult an original source

The semantic corpus is not a byte-for-byte archive. Open/recover the original source when an exact figure, handwritten annotation, exact quotation, administrative wording, raw dataset value or source-specific exercise statement is required. Source identity and SHA-256 provenance remain in `sources/MANIFEST.tsv` and `docs/SOURCE_COVERAGE.md`.

## Final verdict

After remediation, the repository passes the strict deep-coverage audit for the **taught 2025/2026 program represented by the supplied corpus**. Future substantive course answers should retrieve the base module and, when listed in `knowledge/depth/README.md`, its depth supplement before answering.
