# 2026-10-08 — Iterative-methods slide audit and teaching backlog

status: **source comparison completed; this is NOT a learner-mastery record**
last-updated: 2026-10-08
sources-inspected:
- user-uploaded `Lecture3-Iterative-methods (1).pdf` (32 pages; title page updated 2026-10-04)
- user-uploaded `Lecture3-Appendix-convergence_jacobi_gauss_seidel.pdf` (5 pages)
- `memory/2026-10-01_L15_step02_matrix-splitting.md`
- `memory/2026-10-01_L15_step03_spectral-radius-convergence.md`
- `memory/2026-10-02_L15_step04_norm-convergence-test.md`
- `memory/2026-10-02_L16_step01_jacobi-method.md`
- `memory/2026-09-18_L04_step14_norms.md`
- `memory/2026-09-18_L04_step15_conditioning.md`
- `memory/2026-09-18_L04_step16_residual-vs-forward-error.md`
- `knowledge/modules/04-stationary-iterative-methods.md`
- `knowledge/depth/04-stationary-convergence-details.md`

## Documented first-pass coverage
- Why sparse/large systems motivate iterations (prior lectures).
- Norms, induced matrix norms, condition numbers and residual-versus-error relation (2026-09-18).
- Starting from an initial guess, fixed-point form, matrix splitting and the iteration matrix (2026-10-01).
- Error recurrence `e^(k)=B^k e^(0)`, exact spectral-radius criterion `rho(B)<1`, and norm sufficient test `||B||<1` (2026-10-01/02).
- Jacobi componentwise update and first worked 3x3 iteration (2026-10-02).
- These are generally **first-pass explanations, not automatically verified mastery**.

## Still to teach or explicitly verify, in recommended order
1. Slide pp.5–9: convergence of vector sequences, equivalence of norms in finite dimensions, componentwise equivalence; revisit inequalities among 1-, 2-, infinity and Frobenius norms.
2. Slide pp.19, 22: asymptotic speed from spectral radius and zero diagonal/permuting rows, including effect of row ordering.
3. Slide pp.23–24: Gauss–Seidel, including full row-by-row example, lower-triangular solve and reusing newest components; compare with the same Jacobi example.
4. Slide pp.25–29: stopping by relative/absolute successive difference, residual-relative criterion, conditioning bound `||e||/||x_*|| <= kappa(A)||r||/||b||`, maximum iterations; explain their practical limitations.
5. Slide p.30 and appendix pp.1–3: strict diagonal dominance; proof for Jacobi via induced infinity norm, proof for GS by dominant eigenvector component; sufficient versus necessary hypotheses; column-dominance variant mentioned in slides.
6. Slide p.30 and appendix pp.3–5: SPD, proof of GS convergence, energy-minimization interpretation, and why SPD alone does not guarantee ordinary Jacobi convergence.
7. Slides pp.31–32: Stein–Rosenberg comparison under nonpositive off-diagonal/positive diagonal hypotheses; tridiagonal case `rho(B_GS)=rho(B_J)^2`, correct interpretation of 'twice' (asymptotic rate exponent rather than necessarily wall-clock time).
8. Cost per iteration versus iteration count, performance comparisons, and practical numerical checks, as contextualized by Module 4.

## Verified notation differences / source errata
- **Different but equivalent conventions:** source deck uses `A=M+N` and `A=D+E+F`; current repository explains `A=M-N` and `A=D-L-U`. Thus `E=-L` and `F=-U`. Explain the sign mapping explicitly; do not combine the two sets of formulas blindly.
- **Slide p.15:** final recurrence contains `...=B^k e^(1)=B^k e^(0)`; the penultimate exponent is a typo. Correct: `e^(k)=B^(k-1)e^(1)=B^k e^(0)`.
- **Slide p.16:** `B^k e^(0)->0` only implies `B^k->0` when convergence is asserted for **every** initial error, not an arbitrary single starting vector.
- **Appendix p.2:** `B_J=-D^(-1)(L+U)` uses symbols L and U that the appendix never defined; under its `A=D+E+F` convention, write `B_J=-D^(-1)(E+F)`.
- **Appendix p.4:** phrase 'Since L is real' should refer to `E`; the proof correctly uses `v* E^T v = conjugate(v* E v)`.
- **Slide p.32:** 'double convergence speed' expresses the tridiagonal asymptotic rate `rho(B_GS)=rho(B_J)^2`, not a universal halving of runtime.
- **Slide p.6 (minor):** equivalence-of-norm constants should be specified as positive `m,M>0`.

## Next learner-facing action
Begin with the missing norm-equivalence/convergence preliminaries in a short grounded example, then teach Gauss–Seidel with the exact 3x3 matrix used for Jacobi. Do not mark this review itself as mastery. After actual study interactions, append dated verified/first-pass records as appropriate.
