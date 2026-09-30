# Lecture 12 — Step 3 review: conditioning and least squares through QR

status: review delivered — verification pending
last-updated: 2026-09-30
source_paths:
- knowledge/modules/02-linear-algebra-and-direct-methods.md
- knowledge/modules/03-orthogonality-qr-projectors-least-squares.md
- knowledge/depth/03-qr-construction-details.md

topics reviewed:
- Conditioning measures sensitivity of a mathematical problem to perturbations; in the 2-norm, kappa_2(A)=||A||_2||A^{-1}||_2=sigma_max(A)/sigma_min(A) for an invertible square matrix, with the analogous singular-value ratio used for full-column-rank rectangular least-squares matrices.
- A large condition number means small perturbations/rounding can be strongly amplified in the computed solution.
- Forming the normal-equation matrix A^T A squares the 2-norm condition number: kappa_2(A^T A)=kappa_2(A)^2 for full-column-rank A. Thus the normal-equations route can make an already sensitive least-squares problem substantially more sensitive numerically.
- Least squares seeks x_* minimizing ||Ax-b||_2 for an inconsistent/overdetermined system.
- Im(A)=Col(A) is the set of all attainable vectors Ax.
- Ax_* is the orthogonal projection of b onto Im(A); the residual r_*=b-Ax_* lies in Im(A)^perp.
- Residual orthogonality gives A^T(b-Ax_*)=0 and therefore the normal equations A^T A x_*=A^T b.
- Thin QR factorization A=QR replaces the original basis of Im(A) by orthonormal columns Q while R records the coordinate conversion.
- Because Q^T Q=I and Im(Q)=Im(A), projection coordinates are Q^T b and the least-squares coefficients satisfy R x_*=Q^T b.
- R is upper triangular, so the final solve is performed by back substitution.
- QR avoids explicitly forming A^T A and is therefore generally numerically preferable to the normal-equations route.
- Householder QR is the standard robust dense construction; Givens is useful for selective/sparse eliminations.

mastery note:
- This session is a recovery/review after time away from the topic. Do not mark the QR least-squares step verified until the learner explicitly demonstrates or confirms the conceptual chain, especially the role of Q^T b and R.
