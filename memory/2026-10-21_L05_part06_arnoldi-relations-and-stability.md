# Lecture 5 Part 6 — Arnoldi matrix relations, breakdown, numerical stability

status: studied (explanation delivered); comprehension not independently verified
last-updated: 2026-10-21

source_paths:
- user-uploaded Lecture5-KrylovSpaces.pdf, slides 19–24
- knowledge/modules/06-krylov-arnoldi-fom-gmres.md
- knowledge/depth/06-krylov-projection-and-gmres-implementation.md
- memory/2026-10-20_L05_part05_arnoldi-gram-schmidt.md

Topics successfully explained:
- The scalar Arnoldi coefficients h_ij encode the expansion of A v_j in the Arnoldi basis; matrix V_m has columns v_1 through v_m (shape n by m), and H_m is the small m by m upper Hessenberg coefficient matrix.
- Original repeated example A=[[4,1],[1,3]], b=[1,2], v1=[1,2]/sqrt(5), v2=[2,-1]/sqrt(5): A v1 = 4 v1 + v2, A v2 = v1 + 3 v2. Thus V2=(1/sqrt(5))*[[1,2],[2,-1]], H2=[[4,1],[1,3]], and A V2 = V2 H2 since second Arnoldi remainder is zero. Numeric coincidence H2=A is specific to this example, not a general property.
- General Arnoldi relation A V_m = V_m H_m + w_m e_m^T where e_m is the last canonical coordinate in R^m, and w_m is orthogonal to V_m; if w_m nonzero, write w_m=h_(m+1),m v_(m+1) and A V_m = V_(m+1) Hbar_m. Explain the dimensions and how the rank-one remainder affects only the final column.
- Left multiplication by V_m^T yields H_m=V_m^T A V_m because V_m^T V_m=I and V_m^T w_m=0; purpose is a small representation of action of A on the Krylov space.
- Hbar_m has size (m+1) by m; upper Hessenberg means zero entries below first subdiagonal because A v_j expands only in directions v1 through v_(j+1).
- Breakdown h_(j+1),j=0 means w_j=0 and invariance/saturation; grade equals j in exact arithmetic. At breakdown v_(m+1) is not available; rely on the w_m relation and A V_m=V_m H_m (avoid claiming V_(m+1) exists).
- Modified Arnoldi/modified Gram-Schmidt computes each h_ij against the sequentially updated remainder w, subtracting immediately. In exact arithmetic it agrees with basic Arnoldi; more robust against floating-point rounding. Reorthogonalization and Householder orthogonalization are stabilization strategies mentioned on slide 24.
- Example at j=2: u=A v2=[7,-1]/sqrt(5), h12=1 -> updated w=[6,-3]/sqrt(5), h22=3 -> w=0.
- Arnoldi prepares a basis; actual coefficients for solving Ax=b come later through FOM/GMRES (Part 7).

Comprehension check: pending.
Next step: Lecture 5 Part 7 — Full Orthogonalization Method (FOM), slides 25–29.
