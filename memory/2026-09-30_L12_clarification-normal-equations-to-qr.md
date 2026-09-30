# Lecture 12 — Clarification: from normal equations to QR least-squares equation

status: clarification delivered — verification pending
last-updated: 2026-09-30
source_paths:
- knowledge/modules/03-orthogonality-qr-projectors-least-squares.md

clarification:
- Start from the normal equations A^T A x_* = A^T b.
- Substitute the thin QR factorization A=QR, so A^T=R^T Q^T.
- Then (R^T Q^T)(Q R)x_* = R^T Q^T b.
- Since Q has orthonormal columns, Q^T Q=I, giving R^T R x_* = R^T Q^T b.
- If A has full column rank, R is invertible, hence R^T is invertible. Left-multiplying by (R^T)^{-1} gives R x_* = Q^T b.
- Multiplying this last equation by Q gives Q R x_* = Q Q^T b, i.e. A x_* = Q Q^T b.
- Therefore QRx_*=QQ^Tb is not a mysterious direct algebraic rewrite of A^TAx_*=A^Tb; it comes either by the above sequence or directly from the geometric statement that Ax_* is the orthogonal projection of b onto Im(A)=Im(Q).

mastery note:
- learner explicitly identified the missing algebraic bridge; verification pending after explanation.
