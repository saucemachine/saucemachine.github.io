---
layout: default
title: Notes
---

# Notes

Short technical and conceptual notes on decision systems, knowledge graphs,
and applied machine learning. These are not posts or essays — just working
thoughts worth keeping.

---

<details>
<summary><strong>Decision Surfaces vs Rule Engines</strong></summary>

Rule engines dominate underwriting systems because they are easy to explain,
audit, and enforce. Their failure mode is rigidity: every exception must be
anticipated in advance.

Decision surfaces, whether learned or hand-constructed, behave differently.
They allow local smoothness and global constraint simultaneously. Instead of
encoding *what must happen*, they encode *what is likely to happen* under
similar conditions.

In practice, most production systems end up hybrid:
- hard constraints for regulatory or structural limits
- soft decision surfaces for ranking, routing, or appetite estimation

The mistake is treating these as competing paradigms rather than layers.
</details>

---

<details>
<summary><strong>Knowledge Graphs vs Feature Tables</strong></summary>

Feature tables collapse structure into columns. This is efficient, but lossy.

Knowledge graphs preserve:
- relationships
- cardinality
- optionality
- evolving schema

The cost is higher ingestion complexity and slower iteration early on. The
benefit appears later, when new questions emerge that were not anticipated at
data collection time.

A useful heuristic:
- if the question space is stable, use tables
- if the question space is evolving, use graphs

In lending systems, the question space is almost never stable.
</details>

---

<details>
<summary><strong>Explainability as a First-Class System Constraint</strong></summary>

Explainability is often treated as a post-processing step: generate a score,
then attach an explanation.

This works poorly in systems where:
- decisions are contested
- feedback loops exist
- human override is expected

In these cases, explainability must shape the model *itself*. Feature design,
aggregation logic, and thresholding should all be influenced by what can be
reasonably explained to a human operator.

This does not imply simplistic models. It implies models whose internal logic
maps cleanly onto human concepts.
</details>

---

<details>
<summary><strong>Lender Appetite Is Not a Scalar</strong></summary>

Many systems model appetite as a single score or acceptance probability.
This hides important structure.

In reality, appetite is conditional:
- on deal type
- on risk distribution
- on operational capacity
- on recent outcomes

Graph representations make this explicit by allowing appetite to exist at the
intersection of multiple dimensions, rather than as a global attribute.

This is less convenient, but more faithful to how decisions are actually made.
</details>
