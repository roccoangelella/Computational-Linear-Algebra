# Lecture 5 Part 10 — Givens QR in GMRES

status: explained; mastery not independently verified
last-updated: 2026-10-26
source_paths: uploaded Lecture5-KrylovSpaces.pdf slides 39-44; knowledge/depth/06-krylov-projection-and-gmres-implementation.md

A Givens transform [[c,s],[-s,c]] eliminates the second component d of [a,d] using r=sqrt(a^2+d^2), c=a/r, s=d/r. Applied to neighboring matrix rows, this eliminates a Hessenberg subdiagonal without altering 2-norms.

Example Hbar2=[[3,1],[1,3],[0,sqrt2]], rhs=[sqrt2,0,0]. Rotation 1: c1=3/sqrt10, s1=1/sqrt10, resulting Hbar=[[sqrt10,6/sqrt10],[0,8/sqrt10],[0,sqrt2]], rhs=[3/sqrt5,-1/sqrt5,0]. Rotation 2: c2=4/sqrt21, s2=sqrt(5/21), yielding [R2;0] with R2=[[sqrt10,6/sqrt10],[0,sqrt(42/5)]], transformed rhs=[3/sqrt5,-4/sqrt105,1/sqrt21]. Solve R2 y=first two rhs components: y=[5sqrt2/14,-2sqrt2/21]. Reconstruct x2=[11/42,19/42,0], r2=[-1/21,2/21,4/21], norm=1/sqrt21 approximately .2182, below FOM m=2 residual .25. Each rotation is computed from the two entries, not arbitrarily chosen. This explicitly links Givens to reduced GMRES solution.
