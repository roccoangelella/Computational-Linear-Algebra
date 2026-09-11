# Depth supplement 4 - Sharper convergence theory for Jacobi and Gauss-Seidel

This supplement expands `knowledge/modules/04-stationary-iterative-methods.md` with the comparison theorems stated in `Slides/Lecture1019-Iterative.pdf`.

## 1. Recall the exact criterion

A stationary iteration

`x^(k+1)=B x^(k)+c`

has error

`e^(k)=B^k e^(0)`.

It converges for every initial vector exactly when

`rho(B)<1`.

A matrix norm condition such as `||B||<1` is sufficient because `rho(B)<=||B||`, but it is not generally necessary.

## 2. Strict diagonal dominance

A matrix is strictly diagonally dominant by rows when

`|a_ii| > sum_{j!=i}|a_ij|`

for every `i`. There is an analogous column condition.

The course states the following useful sufficient results:

- if `A` is strictly diagonally dominant, Jacobi converges;
- if `A` is strictly diagonally dominant, Gauss-Seidel converges.

These are stronger practical statements than merely writing `rho(B)<1`, because they let us infer convergence directly from the entries of `A` without explicitly forming all eigenvalues of the iteration matrix.

Diagonal dominance is sufficient, not necessary: a method can converge even when the condition fails.

## 3. Symmetric positive definite matrices

If `A` is real symmetric positive definite, meaning

`A=A^T`, and `x^T A x>0` for every nonzero `x`,

then Gauss-Seidel converges under the standard splitting.

This theorem illustrates an important recurring theme: structural information about `A` can imply spectral information about an iteration without directly computing `rho(B_GS)`.

## 4. Jacobi and Gauss-Seidel do not universally succeed together

Outside special matrix classes, convergence of Jacobi does not imply convergence of Gauss-Seidel, and convergence of Gauss-Seidel does not imply convergence of Jacobi. The informal statement “Gauss-Seidel is always better” is false.

When both converge, Gauss-Seidel often contracts faster because it immediately reuses new components, but a rigorous comparison needs hypotheses.

## 5. Stein-Rosenberg theorem

For the matrix class stated in the course,

`a_ij <= 0` for `i != j`, and `a_ii > 0`,

one and only one of the following spectral-radius configurations occurs:

1. `0 < rho(B_GS) < rho(B_J) < 1`;
2. `1 < rho(B_J) < rho(B_GS)`;
3. `rho(B_GS)=rho(B_J)=0`;
4. `rho(B_GS)=rho(B_J)=1`.

The first case formalizes the familiar favorable situation: both methods converge, and Gauss-Seidel has the smaller asymptotic contraction factor. The second case shows that when the relevant radii exceed one, both diverge, with Gauss-Seidel worse in this ordering.

The theorem is conditional on this sign structure; do not apply it to an arbitrary matrix.

## 6. Tridiagonal positive-diagonal case

For the matrix class stated in the course - tridiagonal coefficient matrices with positive diagonal entries - the iteration matrices satisfy

`rho(B_GS) = rho(B_J)^2`.

Therefore Jacobi and Gauss-Seidel either both converge or both fail to converge in that setting. If `0<rho(B_J)<1`, squaring a number in `(0,1)` makes it smaller, so Gauss-Seidel has faster asymptotic decay.

If a representative Jacobi error component behaves like `rho(B_J)^k`, the Gauss-Seidel relation behaves like `rho(B_J)^(2k)`, which motivates the course statement that its convergence speed is effectively doubled in the asymptotic exponent for this class.

## 7. Residual-based stopping and conditioning

The course connects residual tolerance to forward error through conditioning. If `r=b-Ax` and `x_*` is the exact solution, then `e=x-x_*=-A^{-1}r` under the module's sign convention. Relative error can therefore be bounded by a condition-number multiple of relative residual, up to the precise norm/normalization assumptions:

`relative forward error <= kappa(A) * relative residual`.

Thus a residual tolerance such as `10^-8` is not automatically an eight-digit solution guarantee. The interpretation depends on `kappa(A)`.

Always combine a convergence test with a maximum iteration count to avoid an indefinitely running iteration when assumptions fail or convergence is unacceptably slow.

## 8. How to compare methods scientifically

For a specific matrix:

1. derive the Jacobi and Gauss-Seidel splittings;
2. identify `B_J` and `B_GS`;
3. use a theorem based on matrix structure when applicable;
4. otherwise estimate/compute spectral radii for a diagnostic small problem;
5. compare residual histories and work per iteration;
6. account for sparsity and the sequential nature of Gauss-Seidel updates.

A smaller iteration count is not by itself a complete performance comparison; wall-clock work and parallelism can differ.

## 9. Deep-understanding checkpoint

Be able to distinguish exact and sufficient convergence criteria; prove/use diagonal-dominance implications at the level required by the course; state the SPD Gauss-Seidel result; explain why Jacobi and Gauss-Seidel are not universally ordered; state the Stein-Rosenberg alternatives with their hypotheses; derive the implication of `rho(B_GS)=rho(B_J)^2` in the tridiagonal case; and relate residual tolerance to conditioning.

## Sources

Primary: `Slides/Lecture1019-Iterative.pdf` and transcripts `15Lecture1020_1.txt`, `16Lecture1020_2.txt`, `18Lecture1024_2.txt`, `19Lecture1027.txt`, `20Lecture1029.txt`.
