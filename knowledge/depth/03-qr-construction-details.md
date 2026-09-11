# Depth supplement 3 - Constructing QR with Householder reflectors and Givens rotations

This supplement adds the explicit constructions used in `Slides/Lecture1016-OrtProj.pdf` to `knowledge/modules/03-orthogonality-qr-projectors-least-squares.md`.

## 1. Householder reflector that zeros a vector tail

Given a nonzero vector `x in R^m`, the goal is to construct an orthogonal reflector `H` such that `Hx` is a multiple of the first coordinate vector. A numerically sensible construction is

`v = x + sign(x_1) ||x||_2 e_1`,

followed by

`H = I - 2 vv^T/(v^T v)`.

Then

`Hx = -sign(x_1)||x||_2 e_1`.

The sign choice avoids subtracting nearly equal numbers when constructing `v`; this is a concrete example of a mathematically equivalent formula being chosen for better floating-point behavior.

`H` is symmetric and orthogonal, so `H^T=H=H^{-1}`. Applying it preserves Euclidean norms while annihilating all components of `x` below the first.

## 2. Householder QR

For `A in R^{m x n}`, `m >= n`, start from `R=A` and `Q=I_m`. At step `j`:

1. take the active column tail `x = R[j:m, j]`;
2. build a Householder reflector `H_j` acting only on rows `j:m` so that the tail below the diagonal is zeroed;
3. update the active matrix by `R <- H_j R`;
4. accumulate the orthogonal factor consistently, e.g. `Q <- Q H_j` because `H_j^T=H_j`.

After the required steps,

`R = H_k ... H_2 H_1 A`

is upper triangular/trapezoidal and

`A = Q R`,

where `Q` is the product of the reflectors in the corresponding reverse/transpose relation.

One usually stores reflector vectors rather than forming every dense `H_j` explicitly.

## 3. Givens rotation

A Givens rotation acts only in a coordinate plane. To eliminate a component `b` below a pivot-like component `a`, choose

`r = sqrt(a^2+b^2)`,

`c = a/r`, `s = b/r`,

with sign variations possible depending on the rotation convention. The active block can be written

`[[c, s],[-s, c]]`,

so that the chosen two-vector is rotated to one with second component zero.

The full `m x m` Givens matrix is the identity except for this `2 x 2` block in the selected rows.

## 4. Givens QR

Set `R=A`, `Q=I`. Sweep column by column. For each entry below the diagonal, usually from bottom to top:

1. construct a Givens rotation `G` that eliminates the selected `R[i,j]`;
2. update `R <- G R`;
3. accumulate `Q <- Q G^T`.

After all subdiagonal entries are eliminated,

`A = Q R`.

Because each Givens rotation changes only two rows, it can preserve sparsity/structure better than a reflector when only a small number of entries must be eliminated.

## 5. Householder versus Givens

For a dense matrix, one Householder transformation can annihilate an entire column tail at once, so it is generally the standard efficient dense QR mechanism. Givens rotations annihilate entries one at a time but touch only two rows; they are especially valuable for sparse, incremental or structured problems and for updating small Hessenberg least-squares problems inside GMRES.

Both are orthogonal transformations, so neither magnifies the Euclidean norm merely through the coordinate transformation itself.

## 6. Stability and diagnostics

A computed QR factorization should be checked using two distinct properties:

`||A-QR||`

for reconstruction, and

`||Q^T Q-I||`

for orthogonality. A small reconstruction error alone does not prove that the computed `Q` is sufficiently orthogonal.

For nearly dependent columns, Gram-Schmidt variants can lose orthogonality; Householder QR is normally much more robust for dense problems. Modified Gram-Schmidt can be adequate and convenient, especially when the orthonormal basis is generated sequentially as in Arnoldi.

## 7. Why QR matters later

- Least squares reduces to `Rx=Q^T b`.
- Arnoldi is repeated orthogonalization of new Krylov vectors.
- GMRES solves its reduced least-squares problem by QR updates of the Hessenberg matrix.
- The QR eigenvalue algorithm repeatedly forms `A_k=Q_kR_k` and reverses the factors.
- Householder transformations also reduce matrices to Hessenberg, tridiagonal and bidiagonal forms.

Thus QR is a reusable numerical pattern rather than an isolated factorization.

## 8. Deep-understanding checkpoint

Be able to derive a Householder reflector for a given vector, explain the sign choice, write the QR accumulation logic, compute Givens `c,s` for a two-entry vector, explain why Givens can be preferable for sparse/selective elimination, and connect QR construction to least squares and later eigensolver/Krylov algorithms.

## Sources

Primary: `Slides/Lecture1016-OrtProj.pdf`, transcripts `09Lecture1010_2.txt` through `14Lecture1017_2.txt`, and `Della Santa/PyLab02_orthog.ipynb` plus solution.
