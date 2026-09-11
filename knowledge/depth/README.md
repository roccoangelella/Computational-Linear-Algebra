# Depth supplements

The 13 files in `knowledge/modules/` remain the main study sequence. This directory contains targeted supplements added after strict comparisons against the official slides, transcripts and labs. A supplement exists only where the base module was found to omit material needed for a genuinely deep reconstruction of the taught program.

## Supplements

| Base module | Supplement | Why it exists |
|---|---|---|
| Module 0 | `00-sparse-formats-operations-reorderings.md` | DOK/LIL/MSR/diagonal/ELL formats, sparse operations, bandwidth, Cuthill-McKee and independent-set ordering |
| Module 2 | `02-foundations-lu-morphisms-change-of-basis.md` | Rouché-Capelli, `PA=LU`, coordinate/morphism matrices, change of basis, similarity, diagonalization and Cayley-Hamilton |
| Module 3 | `03-qr-construction-details.md` | explicit Householder/Givens constructions and QR algorithms |
| Module 4 | `04-stationary-convergence-details.md` | diagonal-dominance/SPD results, Stein-Rosenberg and tridiagonal Jacobi/GS comparison |
| Module 5 | `05-polynomial-interpolation-and-convergence.md` | Lagrange interpolation, Lebesgue constant, Weierstrass, Chebyshev nodes and Runge phenomenon |
| Module 6 | `06-krylov-projection-and-gmres-implementation.md` | search/test spaces, restarted FOM/GMRES, cost growth and incremental Givens QR |
| Module 8 | `08-power-shifting-householder-deflation.md` | symmetric power convergence, course-specific rank-one “shifting”, Householder deflation, recursive reduction and eigenvector recovery |
| Module 9 | `09-pca-preprocessing-and-cluster-validation.md` | scaling/encoding, k-means geometry, Davies-Bouldin, inertia and silhouette analysis |
| Module 10 | `10-eigenvalue-convergence-details.md` | Gershgorin nonsingularity/conditioning, nested Ritz bounds, Ritz residuals, QR convergence assumptions, Hessenberg/shift/deflation details |
| Module 11 | `11-svd-computation-details.md` | SVD existence/uniqueness proof, left/right Householder bidiagonalization and structured SVD computation |

Modules 1, 7 and 12 pass the strict depth comparison without a separate supplement: their main modules already contain the course-relevant depth needed for the taught program. This does not mean no external reference could add further theory; it means no substantive official-course gap remains in those modules after the current audit.

## Retrieval rule

When studying a module that has a supplement, read the main module first, then its supplement. The main module establishes the conceptual spine; the supplement restores details that would otherwise be easy to miss when the original slides/notebooks are not open.

`docs/DEEP_COVERAGE_AUDIT.md` records the audit standard, gaps found, remediation and remaining limitations.
