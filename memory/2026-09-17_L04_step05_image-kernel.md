# Lecture 04 — Step 5: Column space / image and kernel / null space

status: **verified**
last-updated: **2026-09-17**
source_paths:
- `knowledge/modules/02-linear-algebra-and-direct-methods.md`

topics studied:
- column space / image `Im(A)` as the span of the columns of `A`, equivalently the set of all possible outputs `Ax`;
- solvability criterion `Ax=b` has a solution iff `b in Im(A)`;
- kernel / null space `ker(A)={x:Ax=0}` as the set of inputs mapped to zero;
- explicit example `A=[[1,2],[2,4]]`, whose image is the line spanned by `[1,2]^T` and whose kernel is the line spanned by `[-2,1]^T`;
- nonzero kernel vectors imply nonuniqueness: if `Ax=b` and `Az=0` with `z != 0`, then `A(x+z)=b`;
- equivalence between trivial kernel and linear independence of the columns;
- image lives in the output space `R^m`, while kernel lives in the input space `R^n` for `A:R^n->R^m`.

comprehension check:
- learner chose to continue after the image/kernel explanation.

mastery note:
- first-pass conceptual understanding considered sufficient to proceed to rank and rank-nullity; reinforce these ideas through later examples and elimination.
