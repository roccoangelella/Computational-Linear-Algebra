# Lecture 12 — Step 1: Orthogonal projectors introduction

status: studied — first pass
last-updated: 2026-09-22
source_paths:
- knowledge/modules/03-orthogonality-qr-projectors-least-squares.md
- docs/LECTURE_INDEX.md

topics studied:
- Purpose: package orthogonal projection onto a fixed subspace into a matrix P that can be applied to any vector.
- If Q has orthonormal columns spanning a subspace S, then the orthogonal projector onto S is P = QQ^T.
- For any vector b, p = Pb = QQ^T b lies in S and is the closest point in S to b in Euclidean norm.
- Q^T b computes the coordinates of b along the orthonormal basis directions; multiplying by Q reconstructs the projected vector in the original ambient space.
- A projector satisfies P^2 = P: after a vector has been projected into the target subspace, projecting it again changes nothing.
- An orthogonal projector is also symmetric, P^T = P.

mastery note:
- Introductory explanation delivered; learner verification and further examples still required.
