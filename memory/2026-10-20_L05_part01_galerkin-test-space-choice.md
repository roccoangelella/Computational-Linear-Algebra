# Lecture 5 — Choice of search and test spaces: FOM versus GMRES

status: clarification explained; comprehension not yet independently verified
last-updated: 2026-10-20
source_paths:
- uploaded Lecture5-KrylovSpaces.pdf: slides 2–4, 25, 30–32
- knowledge/depth/06-krylov-projection-and-gmres-implementation.md
- knowledge/modules/06-krylov-arnoldi-fom-gmres.md

Learner challenged an unjustified choice in the numerical example: K=L=span(b) was used to produce x1=b/4 without first explaining that this is a particular Galerkin/FOM projection rule rather than a requirement of the Krylov construction.

Clarification:
- A Krylov space K defines allowed correction directions, not which correction coefficients to choose.
- Test space L is a deliberate method choice, usually of equal dimension to K; r is required orthogonal to L.
- Galerkin/FOM: choose L=K. For SPD A this corresponds to minimizing quadratic energy on x0+K, rather than minimizing the Euclidean residual directly.
- GMRES: choose L=AK, yielding residual 2-norm minimization for the nonsingular case.
- For A=[[4,1],[1,3]], b=[1,2], x0=0, K=span(b), candidate x=alpha b, Ab=[6,7]. Galerkin: b dot (b-alpha Ab)=0, alpha=(b dot b)/(b dot Ab)=5/20=1/4. GMRES: (Ab) dot (b-alpha Ab)=0, alpha=(Ab dot b)/(Ab dot Ab)=20/85=4/17. Both stay in the same Krylov search space; only the residual criterion differs.

Do not mark as mastered without learner confirmation.