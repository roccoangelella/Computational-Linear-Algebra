# Deep coverage audit

Date: 2026-09-11

## Purpose

This document records strict re-audits of whether the GitHub repository is sufficient to support a **deep understanding of the entire taught Computational Linear Algebra program**, not merely whether every topic name appears somewhere.

The study layer is compared against the complete supplied 91-file course corpus catalogued in `docs/SOURCE_COVERAGE.md` and `sources/MANIFEST.tsv`. Official slides/homework material are treated as highest-authority course evidence; labs/notebooks are checked for implementation detail; transcripts recover lecture explanations and handwritten-slide content; supplied external references provide secondary depth.

A fresh attached copy of the course archive was re-inventoried during the third pass on 2026-09-11. It again contained 91 source files with the same path structure as the repository manifest. Representative SHA-256 checks across the PCA specification, Krylov lab, PCA slides, general homework sheet, PageRank paper/data, Saad reference, handwritten eigenvalue slides, Krylov slides and early/late eigenvalue transcripts matched the hashes in `sources/MANIFEST.tsv`.

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

## Earlier second-pass findings and remediation

The original 13-module semantic corpus had strong breadth but the first strict comparison found real omissions. The largest missing block was polynomial interpolation: Lagrange interpolation, interpolation-error analysis, the Lebesgue constant, Weierstrass approximation, Chebyshev nodes and the Runge phenomenon.

Additional gaps were found in sparse formats/reorderings; `PA=LU`, morphism matrices and change of basis; explicit Householder/Givens QR construction; sharper Jacobi/Gauss-Seidel convergence theorems; restarted/practical GMRES; PCA cluster-validation metrics; QR eigensolver convergence assumptions; and SVD bidiagonalization details.

Those findings produced the original `knowledge/depth/` supplements for Modules 0, 2, 3, 4, 5, 6, 9, 10 and 11.

## Third-pass findings from the fresh archive

The new source-by-source comparison found that the previous audit was still too optimistic in three places.

### 1. Module 8 terminology and Householder deflation

This was the substantive remaining gap.

In the official course material, the symmetric rank-one update

`A_1 = A - lambda_1 x_1 x_1^T`

is introduced under **shifting**: it moves the known eigenvalue `lambda_1` to zero while preserving the other symmetric eigenpairs in exact arithmetic.

The course then introduces a different algorithm called **deflation**. Given a known eigenpair, a Householder matrix maps the eigenvector to the first canonical vector, and the orthogonal similarity

`B_1=P_1 A P_1^T`

isolates the known eigenvalue in the first row/column. In the symmetric case this becomes a block diagonal separation, so the computation continues recursively on a smaller trailing matrix. Reduced eigenvectors must then be transformed back through the accumulated Householder factors.

The old Module 8 used common textbook terminology in which the rank-one update was called deflation and therefore omitted the actual Householder-deflation construction taught in these lectures. It also did not explicitly preserve the symmetric power-method distinction between eigendirection convergence `O(|lambda_2/lambda_1|^k)` and Rayleigh-quotient eigenvalue convergence `O(|lambda_2/lambda_1|^(2k))`.

Remediation:

- Module 8 was rewritten to follow the course terminology explicitly while also warning about textbook naming differences.
- `knowledge/depth/08-power-shifting-householder-deflation.md` was added with the derivation, recursion, numerical comparison and eigenvector back-transformation.

### 2. Gershgorin/Lanczos details

The Gershgorin lecture explicitly applies spectral localization to estimating the 2-norm condition number of a symmetric nonsingular matrix when the disks provide both an upper spectral bound and a positive distance from zero. It also shows why the same information can fail to bound conditioning when disks touch zero even though an irreducibility argument proves nonsingularity.

The Lanczos slides also state the monotonic behavior of extreme Ritz values on nested subspaces. These results were only implicit in the previous Module 10 treatment.

Remediation: `knowledge/depth/10-eigenvalue-convergence-details.md` now contains the symmetric Gershgorin condition-number bound, its failure mode, reducibility/strong-connectivity detail, and explicit nested-subspace inequalities for extreme Ritz values.

### 3. SVD theorem proof and uniqueness

The final SVD lectures devote significant time to an existence proof by constructing the leading singular-vector pair, extending it to orthonormal bases, reducing to a smaller trailing block and applying induction. They also distinguish uniqueness of the ordered singular values from nonuniqueness of the singular-vector bases.

The previous semantic layer stated the theorem and covered its consequences/computation but did not reconstruct that proof at comparable depth.

Remediation: `knowledge/depth/11-svd-computation-details.md` now includes the variational construction of `sigma_1`, the one-step block reduction, induction, uniqueness through `A^T A`, singular-vector nonuniqueness, and the numerical bidiagonalization material already present.

## Current depth supplements

The source-indexed supplements under `knowledge/depth/` are now:

- `00-sparse-formats-operations-reorderings.md`
- `02-foundations-lu-morphisms-change-of-basis.md`
- `03-qr-construction-details.md`
- `04-stationary-convergence-details.md`
- `05-polynomial-interpolation-and-convergence.md`
- `06-krylov-projection-and-gmres-implementation.md`
- `08-power-shifting-householder-deflation.md`
- `09-pca-preprocessing-and-cluster-validation.md`
- `10-eigenvalue-convergence-details.md`
- `11-svd-computation-details.md`

