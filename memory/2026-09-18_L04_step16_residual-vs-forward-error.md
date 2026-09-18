# Lecture 04 — Step 16: Residual versus forward error

status: studied
last-updated: 2026-09-18
source_paths:
- `knowledge/modules/02-linear-algebra-and-direct-methods.md`

topics studied:
- exact solution `x_*` satisfies `A x_* = b`;
- an approximation `x` has forward error `e = x - x_*`;
- its residual is `r = b - A x`;
- with this sign convention, `r = -A e` and, for invertible `A`, `e = -A^{-1} r`;
- residual measures how well the computed vector satisfies the equations, while forward error measures how close it is to the true solution;
- norm bound `||e|| <= ||A^{-1}|| ||r||`;
- relative bound `||e||/||x_*|| <= kappa(A) ||r||/||b||` for compatible induced norms;
- therefore a small residual guarantees a small forward error only when the problem is sufficiently well-conditioned;
- example `A = diag(1, 10^{-8})`, exact `x_*=(1,1)^T`, approximate `x=(1,0)^T`: residual has norm `10^{-8}` while the solution error has norm `1`;
- geometric reason: an ill-conditioned matrix can strongly compress an error direction, making a large error nearly invisible in the residual;
- practical lesson: residual checks are essential but should be interpreted together with conditioning/scaling rather than as direct proof of solution accuracy.

mastery note:
- first-pass explanation delivered; learner confirmation to be checked before assuming full mastery.
