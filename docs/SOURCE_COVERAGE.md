# Source coverage audit

This document records how **every one of the 91 files** in the supplied `CLA.zip` contributes to the repository's study-complete semantic representation. The archive was content-inspected on 2026-09-11: PDFs were page/text parsed, notebooks were parsed by cell and section, text/code files were read, tabular data were schema/shape inspected, and the PageRank graph file structure was inspected.

`source/MANIFEST.tsv` (path: `sources/MANIFEST.tsv`) remains the byte-level SHA-256 ledger. This file records semantic coverage rather than replacing that integrity record.

## A. Della Santa teaching/laboratory material - 26 files

| Source | Content observed | Study representation |
|---|---|---|
| `Della Santa/CLA4LSPpyslides2223.pdf` | 65-page Python/Jupyter laboratory slide set: Python basics, OOP hints, conditions/loops, functions, modules/packages, Jupyter | Module 1 |
| `Della Santa/fifa19datastats.csv` | 18,147 rows x 39 columns; FIFA skill/statistics dataset used by homework-simulation/PCA workflow | Module 9 |
| `Della Santa/IntroPython.ipynb` | 19 cells; Python/Jupyter introduction, control flow, functions, imports, LaTeX, images, plotting, error messages | Module 1 |
| `Della Santa/intropython_module.py` | tiny import example defining `int_example` and `loaded_function_example` | Module 1 |
| `Della Santa/LinAlgebra.ipynb` | 66 cells; NumPy ndarrays, dimensions, dtypes, indexing/slicing, array creation/operations and linear algebra/sparse usage | Modules 0-1 |
| `Della Santa/PCA_CLA4LSPslides_2526.pdf` | 127-page current PCA course slide set | Module 9 |
| `Della Santa/PyLab01_basictools.ipynb` | 19 cells; determinant, Gaussian elimination, REF/RREF, tolerance, linear systems | Module 2 |
| `Della Santa/PyLab02_orthog.ipynb` | 27 cells; Gram-Schmidt, modified GS, Givens and Householder methods | Module 3 |
| `Della Santa/PyLab03_krylov.ipynb` | 17 cells; Krylov spaces, minimal polynomials, Arnoldi, modified Arnoldi, basic FOM | Module 6 |
| `Della Santa/PyLab04a_SklearnAndPandasIntro.ipynb` | 94 cells; pandas and scikit-learn interfaces, `StandardScaler`, PCA, k-means, Series/DataFrames | Modules 1 and 9 |
| `Della Santa/PyLab04b_PCA.ipynb` | 28 cells; Iris/Wine PCA, score/loading graphs, biplot, PC interpretation, k-means and centroid interpretation | Module 9 |
| `Della Santa/PyLab05_HWsimulation.ipynb` | 31 cells; simplified end-to-end PCA homework simulation, variance analysis, dimension reduction, interpretation/clustering | Module 9 |
| `Della Santa/requirements_cla4lsp.txt` | allowed lab environment: NumPy, SciPy, scikit-learn, pandas, Matplotlib (plus notebook environment dependencies) | Modules 1 and 9 assessment notes |
| `Della Santa/skillcategories.csv` | 34 rows x 2 columns; maps FIFA skills to semantic categories | Module 9 |
| `Della Santa/skilltypes.csv` | 34 rows x 2 columns; maps FIFA skills to types | Module 9 |
| `Della Santa/solPyLab01_basictools.ipynb` | 20-cell worked solution to Lab 01 | Module 2; implementation evidence |
| `Della Santa/solPyLab02_orthog.ipynb` | 27-cell worked orthogonalization solution | Module 3; implementation evidence |
| `Della Santa/solPyLab03_krylov.ipynb` | 17-cell worked Krylov/Arnoldi/FOM solution | Module 6; implementation evidence |
| `Della Santa/solPyLab04b_PCA.ipynb` | 27-cell worked PCA/k-means analysis with stored outputs/plots | Module 9; implementation evidence |
| `Della Santa/solPyLab05_HWsimulation_onlyoutputs_nocode_nocomments.pdf` | 23-page output-only solution artifact for Lab 05 simulation | Module 9; expected-result/visualization evidence |
| `Della Santa/testmatrices.py` | NumPy test matrices/systems used in numerical experiments | Module 2 and lab verification |
| `Della Santa/How PCA/HWpca_CLA4LSP_2526.pdf` | 11-page current PCA homework specification, rules, YPS data description and survey-question appendix | Module 9 and `docs/ASSESSMENT.md` |
| `Della Santa/How PCA/HWpca_Surname1_Surname2.ipynb` | 37-cell current student homework template: preprocessing, variance, PCs, reduction, interpretation, scores, clustering | Module 9 and assessment retrieval |
| `Della Santa/How PCA/columns_hw.csv` | 150 rows x 3 columns: original survey question, short name, data type | Module 9 |
| `Della Santa/How PCA/responses_hw.csv` | physical CSV is 674 rows x 151 columns because it includes an index-like `Unnamed: 0`; homework describes 150 survey variables (139 integer + 11 categorical) | Module 9 |
| `Della Santa/How PCA/test_SVD_vs_PCA.ipynb` | 21 cells; validates a custom SVD formulation against scikit-learn PCA after identical preprocessing | Modules 9 and 11 |

