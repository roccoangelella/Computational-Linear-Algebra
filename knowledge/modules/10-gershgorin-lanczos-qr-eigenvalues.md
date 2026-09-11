# Module 10 - Gershgorin localization, Lanczos and QR eigenvalue iteration

## 1. Why more eigenvalue algorithms are needed

Power and inverse iterations are effective when one eigenpair is wanted and a favorable spectral separation/shift is available. Other situations require:

- locating eigenvalues before computing them;
- computing several extreme eigenpairs of a large symmetric sparse matrix;
- computing all eigenvalues of a moderate dense matrix.

This module covers three complementary tools: Gershgorin disks, Lanczos and QR iteration.

Primary sources: `Slides/EigenValues/3 - Gerschgorin circles.pdf`, `4 - Lanczos.pdf`, `5 - QR method for eigenvalues.pdf`; transcripts `35Lecture1205.txt` through the QR/SVD transition in `38Lecture1215.txt`.

## 2. Gershgorin disks

For `A=(a_ij) in C^{n x n}`, define for row `i`

`R_i = sum_{j != i} |a_ij|`.

The i-th Gershgorin disk is

`G_i = { z in C : |z-a_ii| <= R_i }`.

**Gershgorin theorem:** every eigenvalue of `A` lies in the union

`G_1 union ... union G_n`.

The diagonal entry gives the disk center; the magnitude of off-diagonal entries in that row gives its radius.

A column version also exists, because applying the theorem to `A^T`/`A^*` yields the same eigenvalues with radii based on columns.

## 3. Why Gershgorin is true

Let `Ax=lambda x` and choose an index `i` for which `|x_i|` is maximal. Then

`(lambda-a_ii)x_i = sum_{j != i} a_ij x_j`.

Taking absolute values,

`|lambda-a_ii| |x_i| <= sum_{j != i}|a_ij||x_j|`.

Since `|x_j| <= |x_i|`, division by the nonzero maximal component gives

`|lambda-a_ii| <= sum_{j != i}|a_ij| = R_i`.

Hence the eigenvalue lies in at least one disk.

## 4. What Gershgorin can and cannot tell us

The theorem is a **localization** result, not normally a high-accuracy eigensolver. It can:

- bound where the spectrum may lie;
- show that zero cannot be an eigenvalue if all disks exclude zero;
- help identify separated groups of eigenvalues;
- support qualitative arguments about diagonal dominance and spectral location.

A refinement states that if a connected component of the union of disks consists of exactly `k` disks and is disjoint from the others, then it contains exactly `k` eigenvalues counted with algebraic multiplicity.

## 5. Rayleigh quotient for symmetric matrices

For real symmetric `A`, the Rayleigh quotient

`R_A(x)=x^T A x/(x^T x)`

has extremal characterization

`lambda_min = min_{x != 0} R_A(x)`,

`lambda_max = max_{x != 0} R_A(x)`.

More generally, min-max principles characterize ordered eigenvalues through subspaces. This variational view is central to understanding why projected eigenproblems approximate extreme eigenvalues.

The gradient of the Rayleigh quotient is aligned with

`Ax - R_A(x)x`

(up to a scalar factor depending on normalization). This is precisely the eigen-residual direction: it vanishes at an eigenvector.

## 6. Ritz projection idea

Let `S_m` be an `m`-dimensional subspace with orthonormal basis `Q_m`. The projected matrix is

`T_m = Q_m^T A Q_m`.

If `(theta,y)` is an eigenpair of `T_m`, then

`u = Q_m y`

is a **Ritz vector** and `theta` a **Ritz value** approximating an eigenpair of `A`.

This is the eigenvalue analogue of projecting a large linear system onto a smaller subspace.

## 7. Lanczos as symmetric Arnoldi

For a general matrix, Arnoldi produces an upper-Hessenberg projection. When `A=A^T`, symmetry forces the projected matrix to be both symmetric and upper Hessenberg, hence tridiagonal.

Lanczos exploits this to replace full orthogonalization by a three-term recurrence in exact arithmetic.

Given normalized `q_1` and `q_0=0`, `beta_1=0`, for `j=1,2,...`:

1. `v = A q_j - beta_j q_{j-1}`;
2. `alpha_j = q_j^T v`;
3. `v <- v - alpha_j q_j`;
4. `beta_{j+1}=||v||_2`;
5. `q_{j+1}=v/beta_{j+1}` if `beta_{j+1} != 0`.

Equivalently,

`Aq_j = beta_j q_{j-1} + alpha_j q_j + beta_{j+1} q_{j+1}`.

## 8. Lanczos matrix relation

With `Q_m=[q_1,...,q_m]`,

`Q_m^T A Q_m = T_m`,

where

`T_m = tridiag(beta_2,...,beta_m; alpha_1,...,alpha_m; beta_2,...,beta_m)`.

The extended relation is

