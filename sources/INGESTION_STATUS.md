# Source ingestion status

Last updated: 2026-09-11

## Completed

- The supplied `CLA.zip` has been inventoried completely: **91 files**, about **161 MB** uncompressed.
- Every original archive path, byte size, detected type and SHA-256 digest is recorded in `sources/MANIFEST.tsv`.
- All 42 lecture transcripts have been mapped chronologically and semantically in `docs/LECTURE_INDEX.md`.
- All supplied notebooks/labs are mapped in `docs/LAB_INDEX.md`.
- Official slides, homework material, references and labs are routed by module in `docs/COURSE_MAP.md`.
- Source authority, conflict resolution and provenance rules are defined in `docs/SOURCE_POLICY.md`.

## Raw-byte mirror

The large binary source artifacts are **not yet byte-for-byte mirrored into this Git history**. Several PDFs are tens of megabytes (the SVD deck is about 44.6 MB), so ordinary Git blobs are the wrong ingestion path for the complete archive. `.gitattributes` configures PDF and DAT files for **Git LFS**.

A future byte mirror must preserve the original relative paths from `sources/MANIFEST.tsv` and verify each copied artifact against its recorded SHA-256. Until then, the manifest is the integrity/provenance ledger for the uploaded corpus, while `docs/` and `memory/` provide the navigational/semantic layer.

## Why this status is explicit

A source-of-truth repository should distinguish **material actually present in Git** from **material merely catalogued elsewhere**. Derived summaries must never create the appearance that a raw source was committed when it was not. This file makes that boundary auditable.
