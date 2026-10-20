# Lecture 5 — Part 5: Basic Arnoldi and Gram–Schmidt

status: explanation delivered; comprehension pending
last-updated: 2026-10-20

source_paths:
- user-uploaded Lecture5-KrylovSpaces.pdf, slides 15–18
- knowledge/modules/06-krylov-arnoldi-fom-gmres.md
- memory/2026-10-20_L05_part04_grade-and-saturation.md

Covered:
- Why the raw Krylov power basis may be numerically problematic: poor scaling and nearly parallel directions.
- Arnoldi constructs an orthonormal basis (unit length and pairwise orthogonality) for the same Krylov space, via Gram–Schmidt.
- Starting with nonzero residual b, let v1=b/||b||. At iteration j compute A vj, Gram–Schmidt coefficients hij=vi^T(A vj), orthogonal remainder wj=A vj-sum_i hij vi, and subdiagonal coefficient h_(j+1),j=||wj||. If nonzero normalize v_(j+1)=wj/h_(j+1),j.
- Explained each coefficient's purpose, why subtracting projections removes existing directions, why normalization matters, and that Arnoldi basis vectors are still polynomial expressions in A applied to b.
- Original example A=[[4,1],[1,3]], b=[1,2]: v1=[1,2]/sqrt(5), A v1=[6,7]/sqrt(5), h11=4, w1=[2,-1]/sqrt(5), h21=1, v2=[2,-1]/sqrt(5). Inner product v1^T v2=0.
- Next iteration A v2=[7,-1]/sqrt(5), h12=1, h22=3, w2=0, consistent with grade 2. A zero remainder indicates no further independent Krylov direction in exact arithmetic (happy breakdown).
- Distinguish constructing the basis from computing the solution: the later FOM/GMRES step determines approximation coefficients.
- Careful geometry note: v2=[2,-1]/sqrt(5) points right and down in standard coordinates; do not graph it upward.

Comprehension: not independently verified.
Next: Lecture 5 Part 6, Arnoldi matrix relations, breakdown, stability (slides 19–24).