# Lecture 5 — Part 9: QR solves the GMRES least-squares problem

Date: 2026-10-27
Status: explained and numerically worked; learner understanding not yet independently checked
Sources: user-uploaded Lecture5-KrylovSpaces.pdf slides 35–38; knowledge/modules/06-krylov-arnoldi-fom-gmres.md; knowledge/depth/06-krylov-projection-and-gmres-implementation.md

Core point: GMRES minimizes ||beta e1-Hbar_m y||_2. The slide uses Hbar_m=Q_m^T Rbar_m, where Q_m is (m+1)x(m+1) orthogonal and Rbar_m is (m+1)xm upper triangular with final row zero. Thus Q_m Hbar_m=Rbar_m; transform right-hand side gbar_m=Q_m beta e1. Orthogonality preserves 2-norm, so the objective squared is ||g_m-R_m y||_2^2+|gamma_(m+1)|^2. If R_m is nonsingular, solve small triangular system R_m y=g_m; the remaining GMRES residual norm is |gamma_(m+1)|. QR avoids solving normal equations Hbar^T Hbar that square conditioning. Important: Q_m for QR is distinct from Arnoldi basis V_m.

Same grounded example as Part 8: Hbar2=[[3,1],[1,3],[0,sqrt2]], d=beta e1=[sqrt2,0,0]. QR Gram–Schmidt: q1=[3,1,0]/sqrt10; r11=sqrt10; r12=6/sqrt10; second orthogonal remainder w=[-4/5,12/5,sqrt2], length r22=sqrt210/5; q2=[-4,12,5sqrt2]/sqrt210; choose third orthonormal direction q3=[1,-3,4sqrt2]/sqrt42. Q has rows q1^T,q2^T,q3^T and Rbar=[[sqrt10,6/sqrt10],[0,sqrt210/5],[0,0]]. gbar=Qd=[3/sqrt5,-4/sqrt105,1/sqrt21]. Back substitution gives y2=-2sqrt2/21, y1=5sqrt2/14, same as normal equations; residual norm = 1/sqrt21. Reconstruct x2=V2 y=[11/42,19/42,0].

Slides additionally give rank(AV_m)=rank(R_m) and, if r_mm=0 (full rank QR/Arnoldi assumptions), A must be singular; explanation: AV_m and Rbar have same column rank due orthonormal factors, and if A invertible and V_m full column rank then AV_m must also have full rank. GMRES can still be defined in rank-deficient situations but triangular solve formula assumes nonsingular R_m.

Next: Part 10 Givens rotations for updating QR of the small GMRES Hessenberg matrix, slides 39–44. Reminder: one lecture part per user turn.