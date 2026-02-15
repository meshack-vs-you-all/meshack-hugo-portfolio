---
title: "System Design: Scaling to 1 Million Users"
date: 2026-02-04
draft: false
description: "A practical roadmap for scaling a web application from a single server to a distributed system."
summary: "Load balancers, caching, database sharding, and CDNs. The missing guide to system architecture."
tags: ["System Design", "Architecture", "Scalability", "High Performance"]
series: ["System Design Masterclass"]
featuredImage: "https://images.unsplash.com/photo-1451187580459-43490279c0fa?q=80&w=2072&auto=format&fit=crop"
layout: "simple"
---

{{< lead >}}
Scaling isn't about buying bigger servers. It's about removing bottlenecks. Here is the evolution of a startup's architecture.
{{< /lead >}}

## Stage 1: The Monolith (0 - 1k Users)

One server. Database + App + Web Server all on the same machine.
*   **Pros**: Simple deployment, cheap.
*   **Cons**: Single point of failure.

## Stage 2: Vertical Scaling (1k - 10k Users)

Upgrade the instance size (t3.micro -> m5.large).
This works until it doesn't. You eventually hit the limit of a single machine.

## Stage 3: Horizontal Scaling (10k - 100k Users)

This is the big jump.

1.  **Load Balancer (ELB/Nginx)**: Distributes traffic across multiple app servers.
2.  **Stateless Apps**: User sessions moved to Redis.
3.  **Database Separation**: Master (Write) / Replica (Read) architecture.

{{< mermaid >}}
graph TD
    User --> LB[Load Balancer]
    LB --> App1[App Server 1]
    LB --> App2[App Server 2]
    App1 --> Redis[Redis Cache]
    App2 --> Redis
    App1 --> DB_M[DB Master]
    App2 --> DB_R[DB Replica]
    DB_M -->|Replication| DB_R
{{< /mermaid >}}

## Stage 4: 1M+ Users

Now we need serious optimizations.

*   **CDN (Cloudflare)**: Cache static assets at the edge.
*   **Database Sharding**: Split the database by User ID (Users 1-1M on DB1, 1M-2M on DB2).
*   **Async Workers (Celery/Kafka)**: Move everything non-essential (email, PDF generation) to background queues.
