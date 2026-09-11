# Knowledge architecture for LLM-assisted study

## Design objective

The repository must support two very different queries:

1. **local precision** — e.g. “what stopping criterion did the course use for Jacobi?”;
2. **global synthesis** — e.g. “how do orthogonality, Krylov methods, Lanczos and SVD fit together?”

A flat folder of PDFs is weak at both. The architecture therefore uses an immutable evidence layer plus multiple small, linked representations optimized for retrieval.

## Layers

```text
AGENTS.md                  -> operating rules for an LLM/coding agent
memory/CORE.md             -> compact persistent orientation

docs/
  COURSE_MAP.md            -> module-scale hierarchical summary
  LECTURE_INDEX.md         -> chronological access path
  CONCEPT_GRAPH.md         -> prerequisite/application links + search aliases
  ASSESSMENT.md            -> exam/homework-specific retrieval path
  SOURCE_POLICY.md         -> authority/conflict/provenance rules
  RESEARCH_BASIS.md        -> external evidence for this architecture

sources/
  MANIFEST.tsv             -> integrity/provenance ledger for original upload
  official/                -> official current-course artifacts / normalized extracts
  labs/                    -> notebook/code representations
  transcripts/             -> lecture transcripts
  references/              -> supplied external literature / representations
```

## Why this is memory rather than merely documentation

An agent memory system must decide **what to write, how to organize it, and what to read back**. The repository makes those operations explicit:

- **write**: source artifacts are ingested without reinterpretation; derived notes are only added with provenance;
- **manage**: information is organized by authority, chronology, concept dependencies and assessment relevance;
- **read**: the agent starts from compact maps, then expands only into the evidence needed for the question.

This keeps the always-loaded memory small while preserving deep access to the corpus.

## Multi-scale representation

The architecture follows the same broad principle as hierarchical retrieval systems: retain fine-grained evidence while adding progressively more abstract summaries.

- File/source level: exact or normalized artifact.
- Lecture level: `LECTURE_INDEX.md`.
- Module level: `COURSE_MAP.md`.
- Cross-module/global level: `memory/CORE.md` and `CONCEPT_GRAPH.md`.

A global question should be answered from module/concept summaries and then verified against selected sources. A formula-level question should skip global summarization and retrieve the relevant source directly.

## Hybrid retrieval without committing to one vector database

Repository structure should remain useful even when the retrieval engine changes. Therefore every concept is discoverable through:

- meaningful filenames and headings;
- canonical names plus transcript aliases;
- explicit source paths;
- prerequisites/application links;
- chronology;
- exact lexical search.

An external semantic/vector index can be added later, but the repository remains intelligible without it. If such an index is added, use hybrid retrieval: exact lexical/BM25 matching for symbols and names plus semantic embeddings for paraphrases, followed by reranking and source verification.

## Graph retrieval

The course naturally forms a knowledge graph. Examples:

`orthogonality -> Arnoldi -> Krylov -> Lanczos`

`eigenvalues -> PageRank / spectral clustering / PCA`

`SVD -> low-rank approximation / pseudoinverse / PCA`

Graph traversal prevents a retrieval system from returning only the closest wording while missing prerequisite machinery or downstream applications. `CONCEPT_GRAPH.md` is the minimal portable representation of that graph; it can later be serialized to JSON/GraphML if automated graph search is needed.

## Memory consolidation policy

Not every chat insight deserves persistence. A durable memory entry should be written only when it is:

- source-verifiable;
- likely to recur across future study sessions;
- concise enough to retrieve cheaply;
- not a duplicate of an existing concept note.

When a new insight changes an older derived explanation, update the existing note and record the supporting source rather than appending contradictory fragments. Source artifacts themselves remain immutable.

## Retrieval protocol for future agents

For a course question, use the following sequence:

1. retrieve `memory/CORE.md`;
2. identify relevant module(s) in `COURSE_MAP.md`;
3. traverse prerequisite/application edges in `CONCEPT_GRAPH.md` if the question spans concepts;
4. retrieve the highest-authority source(s) for the exact claim;
5. use transcripts to recover classroom motivation, examples and oral clarifications;
6. use supplied references for deeper theory only after the course-specific formulation is known;
7. answer with source paths and distinguish explicit course content from explanatory background.

## Evaluation

A memory/documentation architecture should be testable. Future repository checks should include a small question set covering:

- exact fact retrieval (definition/algorithm step);
- temporal/chronological questions (“when was X introduced?”);
- cross-source synthesis;
- prerequisite reasoning;
- source conflict resolution;
- abstention when a claim is absent from the corpus.

This mirrors the capabilities emphasized by modern long-memory benchmarks rather than optimizing only for nearest-neighbor recall.
