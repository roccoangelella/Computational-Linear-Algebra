# Depth supplement 10 - Eigenvalue convergence details: Gershgorin, Lanczos and QR

This supplement expands `knowledge/modules/10-gershgorin-lanczos-qr-eigenvalues.md` with structural and convergence details from the official eigenvalue lectures.

## 1. Gershgorin and nonsingularity

For row disks

`G_i={z: |z-a_ii| <= sum_{j != i}|a_ij|}`,

every eigenvalue lies in their union. Therefore if every disk excludes zero, zero cannot be an eigenvalue and the matrix is nonsingular.

Strict row diagonal dominance gives exactly this situation:

`|a_ii| > sum_{j != i}|a_ij|`

implies that the disk centered at `a_ii` cannot contain zero. Thus Gershgorin gives a spectral proof of nonsingularity for strictly diagonally dominant matrices.

A related irreducible diagonal-dominance result relaxes strictness in some rows provided the matrix/graph is irreducibly coupled and at least one row is strict. The key lesson is that graph connectivity plus dominance can rule out a zero eigenvalue even when not every row is strictly dominant.

## 2. Reducibility, irreducibility and the graph test

A square matrix is **reducible** if a simultaneous permutation of rows and columns can put it into block upper-triangular form. Otherwise it is **irreducible**.

For the directed adjacency graph induced by the nonzero pattern, irreducibility is equivalent to strong connectivity: every vertex can reach every other vertex by a directed path.

The course uses the strengthened Gershgorin boundary theorem for an irreducible matrix: if an eigenvalue lies on the boundary of one Gershgorin disk, then it must lie on the boundary of all disks in the relevant union. This can exclude zero even when ordinary disks touch zero and the basic theorem alone would be inconclusive.

For a symmetric matrix the graph is effectively undirected, so ordinary connectedness is the corresponding structural picture.

## 3. Gershgorin estimates for the 2-norm condition number of a symmetric matrix

For a real symmetric nonsingular matrix, singular values are the absolute values of the eigenvalues. Therefore

`kappa_2(A) = max_i |lambda_i| / min_i |lambda_i|`.

Gershgorin localization can sometimes bound both numerator and denominator without computing the eigenvalues. Suppose the union of the disks implies

`|lambda| <= beta`

for every eigenvalue and, crucially, also excludes a neighborhood of zero so that

`|lambda| >= gamma > 0`.

Then

`kappa_2(A) <= beta/gamma`.

For a symmetric positive-definite matrix, if Gershgorin places every eigenvalue in a positive real interval `[ell,u]` with `ell>0`, then the particularly simple estimate is

`kappa_2(A) <= u/ell`.

This is the application explicitly discussed in the Gershgorin lecture. It also shows the limitation of the technique: if one or more disks touch or cross zero, Gershgorin may still prove nonsingularity by an irreducibility argument, yet fail to provide a useful positive lower bound on `min |lambda_i|`. In that situation a condition-number estimate requires additional information.

The diagonal entries, being disk centers, can also provide rough spectral location information and can be useful first guesses for shifts in inverse iteration, but they are localization cues rather than guaranteed accurate eigenvalue approximations.

## 4. Variational view and Ritz values

For symmetric `A`, ordered eigenvalues admit min-max characterizations. The largest eigenvalue is

`lambda_max = max_{||x||=1} x^T A x`,

and the smallest is the corresponding minimum. More generally, ordered eigenvalues can be characterized by optimizing the Rayleigh quotient over subspaces.

If `Q_m` spans a subspace `S_m`, the Ritz values are eigenvalues of

`T_m=Q_m^T A Q_m`.

The extreme Ritz values are exactly the extreme Rayleigh quotients restricted to `S_m`:

`theta_max^(m) = max_{x in S_m, ||x||=1} x^T A x`,

`theta_min^(m) = min_{x in S_m, ||x||=1} x^T A x`.

## 5. Monotonic extreme Ritz bounds for nested subspaces

If

`S_m subseteq S_{m+1}`,

then enlarging the set over which the Rayleigh quotient is optimized gives

`theta_max^(m) <= theta_max^(m+1) <= lambda_max(A)`,

and

`lambda_min(A) <= theta_min^(m+1) <= theta_min^(m)`.

Thus the largest Ritz value is a nondecreasing lower bound on the largest eigenvalue, while the smallest Ritz value is a nonincreasing upper bound on the smallest eigenvalue. If the subspaces ultimately span all of `R^n`, the extreme Ritz values become the exact extreme eigenvalues.

This is the explicit form of the convergence intuition stated in the Lanczos lecture: a smart sequence of much smaller subspaces can approach the spectral extremes long before the full dimension is reached.

More refined interlacing/min-max statements apply to all ordered Ritz values. For exam purposes, the essential mechanism is that nested subspaces plus the Rayleigh variational principle produce rigorous spectral bounds, not merely heuristic approximations.

Individual Ritz vectors can change substantially when eigenvalues are clustered/repeated; the invariant subspace can be much more stable than a particular basis vector.

## 6. Lanczos residual for a Ritz pair

Lanczos gives

`A Q_m = Q_m T_m + beta_{m+1} q_{m+1} e_m^T`.

If `T_m y = theta y` and `u=Q_m y`, then

