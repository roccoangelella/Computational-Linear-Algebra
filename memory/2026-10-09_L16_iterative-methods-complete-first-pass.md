# 2026-10-09 — Iterative Methods Lecture 3 and Appendix: full first-pass explanation

status: **explained in conversation — understanding NOT YET VERIFIED**
last-updated: 2026-10-09
source_paths:
- user-uploaded `Lecture3-Iterative-methods (1).pdf`, 32 slides, dated 2026-10-04
- user-uploaded `Lecture3-Appendix-convergence_jacobi_gauss_seidel.pdf`, 5 pages
- `knowledge/modules/04-stationary-iterative-methods.md`
- `knowledge/depth/04-stationary-convergence-details.md`
- `memory/2026-10-02_L16_step01_jacobi-method.md`
- `memory/2026-10-08_iterative-methods-slides-gap-audit.md`

## Topics explained on this date (first pass)
1. Vector-sequence convergence via norm of error; finite-dimensional equivalence of norms; componentwise convergence; 1-, 2-, infinity norms and Frobenius norm, with their purposes and comparison inequalities.
2. Difference between exact convergence criterion `rho(B)<1`, sufficient induced-norm bound `||B||<1`, and asymptotic convergence speed; scalar sample factors 0.2 and 0.9.
3. Gauss–Seidel: precise new-versus-old component usage, source splitting `A=D+E+F`, relation `(D+E)x_new=b-Fx_old`, iteration matrix `B_GS=-(D+E)^(-1)F`, and triangular solve without explicit inversion.
4. Worked numerical comparison on the original Jacobi system `A=[[4,-1,0],[-1,4,-1],[0,-1,3]], b=(15,10,10), x0=(0,0,0)`, exact `x*=(5,5,5)`. GS sweep 1: `(3.75,3.4375,4.4791667)`; sweep 2: `(4.609375,4.7721354,4.9240451)`. Jacobi sweep 1: `(3.75,2.5,3.3333333)`; sweep 2: `(4.375,4.2708333,4.1666667)`.
5. Zero diagonal and row reordering, nonzero diagonal as a definability/applicability rather than convergence condition.
6. Absolute and relative successive-iterate change, residual-based stopping and residual-versus-error conditioning inequality `||e||/||x*|| <= kappa(A) ||r||/||b||` for b != 0; failure modes; maximum iteration safeguards.
7. Strict row diagonal dominance definition and proof of Jacobi via infinity-norm bound; Gauss–Seidel proof via largest-magnitude eigenvector component and contradiction; column diagonal dominance guarantee; strong versus weak / sufficient versus necessary.
8. SPD definition and role; Gauss–Seidel SPD eigenvalue proof with `d=v*Dv`, `ell=v*Ev`, `|d+ell|^2-|ell|^2=(v*Dv)(v*Av)>0`; energy minimization `Phi(x)=0.5 x^T A x - b^T x` / coordinate-descent perspective. Counterexample SPD-but-Jacobi-not-convergent: A with diag 3 and every off-diagonal 2, eigenvalue -4/3 for B_J.
9. Stein–Rosenberg alternatives under positive diagonal/nonpositive off-diagonal hypotheses.
10. Tridiagonal positive-diagonal theorem `rho(B_GS)=rho(B_J)^2`, explicit calculation on same 3x3 example: `rho(B_J)=sqrt(7/48)`, `rho(B_GS)=7/48`; asymptotic rate is not wall-clock time.
11. Sparse-sweep work model, sequential-vs-parallel tradeoffs, why the same accuracy target and total costs matter.

## Teaching notes / future verification
- This was a long written explanation in response to request to explain *all* missing topics. None of the new material has been independently re-derived by the learner yet; do not upgrade to verified or mastered.
- Highest-priority active-recall checkpoints: reproduce GS sweep 1 without looking; explain why GS uses new x1 during x2 update; compute `||B_J||_infinity` and use strict dominance; distinguish absolute step change from residual/true error; explain why SPD implies GS but not Jacobi; explain squared spectral-radius comparison.
- Appendix notation errors flagged in 2026-10-08 audit remain; use `E,F` sign convention from the new slides rather than mixing with repository `D-L-U`.
- The deck states tridiagonal comparison under positive diagonal, so retain those assumptions when attributing the theorem to the slides.
