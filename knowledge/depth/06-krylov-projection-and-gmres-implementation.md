# Depth supplement 6 - Projection framework, restarting and practical GMRES

This supplement expands `knowledge/modules/06-krylov-arnoldi-fom-gmres.md` with implementation and projection details from `Slides/Lecture1030-Krylov.pdf`.

## 1. General projection framework

For a large linear system `Ax=b`, start from `x_0` and seek a correction `delta` in a low-dimensional **search space** `K`:

`x = x_0 + delta`, with `delta in K`.

The residual is

`r=b-Ax`.

A projection method determines the correction by requiring the residual to satisfy conditions against a **test/constraint space** `L`, usually of the same dimension as `K`:

`r orthogonal to L`.

If `K=L`, the method is an orthogonal/Galerkin projection in the Euclidean inner-product sense. If `K` and `L` differ, the projection is oblique. This language unifies many methods: the approximation space alone does not define the method; the residual condition matters equally.

For FOM, both spaces are the Krylov space. For GMRES, the approximation lies in a Krylov space while the residual is chosen by a least-squares/minimum-residual condition, equivalently an orthogonality condition against `A K_m` under the standard Euclidean formulation.

## 2. Cayley-Hamilton and finite Krylov dimension

Cayley-Hamilton says that an `n x n` matrix satisfies its characteristic polynomial. Therefore `A^n` is a linear combination of lower powers of `A`. Applied to a vector `r_0`, this implies that

`r_0, A r_0, ..., A^n r_0`

cannot all be linearly independent. Hence the Krylov sequence saturates in at most `n` dimensions.

The sharper object is the minimal polynomial relative to `r_0`; its degree determines when the generated sequence first becomes algebraically dependent. This is the exact-arithmetic reason finite termination is possible.

## 3. Cost growth of full Arnoldi/FOM

At Arnoldi step `j`, the new vector must be orthogonalized against roughly `j` existing vectors. If each vector has length `n`, the cumulative orthogonalization work through dimension `m` grows like `O(m^2 n)` in the standard Gram-Schmidt organization, in addition to `m` matrix-vector products.

Memory also grows because the method stores `m` basis vectors of length `n`, i.e. `O(mn)` vector storage, plus the small Hessenberg matrix.

This is why a mathematically finite process can still become impractical long before `m=n`.

## 4. Restarted FOM

A restart limits the basis dimension to a chosen `M`:

1. run FOM for at most `M` Krylov steps from the current initial guess;
2. take the resulting approximation as the new `x_0`;
3. recompute the residual;
4. build a fresh Krylov basis;
5. repeat until the global stopping criterion is met.

Restarting caps memory and per-cycle orthogonalization cost. The tradeoff is that discarding the old subspace can also discard useful spectral information, so convergence may slow or stagnate.

## 5. GMRES reduced least-squares problem

With Arnoldi

`A Q_m = Q_{m+1} Hbar_m`

and `r_0=beta q_1`, GMRES solves

`min_y || beta e_1 - Hbar_m y ||_2`.

A naive solution through normal equations

`Hbar_m^T Hbar_m y = Hbar_m^T beta e_1`

would unnecessarily square conditioning. Instead, the reduced problem is maintained through an orthogonal QR factorization of `Hbar_m`.

## 6. Why Givens rotations are natural inside GMRES

At each Arnoldi step, `Hbar_m` gains only one new column and one new subdiagonal entry. Previously computed Givens rotations can be applied to the new column, and then one new rotation annihilates the fresh subdiagonal element.

This yields two important computational advantages:

- the triangular factor needed to recover `y_m` is updated incrementally rather than recomputed from scratch;
- applying the same rotations to `beta e_1` exposes the residual norm cheaply, so GMRES can monitor convergence without explicitly forming the large residual vector every time.

This is a concrete link between Module 3's Givens QR and the large-scale solver.

## 7. Householder alternative

Householder transformations can also be used to implement orthogonalization/QR stably. They tend to provide excellent orthogonality but can require a different storage/update organization than modified Gram-Schmidt. The course presents them as another route for robust orthogonal transformations.

In large sparse Krylov software, the implementation choice balances stability, data movement, storage and ease of updating the small projected problem.

## 8. Restarted GMRES

GMRES suffers the same growing-basis issue as FOM, so `GMRES(M)` restarts after a fixed subspace dimension. Each cycle minimizes the residual over the current Krylov space, then starts again from the new residual.

Restarting makes memory predictable, but unlike unrestarted GMRES the residual-minimizing spaces are no longer nested across all historical iterations. Consequently restarted GMRES can converge much more slowly and can stagnate on difficult spectra.

The restart dimension is therefore a numerical parameter, not merely a memory setting.

## 9. Residual polynomial viewpoint

For `x_0=0` or, more generally, after accounting for the initial residual, a Krylov residual can often be written

`r_m = p_m(A) r_0`

for a polynomial satisfying `p_m(0)=1`. GMRES chooses, implicitly, a polynomial that makes the residual norm small over the spectral/nonnormal behavior seen by `r_0`.

This explains why eigenvalue distribution matters but does not tell the whole story for nonsymmetric matrices: nonnormality/eigenvector conditioning can make convergence behavior more complicated than a simple eigenvalue-ratio estimate.

## 10. Preconditioning in the projection picture

A preconditioner replaces the original equation by an equivalent or closely related system whose Krylov geometry is more favorable. Left preconditioning uses

`M^{-1}Ax = M^{-1}b`.

Right preconditioning writes

`A M^{-1} y=b`, followed by `x=M^{-1}y`.

The two choices lead to different residuals/search spaces, so a practical implementation must state which convention it uses. The ideal `M` approximates `A` well enough to improve convergence while remaining cheap to apply/solve with.

## 11. Deep-understanding checkpoint

You should be able to define search and test spaces; distinguish Galerkin and oblique projection; derive why Cayley-Hamilton bounds Krylov dimension; explain the `O(m^2 n)` orthogonalization and `O(mn)` basis-storage growth; describe restarted FOM/GMRES and their convergence tradeoff; derive the reduced GMRES least-squares problem; explain why incremental Givens QR is used instead of normal equations; and state how preconditioning changes the operator being explored.

## Sources

Primary: `Slides/Lecture1030-Krylov.pdf`, transcripts `22Lecture1031_2.txt` through the Krylov part of `25Lecture1107.txt`, `Della Santa/PyLab03_krylov.ipynb` and solution, with `OtherMaterials/Saad_IteratveMethods_2000.pdf` as secondary deep reference.
