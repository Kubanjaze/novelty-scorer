# Phase 66 — Claude Scoring Compound Novelty vs Prior Art

**Version:** 1.1 | **Tier:** Standard | **Date:** 2026-03-27

## Goal
Ask Claude to score how novel each compound is relative to known CETP inhibitor prior art (anacetrapib, torcetrapib, dalcetrapib, evacetrapib). Tests Claude's pharmaceutical domain knowledge.

CLI: `python main.py --input data/compounds.csv --n 3`

Outputs: novelty_scores.json

## Logic
- Load N compounds from CSV (name, SMILES, pIC50)
- Build a prompt with compound data + named CETP inhibitor references
- Ask for: novelty_score (1-10), rationale, closest_known_analog per compound
- Parse structured JSON array of novelty assessments
- Report: novelty scores, analog matches, rationale quality

## Key Concepts
- Claude as patent/novelty assessor using domain knowledge
- Structured JSON output: `[{compound_name, novelty_score, rationale, closest_known_analog}]`
- Reference compounds: anacetrapib (Merck), torcetrapib (Pfizer), dalcetrapib (Roche), evacetrapib (Lilly)
- Tests whether Claude can distinguish novel chemistry from known scaffolds

## Verification Checklist
- [x] Claude generates novelty scores for all compounds
- [x] Scores include closest known analog references
- [x] Rationale references specific structural features
- [x] One clean API call

## Results
| Metric | Value |
|--------|-------|
| Compounds scored | 3 |
| Mean novelty score | 2.0/10 |
| Closest analogs | torcetrapib/anacetrapib (acrylamide core) |
| Input tokens | 236 |
| Output tokens | 459 |
| Est. cost | $0.0020 |

Key finding: All compounds scored low novelty (2/10) — Claude correctly identified that simple acrylamide-aniline scaffolds are well-established in CETP inhibitor prior art. The minimal halogen substitutions (F/Cl/Br) do not provide meaningful novelty vs known CETPi.

## Risks (resolved)
- Claude's prior art knowledge may be outdated — referenced correct known CETPi drugs (anacetrapib, torcetrapib)
- Novelty scores may be uniformly low for structurally simple compounds — confirmed (all 2/10 for acrylamide-anilines)
- No access to actual patent databases — scoring based on Claude's training data knowledge only
