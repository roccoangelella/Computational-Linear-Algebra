# Lecture 04 — Step 15: Conditioning and condition number

status: studied
last-updated: 2026-09-18
source_paths:
- `knowledge/modules/02-linear-algebra-and-direct-methods.md`
- `docs/COURSE_MAP.md`

topics studied:
- conditioning as sensitivity of the mathematical problem to perturbations in the input data;
- distinction between conditioning of a problem and numerical stability of an algorithm;
- for an invertible square matrix and a compatible induced norm, `kappa(A)=||A|| ||A^{-1}||`;
- `kappa(A) >= 1` for induced norms;
- interpretation: `||A||` measures maximum forward amplification while `||A^{-1}||` measures amplification when mapping data perturbations back to solution perturbations;
- relative perturbation bound for fixed `A`: `||delta x||/||x|| <= kappa(A) ||delta b||/||b||`;
- condition number near 1 means the linear solve is well-conditioned in that norm; a large condition number means relative input perturbations may be greatly amplified;
- example `A=diag(1,0.01)` has `kappa_2(A)=100`, showing strong sensitivity in the second coordinate;
- in the 2-norm, `kappa_2(A)=sigma_max(A)/sigma_min(A)`, to be derived later with the SVD;
- an exactly singular matrix has infinite condition number under the usual convention;
- geometric interpretation: ill-conditioned matrices strongly compress some direction, so inversion must strongly expand it;
- conditioning does not imply that every perturbation is amplified by the full condition number; the condition number is a worst-case sensitivity measure.

mastery note:
- first-pass explanation delivered; learner confirmation to be checked before assuming full mastery.
