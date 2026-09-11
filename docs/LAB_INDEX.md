# Laboratory and notebook index

This index maps the supplied notebooks to the mathematical ideas they implement. Notebooks are instructional evidence: use them to understand the course's computational workflow, but verify mathematical definitions against the official slides when precision matters.

| Notebook | Role | Mathematical/computational content |
|---|---|---|
| `Della Santa/IntroPython.ipynb` | Python prerequisite lab | Jupyter workflow, Python syntax, containers, functions and basic numerical programming |
| `Della Santa/LinAlgebra.ipynb` | NumPy/SciPy linear algebra | Arrays, shapes, indexing, matrix/vector operations, dense vs sparse representations, SciPy sparse matrices |
| `Della Santa/PyLab01_basictools.ipynb` | Basic linear algebra lab | Determinant, Gaussian elimination, REF/RREF, solving linear systems, tolerance/numerical issues |
| `Della Santa/solPyLab01_basictools.ipynb` | Lab 01 solution | Worked implementation of the Lab 01 tasks |
| `Della Santa/PyLab02_orthog.ipynb` | Orthogonalization lab | Classical/modified Gram–Schmidt, Givens rotations, Householder transformations, accuracy/performance comparisons |
| `Della Santa/solPyLab02_orthog.ipynb` | Lab 02 solution | Worked orthogonalization implementations and comparisons |
| `Della Santa/PyLab03_krylov.ipynb` | Krylov lab | Krylov spaces, minimal-polynomial experiments, Arnoldi, modified Arnoldi and a basic FOM implementation |
| `Della Santa/solPyLab03_krylov.ipynb` | Lab 03 solution | Worked Krylov/Arnoldi/FOM implementation |
| `Della Santa/PyLab04a_SklearnAndPandasIntro.ipynb` | Data-science tooling | pandas data handling; scikit-learn interfaces used later for PCA and clustering |
| `Della Santa/PyLab04b_PCA.ipynb` | PCA lab | PCA on toy/data examples, scores, loadings, explained variance, biplot-style interpretation, k-means connection |
| `Della Santa/solPyLab04b_PCA.ipynb` | PCA solution | Worked PCA/clustering analysis |
| `Della Santa/PyLab05_HWsimulation.ipynb` | PCA homework simulation | End-to-end FIFA19-style workflow: preprocessing, PCA, variance selection, reduced representation, k-means, internal/external evaluation |
| `Della Santa/How PCA/HWpca_Surname1_Surname2.ipynb` | Current PCA homework template | Student-facing structure for the mandatory PCA project |
| `Della Santa/How PCA/test_SVD_vs_PCA.ipynb` | PCA/SVD bridge | Numerical comparison of PCA and SVD formulations |

## Support files

- `Della Santa/testmatrices.py` provides matrices used in numerical experiments.
- `Della Santa/intropython_module.py` is a small Python support module.
- `Della Santa/fifa19datastats.csv`, `skillcategories.csv`, and `skilltypes.csv` support PCA/data-analysis exercises.
- `Della Santa/How PCA/responses_hw.csv` and `columns_hw.csv` belong to the current PCA homework data workflow.

## Retrieval rule

When a question is about **how the course implements** an algorithm, search the corresponding notebook and its solution. When it is about **why the algorithm is mathematically valid**, route from this index to `docs/COURSE_MAP.md` and then to the official slide/reference source.
