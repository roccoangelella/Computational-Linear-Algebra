# Assessment and homework map

Status: **verified against the supplied 2025/2026 homework overview and current PCA homework specification**.

## Overall format

The supplied `Homeworks/Homeworks.pdf` states:

- **2 mandatory homeworks**: **PageRank** and **Principal Component Analysis (PCA)**;
- **1 non-mandatory homework/project** is available;
- work is done in groups of **1 or 2 people** in the general homework overview, with homework-specific instructions taking precedence if more specific;
- deliverables include the reports and the code used to produce the results;
- the exam requires presenting the work and answering questions about its **mathematical content**.

The course therefore evaluates both computational results and the ability to justify the mathematics behind them.

For exact rules, authority is:

1. current homework-specific specification, where present;
2. `Homeworks/Homeworks.pdf`;
3. current lecture announcements represented in the transcript/source map.

## Mandatory homework 1 - PageRank

The current general homework sheet asks students to:

1. read `Homeworks/PageRank/googleFinalVersionFixed.pdf` to understand PageRank;
2. solve **two exercises of their choice** from the paper;
3. write code implementing the algorithm;
4. test the code on the two graphs in the paper (Figures 2.1 and 2.2);
5. test the code on the supplied `hollins.dat` dataset;
6. write a report containing a mathematically sound description of the algorithm, results, and the solutions of the two selected exercises.

The sheet explicitly says that implementing the algorithms yourselves with basic data structures is the strongest route to a good grade, while correct library use can still receive a good evaluation. Students must know and be able to explain the mathematics in PageRank.

### PageRank theory to defend

Be prepared to explain:

- graph orientation and hyperlink/link-matrix construction;
- column-stochastic matrices and why eigenvalue `1` appears;
- the stationary/dominant eigenvector interpretation;
- non-unique rankings/reducibility;
- dangling nodes and how the implementation repairs them;
- damping/teleportation, including the supplied paper's `M=(1-m)A+mS` formulation (`m=0.15` is the reported standard example, equivalent to damping `alpha=0.85`);
- positivity/uniqueness rationale;
- power iteration and convergence/stopping criteria;
- sparse implementation and validation on small graphs;
- interpretation of the results on the supplied dataset.

Detailed study: `knowledge/modules/12-pagerank-project.md`.

### Hollins dataset

`hollins.dat` begins with `6012 23875`: 6,012 page/node records and 23,875 directed links. The first 6,012 following records map IDs to URLs; the remainder contains edge pairs. The report/code should document the chosen source/target convention explicitly so the stochastic matrix is not accidentally transposed.

## Mandatory homework 2 - PCA

The current dedicated specification is `Della Santa/How PCA/HWpca_CLA4LSP_2526.pdf`, with template `HWpca_Surname1_Surname2.ipynb`.

### Current PCA administrative rules

The supplied 2025/2026 specification states:

- teams contain **at most 2 people**;
- team members can receive different scores because the final assignment score depends on both report content and individual defense performance;
- team members are expected to take the exam in the same call, with the stated exception that a member who fails/rejects the mark can take a later call while retaining the same report;
- the report must be the **PDF print/export of the notebook**, showing both code and text;
- only Python modules/packages used in the laboratories, i.e. those allowed by the supplied requirements environment, may be used;
- figures and tables in the exported PDF must be clear/readable;
- one zip is submitted per group containing **only** the Jupyter notebook and PDF report;
- submission is through the course's assignment-delivery area and follows the official filename convention;
- the submission deadline is the date of the official exam call at which the team intends to take the exam;
- for the discussion, the team brings a PC with code ready if needed and the report PDF;
- the stated presentation time is **10 minutes**, followed by teacher questions involving the underlying theory;
- the team comments directly on the complete report PDF, without running code, support slides or a separate summary presentation during the normal presentation.

If any procedural rule is needed for an actual future exam date, re-check the current official course page because administrative rules can change after the supplied corpus.

### Current PCA dataset

The homework uses the Young-People-Survey (YPS). The specification describes **674 observations and 150 survey variables**, of which **139 are integer and 11 categorical**; the dataset is already cleansed. The physical CSV in the supplied archive has 151 columns because it also contains an index-like `Unnamed: 0` column.

Survey categories:

1. Music preferences - 19 items
2. Movie preferences - 12 items
3. Hobbies & interests - 32 items
4. Phobias - 10 items
5. Health habits - 3 items
6. Personality traits, views on life and opinions - 57 items
7. Spending habits - 7 items
8. Demographics - 10 items

`columns_hw.csv` maps original questions to shortened names and data types.

### PCA task

The assignment asks students to use PCA to reduce dimensionality and then k-means to identify meaningful groups/profiles if present. The scenario is deliberately interpretation-oriented: summarize many customer/survey variables into a few understandable concepts. The specification explicitly notes that the selected number of PCs may be **very low**, prioritizing dimensionality reduction/interpretability over preserving nearly all information.

The template covers:

- categorical encoding and preprocessing;
- feature variances and effects of preprocessing;
- computation of all PCs and cumulative explained variance;
- selection of a reduced number of PCs;
- loading-based interpretation/naming of PCs;
- score visualization;
- k-means clustering and cluster interpretation/evaluation.

Detailed study: `knowledge/modules/09-pca-and-kmeans.md`.

### PCA theory to defend

Be prepared to derive/explain:

- mean, variance, covariance and correlation;
- centering versus standardization and why scale matters;
- PCA as maximizing projected variance / covariance eigenvectors;
- scores and loadings;
- explained/cumulative explained variance;
- reduced reconstruction/projector interpretation;
- PCA-SVD equivalence and sign ambiguity;
- k-means objective/alternating updates/local minima;
- why every preprocessing, number-of-PCs and number-of-clusters choice is justified for the data rather than merely a library default.

## Non-mandatory homework/project

The general homework sheet offers two broad routes:

- solve at least **10 additional exercises** from the PageRank paper and be ready to justify them; or
- choose a topic involving implementation of algorithms seen during the semester, with a report containing the mathematical problem description, obtained results and produced code, followed by mathematical questioning.

Specific topic approval remains instructor-dependent.

## Exam-preparation rule

For each result in either project, prepare four layers of explanation:

1. **what** was computed;
2. **why** the mathematics justifies it;
3. **how** the algorithm/code implements that mathematics;
4. **which numerical/data assumptions or failure modes** could make the result misleading.

Use the corresponding `knowledge/modules/*.md` file as the theory checklist, then connect each statement to your own code/output.