`knowledge/depth/README.md` routes these supplements from their corresponding base modules.

## Module-by-module status after the third pass

| Module | Strict-depth status | Evidence/reason |
|---|---|---|
| 0 Large-scale/sparse | PASS with supplement | storage taxonomy, sparse kernels, graph/bandwidth/reordering and large-scale cost model are represented |
| 1 Python/tooling | PASS | arrays/shapes/dtypes, vectorization, sparse objects, floating point/tolerances, pandas/sklearn workflow and reproducibility are represented |
| 2 Foundations/direct methods | PASS with supplement | spaces/rank/norms/conditioning/elimination plus solvability, `PA=LU`, linear-map matrices, change of basis, similarity and Cayley-Hamilton |
| 3 Orthogonality/QR/projectors | PASS with supplement | GS/MGS, projectors/least squares plus explicit stable Householder and Givens QR construction |
| 4 Stationary iterations | PASS with supplement | splitting/error recurrence/spectral-radius criterion/residuals plus diagonal-dominance, SPD, Stein-Rosenberg and tridiagonal comparison results |
| 5 Approximation | PASS with supplement | polynomial interpolation/convergence/node choice plus least-squares geometry and QR/SVD connections |
| 6 Krylov methods | PASS with supplement | Krylov/minimal polynomial, Arnoldi/FOM/GMRES plus projection spaces, restart, complexity and practical Hessenberg QR updates |
| 7 Spectral clustering | PASS | Laplacian quadratic form/PSD, connected components, Fiedler/Rayleigh view, normalized variants, cut relaxation, spectral embedding and computational issues |
| 8 Power/shifts/deflation | PASS with supplement | power/inverse/shifted iteration, symmetric Rayleigh convergence, course rank-one shifting, Householder deflation, recursive dimension reduction and eigenvector recovery |
| 9 PCA/k-means | PASS with supplement | PCA derivation/SVD/reconstruction/current homework plus preprocessing and internal/external clustering evaluation formulas |
| 10 Gershgorin/Lanczos/QR | PASS with supplement | localization/proof, irreducibility, symmetric condition estimates, Ritz/Lanczos recurrence and monotonic bounds, finite-precision issues, QR convergence/Hessenberg/shifts/deflation |
| 11 SVD | PASS with supplement | theorem existence/uniqueness proof, geometry/subspaces/norms/Eckart-Young/pseudoinverse/least squares plus bidiagonalization and structured computation |
| 12 PageRank | PASS | stochastic construction, failure modes, teleportation/uniqueness, power iteration, convergence, sparse implementation, dataset parsing and validation |

## Cross-topic coherence check

The repository contains the prerequisite chains needed to reason across modules rather than memorize isolated algorithms. Examples:

- sparse representation -> cheap matvec -> stationary/Krylov/power/Lanczos/PageRank;
- basis/change-of-basis -> similarity -> Householder deflation and QR eigenvalue algorithms;
- orthogonality -> QR/projectors -> least squares -> Arnoldi/GMRES -> eigenvalue/SVD transformations;
- polynomial approximation -> least squares -> projection methods;
- spectral radius -> stationary convergence and power-method convergence;
- Rayleigh quotient -> power methods, spectral clustering, Lanczos and PCA;
- SVD -> conditioning, pseudoinverse, low-rank approximation and PCA.

`docs/CONCEPT_GRAPH.md` remains the global routing layer; the depth supplements ensure those edges lead to enough mathematical detail.

## Scope of “complete”

The ZIP also contains large secondary literature, most notably the full Saad iterative-methods reference and several spectral-clustering references. The repository intentionally does **not** reproduce every theorem and page of those external books/papers. It integrates the portions needed to understand the taught program and uses those references as deeper supporting literature.

Therefore the certification is for the **taught 2025/2026 Computational Linear Algebra program represented by the official slides, transcripts, labs and assessment material**, with supporting-reference material integrated where it serves that program. It is not a claim that the repository is a verbatim replacement for every supplied external reference book.

## What this audit can and cannot certify

**Certified:** after the third-pass remediation, the repository contains enough source-indexed mathematical and computational material to support deep study of the full taught program without routinely reopening the original binary PDFs. A student can use it to derive the main algorithms, state assumptions, explain convergence/numerical behavior, connect implementations to theory, reproduce the important theorem proofs emphasized in class, and prepare for the mathematical oral discussion described in the assessment material.

**Not certified:** merely reading the repository guarantees mastery or a particular grade. Deep understanding is a property of the learner, not of a document collection. It requires solving problems, reproducing derivations without looking, implementing/debugging algorithms, interpreting numerical experiments and answering oral questions. The repository is sufficient material for that process; it cannot replace the process.

## Residual reasons to consult an original source

The semantic corpus is not a byte-for-byte archive. Open/recover an original source when an exact figure, handwritten annotation, exact quotation, administrative wording, raw dataset value, complete supporting-reference proof, or source-specific exercise statement is required. Source identity and SHA-256 provenance remain in `sources/MANIFEST.tsv` and `docs/SOURCE_COVERAGE.md`.

## Final verdict

After this third-pass comparison and remediation, the repository passes the strict deep-coverage audit for the **taught 2025/2026 program represented by the supplied corpus**. Future substantive course answers should retrieve the base module and, when listed in `knowledge/depth/README.md`, its depth supplement before answering.
