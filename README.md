# Computational Linear Algebra

Canonical study knowledge base for **Computational Linear Algebra for Large Scale Problems** (Politecnico di Torino, A.Y. 2025/2026).

The supplied course archive has been inspected file-by-file and reconstructed into a searchable, source-indexed semantic study corpus. The repository is designed both for a human studying the entire program and for an LLM agent that must recover the global context before answering a local question.

Successive strict depth audits compared the study corpus back against the official slides, labs and transcripts using a stronger standard than topic coverage. A fresh 91-file archive was rechecked on 2026-09-11; residual gaps found in that third pass were repaired in `knowledge/modules/` and `knowledge/depth/`. See `docs/DEEP_COVERAGE_AUDIT.md`.

## Start here

1. [`memory/CORE.md`](memory/CORE.md) — compact whole-course orientation.
2. [`knowledge/README.md`](knowledge/README.md) — entry point to the detailed study corpus.
3. [`knowledge/modules/`](knowledge/modules/) — 13 main modules containing definitions, formulas, algorithms, assumptions, convergence, numerical caveats and assessment links.
4. [`knowledge/depth/`](knowledge/depth/) — targeted supplements restoring source-specific details found missing by strict audits.
5. [`docs/DEEP_COVERAGE_AUDIT.md`](docs/DEEP_COVERAGE_AUDIT.md) — criteria, gaps, remediation and current deep-coverage verdict.
6. [`docs/COURSE_MAP.md`](docs/COURSE_MAP.md) and [`docs/CONCEPT_GRAPH.md`](docs/CONCEPT_GRAPH.md) — global curriculum, prerequisites and applications.
7. [`docs/SOURCE_COVERAGE.md`](docs/SOURCE_COVERAGE.md) — audit showing how every one of the 91 supplied files is represented.
8. [`docs/LECTURE_INDEX.md`](docs/LECTURE_INDEX.md) and [`docs/LAB_INDEX.md`](docs/LAB_INDEX.md) — lecture/notebook navigation.
9. [`docs/ASSESSMENT.md`](docs/ASSESSMENT.md) — PageRank/PCA projects and exam retrieval path.
10. [`AGENTS.md`](AGENTS.md) — mandatory retrieval/source-authority rules for AI agents.

## Course spine

The study corpus covers sparse matrices; Python/NumPy/SciPy tooling; linear-algebra foundations and Gaussian elimination/`PA=LU`; basis changes and similarity; orthogonalization, QR and projectors; polynomial interpolation, convergence and least squares; stationary iterative solvers; Krylov subspaces, Arnoldi, FOM and GMRES; spectral clustering; power/inverse-power methods, scalar shifts, the course's symmetric rank-one shifting and Householder deflation; PCA and k-means; Gershgorin localization and conditioning estimates; Lanczos/Ritz methods; QR eigenvalue iteration; SVD existence/uniqueness, bidiagonalization, optimal low-rank approximation and pseudoinverse; and the PageRank project. The current assessment material specifies PageRank and PCA as the two mandatory projects.

## What “complete” means here

The original `CLA.zip` contains **91 files (~161 MB)**. Every file has been content-inspected and is accounted for in [`docs/SOURCE_COVERAGE.md`](docs/SOURCE_COVERAGE.md); every original path, size and SHA-256 is retained in [`sources/MANIFEST.tsv`](sources/MANIFEST.tsv). The mathematical/program content needed to study the course has been semantically reconstructed in `knowledge/` rather than requiring the binary PDFs to be opened for ordinary study.

The strict audit checks more than coverage: it requires definitions/assumptions, derivations or justification, algorithm steps, convergence/existence/stability conditions, numerical caveats, computational implications and implementation/cross-topic links. After the remediation recorded in `docs/DEEP_COVERAGE_AUDIT.md`, the repository passes that standard for the taught program represented by the supplied corpus.

This is intentionally different from a byte-for-byte mirror. Large binary PDFs and raw datasets are not all duplicated in Git history. [`sources/INGESTION_STATUS.md`](sources/INGESTION_STATUS.md) records that distinction. A raw LFS mirror would improve archival completeness, but it is not required for ordinary study/retrieval.

The supplied `OtherMaterials/` references are deeper literature, including a full iterative-methods text and spectral-clustering papers. The repository integrates the parts needed for the taught program rather than reproducing every theorem/page of those secondary references verbatim.

## Source-of-truth model

Current official 2025/2026 course requirements and definitions have the highest authority; laboratory material controls the intended computational workflow; transcripts provide lecture explanation but may contain speech-to-text errors; supplied external references deepen theory. `knowledge/` is the searchable semantic reconstruction of those materials and always retains provenance back to source identities.

For an exact administrative/homework constraint, consult `docs/ASSESSMENT.md` and the source coverage entry. For a mathematical topic, start from the corresponding `knowledge/modules/*.md` file, then read the matching `knowledge/depth/*.md` supplement if one exists.

## Important limitation

No repository can guarantee understanding or a grade. This repository now contains sufficient material for deep study of the taught program, but mastery requires actively reproducing derivations, solving problems, implementing/debugging algorithms, interpreting numerical results and defending choices orally.

## Why this layout

The design uses hierarchical retrieval: global memory -> module map -> detailed semantic module -> targeted depth supplement -> source provenance. This keeps the whole course visible while avoiding the failure mode of retrieving one isolated chunk without its prerequisites or applications. See [`docs/KNOWLEDGE_ARCHITECTURE.md`](docs/KNOWLEDGE_ARCHITECTURE.md) and [`docs/RESEARCH_BASIS.md`](docs/RESEARCH_BASIS.md).
