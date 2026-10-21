# Lecture 5 Part 5: Arnoldi variable meanings

status: explained, comprehension not verified
last-updated: 2026-10-21
source_paths: knowledge/modules/06-krylov-arnoldi-fom-gmres.md; uploaded Lecture5-KrylovSpaces.pdf slides 15-18

Learner needed the meaning and purpose of u=Av_j, v_i, and h_ij=v_i^T u. Explain: v_j is the current unit Arnoldi basis vector, u is a temporary candidate A v_j (letter u only pedagogical; lecture writes A v_j), and h_ij is a scalar dot product measuring the component of u along earlier unit vector v_i. j indexes Arnoldi iteration and i indexes existing basis vector. Because the basis vectors are unit length, h_ij v_i is the projection of u along v_i; subtracting all such projections gives a vector orthogonal to previous directions. Then h_(j+1),j is the norm of the remaining vector and is used for normalization, not an existing-direction projection coefficient.

Numerical anchor: A=[[4,1],[1,3]], b=[1,2], v1=b/sqrt5. u=A v1=[6,7]/sqrt5, h11=v1^T u=4, w1=u-4v1=[2,-1]/sqrt5. Dot product v1^T w1=0. Norm h21=1, so v2=w1. At next iteration h12=1 and h22=3.

Do not advance to part 6 until this notation is clear. Understanding not independently checked.