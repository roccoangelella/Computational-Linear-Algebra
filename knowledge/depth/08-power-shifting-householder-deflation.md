# Depth supplement 8 - Power convergence, course shifting and Householder deflation

This supplement restores details from `Slides/EigenValues/1 - Power Methods.pdf`, `Slides/EigenValues/2 - Shifting, deflation.pdf`, `Slides/EigenValues/lab-deflation.pdf` and transcripts `26Lecture1114.txt` through `28Lecture1119.txt` that require more precision than the base Module 8 currently provides.

A terminology warning is essential. In the supplied course material, **shifting** includes the symmetric rank-one modification that moves a known eigenvalue to zero, while **deflation** is presented as a Householder orthogonal-similarity reduction that removes one already-known eigenpair from the active problem. Some numerical-linear-algebra texts use the word *deflation* for the rank-one update as well. For this course, use the lecturer's convention when explaining the algorithms.

## 1. Power iteration: vector and eigenvalue convergence are different

Assume `A` is diagonalizable and has a unique dominant eigenvalue in magnitude,

`|lambda_1| > |lambda_2| >= ... >= |lambda_n|`,

and that the starting vector has a nonzero component along the dominant eigenvector. The normalized power iterates approach the dominant eigendirection with an asymptotic factor governed by

`|lambda_2/lambda_1|`.

For a real symmetric matrix the eigenvectors can be chosen orthonormal. If a normalized iterate has the form

`x_k = c_1 v_1 + sum_{j>=2} c_j v_j`,

then the unwanted coefficients relative to the dominant one behave like powers of `lambda_j/lambda_1`. Therefore the **directional/eigenvector error** remains first order in the dominant ratio:

`sin angle(x_k,v_1) = O(|lambda_2/lambda_1|^k)`

under the standard simple-dominant-eigenvalue assumptions.

The course's statement that convergence “doubles” for symmetric matrices refers to the **eigenvalue estimate obtained from the Rayleigh quotient**. Because orthogonality cancels the first-order cross terms,

`rho_A(x_k) - lambda_1 = O(|lambda_2/lambda_1|^(2k))`.

Thus the exponent governing the Rayleigh-quotient eigenvalue error is doubled, even though the eigendirection itself still converges with the first power of the ratio. This distinction prevents an imprecise statement such as “the whole power method is twice as fast” from being used without saying which error is being measured.

## 2. Cost and stopping logic emphasized in the power-method lecture

A practical power step is dominated by the matrix-vector product `A x_k`.

- Dense `n x n` storage gives approximately `O(n^2)` work per matvec.
- If each sparse row contains at most `N_r` stored entries, a row-oriented implementation costs about `O(n N_r)`, equivalently `O(nnz(A))` in the usual sparse count.

The lecture's inexpensive stopping test monitors successive scalar eigenvalue estimates rather than recomputing a full eigen-residual every iteration. A residual test `||Ax-lambda x||` is mathematically stronger, but it may require an additional matvec unless the implementation reuses already-computed products. The general numerical rule is to state what the stopping test certifies and what its cost is.

## 3. Inverse and shifted inverse power methods

If `A` is nonsingular, `A^{-1}` has the same eigenvectors and eigenvalues `1/lambda_i`. Hence inverse iteration targets the eigenvalue of `A` with smallest magnitude. Numerically one never forms `A^{-1}` explicitly; each step solves

`A y_k = x_k`.

For a prescribed scalar `mu`, shifted inverse iteration instead solves

`(A-mu I)y_k=x_k`.

The transformed eigenvalues are `1/(lambda_i-mu)`, so the eigenvalue of `A` closest to `mu` becomes dominant in magnitude, provided the relevant separation assumptions hold. If `mu` equals an eigenvalue exactly, the shifted matrix is singular; in practice a nearby shift is used when an eigenvector is to be isolated through inverse iteration.

This scalar shift `A-mu I` is a different operation from the course's rank-one **shifting** procedure below. Both alter the spectrum to make a desired eigenpair easier to isolate, but they do so in different ways.

## 4. Course “shifting” for a known symmetric eigenpair

Let `A=A^T` and suppose `(lambda_1,x_1)` is a known eigenpair with `||x_1||_2=1`. By the spectral theorem, choose an orthonormal eigenbasis and write

`A = sum_i lambda_i x_i x_i^T`.

Define

`A_1 = A - lambda_1 x_1 x_1^T`.

Then

`A_1 x_1 = 0`,

while for every other orthonormal eigenvector `x_j`, `j != 1`,

`A_1 x_j = lambda_j x_j`,

because `x_1^T x_j=0`.

Therefore the known eigenvalue `lambda_1` is moved to zero and all the other symmetric eigenpairs are preserved. If

`|lambda_1|>|lambda_2|>|lambda_3|...`,

a power method applied to `A_1` can expose the next eigenpair. Repeating the rank-one modification is the course's “shifting” strategy for successively moving computed eigenvalues into the kernel.

The same spectral-expansion idea can also move known zero-eigendirections away from zero by adding appropriately weighted rank-one terms along known kernel eigenvectors. The lecture presents this as a possible stabilization idea: the important mechanism is direct control of selected eigenvalues while preserving the eigenvectors in the symmetric setting.

## 5. Why repeated rank-one shifting can degrade numerically

In exact arithmetic the update above preserves the remaining symmetric eigenpairs. In floating point, however, every computed `lambda_i` and `x_i` contains error. Repeatedly modifying the full matrix with inexact rank-one terms accumulates perturbations. The Hilbert-matrix laboratory is designed to make this visible: later recovered eigenpairs can have much larger residuals than the first ones.

For each computed pair, evaluate

`||A x_i-lambda_i x_i||_2`

