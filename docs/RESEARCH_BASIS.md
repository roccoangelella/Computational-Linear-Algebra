# Research basis for the repository memory design

The architecture is intentionally conservative: it adopts techniques that have empirical or systems support, but stores the underlying knowledge in plain version-controlled files so the corpus is not locked to one RAG framework.

## 1. Separate memory formation, organization and retrieval

Recent surveys frame agent memory as an explicit lifecycle rather than an ever-growing prompt. A useful abstraction is a **write/manage/read** loop: select what deserves persistence, consolidate/organize it, then retrieve only task-relevant evidence.

- Du, P. (2026), *Memory for Autonomous LLM Agents: Mechanisms, Evaluation, and Emerging Frontiers*, arXiv:2603.07670 — https://arxiv.org/abs/2603.07670
- Hu et al. (2025), *Memory in the Age of AI Agents*, arXiv:2512.13564 — https://arxiv.org/abs/2512.13564

**Repository consequence:** `sources/` is persistent evidence, `docs/` is consolidated semantic organization, and `memory/CORE.md` is a deliberately small high-value recall layer.

## 2. File-based memory is a strong baseline for capable agents

LongMemEval-V2 evaluates agents that must internalize large histories of environment-specific experience. Its AgentRunbook-C method stores trajectories as files and lets a coding agent gather evidence from that filesystem, achieving stronger accuracy than the paper's RAG baseline at higher latency cost.

- Wu et al. (2026), *LongMemEval-V2: Evaluating Long-Term Agent Memory Toward Experienced Colleagues*, arXiv:2605.12493 — https://arxiv.org/abs/2605.12493

**Repository consequence:** do not hide the course exclusively behind a vector store. Maintain a clean, searchable file hierarchy that an agent can inspect directly.

## 3. Hierarchical summaries improve global sense-making

RAPTOR recursively clusters and summarizes text so retrieval can operate at multiple abstraction levels. GraphRAG similarly creates entity/relationship structure and community summaries to answer global questions that ordinary chunk retrieval handles poorly.

- Sarthi et al. (ICLR 2024), *RAPTOR: Recursive Abstractive Processing for Tree-Organized Retrieval* — https://arxiv.org/abs/2401.18059
- Edge et al. (2024), *From Local to Global: A Graph RAG Approach to Query-Focused Summarization* — https://arxiv.org/abs/2404.16130

**Repository consequence:** keep lecture-level, module-level and global summaries simultaneously instead of choosing a single chunk size.

## 4. Graph structure helps associative/multi-hop retrieval

HippoRAG 2 augments retrieval with a graph and Personalized PageRank-style propagation to improve factual, associative and sense-making memory. A-MEM uses dynamically linked notes inspired by Zettelkasten to create an evolving network of related memories. LightRAG likewise combines graph structure with vector retrieval at multiple levels.

- Gutiérrez et al. (2025), *From RAG to Memory: Non-Parametric Continual Learning for Large Language Models (HippoRAG 2)*, arXiv:2502.14802 — https://arxiv.org/abs/2502.14802
- Xu et al. (2025), *A-MEM: Agentic Memory for LLM Agents*, arXiv:2502.12110 — https://arxiv.org/abs/2502.12110
- Guo et al. (2024), *LightRAG: Simple and Fast Retrieval-Augmented Generation*, arXiv:2410.05779 — https://arxiv.org/abs/2410.05779

**Repository consequence:** `CONCEPT_GRAPH.md` encodes prerequisite and application relations explicitly, so retrieval can expand from a local concept into its mathematically relevant neighbors.

## 5. Hybrid lexical + semantic retrieval is safer than embeddings alone

Contextual Retrieval combines contextualized embeddings with BM25-style lexical retrieval and rank fusion. The practical motivation is important for mathematics: exact strings such as `GMRES`, `rho(B)`, `Moore-Penrose`, a theorem name, or a homework filename can be crucial even when a semantic embedding is uncertain.

- Anthropic (2024), *Introducing Contextual Retrieval* — https://www.anthropic.com/engineering/contextual-retrieval

**Repository consequence:** preserve canonical terminology, aliases, headings and paths. If a vector index is added, retain lexical search and rerank the union.

## 6. Structure-preserving document conversion matters

Docling is designed to convert PDFs and other documents into structured machine-readable representations while retaining hierarchy, tables, formulas/layout cues more reliably than naive text extraction.

- Livathinos et al. (AAAI 2025), *Docling: An Efficient Open-Source Toolkit for AI-driven Document Conversion* — https://arxiv.org/abs/2408.09869

**Repository consequence:** normalized document representations should preserve page/section provenance. Plain `pdftotext` extracts are useful for initial indexing but should not be treated as lossless replacements for visual mathematical slides.

## 7. Long-memory systems must support updates, temporal reasoning and abstention

LongMemEval evaluates information extraction, multi-session reasoning, temporal reasoning, knowledge updates and abstention, showing that memory quality is not equivalent to “can retrieve a vaguely similar chunk.”

- Wu et al. (2024), *LongMemEval: Benchmarking Chat Assistants on Long-Term Interactive Memory*, arXiv:2410.10813 — https://arxiv.org/abs/2410.10813

**Repository consequence:** preserve chronology, version current-year rules separately from generic references, and allow “not found in the corpus” as a correct outcome.

## Design choices deliberately not made

- **No single opaque vector database is the source of truth.** It is an index, not evidence.
- **No unbounded chat-log memory.** Conversation residue is noisy and difficult to verify.
- **No automatic overwrite of old claims.** Conflicts are resolved with source authority and provenance.
- **No graph-only retrieval.** Exact mathematical notation and local passages still require lexical/source lookup.
- **No generated summary as sole evidence.** Summaries are navigation; the answer should descend to original or normalized source material for verification.
