# Concept clarification — Jacobi iteration vs. Jacobian conjecture

status: explained — learner verification pending
last-updated: 2026-10-08
source_paths:
- memory/2026-10-02_L16_step01_jacobi-method.md
- knowledge/modules/04-stationary-iterative-methods.md
external_references:
- https://www.treccani.it/enciclopedia/jacobi_%28Enciclopedia-della-Matematica%29/
- https://terrytao.wordpress.com/2026/07/21/a-digestion-of-the-jacobian-conjecture-counterexample/
- https://isa-afp.org/entries/Jacobian_Counterexample.html

clarification presented:
- Jacobi's stationary linear solver addresses Ax=b by computing all new components from the old iterate: x_i^(k+1)=(b_i-sum_{j!=i} a_ij x_j^(k))/a_ii.
- The Jacobian matrix of F=(f_1,...,f_n) is the n-by-n matrix of partial derivatives (partial f_i / partial x_j). This is NOT the iteration matrix of the Jacobi solver.
- Both the iterative method and the Jacobian determinant are named after Carl Gustav Jacob Jacobi; they are not the same mathematical construction.
- The Jacobian conjecture asked whether a polynomial map in n complex variables with nonzero constant Jacobian determinant must have a polynomial inverse (a local-to-global assertion).
- In July 2026 Levent Alpoege announced an explicit 3-dimensional counterexample developed with Claude Fable. Tao analyzed it, and Isabelle/HOL independently verified the constant determinant and collision of distinct input points. This refutes the conjecture for n >= 3; the 2-dimensional case remains open as of 2026-10-08.
- Distinguish discovery/disproof from mere AI-generated unverified claims; a computer-checked proof independently supports the result.

mastery note:
- Cross-topic question answered; do not infer independent mastery or mark original Jacobi derivation verified. No new algorithm step was completed.
