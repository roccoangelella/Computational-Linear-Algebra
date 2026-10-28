# Clarification — d in GMRES/Givens example

Date: 2026-10-28
Status: explained; understanding not independently checked.
Source: knowledge/modules/06-krylov-arnoldi-fom-gmres.md; previous Part 10 examples.

The new symbol d was introduced without explanation, causing confusion. It is only an optional shorthand for the reduced right-hand side d=beta e1 in the GMRES least-squares problem min ||beta e1-Hbar_m y||. beta=||r0|| and e1 is the first coordinate vector of length m+1. At m=1 in the example b=[1,1,0], x0=0, beta=sqrt(2), e1=[1,0], so d=[sqrt(2),0]. This two-entry coordinate vector is NOT the original three-entry residual; r0=V2 d since v1=r0/beta. Prefer avoiding d entirely and use beta e1 explicitly when explaining the first Givens rotation. The complete minimized expression is ||[sqrt(2),0] - [3,1]*y1||_2.