## B. Homework material - 3 files

| Source | Content observed | Study representation |
|---|---|---|
| `Homeworks/Homeworks.pdf` | 4-page 2025/26 homework overview: two mandatory projects (PageRank, PCA), one optional project, delivery/exam expectations; PageRank project instructions | Modules 9 and 12; assessment docs |
| `Homeworks/PageRank/googleFinalVersionFixed.pdf` | 11-page Bryan/Leise PageRank paper: stochastic link matrices, nonunique rankings, dangling nodes, modified matrix `M=(1-m)A+mS`, positivity/uniqueness, power computation and exercises | Module 12 |
| `Homeworks/PageRank/hollins.dat` | 29,888 lines. Header `6012 23875`; 6,012 node-ID/URL records followed by directed edge pairs representing 23,875 links | Module 12 |

## C. Supplied external/reference material - 6 files

These files deepen the course but do not override current official slides/homework instructions. Their course-relevant mathematical results have been integrated into the module notes rather than treating hundreds of reference pages as the first retrieval layer.

| Source | Content observed | Used for |
|---|---|---|
| `OtherMaterials/Cayley-Hamilton.pdf` | 10-page treatment of Cayley-Hamilton and Jordan normal form | eigenvalue foundations / polynomial viewpoint |
| `OtherMaterials/Jiang_SpectralClustering.pdf` | 16-page introduction to spectral graph theory and Laplacian/eigenvalue graph structure | Module 7 |
| `OtherMaterials/Luxburg06_SpectralClustering.pdf` | 26-page tutorial on spectral clustering, graph Laplacians, normalized/unnormalized algorithms and perturbation intuition | Module 7 |
| `OtherMaterials/Saad_IteratveMethods_2000.pdf` | 460-page *Iterative Methods for Sparse Linear Systems* reference | Modules 0, 4 and 6; deep reference for sparse/stationary/Krylov methods |
| `OtherMaterials/SHU_spectralClustering.pdf` | 12-page spectral-clustering/graph-Laplacian notes | Module 7 |
| `OtherMaterials/SpectralGraphTheory.pdf` | 30-page Spielman spectral graph theory chapter | Module 7 |

## D. Official/topic slide PDFs - 14 files

| Source | Pages | Coverage |
|---|---:|---|
| `Slides/Lecture0921-SparseMatrices.pdf` | 63 | Module 0: sparse matrices, storage and large-scale viewpoint |
| `Slides/Lecture1003-BasicTools.pdf` | 119 | Module 2: core linear algebra and direct-method tools |
| `Slides/Lecture1016-OrtProj.pdf` | 47 | Module 3: orthogonalization, projectors and least squares |
| `Slides/Lecture1019-Iterative.pdf` | 32 | Module 4: stationary iterative methods |
| `Slides/Lecture1024-Approssimazione.pdf` | 27 | Module 5: approximation/least squares |
| `Slides/Lecture1030-Krylov.pdf` | 56 | Module 6: Krylov/Arnoldi/projection methods |
| `Slides/Lecture1106-SpectralClustering.pdf` | 25 | Module 7: graph Laplacian/spectral clustering |
| `Slides/EigenValues/1 - Power Methods.pdf` | 36 | Module 8: eigenvalue foundations and power-type methods |
| `Slides/EigenValues/2 - Shifting, deflation.pdf` | 23 | Module 8: shifts and deflation |
| `Slides/EigenValues/3 - Gerschgorin circles.pdf` | 15 | Module 10: eigenvalue localization |
| `Slides/EigenValues/4 - Lanczos.pdf` | 14 | Module 10: symmetric Krylov/Lanczos |
| `Slides/EigenValues/5 - QR method for eigenvalues.pdf` | 20 | Module 10: QR eigenvalue iteration |
| `Slides/EigenValues/6 - Singular value decomposition.pdf` | 72 | Module 11: SVD, low-rank approximation, pseudoinverse/applications |
| `Slides/EigenValues/lab-deflation.pdf` | 1 | Module 8: deflation laboratory prompt |

