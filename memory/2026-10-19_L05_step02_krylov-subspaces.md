# Lecture 5 Part 2 — Krylov subspaces

status: studied; comprehension pending
last-updated: 2026-10-19
source_paths: uploaded Lecture5-KrylovSpaces.pdf slides 4-5; knowledge/modules/06-krylov-arnoldi-fom-gmres.md

Studied topics:
- Initial residual r0=b-Ax0.
- Krylov space K_m(A,r0)=span(r0,Ar0,...,A^(m-1)r0).
- Generate successive directions with sparse matrix-vector products.
- Nested spaces, linear independence and dimension.
- Polynomial representation: any correction equals p(A)r0 for a polynomial degree at most m-1.
- Example A=[[4,1],[1,3]], b=[1,2]: Ab=[6,7], independent from b. The exact solution can be written (7b-Ab)/11.
- A space construction alone does not choose approximation coefficients; later projection methods determine them.

Understanding not yet independently checked. Next: minimal polynomials, slides 6-10.
