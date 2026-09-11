# Source policy and provenance

## Purpose

This repository contains both **evidence** (course artifacts) and **derived organization** (maps, summaries, memory). They must not be treated as equally authoritative.

## Authority tiers

| Tier | Material | Use |
|---|---|---|
| A | Current A.Y. 2025/2026 official slides, homework specifications, instructor-issued documents | Canonical for course definitions, algorithms, required deliverables, and current-year details |
| B | Current instructor notebooks/code | Canonical for lab implementation details and expected computational workflow |
| C | Lecture transcripts | Canonical for what was said in class, but noisy for symbols, names and formulas; corroborate mathematical details |
| D | Supplied external references (Saad, von Luxburg, PageRank paper, etc.) | Background, deeper derivations, alternative explanations |
| E | `docs/` and `memory/` | Retrieval/synthesis layer; must preserve provenance and defer to A–D |

## Conflict resolution

When two files disagree, do not average or silently reconcile them. Record both claims, then apply the tier ordering. Current-year material outranks older generic lab slides where the course has changed. A transcript typo must never override a clearly typeset formula in an official slide.

## Provenance conventions

A derived note should state or encode:

- `source_paths`: repository paths supporting the claim;
- `status`: `verified`, `derived`, or `needs-check`;
- `scope`: lecture/module/concept/homework;
- `last_updated`: ISO date.

For a numerical algorithm, provenance should cover the exact variant used in class. For example, “Gram–Schmidt” is ambiguous unless the note distinguishes classical and modified variants when that distinction matters.

## Integrity

`sources/MANIFEST.tsv` is the ingestion ledger for the uploaded archive. It records original relative path, byte size, file type and SHA-256. A source is considered byte-for-byte mirrored only when its repository copy matches the manifest hash. Normalized text or notebook extracts are **representations**, not byte-identical replacements.
