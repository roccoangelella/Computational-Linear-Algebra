# Depth supplement 11 - SVD existence, uniqueness and numerical computation

This supplement expands `knowledge/modules/11-singular-value-decomposition.md` using the final SVD lectures. It includes both the theorem-level construction emphasized in the course and the numerical bidiagonalization route used for computation.

## 1. Precise existence and uniqueness statement

For every `A in R^{m x n}` there exist orthogonal matrices `U in R^{m x m}` and `V in R^{n x n}` and a rectangular diagonal matrix `Sigma in R^{m x n}` such that

`A = U Sigma V^T`,

with diagonal entries

`sigma_1 >= sigma_2 >= ... >= sigma_p >= 0`, `p=min(m,n)`.

The ordered singular values are uniquely determined by `A`. The matrices `U` and `V` are generally **not** unique:

- every singular-vector pair can be multiplied by a common sign in the real case (or compatible complex phases in the complex case);
- when a positive singular value is repeated, any orthonormal basis of its singular subspace can be rotated within that subspace;
- bases of the left/right null spaces associated with zero singular values are likewise nonunique.

Thus the invariant singular subspaces and singular values are intrinsic; a particular orthonormal basis for them need not be.

## 2. First singular value from a variational problem

Consider the continuous function

`f(v)=||Av||_2`

on the unit sphere `||v||_2=1`. The sphere is compact, so `f` attains a maximum. Define

`sigma_1 = max_{||v||=1} ||Av||_2`,

and choose a maximizing unit vector `v_1`.

If `sigma_1>0`, set

`u_1 = Av_1/sigma_1`.

Then `||u_1||=1` and

`Av_1=sigma_1 u_1`.

Equivalently, maximizing `||Av||^2=v^T A^T A v` is the Rayleigh-quotient problem for the symmetric positive-semidefinite matrix `A^T A`. Therefore

`A^T A v_1 = sigma_1^2 v_1`.

Multiplying `Av_1=sigma_1u_1` by `A^T` gives

`A^T u_1=sigma_1 v_1`.

These paired equations are the first left/right singular-vector relations.

## 3. One-step block reduction behind the existence proof

Extend `u_1` to an orthonormal basis of `R^m` and `v_1` to an orthonormal basis of `R^n`. Put those bases into orthogonal matrices

`U_1=[u_1,U_perp]`, `V_1=[v_1,V_perp]`.

Then the first column of

`U_1^T A V_1`

is

`U_1^T A v_1 = sigma_1 e_1`.

The rest of the first row is also zero. Indeed, for any `w` orthogonal to `v_1`,

`u_1^T A w = (A^T u_1)^T w = sigma_1 v_1^T w = 0`.

Hence

`U_1^T A V_1 = [[sigma_1,0],[0,B]]`

with a smaller rectangular trailing matrix `B`.

This is the structural heart of the induction proof presented in the SVD lectures.

## 4. Induction completes the SVD existence proof

Apply the same construction recursively to `B`. By induction on the smaller dimension, there exist orthogonal `U_2,V_2` that diagonalize the trailing block in the singular-value sense.

Embed those factors into block-diagonal orthogonal matrices and multiply them into `U_1,V_1`. Repeating the process yields

`U^T A V = Sigma`.

Equivalently,

`A=U Sigma V^T`.

If at some stage the maximal singular value of the remaining block is zero, that entire remaining block is zero and the construction terminates immediately.

This proof is constructive at the level of linear-algebra existence, but it is not yet the preferred high-performance numerical algorithm: it establishes that the factorization exists and explains the geometry of paired left/right orthogonal directions.

## 5. Why the singular values are unique

From any SVD,

`A^T A = V Sigma^T Sigma V^T`.

Therefore the eigenvalues of `A^T A` are exactly

`sigma_1^2,...,sigma_p^2`

plus any dimension-required zeros. Eigenvalues of a fixed matrix are intrinsic, and singular values are defined as their nonnegative square roots, sorted in nonincreasing order. Hence the ordered diagonal of `Sigma` is unique.

This gives a short uniqueness proof even though the associated singular-vector bases can be nonunique.

## 6. Why the existence proof is not the preferred numerical algorithm

From

`A^T A v_i = sigma_i^2 v_i`,

one can mathematically obtain singular values by solving the eigenproblem for `A^T A`. Numerically, explicitly forming `A^T A` is often undesirable:

- the 2-norm condition number is squared: `kappa_2(A^T A)=kappa_2(A)^2` for full column rank;
- small singular values become squared and can lose relative accuracy;
- forming the product can destroy sparsity/structure and add arithmetic.

A robust SVD algorithm instead reduces `A` to a simpler matrix using orthogonal transformations, which preserve singular values without squaring the problem first.

## 7. Orthogonal equivalence

If `Q` and `Z` are orthogonal and

`B=Q^T A Z`,

then `A` and `B` have the same singular values because

`B^T B = Z^T A^T A Z`.

Thus `B^TB` is orthogonally similar to `A^TA`. This is the SVD analogue of using orthogonal similarity transformations in eigenvalue algorithms.

