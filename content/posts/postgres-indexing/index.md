---
title: "PostgreSQL Performance: Indexing Strategies"
date: 2026-02-09
draft: false
description: "How to speed up slow queries using B-Tree, GIN, and Partial Indexes in PostgreSQL."
summary: "Database performance isn't magic. It's about data structures. Learn how to optimize your Postgres queries."
tags: ["PostgreSQL", "Database", "Performance", "SQL"]
featuredImage: "https://images.unsplash.com/photo-1544383835-bda2bc66a55d?q=80&w=2021&auto=format&fit=crop"
layout: "simple"
---

{{< lead >}}
A slow application is usually a slow database. Before you cache everything in Redis, verify your **indexes**.
{{< /lead >}}

## The `EXPLAIN ANALYZE` Command

This is your best friend. It tells you exactly how Postgres executes a query.

```sql
EXPLAIN ANALYZE SELECT * FROM users WHERE email = 'test@example.com';
```

If you see `Seq Scan` (Sequential Scan), Postgres is reading every row in the table. That's O(N). We want O(log N).

## Index Types

1.  **B-Tree** (Default): Great for `=`, `<`, `>`, `BETWEEN`.
    ```sql
    CREATE INDEX idx_users_email ON users(email);
    ```

2.  **GIN** (Generalized Inverted Index): Essential for JSONB and Full-Text Search.
    ```sql
    CREATE INDEX idx_products_data ON products USING GIN (data);
    ```

## Partial Indexes

{{< alert icon="bolt" >}}
**Optimization**: If you frequently query a subset of data (e.g., `is_active=True`), creating an index ONLY for those rows saves space and speeds up writes.
{{< /alert >}}

```sql
CREATE INDEX idx_active_users ON users(id) WHERE is_active = TRUE;
```
