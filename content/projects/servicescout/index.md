---
title: "ServiceScout"
date: 2026-02-02
draft: false
summary: "SEO-first local service aggregator that connects users with vetted service providers across Nairobi — with dynamic landing pages and smart lead capture."
tags: ["Django", "SEO", "Python"]
featured: true
showReadingTime: false
showTableOfContents: false
showHero: true
heroStyle: "thumbAndBackground"
weight: 4
links:
  - icon: github
    icon_pack: fab
    name: GitHub
    url: https://github.com/meshack-vs-you-all/servicescout
---

{{< button href="https://github.com/meshack-vs-you-all/servicescout" target="_blank" >}}
{{< icon "github" >}}&nbsp; View Source on GitHub
{{< /button >}}


## Overview

ServiceScout is a local service aggregator platform designed to bridge the gap between service seekers and providers in Nairobi. Rather than building yet another directory, the platform takes an SEO-first approach — generating high-intent landing pages that capture organic traffic from people actively searching for services like "plumber in Westlands" or "electrician in Kilimani."

## Architecture & Technical Decisions

Built on **Django 5**, ServiceScout uses a clean URL hierarchy (`/<service>/<city>/<area>/`) that maps directly to search intent. Each URL combination dynamically generates a fully SEO-optimized page with unique H1 tags, meta descriptions, and structured content — without requiring manual content creation for every service-location pair.

{{< mermaid >}}
graph LR
    A[User Search: "Plumber Westlands"] --> B(ServiceScout Router)
    B --> C{URL Match?}
    C -- Yes --> D[Fetch Service & Location Data]
    D --> E[Generate Dynamic SEO Content]
    E --> F[Render Landing Page]
    C -- No --> G[404 / Suggest Nearby]
{{< /mermaid >}}

The lead capture system is deliberately minimal: a single streamlined form that collects just enough information to route a qualified lead to the right provider. Form hardening includes Kenyan phone number validation (07XX/01XX/+254 formats), whitespace stripping, and empty-description prevention to maintain lead quality.

The admin dashboard surfaces leads with enhanced filtering and search capabilities, giving providers quick access to relevant opportunities without wading through noise.

## Design Philosophy

Every architectural decision prioritizes **speed and discoverability**: minimal templates for fast page loads, dynamic SEO content that scales across hundreds of service-location combinations, and a URL structure that search engines can crawl and index efficiently. The platform deliberately avoids heavy JavaScript frameworks — server-rendered HTML keeps time-to-first-byte low and ensures full crawlability.

## Impact

ServiceScout provides a scalable model for hyperlocal service marketplaces in East African cities, where service discovery still relies heavily on word-of-mouth and social media. The SEO-first approach generates organic leads at near-zero customer acquisition cost, making it viable for markets where paid advertising budgets are constrained.
