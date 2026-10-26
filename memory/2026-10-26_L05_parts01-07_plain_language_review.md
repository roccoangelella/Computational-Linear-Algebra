# Lecture 5 parts 1-7: Plain-language integrated review

status: recap delivered; mastery not independently verified
last-updated: 2026-10-26
source_paths: knowledge/modules/06-krylov-arnoldi-fom-gmres.md; memory/2026-10-20_L05_part04_grade-and-saturation.md; memory/2026-10-21_L05_part07_FOM-and-restarted-FOM.md; user-uploaded Lecture5-KrylovSpaces.pdf slides 2-29

Learner requested a simple recap because the lecture's multiple terms feel hard to retain. Organized the prior learning as one procedure rather than disconnected definitions.

Reviewed: Ax=b and residual r0=b-Ax0; Krylov search space span(r0,Ar0,...); polynomial view; minimal polynomial relative to the starting residual and its degree (grade), saturation, and theoretical role of Cayley-Hamilton; Arnoldi's Gram-Schmidt orthonormalization of Krylov directions and stopping on zero remainder; V_m as directions and H_m=V_m^T A V_m as the projected small matrix; FOM's deliberate Galerkin condition, reduced system H_m y_m=beta e1, reconstruction x_m=x0+V_m y_m; residual testing and restart if continued basis growth is too expensive. Contrasted exact saturation with practical stopping from small residual norm. GMRES not yet studied; next is part 8.

Previously grounded examples: 2x2 A=[[4,1],[1,3]], b=[1,2], grade 2 because A2b=7Ab-11b; 3x3 A=[[4,0,1],[0,2,-1],[1,-1,3]], b=[1,1,0], V2 from [1,1,0] and [1,-1,0], H2=[[3,1],[1,3]], FOM x2=[1/4,1/2,0], residual=[0,0,1/4].

Main teaching need: keep high-level story explicit, explain why each stage exists before adding notation, and avoid accumulating new terms without connecting them to solving the system.