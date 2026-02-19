---
title: "JPF Stretch Hub (CMS Edition)"
date: 2026-02-19
draft: false
summary: "A robust CMS-driven implementation of the fitness studio platform using Wagtail for content management and Django REST Framework for API integration."
tags: ["Django", "Wagtail", "DRF", "PostgreSQL", "CMS"]

featured: false
showReadingTime: false
showTableOfContents: false
showHero: true
heroStyle: "thumbAndBackground"
weight: 10
---

{{< button href="https://github.com/meshack-vs-you-all/jpf_stretch_hub_wt" target="_blank" >}}
{{< icon "github" >}}&nbsp; View Source on GitHub
{{< /button >}}

{{< github repo="meshack-vs-you-all/jpf_stretch_hub_wt" >}}

## Overview

This iteration of the JPF Stretch Hub platform focuses on empowering non-technical staff to manage website content dynamically. By leveraging the **Wagtail CMS**, the studio can now easily update service descriptions, schedules, and blog posts without developer intervention.

## Core Features & Functionality

- **Dynamic Content Management**: A user-friendly admin interface for managing every aspect of the site's content.
- **Wagtail Integration**: Seamless blending of CMS capabilities with standard Django features.
- **REST API Endpoints**: Dedicated API layer built with **Django REST Framework** for authentication and data handling.
- **Role-Based Access**: Granular control over user permissions, allowing for separate client and administrator workflows.

## Technical Implementation

- **Framework**: Built on **Django** with **Wagtail 5.2**, providing a solid foundation for both CMS and custom application logic.
- **API Layer**: Uses **Django REST Framework** to expose status checks, registration, and profile endpoints.
- **Database**: Employs **PostgreSQL** for reliable data storage and scalability.
- **Modular Design**: A clean directory structure separating API, core, and project-level settings for better maintainability.

## Strategic Impact

The CMS-driven approach significantly reduces the ongoing maintenance burden for the business. It provides a scalable and flexible platform that can grow with the studio's needs, while ensuring a high level of performance and security.
