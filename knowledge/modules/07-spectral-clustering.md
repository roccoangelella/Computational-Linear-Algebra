# Module 7 - Spectral clustering and graph Laplacians

## 1. Clustering through a graph

Clustering aims to divide data into groups whose members are strongly related internally and weakly related across groups. Standard k-means works directly in the original Euclidean feature space and is naturally adapted to roughly convex/spherical clusters. Spectral clustering instead builds a graph encoding pairwise similarity and uses eigenvectors of a graph Laplacian to reveal structure before applying a conventional clustering method.

Primary course source: `Slides/Lecture1106-SpectralClustering.pdf` and the spectral-clustering part of `25Lecture1107.txt`. Supplied supporting references include `Luxburg06_SpectralClustering.pdf`, `Jiang_SpectralClustering.pdf`, `SHU_spectralClustering.pdf`, and `SpectralGraphTheory.pdf`.

## 2. Weighted graph representation

Let a dataset contain `n` objects. Construct a weighted undirected graph `G=(V,E)` with one vertex per object. A symmetric weight matrix

`W = (w_ij)`

encodes similarity. Large `w_ij` means objects `i` and `j` are strongly connected; zero can mean no graph edge.

Common constructions include:

- epsilon-neighborhood graphs;
- k-nearest-neighbor graphs;
- fully connected graphs with a rapidly decaying similarity such as a Gaussian kernel.

The graph-construction step is a modeling choice. Spectral clustering does not create information absent from the similarity graph.

## 3. Degree matrix

The weighted degree of vertex `i` is

`d_i = sum_j w_ij`.

Define the diagonal degree matrix

`D = diag(d_1,...,d_n)`.

For an unweighted graph, `d_i` is the usual number of incident edges. For a weighted graph it is the total connection strength.

## 4. Unnormalized graph Laplacian

The unnormalized Laplacian is

`L = D - W`.

It is symmetric when `W` is symmetric. For any vector `x`,

`x^T L x = 1/2 sum_{i,j} w_ij (x_i-x_j)^2 >= 0`.

Therefore `L` is positive semidefinite and all of its eigenvalues are nonnegative.

The constant vector `1` satisfies

`L 1 = 0`,

because `D1=W1`. Hence zero is always an eigenvalue.

## 5. Connected components and the zero eigenvalue

A fundamental theorem is that the multiplicity of eigenvalue zero of `L` equals the number of connected components of the graph. If the graph has `k` disconnected components, the null space of `L` is spanned by their indicator vectors.

This fact gives the idealized basis of spectral clustering: if the desired clusters were perfectly disconnected, the cluster structure would be encoded exactly by eigenvectors associated with eigenvalue zero.

When the components are only weakly connected, the eigenvectors associated with the smallest eigenvalues provide an approximate version of those indicator vectors.

## 6. Rayleigh quotient and smooth graph signals

For a nonzero vector `x`, the Rayleigh quotient of `L` is

`R_L(x)=x^T L x / x^T x`.

Since

`x^T L x = 1/2 sum_ij w_ij(x_i-x_j)^2`,

a small Rayleigh quotient means `x_i` and `x_j` tend to be similar when vertices `i,j` are strongly connected. Therefore eigenvectors corresponding to the smallest Laplacian eigenvalues are smooth over strong edges and can expose low-cut graph partitions.

## 7. The second eigenvector and two-way partitioning

For a connected graph, the smallest eigenvalue is `lambda_1=0` with eigenvector `1`. The second-smallest eigenvalue `lambda_2` is often called the algebraic connectivity, and an associated eigenvector is the **Fiedler vector**.

Its signs or relative values can be used to separate a graph into two groups. Intuitively, the Fiedler vector is the smoothest nonconstant direction on the graph and changes most significantly across weak connections.

The course uses this as a bridge between eigenvalue problems and combinatorial clustering.

## 8. Multiway spectral embedding

For `k` clusters, compute eigenvectors `u_1,...,u_k` associated with the `k` smallest relevant eigenvalues of the chosen Laplacian. Form

`U = [u_1,...,u_k] in R^{n x k}`.

Row `i` of `U` is now a `k`-dimensional representation of graph vertex `i`. Apply k-means to these row vectors.

