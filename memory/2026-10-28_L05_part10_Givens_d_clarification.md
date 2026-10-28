# Part 10 GMRES notation clarification: d

Status: clarification provided; learner comprehension not independently verified.
Date: 2026-10-28
Source: knowledge/modules/06-krylov-arnoldi-fom-gmres.md; memory/2026-10-28_L05_part10_Givens_in_GMRES.md.

In the explanation of GMRES Givens rotations, the letter d was introduced without a definition. It was merely a pedagogical shorthand for beta e1, not a new mathematical object. In the established example x0=0, b=[1,1,0], so r0=b and beta=||r0||=sqrt2. At the first Arnoldi step e1=[1,0], hence d=beta e1=[sqrt2,0]. This is the right-hand side of min_y ||beta e1-Hbar1 y||, not the original b. Applying G1 to the whole least-squares difference requires rotating beta e1 and Hbar1 consistently: G1(beta e1-Hbar1*y)=G1(beta e1)-(G1 Hbar1)*y. Prefer the established notation beta e1; avoid unannounced symbols.
