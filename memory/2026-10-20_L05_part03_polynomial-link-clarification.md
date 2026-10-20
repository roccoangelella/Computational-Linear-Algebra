# Lecture 5 Part 3 — Why minimal polynomials are relevant to Krylov methods

status: explained; learner comprehension pending
last-updated: 2026-10-20
source_paths: user-uploaded Lecture5-KrylovSpaces.pdf slides 6-10; knowledge/modules/06-krylov-arnoldi-fom-gmres.md

Learner raised a critical explanation gap: the matrix minimal polynomial q(A)=0 was introduced without explaining its relationship to the Krylov approximation polynomial p_(m-1)(A). The two polynomials serve different roles but are algebraically linked.

The link is: for nonsingular A, an annihilating polynomial q(t)=t^d+...+c0 with c0 nonzero yields an identity for A inverse as a polynomial of degree at most d-1. Then the exact solution is A inverse times b, hence belongs to the Krylov span of b, Ab, ..., A^(d-1)b. For nonzero initial guess, replace b with r0 and write x*=x0+A inverse r0. This explains the significance of the polynomial, rather than introducing it as an isolated theorem.

Concrete example: A=[[4,1],[1,3]], b=[1,2]. The minimal polynomial q(t)=t^2-7t+11 satisfies q(A)=0. Rearrangement gives A inverse=(7I-A)/11. Thus p1(t)=(7-t)/11 gives x*=p1(A)b=(7b-Ab)/11. q and p1 are different polynomials linked by the inverse identity.

Do not claim that the learner has mastered this until independently checked.
