# 2026-10-14 — General projectors, first step: image, kernel and direct-sum decomposition

status: **explained in conversation — learner comprehension not yet verified**
last-updated: 2026-10-14
source_paths:
- user-uploaded `Lecture4-Ortogonalization.pdf` (slides 37–40)
- `knowledge/modules/03-orthogonality-qr-projectors-least-squares.md`
- `memory/2026-10-14_L04_orthogonalization-slide-gap-audit.md`

## Material explained

- Definition of projector: `P^2=P`, equivalently projecting twice changes nothing.
- Every projector has target subspace `Im(P)`, defined as all outputs `Px`; and kernel `ker(P)`, defined by `Px=0`, the directions collapsed to zero.
- General projectors do not have to be orthogonal (symmetric).
- Concrete non-orthogonal example: `P=[[1,1],[0,0]]`, `x=(2,3)`, `Px=(5,0)`, `(I-P)x=(-3,3)`. Image is the horizontal axis `span((1,0))`; kernel is `span((-1,1))`.
- Algebraic decomposition for every x: `x=Px+(I-P)x`; proof that `(I-P)x` lies in the kernel uses `P(I-P)=P-P^2=0`.
- The image and kernel intersect only at zero: if z=Py and Pz=0, then z=P^2 y=Pz=0.
- Therefore `R^2=Im(P) ⊕ ker(P)` (and analogously `R^n`): every vector splits *uniquely* into output component plus eliminated component.
- Connection forward: an image specifies onto what subspace, while the kernel specifies along what subspace. This prepares orthogonal-versus-oblique comparison without prematurely introducing the full `V(W^TV)^{-1}W^T` formula.

## Checkpoint pending

Ask learner to calculate `Px` and `(I-P)x` for `x=(1,2)` and interpret which lies in the image/kernel. Expected outputs: `Px=(3,0)`, `(I-P)x=(-2,2)`.

Do not mark as independently understood or mastered until learner responds.
