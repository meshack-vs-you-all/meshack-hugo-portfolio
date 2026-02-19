---
title: "Kenya Scraper Platform"
date: 2025-10-16
draft: false
summary: "Production-grade ethical web scraping engine for Kenyan websites — with automatic robots.txt compliance, Playwright-based rendering, and Kubernetes-ready deployment."
tags: ["FastAPI", "Playwright", "Celery", "PostgreSQL", "Docker"]


featured: false
showReadingTime: false
showTableOfContents: false
showHero: true
heroStyle: "thumbAndBackground"
weight: 4
---

{{< badge >}} Python {{< /badge >}} {{< badge >}} Scrapy {{< /badge >}} {{< badge >}} Celery {{< /badge >}}

{{< button href="https://github.com/meshack-vs-you-all/ksp" target="_blank" >}}
{{< icon "github" >}}&nbsp; View Source on GitHub
{{< /button >}}

{{< github repo="meshack-vs-you-all/ksp" >}}


## Overview

The Kenya Scraper Platform (KSP) is a purpose-built web scraping infrastructure designed specifically for Kenyan websites. It prioritizes ethical data collection with built-in compliance mechanisms while maintaining the throughput needed for production workloads.

## Architecture & Technical Decisions

The API layer is built on **FastAPI** for its async-first design and automatic OpenAPI documentation — critical for a platform where multiple internal services submit scraping jobs. Data validation uses **Pydantic v2** models throughout, catching malformed requests before they reach the task queue.

For rendering JavaScript-heavy sites (common in Kenyan fintech and e-commerce), the platform uses **Playwright** instead of simple HTTP requests. This handles SPAs, lazy-loaded content, and pages behind client-side routing that would otherwise return empty responses to traditional scrapers.

Job orchestration is handled by **Celery** with Redis as the broker, distributing scraping tasks across workers with configurable concurrency and rate limiting per domain. Persistent storage uses **PostgreSQL** via **SQLAlchemy** with Alembic managing schema migrations, while raw HTML snapshots are stored in **MinIO/S3-compatible** storage.

### Ethical Compliance

The platform automatically parses and respects `robots.txt` for every target domain. Rate limiting is configurable per-site, the user agent clearly identifies the scraper, and CAPTCHA detection triggers manual intervention queues rather than automated bypass — ensuring compliance with website terms of service.

## Deployment

KSP ships with both Docker Compose for dev/staging and **Kubernetes manifests** for production environments. The Dockerfile uses a multi-stage build to minimize the final image footprint, and Helm-compatible configs allow scaling scraper workers independently of the API tier.

## Impact

The platform provides structured, reliable data extraction from Kenyan web sources — supporting market research, price monitoring, and business intelligence workflows where commercial scraping APIs have limited coverage of East African websites.
