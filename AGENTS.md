# Agent operating guide

This repository is the canonical knowledge base for **Computational Linear Algebra for Large Scale Problems** (Politecnico di Torino, A.Y. 2025/2026).

## Non-negotiable source policy

When answering a course question, reason from this repository first. Do not silently substitute generic textbook conventions when the course uses a specific notation, algorithm, stopping criterion, project rule or implementation workflow.

The repository now contains a **study-complete semantic transcription** of the 91-file supplied corpus under `knowledge/`, together with file-level provenance in `docs/SOURCE_COVERAGE.md` and SHA-256 identities in `sources/MANIFEST.tsv`.

Authority when statements conflict:

1. **Current official 2025/2026 course requirements and mathematical statements**, as reconstructed with provenance in the relevant `knowledge/modules/*.md` file and assessment/source-coverage documents.
2. **Current instructor laboratory/notebook material**, which controls the intended computational workflow and allowed packages.
3. **Lecture transcripts**, which are valuable explanatory evidence but can contain speech-to-text errors, especially mathematical symbols and names.
4. **Supplied external references**, used for deeper background and verification.
5. **Derived memory/navigation**, such as `memory/CORE.md` and high-level maps, which must never override a more specific source-backed statement.

The large original binaries are not all byte-for-byte mirrored in Git. Do not claim that a raw PDF/notebook is physically present when it is only represented semantically. `sources/INGESTION_STATUS.md` is authoritative about that boundary.

## Retrieval procedure

For every substantive course question:

1. Read `memory/CORE.md` to recover the whole-course conceptual spine.
2. Locate the topic in `docs/COURSE_MAP.md` and, when dependencies matter, `docs/CONCEPT_GRAPH.md`.
3. Read the corresponding detailed file under `knowledge/modules/`. This is the main searchable mathematical study layer.
4. Check the module's source list and `docs/SOURCE_COVERAGE.md` when a course-specific detail, lecture nuance, laboratory convention or source identity matters.
5. For implementation questions, also read `docs/LAB_INDEX.md` and use the notebook/source roles recorded there and in the module.
6. For PageRank/PCA/exam questions, always also read `docs/ASSESSMENT.md`; current project constraints must not be inferred from generic knowledge.
7. For multi-topic questions, follow prerequisite/application links rather than retrieving only the lexically closest topic.
8. Distinguish **course fact** (what this course teaches/requires) from **background fact** (standard theory used to explain it).

If an exact wording, equation transcription or administrative detail is not represented in the repository with enough certainty, say so rather than inventing it. The repository is study-complete semantically, not a claim that every source byte or every visual annotation has been reproduced verbatim.

## Explanation standard

Explanations must be mathematically explicit and self-contained. Every introduced object should be briefly defined: dimensions, assumptions, meaning and role. Never rely on a named concept without recalling what it means.

For an algorithm, state:

- the target problem;
- assumptions/structure exploited;
- initialization;
- iteration/update or factorization steps;
- stopping criterion where applicable;
- why the method is mathematically valid;
- convergence condition/rate at the level taught in the course;
- computational/storage cost at the level relevant to large-scale problems;
- numerical caveats;
- links to preceding/following course concepts.

For a proof, separate hypotheses, claim, key construction and conclusion. For code, connect each operation to the mathematical object it implements and check dimensions, residuals/reconstruction and tolerances.

## Memory model used in this repository

The repository separates five layers:

- **Integrity/provenance memory**: `sources/MANIFEST.tsv` and `docs/SOURCE_COVERAGE.md`, identifying all 91 original artifacts and their roles.
- **Semantic course memory**: `knowledge/modules/`, containing the detailed study reconstruction of the entire program.
- **Navigation/graph memory**: `docs/COURSE_MAP.md`, `docs/CONCEPT_GRAPH.md`, lecture/lab indexes and assessment routing.
- **Compact durable memory**: `memory/CORE.md`, which keeps only the global conceptual spine and must remain small.
- **Working memory**: the few files retrieved for the current question; it is not persisted unless a validated durable insight should be added to the repository.

New durable notes should include provenance (`source_paths` or source identities), status (`verified`, `needs-check`, or `derived`) and date. Never promote an unverified inference into `memory/CORE.md`.

## Repository invariants

- Every original source identity is tracked in `sources/MANIFEST.tsv`.
- `docs/SOURCE_COVERAGE.md` must account for all original files.
- Detailed mathematical coverage belongs in `knowledge/modules/`, not in `memory/CORE.md`.
- Derived notes must retain source provenance.
- Conflicts are resolved by authority, not by deleting evidence.
- Transcript recognition errors must not silently become formulas.
- Exact assessment rules are treated as time-sensitive course facts and checked against the current 2025/2026 assessment representation.
- Prefer meaningful headings/filenames and explicit terminology so GitHub lexical search remains effective.
