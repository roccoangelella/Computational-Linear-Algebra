# Module 3 - Orthogonality, QR ideas, projectors and least squares

## 1. Inner products and orthogonality

For real vectors, the standard inner product is

`<x,y> = x^T y`.

It measures both length and angle. The Euclidean norm is induced by it:

`||x||_2 = sqrt(<x,x>)`.

Two vectors are **orthogonal** when `<x,y>=0`. A set `{q_1,...,q_k}` is **orthonormal** when the vectors are mutually orthogonal and each has unit norm. If `Q` has orthonormal columns, then

`Q^T Q = I`.

For a square real orthogonal matrix, also `QQ^T=I`, so `Q^{-1}=Q^T`. In the complex case, transpose is replaced by conjugate transpose.

Primary sources: `Slides/Lecture1016-OrtProj.pdf`; transcripts `09Lecture1010_2.txt` through `14Lecture1017_2.txt`, plus the projection/least-squares material around `17Lecture1024_1.txt`; `PyLab02_orthog.ipynb` and solution.

## 2. Why orthogonal transformations are numerically valuable

Orthogonal matrices preserve Euclidean lengths and inner products:

`||Qx||_2 = ||x||_2`.

Therefore applying an orthogonal change of coordinates does not magnify perturbations in the 2-norm. This is one reason QR-type methods are preferred over explicitly forming normal equations for many least-squares problems, and why orthogonal transformations recur in Arnoldi, Lanczos, QR eigenvalue iteration and SVD algorithms.

## 3. Classical Gram-Schmidt

Suppose `a_1,...,a_n` are linearly independent vectors. Classical Gram-Schmidt constructs orthonormal vectors spanning the same nested subspaces.

Start with

`q_1 = a_1 / ||a_1||_2`.

For `j=2,...,n`, remove from `a_j` all components in the directions already constructed:

`v_j = a_j - sum_{i=1}^{j-1} (q_i^T a_j) q_i`,

then normalize:

`q_j = v_j / ||v_j||_2`.

The coefficients `r_ij = q_i^T a_j` together with `r_jj=||v_j||_2` form an upper triangular matrix `R`, producing

`A = QR`.

In exact arithmetic the result is orthonormal. In floating point, cancellation and roundoff can cause loss of orthogonality when columns are nearly dependent.

## 4. Modified Gram-Schmidt

Modified Gram-Schmidt performs the same mathematical projection removals in a different computational order. For each new vector, it updates the working vector immediately after each projection:

`v <- v - (q_i^T v) q_i`.

The exact-arithmetic factorization is equivalent to classical Gram-Schmidt, but the modified organization is usually more robust numerically. The lab explicitly compares these implementations.

A very small `||v||` signals exact or numerical linear dependence and must be handled through a tolerance rather than blindly dividing by it.

## 5. Givens rotations

A Givens rotation acts nontrivially only on two coordinates. For indices `h` and `k`, its active 2x2 block has the form

`[[c, s],[-s, c]]`, with `c^2+s^2=1`,

up to a sign convention. Parameters are chosen so that applying the rotation zeros a selected matrix entry.

Because a Givens transformation changes only two rows (or columns), it is useful when individual entries must be eliminated, especially in structured or sparse computations.

## 6. Householder reflections

A Householder matrix has the form

`H = I - 2 vv^T/(v^T v)`

for a nonzero vector `v`. It is symmetric and orthogonal:

`H^T=H`, `H^T H=I`, and `H^{-1}=H`.

Geometrically it reflects vectors across the hyperplane orthogonal to `v`. In numerical linear algebra, `v` is chosen so that `Hx` maps a vector `x` onto a multiple of a coordinate vector, thereby zeroing an entire group of entries at once.

Householder transformations are the standard dense tool for stable QR factorization and later appear in Hessenberg/tridiagonal/bidiagonal reductions.

## 7. QR factorization

For `A in R^{m x n}` with `m >= n` and full column rank, a thin QR factorization is

`A = QR`,

where `Q in R^{m x n}` has orthonormal columns and `R in R^{n x n}` is upper triangular and nonsingular.

