# Module 8 - Eigenvalues: power methods, shifts and deflation

## 1. Eigenpairs

For a square matrix `A in C^{n x n}`, an eigenpair `(lambda,x)` satisfies

`Ax = lambda x`, with `x != 0`.

The scalar `lambda` is an eigenvalue and `x` an eigenvector. Multiplying an eigenvector by any nonzero scalar gives another eigenvector for the same eigenvalue, so algorithms usually normalize eigenvectors, often to `||x||_2=1`.

Primary sources: `Slides/EigenValues/1 - Power Methods.pdf`, `2 - Shifting, deflation.pdf`, `lab-deflation.pdf`; transcripts `26Lecture1114.txt` through `28Lecture1119.txt`.

## 2. Characteristic polynomial and multiplicities

Eigenvalues are roots of the characteristic polynomial

`p_A(lambda)=det(A-lambda I)`.

The **algebraic multiplicity** of an eigenvalue is its multiplicity as a root of `p_A`. The **geometric multiplicity** is the dimension of its eigenspace `ker(A-lambda I)`.

For every eigenvalue,

`1 <= geometric multiplicity <= algebraic multiplicity`.

A matrix is diagonalizable when it possesses `n` linearly independent eigenvectors. Equivalently, the geometric and algebraic multiplicities combine so that the eigenspaces supply `n` independent vectors.

If `X=[x_1,...,x_n]` contains an eigenbasis and `D=diag(lambda_1,...,lambda_n)`, then

`AX=XD`, hence `A=XDX^{-1}`.

For a real symmetric matrix, the spectral theorem gives the stronger orthogonal diagonalization

`A=Q Lambda Q^T`, with `Q^TQ=I` and real eigenvalues.

## 3. Similarity

Matrices `A` and `B` are **similar** if

`B=S^{-1}AS`

for an invertible `S`. Similar matrices represent the same linear operator in different bases and have the same characteristic polynomial/eigenvalues.

Similarity transformations are central to eigenvalue algorithms: the goal is often to transform `A` into a simpler similar matrix whose eigenvalues are visible, without changing the spectrum.

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
5. stop when the residual `Ax-lambda x` is sufficiently small.

## 5. Convergence rate of power iteration

Under the simple dominant-eigenvalue assumptions, the asymptotic directional error behaves roughly like

`|lambda_2/lambda_1|^k`.

Thus convergence is fast when the dominant eigenvalue is well separated in magnitude and slow when the two largest magnitudes are close.

If the initial vector has zero component in the dominant eigendirection, the method cannot generate that component in exact arithmetic and instead converges according to the largest eigenvalue present in the initial expansion.

If multiple eigenvalues share the same dominant magnitude, simple directional convergence can fail or oscillate.

## 6. Rayleigh quotient

For a nonzero real vector `x`, the Rayleigh quotient is

`R_A(x)=x^T A x/(x^T x)`.

If `x` is an exact eigenvector, `R_A(x)` equals its eigenvalue. For symmetric `A`, the Rayleigh quotient has especially strong geometric properties: its minimum and maximum over nonzero vectors are the smallest and largest eigenvalues.

When an approximate eigenvector is available, `R_A(x)` is a natural eigenvalue estimate.

## 7. Residual for an approximate eigenpair

Given normalized `x` and scalar `mu`, define

`r = Ax-mu x`.

An exact eigenpair has `r=0`. Therefore `||r||` is the natural computable measure of how closely the pair satisfies the eigenvalue equation.

Stopping based only on changes in `x` can be misleading because eigenvectors are defined up to sign; using the eigen-residual avoids this ambiguity.

## 8. Inverse power iteration

If `A` is nonsingular, eigenvectors of `A^{-1}` are the same as those of `A`, while eigenvalues become `1/lambda_i`. Therefore applying power iteration to `A^{-1}` targets the eigenvalue of `A` with smallest magnitude.

Do **not** form `A^{-1}` explicitly. Each iteration solves

`A y = x^(k)`

and normalizes `y`.

If many iterations use the same matrix, a factorization can be computed once and reused for the solves.

