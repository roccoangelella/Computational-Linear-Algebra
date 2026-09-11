# Concept graph

This document is a lightweight, human-readable knowledge graph. An arrow `A -> B` means that understanding `A` is a useful prerequisite for `B` in this course. “Uses” links describe applications rather than strict prerequisites.

## Core dependency graph

```text
matrix/vector basics
  -> sparse matrix representation
  -> linear systems -> Gaussian elimination -> conditioning
  -> vector spaces -> inner products/norms -> orthogonality
                                    -> projectors -> least squares
                                    -> Gram-Schmidt/Givens/Householder -> QR ideas
                                                                       -> Arnoldi -> Krylov solvers
                                                                       -> Lanczos
                                                                       -> QR eigensolver
                                                                       -> SVD computation
  -> eigenvalues/eigenvectors -> spectral radius -> stationary iteration convergence
                              -> power/inverse-power -> shifts/deflation
                              -> graph Laplacian spectra -> spectral clustering
                              -> PageRank
                              -> covariance eigendecomposition -> PCA
  -> polynomials of matrices -> minimal polynomial -> Krylov spaces -> Arnoldi/FOM/GMRES
  -> SVD -> low-rank approximation
         -> pseudoinverse -> least squares/minimum norm
         -> PCA via centered data matrix

statistics (mean/variance/covariance)
  -> covariance matrix -> PCA -> k-means on reduced scores

graphs (adjacency/degree)
  -> sparse matrices
  -> graph Laplacian -> spectral clustering
  -> hyperlink matrix -> PageRank
```

## Retrieval aliases

Use these aliases when GitHub search misses a concept because transcripts contain recognition errors.

| Canonical concept | Useful aliases / transcript variants |
|---|---|
| Gram–Schmidt | Gram Schmidt, Grashmint, GrungeMit |
| Householder | Householder, Hausweilden, outsolder |
| Givens | Givens, Gibbons |
| Krylov | Krylov, Krilov, Cree-Lob, criminal subspace (ASR error) |
| Arnoldi | Arnoldi |
| Hessenberg | Hessenberg, S-mberg (ASR error) |
| Gauss–Seidel | Gauss Seidel, Seidel |
| Gershgorin | Gershgorin, Gerschgorin |
| Rayleigh quotient | Rayleigh quotient, really quotient (ASR error) |
| eigenvalue | eigenvalue, eigen value, “agent value/venue” (ASR errors) |
| SVD | singular value decomposition, singular values |
| PCA | principal component analysis, principal components |
| Moore–Penrose pseudoinverse | pseudoinverse, pseudo inverse, pinv |

## High-value conceptual bridges

### Orthogonality -> numerical algorithms

An orthonormal basis preserves Euclidean geometry and avoids solving badly scaled coordinate systems. The course repeatedly reuses orthogonality: QR factorization, stable basis construction, projections, Arnoldi/Lanczos, and SVD all depend on it.

### Polynomial approximation -> Krylov methods

A vector in `K_m(A,b)` has the form `p_{m-1}(A)b` for a polynomial of degree at most `m-1`. This is why minimal polynomials, finite termination, and approximation quality are linked.

### Spectral radius -> stationary iteration

For an iteration `x^{(k+1)} = Bx^{(k)} + c`, the error satisfies `e^{(k+1)} = B e^{(k)}`. Thus powers `B^k` govern convergence, and the spectral radius `rho(B)` is the decisive asymptotic quantity.

### Eigenvalues -> data/graph applications

The same eigenvector mathematics appears in three distinct applications: PageRank (dominant stationary vector), spectral clustering (Laplacian eigenvectors), and PCA (covariance eigenvectors). Retrieval should therefore search across the eigenvalue module and the application-specific source.

### SVD -> least squares and PCA

The SVD separates a linear map into orthogonal coordinate changes plus axis-wise scaling. Nonzero singular directions reveal rank; truncation yields low-rank approximations; reciprocals of nonzero singular values define the pseudoinverse; applying SVD to centered data yields principal directions without explicitly forming the covariance matrix.
