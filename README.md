# Computational Linear Algebra

Canonical study knowledge base for **Computational Linear Algebra for Large Scale Problems** (Politecnico di Torino, A.Y. 2025/2026).

The repository is organized for two audiences at once: a human studying for the exam and an LLM agent that must retrieve the right evidence without losing the global structure of the course.

## Start here

1. [`memory/CORE.md`](memory/CORE.md) — compact whole-course orientation.
2. [`docs/COURSE_MAP.md`](docs/COURSE_MAP.md) — complete module map and source routing.
3. [`docs/CONCEPT_GRAPH.md`](docs/CONCEPT_GRAPH.md) — prerequisites, applications, and transcript search aliases.
4. [`docs/LECTURE_INDEX.md`](docs/LECTURE_INDEX.md) — chronological map of all 42 transcript files.
5. [`docs/ASSESSMENT.md`](docs/ASSESSMENT.md) — PageRank/PCA projects and exam retrieval path.
6. [`AGENTS.md`](AGENTS.md) — mandatory retrieval/source-authority rules for AI agents.

## Course spine

The supplied corpus covers sparse matrices; Python/NumPy/SciPy tooling; linear-algebra foundations and Gaussian elimination; orthogonalization and projectors; least squares; stationary iterative solvers; Krylov/Arnoldi/FOM/GMRES ideas; spectral clustering; power/inverse-power, shifts and deflation; PCA and k-means; Gershgorin localization; Lanczos; QR eigenvalue iteration; and SVD with low-rank approximation and pseudoinverse applications. The two mandatory projects in the current material are PageRank and PCA.

## Source-of-truth model

Course evidence and derived memory are deliberately separated. Current official 2025/2026 material outranks lab notes, which outrank transcripts for exact formulas, while supplied external references provide background. Derived files in `docs/` and `memory/` are navigation/synthesis and must never silently override the evidence. See [`docs/SOURCE_POLICY.md`](docs/SOURCE_POLICY.md).

The integrity ledger [`sources/MANIFEST.tsv`](sources/MANIFEST.tsv) records all 91 files from the supplied `CLA.zip` with byte sizes and SHA-256 hashes. Raw binary mirroring should preserve those hashes; normalized extracts must be labeled as representations rather than byte-identical originals.

## Why this layout

The design combines ideas from hierarchical retrieval, graph-based retrieval, hybrid lexical/semantic search, and modern agent-memory evaluations. It intentionally remains plain-file and version-controlled so GitHub itself stays inspectable and auditable. See [`docs/KNOWLEDGE_ARCHITECTURE.md`](docs/KNOWLEDGE_ARCHITECTURE.md) and [`docs/RESEARCH_BASIS.md`](docs/RESEARCH_BASIS.md).
