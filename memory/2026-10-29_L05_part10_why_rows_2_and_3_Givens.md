# Part 10 Givens: Why rotate rows 2 and 3?

status: clarification delivered; learner understanding pending
last-updated: 2026-10-29
source_paths: knowledge/depth/06-krylov-projection-and-gmres-implementation.md; memory/2026-10-28_L05_part10_Givens_in_GMRES.md

After the first rotation, Hbar2=[[sqrt(10),6/sqrt(10)],[0,8/sqrt(10)],[0,sqrt(2)]]. The only remaining nonzero subdiagonal entry is at row 3, column 2. To make an upper triangular matrix, Givens acts on the pair from rows 2 and 3 of column 2, [8/sqrt(10),sqrt(2)], yielding [sqrt(42/5),0]. The same rotation acts on rows 2 and 3 in the entire matrix, but in column 1 both entries are zero, so they stay zero and earlier work is preserved. Mixing rows 1 and 3 instead could introduce a new nonzero entry at row 3, column 1 because its current entries are [sqrt(10),0]. State the general rule: eliminate a subdiagonal entry at (j+1,j) by mixing rows j and j+1, preserving already formed zeros. Givens preserves norm and moves magnitude, rather than deleting a nonzero contribution.
