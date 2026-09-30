# Lecture 12 — Clarification: why QR projection is numerically healthier; full column rank and invertibility of R

status: clarification delivered — verification pending
last-updated: 2026-09-30
source_paths:
- knowledge/modules/02-linear-algebra-and-direct-methods.md
- knowledge/modules/03-orthogonality-qr-projectors-least-squares.md
- knowledge/depth/03-qr-construction-details.md

topics clarified:
- The projector A(A^T A)^{-1}A^T and the QR projector QQ^T are mathematically identical when A has full column rank and A=QR is a thin QR factorization.
- QR is numerically preferable because it avoids explicitly forming A^T A, whose 2-norm condition number is squared relative to A, and avoids solving a system built from that worsened normal matrix.
- Orthogonal transformations preserve Euclidean norms, so applying Q or Q^T does not itself amplify 2-norm perturbations.
- In practical QR least squares, one normally computes c=Q^T b and solves Rx=c rather than explicitly forming QQ^T.
- Full column rank for A in R^{m x n}, m>=n, means rank(A)=n: all n columns are linearly independent. Equivalently, Ax=0 implies x=0.
- In thin QR, Q has orthonormal columns and R is n x n upper triangular. Since A=QR and Q^T Q=I, ker(A)=ker(R).
- Therefore full column rank of A implies ker(R)={0}. A square matrix with trivial kernel is invertible, so R is invertible; for triangular R this is equivalent to all diagonal entries being nonzero.
- If A is rank deficient, R is singular and the least-squares minimizer is generally not unique; pivoted QR or SVD/pseudoinverse methods are then needed for a robust rank-aware solution.

numerical illustration:
- For A=[[1,1],[1,1+1e-6],[1,1-1e-6]], kappa_2(A) is about 2.45e6 while kappa_2(A^T A) is about 6.0e12.
- With b chosen from the exact model x=(1,1), a QR/SVD-based least-squares solve recovers approximately (1,1), while direct normal equations in double precision show visible coefficient error (~2.22e-4 in opposite directions). With perturbation 1e-8 in the second column, A^T A becomes numerically singular in this experiment.

mastery note:
- Learner requested explicit conceptual and numerical explanation; verification pending.
