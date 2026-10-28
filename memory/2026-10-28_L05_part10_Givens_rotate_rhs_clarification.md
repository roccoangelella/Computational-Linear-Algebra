# GMRES QR: Why rotate the right-hand side too?

status: explanation delivered; learner comprehension unverified
last-updated: 2026-10-28
source_paths: knowledge/depth/06-krylov-projection-and-gmres-implementation.md; user-uploaded Lecture5-KrylovSpaces.pdf slides 35-40

Conceptual clarification: the right-hand side d=beta e1 is the target vector in the reduced GMRES least-squares min_y ||d-Hbar_m y||_2. Orthogonal Givens rotation G preserves all Euclidean norms, hence ||d-Hbar_m y||=||G(d-Hbar_m y)||=||Gd-(G Hbar_m)y||. Rotating Hbar_m alone changes the relative positions of target and predicted vector and solves a different problem, analogous to applying row operations to only one side of an equation.

At m=1 in repeated example, Hbar1=[3,1]^T, d=[sqrt(2),0]^T, G=(1/sqrt(10))*[[3,1],[-1,3]], G Hbar1=[sqrt(10),0]^T, Gd=[3/sqrt(5),-1/sqrt(5)]^T. Correct transformed minimization chooses y1=3sqrt(2)/10 and has residual norm 1/sqrt(5). If d were left unchanged, the incorrect transformed problem would falsely appear to have zero residual by setting y1=1/sqrt(5); in fact the original residual is nonzero.

Pedagogical emphasis: specify what d denotes before algebra, make clear that we transform the whole difference rather than only the matrix, and use the impossible-to-remove second component to explain residual norm.
