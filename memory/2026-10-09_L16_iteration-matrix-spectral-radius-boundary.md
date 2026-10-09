# Study clarification 2026-10-09

Status: explanation provided, verification pending.

Question: Why can spectral radii differ for Jacobi and Gauss-Seidel on the same A? What does radius exactly 1 mean?

Key idea: B is method-dependent, not only A-dependent. Jacobi and Gauss-Seidel use different update rules, hence different B matrices.

Illustration: for A = [[1,-t],[-t,1]], t>=0, Jacobi has B_J=[[0,t],[t,0]], eigenvalues +/-t; Gauss-Seidel has B_GS=[[0,t],[0,t*t]], eigenvalues 0,t*t. Consequently rhoJ=t and rhoGS=t*t. Cases t=0, 0.5, 1, and values greater than 1 reproduce the four Stein-Rosenberg regimes from lecture slide 31.

At t=1 and b=0, A is singular and both radii equal 1. With x0=(0,1), Jacobi alternates between (0,1) and (1,0), while Gauss-Seidel reaches (1,1), a different valid solution than x*=0. Thus spectral radius 1 rules out B^k tending to zero, not all conceivable sequences converging.

Still to verify learner comprehension: method-specific B, eigenvalue of modulus 1 and lack of guaranteed error decay. Sources: knowledge/modules/04-stationary-iterative-methods.md and knowledge/depth/04-stationary-convergence-details.md. 