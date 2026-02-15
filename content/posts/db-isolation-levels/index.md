---
title: "Understanding Database Isolation Levels"
date: 2026-02-01
draft: false
description: "Dirty reads, phantom reads, and non-repeatable reads. What happens when concurrent transactions collide?"
summary: "If you don't understand isolation levels, your financial application has a race condition. Guaranteed."
tags: ["Database", "SQL", "PostgreSQL", "Backend"]
series: ["System Design Masterclass"]
featuredImage: "https://images.unsplash.com/photo-1555949963-ff9fe0c870eb?q=80&w=2070&auto=format&fit=crop"
layout: "simple"
---

{{< lead >}}
The default isolation level in many databases allows race conditions. Do you know what yours is set to?
{{< /lead >}}

## The Phenomena

1.  **Dirty Read**: Reading uncommitted data from another transaction.
2.  **Non-Repeatable Read**: Reading the same row twice gets different data (someone updated it).
3.  **Phantom Read**: Running the same conceptual query gets different rows (someone inserted a new row).

## The Levels

| Level | Dirty Read | Non-Repeatable | Phantom |
| :--- | :---: | :---: | :---: |
| **Read Uncommitted** | Yes | Yes | Yes |
| **Read Committed** (Postgres Default) | No | Yes | Yes |
| **Repeatable Read** | No | No | Yes |
| **Serializable** | No | No | No |

## When to use Serializable?

When correctness is more important than speed. E.g., Preventing double-spending in a banking ledger.

```sql
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;
BEGIN;
-- Your logic
COMMIT;
```

It guarantees that the result is the same as if transactions were executed one after another.
