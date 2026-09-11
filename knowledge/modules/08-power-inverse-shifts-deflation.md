# Module 8 - Eigenvalues: power methods, shifts and deflation

## 1. Eigenpairs

For a square matrix `A in C^{n x n}`, an eigenpair `(lambda,x)` satisfies

`Ax = lambda x`, with `x != 0`.

The scalar `lambda` is an eigenvalue and `x` an eigenvector. Multiplying an eigenvector by any nonzero scalar gives another eigenvector for the same eigenvalue, so algorithms usually normalize eigenvectors, often to `||x||_2=1`.

Primary sources: `Slides/EigenValues/1 - Power Methods.pdf`, `2 - Shifting, deflation.pdf`, `lab-deflation.pdf`; transcripts `26Lecture1114.txt` through `28Lecture1119.txt`. Detailed course-specific shifting/Householder-deflation mechanics are restored in `knowledge/depth/08-power-shifting-householder-deflation.md`.

## 2. Characteristic polynomial and multiplicities

Eigenvalues are roots of the characteristic polynomial

`p_A(lambda)=det(A-lambda I)`.

The **algebraic multiplicity** of an eigenvalue is its multiplicity as a root of `p_A`. The **geometric multiplicity** is the dimension of its eigenspace `ker(A-lambda I)`.

For every eigenvalue,

`1 <= geometric multiplicity <= algebraic multiplicity`.

A matrix is diagonalizable when it possesses `n` linearly independent eigenvectors. Equivalently, the eigenspaces together supply `n` independent vectors.

If `X=[x_1,...,x_n]` contains an eigenbasis and `D=diag(lambda_1,...,lambda_n)`, then

`AX=XD`, hence `A=XDX^{-1}`.

For a real symmetric matrix, the spectral theorem gives the stronger orthogonal diagonalization

`A=Q Lambda Q^T`, with `Q^TQ=I` and real eigenvalues.

## 3. Similarity

Matrices `A` and `B` are **similar** if

`B=S^{-1}AS`

for an invertible `S`. Similar matrices represent the same linear operator in different bases and have the same characteristic polynomial/eigenvalues.

Similarity is especially important for the Householder deflation method taught in this course: an orthogonal change of basis isolates a known eigenpair without changing the spectrum, after which a smaller trailing block remains to be solved.

## 4. Power iteration

Suppose `A` is diagonalizable and its eigenvalues are ordered by magnitude

`|lambda_1| > |lambda_2| >= ... >= |lambda_n|`.

Expand the starting vector in the eigenbasis:

`x^(0)=c_1 v_1+...+c_n v_n`, with `c_1 != 0`.

Then

`A^k x^(0) = c_1 lambda_1^k [v_1 + sum_{j=2}^n (c_j/c_1)(lambda_j/lambda_1)^k v_j]`.

After normalization, the terms involving smaller eigenvalue ratios decay, so the direction converges to the dominant eigenvector `v_1` up to sign/phase.

Algorithmically:

1. choose `x^(0)` with `||x^(0)||_2=1`;
2. compute `y=A x^(k)`;
3. normalize `x^(k+1)=y/||y||_2`;
4. estimate the eigenvalue, commonly with a Rayleigh quotient;
5. stop when an appropriate convergence test is satisfied.

## 5. Convergence rate of power iteration

Under the simple dominant-eigenvalue assumptions, the asymptotic **directional** error behaves roughly like

`|lambda_2/lambda_1|^k`.

Thus convergence is fast when the dominant eigenvalue is well separated in magnitude and slow when the two largest magnitudes are close.

If the initial vector has zero component in the dominant eigendirection, the method cannot generate that component in exact arithmetic and instead converges according to the largest eigenvalue present in the initial expansion. If multiple eigenvalues share the same dominant magnitude, simple directional convergence can fail or oscillate.

For a real symmetric matrix, orthogonality of the eigenbasis gives an additional course result: the Rayleigh-quotient **eigenvalue error** is second order in the eigendirection error, and under the standard simple-dominant setting behaves like

