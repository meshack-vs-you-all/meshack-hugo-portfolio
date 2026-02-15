---
title: "Microservices vs Monolith: The Honest Truth"
date: 2026-02-02
draft: false
description: "Why you probably don't need microservices, and when you actually do."
summary: "Microservices are not a default. They are a solution to organizational scaling problems, not technical ones."
tags: ["Architecture", "Microservices", "System Design"]
series: ["System Design Masterclass"]
featuredImage: "https://images.unsplash.com/photo-1486312338219-ce68d2c6f44d?q=80&w=2072&auto=format&fit=crop"
layout: "simple"
---

{{< lead >}}
"We need microservices because Netflix uses them."
This sentence has killed more startups than bad product-market fit.
{{< /lead >}}

## The Hidden Cost of Microservices

You trade **complexity of code** for **complexity of infrastructure**.

1.  **Network Latency**: Function calls are nanoseconds. HTTP calls are milliseconds.
2.  **Distributed Transactions**: Rollbacks across 3 services are a nightmare (Requires Sagas pattern).
3.  **Observability**: Debugging a request that jumps through 5 containers requires expensive tracing tools (Jaeger/OpenTelemetry).

## The Modular Monolith

This is the sweet spot for 99% of companies.
Keep code in one repo. Deploy as one binary. But enforce strict module boundaries.

```python
# Django Example
/users
/payments
/inventory
```

If `payments` imports from `inventory`, you have a violation. Enforce this via linters, not network boundaries.

## When to Split?

1.  **Independent Scaling**: Video processing needs 100 GPUs. The user login service needs 1 CPU.
2.  **Team Scaling**: You have 50 engineers. API collisions in git are slowing you down.
