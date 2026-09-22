# Lecture 09 — Step 3: QR factorization meaning

status: studied — first pass
last-updated: 2026-09-22
source_paths:
- knowledge/modules/03-orthogonality-qr-projectors-least-squares.md
- knowledge/depth/03-qr-construction-details.md

topics studied:
- For A in R^(m x n) with m>=n and full column rank, a thin QR factorization writes A=QR.
- Q in R^(m x n) has orthonormal columns; its columns form an orthonormal basis for the same column space as A.
- R in R^(n x n) is upper triangular and stores the coefficients needed to reconstruct each original column a_j from q_1,...,q_j.
- The purpose of QR is to separate the geometry of the column space (Q) from the coordinate/reconstruction information (R), without changing the subspace represented by A.
- In Gram-Schmidt, a_1=r_11 q_1; a_2=r_12 q_1+r_22 q_2; in general a_j=sum_{i<=j} r_ij q_i. Because column j uses only q_1 through q_j, coefficients below the diagonal are zero, hence R is upper triangular.
- Worked example: a_1=(1,1)^T, a_2=(1,0)^T. Then q_1=(1/sqrt(2))(1,1)^T, q_2=(1/sqrt(2))(1,-1)^T, r_11=sqrt(2), r_12=1/sqrt(2), r_22=1/sqrt(2), giving Q=(1/sqrt(2))[[1,1],[1,-1]] and R=[[sqrt(2),1/sqrt(2)],[0,1/sqrt(2)]], with QR=A.
- The previous example a_1=(1,0)^T, a_2=(1,1)^T is a special case where Gram-Schmidt returns the standard basis, so Q=I and R=A.

mastery note:
- First-pass conceptual explanation delivered; learner verification is still required before assuming full mastery.
