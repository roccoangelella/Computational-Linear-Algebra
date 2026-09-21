# Lecture 04 — Step 17: Rectangular linear systems

status: studied — first pass
last-updated: 2026-09-21
source_paths:
- knowledge/modules/02-linear-algebra-and-direct-methods.md
- docs/COURSE_MAP.md

topics studied:
- For A in R^(m x n), m is the number of equations and n the number of unknowns.
- Ax=b is consistent exactly when b belongs to the column space Im(A).
- Equivalently, consistency means rank(A)=rank([A|b]).
- If x_p is one solution, all solutions are x_p+z with z in ker(A); therefore a nonempty solution set has n-rank(A) free dimensions.
- If m>n, the system is overdetermined. It may have a unique exact solution when A has full column rank and b is in Im(A), but right-hand sides outside Im(A) give no exact solution.
- Example: A=[[1,0],[0,1],[1,1]]. For b=(1,2,3)^T the solution is x=(1,2)^T. For b=(1,2,4)^T there is no exact solution because the first two equations force the third left-hand side to be 3.
- Geometrically, two independent columns in R^3 span a plane; an exact solution exists exactly when b lies in that plane.
- If m<n, the system is underdetermined. Since rank(A)<=m<n, any consistent system has a nontrivial kernel and therefore infinitely many solutions.
- Example: x1+x2+x3=2 has a two-dimensional family of solutions.
- Inconsistent overdetermined systems motivate least squares: minimize ||Ax-b||_2 instead of requiring exact equality.

mastery note:
- First-pass explanation delivered; learner verification is still required before full mastery is assumed.
