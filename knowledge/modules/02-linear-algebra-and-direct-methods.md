# Module 2 - Linear algebra foundations and direct methods

## 1. Linear systems as the basic problem

A linear system is written

`Ax = b`,

where `A in R^{m x n}` is the coefficient matrix, `x in R^n` is the unknown vector and `b in R^m` is the right-hand side. When `m=n`, the system is square. A square system has a unique solution for every `b` exactly when `A` is invertible, equivalently when `rank(A)=n`, `det(A) != 0`, and `ker(A)={0}`.

These equivalences are mathematical; numerically, a matrix can be invertible but extremely ill-conditioned, so small perturbations or rounding errors may cause large changes in the computed solution.

Primary sources: `Slides/Lecture1003-BasicTools.pdf`; transcripts `04Lecture1003_1.txt` through `08Lecture1010_1.txt`; `Della Santa/PyLab01_basictools.ipynb` and its solution; `Della Santa/testmatrices.py`.

## 2. Vector spaces, span, independence and basis

A vector space is a set closed under vector addition and scalar multiplication. For vectors `v_1,...,v_k`,

`span{v_1,...,v_k}`

is the set of all linear combinations `alpha_1 v_1 + ... + alpha_k v_k`.

The vectors are **linearly independent** if

`alpha_1 v_1 + ... + alpha_k v_k = 0`

implies every `alpha_i=0`. A **basis** is a linearly independent generating set. The number of basis vectors is the dimension of the space.

For a matrix `A`:

- the **column space** or image `Im(A)` is the span of its columns;
- the **null space** or kernel `ker(A)` is `{x : Ax=0}`;
- `rank(A)=dim(Im(A))`;
- rank-nullity gives `rank(A)+dim(ker(A))=n` for `A in R^{m x n}`.

## 3. Linear transformations and matrices

A linear map `T` satisfies

`T(alpha x + beta y)=alpha T(x)+beta T(y)`.

Once bases are fixed, every finite-dimensional linear map is represented by a matrix. Matrix multiplication corresponds to composition of linear maps. This viewpoint is useful later because orthogonal projections, Householder reflections, Givens rotations and Krylov projections are all linear transformations represented by structured matrices.

## 4. Determinant

For a square matrix, the determinant is a scalar with several equivalent interpretations. It detects singularity:

`det(A)=0` if and only if `A` is singular.

The labs recall Laplace/cofactor expansion as a mathematical definition/recursive construction. For an `n x n` matrix,

`det(A) = sum_j (-1)^{i+j} a_{ij} det(A_{ij})`

for any fixed row `i`, where `A_{ij}` is the submatrix obtained by deleting row `i` and column `j`.

This formula is conceptually useful but computationally poor for large `n`; elimination-based determinant computation is much more efficient.

## 5. Elementary row operations

Gaussian elimination transforms a system into an equivalent one using operations that preserve its solution set:

1. swap two rows;
2. multiply a row by a nonzero scalar;
3. add a multiple of one row to another.

Applied to the augmented matrix `[A | b]`, these operations simplify the system without changing the set of `x` satisfying it.

## 6. Row echelon and reduced row echelon forms

A matrix is in **row echelon form (REF)** when zero rows are below nonzero rows, each leading/pivot entry occurs to the right of the pivot in the row above, and entries below each pivot are zero.

A matrix is in **reduced row echelon form (RREF)** when, additionally, each pivot is normalized to one and is the only nonzero entry in its pivot column.

REF is sufficient for solving a nonsingular square system by back substitution. RREF exposes the complete solution structure of rectangular/rank-deficient systems: pivot variables, free variables, consistency and null-space degrees of freedom.

## 7. Gaussian elimination

For a square nonsingular system, elimination proceeds column by column. At step `k`, choose a nonzero pivot in column `k`; for each row `i>k`, eliminate `a_{ik}` using a multiplier

`m_{ik}=a_{ik}/a_{kk}`,

and update

`row_i <- row_i - m_{ik} row_k`.

After the forward phase, the matrix is upper triangular and the system `Ux=c` is solved by back substitution.

