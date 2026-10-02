# Lecture 15 — Clarification: what an eigenvector means geometrically

status: clarification delivered — verification pending
last-updated: 2026-10-02
source_paths:
- knowledge/modules/08-power-inverse-shifts-deflation.md
- knowledge/modules/04-stationary-iterative-methods.md

topics clarified:
- The repository definition of an eigenpair is Bv=lambda v with v!=0.
- Saying an eigenvector's "direction is not changed" means Bv remains on the same one-dimensional subspace span{v}; it is a scalar multiple of v.
- If lambda>0, Bv points along the same orientation as v and is stretched/shrunk by |lambda|.
- If lambda<0, Bv lies on the same line but points in the opposite orientation; the eigendirection is still preserved.
- If lambda=0, Bv=0; v is still an eigenvector even though the image vector has no direction.
- A generic vector is usually rotated/sheared into a different direction by a matrix and is therefore not an eigenvector.
- This meaning connects directly to stationary-iteration convergence: along an eigenvector v, repeated application gives B^k v=lambda^k v, so |lambda| controls whether that error component shrinks or grows.

mastery note:
- clarification delivered after learner reported that the phrase "direction is not changed" was unclear; verification pending.
