# Lecture 5 Part 7 — FOM and restarted FOM

status: explained; learner comprehension not yet independently verified
last-updated: 2026-10-21
source_paths: user-uploaded Lecture5-KrylovSpaces.pdf slides 25-29; knowledge/modules/06-krylov-arnoldi-fom-gmres.md; knowledge/depth/06-krylov-projection-and-gmres-implementation.md

Topics explained:
- FOM (Full Orthogonalization Method) deliberately chooses test space equal to Krylov search space; the Galerkin residual is perpendicular to its Arnoldi basis vectors.
- For initial guess x0 and initial residual r0=b-Ax0, represent approximation x_m=x0+V_m y_m. Let beta=norm(r0) and v1=r0/beta. From Galerkin orthogonality and H_m=V_m^T A V_m, derive the reduced system H_m y_m=beta e1; reconstruct x_m after solving it.
- FOM may fail if reduced H_m is singular; not every Krylov iteration has a valid FOM solve.
- From Arnoldi relation A V_m=V_m H_m+w_m e_m^T derive r_m=-w_m*(last component of y_m), hence norm(r_m)=h_(m+1,m)*abs(last component of y_m). This gives cheap stopping checks without forming full high-dimensional residual at every iteration.
- Continue earlier example A=[[4,0,1],[0,2,-1],[1,-1,3]], b=[1,1,0], x0=0. Two-step V2=(1/sqrt2)*[[1,1],[1,-1],[0,0]], H2=[[3,1],[1,3]], y2=[3sqrt2/8,-sqrt2/8]. Approximation x2=[1/4,1/2,0], r2=[0,0,1/4]. The Arnoldi remainder w2=[0,0,sqrt2], so residual norm formula gives sqrt2*sqrt2/8=1/4.
- Third Arnoldi vector v3=[0,0,1], projected matrix H3=[[3,1,0],[1,3,sqrt2],[0,sqrt2,3]], coefficients y3=[7sqrt2/18,-sqrt2/6,1/9]. Reconstructed exact solution x3=[2/9,5/9,1/9] with zero residual. At m=1, x1=[1/3,1/3,0], residual norm sqrt2/3.
- Restarted FOM limits subspace size to M to manage basis memory O(Mn) and growing Gram-Schmidt cost. After a cycle, adopt approximation as new x0, recompute residual, and restart Arnoldi. Restarting can slow convergence by discarding useful directions.

Next part: Lecture 5 Part 8 GMRES slides 30-34.