`A Q_m = Q_m T_m + beta_{m+1} q_{m+1} e_m^T`.

This mirrors Arnoldi but with only three nonzero bands in the small projected matrix.

## 9. Why Lanczos is useful

If `m << n`, compute eigenvalues/eigenvectors of the small tridiagonal `T_m`. Its extreme Ritz values often converge quickly to extreme eigenvalues of `A`, making Lanczos suitable for large sparse symmetric problems such as graph Laplacians.

Each iteration needs one sparse matrix-vector product and a small number of vector operations. Only a few vectors are needed for the mathematical three-term recurrence, although practical implementations may store more for Ritz vectors or reorthogonalization.

## 10. Loss of orthogonality in finite precision

In exact arithmetic, Lanczos vectors are orthogonal automatically because of symmetry. In floating point, roundoff can destroy that orthogonality. Converged Ritz directions can reappear, leading to duplicated/spurious numerical copies of eigenvalues unless reorthogonalization or other safeguards are used.

Thus the elegant three-term exact recurrence does not remove the need for numerical analysis.

## 11. Dense all-eigenvalues problem and QR iteration

For a dense matrix when many or all eigenvalues are needed, QR iteration is a fundamental method. Starting with

`A_0=A`,

repeat:

1. factor `A_k = Q_k R_k` with `Q_k` orthogonal and `R_k` upper triangular;
2. set
   `A_{k+1}=R_k Q_k`.

Since

`A_{k+1}=R_k Q_k = Q_k^T A_k Q_k`,

successive matrices are orthogonally similar and therefore have exactly the same eigenvalues.

Under appropriate conditions, the sequence tends toward an upper triangular (real Schur/quasi-triangular in the real nonsymmetric case) form from which eigenvalues are read from the diagonal or small diagonal blocks.

## 12. Why the naive QR algorithm is too expensive

Factoring a full dense `n x n` matrix from scratch at every iteration costs `O(n^3)` per step. A practical QR eigensolver first reduces the matrix by orthogonal similarity transformations to **upper Hessenberg form**:

`h_ij=0` for `i>j+1`.

For symmetric matrices, Hessenberg form is tridiagonal.

Householder transformations perform this reduction stably. Once Hessenberg structure is present, a QR step can preserve it and be carried out much more cheaply.

This explains why Householder matrices introduced in the orthogonality module return in eigenvalue computation.

## 13. Shifted QR iteration

Convergence can be accelerated with shifts. Choose `mu_k` and factor

`A_k - mu_k I = Q_k R_k`,

then set

`A_{k+1}=R_k Q_k + mu_k I`.

Again,

`A_{k+1}=Q_k^T A_k Q_k`,

so eigenvalues are preserved. A shift near an eigenvalue can accelerate deflation/convergence of a trailing block.

The general pattern is the same as shifted inverse iteration: a judicious spectral shift concentrates the computation on the desired part of the spectrum.

## 14. Deflation in QR

As QR iteration progresses, subdiagonal entries can become very small. If `a_{i+1,i}` is negligible relative to neighboring scales, it can be set to zero numerically, splitting the matrix into independent blocks. This is a form of deflation: a converged eigenvalue/block is separated and the active problem shrinks.

The tolerance is numerical rather than exact; scaling matters.

## 15. Symmetric case

For real symmetric `A`:

- all eigenvalues are real;
- the matrix can first be reduced to real symmetric tridiagonal form;
- orthogonal similarity preserves symmetry;
- QR iteration converges toward a diagonal matrix under the appropriate shifted strategy, with eigenvectors accumulated from the orthogonal factors if required.

This is a particularly clean and important case.

## 16. Relationship between Lanczos and QR

Lanczos is attractive when `n` is huge and only a few eigenpairs are needed: project to a small tridiagonal matrix.

QR iteration is attractive when a dense/moderate problem requires many or all eigenvalues: reduce the full matrix to structured form and iteratively triangularize it.

Both exploit orthogonal similarity/projection and both ultimately move the problem toward a small/triangular structured representation.

## 17. Exam checklist

Be able to state/prove Gershgorin; interpret separated disks; state Rayleigh quotient extremal properties for symmetric matrices; derive Lanczos from symmetric Arnoldi and write the three-term recurrence; define Ritz values/vectors; explain finite-precision loss of orthogonality; derive the similarity behind the QR iteration; explain Hessenberg reduction, shifts and deflation.

## 18. Sources

- `Slides/EigenValues/3 - Gerschgorin circles.pdf`
- `Slides/EigenValues/4 - Lanczos.pdf`
- `Slides/EigenValues/5 - QR method for eigenvalues.pdf`
- `Slides/Trascrizioni/35Lecture1205.txt`
- `Slides/Trascrizioni/36Lecture1210.txt`
- `Slides/Trascrizioni/37Lecture1212.txt`
- QR part of `Slides/Trascrizioni/38Lecture1215.txt`
