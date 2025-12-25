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

**Context**  
Most underwriting systems still rely on rule engines because they are legible,
auditable, and easy to reason about under regulatory pressure.

**Observation**  
Rule engines fail at boundaries. Every exception must be anticipated in advance,
and once exceptions accumulate, the rule set becomes opaque even to its authors.

**Alternative**  
Decision surfaces allow smooth local behavior while respecting global constraints.
They model *likelihood*, not *permission*.

**Practice**  
In production systems, the most robust architecture is hybrid:

- hard constraints for structural limits
- soft surfaces for ranking, routing, and appetite estimation

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

```python
def score(application):
    constraints = hard_constraints(application)
    surface_score = model.predict(application.features)

    if not constraints:
        return None

    return surface_score

This does not imply simplistic models. It implies models whose internal logic
maps cleanly onto human concepts.
</details>

---

<details>
<summary><strong>Lender Appetite Is Not a Scalar</strong></summary>

![Conditional appetite sketch](/assets/appetite-graph.png)

Appetite varies across dimensions:
- deal type
- risk distribution
- operational load
- recent outcomes

Graph representations allow appetite to exist at intersections,
not as a global score.
</details>