The key idea is that the nonlinear/geometric cluster structure in the original space may become linearly separable or compact in the eigenvector embedding.

## 9. Normalized Laplacians

The supplied references discuss normalized variants, which account for unequal vertex degrees. Two standard choices are

`L_sym = I - D^{-1/2} W D^{-1/2}`

and

`L_rw = I - D^{-1}W`.

They are related but lead to different eigenvector normalizations and cut objectives. Degree normalization can prevent high-degree vertices from dominating purely because of scale.

When discussing a concrete algorithm, identify which Laplacian convention is being used instead of treating all forms as interchangeable.

## 10. Cut objectives

For a partition `A` and its complement, the cut weight is the total edge weight crossing the partition. Minimizing raw cut alone can favor tiny isolated sets. Normalized criteria such as RatioCut or normalized cut compensate for cluster size or volume.

Spectral clustering arises by relaxing a discrete combinatorial optimization into a continuous eigenvalue problem. The relaxed optimum is described by extremal eigenvectors of the Laplacian, after which a discrete grouping is recovered, typically with k-means.

This relaxation viewpoint is important: spectral clustering is not an arbitrary use of eigenvectors; the eigenproblem is the tractable continuous counterpart of a graph partition objective.

## 11. Relation to k-means

K-means minimizes within-cluster squared Euclidean distances to centroids:

`sum_{clusters C_l} sum_{i in C_l} ||z_i-mu_l||_2^2`.

In spectral clustering, k-means is usually not run on the original samples `x_i`, but on spectral coordinates `z_i` given by rows of the eigenvector matrix. This changes the geometry seen by k-means.

## 12. Computational considerations

For a large sparse graph, the Laplacian is sparse. Forming all eigenvectors densely would defeat the large-scale purpose. Only a small set of extremal eigenvectors is required, which motivates iterative eigenvalue methods such as Lanczos/Arnoldi.

Thus the module is also an application of the course's central computational principle: exploit sparsity and compute only the spectral information actually needed.

## 13. Practical spectral clustering pipeline

A typical pipeline is:

1. choose/construct the similarity matrix `W`;
2. compute degrees `D`;
3. build the chosen Laplacian;
4. compute the `k` eigenvectors associated with the relevant smallest eigenvalues;
5. create the spectral embedding from their rows;
6. normalize rows if required by the selected normalized algorithm;
7. apply k-means in the embedding;
8. map labels back to the original observations.

Hyperparameters include graph neighborhood rules, similarity scales and the desired number of clusters. These affect the graph before the eigensolver is even called.

## 14. What can go wrong

- A poor similarity graph can destroy cluster information.
- Too small a neighborhood can disconnect a graph unintentionally.
- Too large a neighborhood can blur separate clusters.
- The number of clusters may be ambiguous; an eigengap can be informative but is not universally decisive.
- Repeated/close eigenvalues can make individual eigenvectors nonunique even though the invariant subspace is meaningful.
- K-means introduces its own initialization/local-minimum issues.

## 15. Connection to later eigenvalue methods

Spectral clustering needs a few extremal eigenvectors of a large symmetric sparse matrix. This is precisely the setting in which Lanczos is useful. The theoretical graph material therefore motivates why the course next develops specialized eigenvalue algorithms instead of relying on a dense all-eigenvalues routine.

## 16. Exam checklist

Be able to define `W`, `D` and `L`; prove/interpret `x^TLx = 1/2 sum w_ij(x_i-x_j)^2`; explain why `L` is positive semidefinite; connect the multiplicity of zero to connected components; explain the Fiedler vector; describe the spectral embedding + k-means pipeline; and distinguish unnormalized from normalized Laplacian formulations.

## 17. Sources

- `Slides/Lecture1106-SpectralClustering.pdf`
- relevant part of `Slides/Trascrizioni/25Lecture1107.txt`
- `OtherMaterials/Luxburg06_SpectralClustering.pdf`
- `OtherMaterials/Jiang_SpectralClustering.pdf`
- `OtherMaterials/SHU_spectralClustering.pdf`
- `OtherMaterials/SpectralGraphTheory.pdf`
