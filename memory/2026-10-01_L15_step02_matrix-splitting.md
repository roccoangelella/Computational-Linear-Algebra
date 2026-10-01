# Lecture 15 — Step 2: Matrix splitting

status: studied — first pass
last-updated: 2026-10-01
source_paths:
- knowledge/modules/04-stationary-iterative-methods.md
- docs/LECTURE_INDEX.md

topics studied:
- Matrix splitting provides a systematic way to obtain the fixed-point iteration x^(k+1)=B x^(k)+c from the original linear system Ax=b.
- Split A as A=M-N, with M chosen so that systems involving M are easy to solve.
- Starting from Ax=b: (M-N)x=b, hence Mx=Nx+b.
- Replacing the unknown x on the right-hand side by the current iterate x^(k) and the x on the left-hand side by the next iterate x^(k+1) gives M x^(k+1)=N x^(k)+b.
- Solving the easy M-system yields x^(k+1)=M^{-1}N x^(k)+M^{-1}b conceptually, so B=M^{-1}N and c=M^{-1}b.
- In actual computation one should solve M y=rhs rather than explicitly form M^{-1}.
- The purpose of choosing M is computational: it should approximate the useful structure of A while being cheap to solve with at every iteration.
- Different choices of M and N produce different stationary methods; Jacobi and Gauss-Seidel are later obtained by different splittings of the same A.

mastery note:
- first-pass explanation delivered; learner verification pending before moving to the spectral-radius convergence criterion.