`O(|lambda_2/lambda_1|^(2k))`.

This is the precise meaning behind the lecture statement that the eigenvalue convergence rate “doubles” in the symmetric case. See the Module 8 depth supplement for the distinction between eigenvector and eigenvalue convergence.

## 6. Rayleigh quotient

For a nonzero real vector `x`, the Rayleigh quotient is

`R_A(x)=x^T A x/(x^T x)`.

If `x` is an exact eigenvector, `R_A(x)` equals its eigenvalue. For symmetric `A`, the Rayleigh quotient has especially strong geometric properties: its minimum and maximum over nonzero vectors are the smallest and largest eigenvalues.

When an approximate eigenvector is available, `R_A(x)` is a natural eigenvalue estimate.

## 7. Residual for an approximate eigenpair

Given normalized `x` and scalar `mu`, define

`r = Ax-mu x`.

An exact eigenpair has `r=0`. Therefore `||r||` is the natural computable measure of how closely the pair satisfies the eigenvalue equation.

Stopping based only on changes in `x` can be misleading because eigenvectors are defined up to sign; stopping based only on successive eigenvalue estimates can be cheap but does not by itself certify the full eigenpair. The residual is the most direct verification quantity.

## 8. Computational cost of a power step

The dominant cost is the matrix-vector product.

- For a dense `n x n` matrix, a matvec costs `O(n^2)` arithmetic.
- For a sparse matrix, a storage-aware matvec costs `O(nnz(A))`.

This is why the power method can scale to PageRank-sized graph problems: it can avoid matrix factorization and repeatedly use only sparse products.

## 9. Inverse power iteration

If `A` is nonsingular, eigenvectors of `A^{-1}` are the same as those of `A`, while eigenvalues become `1/lambda_i`. Therefore applying power iteration to `A^{-1}` targets the eigenvalue of `A` with smallest magnitude.

Do **not** form `A^{-1}` explicitly. Each iteration solves

`A y = x^(k)`

and normalizes `y`.

If many iterations use the same matrix, a factorization can be computed once and reused for the solves.

## 10. Shifted inverse iteration

For a scalar shift `sigma`, consider

`(A-sigma I)^{-1}`.

Its eigenvectors remain those of `A`, while eigenvalues become

`1/(lambda_i-sigma)`.

The dominant transformed eigenvalue corresponds to the eigenvalue of `A` closest to `sigma`. Therefore shifted inverse iteration can target an interior eigenvalue rather than only an extreme one.

Each iteration solves

`(A-sigma I)y=x^(k)`.

A good shift can yield very fast convergence, but if `sigma` is extremely close to an eigenvalue the shifted matrix becomes ill-conditioned; if `sigma` equals an eigenvalue exactly, it is singular.

## 11. Rayleigh quotient iteration

A natural adaptive shift is the current Rayleigh quotient

`sigma_k = R_A(x^(k))`.

Then solve

`(A-sigma_k I)y=x^(k)`

and normalize. For symmetric matrices and a sufficiently good starting vector, Rayleigh quotient iteration has very rapid local convergence. It is a shift strategy rather than a fundamentally separate eigenspace principle.

## 12. Scalar spectral shifting

For

`B=A-sigma I`,

eigenvectors are unchanged and eigenvalues become `lambda_i-sigma`. For `A+sigma I`, eigenvalues shift by `+sigma`.

This identity underlies shifted inverse iteration. It should be distinguished from the course's next construction, which also uses the word **shifting** but modifies one known symmetric eigenpair by a rank-one term.

## 13. Course “shifting”: move a known symmetric eigenvalue to zero

Let `A=A^T`, and suppose `(lambda_1,v_1)` is a known eigenpair with `||v_1||_2=1`. Define

`A_1 = A - lambda_1 v_1 v_1^T`.

Because symmetric eigenvectors can be chosen orthonormal,

`A_1 v_1=0`,

while

`A_1 v_j=lambda_j v_j` for `j != 1`.

