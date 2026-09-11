# Agent operating guide

This repository is the canonical knowledge base for **Computational Linear Algebra for Large Scale Problems** (Politecnico di Torino, A.Y. 2025/2026).

## Non-negotiable source policy

When answering questions about the course, reason from this repository first and cite repository paths. Do not silently substitute generic textbook conventions when the course uses a specific definition, notation, algorithm, stopping criterion, or homework rule. A concrete example is Module 8: the course calls `A-lambda xx^T` **shifting** and teaches a separate Householder similarity/dimension-reduction procedure as **deflation**, even though external texts may use different terminology.

Authority order when sources disagree:

1. current official course/homework material represented and indexed by the repository;
2. instructor notebooks/labs and supplied code;
3. lecture transcripts, which have excellent coverage but may contain speech-to-text errors, especially names and mathematical symbols;
4. supplied external references;
5. derived `knowledge/`, `docs/` and `memory/` layers, which accelerate retrieval but never silently overrule higher-authority evidence.

If a formula or theorem is supported only by transcript evidence, cross-check it against a written course source/reference when possible. If verification is impossible, explicitly mark it as transcript-derived.

## Retrieval procedure

For every substantive course question:

1. Read `memory/CORE.md` for global orientation when the topic/prerequisites are not already active in context.
2. Locate the topic in `docs/COURSE_MAP.md` and `docs/CONCEPT_GRAPH.md`.
3. Read the corresponding `knowledge/modules/*.md` document.
4. Check `knowledge/depth/README.md`; if that module has a supplement, read the supplement before constructing a deep answer.
5. For multi-topic questions, follow prerequisite/application links rather than retrieving only the lexically closest file.
6. For exam/homework questions, also read `docs/ASSESSMENT.md` and the relevant module/project material.
7. If an exact course-specific statement is ambiguous or high stakes, follow provenance through `docs/SOURCE_COVERAGE.md` to the highest-authority source identity.
8. Distinguish **course fact** (what is taught/required) from **background fact** (standard theory used to explain it).

`docs/DEEP_COVERAGE_AUDIT.md` records the successive strict completeness audits, the residual gaps found by the fresh-archive third pass, and why the depth supplements exist.

## Explanation standard

Explanations must be mathematically explicit and self-contained. Every introduced object should be briefly defined: dimensions, assumptions, meaning and role. For algorithms, state the target problem, assumptions, iteration/update, stopping criterion, convergence idea, computational cost at the level relevant to the course, and numerical caveats. For proofs, separate hypotheses, claim, key construction and conclusion. For code, connect each operation to the mathematical object it implements.

Do not assume that a named theorem or algorithm is already understood merely because it was mentioned earlier. Briefly recall what it says and why it is being used.

A deep answer should normally make the following distinctions explicit when relevant:

- exact mathematics versus floating-point implementation;
- residual versus forward error;
- existence/uniqueness versus conditioning;
- convergence guarantee versus convergence speed;
- dense complexity versus sparse/structured cost;
- abstract linear map/subspace versus its coordinates/matrix representation;
- theorem hypotheses versus informal rules of thumb.

## Memory model used in this repository

The repository deliberately separates four memory layers:

- **Source memory**: provenance of the supplied course artifacts under `sources/` and `docs/SOURCE_COVERAGE.md`.
- **Semantic memory**: stable concepts, modules, prerequisites and relationships under `knowledge/` and `docs/`.
- **Episodic/study memory**: durable discoveries, misconceptions, solved patterns and corrections under `memory/`.
- **Working memory**: the small set of files retrieved for the current question; it is not persisted unless validated and useful beyond one interaction.

New durable notes should include provenance (`source_paths`), status (`verified`, `needs-check`, or `derived`) and last-updated date. Never promote an unverified inference into `memory/CORE.md`.

## Repository invariants

- Original source paths and SHA-256 hashes are tracked in `sources/MANIFEST.tsv`.
- Every supplied source has a semantic routing entry in `docs/SOURCE_COVERAGE.md`.
- Derived notes must preserve source provenance.
- Duplicate or conflicting statements are not resolved by deletion; record the conflict and identify the higher-authority source.
- Keep `memory/CORE.md` compact. Put detail in modules/depth documents and link to it.
- Prefer one concept per section and meaningful filenames so lexical GitHub search remains effective.
- Do not claim that the repository can guarantee mastery: it can provide sufficient course material, but mastery requires derivation, exercises, implementation and oral explanation by the learner.
