# Lecture 5: Why V and H enable smaller solves

status: explained; mastery unverified
last-updated: 2026-10-21
source_paths: user-uploaded Lecture5-KrylovSpaces.pdf slides 19-21, 25-27; knowledge/modules/06-krylov-arnoldi-fom-gmres.md

Core point: V_m maps m search coefficients y back to an n-vector x=x0+V_m y. H_m=V_m^T A V_m is an m by m matrix of projected operator coefficients. Choosing Galerkin/FOM test space K yields H_m y=V_m^T r0. This is a smaller system, rather than directly solving n unknowns. It does not replace A for all purposes and residual may remain nonzero.

Worked example A=[[4,0,1],[0,2,-1],[1,-1,3]], b=[1,1,0], x0=0. Arnoldi v1=[1,1,0]/sqrt(2), v2=[1,-1,0]/sqrt(2), h11=3, h21=1, h12=1, h22=3, with second remainder w2=[0,0,sqrt(2)]. Thus H2=[[3,1],[1,3]], V2=(1/sqrt(2))*[[1,1],[1,-1],[0,0]]. Galerkin: H2 y=[sqrt(2),0], y=[3sqrt(2)/8,-sqrt(2)/8]; reconstruct x2=V2 y=[1/4,1/2,0]. Check A x2=[1,1,-1/4], so residual=[0,0,1/4], nonzero but orthogonal to both Arnoldi directions. Exact solution is [2/9,5/9,1/9]. H2 differs from the upper left submatrix of A.

Scale comparison: n=100000, m=20, H_m contains 400 entries, V_m contains 2 million, and A still participates in m matrix-vector multiplications. Distinguish projected solve from full A inversion.

Learner understanding awaits confirmation.
