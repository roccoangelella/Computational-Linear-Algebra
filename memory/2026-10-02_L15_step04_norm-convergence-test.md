# Lecture 15 — Step 4: Norm-based sufficient convergence test

status: studied — first pass
last-updated: 2026-10-02
source_paths:
- knowledge/modules/02-linear-algebra-and-direct-methods.md
- knowledge/modules/04-stationary-iterative-methods.md
- knowledge/depth/04-stationary-convergence-details.md

topics studied:
- A matrix norm measures the size/stretching effect of a linear operator; for an induced norm, ||B||=max_{x!=0} ||Bx||/||x||.
- From the stationary error relation e^(k)=B^k e^(0), submultiplicativity gives ||e^(k)|| <= ||B||^k ||e^(0)||.
- Therefore, if ||B||<1, the factor ||B||^k tends to zero and every initial error is forced to zero.
- Thus ||B||<1 is a sufficient convergence condition.
- The spectral-radius condition rho(B)<1 remains the exact necessary-and-sufficient criterion.
- Since rho(B)<=||B|| for any consistent/submultiplicative matrix norm, ||B||<1 immediately implies rho(B)<1.
- The norm condition is not necessary: a chosen matrix norm may exceed 1 even though all eigenvalues have modulus below 1 and B^k still tends to zero.
- Practical interpretation: a norm bound below 1 proves the iteration is a contraction in that norm, but failure of the norm test does not prove divergence.

mastery note:
- first-pass explanation delivered; learner verification pending before moving to Jacobi.
