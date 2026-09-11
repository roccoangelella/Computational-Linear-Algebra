# Module 5 - Approximation, regression and least squares

## 1. From exact interpolation to approximation

Given observations `(t_i,y_i)`, one can try to construct a function that reproduces every value exactly or a function that approximates the data according to a criterion.

**Interpolation** imposes exact conditions `p(t_i)=y_i`. If the model has enough degrees of freedom and the interpolation matrix is nonsingular, an exact fit exists. Exact interpolation is appropriate when the data are regarded as exact samples of an underlying function and matching them is the goal.

**Approximation/regression** accepts nonzero discrepancies and chooses model parameters that make those discrepancies small according to an objective. This is more natural for noisy data or when a low-dimensional model is intentionally used.

Primary sources: `Slides/Lecture1024-Approssimazione.pdf`; lecture `21Lecture1031_1.txt` and relevant material in `22Lecture1031_2.txt`; orthogonal-projection foundations from Module 3.

## 2. Linear-in-the-parameters models

Suppose the model is

`f(t; x) = x_1 phi_1(t) + ... + x_n phi_n(t)`,

where the basis functions `phi_j` are fixed and the coefficients `x_j` are unknown. Evaluating at data points `t_1,...,t_m` produces the design matrix

`A_ij = phi_j(t_i)`.

Then the predicted data are `Ax` and fitting becomes a linear-algebra problem.

For polynomial fitting with degree `n-1`, a common basis is

`1, t, t^2, ..., t^{n-1}`,

giving a Vandermonde-type design matrix. The model is nonlinear as a function of `t` but linear in the unknown coefficients, so linear least squares applies.

## 3. Overdetermined systems

Usually `m>n`: there are more observations than model parameters. The system

`Ax=b`

will generally be inconsistent because the data vector `b` need not lie exactly in the `n`-dimensional column space of `A`.

The least-squares problem is

`min_x ||Ax-b||_2`.

The minimizer selects the point `Ax` in `Im(A)` closest to `b` in Euclidean distance.

## 4. Geometric derivation

At the optimum `x_*`, the residual

`r_*=b-Ax_*`

must be orthogonal to the column space of `A`. Otherwise moving the approximation in a column-space direction could decrease the distance.

Thus

`A^T r_* = 0`,

which gives the normal equations

`A^T A x_* = A^T b`.

If the columns of `A` are linearly independent, `A^T A` is symmetric positive definite and the minimizer is unique.

The approximation itself is the orthogonal projection

`p = Ax_* = P_A b`,

where

`P_A = A(A^T A)^{-1}A^T`

for full column rank.

## 5. QR solution

If `A=QR` is a thin QR factorization with `Q^TQ=I`, then

`Ax = QRx`.

The optimality condition becomes

`R x_* = Q^T b`.

This reduces the problem to an upper-triangular solve and avoids explicitly forming `A^T A`.

The numerical advantage is important because

`kappa_2(A^T A)=kappa_2(A)^2`.

Thus the normal equations can lose substantially more accuracy when `A` is poorly conditioned.

## 6. Residual sum of squares

Minimizing the Euclidean norm is equivalent to minimizing its square:

`||Ax-b||_2^2 = sum_i (prediction_i - observation_i)^2`.

This quantity is the residual sum of squares. Squaring makes the objective differentiable and penalizes large deviations more strongly than small ones.

Taking derivatives gives another derivation of the normal equations:

`f(x)=||Ax-b||_2^2`

has gradient

`grad f(x)=2 A^T(Ax-b)`.

Setting the gradient to zero yields

`A^T A x=A^T b`.

## 7. Choice of basis and conditioning

Two sets of basis functions can span the same model space but lead to matrices with very different conditioning. High-degree monomials on an inconvenient interval can produce a severely ill-conditioned Vandermonde matrix. This is a numerical issue, not a change in the abstract approximation space.

Orthogonal or better-scaled bases can reduce conditioning problems. The broader lesson is that a representation/basis is part of numerical algorithm design.

## 8. Model complexity

Using more basis functions gives a larger approximation space, so the least-squares residual cannot increase in exact arithmetic. However, a smaller training residual does not automatically imply a better model of unseen/noisy data. From the linear-algebra perspective, increasing the dimension also changes conditioning and can make coefficients more sensitive.

The course's main focus is the numerical linear-algebra machinery, but this modeling distinction explains why approximation is not simply 'interpolate with the highest possible degree'.

## 9. Rank-deficient least squares

If the columns of `A` are linearly dependent, `A^T A` is singular and coefficient vectors minimizing the residual need not be unique. The fitted vector `Ax` can still be well-defined even when multiple coefficient vectors produce it.

The later SVD module gives the complete treatment. The Moore-Penrose pseudoinverse provides the minimum-Euclidean-norm least-squares solution

`x^+ = A^+ b`.

This is one reason the SVD closes the conceptual loop of the course.

## 10. Approximation and projection methods

Least squares introduces a general pattern that reappears in Krylov methods:

1. choose a lower-dimensional subspace in which the approximation will live;
2. characterize the best approximation by an orthogonality/minimization condition;
3. solve a smaller projected problem.

FOM and GMRES differ in their precise conditions, but conceptually they are projection methods applied to the solution/residual of a large linear system.

## 11. Practical workflow

For a data-fitting problem:

1. choose basis functions and form the design matrix `A`;
2. inspect dimensions and rank/conditioning;
3. compute a QR factorization or use a reliable least-squares routine;
4. solve the resulting triangular problem;
5. inspect residuals and, if meaningful, compare fit quality for different model spaces;
6. do not infer numerical accuracy solely from a small residual if the design matrix is ill-conditioned.

## 12. Exam checklist

Be able to distinguish interpolation and approximation; construct a design matrix; formulate least squares; derive the residual-orthogonality condition; derive the normal equations; derive the QR solution; explain why forming `A^T A` can be numerically undesirable; and explain what changes when `A` is rank deficient.

## 13. Sources

- `Slides/Lecture1024-Approssimazione.pdf`
- `Slides/Trascrizioni/21Lecture1031_1.txt`
- `Slides/Trascrizioni/22Lecture1031_2.txt`
- prerequisites: `Slides/Lecture1016-OrtProj.pdf` and Module 3
