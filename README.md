# Computational Linear Algebra

Canonical study knowledge base for **Computational Linear Algebra for Large Scale Problems** (Politecnico di Torino, A.Y. 2025/2026).

The supplied course archive has been inspected file-by-file and reconstructed into a searchable, source-indexed semantic study corpus. The repository is designed both for a human studying the entire program and for an LLM agent that must recover the global context before answering a local question.

## Start here

1. [`memory/CORE.md`](memory/CORE.md) — compact whole-course orientation.
2. [`knowledge/README.md`](knowledge/README.md) — entry point to the detailed study-complete transcription.
3. [`knowledge/modules/`](knowledge/modules/) — 13 self-contained modules containing definitions, formulas, algorithms, assumptions, convergence, numerical caveats and assessment links.
4. [`docs/COURSE_MAP.md`](docs/COURSE_MAP.md) — global curriculum and source routing.
5. [`docs/CONCEPT_GRAPH.md`](docs/CONCEPT_GRAPH.md) — prerequisite/application relationships and transcript aliases.
6. [`docs/SOURCE_COVERAGE.md`](docs/SOURCE_COVERAGE.md) — audit showing how every one of the 91 supplied files is represented.
7. [`docs/LECTURE_INDEX.md`](docs/LECTURE_INDEX.md) and [`docs/LAB_INDEX.md`](docs/LAB_INDEX.md) — lecture/notebook navigation.
8. [`docs/ASSESSMENT.md`](docs/ASSESSMENT.md) — PageRank/PCA projects and exam retrieval path.
9. [`AGENTS.md`](AGENTS.md) — mandatory retrieval/source-authority rules for AI agents.

## Course spine

The study corpus covers sparse matrices; Python/NumPy/SciPy tooling; linear-algebra foundations and Gaussian elimination; orthogonalization, QR ideas and projectors; least squares and approximation; stationary iterative solvers; Krylov subspaces, Arnoldi, FOM and GMRES; spectral clustering; power/inverse-power, shifts and deflation; PCA and k-means; Gershgorin localization; Lanczos; QR eigenvalue iteration; SVD, optimal low-rank approximation and pseudoinverse; and the PageRank project. The current assessment material specifies PageRank and PCA as the two mandatory projects.

## What “complete” means here

The original `CLA.zip` contains **91 files (~161 MB)**. Every file has been content-inspected and is accounted for in [`docs/SOURCE_COVERAGE.md`](docs/SOURCE_COVERAGE.md); every original path, size and SHA-256 is retained in [`sources/MANIFEST.tsv`](sources/MANIFEST.tsv). The mathematical/program content needed to study the course has been semantically reconstructed in `knowledge/` rather than requiring the binary PDFs to be opened for ordinary study.

This is intentionally different from a byte-for-byte mirror. Large binary PDFs and raw datasets are not all duplicated in Git history. [`sources/INGESTION_STATUS.md`](sources/INGESTION_STATUS.md) records that distinction. A raw LFS mirror would improve archival completeness, but it is no longer a prerequisite for using this repository as the study source of truth.

## Source-of-truth model

Current official 2025/2026 course requirements and definitions have the highest authority; laboratory material controls the intended computational workflow; transcripts provide lecture explanation but may contain speech-to-text errors; supplied external references deepen theory. `knowledge/` is the searchable semantic transcription of those materials and always retains provenance back to source identities.

For an exact administrative/homework constraint, consult `docs/ASSESSMENT.md` and the source coverage entry. For a mathematical topic, start from the corresponding `knowledge/modules/*.md` file and follow its provenance links when necessary.

## Why this layout

The design uses hierarchical retrieval: global memory -> module map -> detailed semantic module -> source provenance. This keeps the entire course visible while avoiding the failure mode of retrieving one isolated chunk without its prerequisites or applications. See [`docs/KNOWLEDGE_ARCHITECTURE.md`](docs/KNOWLEDGE_ARCHITECTURE.md) and [`docs/RESEARCH_BASIS.md`](docs/RESEARCH_BASIS.md).
