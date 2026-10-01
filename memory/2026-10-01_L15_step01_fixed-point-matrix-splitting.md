# Lecture 15 — Step 1: Why iterative solvers; fixed-point form and matrix splitting

status: studied — first pass
last-updated: 2026-10-01
source_paths:
- knowledge/modules/04-stationary-iterative-methods.md
- knowledge/depth/04-stationary-convergence-details.md
- docs/LECTURE_INDEX.md

topics studied:
- Motivation for iterative linear solvers: for large sparse systems, direct factorizations can require excessive work/memory and can create fill-in; an approximate solution may be sufficient.
- An iterative method starts from a guess x^(0) and generates x^(1),x^(2),... with the goal x^(k) -> x_* satisfying Ax_*=b.
- A stationary linear iteration has fixed matrices/vectors B,c and the form x^(k+1)=B x^(k)+c.
- A fixed point x_* is a vector unchanged by the iteration: x_*=B x_*+c.
- Matrix splitting writes A=M-N, choosing M so systems with M are easy to solve.
- From (M-N)x=b, rearrange to Mx=Nx+b and define the iteration M x^(k+1)=N x^(k)+b.
- Equivalently x^(k+1)=M^{-1}N x^(k)+M^{-1}b, but in computation one solves systems with M rather than explicitly forming M^{-1}.
- The iteration matrix is B=M^{-1}N and c=M^{-1}b.
- If the iteration converges to some limit x_*, taking the limit in Mx^(k+1)=Nx^(k)+b gives (M-N)x_*=b, hence Ax_*=b; therefore any converged fixed point is the original linear-system solution.
- Preview example with A=[[4,1],[2,3]], b=(1,2)^T and M=diag(4,3): updates become x1^(k+1)=(1-x2^(k))/4 and x2^(k+1)=(2-2x1^(k))/3. This splitting is the Jacobi choice, to be studied next.

mastery note:
- first-pass explanation delivered; learner verification still required before marking mastery.
