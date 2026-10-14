# 2026-10-14 — Orthogonalization slide deck gap audit

status: **verified comparison, NOT evidence that new topics were studied or mastered**
last-updated: 2026-10-14
source_paths:
- user-uploaded `Lecture4-Ortogonalization.pdf` (53-slide deck, Adriano Festa, dated 2025-10-16)
- `knowledge/modules/03-orthogonality-qr-projectors-least-squares.md`
- `knowledge/depth/03-qr-construction-details.md`
- `memory/2026-09-22_L09_step02_projection-and-gram-schmidt.md`
- `memory/2026-09-22_L09_step03_qr-factorization.md`
- `memory/2026-09-22_L10_step01_classical-vs-modified-gram-schmidt.md`
- `memory/2026-09-22_L11_step01_givens-rotations.md`
- `memory/2026-09-22_L11_step02_householder-full-example.md`
- `memory/2026-09-22_L12_step01_orthogonal-projectors-intro.md`
- `memory/2026-09-25_L12_step02_least-squares-residual-orthogonality.md`
- `memory/2026-09-25_L12_step03_least-squares-through-qr.md`
- `memory/2026-09-30_L12_clarification-qr-healthier-full-column-rank.md`
- `memory/2026-10-01_L13_bridge_qr-stability-diagnostics.md`
- `memory/2026-10-02_L15_clarification-eigenvector-meaning.md`

## Coverage confirmed from prior conversations

- Slides 5–16: orthogonality/orthonormality, orthogonal matrices, Gram–Schmidt (classical and modified), QR. Covered at least first pass.
- Slides 18–31: Givens, Householder, QR, method comparison, and stability checks. Covered core, including a full dense Householder example; precise Householder projector proof and stable sign-cancellation rationale are not independently verified.
- Slides 37–38 and 44, 47–51: elementary orthogonal projector `P=QQ^T`, idempotence, residual orthogonality, least-squares geometry, normal equations vs QR and conditioning. Covered in conversation; some mastery checkpoints pending.
- The slide-17 30-by-n Vandermonde stress experiment is a new *illustration*, not a new algorithm.

## Not yet systematically studied / gaps to cover

1. Slides 3–4: characteristic polynomial, algebraic/geometric multiplicity, similarity, diagonalizability and real-symmetric spectral theorem. Eigenpair definition and eigenvalue-based stationary convergence have been introduced, but not the whole theory.
2. Slides 32–35: unitary matrices as complex orthogonal analogues; Hadamard gate, its reflection interpretation, and quantum example. The basic complex conjugate-transpose idea exists in semantic repository knowledge but not verified in tutoring history.
3. Slides 39–43: projector image/kernel direct-sum decomposition; difference between oblique and orthogonal projection; general oblique formula `P=V(W^T V)^{-1}W^T` and hypotheses; projector eigenvalues 0,1 and diagonalizability. Only elementary orthogonal projection had been taught.
4. Slide 46: Pythagorean proof of best-approximation theorem; closest-point property had been introduced but not rigorously proved in study sessions.
5. Slides 19–20: a formal proof `(I-2P_v)^T(I-2P_v)=I` and floating-point motivation for the stable Householder sign rule can be reinforced.

## Verified numerical and ordering issues in the uploaded deck

- Slide 28 starts with `A=[[6,5],[5,1],[0,4]]` and `G1` with active block `[[6,5],[-5,6]]/sqrt(61)`. The (2,2) entry of `G1 A` should be `(-5*5+6*1)/sqrt(61)=-19/sqrt(61)`, **not** `-24/sqrt(61)`. This carries over to incorrect slide-29 coefficients and second QR diagonal. Correct second diagonal (with positive r convention) is `sqrt(1337/61)`.
- Slide 29 states `R=G2 G1 A` but `Q=(G1 G2)^T`. Correct accumulation is `Q=(G2 G1)^T=G1^T G2^T`.
- Slide 24's general Householder product/transposition can be confusing/inconsistent with slide 21: if `R=H_k...H_1 A`, and every `H_j=H_j^T`, then `Q=H_1...H_k` (not its transpose in that order).

## Teaching decision

Next time on this slide deck: prioritize spectral preliminaries, unitary/Hadamard material (if examinable), general/oblique projector geometry and formula, eigenvalues of projectors, and best-approximation proof. Do NOT mark these as studied or mastered from this audit alone.
