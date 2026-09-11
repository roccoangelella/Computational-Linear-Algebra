# Depth supplement 11 - Numerical computation of the SVD

This supplement expands the computational part of `knowledge/modules/11-singular-value-decomposition.md` using the final SVD lectures.

## 1. Why the existence proof is not the preferred algorithm

From

`A^T A v_i = sigma_i^2 v_i`,

one can mathematically obtain singular values by solving the eigenproblem for `A^T A`. Numerically, explicitly forming `A^T A` is often undesirable:

- the 2-norm condition number is squared: `kappa_2(A^T A)=kappa_2(A)^2` for full column rank;
- small singular values become squared and can lose relative accuracy;
- forming the product can destroy sparsity/structure and add arithmetic.

A robust SVD algorithm instead reduces `A` to a simpler matrix using orthogonal transformations, which preserve singular values without squaring the problem first.

## 2. Orthogonal equivalence

If `Q` and `Z` are orthogonal and

`B=Q^T A Z`,

then `A` and `B` have the same singular values because

`B^T B = Z^T A^T A Z`.

Thus `B^TB` is orthogonally similar to `A^TA`. This is the SVD analogue of using orthogonal similarity transformations in eigenvalue algorithms.

The goal is therefore to choose `Q,Z` so that `B` has a structure that is cheap to solve.

## 3. Bidiagonal form

For a general real `m x n` matrix, orthogonal Householder transformations can reduce it to bidiagonal form: nonzeros remain only on the main diagonal and one adjacent diagonal (upper bidiagonal when `m>=n` in the common convention).

Schematically,

`B = Q^T A Z`.

The reduction alternates transformations from the left and right:

1. a left Householder reflector zeros entries below the current diagonal element in a column;
2. a right Householder reflector zeros entries to the right of the first superdiagonal position in the corresponding row;
3. repeat on the trailing submatrix.

Earlier zeros are preserved because each reflector is embedded to act only on the active trailing block.

## 4. First bidiagonalization step

Assume `m>=n`. For the first column, construct a Householder `H_1` so that

`H_1 A[:,1]`

has zeros below its first component. After applying `H_1` from the left, consider the remaining part of the first row. Construct a right reflector `G_1` so that multiplying from the right makes that row zero beyond its first superdiagonal entry.

After these two transformations the first column and row have the desired bidiagonal structure. The process continues recursively on rows/columns `2:`.

No eigenvalues have been computed yet: this phase is only a stable structural reduction.

## 5. Accumulating singular vectors

Suppose the sequence of left reflectors produces an orthogonal product `Q` and the right reflectors produce `Z`, with

`B=Q^T A Z`.

Now compute an SVD of the bidiagonal matrix:

`B = U_B Sigma V_B^T`.

Then

`A = Q U_B Sigma V_B^T Z^T`.

Therefore singular-vector matrices for `A` are obtained as

`U = Q U_B`,

`V = Z V_B`.

In practical software, reflectors are normally stored compactly and applied/accumulated as needed rather than materializing every full dense reflector.

## 6. Solving the bidiagonal problem

Once bidiagonal, the singular-value problem is much cheaper and more structured. Specialized iterative methods can work on `B` (or closely related tridiagonal eigenproblems) while preserving the bidiagonal structure and exploiting shifts/deflation ideas analogous to QR eigenvalue algorithms.

The conceptual separation is important:

- **reduction phase:** turn a general dense matrix into bidiagonal form with orthogonal transformations;
- **iteration phase:** compute singular values/vectors of the structured matrix;
- **back-transformation phase:** recover singular vectors of the original matrix.

This same architecture appeared for dense eigenvalues: reduce to Hessenberg/tridiagonal form, iterate on the structured matrix, then recover vectors if needed.

## 7. Deflation and numerical zero

As the iterative bidiagonal solver progresses, off-diagonal entries can become negligible. When they are small relative to neighboring scales, the problem can split into smaller blocks. This is numerical deflation.

The threshold must be scale-aware. Setting an entry to zero because it is small in absolute magnitude can be incorrect if the whole matrix is similarly small.

## 8. Singular values and conditioning during computation

If singular values span many orders of magnitude, the smallest ones are the most difficult to compute relatively accurately. This is exactly the regime where solving through `A^T A` is most dangerous because squaring magnifies the dynamic range.

When an application uses `1/sigma_i`, as in a pseudoinverse, small errors in tiny singular values can be greatly amplified. That is why numerical rank/tolerance and regularized truncation are not cosmetic post-processing choices.

## 9. Connection to least squares and pseudoinverse

Once an SVD is available,

`x^+ = sum_{i=1}^r (u_i^T b / sigma_i) v_i`.

This formula makes numerical sensitivity visible: components associated with small `sigma_i` are magnified. A truncated SVD replaces the reciprocals of very small singular values by zero, trading bias for stability.

Thus the computational SVD and the theory of conditioning are the same story: the algorithm exposes the directions in which inversion is reliable or unstable.

## 10. Connection to PCA

For centered data `X_c`, the right singular vectors are PCA directions and `sigma_i^2/(m-1)` are covariance eigenvalues under the sample convention. Computing PCA directly from an SVD of the centered/scaled data avoids explicitly forming the covariance matrix and is often the numerically preferred route, especially when dimensions are unbalanced.

## 11. Deep-understanding checkpoint

Be able to explain why `A^T A` is mathematically valid but numerically risky; prove that left/right orthogonal transformations preserve singular values; describe one full left-right Householder bidiagonalization step; show how singular vectors of the bidiagonal matrix map back to those of `A`; connect deflation to structured iterations; and explain why small singular values govern pseudoinverse/least-squares sensitivity.

## Sources

Primary: `Slides/EigenValues/6 - Singular value decomposition.pdf` and the SVD/computation portions of transcripts `38Lecture1215.txt` through `42Lecture0107.txt`. The Householder prerequisite is `knowledge/depth/03-qr-construction-details.md`.
