# Depth supplement 2 - Foundations: solvability, PA=LU, linear maps and change of basis

This supplement expands `knowledge/modules/02-linear-algebra-and-direct-methods.md` using the material in `Slides/Lecture1003-BasicTools.pdf`.

## 1. Rank, minors and solvability

For a matrix `A`, the rank is the maximum number of linearly independent columns (equivalently rows). A complementary characterization used in the course is that `rank(A)=r` when there exists at least one nonzero `r x r` minor while all larger minors vanish.

For a system `Ax=b`, the Rouché-Capelli theorem states that the system is consistent exactly when

`rank(A) = rank([A | b])`.

When the system is consistent, the number of free parameters is

`n - rank(A)`

for `n` unknowns. Thus:

- if `rank(A)=rank([A|b])=n`, the solution is unique;
- if the common rank is `< n`, infinitely many solutions exist;
- if `rank(A) != rank([A|b])`, no solution exists.

This theorem is the structural version of what RREF reveals algorithmically.

## 2. Gaussian elimination as a factorization

Elimination can be recorded as a matrix factorization rather than repeated from scratch. With partial pivoting, the course writes

`P A = L U`,

where `P` is a permutation matrix, `L` is unit lower triangular (or rectangular lower-trapezoidal in the general rectangular formulation) and `U` is upper triangular/trapezoidal.

At elimination step `k`, a pivot row is selected, commonly by the largest absolute entry available in column `k`. After any row swap, the multiplier used to eliminate entry `a_ik` is

`l_ik = a_ik / a_kk`.

The row update is

`A[i,k+1:n] <- A[i,k+1:n] - l_ik A[k,k+1:n]`.

The multipliers are precisely the subdiagonal entries stored in `L`; the remaining upper part becomes `U`.

## 3. Solving with PA=LU

If `A` is square and nonsingular, solve

`Ax=b`

through

`P A x = P b`, hence `L U x = P b`.

First solve the lower-triangular system

`L y = P b`

by forward substitution, then

`U x = y`

by back substitution.

The dense factorization costs `O(n^3)`, whereas each triangular solve costs `O(n^2)`. Therefore the factorization is particularly useful when many right-hand sides share the same `A`: factor once, reuse `L,U,P`.

Partial pivoting is not a change in the mathematical system; `P` records row reordering chosen for numerical safety.

## 4. Cramer's rule and why it is not a numerical algorithm of choice

For an invertible square matrix, Cramer's rule expresses each unknown as a ratio of determinants. It is mathematically useful for proofs and small symbolic systems, but computing a large linear system by many determinants is much less efficient and generally less numerically appropriate than factorization. The course includes it as linear-algebra structure, not as the recommended large-scale solver.

## 5. Coordinates in a basis

Let `V={v_1,...,v_n}` be a basis of an `n`-dimensional vector space. Every vector `v` has a unique expansion

`v = alpha_1 v_1 + ... + alpha_n v_n`.

The coordinate vector relative to `V` is

`[v]_V = (alpha_1,...,alpha_n)^T`.

A vector is an abstract object; its coordinate array depends on the chosen basis. This distinction becomes essential for understanding matrix representations and similarity.

## 6. Matrix representation of a linear map

Let `F: V -> W` be linear, with bases

`V={v_1,...,v_n}`, `W={w_1,...,w_m}`.

The transformation matrix `A_V^W(F)` is defined columnwise: column `j` is the coordinate vector of `F(v_j)` in basis `W`.

Then for every `v in V`,

`[F(v)]_W = A_V^W(F) [v]_V`.

This is why matrices represent linear maps only after bases have been chosen.

The rank of the transformation matrix equals the dimension of the image of the map:

`rank(A_V^W(F)) = dim(Im(F))`.

For finite-dimensional spaces of the same dimension, a linear map is an isomorphism exactly when its representation matrix is invertible.

## 7. Composition

If `F: V -> W` and `G: W -> Z`, with compatible bases, the matrix of `G o F` is the product of the representation matrices in the same order as function composition:

`A_V^Z(G o F) = A_W^Z(G) A_V^W(F)`.

This explains matrix multiplication as composition of linear transformations rather than as an arbitrary formula.

## 8. Change of basis

Let `V` and `W` be two bases of the same vector space. The identity map has a nontrivial matrix between these coordinate systems; this is the change-of-basis matrix.

If `P` maps `W`-coordinates into `V`-coordinates, then

`[x]_V = P [x]_W`,

and

`[x]_W = P^{-1}[x]_V`.

The exact direction of `P` depends on the naming convention, so always state what its columns mean. Typically its columns are the new basis vectors expressed in the old basis.

## 9. Similar matrices

Let `F: V -> V` be a linear endomorphism. Suppose `A` and `B` are matrices representing the same map in two different bases. Then

`B = P^{-1} A P`

for the appropriate change-of-basis matrix `P`.

Matrices related this way are **similar**. Similarity preserves intrinsic information about the linear map, including characteristic polynomial, determinant, trace and eigenvalues.

This is the conceptual foundation of eigenvalue algorithms: we seek a convenient basis in which the same operator has a simpler matrix.

## 10. Diagonalization

A square matrix is diagonalizable if it is similar to a diagonal matrix:

`A = X Lambda X^{-1}`.

The columns of `X` are a basis of eigenvectors and `Lambda` contains the corresponding eigenvalues. Thus diagonalization is not merely an equation: it means choosing a basis made of eigenvectors so that the linear map acts by independent scalar multiplications.

A real symmetric matrix admits the stronger orthogonal diagonalization

`A = Q Lambda Q^T`.

## 11. Cayley-Hamilton theorem

Let

`p_A(lambda)=det(A-lambda I)`

be the characteristic polynomial, up to the course's sign convention. Cayley-Hamilton states that the matrix satisfies its own characteristic equation:

`p_A(A)=0`.

Consequences relevant later include:

- sufficiently high powers of `A` can be expressed as combinations of lower powers;
- the minimal polynomial has degree at most `n`;
- Krylov spaces cannot keep gaining independent directions beyond dimension `n`.

Thus a theorem introduced in the foundations returns directly in the Krylov module.

## 12. Deep-understanding checkpoint

You should be able to use ranks to classify a system through Rouché-Capelli; derive how elimination multipliers produce `PA=LU`; solve with forward/back substitution and explain factorization reuse; distinguish an abstract linear map from its matrix in a basis; construct a transformation matrix from basis images; derive the similarity relation under change of basis; interpret diagonalization as an eigenvector basis; and state why Cayley-Hamilton limits polynomial powers/Krylov dimensions.

## Sources

Primary: `Slides/Lecture1003-BasicTools.pdf`, transcripts `04Lecture1003_1.txt` through `08Lecture1010_1.txt`, and `Della Santa/PyLab01_basictools.ipynb` with its solution.
