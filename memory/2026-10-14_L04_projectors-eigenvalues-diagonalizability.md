# 2026-10-14 — Projector eigenvalues and diagonalizability (slide 41)

status: **explained in conversation — comprehension not independently verified**
last-updated: 2026-10-14
source_paths:
- user-uploaded `Lecture4-Ortogonalization.pdf` (slide 41)
- `knowledge/modules/03-orthogonality-qr-projectors-least-squares.md`
- `memory/2026-10-14_L04_projector-image-kernel-first-step.md`
- `memory/2026-10-14_L04_projectors-general-oblique-formula.md`

## Explanation given
- Recalled eigenpair definition `Pu=lambda u` with `u != 0`, describing nonzero input direction whose image is scalar multiple.
- Derivation from idempotence `P^2=P`: `P^2u=lambda^2u=Pu=lambda u`, hence `lambda(lambda-1)=0`, so every projector eigenvalue belongs to `{0,1}`. Note a specific projector may have only one of the two eigenvalues (e.g. `P=0` or `P=I`).
- `lambda=1` eigenspace equals `Im(P)`, since `P(Py)=Py` and `Pz=z => z∈Im(P)`. `lambda=0` eigenspace equals `ker(P)` by definition.
- Recalled unique direct-sum decomposition `R^n=Im(P)⊕ker(P)`; concatenating bases of image and kernel forms n independent eigenvectors, therefore `P` is diagonalizable (similar to `diag(I_r,0)` where `r=rank(P)`).
- Numerical example oblique `P=[[1,1],[0,0]]`, eigenvectors `v1=(1,0)` for 1 and `v0=(-1,1)` for 0. With `X=[[1,-1],[0,1]]`, `D=diag(1,0)`, `P=XDX^{-1}`, `X^{-1}=[[1,1],[0,1]]`.
- Diagonalizable does not imply orthogonally diagonalizable; the chosen eigenvectors for oblique example are not perpendicular. Oblique projectors can amplify Euclidean length on certain vectors despite eigenvalues 0/1 (e.g. x=(2,3), Px=(5,0), 5>sqrt(13)).
- Lesson is spectral bridge to later eigenvalue/diagonalization/spectral-theorem topic; next step in proposed course gap path: spectral foundations (slides 3–4), unless user prefers proof of best approximation first.

## Verification status
- User asked to proceed; no independent derivation or response to checkpoint yet. Do not mark mastered.
