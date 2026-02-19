---
title: "JPF Stretch Hub"
date: 2026-01-21
draft: false
summary: "Booking, payment, and user management platform for a stretching and fitness studio — built with Django, React, and Celery."
tags: ["Django", "React", "Celery", "TailwindCSS", "Docker"]


featured: true
showReadingTime: false
showTableOfContents: false
showHero: true
heroStyle: "thumbAndBackground"
weight: 9
---

{{< badge >}} Django {{< /badge >}} {{< badge >}} PostgreSQL {{< /badge >}} {{< badge >}} Tailwind {{< /badge >}}

{{< button href="https://github.com/meshack-vs-you-all/jpf_stretch_hub" target="_blank" >}}
{{< icon "github" >}}&nbsp; View Source on GitHub
{{< /button >}}

{{< github repo="meshack-vs-you-all/jpf_stretch_hub" >}}


## Overview

JPF Stretch Hub is a comprehensive web application designed for a stretching and fitness studio, handling everything from class bookings and payment processing to user account management. It was scaffolded with **Cookiecutter Django** to ensure production-grade defaults from day one.

## Architecture & Technical Decisions

The backend runs on **Django 5** with **django-allauth** providing authentication (including MFA via FIDO2) — a deliberate choice to support passwordless login flows for studio members who book on mobile devices.

The frontend is a standalone **React 19** SPA bundled with **Vite**, styled with **TailwindCSS**, and communicating with the backend via REST APIs. The decoupled architecture allows the frontend team to iterate on the booking UI independently of backend releases.

Background task processing — confirmation emails, payment webhooks, and schedule reminders — is handled by **Celery** backed by Redis, with **Flower** providing real-time task monitoring. Periodic tasks like session cleanup and report generation use **django-celery-beat** for cron-style scheduling.

## Deployment

The project ships with production-grade Docker Compose configurations. Static assets are compiled, compressed, and fingerprinted using **django-compressor** and served through **WhiteNoise**. Security hardening follows Cookiecutter Django's opinionated defaults, including Argon2 password hashing and strict CSP headers.

## Impact

The platform replaced a manual booking system (phone calls + spreadsheets) with a self-service portal that handles scheduling, payments, and client communications — streamlining studio operations and reducing administrative overhead for a growing fitness business in Nairobi.