## 9. Shifted inverse iteration

For a scalar shift `sigma`, consider

`(A-sigma I)^{-1}`.

Its eigenvectors remain those of `A`, while eigenvalues become

`1/(lambda_i-sigma)`.

The dominant transformed eigenvalue corresponds to the eigenvalue of `A` closest to `sigma`. Therefore shifted inverse iteration can target an interior eigenvalue rather than only an extreme one.

Each iteration solves

`(A-sigma I)y=x^(k)`.

A good shift can yield very fast convergence, but if `sigma` is extremely close to an eigenvalue the shifted matrix becomes ill-conditioned. The mathematical amplification that accelerates eigenvector selection also makes the linear solve sensitive.

## 10. Rayleigh quotient iteration

A natural adaptive shift is the current Rayleigh quotient

`sigma_k = R_A(x^(k))`.

Then solve

`(A-sigma_k I)y=x^(k)`

and normalize. For symmetric matrices and a sufficiently good starting vector, Rayleigh quotient iteration has very rapid local convergence. It is a shift strategy rather than a fundamentally separate eigenspace principle.

## 11. Shifting the spectrum

For

`B=A-sigma I`,

eigenvectors are unchanged and eigenvalues become `lambda_i-sigma`. This elementary identity is exploited throughout eigenvalue algorithms to move the part of the spectrum of interest into a favorable location.

For

`A+sigma I`,

eigenvalues shift by `+sigma`.

Shifts do not alter eigenvectors, but they do alter magnitude ordering, separation and conditioning of inverse systems.

## 12. Deflation idea

Once an eigenpair has been found, one may want to remove its contribution so that another eigenpair becomes accessible. This is called **deflation**.

For a symmetric matrix with normalized eigenvector `v_1` and eigenvalue `lambda_1`, a simple rank-one deflation is

`A_1 = A - lambda_1 v_1 v_1^T`.

Because `v_1^T v_j=0` for other orthonormal eigenvectors,

`A_1 v_1=0`,

while

`A_1 v_j=lambda_j v_j` for `j != 1`.

Thus the already-computed eigenvalue is replaced by zero while the other symmetric eigenpairs are preserved.

This simple formula relies strongly on orthogonality/symmetry. Deflation for a general nonsymmetric matrix requires more care, often involving both right and left eigenvectors or similarity transformations.

## 13. Orthogonal projection view of deflation

For a normalized known eigenvector `v`, the projector onto its orthogonal complement is

`P=I-vv^T`.

For a symmetric matrix, working in the orthogonal complement of previously computed eigenvectors prevents the iteration from returning to those eigendirections. This gives a geometric interpretation of multi-eigenpair computation.

## 14. Relationship to PageRank

PageRank is a dominant-eigenvector/stationary-distribution problem for a large sparse stochastic matrix (after handling dangling nodes and introducing damping). Basic power iteration is therefore directly relevant: PageRank can be computed by repeated sparse matrix-vector products.

## 15. Practical algorithm checks

For any eigenvalue iteration, monitor:

- normalization of the iterate;
- eigen-residual `||Ax-lambda x||`;
- convergence of the Rayleigh quotient/eigenvalue estimate;
- whether sign changes alone are being mistaken for nonconvergence;
- the spectral separation that controls convergence;
- linear-solve conditioning for inverse/shifted methods.

## 16. Exam checklist

Be able to define algebraic/geometric multiplicity and diagonalizability; explain similarity; derive power-method convergence from an eigenbasis expansion; state the role of `|lambda_2/lambda_1|`; derive inverse and shifted inverse iteration; define the Rayleigh quotient; explain the eigen-residual; and derive symmetric rank-one deflation.

## 17. Sources

- `Slides/EigenValues/1 - Power Methods.pdf`
- `Slides/EigenValues/2 - Shifting, deflation.pdf`
- `Slides/EigenValues/lab-deflation.pdf`
- `Slides/Trascrizioni/26Lecture1114.txt`
- `Slides/Trascrizioni/27Lecture1117.txt`
- `Slides/Trascrizioni/28Lecture1119.txt`
