# Lecture 12 — Step 3: Least squares through QR

status: studied — first pass
last-updated: 2026-09-25
source_paths:
- knowledge/modules/03-orthogonality-qr-projectors-least-squares.md
- knowledge/depth/03-qr-construction-details.md

topics studied:
- For a full-column-rank matrix A with thin QR factorization A=QR, Q has orthonormal columns spanning the same column space as A and R is upper triangular.
- Replacing A by QR does not change the set of attainable vectors Ax; it only changes the coordinates used to describe the same column space.
- The least-squares projection Ax_* can be written as Q(Rx_*).
- Because Q is an orthonormal basis for Im(A), the coordinates of the projection of b in that basis are Q^T b.
- Therefore the least-squares coefficients satisfy R x_* = Q^T b.
- Solving least squares through QR reduces the problem to an upper-triangular solve after QR factorization.
- This avoids explicitly forming A^T A, whose 2-norm condition number is kappa_2(A)^2 when A has full column rank.
- Running line-fitting example: A=[[1,0],[1,1],[1,2]], b=(1,2,2)^T. A thin QR obtained by Gram-Schmidt has q1=(1,1,1)^T/sqrt(3), q2=(-1,0,1)^T/sqrt(2), R=[[sqrt(3),sqrt(3)],[0,sqrt(2)]]. Then Q^T b=(5/sqrt(3),1/sqrt(2))^T and triangular solution gives c1=1/2, c0=7/6, matching the normal-equations solution.

mastery note:
- first-pass explanation delivered; learner verification still required, especially the interpretation of Q^T b as projection coordinates and R as the conversion from orthonormal-basis coordinates back to coefficients in the original columns of A.
