# Module 9 - Principal Component Analysis and k-means

## 1. Goal of PCA

Principal Component Analysis (PCA) replaces a set of possibly correlated variables by orthogonal directions chosen to capture as much variance as possible. It serves two linked purposes:

1. **dimensionality reduction**: represent observations with fewer coordinates;
2. **interpretation**: identify directions that summarize dominant patterns in the data.

The course treats PCA both mathematically and computationally, and it is one of the two mandatory projects.

Primary sources: `Della Santa/PCA_CLA4LSPslides_2526.pdf`; transcripts `29Lecture1121.txt` through `34Lecture1203.txt`; `PyLab04a_SklearnAndPandasIntro.ipynb`, `PyLab04b_PCA.ipynb`, its solution, `PyLab05_HWsimulation.ipynb`, the current homework document/template and `test_SVD_vs_PCA.ipynb`.

## 2. Data matrix and centering

Let `X in R^{m x n}` contain `m` observations (rows) and `n` features (columns). For feature `j`, let

`mu_j = (1/m) sum_i X_ij`.

The centered data matrix is

`X_c = X - 1 mu^T`,

meaning each feature mean is subtracted from that column. PCA is fundamentally a method about variation around the mean, so centering is essential.

If features have very different physical units or scales, the course also considers standardization:

`Z_ij = (X_ij-mu_j)/s_j`,

where `s_j` is a standard deviation estimate. PCA on standardized data is effectively driven by correlations rather than raw variances.

## 3. Variance and covariance

For centered data, the sample covariance matrix can be written, up to the convention `m` versus `m-1`, as

`C = (1/(m-1)) X_c^T X_c`.

`C` is symmetric positive semidefinite. Its diagonal entries are feature variances and its off-diagonal entries are covariances.

The covariance between two features measures whether they tend to move together. Correlation is the scale-normalized version of covariance.

Because `C` is symmetric, it has an orthonormal eigenbasis and nonnegative eigenvalues.

## 4. First principal component as maximum-variance direction

Consider a unit direction `v`, `||v||_2=1`. Projecting centered observations onto `v` gives the score vector

`t = X_c v`.

Its variance is proportional to

`v^T C v`.

The direction maximizing this quantity under `||v||_2=1` is an eigenvector of `C` corresponding to its largest eigenvalue. Therefore the first principal component direction solves

`max_{||v||=1} v^T C v = lambda_1`.

The second principal component maximizes variance subject to being orthogonal to the first, and so on. Consequently PCA is an eigenvalue problem.

## 5. Principal directions, loadings and scores

Let

`C v_j = lambda_j v_j`,

with eigenvalues sorted

`lambda_1 >= lambda_2 >= ... >= lambda_n >= 0`.

The eigenvectors `v_j` are the principal directions. In common data-analysis language, their coefficients are called **loadings** because they describe how strongly each original feature contributes to a component.

Collect the first `r` directions in

`V_r=[v_1,...,v_r]`.

The reduced coordinates or **scores** are

`T_r = X_c V_r`.

Each row of `T_r` represents one observation in principal-component coordinates.

## 6. Explained variance

The eigenvalue `lambda_j` equals the variance captured by principal component `j` under the covariance convention used. The explained-variance ratio is

`EVR_j = lambda_j / sum_i lambda_i`.

The cumulative explained variance after `r` components is

`CEV_r = sum_{j=1}^r EVR_j`.

A common dimensionality-reduction rule chooses the smallest `r` reaching a desired cumulative threshold. However, the current homework explicitly emphasizes that the business/problem interpretation may deliberately favor **very low dimension** over retaining nearly all information. Therefore component selection is not a purely mechanical percentage rule.

## 7. Reconstruction

Using `r` components, centered data are approximated by

`X_c approximately T_r V_r^T = X_c V_r V_r^T`.

To return to the original coordinates, add the mean vector back. The matrix `V_r V_r^T` is the orthogonal projector onto the retained principal subspace.

