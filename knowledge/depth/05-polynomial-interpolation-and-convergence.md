# Depth supplement 5 - Polynomial interpolation, convergence and the transition to least squares

This supplement fills the largest gap found by the deep-coverage audit. It reconstructs the polynomial-interpolation material from `Slides/Lecture1024-Approssimazione.pdf` that precedes least squares in the course.

## 1. Approximation spaces and uniform error

An approximation problem chooses a finite-dimensional function space `F_m` and an approximant `f_m in F_m`. The dimension of `F_m` counts how many independent coefficients must be determined.

For continuous functions on `[a,b]`, the course uses the uniform norm

`||f||_infinity = max_{x in [a,b]} |f(x)|`.

A sequence of approximants converges uniformly to `f` when

`||f-f_m||_infinity -> 0`.

Uniform convergence controls the worst pointwise error on the whole interval.

## 2. Polynomial interpolation problem

Given `n+1` distinct nodes and data

`(x_i,y_i)`, `i=0,...,n`,

seek a polynomial `p_n in P_n` satisfying

`p_n(x_i)=y_i` for every `i`.

Let `{phi_0,...,phi_n}` be a basis of `P_n` and write

`p_n(x)=sum_{k=0}^n a_k phi_k(x)`.

Imposing the interpolation conditions produces the square system

`G a = y`,

with

`G_ik = phi_k(x_i)`.

Existence and uniqueness of the interpolant are equivalent to invertibility of this interpolation matrix. For polynomial interpolation, distinct nodes guarantee a unique degree-at-most-`n` interpolating polynomial.

## 3. Monomial basis and Vandermonde matrix

With the monomial basis

`1,x,x^2,...,x^n`,

the interpolation matrix is a Vandermonde matrix. Its determinant is nonzero for distinct nodes, so the interpolation problem is mathematically well posed in the sense of uniqueness.

However, uniqueness does not imply good numerical conditioning. Vandermonde systems in the monomial basis can be badly conditioned, especially as degree grows or nodes are poorly scaled. The course therefore motivates choosing a basis that represents the interpolation conditions directly.

## 4. Lagrange basis

Define the Lagrange basis polynomials

`ell_k(x) = product_{i != k} (x-x_i)/(x_k-x_i)`.

They satisfy the cardinal property

`ell_k(x_i) = delta_ik`,

where `delta_ik` is `1` when `i=k` and `0` otherwise.

Therefore the interpolating polynomial is immediately

`p_n(x) = sum_{k=0}^n y_k ell_k(x)`.

No general linear system for the coefficients is needed because, in this basis, the interpolation coefficients are exactly the data values `y_k`.

The Lagrange representation makes the mathematical interpolant explicit. It does not by itself mean that the naive product formula is the best high-performance evaluation algorithm; numerical implementation and representation remain separate questions.

## 5. Interpolation error

For an underlying function `f`, define

`E_n(x)=f(x)-p_n(x)`.

The error vanishes at every interpolation node. If `f` itself belongs to `P_n`, the error is identically zero because the degree-at-most-`n` interpolant is unique.

The central question is whether

`||E_n||_infinity -> 0`

as more interpolation nodes are added. The answer depends not only on the smoothness/approximability of `f`, but also on how the nodes are chosen.

## 6. Lebesgue constant and the fundamental stability bound

Let

`Lambda_n = max_{x in [a,b]} sum_{i=0}^n |ell_i(x)|`

be the Lebesgue constant for the chosen nodes. It measures how strongly interpolation can amplify perturbations/best-approximation error.

The course states the bound

`||f-p_n||_infinity <= (1+Lambda_n) min_{q in P_n} ||f-q||_infinity`.

This separates two effects:

- `min_{q in P_n} ||f-q||_infinity` depends on how well degree-`n` polynomials can approximate the function;
- `Lambda_n` depends only on the node set and measures the stability/quality of interpolation relative to best polynomial approximation.

A function may be very well approximable by polynomials while interpolation at a poor sequence of nodes still behaves badly because the Lebesgue constant grows too rapidly.

## 7. Weierstrass approximation theorem

For every continuous function `f` on a closed interval and every `epsilon>0`, there exists a polynomial `p` such that

`||f-p||_infinity < epsilon`.

Equivalently, the best polynomial-approximation error tends to zero as degree increases:

`min_{q in P_n} ||f-q||_infinity -> 0`.

This theorem guarantees that polynomials are rich enough to approximate continuous functions uniformly. It does **not** say that interpolation on every node sequence converges. The Lebesgue factor in the previous bound is why the distinction matters.

## 8. Equally spaced versus Chebyshev nodes

For equally spaced nodes, the Lebesgue constant can grow very rapidly with `n`, making high-degree global interpolation unstable and potentially nonconvergent near interval endpoints for some smooth functions.

A much better node distribution on `[-1,1]` is given by Chebyshev-type nodes

`x_i = cos( ((2i+1)/(2(n+1))) pi )`, `i=0,...,n`.

These cluster near the endpoints and produce much slower growth of the Lebesgue constant (logarithmic in the standard asymptotic result). This is a major example of numerical algorithm design: the interpolation space is the same `P_n`, but the chosen sampling geometry changes stability dramatically.

For a general interval `[a,b]`, map the Chebyshev nodes affinely from `[-1,1]`.

## 9. Runge phenomenon

The classical Runge example demonstrates that increasing the degree of a global interpolating polynomial on equally spaced nodes can make the approximation worse near the endpoints instead of better. The problem is not lack of polynomial approximability; it is the instability of that interpolation process/node choice.

The lesson is therefore stronger than “higher degree is sometimes bad”:

- interpolation error is a combination of approximation power and interpolation stability;
- node placement is part of the numerical method;
- exact matching of all data points can be undesirable, especially with noisy measurements.

## 10. Why the course transitions to least squares

Global polynomial interpolation has two important limitations for data analysis:

1. high-degree interpolation can be numerically unstable and oscillatory;
2. experimental/noisy data should not necessarily be matched exactly.

Least squares instead chooses a lower-dimensional model and minimizes aggregate discrepancy. With more observations than parameters, it trades exact interpolation for a controlled best fit in a norm.

This transition connects function approximation back to the linear-algebra geometry developed earlier: design matrices, orthogonal projection, QR factorization and later the SVD pseudoinverse.

## 11. Interpolation versus regression: conceptual comparison

Interpolation:

- `n+1` independent conditions determine a degree-at-most-`n` polynomial;
- residual at each node is exactly zero;
- node placement strongly controls stability;
- exactness can amplify noise.

Least squares:

- typically has more data than parameters;
- residuals are nonzero but minimized in aggregate;
- model complexity can be chosen independently of the number of samples;
- QR/SVD provide stable linear-algebra solutions.

Neither is universally superior; they answer different mathematical modeling questions.

## 12. Deep-understanding checkpoint

You should be able to formulate polynomial interpolation as `Ga=y`; prove/recall uniqueness for distinct nodes; construct the Lagrange basis and interpolant; define the interpolation error and Lebesgue constant; interpret the bound `(1+Lambda_n) * best-approximation error`; state what Weierstrass does and does not imply; explain why Chebyshev nodes are preferable to equally spaced nodes for high-degree global interpolation; explain the Runge phenomenon; and motivate the move from exact interpolation to least squares for noisy/overdetermined data.

## Sources

Primary: `Slides/Lecture1024-Approssimazione.pdf`, `Slides/Trascrizioni/21Lecture1031_1.txt` and the approximation part of `22Lecture1031_2.txt`. Least-squares continuation is in `knowledge/modules/05-approximation-and-least-squares.md` and Module 3.
