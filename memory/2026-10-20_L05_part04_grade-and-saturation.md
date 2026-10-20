# Lecture 5 Part 4 — Grade and Krylov saturation

status: explained; comprehension not yet verified
last-updated: 2026-10-20
source_paths: uploaded Lecture5-KrylovSpaces.pdf slides 11-14; knowledge/modules/06-krylov-arnoldi-fom-gmres.md

Studied: grade of nonzero vector v relative to A is the degree mu of the smallest monic polynomial q_mu satisfying q_mu(A)v=0. Equivalently, mu is the first power for which A^mu v lies in the span of v through A^(mu-1)v. This gives dim K_m(A,v)=min(m,mu). Once K_mu is closed under multiplication by A (A-invariant), higher powers cannot add directions and K_m=K_mu for every m>=mu.

Original 2x2 example: A=[[4,1],[1,3]], b=[1,2], Ab=[6,7], A2b=[31,27]=7Ab-11b. First two vectors independent; the third dependent; grade(b,A)=2. For a 3x3 illustration of early saturation, D=diag(1,2,3), v=[1,0,1]. Av=[1,0,3], A2v=[1,0,9]=4Av-3v. Thus grade(v,D)=2 despite ambient dimension 3. Distinguish relative minimal polynomial of vector from polynomial annihilating whole matrix.

Practical distinction: grade predicts the maximal independent Krylov space, not the desired runtime stopping criterion, which monitors a residual tolerance and can stop earlier. Exact dependence is theoretical exact-arithmetic statement; numerical methods need stability checks.

Next: Lecture 5 Part 5, Arnoldi and Gram-Schmidt, slides 15-18. Learner comprehension pending.