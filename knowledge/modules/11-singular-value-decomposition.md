# Module 11 - Singular value decomposition

## 1. What the SVD is

For any matrix `A in R^{m x n}` (or `C^{m x n}`), let `p=min(m,n)`. The singular value decomposition writes

`A = U Sigma V^T`

in the real case, or `A=U Sigma V^*` in the complex case, where

- `U in R^{m x m}` is orthogonal;
- `V in R^{n x n}` is orthogonal;
- `Sigma in R^{m x n}` is diagonal in the rectangular sense;
- its diagonal entries satisfy
  `sigma_1 >= sigma_2 >= ... >= sigma_p >= 0`.

The `sigma_i` are the **singular values**. Columns `u_i` of `U` are left singular vectors and columns `v_i` of `V` are right singular vectors.

Unlike an eigenvalue decomposition, the SVD exists for **every** rectangular or square matrix. It is therefore a universal coordinate system for understanding the action of a linear map.

Primary sources: `Slides/EigenValues/6 - Singular value decomposition.pdf`; transcripts from the SVD part of `38Lecture1215.txt` through `42Lecture0107.txt`; PCA/SVD bridge notebook `test_SVD_vs_PCA.ipynb`.

## 2. Geometric interpretation

The factorization can be read from right to left:

1. `V^T` rotates/reflection-changes coordinates in the input space;
2. `Sigma` scales orthogonal coordinate directions by nonnegative factors `sigma_i`, possibly annihilating some of them;
3. `U` rotates/reflection-changes coordinates in the output space.

Thus any linear map can be understood as orthogonal input coordinates, axis-aligned scaling, then orthogonal output coordinates.

## 3. Relation to A^T A and AA^T

From

`A = U Sigma V^T`,

we obtain

`A^T A = V Sigma^T Sigma V^T`.

Therefore the right singular vectors are eigenvectors of `A^T A`, and

`A^T A v_i = sigma_i^2 v_i`.

Similarly,

`AA^T = U Sigma Sigma^T U^T`,

so left singular vectors satisfy

`AA^T u_i = sigma_i^2 u_i`.

Consequently singular values are the nonnegative square roots of the eigenvalues of `A^T A` (equivalently the nonzero eigenvalues of `AA^T`).

This does **not** imply that explicitly forming `A^T A` is always the best numerical algorithm for computing an SVD. Forming the product can square conditioning and lose relative information in small singular values.

## 4. Singular-vector equations

For each nonzero singular value,

`A v_i = sigma_i u_i`,

`A^T u_i = sigma_i v_i`.

These equations show how paired input/output directions are linked. A right singular vector is an input direction that is mapped exactly into the corresponding left singular direction with stretch factor `sigma_i`.

## 5. Rank and singular values

The rank of `A` is exactly the number of positive singular values:

`rank(A)=r` iff

`sigma_1 >= ... >= sigma_r > 0 = sigma_{r+1}=...`.

Therefore the SVD makes numerical rank visible. In floating point, 'zero' singular values are assessed relative to a tolerance; a sharp drop in the singular-value spectrum often indicates an effectively low-rank structure.

## 6. Fundamental subspaces from the SVD

Suppose `rank(A)=r`. Then

`Im(A) = span{u_1,...,u_r}`,

`ker(A^T) = span{u_{r+1},...,u_m}`,

`Im(A^T) = span{v_1,...,v_r}`,

`ker(A) = span{v_{r+1},...,v_n}`.

These are the four fundamental subspaces. The SVD therefore simultaneously exposes rank, image and null spaces.

## 7. Thin/reduced SVD

If `rank(A)=r`, the nonzero part can be written

`A = U_r Sigma_r V_r^T`,

where

- `U_r in R^{m x r}`;
- `Sigma_r in R^{r x r}` contains only positive singular values;
- `V_r in R^{n x r}`.

This reduced representation is often all that is needed for computation and makes low-rank structure explicit.

A compact SVD may instead keep `p=min(m,n)` columns even if some singular values are zero; terminology varies, so dimensions should always be stated.

