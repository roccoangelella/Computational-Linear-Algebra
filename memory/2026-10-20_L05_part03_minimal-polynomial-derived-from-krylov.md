# Lecture 5 — Rebuilding the polynomial example from A and b

status: studied — clarification given; not yet independently verified
last-updated: 2026-10-20

source_paths:
- user-uploaded Lecture5-KrylovSpaces.pdf, slides 4–10
- knowledge/modules/06-krylov-arnoldi-fom-gmres.md
- knowledge/depth/06-krylov-projection-and-gmres-implementation.md

Learner reported a serious earlier explanation gap: the polynomial q(t)=t^2-7t+11 was introduced without deriving it from the original A and b. Do not start such examples with an unexplained polynomial.

Reconstruct the example strictly in this order:
1. Start A=[[4,1],[1,3]], b=[1,2], x0=0, r0=b.
2. Generate Krylov vectors b=[1,2], Ab=[6,7], A^2b=[31,27]. The first two vectors are independent in R^2.
3. As the third lies in the two-dimensional span, solve A^2b=u Ab+v b: 31=6u+v, 27=7u+2v; obtain u=7 and v=-11.
4. Rearrange A^2b-7Ab+11b=0, yielding q_b(A)b=0 with q_b(t)=t^2-7t+11. Emphasize that, in general, annihilating b need not imply q_b(A)=0.
5. For this example verify A^2=[[17,7],[7,10]] and A^2-7A+11I=0, so q is also the degree-two minimal polynomial of A. Its equality to det(tI-A) follows by direct characteristic-polynomial calculation and agrees with Cayley–Hamilton.
6. Rearrange A(7b-Ab)=11b, so x=(7b-Ab)/11=[1/11,7/11]. This is a vector in K_2(A,b), namely x=p_1(A)b, p_1(t)=(7-t)/11. Thus q produces the dependence relation; p_1 represents the exact solution.
7. Explain the general motivation: minimal polynomial bounds Krylov growth and the inverse of nonsingular A has a polynomial representation; actual Krylov solvers seek approximation coefficients without calculating the minimal polynomial.

No independent comprehension check has been passed yet.