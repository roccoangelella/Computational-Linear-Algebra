# Sources

`sources/MANIFEST.tsv` is the integrity ledger for the 91 files supplied in `CLA.zip` (about 161 MB uncompressed). It records original relative paths, byte sizes, file types, and SHA-256 hashes.

## Intended source layout

- `official/` — current-course slide decks, homework specifications, and official PDF representations.
- `labs/` — notebooks, Python support files, and normalized notebook-source views.
- `transcripts/` — lecture transcripts or retrieval bundles preserving their exact text.
- `references/` — supplied external literature (Saad, von Luxburg, spectral graph theory, PageRank paper, etc.).
- `data/` — supplied datasets and graph data.

## Important integrity rule

A normalized Markdown/text extraction is useful for search but is not the same artifact as the original PDF/notebook. The original `path + SHA-256` pair in `MANIFEST.tsv` is the identity of the source. Mathematical claims extracted from visually rich or handwritten PDFs must be checked against the rendered source before being treated as exact.

## Current ingestion note

The repository's navigation, authority rules, course map, lecture map, concept graph, assessment map, research basis and complete archive manifest are established first. Large binary course artifacts should be mirrored with Git LFS (especially the eigenvalue/SVD PDFs) so GitHub does not reject files above its normal blob limits; once mirrored, hashes should be checked against `MANIFEST.tsv`.
