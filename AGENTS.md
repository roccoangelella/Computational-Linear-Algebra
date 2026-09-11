# Agent operating guide

This repository is the canonical knowledge base for **Computational Linear Algebra for Large Scale Problems** (Politecnico di Torino, A.Y. 2025/2026).

## Non-negotiable source policy

When answering questions about the course, reason from this repository first and cite repository paths. Do not silently substitute generic textbook conventions when the course uses a specific definition, notation, algorithm, stopping criterion, or homework rule.

Authority order when sources disagree:

1. `sources/official/` — official 2025/2026 slides, homework specifications, and instructor material.
2. `sources/labs/` — instructor notebooks and supplied code for the current course.
3. `sources/transcripts/` — lecture transcripts. They have excellent coverage but may contain speech-to-text errors, especially names and mathematical symbols.
4. `sources/references/` — supplementary literature supplied with the course.
5. `docs/` and `memory/` — derived navigation and synthesis. These help retrieval but never overrule a higher-authority source.

If a formula or theorem appears only in a transcript, verify it against a slide/notebook/reference whenever possible. If verification is impossible, explicitly mark the statement as transcript-derived.

## Retrieval procedure

For every substantive course question:

1. Read `memory/CORE.md` for the global map and terminology.
2. Locate the topic in `docs/COURSE_MAP.md` and `docs/CONCEPT_GRAPH.md`.
3. Search the relevant official source/lab/transcript paths listed there.
4. For multi-topic questions, follow prerequisite and application links in `docs/CONCEPT_GRAPH.md`; do not retrieve only the lexically closest file.
5. For exam/homework questions, also read `docs/ASSESSMENT.md` and the corresponding official homework source.
6. Distinguish **course fact** (what is taught/required) from **background fact** (standard theory used to explain it).

## Explanation standard

Explanations must be mathematically explicit and self-contained. Every introduced object should be briefly defined: dimensions, assumptions, meaning, and role. For algorithms, state the target problem, assumptions, iteration/update, stopping criterion, convergence idea, computational cost at the level relevant to the course, and numerical caveats. For proofs, separate hypotheses, claim, key construction, and conclusion. For code, connect each operation to the mathematical object it implements.

Do not assume that a named theorem or algorithm is already understood merely because it was mentioned earlier. Briefly recall what it says and why it is being used.

## Memory model used in this repository

The repository deliberately separates four memory layers:

- **Source memory**: immutable course artifacts and normalized extracts under `sources/`.
- **Semantic memory**: stable concepts, prerequisites, and relationships under `docs/`.
- **Episodic/study memory**: durable discoveries, misconceptions, solved patterns, and corrections under `memory/`.
- **Working memory**: the small set of files retrieved for the current question; it is not persisted unless the information is validated and useful beyond one interaction.

New durable notes should include provenance (`source_paths`), status (`verified`, `needs-check`, or `derived`), and last-updated date. Never promote an unverified inference into `memory/CORE.md`.

## Repository invariants

- Original source paths and SHA-256 hashes are tracked in `sources/MANIFEST.tsv`.
- Derived notes must point back to source paths.
- Duplicate or conflicting statements are not resolved by deletion; record the conflict and identify the higher-authority source.
- Keep `memory/CORE.md` compact. Put detail in topic/module documents and link to it.
- Prefer one concept per section and meaningful filenames so lexical GitHub search remains effective.