using the **original** matrix `A`. This checks whether the pair is genuinely an eigenpair of the problem we meant to solve, rather than merely of the repeatedly perturbed working matrix.

This experiment motivates the orthogonal-similarity deflation method below.

## 6. Householder deflation: the general one-step idea

Suppose `A in R^{n x n}` and a normalized eigenpair `(lambda_1,x_1)` is known. Choose an orthogonal Householder matrix `P_1` such that

`P_1 x_1 = -e_1`,

where `e_1` is the first canonical basis vector. One suitable reflector, barring the usual sign/special-case conventions, is built from

`w = x_1 + e_1`,

`P_1 = I - 2 w w^T/(w^T w)`.

Because a Householder reflector is orthogonal and symmetric,

`P_1^{-1}=P_1^T=P_1`.

Form the orthogonally similar matrix

`B_1 = P_1 A P_1^T`.

Similarity preserves eigenvalues. Moreover,

`B_1 e_1 = lambda_1 e_1`,

so the first column of `B_1` has the block form

`[lambda_1; 0]`.

Thus

`B_1 = [[lambda_1, b_1^T], [0, A_2]]`.

The remaining eigenvalues of `A` are the eigenvalues of the trailing `(n-1)x(n-1)` block `A_2`. One eigenpair has therefore been separated and the active eigenvalue problem is one dimension smaller.

## 7. Symmetric case: block diagonalization after one deflation

If `A` is symmetric, then `B_1=P_1AP_1^T` is also symmetric. Since the lower-left block is zero, symmetry forces the upper-right block to be zero as well:

`B_1 = [[lambda_1, 0], [0, A_2]]`.

This is the especially clean case emphasized in the course. The remaining matrix `A_2` is itself symmetric, so the same construction can be applied recursively.

The contrast with rank-one shifting is important:

- shifting keeps the matrix size fixed and changes a selected eigenvalue;
- Householder deflation uses an orthogonal similarity, preserves the entire spectrum, and then isolates a smaller trailing problem.

## 8. Recovering eigenvectors of the original matrix

Deflation changes coordinates, so an eigenvector computed in a reduced block must be mapped back.

After one symmetric deflation, suppose

`A_2 z_2 = lambda_2 z_2`.

Embed the reduced vector into the full transformed coordinates:

`y_2 = [0; z_2]`.

Since `B_1 y_2=lambda_2 y_2` and `B_1=P_1AP_1^T`, an eigenvector of the original matrix is

`x_2 = P_1^T y_2`.

At later stages, the back-transformation contains the accumulated orthogonal transformations from all previous deflations. Conceptually, if the recursive process has produced embedded reduced eigenvector `y_j`, then the original eigenvector is obtained by applying the appropriate product of transposed Householder factors in reverse coordinate order.

This reconstruction step is essential: the eigenvectors of a trailing block live in reduced coordinates and are not automatically eigenvectors of the original matrix.

## 9. Recursive symmetric deflation algorithm

For a symmetric matrix, the course procedure can be organized as follows.

1. Set the active matrix `A_1=A` and the accumulated orthogonal transformation initially to the identity.
2. Compute an eigenpair `(lambda_i,z_i)` of the current active matrix `A_i`, for example an extreme pair with a power-type method.
3. Construct a Householder reflector `P_i` that maps the normalized active eigenvector `z_i` to `-e_1` in the current dimension.
4. Form `P_i A_i P_i^T`.
5. Record the isolated eigenvalue and extract the bottom-right block as `A_{i+1}`.
6. Accumulate the coordinate transformations needed to reconstruct the corresponding full-space eigenvector.
7. Repeat on the smaller symmetric block.

Each step reduces the active dimension by one. In exact arithmetic, all eigenvalues can therefore be exposed after finitely many deflation steps.

## 10. Why orthogonal deflation is numerically attractive

The transformations are orthogonal, so they preserve the Euclidean norm and have 2-norm condition number one. The algorithm changes basis instead of repeatedly subtracting inexact spectral rank-one contributions from the full matrix. This generally gives a cleaner numerical route to separating already-computed eigenpairs.

That does not make the method immune to roundoff: computed eigenvectors, Householder reflectors, and reduced problems are still finite-precision objects. The scientific comparison is therefore empirical as well as theoretical: on the laboratory matrices, compare residuals of the recovered eigenpairs against those obtained by repeated rank-one shifting.

## 11. Course terminology versus broader literature

You may encounter the following naming difference in books/software:

- `A-lambda x x^T` is often called **Hotelling deflation** or rank-one deflation;
- the course calls this spectral modification **shifting**;
- the course reserves **deflation** for the Householder/similarity dimension-reduction construction.

For an exam answer, state the formula first and then use the course terminology. That eliminates ambiguity even when another source uses a different label.

## 12. Deep-understanding checkpoint

You should be able to distinguish eigendirection convergence from Rayleigh-quotient convergence in the symmetric power method; derive inverse and shifted inverse iteration without forming a matrix inverse; prove that `A-lambda_1x_1x_1^T` moves only the selected symmetric eigenvalue to zero; explain why repeated inexact shifting can accumulate error; construct the Householder map sending a known eigenvector to `e_1` up to sign; derive the block form of `PAP^T`; prove why symmetry makes the off-diagonal block vanish; recurse on the trailing block; and map reduced eigenvectors back to the original coordinates.

## Sources

Primary: `Slides/EigenValues/1 - Power Methods.pdf`, `Slides/EigenValues/2 - Shifting, deflation.pdf`, `Slides/EigenValues/lab-deflation.pdf`, and transcripts `26Lecture1114.txt`, `27Lecture1117.txt`, `28Lecture1119.txt` plus the opening review in `35Lecture1205.txt`.
