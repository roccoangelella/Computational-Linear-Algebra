# Lecture 09 — Step 2 clarification: projection and Gram–Schmidt intentions

status: clarification delivered; mastery not yet verified
last-updated: 2026-09-22
source_paths:
- knowledge/modules/03-orthogonality-qr-projectors-least-squares.md
- knowledge/modules/02-linear-algebra-and-direct-methods.md

topics clarified:
- The projection formula is best understood through the decomposition a = a_parallel + a_perp relative to a unit direction q.
- For unit q, q^T a is the signed scalar coordinate of a along q, because if a=cq+w with w orthogonal to q, then q^T a=c.
- The vector (q^T a)q is therefore the actual parallel component of a along q.
- Subtracting that projection leaves a_perp, and q^T a_perp=0, so the remainder is orthogonal to q.
- 'Pointing toward q' should mean having a nonzero component along q; a vector orthogonal to q has zero component along q, while a parallel vector consists entirely of such a component.
- In Gram–Schmidt, q1 is already the normalized direction of a1. The next input vector a2 is modified by removing its q1-component so that the new direction is orthogonal to q1 while remaining in span{a1,a2}.
- Removing the q1-component from a1 itself would produce zero, because a1 is entirely parallel to q1.
- v2 is normalized only after orthogonality is obtained: normalization preserves direction and orthogonality while setting length to 1, yielding q2 and simplifying later projection formulas.
- The reason for preserving the same span is that Gram–Schmidt is changing the basis used to describe the same subspace, not changing the subspace/problem itself. The original columns of A span Im(A); the orthonormal columns q_i should span that same Im(A), which later allows QR and projection/least-squares computations without losing any direction present in A.
- 'There is nothing to be perpendicular to yet' means orthogonality is a relation between at least two nonzero vectors. At the first step no q_i has yet been constructed, so the only task is to choose the first direction from a1 and normalize it. Starting from the second vector, each new q_j must be orthogonal to all previously constructed q_i.
- Completed example: a1=(1,0)^T and a2=(1,1)^T. Since ||a1||=1, q1=(1,0)^T. The projection of a2 onto q1 is (q1^T a2)q1=(1,0)^T. Subtracting it gives v2=(0,1)^T, already unit length, so q2=(0,1)^T. Thus span{a1,a2}=span{q1,q2}=R^2 while q1 and q2 are orthonormal.
- For this example A=[[1,1],[0,1]], Q=I_2, and the Gram-Schmidt coefficients produce R=[[1,1],[0,1]], so A=QR. This special example gives Q=I because the orthonormalized basis happens to be the standard basis.

mastery note:
- User explicitly reported that the earlier explanation hid the purpose of each operation. Future explanations of algorithms should state the goal of each transformation before giving the formula. Do not mark this step fully mastered until the user confirms the rebuilt explanation.