## 8. Matrix norms

The SVD yields important norms immediately:

`||A||_2 = sigma_1`,

and the Frobenius norm satisfies

`||A||_F = sqrt(sum_i sigma_i^2)`.

If `A` is square and nonsingular,

`||A^{-1}||_2 = 1/sigma_n`,

so

`kappa_2(A)=sigma_1/sigma_n`.

For a rectangular full-rank problem the ratio of largest to smallest nonzero singular value similarly quantifies sensitivity on the relevant subspaces.

## 9. Outer-product expansion

The SVD can be expanded as

`A = sum_{i=1}^r sigma_i u_i v_i^T`.

Each term is rank one. The decomposition therefore orders rank-one contributions from strongest to weakest according to their singular values.

This expansion is the basis of optimal low-rank approximation and compression.

## 10. Best low-rank approximation: Eckart-Young-Mirsky

For `k<r`, define the truncated SVD

`A_k = sum_{i=1}^k sigma_i u_i v_i^T`.

Among all matrices `B` with `rank(B) <= k`, `A_k` is optimal in both spectral and Frobenius norms:

`min_{rank(B)<=k} ||A-B||_2 = sigma_{k+1}`,

and

`min_{rank(B)<=k} ||A-B||_F = sqrt(sum_{i=k+1}^r sigma_i^2)`.

This is one of the most important theoretical results in the course: if information is represented by a matrix and only rank `k` information may be retained, truncated SVD gives the best approximation for these norms.

## 11. Compression

A dense `m x n` matrix requires `mn` numbers. A rank-`k` truncated SVD can be represented by

- `U_k`: `mk` numbers;
- singular values: `k` numbers;
- `V_k`: `nk` numbers.

Total storage is approximately

`k(m+n+1)`.

Compression is beneficial when `k(m+n+1) << mn` and neglected singular values are small enough for the desired fidelity.

The lectures use image compression as an intuitive example: pixel intensity arrays can often be approximated by a much lower-rank matrix while retaining dominant visual structure.

## 12. Moore-Penrose pseudoinverse

For

`A=U Sigma V^T`,

define `Sigma^+` by transposing the rectangular diagonal layout and replacing each positive singular value by its reciprocal:

`sigma_i -> 1/sigma_i` for `i<=r`,

while zeros remain zero. Then

`A^+ = V Sigma^+ U^T`.

`A^+` is the **Moore-Penrose pseudoinverse**. It exists for every matrix, including rectangular and rank-deficient ones.

It is characterized by the four Penrose equations:

`AA^+A=A`,

`A^+AA^+=A^+`,

`(AA^+)^T=AA^+`,

`(A^+A)^T=A^+A`

in the real case.

## 13. Least-squares solution with the SVD

For arbitrary `A` and `b`, the vector

`x^+ = A^+ b`

is a least-squares solution:

`x^+ in argmin_x ||Ax-b||_2`.

If the least-squares minimizer is not unique because `A` is rank deficient, `A^+b` is the one with minimum Euclidean norm.

To see the filtering structure, expand `b` in the left singular basis:

`x^+ = sum_{i=1}^r (u_i^T b / sigma_i) v_i`.

Small singular values produce large factors `1/sigma_i`, explaining sensitivity and ill-conditioning.

## 14. Minimum-norm exact solutions

If `Ax=b` is consistent but underdetermined, there may be infinitely many exact solutions differing by vectors in `ker(A)`. `A^+b` is the exact solution orthogonal to `ker(A)`, equivalently the solution of smallest Euclidean norm.

This gives a canonical answer to an otherwise nonunique problem.

## 15. Projectors from the pseudoinverse

For rank `r`,

`AA^+ = U_r U_r^T`

is the orthogonal projector onto `Im(A)`, while

`A^+A = V_r V_r^T`

is the orthogonal projector onto `Im(A^T)`.

Thus the pseudoinverse unifies least squares and orthogonal projection.

## 16. SVD and PCA