Thus the already-computed eigenvalue is moved to zero and the remaining symmetric eigenpairs are preserved in exact arithmetic. Repeating the power method on the modified matrix can expose successive eigenpairs when the magnitude ordering is favorable.

This rank-one spectral modification is called **shifting** in the supplied lectures. Many external texts call essentially this construction rank-one or Hotelling **deflation**; when preparing for the course, state the formula and follow the course terminology.

Repeated finite-precision shifts can accumulate error because each update uses an approximate eigenpair. The deflation laboratory checks this by evaluating eigen-residuals against the original matrix.

## 14. Course “deflation”: Householder similarity and dimension reduction

The separate deflation method taught in the course uses a known eigenvector to construct an orthogonal Householder matrix `P_1` satisfying, up to sign,

`P_1 v_1 = e_1`.

Then

`B_1 = P_1 A P_1^T`

is orthogonally similar to `A` and therefore has exactly the same eigenvalues. Its first column isolates `lambda_1`, so it has block upper-triangular form

`B_1 = [[lambda_1, b^T],[0,A_2]]`.

The eigenvalues of the trailing `(n-1)x(n-1)` block `A_2` are the remaining eigenvalues. If `A` is symmetric, `B_1` is also symmetric, forcing `b=0`, so the first eigenpair is cleanly separated from the smaller symmetric problem.

The procedure is then applied recursively to `A_2`. Eigenvectors computed in reduced coordinates must be embedded and transformed back through the accumulated Householder transformations to obtain eigenvectors of the original matrix.

The full derivation, recursive algorithm and comparison with rank-one shifting are in `knowledge/depth/08-power-shifting-householder-deflation.md`.

## 15. Why orthogonal deflation is attractive

An orthogonal matrix preserves Euclidean norms and has 2-norm condition number one. Householder deflation therefore changes coordinates through a numerically benign similarity transformation rather than repeatedly perturbing the full matrix by inexact rank-one spectral updates.

This does not remove floating-point error, but it explains why the course laboratory compares the two strategies and observes cleaner behavior from deflation on difficult examples.

## 16. Relationship to PageRank

PageRank is a dominant-eigenvector/stationary-distribution problem for a large sparse stochastic matrix after handling dangling nodes and introducing damping. Basic power iteration is therefore directly relevant: PageRank can be computed by repeated sparse matrix-vector products.

## 17. Practical algorithm checks

For eigenvalue iterations, monitor:

- normalization of the iterate;
- eigen-residual `||Ax-lambda x||`;
- convergence of the Rayleigh quotient/eigenvalue estimate;
- whether sign changes alone are being mistaken for nonconvergence;
- spectral separation controlling power/inverse convergence;
- linear-solve conditioning for inverse/shifted methods;
- residuals against the **original** matrix after repeated shifting/deflation;
- correct back-transformation of eigenvectors produced by reduced deflation problems.

## 18. Exam checklist

Be able to define algebraic/geometric multiplicity and diagonalizability; explain similarity; derive power-method convergence from an eigenbasis expansion; distinguish the `|lambda_2/lambda_1|^k` eigendirection rate from the squared symmetric Rayleigh-quotient rate; derive inverse and shifted inverse iteration; define the Rayleigh quotient and eigen-residual; derive the course rank-one shifting formula; derive the Householder deflation block reduction and explain why symmetry makes it block diagonal; and explain how reduced eigenvectors are mapped back to the original coordinates.

## 19. Sources

- `Slides/EigenValues/1 - Power Methods.pdf`
- `Slides/EigenValues/2 - Shifting, deflation.pdf`
- `Slides/EigenValues/lab-deflation.pdf`
- `Slides/Trascrizioni/26Lecture1114.txt`
- `Slides/Trascrizioni/27Lecture1117.txt`
- `Slides/Trascrizioni/28Lecture1119.txt`
- opening eigenvalue review in `Slides/Trascrizioni/35Lecture1205.txt`
- detailed supplement: `knowledge/depth/08-power-shifting-householder-deflation.md`
