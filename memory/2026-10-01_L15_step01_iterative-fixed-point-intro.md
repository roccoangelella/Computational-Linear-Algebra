# Lecture 15 — Step 1: Why iterative solvers; fixed-point form

status: studied — first pass
last-updated: 2026-10-01
source_paths:
- docs/LECTURE_INDEX.md
- knowledge/modules/04-stationary-iterative-methods.md

recap supplied before transition:
- Gram-Schmidt: starting from linearly independent columns, repeatedly removes components along previously constructed directions and normalizes, producing an orthonormal basis Q spanning the same column space and an upper-triangular R with A=QR.
- Modified Gram-Schmidt performs the same projection removals in an updated sequential order and is generally more robust numerically.
- Householder reflection: an orthogonal reflector H=I-2vv^T/(v^Tv), with v chosen from the active column so that H maps that column tail to a multiple of a coordinate vector and zeros all entries below the pivot at once; repeated reflectors give a stable dense QR factorization.

new topic studied:
- Motivation for iterative linear solvers: for large sparse Ax=b, direct factorization can be too expensive in memory/work and can create fill-in; an iterative method instead starts from x^(0) and generates successive approximations.
- Target behavior is x^(k) -> x_*, where Ax_*=b.
- Stationary fixed-point form: x^(k+1)=B x^(k)+c, with B and c unchanged from iteration to iteration.
- A fixed point x_* is a vector unchanged by the iteration: x_*=Bx_*+c.
- Subtracting the fixed-point equation from the iteration yields the error recurrence e^(k+1)=B e^(k), where e^(k)=x^(k)-x_*.
- Therefore e^(k)=B^k e^(0), which is the basis for later convergence analysis.

mastery note:
- first-pass transition into iterative methods; learner verification pending before assuming mastery of the fixed-point/error recurrence.
