# Lecture 5 — Krylov solving versus space saturation

status: explained; independent comprehension not yet verified
last-updated: 2026-10-20
source_paths: knowledge/modules/06-krylov-arnoldi-fom-gmres.md; knowledge/depth/06-krylov-projection-and-gmres-implementation.md; uploaded Lecture5-KrylovSpaces.pdf slides 4-14 and FOM/GMRES sections

Clarification: We do NOT usually generate raw Krylov vectors until a new one is linearly dependent and only then solve. Each iteration enlarges a search space; FOM selects coefficients through Galerkin residual orthogonality, while GMRES minimizes residual norm. Check convergence and stop when accurate enough, often long before saturation. If a new direction becomes exactly dependent, the space is invariant (Arnoldi happy breakdown), and for nonsingular A the exact correction belongs to that Krylov space in exact arithmetic.

Original example A=[[4,1],[1,3]], b=[1,2], x0=0: K1=span(b) gives approximate x1; K2=span(b,Ab) already equals R2 and contains exact solution [1/11,7/11]. A2b=7Ab-11b only proves a third direction adds no information; explicitly computing this polynomial dependence is a theoretical illustration and not usual FOM/GMRES procedure.

Understanding not yet independently checked.