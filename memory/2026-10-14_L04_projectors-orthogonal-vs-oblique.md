# 2026-10-14 — General projectors, second step: orthogonal versus oblique

status: **explained in conversation — learner comprehension not yet verified**
last-updated: 2026-10-14
source_paths:
- user-uploaded `Lecture4-Ortogonalization.pdf` (slides 39–42)
- `knowledge/modules/03-orthogonality-qr-projectors-least-squares.md`
- `memory/2026-10-14_L04_projector-image-kernel-first-step.md`

## Topic explained
- For any projector `P^2=P`, image `M=Im(P)` is the target subspace and kernel `S=ker(P)` is the along-direction: `x=Px+(x-Px)`, with `x-Px ∈ S`.
- Orthogonal projector: `ker(P)=Im(P)^perp`; thus residual is perpendicular to target, and output minimizes Euclidean distance to target. In real matrices, its symmetric/idempotent characterization is `P^T=P, P^2=P`.
- Oblique projector: residual lies in complementary direction `S` that need not equal `M^perp`; general oblique projectors remain idempotent but are generally not symmetric.
- Example with same target `M=span((1,0))` and input `x=(2,3)`:
  - orthogonal `P_orth=[[1,0],[0,0]]`: `Px=(2,0)`, residual `(0,3)`, kernel `span((0,1))`, distance 3;
  - oblique `P_obl=[[1,1],[0,0]]`: `Px=(5,0)`, residual `(-3,3)`, kernel `span((-1,1))`, distance `sqrt(18)`;
  - same image, different kernel => different projection result.
- Check perpendicularity by inner product with target direction (1,0), giving 0 for orth residual and -3 for oblique residual.
- Symmetry diagnostic: `P_orth^T=P_orth`; `P_obl^T ≠ P_obl`.
- Distinguish orthogonal *projector* from an orthogonal *matrix*: projectors generally shrink/eliminate components and are noninvertible; orthogonal matrices preserve norms/invertibility.
- Next topic: derive slide 43 oblique projection formula `P=V(W^T V)^{-1}W^T`; projector eigenvalues follow.

## Mastery
User had requested to continue without answering the previous first-step checkpoint. Do not mark understanding as independently verified; verify when the learner is ready.
