# Assessment and homework map

Status: `verified` against the supplied 2025/2026 homework overview and lecture material.

## Overall format

The supplied course overview states:

- **2 mandatory homeworks**: a **PageRank** project and a **Principal Component Analysis** project.
- **1 non-mandatory homework/project** may be completed for additional evaluation.
- Work is performed in small groups according to the current homework instructions; use the current official PDF for the exact permitted group size and submission packaging.
- The exam centers on presenting the work and answering questions about its mathematical content. Code alone is not sufficient evidence of understanding.

Source priority for exact rules:

1. `Homeworks/Homeworks.pdf`
2. the current homework-specific specification, especially `Della Santa/How PCA/HWpca_CLA4LSP_2526.pdf`
3. relevant lecture transcript announcements

## Mandatory homework 1 — PageRank

Core mathematical ideas to be ready to explain:

- directed graph / hyperlink matrix representation;
- stochastic matrix interpretation;
- stationary distribution / dominant eigenvector viewpoint;
- existence/uniqueness issues and how the Google matrix construction addresses them;
- the iterative computation used and its convergence rationale;
- behavior on the supplied graph data.

Supplied project reference: `Homeworks/PageRank/googleFinalVersionFixed.pdf` (Bryan & Leise, *The $25,000,000,000 Eigenvector*), with `Homeworks/PageRank/hollins.dat` as data.

## Mandatory homework 2 — PCA

The PCA homework has its own current-year specification and template. Study the entire pipeline rather than only plotting results:

- data meaning and preprocessing;
- variance/covariance and feature scaling;
- principal components, scores, loadings and explained variance;
- dimensionality reduction and component interpretation;
- k-means in the reduced representation;
- internal/external cluster evaluation where requested;
- connection of PCA to eigendecomposition/SVD.

Primary sources include `Della Santa/PCA_CLA4LSPslides_2526.pdf`, `Della Santa/How PCA/HWpca_CLA4LSP_2526.pdf`, the PCA lab notebooks, and `PyLab05_HWsimulation.ipynb`.

## Non-mandatory project

Lecture announcements indicate that topics connected to course methods/applications can be proposed. Examples mentioned in the supplied material include spectral clustering and SVD/image-compression-style applications. Because optional-project rules may be instructor-dependent, verify the current official instructions before treating any example as automatically approved.

## Exam-preparation rule

For each submitted result, prepare four layers of explanation: **what was computed**, **why the mathematics justifies it**, **how the algorithm implements that mathematics**, and **what numerical/data assumptions could make the result misleading**. This mirrors the course emphasis on computational methods rather than black-box library use.
