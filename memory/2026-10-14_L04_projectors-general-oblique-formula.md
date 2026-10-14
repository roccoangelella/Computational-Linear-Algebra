# 2026-10-14 — General oblique projector matrix formula (slide 43)

status: **explained in conversation — learner comprehension not yet verified**
last-updated: 2026-10-14
source_paths:
- user-uploaded `Lecture4-Ortogonalization.pdf` (slide 43)
- `knowledge/modules/03-orthogonality-qr-projectors-least-squares.md`
- `memory/2026-10-14_L04_projectors-orthogonal-vs-oblique.md`

## Topics explained
- Construction problem: define a projector onto `M=Col(V)` from a target basis matrix `V ∈ R^(n×r)` and test directions/orthogonality constraints defined by columns of `W ∈ R^(n×r)`. Clarify that W is not the set of vectors we project *along*: residuals lie in `ker(W^T)`, perpendicular to columns of W.
- The projected vector is `p=Vy` for some coefficient vector `y∈R^r`; the residual `x-Vy` must satisfy `W^T(x-Vy)=0`. Expand to `W^TV y=W^Tx`.
- Assumption: `W^TV` must be square/invertible. Then `y=(W^TV)^(-1)W^Tx`, and `P=V(W^TV)^(-1)W^T` (source slide 43).
- Meaning: `Im(P)=Col(V)`, `ker(P)=ker(W^T)`, and `P^2=P` follows by direct multiplication and `W^TV` cancellation.
- Fully worked example reused: `V=(1,0)^T`, `W=(1,1)^T`, `W^TV=1`, hence `P=[[1,1],[0,0]]`. Acting on `x=(2,3)^T` yields `y=5`, `Px=(5,0)^T` and `r=(-3,3)^T`; indeed `W^Tr=0` even though `V^Tr=-3` — oblique rather than orthogonal.
- Contrast special case `W=V`: `P=V(V^TV)^{-1}V^T`, orthogonal projector; for orthonormal columns `Q`, this reduces to `P=QQ^T`.
- Why invertibility matters: if `W^TV` singular, projection conditions do not determine a unique target coefficient for arbitrary x.
- Optional note: computing the mapping in practice uses a solve with `W^TV`, not explicit inverse.

## Next topic and verification
- Next slide 41 property (in deck order distinct from derivation): projectors only have eigenvalues 0 and 1; full diagonalizability follows from image/kernel decomposition.
- No independent comprehension demonstrated yet; maintain pending rather than marking mastered.
