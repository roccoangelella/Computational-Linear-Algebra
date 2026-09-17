# 2026-09-17 — Lecture 03: Jupyter execution state

status: **verified**
last-updated: **2026-09-17**
source_paths:
- `knowledge/modules/01-python-and-numerical-tooling.md`
- `docs/LECTURE_INDEX.md`

topics studied:
- role of Jupyter notebooks as an ordered mix of Markdown and executable code cells;
- distinction between code currently visible in a notebook and variables currently stored in the kernel state;
- why executing cells out of order can make displayed code and actual computation disagree;
- meaning of a fresh kernel / restart as clearing the stored execution state;
- reproducibility principle: a numerical notebook should execute correctly from a fresh kernel in logical top-to-bottom order;
- concrete example in which changing `x = 5` to `x = 100` without rerunning that cell leaves the kernel value at `x = 5`, so a later computation still uses the old value;
- numerical-linear-algebra relevance: stale matrices or parameters can yield plausible but incorrect experimental conclusions.

comprehension check:
- learner chose to continue immediately after the explanation, so the first-pass execution-state concept is treated as understood well enough to proceed.

mastery note:
- basic Jupyter execution-state and reproducibility concepts are considered understood; reinforce naturally during later coding exercises.