The goal is therefore to choose `Q,Z` so that `B` has a structure that is cheap to solve.

## 8. Bidiagonal form

For a general real `m x n` matrix, orthogonal Householder transformations can reduce it to bidiagonal form: nonzeros remain only on the main diagonal and one adjacent diagonal (upper bidiagonal when `m>=n` in the common convention).

Schematically,

`B = Q^T A Z`.

The reduction alternates transformations from the left and right:

1. a left Householder reflector zeros entries below the current diagonal element in a column;
2. a right Householder reflector zeros entries to the right of the first superdiagonal position in the corresponding row;
3. repeat on the trailing submatrix.

Earlier zeros are preserved because each reflector is embedded to act only on the active trailing block.

## 9. First bidiagonalization step

Assume `m>=n`. For the first column, construct a Householder `H_1` so that

`H_1 A[:,1]`

has zeros below its first component. After applying `H_1` from the left, consider the remaining part of the first row. Construct a right reflector `G_1` so that multiplying from the right makes that row zero beyond its first superdiagonal entry.

After these two transformations the first column and row have the desired bidiagonal structure. The process continues recursively on the lower-right trailing submatrix.

No singular values have been computed yet: this phase is only a stable structural reduction.

## 10. Accumulating singular vectors

Suppose the sequence of left reflectors produces an orthogonal product `Q` and the right reflectors produce `Z`, with

`B=Q^T A Z`.

Now compute an SVD of the bidiagonal matrix:

`B = U_B Sigma V_B^T`.

Then

`A = Q U_B Sigma V_B^T Z^T`.

Therefore singular-vector matrices for `A` are

`U = Q U_B`,

`V = Z V_B`.

In practical software, reflectors are normally stored compactly and applied/accumulated as needed rather than materializing every full dense reflector.

## 11. Solving the bidiagonal problem

Once bidiagonal, the singular-value problem is much cheaper and more structured. Specialized iterative methods can work on `B` or closely related tridiagonal eigenproblems while preserving structure and exploiting shifts/deflation ideas analogous to QR eigenvalue algorithms.

The conceptual separation is:

1. **reduction phase:** turn a general dense matrix into bidiagonal form with orthogonal transformations;
2. **iteration phase:** compute singular values/vectors of the structured matrix;
3. **back-transformation phase:** recover singular vectors of the original matrix.

This same architecture appeared for dense eigenvalues: reduce to Hessenberg/tridiagonal form, iterate on the structured matrix, then recover vectors if needed.

## 12. Deflation and numerical zero

As the iterative bidiagonal solver progresses, off-diagonal entries can become negligible. When they are small relative to neighboring scales, the problem can split into smaller blocks. This is numerical deflation.

The threshold must be scale-aware. Setting an entry to zero because it is small in absolute magnitude can be incorrect if the whole matrix is similarly small.

## 13. Singular values and conditioning during computation

If singular values span many orders of magnitude, the smallest ones are the most difficult to compute relatively accurately. This is exactly the regime where solving through `A^T A` is most dangerous because squaring magnifies the dynamic range.

When an application uses `1/sigma_i`, as in a pseudoinverse, small errors in tiny singular values can be greatly amplified. That is why numerical rank/tolerance and regularized truncation are not cosmetic post-processing choices.

## 14. Connection to least squares and pseudoinverse

Once an SVD is available,

`x^+ = sum_{i=1}^r (u_i^T b / sigma_i) v_i`.

This formula makes numerical sensitivity visible: components associated with small `sigma_i` are magnified. A truncated SVD replaces the reciprocals of very small singular values by zero, trading bias for stability.

Thus the computational SVD and the theory of conditioning are the same story: the algorithm exposes the directions in which inversion is reliable or unstable.

## 15. Connection to PCA

For centered data `X_c`, the right singular vectors are PCA directions and `sigma_i^2/(m-1)` are covariance eigenvalues under the sample convention. Computing PCA directly from an SVD of the centered/scaled data avoids explicitly forming the covariance matrix and is often the numerically preferred route, especially when dimensions are unbalanced.

## 16. Deep-understanding checkpoint

Be able to state precisely what is unique and nonunique in an SVD; derive `sigma_1=max_{||v||=1}||Av||`; derive the paired relations `Av_1=sigma_1u_1` and `A^Tu_1=sigma_1v_1`; show how extending those vectors to orthonormal bases gives a one-step block reduction; complete the existence proof by induction; prove uniqueness of the singular values through `A^TA`; explain why forming `A^T A` is mathematically valid but numerically risky; prove that left/right orthogonal transformations preserve singular values; describe one full left-right Householder bidiagonalization step; show how singular vectors of the bidiagonal matrix map back to those of `A`; connect deflation to structured iterations; and explain why small singular values govern pseudoinverse/least-squares sensitivity.

## Sources

Primary: `Slides/EigenValues/6 - Singular value decomposition.pdf` and the SVD/computation portions of transcripts `38Lecture1215.txt` through `42Lecture0107.txt`. The Householder prerequisite is `knowledge/depth/03-qr-construction-details.md`.
