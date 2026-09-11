# Module 12 - PageRank project

## 1. Assessment role

PageRank is one of the two mandatory course homeworks. The current `Homeworks/Homeworks.pdf` asks students to read the supplied PageRank paper, choose and solve two exercises, implement the algorithm, test it on the two small graphs in the paper and on the supplied dataset, and write a report containing a mathematically sound algorithm description, results, and the exercise solutions.

The homework guidance explicitly rewards implementing the algorithm with basic data structures and being able to explain the mathematics, although correct use of libraries is still acceptable.

Primary sources: `Homeworks/Homeworks.pdf`, `Homeworks/PageRank/googleFinalVersionFixed.pdf`, `Homeworks/PageRank/hollins.dat`, plus the eigenvalue/power-method material in Module 8.

## 2. Web graph and link matrix

Represent `n` web pages as vertices of a directed graph. A directed edge `j -> i` means page `j` links to page `i`.

Let `d_j` be the number of outgoing links from page `j`. For a page with `d_j>0`, define a link matrix `A` by

`A_ij = 1/d_j` if page `j` links to page `i`,

and `A_ij=0` otherwise.

Thus column `j` distributes one unit of importance equally among the pages linked from page `j`.

If every page has at least one outgoing link, each column sums to one. Such a matrix is **column-stochastic**:

`A_ij >= 0`, and `sum_i A_ij = 1` for every `j`.

## 3. Why eigenvalue 1 appears

Let `e` be the all-ones vector. For a column-stochastic matrix,

`e^T A = e^T`.

Thus `1` is an eigenvalue of `A^T`, and since a matrix and its transpose have the same eigenvalues, `1` is an eigenvalue of `A`.

A ranking vector `q` is sought such that

`Aq=q`,

with nonnegative entries and normalization

`sum_i q_i=1`.

The entry `q_i` is interpreted as the long-run importance/probability associated with page `i`.

## 4. The recursive ranking idea

The model embodies the principle that a page is important if it is linked by important pages. Each page transfers its current importance to its outgoing neighbors. At stationarity, the ranking is unchanged by another transfer:

`q=Aq`.

This self-consistency is exactly an eigenvector equation.

## 5. Why the raw link matrix can be problematic

Two main structural problems are highlighted in the supplied paper.

### Non-unique rankings / reducibility

A web can decompose into disconnected or closed subgraphs. Then eigenvalue `1` can have an eigenspace of dimension greater than one, so the ranking is not unique and can depend on the starting distribution.

### Dangling nodes

A **dangling node** is a page with no outgoing links. Its column in the raw link matrix is all zeros, so the matrix becomes **column-substochastic** rather than column-stochastic. Eigenvalue `1` and conservation of probability are no longer guaranteed in the same way.

A complete practical PageRank implementation must specify how dangling columns are repaired, commonly by replacing each dangling column with a probability distribution such as the uniform vector.

## 6. Teleportation / modified link matrix

For a web with no dangling nodes, the supplied Bryan-Leise paper defines

`M = (1-m) A + m S`,

where every entry of `S` is `1/n`, and reports the common choice

`m=0.15`.

Equivalently, using the more common damping notation `alpha=1-m`,

`M = alpha A + (1-alpha) S`,

with `alpha=0.85`.

`S` represents a random jump to any page. The modification makes all entries of `M` positive when `m>0`, while preserving column stochasticity if `A` is column-stochastic.

## 7. Personalized teleportation

The uniform matrix can be generalized. Let `v` be a probability vector with positive/nonnegative components summing to one. A personalized Google matrix can be written

`G = alpha P + (1-alpha) v e^T`,

where `P` is a repaired column-stochastic link matrix. Each column of `v e^T` equals `v`.

The stationary PageRank vector satisfies

`q = Gq`.

Since `e^Tq=1`, this is equivalently

`q = alpha Pq + (1-alpha)v`.

Uniform PageRank corresponds to `v=(1/n)e`.

## 8. Positivity and uniqueness

The supplied paper proves the important result that a **positive** column-stochastic matrix has a unique normalized positive eigenvector associated with eigenvalue `1`.

Teleportation is therefore not merely a heuristic tie breaker. It changes the matrix so the stationary ranking has strong existence/uniqueness properties. This is closely related to Perron-Frobenius theory for positive/nonnegative matrices.

## 9. Power iteration for PageRank

Because PageRank is the eigenvector associated with dominant eigenvalue `1`, it can be computed with power iteration:

`q^(k+1) = G q^(k)`.

Start from any probability vector `q^(0)`. Because `G` is column-stochastic, probability normalization is preserved in exact arithmetic:

`e^T q^(k)=1`.

For a positive stochastic matrix, the iterates converge to the unique stationary PageRank vector under the standard conditions.

The computation is attractive at web scale because it uses repeated sparse matrix-vector products and does not require a dense eigendecomposition.

## 10. Convergence and damping