For centered data matrix `X_c=U Sigma V^T`, PCA principal directions are columns of `V`, and covariance eigenvalues are proportional to `sigma_i^2`. The rank-`k` PCA reconstruction

`X_c V_k V_k^T`

is exactly the truncated-SVD reconstruction

`U_k Sigma_k V_k^T`.

This explains why PCA provides an optimal low-rank representation of centered data in the least-squares/Frobenius sense.

## 17. Computing the SVD: conceptual route

The existence theorem can be understood via eigenvectors of `A^T A`, but a robust numerical SVD algorithm avoids naively forming that product. The course's final lectures emphasize orthogonal transformations, particularly Householder reflectors, because they preserve norms and reduce a matrix to a simpler structured form without changing singular values.

A standard high-level route is:

1. apply orthogonal Householder transformations from the left and right to reduce `A` to **bidiagonal form** `B`;
2. compute the singular values/vectors of the bidiagonal matrix with a specialized iterative procedure;
3. accumulate the orthogonal transformations to recover singular vectors of `A`.

Bidiagonal means only the main diagonal and one adjacent diagonal are nonzero. This is the SVD analogue of Hessenberg/tridiagonal reduction in eigenvalue computation.

## 18. Why orthogonal equivalence preserves singular values

If `Q` and `Z` are orthogonal and

`B=Q^T A Z`,

then

`B^T B = Z^T A^T A Z`.

This is an orthogonal similarity transformation of `A^T A`, so eigenvalues of `B^TB` equal those of `A^TA`. Therefore `A` and `B` have the same singular values.

This justifies reducing a matrix structurally before solving the singular-value problem.

## 19. Symmetric augmented eigenproblem

Another conceptual relation is the block matrix

`C = [[0, A],[A^T, 0]]`.

If `A v_i = sigma_i u_i` and `A^T u_i=sigma_i v_i`, then

`[u_i; v_i]`

and

`[u_i; -v_i]`

are eigenvectors of `C` with eigenvalues `+sigma_i` and `-sigma_i`, respectively. This makes singular values appear as magnitudes of eigenvalues of a symmetric matrix and helps connect SVD algorithms to symmetric eigenvalue techniques.

## 20. Numerical rank and truncation

In exact mathematics, rank counts strictly positive singular values. With measured data and floating point, tiny singular values may represent noise or numerical uncertainty. Truncating them produces a lower-rank model and prevents division by very small values in the pseudoinverse.

A truncated pseudoinverse uses only singular values above a chosen threshold. This regularizes an ill-conditioned inverse problem by discarding directions in which the data provide little reliable information.

The threshold is problem dependent: it should not be presented as a universal magic constant.

## 21. SVD versus eigendecomposition

Do not confuse them:

- eigendecomposition requires a square matrix and may lack a full eigenbasis;
- SVD exists for every rectangular matrix;
- eigenvalues may be complex or signed; singular values are always real and nonnegative;
- left and right singular vectors can be different because input/output spaces may differ;
- for symmetric positive semidefinite matrices, eigen- and singular structures align especially closely.

## 22. Exam checklist

Be able to state the full/thin SVD with dimensions; derive the relation to `A^T A` and `AA^T`; derive rank and four fundamental subspaces; obtain `||A||_2`, Frobenius norm and condition number from singular values; state and explain truncated-SVD optimality; derive the pseudoinverse; explain least-squares/minimum-norm solutions; connect SVD to PCA; and explain why Householder bidiagonalization is preferable to blindly forming `A^TA` in a numerical algorithm.

## 23. Sources

- `Slides/EigenValues/6 - Singular value decomposition.pdf`
- SVD part of `Slides/Trascrizioni/38Lecture1215.txt`
- `Slides/Trascrizioni/39Lecture1217.txt`
- `Slides/Trascrizioni/40Lecture1219_1.txt`
- `Slides/Trascrizioni/41Lecture1219_2.txt`
- `Slides/Trascrizioni/42Lecture0107.txt`
- `Della Santa/How PCA/test_SVD_vs_PCA.ipynb`