**Extraction-quality note.** The eigenvalue slide decks contain substantial handwritten/annotated material, so machine text extraction is imperfect. Their mathematical content is cross-reconstructed in Modules 8, 10 and 11 using the corresponding lecture transcripts, which are considerably more verbose and searchable.

## E. Lecture transcripts - 42 files

All transcript files were read as text. They are speech-to-text evidence and can contain recognition errors for mathematical symbols/names; module notes use them to reconstruct motivation and lecture-specific explanations while official written sources control exact notation when available.

| Transcript | Main semantic routing |
|---|---|
| `01Lecture0924.txt` | sparse matrices / large-scale motivation - Module 0 |
| `02Lecture0926.txt` | sparse matrices and continuation - Module 0 |
| `03Lecture1001.txt` | Python/computational workflow - Module 1 |
| `04Lecture1003_1.txt` | basic linear algebra/direct methods - Module 2 |
| `05Lecture1003_2.txt` | basic tools continuation - Module 2 |
| `06Lecture1006.txt` | elimination/vector-space foundations - Module 2 |
| `07Lecture1008.txt` | direct-method/foundational continuation - Module 2 |
| `08Lecture1010_1.txt` | transition from foundational tools - Module 2 |
| `09Lecture1010_2.txt` | orthogonality/orthogonalization - Module 3 |
| `10Lecture1010_3.txt` | orthogonalization continuation - Module 3 |
| `11Lecture1013.txt` | Gram-Schmidt/Givens/Householder development - Module 3 |
| `12Lecture1015.txt` | orthogonal transformations/QR ideas - Module 3 |
| `13Lecture1017_1.txt` | projectors/least-squares foundations - Module 3 |
| `14Lecture1017_2.txt` | projectors/least squares continuation - Module 3 |
| `15Lecture1020_1.txt` | stationary iterative methods - Module 4 |
| `16Lecture1020_2.txt` | iterative convergence/stationary methods - Module 4 |
| `17Lecture1024_1.txt` | projection/least-squares bridge - Modules 3/5 |
| `18Lecture1024_2.txt` | stationary-iteration continuation - Module 4 |
| `19Lecture1027.txt` | iterative-method continuation/review - Module 4 |
| `20Lecture1029.txt` | iterative-method continuation/review - Module 4 |
| `21Lecture1031_1.txt` | approximation/regression/least squares - Module 5 |
| `22Lecture1031_2.txt` | approximation-to-Krylov transition - Modules 5/6 |
| `23Lecture1103.txt` | Krylov spaces/Arnoldi - Module 6 |
| `24Lecture1105.txt` | Arnoldi/FOM/Krylov continuation - Module 6 |
| `25Lecture1107.txt` | Krylov completion and spectral clustering - Modules 6/7 |
| `26Lecture1114.txt` | eigenvalue foundations/power method - Module 8 |
| `27Lecture1117.txt` | inverse/shifted methods - Module 8 |
| `28Lecture1119.txt` | shifts/deflation/eigenvalue methods - Module 8 |
| `29Lecture1121.txt` | PCA/statistics foundations - Module 9 |
| `30Lecture1124.txt` | PCA variance/covariance/principal directions - Module 9 |
| `31Lecture1126.txt` | PCA interpretation/dimensionality reduction - Module 9 |
| `32Lecture1128.txt` | PCA/k-means/data analysis - Module 9 |
| `33Lecture1201.txt` | PCA/clustering continuation - Module 9 |
| `34Lecture1203.txt` | PCA/k-means/project continuation - Module 9 |
| `35Lecture1205.txt` | Gershgorin/eigenvalue localization - Module 10 |
| `36Lecture1210.txt` | Lanczos/Rayleigh/extreme eigenvalues - Module 10 |
| `37Lecture1212.txt` | QR eigenvalue method - Module 10 |
| `38Lecture1215.txt` | QR finalization and introduction to singular values - Modules 10/11 |
| `39Lecture1217.txt` | SVD existence/properties - Module 11 |
| `40Lecture1219_1.txt` | computing SVD/Householder-based structure - Module 11 |
| `41Lecture1219_2.txt` | optimal low-rank approximation/compression - Module 11 |
| `42Lecture0107.txt` | final SVD details/applications and course closure - Module 11 |

## F. Coverage conclusion

Every file in the 91-file archive is now assigned one of three roles:

1. **direct course evidence** integrated into the corresponding `knowledge/modules/*.md` document;
2. **computational/data evidence** whose structure, intended use and algorithmic role is represented in the relevant module/lab index;
3. **supporting literature** whose course-relevant theory is integrated as secondary background.

For study questions, retrieve `memory/CORE.md` -> `docs/COURSE_MAP.md` -> the relevant `knowledge/modules/*.md` -> any higher-authority official/lab/transcript source identified above if an exact course-specific detail must be checked.
