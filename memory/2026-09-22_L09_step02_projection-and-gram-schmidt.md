# Lecture 09 — Step 2: Projection onto a direction and Classical Gram–Schmidt

status: studied — first pass
last-updated: 2026-09-22
source_paths:
- knowledge/modules/03-orthogonality-qr-projectors-least-squares.md
- knowledge/depth/03-qr-construction-details.md
- docs/LECTURE_INDEX.md

topics studied:
- For a unit vector q, the component of a vector a along q is the orthogonal projection (q^T a)q.
- If the direction vector u is not unit length, the projection is ((u^T a)/(u^T u))u.
- Subtracting the projection removes the component parallel to the chosen direction, leaving a vector orthogonal to that direction.
- Classical Gram–Schmidt turns linearly independent vectors a_1,...,a_n into orthonormal vectors q_1,...,q_n spanning the same subspace.
- First vector: q_1=a_1/||a_1||_2.
- For the second vector, v_2=a_2-(q_1^T a_2)q_1, then q_2=v_2/||v_2||_2.
- General step: v_j=a_j-sum_{i=1}^{j-1}(q_i^T a_j)q_i, then q_j=v_j/||v_j||_2.
- Concrete example with a_1=(1,1)^T and a_2=(1,0)^T yields q_1=(1/sqrt(2))(1,1)^T and q_2=(1/sqrt(2))(1,-1)^T.
- Gram–Schmidt preserves the generated subspace while replacing the original basis by an orthonormal basis.
- A zero or numerically tiny v_j indicates exact or near linear dependence and prevents safe normalization.

mastery note:
- First-pass explanation delivered; learner verification is still required before full mastery is assumed.
