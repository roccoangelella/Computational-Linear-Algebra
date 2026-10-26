# Lecture 5 — Part 8: GMRES fundamental principles (slides 30–34)

Status: explanation delivered, learner comprehension not yet independently verified.
Date: 2026-10-26
Source: user-uploaded Lecture5-KrylovSpaces.pdf pages 30–34; knowledge/modules/06-krylov-arnoldi-fom-gmres.md; knowledge/depth/06-krylov-projection-and-gmres-implementation.md.

Key learning:
- GMRES shares Krylov search space and Arnoldi orthonormal basis with FOM, but chooses coefficients y to minimize the Euclidean residual norm rather than Galerkin residual orthogonality to K_m.
- GMRES test space L=A K_m: optimal residual is orthogonal to images of search directions under A, because variations of x in K_m change Ax in A K_m. This differs from FOM L=K_m.
- Set r0=b-Ax0, beta=||r0||, v1=r0/beta; Arnoldi builds V_m and (m+1) by m Hbar_m satisfying A V_m=V_(m+1) Hbar_m when the next Arnoldi direction exists. Write x=x0+V_m y; then r=V_(m+1)(beta e1-Hbar_m y). Because V_(m+1) is orthonormal, ||r||=||beta e1-Hbar_m y||. Hence GMRES solves a small least-squares minimization. Equivalent formal normal equations Hbar_m^T Hbar_m y=Hbar_m^T beta e1, but QR is preferable in practice (following part).
- Basic Arnoldi + small minimization + reconstruction x_m=x0+V_m y_m is the part 8 algorithm. It does not remove the need for sparse matrix-vector products by A.

Example reused: A=[[4,0,1],[0,2,-1],[1,-1,3]], b=[1,1,0], x0=0. For one direction x=alpha b, FOM chooses alpha=1/3 with residual norm sqrt(2)/3, GMRES minimizes (1-4alpha)^2+(1-2alpha)^2 and chooses alpha=3/10 with residual norm 1/sqrt(5). GMRES residual is orthogonal to Ab and not necessarily to b.
Two-step example: V2=(1/sqrt2)*[[1,1],[1,-1],[0,0]], Hbar2=[[3,1],[1,3],[0,sqrt2]], beta=sqrt2. Normal equations have matrix [[10,6],[6,12]], right side [3sqrt2,sqrt2]. Coefficients y=[5sqrt2/14,-2sqrt2/21], reconstructed x2=[11/42,19/42,0], residual [-1/21,2/21,4/21], norm 1/sqrt21 approx 0.2182, compared with FOM m2 residual norm 1/4. Residual perpendicular to A K2, not to K2.

Next: Part 9 GMRES and QR of Hbar_m (slides 35–38).