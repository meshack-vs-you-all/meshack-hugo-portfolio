---
title: "Docker: Stop Saying 'It Works on My Machine'"
date: 2026-02-12
draft: false
description: "A pragmatic introduction to Docker containers for full-stack developers."
summary: "Containers are the standard unit of software delivery. This guide covers Dockerfiles, Compose, and best practices for Python/Node apps."
tags: ["Docker", "DevOps", "Containers", "Deployment"]
series: ["DevOps Zero to Hero"]
featuredImage: "https://images.unsplash.com/photo-1605745341117-95a12dbe3f3c?q=80&w=2070&auto=format&fit=crop"
layout: "simple"
---

{{< lead >}}
If you're still manually installing dependencies on your server, you're doing it wrong. **Docker** ensures your environment is consistent from dev to prod.
{{< /lead >}}

## The Problem

-   **Dev**: Python 3.12, Postgres 16
-   **Prod**: Python 3.8, Postgres 12 (System Default)
-   **Result**: Crash.

## The Solution: Dockerfile

A `Dockerfile` is a recipe for your environment.

```dockerfile
# Start from a clean slate
FROM python:3.11-slim

# Set working directory
WORKDIR /app

# Install system dependencies (rarely needed with slim)
# RUN apt-get update && apt-get install -y gcc

# Install python dependencies
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy source code
COPY . .

# Run the app
CMD ["python", "app.py"]
```

## Docker Compose

{{< badge >}}
Orchestration
{{< / badge >}}

Manage multi-container apps (App + DB + Redis) with `docker-compose.yml`.

```yaml
version: '3.8'
services:
  web:
    build: .
    ports:
      - "8000:8000"
    depends_on:
      - db
  db:
    image: postgres:15
    environment:
      POSTGRES_PASSWORD: secretpassword
```

{{< alert >}}
With this file, `docker-compose up` is the only command a new developer needs to run to start the entire project.
{{< /alert >}}
