# Part 10 clarification: origin of second Givens pair

status: explanation delivered, learner comprehension unverified
last-updated: 2026-10-28
source_paths: memory/2026-10-28_L05_part10_Givens_in_GMRES.md; knowledge/depth/06-krylov-projection-and-gmres-implementation.md

In the previous 3x2 Hessenberg example, Hbar2=[[3,1],[1,3],[0,sqrt(2)]]. First rotation Omega1 acts on rows 1 and 2 with c=3/sqrt(10), s=1/sqrt(10). Applied to the SECOND COLUMN [1,3,sqrt(2)]^T it produces [6/sqrt(10),8/sqrt(10),sqrt(2)]^T: row 1 is (3*1+1*3)/sqrt(10), row 2 is (-1*1+3*3)/sqrt(10)=8/sqrt(10), row 3 unchanged sqrt(2). The second rotation acts specifically on rows 2,3 to remove the subdiagonal entry in row 3, col 2, so it uses a=8/sqrt(10) and b=sqrt(2). These numbers are not arbitrary and row 1 does not participate. No new independent topic introduced; clarification reinforces the GMRES Givens QR lesson.