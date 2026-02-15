---
title: "Building Production Django Apps: Lessons from Shipping Real Products"
date: 2026-02-15
draft: false
summary: "Hard-won lessons from deploying Django applications for real businesses — covering project structure, Docker workflows, database choices, and the mistakes that taught me the most."
tags: ["Django", "Docker", "PostgreSQL", "Production"]
categories: ["Engineering"]
showTableOfContents: true
showReadingTime: true
---




{{< lead >}}
Most Django tutorials stop at `runserver`. Here's what I've learned building platforms that handle real traffic, real payments, and real users who don't read documentation.
{{< /lead >}}

## The Gap Between Tutorial and Production

Every Django developer knows the feeling: you follow the tutorial, everything works locally, and then you deploy. Suddenly you're debugging CORS errors at 2 AM, your static files are 404ing, and your database migrations are timing out.

After shipping multiple Django platforms — from a consultancy CMS to a fitness booking system — I've developed a set of principles that close the gap between "it works on my machine" and "it works in production."

{{< alert icon="docker" title="Principle #1: Containerize Immediately" >}}
The single biggest mistake I see (and made myself) is treating Docker as a deployment concern. It's not. It's a **development** concern.
{{< /alert >}}

```dockerfile
FROM python:3.12-slim

ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .
```

When your development environment matches production from day one, entire categories of bugs disappear. "It works on my machine" becomes a meaningful statement because your machine *is* the production environment.

## Settings Architecture Matters

Cookiecutter Django gets this right: separate settings for `base`, `local`, and `production`. But the key insight is **what goes where**:

- `base.py`: Everything that doesn't change between environments
- `local.py`: Debug toolbar, console email backend, relaxed security
- `production.py`: Gunicorn, real email, strict CORS, database connection pooling

```python
# base.py — the boring, correct defaults
DATABASES = {
    "default": env.db("DATABASE_URL")
}

# Never hardcode. Always env vars. Always.
SECRET_KEY = env("DJANGO_SECRET_KEY")
```

## Database Migrations in Production

{{< alert icon="triangle-exclamation" >}}
**Never run migrations during deployment without testing them first.** A migration that adds a NOT NULL column without a default will lock your table and take your site down.
{{< /alert >}}

My workflow for every migration:

1. Write the migration locally
2. Test it against a copy of production data
3. Check if it requires a table lock (adding columns, creating indexes)
4. If it locks: schedule downtime or use a two-step migration (add nullable → backfill → add constraint)

## WhiteNoise for Static Files

{{< alert icon="server" title="Simplify Your Stack" >}}
Stop using nginx to serve static files in simple deployments. **WhiteNoise** handles static files directly from your WSGI app with proper caching headers, compression, and fingerprinting.
{{< /alert >}}

```python
MIDDLEWARE = [
    "django.middleware.security.SecurityMiddleware",
    "whitenoise.middleware.WhiteNoiseMiddleware",  # Right after security
    # ...
]

STATICFILES_STORAGE = "whitenoise.storage.CompressedManifestStaticFilesStorage"
```

This eliminates an entire nginx configuration file and simplifies your Docker setup to a single container.

## The Monitoring Blindspot

The one thing I wish I'd set up earlier in every project: **structured logging**. Not `print()` statements. Not even basic Django logging. Structured JSON logs that can be searched, filtered, and alerted on.

```python
LOGGING = {
    "version": 1,
    "handlers": {
        "console": {
            "class": "logging.StreamHandler",
            "formatter": "json",
        },
    },
    "formatters": {
        "json": {
            "class": "pythonjsonlogger.jsonlogger.JsonFormatter",
        },
    },
}
```

## What I'd Tell My Past Self

1. **Use environment variables from the start.** Not "when you deploy." From the first `django-admin startproject`.
2. **Write the Dockerfile before the first model.** The discipline pays for itself within a week.
3. **Separate read and write concerns early.** Even if you're not doing CQRS, having different serializers for list vs. detail views saves enormous refactoring later.
4. **Test the deployment, not just the code.** A passing test suite means nothing if your Docker image doesn't build.

---

*Have questions or want to discuss Django architecture? {{< button href="mailto:meshackmogire406@gmail.com" >}}Reach out{{< /button >}}*
