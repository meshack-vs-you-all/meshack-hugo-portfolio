---
title: "Crafted Edge Solutions"
date: 2026-01-21
draft: false
summary: "Full-stack consultancy platform powering Crafted Edge Solutions Kenya — featuring a Wagtail CMS, client dashboards, analytics, and a blog engine."
tags: ["Django", "Wagtail", "Docker", "PostgreSQL", "REST API"]
externalUrl: "https://github.com/meshack-vs-you-all/Crafted_Edge_main"
featured: true
showReadingTime: false
showTableOfContents: false
showHero: true
heroStyle: "thumbAndBackground"
weight: 1
links:
  - icon: github
    icon_pack: fab
    name: GitHub
    url: https://github.com/meshack-vs-you-all/Crafted_Edge_main
---

{{< button href="https://github.com/meshack-vs-you-all/Crafted_Edge_main" target="_blank" >}}
{{< icon "github" >}}&nbsp; View Source on GitHub
{{< /button >}}

{{< github repo="meshack-vs-you-all/Crafted_Edge_main" >}}


## Overview

Crafted Edge Solutions is the digital backbone for a Nairobi-based consultancy founded in May 2024, focused on empowering businesses through digital transformation. The platform serves as both the public-facing website and an internal operations hub.

## Architecture & Technical Decisions

The backend is built on **Django 5** with **Wagtail 5.2** providing a headless-capable CMS that allows non-technical team members to publish content, manage service pages, and maintain the company blog without touching code. Content editing workflows, including draft → review → publish, are handled entirely through Wagtail's built-in moderation system.

The API layer uses **Django REST Framework** to expose structured data for potential future mobile clients and third-party integrations. Authentication follows Django's session model with additional API token support via DRF.

For data persistence, the project uses **PostgreSQL** in production with **Redis** powering both the caching layer and Celery task queues. Static assets are optimized and served through **WhiteNoise** for zero-config static file handling in containerized deployments.

## Deployment

The entire stack is containerized with **Docker** and orchestrated via Docker Compose, with separate configurations for development and production environments. The production Dockerfile uses a multi-stage build based on Python 3.12-slim to minimize the final image size.

## Impact

The platform consolidates client management, appointment scheduling, analytics tracking, and content publishing into a single, self-hosted system — reducing dependency on fragmented SaaS tools for the consultancy's day-to-day operations.