As `r` grows, reconstruction error cannot increase. The SVD module explains why this approximation is optimal in a precise low-rank sense.

## 8. PCA and SVD

If the centered data have singular value decomposition

`X_c = U Sigma V^T`,

then

`X_c^T X_c = V Sigma^2 V^T`.

Therefore the PCA directions are the right singular vectors of `X_c`, and the covariance eigenvalues are

`lambda_j = sigma_j^2/(m-1)`

under the sample-covariance convention.

The score matrix satisfies

`X_c V = U Sigma`.

The supplied `test_SVD_vs_PCA.ipynb` numerically validates the equivalence between a custom SVD route and scikit-learn PCA, accounting for the usual sign ambiguity of singular/eigenvectors.

## 9. Sign ambiguity

If `v` is an eigenvector, so is `-v`. Thus PCA implementations may produce principal directions with opposite signs while representing exactly the same component. Scores flip sign at the same time. Comparisons between implementations should therefore compare subspaces, absolute correlations, reconstruction, or allow sign alignment rather than declaring a sign-flipped component incorrect.

## 10. Interpreting components

A principal component is not automatically semantically meaningful. Interpretation comes from inspecting its loadings:

- large positive coefficients identify features that increase together along the component;
- large negative coefficients identify features varying in the opposite direction;
- coefficients near zero contribute little to that direction.

The PCA labs ask students to assign descriptive names to components by examining these loading patterns. This is a modeling/interpretation step, not an eigenvalue computation.

## 11. Score plots, loading plots and biplots

A **score plot** visualizes observations in coordinates such as PC1/PC2. It is useful for identifying separation, trends and outliers.

A **loading plot** visualizes feature coefficients in the selected principal directions.

A **biplot** overlays both observation scores and feature directions, helping relate group separation to original variables. Scaling conventions matter when interpreting a biplot, so axes and vector normalization should be identified explicitly.

## 12. k-means

After dimensionality reduction, the course applies k-means to find groups of observations. Given points `z_i` and `k` clusters, k-means minimizes the within-cluster sum of squared distances

`J = sum_{l=1}^k sum_{i in C_l} ||z_i-mu_l||_2^2`,

where `mu_l` is the centroid of cluster `C_l`.

The standard alternating procedure is:

1. initialize `k` centroids;
2. assign each point to its nearest centroid;
3. recompute each centroid as the mean of its assigned points;
4. repeat until assignments/centroids stabilize according to a tolerance.

Each step does not increase `J`, but the algorithm can converge to a local rather than global minimum. Initialization and multiple restarts therefore matter.

## 13. Clustering in PCA coordinates

PCA and k-means solve different problems. PCA maximizes retained variance; k-means minimizes within-cluster Euclidean dispersion. PCA can remove noisy/redundant dimensions and create a compact representation, but maximum variance is not guaranteed to be the same as maximum cluster separation.

Therefore one should compare/interpret clustering quality rather than assume PCA automatically improves every clustering task.

## 14. Cluster interpretation

The PCA lab uses centroids to characterize clusters. A centroid in principal-component coordinates indicates the typical component scores for that group. Because the PCs have been interpreted through their loadings, centroid positions can be translated into qualitative profiles.

If cluster labels external to k-means exist, one can also evaluate agreement with those labels. If no external truth exists, internal measures based on compactness/separation are appropriate.

## 15. pandas/scikit-learn workflow

`PyLab04a` introduces:

- DataFrame construction and labeled columns;
- feature selection/manipulation;
- `StandardScaler` for standardization;
- `PCA` objects and their attributes such as components/explained variance;
- `KMeans` and the estimator `fit`/`transform`/`predict` pattern.

The conceptual rule is to understand the mathematics behind each object rather than treating the library call as the algorithm's explanation.

## 16. Current PCA homework dataset

The current homework uses the **Young-People-Survey (YPS)** dataset. The supplied homework document states:

