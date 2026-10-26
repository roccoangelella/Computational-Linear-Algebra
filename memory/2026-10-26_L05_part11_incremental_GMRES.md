# Lecture 5 Part 11 — Incremental GMRES and convergence (slides 45-50)

status: explained; mastery not independently verified
last-updated: 2026-10-26
source_paths: uploaded Lecture5-KrylovSpaces.pdf slides 45-50; knowledge/depth/06-krylov-projection-and-gmres-implementation.md

Arnoldi enlarges Hbar_m one column at a time. After previously stored Givens rotations have been applied to the new column, one fresh rotation annihilates the new subdiagonal entry. Store c_i,s_i rather than explicitly storing full row-rotation matrices. Transform rhs beta e1 simultaneously. The last transformed entry gamma_(m+1) satisfies ||r_m||_2=abs(gamma_(m+1)) and gamma_(j+1)=-s_j*gamma_j with gamma_1=beta. Thus residual monitoring is cheap and no full x_m or r_m is required at every GMRES iteration; retrieve solution coefficients with triangular solve R_m y=g_m on stopping and lift through V_m.

Example continuing A=[[4,0,1],[0,2,-1],[1,-1,3]], b=[1,1,0]: initial norm sqrt2=1.4142; GMRES first-step norm 1/sqrt5~.4472; second-step norm 1/sqrt21~.2182; third-step exact norm0. Relative tolerance, e.g. 0.2, would allow stopping after second iteration. Arnoldi exact breakdown h_(m+1),m=0 is distinct from tolerance stopping; for invertible A in exact arithmetic GMRES reaches exact solution at Krylov grade. GMRES(M) restarts after M directions, bounding memory and per-cycle orthog cost but possibly stagnating; unrestarted GMRES has at-most-n-step exact termination in exact arithmetic for invertible A.

Comprehension pending. Next Part 12 Householder reflectors, slides 51-56.
