# Lecture 16 — Step 1: Jacobi method

status: studied — first pass
last-updated: 2026-10-02
source_paths:
- knowledge/modules/04-stationary-iterative-methods.md
- knowledge/depth/04-stationary-convergence-details.md
- docs/LECTURE_INDEX.md

topics studied:
- Jacobi is a stationary iterative method for Ax=b obtained by isolating each unknown x_i in its own row.
- From row i, a_ii x_i + sum_{j!=i} a_ij x_j=b_i, so the exact relation is x_i=(1/a_ii)[b_i-sum_{j!=i}a_ij x_j].
- Jacobi turns that exact relation into an iteration by evaluating every off-diagonal x_j on the right-hand side at the old iterate k and assigning the result to x_i^(k+1):
  x_i^(k+1)=(1/a_ii)[b_i-sum_{j!=i}a_ij x_j^(k)].
- All new components are therefore computed from the same old vector x^(k); none of the newly computed components are reused within that iteration. This makes the component updates conceptually parallel.
- The method requires a_ii != 0 for each row in the chosen ordering.
- In the course convention A=D-L-U, where D is the diagonal and -L,-U are the actual strict lower/upper parts of A. Jacobi chooses M=D and N=L+U in the generic splitting A=M-N.
- Hence D x^(k+1)=(L+U)x^(k)+b and B_J=D^{-1}(L+U).
- Example A=[[4,-1,0],[-1,4,-1],[0,-1,3]], b=(15,10,10)^T, x^(0)=0:
  x^(1)=(15/4,10/4,10/3)^T≈(3.75,2.5,3.333)^T;
  x^(2)≈(4.375,4.271,4.167)^T;
  exact solution is (5,5,5)^T.
- This example shows the iterative mechanism; convergence is not guaranteed merely because the first iterates look better. It must be justified by the iteration-matrix theory or structural sufficient conditions.

mastery note:
- first-pass Jacobi derivation delivered; learner verification pending before moving to Gauss-Seidel.
