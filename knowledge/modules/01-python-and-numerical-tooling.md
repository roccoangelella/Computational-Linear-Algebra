# Module 1 - Python and numerical tooling

## 1. Purpose of the computational layer

The course uses Python not as a separate programming subject but as the environment in which the linear-algebra algorithms are inspected, implemented and tested. The main stack in the supplied material is NumPy, SciPy, scikit-learn, pandas and Matplotlib. The file `Della Santa/requirements_cla4lsp.txt` lists these packages.

Primary sources: `Della Santa/CLA4LSPpyslides2223.pdf`, `IntroPython.ipynb`, `LinAlgebra.ipynb`, `intropython_module.py`, and lecture `03Lecture1001.txt`.

## 2. Jupyter notebooks

A Jupyter notebook is an ordered sequence of Markdown cells and executable code cells. Execution state matters: a cell can refer to variables created earlier, and running cells out of order can produce results that do not correspond to the visible top-to-bottom code. For reproducible numerical work, the safest habit is to keep the notebook executable from a fresh kernel in logical order.

Markdown cells are used for mathematical explanations and LaTeX. Code cells are used for experiments, implementations and visualizations. Error messages and array shapes are part of the debugging process rather than something to ignore.

## 3. Core Python mechanics used by the course

The introductory material reviews variables, numeric types, strings, lists/tuples/dictionaries, conditions, loops and functions. A function packages an operation with explicit inputs and return values. Modules allow code to be reused; `intropython_module.py`, for example, defines a variable and a simple imported function.

A key programming distinction is between Python containers and numerical arrays. Lists are general-purpose Python objects; NumPy arrays have a homogeneous `dtype`, a fixed multidimensional shape and vectorized numerical operations.

## 4. NumPy arrays

An `ndarray` is characterized by properties such as:

- `shape`: the length of each axis;
- `ndim`: number of axes;
- `size`: total number of entries;
- `dtype`: numerical representation of the entries.

For a matrix-like array `A` of shape `(m,n)`, `A[i,j]` selects one entry, `A[i,:]` a row and `A[:,j]` a column. Python indexing starts at zero. Slicing uses half-open intervals: `a[p:q]` includes indices `p,...,q-1`.

The distinction between a vector of shape `(n,)` and a column array of shape `(n,1)` is computationally important. NumPy broadcasting rules can make expressions execute even when the intended linear-algebra dimensions are different, so shapes should be checked explicitly.

## 5. Vectorized operations and matrix multiplication

Elementwise multiplication is not matrix multiplication. In NumPy, `A * B` multiplies compatible arrays entrywise, whereas `A @ B` performs matrix multiplication. Similarly, `A.T` is the transpose view for real arrays.

Vectorization means expressing operations through array primitives instead of explicit Python loops when possible. It usually produces clearer mathematical code and moves the heavy arithmetic into optimized compiled libraries.

## 6. Dense linear-algebra routines

NumPy/SciPy provide routines for norms, determinants, linear systems, eigenvalue problems and factorizations. These routines are useful both as computational tools and as references against which student implementations can be compared.

A crucial methodological point in the labs is that calling a library function and implementing an algorithm answer different questions. The implementation exercises expose the mathematical steps and numerical issues; library routines show how a mature numerical package should be used in practice.

## 7. Floating-point arithmetic and tolerances

Computers represent most real numbers approximately. Consequently, a value that is mathematically zero may be stored as a small nonzero floating-point number. Code such as `x == 0` is therefore often inappropriate for results obtained through arithmetic.

The labs use tolerance-based decisions: treat a value as numerically zero when its magnitude is below a scale-appropriate threshold. This becomes essential in Gaussian elimination, rank decisions, orthogonalization breakdown tests and iterative stopping criteria.

The underlying principle is that numerical algorithms solve a floating-point approximation to the exact mathematical problem. Correct code must distinguish exact algebraic identities from finite-precision tests.

## 8. Sparse arrays in SciPy

SciPy supplies sparse matrix classes such as COO, CSR and CSC. The important computational rule is to keep sparse problems sparse. Matrix-vector products and many sparse operations should be performed directly on sparse objects rather than after conversion to a dense array.

The difference can be enormous: a dense `n x n` array requires storage proportional to `n^2`, while a sparse representation is proportional to the number of nonzeros plus indexing overhead.

## 9. pandas and scikit-learn

The later PCA laboratories add two tools.

A **pandas DataFrame** is a labeled two-dimensional table. Its columns represent variables/features and rows represent observations. DataFrames make it possible to select columns by name, inspect data types, handle missing or categorical data and keep semantic labels attached to numerical data.

**scikit-learn** uses a consistent estimator interface. A model object is configured, then fitted to data, and subsequently used to transform or predict. In the course this pattern is used for `StandardScaler`, `PCA` and `KMeans`.

The distinction between `fit`, `transform` and `fit_transform` should be understood:

- `fit` estimates parameters from the supplied data;
- `transform` applies an already fitted transformation;
- `fit_transform` performs both in one call.

## 10. Standardization

For a feature `x_j`, standardization typically maps

`x_ij -> (x_ij - mean_j)/std_j`.

This gives approximately zero mean and unit variance to each standardized feature. It is not a neutral cosmetic operation: PCA and distance-based clustering depend on scale. Without standardization, a variable with a large numerical variance can dominate even if that dominance comes only from its units.

Whether to standardize is therefore part of the mathematical modeling decision.

## 11. Reproducibility and random data

Several labs generate random matrices or use algorithms with randomized initialization. A random seed fixes the pseudo-random sequence, making an experiment reproducible. When comparing implementations, use the same inputs and, when relevant, the same initialization.

## 12. Practical debugging checklist

For numerical code, inspect:

1. array shapes before multiplication;
2. `dtype`, especially accidental integer arrays;
3. whether an operation is elementwise or algebraic;
4. residuals and reconstruction errors rather than only printed solutions;
5. tolerances used in zero/rank/convergence tests;
6. whether a sparse object was accidentally densified;
7. whether a notebook was executed in a reproducible order.

## 13. Source map

- `Della Santa/CLA4LSPpyslides2223.pdf`: extended Python laboratory slides.
- `Della Santa/IntroPython.ipynb`: syntax, functions, modules, LaTeX, plots and error handling.
- `Della Santa/LinAlgebra.ipynb`: NumPy arrays and linear algebra, including sparse structures.
- `Della Santa/intropython_module.py`: tiny module-import example.
- `Della Santa/requirements_cla4lsp.txt`: package environment.
- `Della Santa/PyLab04a_SklearnAndPandasIntro.ipynb`: pandas/scikit-learn layer used for PCA and clustering.
