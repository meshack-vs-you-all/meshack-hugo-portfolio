---
title: "Docker: Stop Saying 'It Works on My Machine'"
date: 2026-02-12
draft: false
description: "A pragmatic introduction to Docker containers for full-stack developers. Covers multi-stage builds, security scanning, and production optimization."
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

## 1. The Dockerfile: From Basic to Production-Ready

A `Dockerfile` is a recipe for your environment.

### Level 1: The Basic Dockerfile (Don't deploy this)

```dockerfile
FROM python:3.11
WORKDIR /app
COPY . .
RUN pip install -r requirements.txt
CMD ["python", "app.py"]
```
*Why this is bad*: It includes the full OS, compiler tools, and is huge >1GB.

### Level 2: Multi-Stage Build (The Professional Way)

We use a "Builder" stage to compile dependencies, and a "Runner" stage to run the app.

```dockerfile
# Stage 1: Builder
FROM python:3.11-slim as builder
WORKDIR /app
COPY requirements.txt .
RUN pip install --user -r requirements.txt

# Stage 2: Runner
FROM python:3.11-distroless
WORKDIR /app
COPY --from=builder /root/.local /root/.local
COPY . .
ENV PATH=/root/.local/bin:$PATH
CMD ["python", "app.py"]
```
*Result*: A 60MB image that is secure and fast.

## 2. Docker Compose: Orchestrating the Stack

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
      - redis
    environment:
      - DATABASE_URL=postgres://user:pass@db:5432/myapp
  
  db:
    image: postgres:15-alpine
    volumes:
      - postgres_data:/var/lib/postgresql/data
    environment:
      POSTGRES_PASSWORD: secretpassword

  redis:
    image: redis:alpine

volumes:
  postgres_data:
```

{{< alert >}}
With this file, `docker-compose up` is the only command a new developer needs to run to start the entire project.
{{< /alert >}}

## 3. Security Best Practices

1.  **Don't run as Root**: By default, Docker containers run as root. This is a security risk.
    ```dockerfile
    RUN adduser -D myuser
    USER myuser
    ```

2.  **Scan your Images**: Use `docker scan` (powered by Snyk) to find vulnerabilities.
    ```bash
    docker scan my-image:latest
    ```

3.  **Use `.dockerignore`**: Prevent secrets from being copied into the image.
    ```text
    .git
    .env
    __pycache__
    passwords.txt
    ```

## 4. Common Commands Cheat Sheet

| Command | Action |
| :--- | :--- |
| `docker build -t myapp .` | Build an image |
| `docker run -p 80:80 myapp` | Run container mapping port 80 |
| `docker ps` | List running containers |
| `docker exec -it <id> bash` | Shell into a container |
| `docker system prune` | Clean up unused images/volumes |