Ignoring pivot search, the dense arithmetic cost of elimination is `O(n^3)` while a triangular solve costs `O(n^2)`. This cubic cost is one reason large sparse systems motivate iterative methods.

## 8. Pivoting

A zero pivot makes the basic formula impossible even if the matrix is nonsingular. A very small pivot can also amplify floating-point errors. Row exchanges are therefore used to obtain a more suitable pivot. **Partial pivoting** selects a large-magnitude available entry in the current column and swaps it into the pivot position.

The conceptual lesson is that algebraically equivalent elimination paths can have very different numerical stability.

## 9. Numerical zero and rank decisions

In exact arithmetic, a pivot is either zero or not. In floating point, computed values can be tiny because of rounding. The labs explicitly emphasize tolerance-based tests. A quantity is treated as zero when

`|a| <= tol`

for a carefully chosen tolerance, possibly scaled to the data.

This is not an arbitrary programming trick: numerical rank is inherently scale- and tolerance-dependent. The same issue recurs in Gram-Schmidt breakdown, singular-value truncation and iterative stopping tests.

## 10. Norms

A vector norm measures size. The course repeatedly uses

`||x||_1 = sum_i |x_i|`,

`||x||_2 = sqrt(sum_i |x_i|^2)`,

`||x||_infinity = max_i |x_i|`.

A matrix norm measures the size of a linear operator. An induced norm is

`||A|| = max_{x != 0} ||Ax||/||x||`.

For the Euclidean norm, `||A||_2` equals the largest singular value of `A`, a fact revisited in the SVD module.

Norms make statements such as convergence, perturbation size, residual size and approximation error precise.

## 11. Conditioning

Conditioning describes sensitivity of a mathematical problem to perturbations. For an invertible linear system, the 2-norm condition number is

`kappa_2(A)=||A||_2 ||A^{-1}||_2 = sigma_max(A)/sigma_min(A)`.

A condition number near one indicates a well-conditioned linear solve; a very large condition number means that small relative perturbations in data or rounding can be strongly amplified.

Conditioning is a property primarily of the problem/matrix, while **stability** describes the behavior of an algorithm. A stable algorithm cannot remove intrinsic ill-conditioning.

## 12. Residual versus forward error

If `x_*` is the exact solution and `x` an approximation, the **forward error** is

`e = x - x_*`.

The **residual** is

`r = b - Ax`.

Since `Ax_*=b`,

`r = -A e`,

up to the chosen sign convention; equivalently `e = -A^{-1}r` when `A` is invertible. Thus a small residual does not automatically mean a small solution error when `A^{-1}` has large norm. This distinction becomes central in iterative methods.

## 13. Rectangular systems

For `A in R^{m x n}` with `m != n`, there may be no solution or infinitely many solutions.

- If `b in Im(A)`, the system is consistent.
- If the columns are not independent, nonzero vectors in `ker(A)` create nonuniqueness.
- If an overdetermined system is inconsistent, the least-squares problem finds an `x` minimizing `||Ax-b||_2` rather than solving `Ax=b` exactly.

This is the bridge to orthogonal projections and least squares.

## 14. Laboratory logic

`PyLab01_basictools.ipynb` asks students to implement determinant computation, REF/RREF and linear-system logic rather than simply calling a black-box solver. The corresponding solution notebook can be used to verify the intended algorithmic structure. `testmatrices.py` supplies matrices/systems for experiments, including cases designed to expose numerical and structural behavior.

For an implementation, always verify results by computing a residual or reconstruction, not only by comparing printed values.

## 15. Exam-level checklist

You should be able to define span, basis, independence, image, kernel and rank; connect invertibility/rank/determinant for square matrices; derive the elimination update; distinguish REF from RREF; explain back substitution; state why pivoting matters; define common norms and conditioning; and explain why residual and forward error are different quantities.

## 16. Sources

- `Slides/Lecture1003-BasicTools.pdf`
- `Slides/Trascrizioni/04Lecture1003_1.txt` through `08Lecture1010_1.txt`
- `Della Santa/PyLab01_basictools.ipynb`
- `Della Santa/solPyLab01_basictools.ipynb`
- `Della Santa/testmatrices.py`
