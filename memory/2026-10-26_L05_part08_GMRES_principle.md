# Lecture 5 Part 8 — GMRES principle (slides 30-34)

status: explained; learner comprehension not yet independently verified
last-updated: 2026-10-26
source_paths: uploaded Lecture5-KrylovSpaces.pdf slides 30-34; knowledge/modules/06-krylov-arnoldi-fom-gmres.md; knowledge/depth/06-krylov-projection-and-gmres-implementation.md

The same Krylov search space x_m=x0+V_m y is shared by FOM and GMRES. FOM imposes residual perpendicular to K_m (Galerkin), whereas GMRES minimizes the Euclidean residual and equivalently tests perpendicularity to A K_m. From the Arnoldi relation A V_m=V_(m+1) Hbar_m and r0=beta v1 derive r_m=V_(m+1)(beta e1-Hbar_m y) and hence y_m=argmin_y norm(beta e1-Hbar_m y). The small problem is (m+1) by m least squares, followed by x_m=x0+V_m y_m.

Using continuing A=[[4,0,1],[0,2,-1],[1,-1,3]], b=[1,1,0], x0=0, v1=[1,1,0]/sqrt2: first-step GMRES candidate x1=yv1 has squared residual 2-6sqrt2*y+10*y^2. Minimum at y=3sqrt2/10 yields x1=[3/10,3/10,0] and norm(residual)=1/sqrt5~0.4472, smaller than FOM first-step norm sqrt2/3~0.4714 with x1=[1/3,1/3,0].

Practical note: the GMRES minimum applies within the chosen Krylov space, not to all possible x. Arnoldi breakdown requires separate handling because v_(m+1) may not exist. Comprehension check pending; next Part 9 QR approach to the reduced least squares problem.