- `responses_hw.csv` contains **674 observations and 150 variables**;
- the variables include **139 integer** and **11 categorical** variables;
- the data are already cleansed;
- `columns_hw.csv` maps original survey questions to shortened column names and records data type.

The survey questions are grouped into eight categories:

1. music preferences - 19 items;
2. movie preferences - 12 items;
3. hobbies and interests - 32 items;
4. phobias - 10 items;
5. health habits - 3 items;
6. personality traits, views on life and opinions - 57 items;
7. spending habits - 7 items;
8. demographics - 10 items.

The document also groups them more broadly as entertainment, personality and demographic questions.

## 17. Current PCA homework task

The assignment requires using PCA to reduce dimensionality and then k-means to identify meaningful groups/profiles of people if such structure exists. The framing is a company attempting to summarize customer survey information into a few understandable concepts for decision making. The assignment explicitly says the chosen number of PCs may be intentionally very low, prioritizing dimensionality reduction and interpretability over preserving nearly all variance.

The notebook template structures the work around:

- categorical encoding and preprocessing;
- comparing feature variances before/after preprocessing;
- computing all PCs and cumulative explained variance;
- choosing a reduced number of PCs;
- interpreting each selected component from loadings;
- score-graph visualization;
- clustering with k-means;
- interpreting/evaluating the resulting clusters.

Exact word limits and template instructions should be checked in `HWpca_Surname1_Surname2.ipynb` when preparing the deliverable.

## 18. Current PCA homework rules

From `HWpca_CLA4LSP_2526.pdf`:

- teams may contain at most two people;
- report score depends on both report content and individual defense performance;
- the report must be a PDF print/export of the homework notebook, showing code and text;
- only Python packages used in the laboratories / listed in the course requirements are allowed;
- submission is a single zip per group containing only the notebook and PDF report;
- at the defense, the team presents from the complete report PDF rather than a separate slide deck and must be ready to explain the theory behind the methods;
- the stated presentation duration is 10 minutes followed by discussion/questions.

When assessment rules matter, the official current homework PDF overrides summaries.

## 19. FIFA19 simulation material

`PyLab05_HWsimulation.ipynb` and the supplied output-only solution PDF simulate an end-to-end homework-style workflow using `fifa19datastats.csv`, supported by `skillcategories.csv` and `skilltypes.csv`. The FIFA dataset has 18,147 rows and 39 columns in the supplied corpus. The lab is useful for learning how to move from feature analysis through PCA to clustering and interpretation before attempting the graded YPS project.

## 20. Exam/project checklist

Be able to derive PCA from a variance-maximization/Rayleigh-quotient problem; connect PCA to covariance eigenvectors and SVD; define scores/loadings/explained variance; explain centering versus standardization; derive reduced reconstruction; interpret signs/loadings; formulate k-means and explain local minima; and defend every preprocessing/component-selection/clustering choice in the homework rather than presenting it as an unexplained library default.

## 21. Sources

- `Della Santa/PCA_CLA4LSPslides_2526.pdf`
- `Slides/Trascrizioni/29Lecture1121.txt` through `34Lecture1203.txt`
- `Della Santa/PyLab04a_SklearnAndPandasIntro.ipynb`
- `Della Santa/PyLab04b_PCA.ipynb`
- `Della Santa/solPyLab04b_PCA.ipynb`
- `Della Santa/PyLab05_HWsimulation.ipynb`
- `Della Santa/solPyLab05_HWsimulation_onlyoutputs_nocode_nocomments.pdf`
- `Della Santa/How PCA/HWpca_CLA4LSP_2526.pdf`
- `Della Santa/How PCA/HWpca_Surname1_Surname2.ipynb`
- `Della Santa/How PCA/responses_hw.csv`
- `Della Santa/How PCA/columns_hw.csv`
- `Della Santa/How PCA/test_SVD_vs_PCA.ipynb`
- `Della Santa/fifa19datastats.csv`, `skillcategories.csv`, `skilltypes.csv`
