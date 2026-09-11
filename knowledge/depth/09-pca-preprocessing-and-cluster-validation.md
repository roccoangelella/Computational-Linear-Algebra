# Depth supplement 9 - PCA preprocessing and k-means cluster validation

This supplement expands `knowledge/modules/09-pca-and-kmeans.md` with preprocessing and clustering-validation details from the current PCA slides/labs.

## 1. Preprocessing is part of the mathematical model

PCA and k-means are not invariant to arbitrary feature scaling. Before computing either method, determine what each feature represents and whether its numerical scale should influence distances/variance.

### Centering

PCA requires centering around feature means:

`X_c = X - 1 mu^T`.

Without centering, the first directions can reflect displacement from the origin rather than variation around the empirical mean.

### Standardization

Standard scaling transforms a numeric feature approximately as

`z_ij=(x_ij-mu_j)/s_j`.

Then each standardized feature has comparable variance scale. PCA on standardized variables is equivalent, up to conventions, to performing PCA using the sample correlation matrix rather than the raw covariance matrix.

This is appropriate when units differ or when one does not want high-variance measurement units to dominate automatically.

### Min-max and other scaling choices

A min-max transformation maps a feature to a chosen interval, commonly `[0,1]`. Unlike standardization it does not force unit variance and can respond differently to outliers. Scaling is therefore not a purely cosmetic library choice: it changes the geometry seen by PCA and k-means.

### Categorical variables

Categorical survey variables must be encoded before numerical algorithms can operate. The encoding should reflect whether categories are nominal or ordered. Assigning arbitrary integers to nominal categories can create artificial Euclidean distances/orderings, so the representation choice must be justified in the project.

## 2. PCA as an optimal linear representation

For centered data and a chosen dimension `r`, PCA selects an `r`-dimensional orthonormal subspace maximizing retained variance. Equivalently, via the SVD/Eckart-Young connection, its orthogonal rank-`r` reconstruction minimizes squared/Frobenius reconstruction error among rank-`r` linear representations.

These two viewpoints - maximum variance and minimum reconstruction error - explain why PCA is a principled linear dimensionality-reduction method rather than a visual heuristic.

## 3. k-means geometry and limitations

K-means assigns each point to the nearest centroid in Euclidean distance. The induced partition is a Voronoi tessellation: each cluster region is formed from points closest to one centroid.

Consequences:

- k-means is naturally suited to compact, roughly convex groups under Euclidean geometry;
- it can perform poorly for concave, ring-shaped or other shape-defined clusters;
- feature scaling directly changes the distances and therefore the partition;
- a low objective value does not by itself prove that clusters are meaningful for the application.

This is why spectral clustering appears elsewhere in the course: it changes the geometry before conventional clustering.

## 4. External versus internal evaluation

**External evaluation** compares clusters with known labels or external information. Agreement may be informative, but disagreement is not automatically failure: clustering seeks similarity structure, which need not coincide with a pre-existing label taxonomy.

**Internal evaluation** judges only the geometry of the produced clusters, typically rewarding small within-cluster dispersion and large between-cluster separation. Internal scores are diagnostics, not proofs of semantic usefulness.

## 5. Inertia

For clusters `S_i` with centroids `w_i`, inertia is

`I = sum_i sum_{x in S_i} ||x-w_i||_2^2`.

This is exactly the k-means objective. It is nonincreasing as `k` grows, because more centroids can always reproduce or improve a previous partition. Therefore the smallest inertia alone cannot select `k`: the trivial limit of many clusters would always look better by this metric.

The elbow heuristic looks for a point where additional clusters yield diminishing reductions, but this can be ambiguous.

## 6. Davies-Bouldin index

Let

`d_i = average_{x in S_i} ||x-w_i||_2`

measure within-cluster spread. For each cluster `i`, compare it with the most similar/least-separated other cluster through

`R_ij = (d_i+d_j)/||w_i-w_j||_2`.

The Davies-Bouldin index is

`DB = (1/k) sum_i max_{j != i} R_ij`.

Small `DB` is preferred: it corresponds to compact clusters whose centroids are well separated relative to their within-cluster radii.

Like every internal score, it depends on the chosen distance geometry and does not guarantee application-level meaning.

## 7. Silhouette coefficient

For a sample `x` belonging to cluster `S_i`, define

`a(x)` = average distance from `x` to the other points in its own cluster,

and

`b(x)` = minimum, over all other clusters `S_j`, of the average distance from `x` to points in `S_j`.

The silhouette coefficient is

`s(x) = (b(x)-a(x))/max(a(x),b(x))`.

It lies in `[-1,1]`:

- near `1`: the point is much closer to its own cluster than to alternatives;
- near `0`: it lies near a boundary/ambiguous region;
- negative: another cluster is, on average, closer than its assigned cluster.

An overall score is the average of `s(x)` across samples.

## 8. Computational cost of silhouette

A direct silhouette calculation requires pairwise distances among many/all observations. For `N` samples there are `N(N-1)/2` unordered pairs, so silhouette evaluation can be substantially more expensive than inertia or simpler centroid-based indices.

This matters for large datasets: an evaluation metric is itself an algorithm with a cost.

## 9. Choosing k

One course strategy is:

1. choose a candidate set `K={k_1,...,k_M}`;
2. run k-means for each candidate, preferably with controlled/repeated initialization;
3. compute the mean silhouette coefficient;
4. identify candidates with high average silhouette;
5. combine this evidence with interpretability, external constraints and domain meaning.

Formally, a silhouette-only choice would be

`k* = argmax_{k in K} (1/N) sum_x s_k(x)`.

But the homework's interpretation goal means a numerically best score can be rejected if it produces a useless or unstable segmentation.

## 10. Validation across PCA dimensions

When clustering is performed after PCA, two model choices interact:

- number of retained principal components `r`;
- number of clusters `k`.

A defensible workflow checks whether cluster conclusions are stable and interpretable under reasonable nearby choices. Very low-dimensional PCA can improve interpretability but may discard low-variance directions that are discriminative for clustering.

Therefore “PCA retains most variance” and “k-means finds good clusters” are logically separate claims and should be evaluated separately.

## 11. Deep-understanding checkpoint

Be able to distinguish centering, standardization and min-max scaling; explain PCA on covariance versus correlation; justify categorical encoding; derive the k-means inertia objective; explain Voronoi/convex-cluster limitations; distinguish external/internal validation; compute and interpret Davies-Bouldin and silhouette scores; explain silhouette's pairwise-distance cost; and justify `r` and `k` using both quantitative and interpretive evidence.

## Sources

Primary: `Della Santa/PCA_CLA4LSPslides_2526.pdf`, `PyLab04a_SklearnAndPandasIntro.ipynb`, `PyLab04b_PCA.ipynb`, `PyLab05_HWsimulation.ipynb`, current PCA homework specification/template, and transcripts `29Lecture1121.txt` through `34Lecture1203.txt`.
