# Lecture 15 — Step 3: Spectral-radius convergence criterion

status: studied — first pass
last-updated: 2026-10-01
source_paths:
- knowledge/modules/04-stationary-iterative-methods.md
- knowledge/depth/04-stationary-convergence-details.md

topics studied:
- For the stationary iteration x^(k+1)=B x^(k)+c, the error satisfies e^(k)=B^k e^(0).
- Therefore convergence for every initial guess means B^k e^(0) -> 0 for every initial error e^(0), equivalently B^k -> 0.
- An eigenvector v of B is a nonzero vector whose direction is preserved by B: Bv=lambda v. The scalar lambda is the corresponding eigenvalue.
- Repeated multiplication gives B^k v=lambda^k v, so along an eigenvector direction the error magnitude is controlled by |lambda|^k.
- If |lambda|<1, that component decays; if |lambda|>1, it grows; if |lambda|=1, it generally does not decay.
- The spectral radius is rho(B)=max_i |lambda_i(B)|, i.e. the largest magnitude among all eigenvalues.
- The exact convergence criterion is rho(B)<1: the stationary iteration converges to the fixed point for every initial guess exactly when every eigenvalue of B lies strictly inside the unit disk.
- “Unit disk” means the set of complex numbers z with |z|<1.
- A sufficient but not necessary condition is ||B||<1 for a consistent/submultiplicative matrix norm, because rho(B)<=||B||.

example used:
- For B=diag(1/2,-1/4), B^k e^(0) scales the two eigendirections by (1/2)^k and (-1/4)^k, so every error goes to zero and rho(B)=1/2<1.
- If one diagonal entry were 1.2 instead, an error component in that eigendirection would grow like 1.2^k and the method would fail for generic initial guesses.

mastery note:
- first-pass explanation delivered; learner verification pending before assuming spectral-radius convergence criterion is mastered.