`A u - theta u = beta_{m+1} q_{m+1} (e_m^T y)`.

Therefore the Ritz residual norm is

`||A u-theta u||_2 = |beta_{m+1} e_m^T y|`

when `q_{m+1}` is normalized. This is powerful computationally: one can estimate eigenpair accuracy from small projected quantities without forming an expensive full residual from scratch.

## 7. Lanczos breakdown and invariant subspaces

If `beta_{m+1}=0` in exact arithmetic, then `A Q_m` lies entirely in `span(Q_m)`. The Krylov subspace is invariant under `A`, and the eigenvalues of `T_m` are exact eigenvalues associated with that invariant subspace. This is the symmetric analogue of happy breakdown in Arnoldi.

Finite precision can produce near-breakdown and loss of orthogonality instead; numerical implementations require thresholds/reorthogonalization strategies.

## 8. Unshifted QR iteration and similarity

The QR algorithm forms

`A_k=Q_k R_k`,

`A_{k+1}=R_k Q_k=Q_k^T A_k Q_k`.

Hence all iterates are orthogonally similar and have the same eigenvalues.

A classical convergence theorem used in the course assumes a favorable spectral ordering, including distinct eigenvalue moduli, together with an LU factorization condition on the eigenvector matrix. Under these hypotheses, the unshifted QR iteration drives the matrix toward upper-triangular form. In the real symmetric positive-definite case the limit is diagonal under the corresponding favorable assumptions.

The precise hypotheses matter: QR is not justified by saying merely that repeated factorization “usually diagonalizes” a matrix.

## 9. Connection with simultaneous/subspace iteration

Repeated QR iteration can be interpreted as a stabilized simultaneous power iteration. Instead of propagating one vector by powers of `A`, it propagates a whole basis and orthonormalizes it at each step. The basis tends to align with invariant subspaces associated with dominant eigenvalue magnitudes.

This interpretation explains why eigenvalue-modulus ratios govern the asymptotic convergence of the unshifted method, analogous to the ratio `|lambda_2/lambda_1|` in ordinary power iteration.

## 10. Why Hessenberg reduction comes first

Applying a full dense QR factorization at every iteration would cost `O(n^3)` per step. Before iterating, a general dense matrix is therefore reduced by orthogonal similarity transformations to upper Hessenberg form `H`, where

`h_ij=0` for `i>j+1`.

The reduction is done once. QR steps then preserve Hessenberg structure and can be executed much more cheaply than dense QR from scratch.

For symmetric matrices, the analogous reduction is to symmetric tridiagonal form, which is even more structured.

This two-phase strategy is central:

1. expensive but stable structure reduction;
2. many cheap structured QR steps.

## 11. Shifted QR

Choose a scalar `mu_k` and factor

`A_k-mu_k I=Q_kR_k`.

Then

`A_{k+1}=R_kQ_k+mu_k I=Q_k^T A_k Q_k`.

Thus the shift accelerates convergence without changing the eigenvalues. A good shift is selected from the trailing part of the active matrix so that one eigenvalue converges rapidly toward the bottom-right position/block.

Shifting is the QR analogue of shifted inverse iteration: manipulate spectral separation while preserving the target spectrum.

## 12. Deflation criterion in QR

As an eigenvalue converges, a subdiagonal entry becomes small. When

`|a_{i+1,i}|`

is negligible relative to neighboring diagonal scales, it can be set to zero numerically. This splits the Hessenberg matrix into independent blocks, and the converged block can be removed from the active iteration.

The decision must be relative/scaled; an absolute threshold independent of the matrix scale is unreliable.

This QR deflation is a third use of the general word “deflation” in numerical linear algebra. It should not be confused with the Householder eigenpair-deflation construction of Module 8; in both cases the unifying idea is to separate already-resolved spectral information from the still-active problem.

## 13. Real nonsymmetric matrices

A real matrix can have complex conjugate eigenpairs, so a real QR algorithm does not necessarily converge to a real diagonal matrix. The natural real limit is quasi-upper-triangular (real Schur form), with `1 x 1` blocks for real eigenvalues and `2 x 2` blocks representing complex conjugate pairs.

This is why “read eigenvalues from the diagonal” must be qualified for the nonsymmetric real case.

## 14. Deep-understanding checkpoint

Be able to derive nonsingularity from Gershgorin exclusion of zero; explain reducibility/irreducibility through the adjacency graph; use Gershgorin bounds to estimate `kappa_2(A)` for a symmetric matrix when the disks bound the spectrum away from zero and explain why the estimate can fail when they do not; connect Rayleigh/min-max principles to monotonic extreme Ritz bounds on nested subspaces; derive the cheap Lanczos Ritz-residual formula; explain QR as orthogonal similarity and as stabilized simultaneous iteration; state that convergence theorems require spectral/eigenvector assumptions; explain Hessenberg reduction, shift acceleration and scaled QR deflation; and distinguish a diagonal limit from real Schur/quasi-triangular form.

## Sources

Primary: `Slides/EigenValues/3 - Gerschgorin circles.pdf`, `4 - Lanczos.pdf`, `5 - QR method for eigenvalues.pdf`, and transcripts `35Lecture1205.txt` through the QR part of `38Lecture1215.txt`.
