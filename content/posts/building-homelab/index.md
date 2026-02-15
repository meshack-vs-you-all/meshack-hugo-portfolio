---
title: "The Joy of Homelabbing: Owning Your Infrastructure"
date: 2026-02-05
draft: false
description: "Why I run my own servers at home, and why you should too."
summary: "Stop renting everything from AWS. Building a homelab teaches you networking, virtualization, and system administration limits."
tags: ["Homelab", "Self-Hosted", "Hardware", "Linux"]
series: ["Hobby IT"]
featuredImage: "https://images.unsplash.com/photo-1591405351990-4726e331f141?q=80&w=2070&auto=format&fit=crop"
layout: "simple"
---

{{< lead >}}
There is a unique satisfaction in knowing exactly where your data lives (hint: it's in the closet under the stairs).
{{< /lead >}}

## What is a Homelab?

A homelab is a server (or cluster of servers) you run in your own home to host services, experiment with software, and learn.

## My Setup

-   **Hardware**: Intel NUC i7, 32GB RAM
-   **OS**: Proxmox VE (Hypervisor)
-   **Services**:
    -   **Pi-hole**: Network-wide ad blocking.
    -   **Jellyfin**: Media streaming (alternative to Netflix).
    -   **Nextcloud**: Personal Google Drive replacement.
    -   **Home Assistant**: Smart home automation.

## Why Do It?

1.  **Privacy**: Your photos stay on your hard drive.
2.  **Learning**: You execute `rm -rf /` once and learn forever.
3.  **Cost**: After hardware, it's free (minus electricity).

{{< badge >}}
Warning: Highly Addictive
{{< /badge >}}

Building a homelab is the best way to gain "Full Stack" confidence. You touch hardware, networking, OS, virtualization, containers, and applications.