QR can be obtained conceptually by Gram-Schmidt or computationally through Givens/Householder transformations. The factorization turns geometric questions about the column space of `A` into triangular algebra.

## 8. Orthogonal projection onto a subspace

Let the columns of `Q` form an orthonormal basis for a subspace `S`. The orthogonal projection of `b` onto `S` is

`p = QQ^T b`.

The matrix

`P = QQ^T`

is the orthogonal projector. It satisfies

`P^2=P`, `P^T=P`,

and the residual `b-p` is orthogonal to every vector in `S`:

`Q^T(b-p)=0`.

If the basis matrix `A` is not orthonormal but has full column rank, the same projector is

`P = A(A^T A)^{-1}A^T`.

This formula is mathematically useful, but QR is usually a better computational route than explicitly forming `A^T A`.

## 9. General projector concept

A matrix `P` is a projector when `P^2=P`. Its range contains points that are unchanged by a second projection. An **orthogonal projector** is additionally symmetric in the real Euclidean setting. Non-symmetric projectors correspond to oblique projection along a direction not perpendicular to the target subspace.

This distinction matters later because Krylov methods impose different projection/orthogonality conditions on residuals.

## 10. Least squares as projection

For an overdetermined system `Ax approximately b`, least squares asks for

`x_* = argmin_x ||Ax-b||_2`.

The vector `Ax_*` must be the orthogonal projection of `b` onto `Im(A)`. Hence the residual

`r_* = b-Ax_*`

is orthogonal to the column space:

`A^T r_* = 0`.

This gives the normal equations

`A^T A x_* = A^T b`.

If `A` has full column rank, the solution is unique. However, forming `A^T A` squares the 2-norm condition number:

`kappa_2(A^T A)=kappa_2(A)^2`.

This can magnify numerical difficulty.

## 11. Least squares through QR

If `A=QR` with `Q` having orthonormal columns, then

`||Ax-b||_2 = ||QRx-b||_2`.

The optimality condition gives

`Rx = Q^T b`.

Thus least squares reduces to an upper-triangular solve after QR. This avoids explicitly forming the normal matrix and is usually more stable.

The geometric meaning and computational factorization are the same story: `Q` identifies the column space, `Q^T b` gives the coordinates of the projection, and `R` converts those coordinates back to coefficients in the original columns of `A`.

## 12. Stability comparison of orthogonalization methods

The lab compares methods not only by whether they work in exact algebra but by how well they preserve orthogonality numerically. Useful diagnostics include

`||Q^T Q - I||`

and the reconstruction error

`||A-QR||`.

A method can reconstruct `A` reasonably well while its computed columns are less orthogonal than expected. Both diagnostics matter.

## 13. Connections forward

This module supplies machinery for nearly everything later:

- Arnoldi repeatedly orthogonalizes `Aq_k` against previous basis vectors;
- Lanczos exploits symmetry to reduce that recurrence;
- QR eigenvalue iteration repeatedly factors matrices as `QR`;
- Householder transformations reduce matrices to Hessenberg/tridiagonal/bidiagonal form;
- SVD uses orthogonal/unitary factors;
- PCA uses orthonormal principal directions;
- least-squares geometry reappears in GMRES and the pseudoinverse.

## 14. Exam checklist

Be able to define orthogonality/orthonormality; derive classical Gram-Schmidt; explain modified Gram-Schmidt and why it is computationally preferable; define a Givens rotation and a Householder reflector; explain `A=QR`; derive `P=QQ^T`; derive normal equations from residual orthogonality; and explain why QR is preferable to explicitly solving normal equations when numerical stability matters.

## 15. Sources

- `Slides/Lecture1016-OrtProj.pdf`
- `Slides/Trascrizioni/09Lecture1010_2.txt` through `14Lecture1017_2.txt`
- `Slides/Trascrizioni/17Lecture1024_1.txt`
- `Della Santa/PyLab02_orthog.ipynb`
- `Della Santa/solPyLab02_orthog.ipynb`
