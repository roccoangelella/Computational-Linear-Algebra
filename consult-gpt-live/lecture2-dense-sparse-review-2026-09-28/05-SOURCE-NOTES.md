# Source notes and conventions

## Repository context used
- `memory/CORE.md`
- `memory/STUDY_PROGRESS.md`
- `knowledge/modules/00-large-scale-and-sparse.md`
- `knowledge/depth/00-sparse-formats-operations-reorderings.md`
- dated Lecture-02 study-memory files.

The attached current deck is the requested basis for this review. Repository notes recover prior study state and known weak spots; they do not overwrite the deck.

## Indexing caution
The lecture's mathematical arrays/examples frequently use **1-based indexing**. Python/SciPy code uses **0-based indexing**. Identify the convention before correcting an answer.

## Terminology caution
- `Nz` in the slides is the number of nonzero entries; repository notes often write `nnz(A)`.
- CSR may also be called CRS / Yale format in the lecture.
- Do not silently replace the lecture's MSR/MSC or DIAG/ELLPACK conventions with a different textbook packing convention.
