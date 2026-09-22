# Lecture 12 — Step 1: Orthogonal projection onto a subspace

status: studied — first pass
last-updated: 2026-09-22
source_paths:
- docs/LECTURE_INDEX.md
- knowledge/modules/03-orthogonality-qr-projectors-least-squares.md

topics studied:
- Purpose: an orthogonal projector extracts from a vector the component lying in a chosen subspace and discards the perpendicular component.
- If Q has orthonormal columns q_1,...,q_k spanning subspace S, then the projection of b onto S is the sum of the scalar projections along the basis directions: p = sum_i (q_i^T b) q_i.
- In matrix form this becomes p = Q Q^T b, so P = Q Q^T is the orthogonal projector onto S.
- The residual r=b-p is orthogonal to every vector in S, equivalently Q^T r=0.
- Applying the projector twice changes nothing further: P^2=P.
- In the real Euclidean setting an orthogonal projector is symmetric: P^T=P.

mastery note:
- First-pass explanation begun; learner verification and a non-axis-aligned numerical example still required.
