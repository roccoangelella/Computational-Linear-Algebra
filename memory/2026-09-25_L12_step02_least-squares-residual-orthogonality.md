# Lecture 12 — Step 2: Least-squares residual and orthogonality

status: clarified — first verification
last-updated: 2026-09-25
source_paths:
- knowledge/modules/03-orthogonality-qr-projectors-least-squares.md

topics clarified:
- In least squares, Ax_* is the orthogonal projection of b onto Im(A)=Col(A).
- The residual r_*=b-Ax_* is therefore the component of b orthogonal to Im(A).
- The statement r_* ⟂ Im(A) is stronger than merely saying r_* is not in Im(A).
- For a subspace S, a nonzero vector can lie outside S without being perpendicular to S.
- In a Euclidean inner-product space, S ∩ S^⊥ = {0}; the only vector that is both in a subspace and orthogonal to it is the zero vector.
- The decomposition b = Ax_* + r_* is an orthogonal decomposition with Ax_* ∈ Im(A) and r_* ∈ Im(A)^⊥.

comprehension note:
- learner correctly interpreted b-Ax_* as removing the component of b contained in Im(A);
- precision correction made: not belonging to Im(A) does not by itself imply perpendicularity. Perpendicularity follows because Ax_* is specifically the orthogonal projection.
