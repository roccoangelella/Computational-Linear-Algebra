# Lecture 11 — Step 1: Givens rotations

status: studied — first pass
last-updated: 2026-09-22
source_paths:
- knowledge/modules/03-orthogonality-qr-projectors-least-squares.md
- knowledge/depth/03-qr-construction-details.md

topics studied:
- Purpose: a Givens rotation is chosen to zero one selected component/matrix entry while preserving Euclidean length and orthogonality.
- The active 2x2 block is G=[[c,s],[-s,c]] with c^2+s^2=1; outside the selected coordinate pair, the full Givens matrix is the identity.
- To eliminate b from the two-vector (a,b)^T, choose r=sqrt(a^2+b^2), c=a/r, s=b/r. Then G(a,b)^T=(r,0)^T.
- Concrete vector example: (3,4)^T gives r=5, c=3/5, s=4/5, hence G(3,4)^T=(5,0)^T.
- Matrix example A=[[3,1],[4,2]]: the same G applied on the left mixes only the two rows and gives R=GA=[[5,11/5],[0,2/5]], which is upper triangular.
- Since G is orthogonal, G^{-1}=G^T. Therefore from R=GA we get A=G^T R, so Q=G^T and A=QR.
- Givens rotations eliminate entries one at a time and alter only two rows/coordinates, which is why they are useful for sparse, structured, or selective elimination problems.

mastery note:
- First-pass explanation delivered; learner verification still required.

clarification added:
- If a column has multiple nonzero entries below the diagonal, one Givens rotation is applied per target entry, typically bottom-up. Each rotation is built from the current pair consisting of the pivot-like entry above and the target entry, so later rotations use values already changed by earlier ones.

- Clarification on advancing to the second column: after column 1 is cleared, the current matrix must be used because previous rotations changed the remaining entries. For column 2 of a 3x3 matrix, only the entry in row 3 lies below the diagonal and must be eliminated. A new Givens rotation acts on rows 2 and 3, using the current pair (R[2,2], R[3,2]). Row 1 is not involved. Because rows 2 and 3 already contain zeros in column 1, mixing those rows preserves the zeros created in column 1. This is why a left-to-right Givens sweep can triangularize the matrix without undoing earlier work.