The supplied paper explains that non-dominant eigenvalues of the modified matrix are bounded in magnitude by the damping factor in the standard construction. With `alpha=0.85`, a representative asymptotic contraction factor is at most approximately `0.85` for the nonstationary part under the stated setting.

The damping parameter creates a tradeoff:

- `alpha` close to 1 follows the hyperlink structure more strongly but can converge more slowly and be more sensitive to graph structure;
- smaller `alpha` gives stronger teleportation and generally faster mixing but makes the ranking less determined by the links.

## 11. Stopping criteria

A practical power iteration can stop when, for example,

`||q^(k+1)-q^(k)||_1 <= tol`,

or when the eigen-residual

`||Gq^(k)-q^(k)||`

is sufficiently small.

The 1-norm is natural for probability distributions because it measures total absolute mass discrepancy. A maximum iteration count should also be included.

## 12. Efficient sparse implementation

Do not build the dense teleportation matrix `S` or `v e^T`. Use

`q^(k+1) = alpha Pq^(k) + (1-alpha)v`.

The expensive operation is the sparse product `Pq`. If the web graph has `E` links, this can be implemented in `O(E)` work per iteration using adjacency/out-degree data.

This is the computational-linear-algebra lesson of the project: formulate a mathematically global eigenvector problem in a way that requires only local sparse graph operations.

## 13. Basic-data-structure implementation

To obtain the strongest educational value requested by the homework, one can store for each source page the list of outgoing targets and its out-degree. To compute `y=Pq`:

1. initialize `y=0`;
2. for each page `j` with out-degree `d_j`, add `q_j/d_j` to `y_i` for every outgoing target `i`;
3. handle dangling mass according to the chosen repair rule;
4. apply damping/teleportation.

This avoids constructing even a sparse matrix object and makes the probability-flow interpretation explicit.

## 14. The supplied Hollins dataset format

`Homeworks/PageRank/hollins.dat` begins with

`6012 23875`.

The first number indicates **6012 pages/nodes** and the second **23875 links/edges**. The next 6012 lines map integer node identifiers to URLs. After those URL records, the remaining lines are pairs such as

`1 2`, `8 2`, `16 2`, ...

representing directed links according to the dataset's source/target convention.

When implementing the parser, determine and document the edge orientation from the file/paper/example and keep it consistent with the column-stochastic convention. A transpose mistake changes the ranking problem.

## 15. Validation on small graphs

Before running the large dataset, reproduce the two graph examples in the supplied paper. Small examples allow the matrix to be written explicitly and checked by hand.

Validate:

- column sums after link normalization/repair;
- nonnegativity;
- PageRank normalization `sum_i q_i approximately 1`;
- residual `||Gq-q||`;
- agreement between the iterative implementation and a small direct eigensolver used only as a verification tool.

A project implementation should be trusted because these invariants are checked, not because it produced a vector without errors.

## 16. Exercises and report

The current general homework sheet asks for **two exercises of your choice** from the PageRank paper. The report must include their solutions and be ready for mathematical defense.

The report should clearly separate:

1. graph/matrix construction;
2. treatment of dangling nodes;
3. damping/teleportation convention;
4. iterative algorithm and stopping rule;
5. verification on the paper's small graphs;
6. results on `hollins.dat`;
7. interpretation of top-ranked pages;
8. selected exercise solutions.

Do not hide a convention inside code: the direction of links, stochastic normalization and damping formula belong in the mathematical description.

## 17. Random-surfer interpretation

PageRank also has a Markov-chain interpretation. At each step, a random surfer either follows a hyperlink according to the link probabilities (probability `alpha`) or teleports according to `v` (probability `1-alpha`). The PageRank vector is the stationary probability distribution.

This interpretation explains why entries sum to one and why teleportation prevents the surfer from becoming trapped in closed parts of the web.

## 18. Relation to the rest of the course

PageRank integrates several course themes:

- sparse graph matrices from Module 0;
- stochastic matrices and eigenvectors;
- power iteration from Module 8;
- spectral convergence controlled by subdominant eigenvalues;
- residual-based stopping;
- large-scale computation via sparse matrix-vector products.

It is therefore a compact application demonstrating why the course develops iterative spectral algorithms.

## 19. Exam/project checklist

Be able to construct the link matrix from a graph; define column stochasticity; prove eigenvalue 1 exists for a stochastic matrix; explain nonuniqueness/dangling nodes; derive the damped matrix; explain why positivity produces a unique positive stationary vector; implement power iteration without forming a dense teleportation matrix; explain convergence qualitatively through the subdominant spectrum; parse/validate the supplied dataset; and defend the mathematical choices in the report.

## 20. Sources

- `Homeworks/Homeworks.pdf`
- `Homeworks/PageRank/googleFinalVersionFixed.pdf`
- `Homeworks/PageRank/hollins.dat`
- Module 8 / power method sources
