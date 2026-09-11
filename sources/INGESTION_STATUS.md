# Source ingestion status

Last updated: 2026-09-11

## Study/semantic ingestion: COMPLETE

The supplied `CLA.zip` has been processed as a course knowledge corpus rather than only inventoried.

Completed work:

- **91/91 files** inventoried and content-inspected.
- Every original path, byte size, type and SHA-256 is recorded in `sources/MANIFEST.tsv`.
- Every file is semantically accounted for in `docs/SOURCE_COVERAGE.md`.
- All 42 lecture transcripts were read and routed chronologically/conceptually.
- All 14 notebooks were parsed by cells/sections and mapped to their mathematical/implementation role.
- All 26 PDFs were text/page inspected; handwritten eigenvalue slide decks were cross-reconstructed using the matching lecture transcripts because raw machine extraction of handwriting is imperfect.
- CSV/DAT/code support files were inspected for schema, dimensions, format and course use. In particular, the current YPS homework data and Hollins PageRank graph structure are represented in the relevant modules.
- The entire taught program is reconstructed into 13 detailed documents under `knowledge/modules/`, covering definitions, formulas, algorithms, assumptions, convergence ideas, numerical caveats, implementation logic and assessment connections.
- `knowledge/README.md` is the entry point to this detailed corpus.

For **ordinary study of the complete program**, the repository is now self-contained at the semantic level: an agent should not need to open the original binary PDFs simply to explain a topic from the syllabus.

## Raw-byte archive mirror: NOT COMPLETE

The repository still does **not** claim that every original binary/source byte is physically duplicated in Git history. The supplied archive is about 161 MB and contains large PDFs (the SVD slide deck alone is about 44.6 MB) and large raw datasets. `.gitattributes` is configured for Git LFS should a byte-for-byte archival mirror be desired.

This distinction is deliberate:

- **semantic completeness** means the full course/program can be studied and retrieved from the repository;
- **archival completeness** means every original file is also stored byte-for-byte.

The first is complete. The second remains optional/outstanding.

## Representation rules

- Course-specific current rules/definitions are preserved in the detailed module/assessment representations with source provenance.
- Lecture transcripts are explanatory evidence and may contain speech-to-text errors; mathematical notation is cross-checked against written sources/standard structure when reconstructing the modules.
- Large supporting literature is integrated as course-relevant theory rather than dumped verbatim as hundreds of pages of reference text.
- Large datasets are represented by their structure, meaning and use; their original hashes remain in the manifest.
- If an exact visual annotation, exact source wording or raw-data reproduction becomes necessary, the original archive identity can be recovered from `sources/MANIFEST.tsv` and `docs/SOURCE_COVERAGE.md`.

## Retrieval consequence

The normal retrieval path is now:

`memory/CORE.md` -> `knowledge/modules/...` -> `docs/SOURCE_COVERAGE.md` / lecture-lab-assessment indexes.

A raw-byte LFS mirror is not required for ordinary course explanations, derivations or exam preparation.
