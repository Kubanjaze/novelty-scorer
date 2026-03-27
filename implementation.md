# Phase 66 — Claude Scoring Compound Novelty vs Prior Art
**Version:** 1.0 | **Date:** 2026-03-27
## Goal
Ask Claude to score how novel each compound is relative to known CETP inhibitor prior art.
Returns structured novelty_score (1-10), rationale, and closest known analog.
CLI: `python main.py --input data/compounds.csv --n 3`
## Key Concepts
- Claude as novelty assessor using domain knowledge
- Structured JSON output: novelty_score, rationale, closest_analog
- Tests Claude's pharmaceutical prior art knowledge
