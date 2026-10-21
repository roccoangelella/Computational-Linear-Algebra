# Arnoldi stopping condition — short review

status: explained; learner comprehension not independently verified
last-updated: 2026-10-21
source_paths: knowledge/modules/06-krylov-arnoldi-fom-gmres.md; user-uploaded Lecture5-KrylovSpaces.pdf slides 15-18

The candidate A v_j is orthogonalized against all existing Arnoldi basis vectors. The remainder w_j=A v_j - sum_(i=1)^j h_ij v_i and norm h_(j+1),j=||w_j||_2 determine whether a new basis vector exists. If h_(j+1),j=0 in exact arithmetic, no independent direction remains, Arnoldi stops, and the Krylov subspace is invariant and saturated. Example A=[[4,1],[1,3]], v1=[1,2]/sqrt(5), v2=[2,-1]/sqrt(5), A v2=v1+3v2, so w2=0, K3=K2, grade=2. Small floating-point remainders need care before treating as exact breakdown.
