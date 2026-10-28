# Lecture 5 — Part 10: Givens rotations inside GMRES

Status: explained; learner comprehension not yet independently verified.
Date: 2026-10-28
Sources: user-uploaded Lecture5-KrylovSpaces.pdf slides 39–44; knowledge/modules/06-krylov-arnoldi-fom-gmres.md; knowledge/depth/06-krylov-projection-and-gmres-implementation.md.

Main idea: GMRES least squares min_y || beta e1 - Hbar_m y ||_2. QR is updated incrementally as Arnoldi adds one column: a Givens rotation is a plane orthogonal transformation [[c,s],[-s,c]] with r=sqrt(a^2+b^2), c=a/r, s=b/r, sending [a,b] to [r,0]. Extended rotations Omega_j act on rows j,j+1 of the upper Hessenberg Hbar_m to eliminate its subdiagonal h_(j+1),j; prior rotations are reused for the next column and a single new rotation clears the new subdiagonal entry. The same rotations are applied to RHS beta e1. As a result, transformed Hbar is upper triangular with zero last row, solved by back substitution; last RHS component gives exact GMRES residual norm in exact arithmetic. Q_m=Omega_m ... Omega_1 is orthogonal, distinct from Arnoldi V_m.

Worked example reused: A=[[4,0,1],[0,2,-1],[1,-1,3]], b=[1,1,0], beta=sqrt2; Arnoldi Hbar1=[3,1]^T, Hbar2=[[3,1],[1,3],[0,sqrt2]]. G1 has c1=3/sqrt10, s1=1/sqrt10 and eliminates h21=1. At iteration 1 transformed RHS [3/sqrt5,-1/sqrt5], so residual norm 1/sqrt5, coefficient y1=3sqrt2/10. At iteration 2, extend G1 to 3x3; apply to new column [1,3,sqrt2]^T to obtain [6/sqrt10,8/sqrt10,sqrt2]^T. G2 rotates rows 2,3 with rho=sqrt(42/5), c2=4/sqrt21, s2=sqrt5/sqrt21. Final upper-triangular Rbar2=[[sqrt10,6/sqrt10],[0,sqrt(42/5)],[0,0]]. Rotated RHS [3/sqrt5,-4/sqrt105,1/sqrt21]. Residual norm 1/sqrt21; triangular back substitution gives y=[5sqrt2/14,-2sqrt2/21], and x2=V2 y=[11/42,19/42,0], matching prior GMRES results.

Pedagogical emphasis: one rotation per newly added Arnoldi column, not rerun QR from scratch; maintain lengths and residual by rotating RHS as well. The lesson's 6x5 illustrative Hessenberg format and Omega_m product generalize the 3x2 worked example.
Next: Part 11 — Incremental GMRES and convergence (slides 45–50).