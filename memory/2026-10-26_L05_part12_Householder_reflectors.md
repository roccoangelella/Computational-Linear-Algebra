# Lecture 5 Part 12 — Householder reflectors (slides 51-56)

status: explained; mastery not independently verified
last-updated: 2026-10-26
source_paths: uploaded Lecture5-KrylovSpaces.pdf slides 51-56; knowledge/depth/06-krylov-projection-and-gmres-implementation.md

Householder reflection P=I-2uu^T for unit vector u preserves vector length, is symmetric and orthogonal, and is involutive. Derive factor 2: decompose x into parallel (u^T x)u and perpendicular parts, then reverse only parallel component, requiring subtraction twice. To map nonzero x to one-coordinate vector, define sigma=sign(x1)*||x||, u_tilde=x+sigma*e1, u=u_tilde/||u_tilde||, yielding Px=-sigma e1; sign limits subtractive cancellation. Example x=[3,4,12], norm13, sigma13, u_tilde=[16,4,12], unit u=[4,1,3]/sqrt26, u^T x=2sqrt26; Px=x-4[4,1,3]=[-13,0,0]. Length is preserved. Compared to Givens that zeros one entry using two rows, Householder can eliminate multiple trailing entries and is an alternative for stable orthogonalization or QR; it is not an extra mandatory step after Givens in GMRES.

Parts 8–12 have now been explained, completing this 56-slide Krylov Methods lecture at the overview+worked-example level; learner comprehension is not independently verified, and later exercises/review may still be needed.
