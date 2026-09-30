# Lecture 12 — Clarification: QR when A is rank-deficient

status: clarification delivered — verification pending
last-updated: 2026-09-30
source_paths:
- knowledge/modules/03-orthogonality-qr-projectors-least-squares.md
- knowledge/modules/05-approximation-and-least-squares.md

topics clarified:
- A QR factorization can still exist when A is rank-deficient.
- What fails is the simple full-column-rank least-squares pipeline in which Q spans exactly Im(A), R is invertible, and Rx=Q^Tb has a unique solution.
- If rank(A)=r<n, then R is singular and the least-squares coefficient vector need not be unique.
- The fitted vector Ax_* (orthogonal projection of b onto Im(A)) can still be unique even when the coefficient vector x_* is not.
- In a rank-revealing/pivoted QR treatment, one identifies an orthonormal basis Q_r for the actual r-dimensional image of A and projects with Q_r Q_r^T.
- The later SVD/pseudoinverse treatment gives the canonical minimum-norm least-squares solution for rank-deficient problems.

mastery note:
- clarification delivered; learner verification pending.
