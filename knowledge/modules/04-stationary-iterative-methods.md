# Module 4 - Stationary iterative methods for linear systems

## 1. Why iterate instead of factorizing

The target problem is again

`Ax=b`,

but now `A` may be large and sparse. A direct factorization can require too much memory, create fill-in, or perform much more work than is needed when only an approximate solution is required. An iterative method starts from a guess `x^(0)` and generates

`x^(1), x^(2), ...`

with the goal `x^(k) -> x_*`, where `Ax_*=b`.

Primary sources: `Slides/Lecture1019-Iterative.pdf`; transcripts `15Lecture1020_1.txt`, `16Lecture1020_2.txt`, `18Lecture1024_2.txt`, and the related `19Lecture1027.txt`/`20Lecture1029.txt`; deeper supplied reference `OtherMaterials/Saad_IteratveMethods_2000.pdf`.

## 2. Fixed-point form

A stationary linear iteration can be written

`x^(k+1) = B x^(k) + c`,

where the iteration matrix `B` and vector `c` do not change with `k`.

A fixed point `x_*` satisfies

`x_* = Bx_* + c`.

Subtracting this from the iteration gives the error recurrence

`e^(k+1)=B e^(k)`,

where `e^(k)=x^(k)-x_*`. Therefore

`e^(k)=B^k e^(0)`.

This equation is the key to convergence analysis.

## 3. Matrix splitting

Write

`A=M-N`,

where `M` is chosen so that systems with `M` are easy to solve. Then

`Mx = Nx+b`,

leading to

`x^(k+1)=M^{-1}N x^(k)+M^{-1}b`.

Thus

`B=M^{-1}N`, `c=M^{-1}b`.

In implementation one should normally solve `M y = rhs` rather than explicitly construct `M^{-1}`.

## 4. Exact convergence criterion

The iteration converges to the solution for every initial guess exactly when

`rho(B) < 1`,

where the **spectral radius** is

`rho(B)=max_i |lambda_i(B)|`.

Why: `e^(k)=B^k e^(0)`, and `B^k -> 0` exactly when all eigenvalues lie strictly inside the unit disk.

A sufficient, easier-to-check condition is

`||B|| < 1`

for any consistent/submultiplicative matrix norm, because `rho(B) <= ||B||`.

The spectral-radius condition is necessary and sufficient; norm conditions are usually sufficient but not necessary.

## 5. Jacobi method

Split the matrix into diagonal and off-diagonal parts. Using a common convention,

`A = D - L - U`,

where `D` is diagonal, `-L` is the strict lower part and `-U` the strict upper part. Jacobi uses only the diagonal at the new step:

`D x^(k+1) = (L+U)x^(k)+b`.

Hence

`B_J = D^{-1}(L+U)`.

Componentwise,

`x_i^(k+1) = (1/a_ii) [ b_i - sum_{j != i} a_ij x_j^(k) ]`.

All components use values from iteration `k`, so the updates are conceptually parallel. The method requires nonzero diagonal entries in the chosen ordering.

## 6. Gauss-Seidel method

Gauss-Seidel immediately reuses newly computed components. With the same splitting,

`(D-L)x^(k+1) = Ux^(k)+b`,

so

`B_GS = (D-L)^{-1}U`.

Componentwise, entries `j<i` use iteration `k+1` while entries `j>i` still use iteration `k`.

Because it incorporates new information sooner, Gauss-Seidel often converges faster than Jacobi, but the exact behavior is matrix-dependent and must be understood through its iteration matrix.

## 7. Common sufficient convergence structures

The course emphasizes spectral-radius analysis. Standard structures that guarantee convergence for important stationary methods include suitable diagonal dominance and, especially for Gauss-Seidel, symmetric positive definiteness under the standard hypotheses.

A matrix is **strictly diagonally dominant by rows** when

`|a_ii| > sum_{j != i} |a_ij|`

for every row. Such conditions help show contraction/convergence without explicitly computing all eigenvalues.

A real matrix is **symmetric positive definite (SPD)** when `A=A^T` and

`x^T A x > 0`

for every nonzero `x`. SPD structure is central throughout numerical linear algebra because it gives strong geometric and convergence properties.

## 8. Residual and error

At iteration `k`, define

`r^(k)=b-Ax^(k)`.

If `x_*` is exact and `e^(k)=x^(k)-x_*`, then

`r^(k) = -A e^(k)`

with this error sign convention, and

`e^(k) = -A^{-1} r^(k)`

when `A` is invertible.

Therefore a small residual does not universally imply a small forward error. For an ill-conditioned matrix, `||A^{-1}||` can strongly amplify the residual.

A useful relative perturbation bound has the form

`relative error <= kappa(A) * relative residual`

up to the precise normalization used. The condition number tells us how informative the residual is about the solution error.

## 9. Stopping criteria

An infinite limiting process must be stopped in computation. Common tests include:

- residual test: `||r^(k)|| <= tol` or a relative version such as `||r^(k)||/||b|| <= tol`;
- iterate-change test: `||x^(k+1)-x^(k)||` small relative to `||x^(k+1)||`;
- maximum iteration count as a safety limit.

The stopping criterion should reflect the actual target. A small iterate change can occur during slow/stagnating convergence, so it is best interpreted together with the residual.

## 10. Convergence speed

When the asymptotic behavior is governed by a dominant eigenvalue of the iteration matrix, the error often decays roughly like

`rho(B)^k`.

Thus `rho(B)=0.1` suggests much faster asymptotic contraction than `rho(B)=0.99`. Merely having `rho(B)<1` says the method converges, not that it converges quickly.

This insight anticipates the power method, where ratios of eigenvalue magnitudes similarly control convergence.

## 11. Cost model

For a sparse problem, one iteration can be cheap if it uses only the stored entries and simple solves with `M`. Total cost is roughly

`cost per iteration x number of iterations`.

Therefore a method with a more expensive iteration can still win if it reduces the iteration count substantially. This tradeoff motivates preconditioning in broader iterative-method theory: replace the problem by an equivalent one whose iteration/Krylov convergence is better while keeping the auxiliary solves cheap.

## 12. Stationary methods as a conceptual bridge

Even when modern large-scale solvers use Krylov methods rather than basic Jacobi/Gauss-Seidel, stationary iterations teach three central ideas:

1. rewrite the problem into an iterative map;
2. analyze convergence through the spectrum of an operator;
3. judge computed approximations through residuals and conditioning.

These ideas recur in every later iterative algorithm.

## 13. Exam checklist

Be able to derive an iteration from `A=M-N`; derive `e^(k+1)=Be^(k)`; state and explain `rho(B)<1`; write Jacobi and Gauss-Seidel in matrix and component form; distinguish residual from error; explain the influence of conditioning; and describe practical stopping criteria and cost tradeoffs.

## 14. Sources

- `Slides/Lecture1019-Iterative.pdf`
- `Slides/Trascrizioni/15Lecture1020_1.txt`, `16Lecture1020_2.txt`, `18Lecture1024_2.txt`, `19Lecture1027.txt`, `20Lecture1029.txt`
- `OtherMaterials/Saad_IteratveMethods_2000.pdf` for extended theory on sparse iterative methods
