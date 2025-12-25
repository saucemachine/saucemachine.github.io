---
layout: default
title: Lender Appetite Is Not a Scalar
---

# Lender Appetite Is Not a Scalar

Many systems model appetite as a single acceptance probability.
This hides structure that matters operationally.

![Conditional appetite sketch](/assets/appetite-graph.png)

Appetite is conditional on:
- deal type
- risk distribution
- operational load
- recent outcomes

Graph representations allow appetite to exist at **intersections**,
not as a global score.

```python
def appetite(application, context):
    if not hard_constraints(application):
        return None

    return surface_model.predict(
        application.features,
        context.signals
    )
