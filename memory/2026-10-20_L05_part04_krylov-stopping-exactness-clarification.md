# Lecture 5 — Krylov dependence, saturation, and exact solution

status: explained; comprehension unverified
last-updated: 2026-10-20

source_paths:
- user-uploaded Lecture5-KrylovSpaces.pdf, slides 4–14
- knowledge/modules/06-krylov-arnoldi-fom-gmres.md
- knowledge/depth/06-krylov-projection-and-gmres-implementation.md

Topics discussed:
- For A=[[4,1],[1,3]] and b=[1,2], vectors b=[1,2] and Ab=[6,7] are independent and span R2. Therefore A2b=[31,27] must be their linear combination; this does not hold for the third Krylov vector in an arbitrary larger-dimensional space.
- Solve A2b=c Ab+d b: c=7, d=-11; rearrange A2b-7Ab+11b=0 and A(7b-Ab)=11b, so x*=(7b-Ab)/11=[1/11,7/11]. We solve for coefficients in the vector relationship, not for the known b.
- Verify Ax*=b exactly; det(A)=11 != 0 so the solution is unique. Contrast exact solution x* with iterative approximation x_m.
- Once a new Krylov vector is in the previous span, subsequent powers remain in that span. For example A3b=7A2b-11Ab, reducible to b, Ab, so creating a fourth vector adds no information.
- In general stop either when true residual is zero (exact arithmetic) or below a tolerance (practical floating-point algorithm), or the Krylov space saturates. The polynomial derivation explains theory, not the usual algorithm: FOM or GMRES determine coefficients via projected conditions without explicitly computing minimal polynomials.
- Differentiate searching with K2 (already contains exact solution) from producing A2b to prove dependence.

User understanding still not independently checked.