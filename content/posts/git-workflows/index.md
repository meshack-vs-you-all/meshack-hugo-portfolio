---
title: "Git Workflows: Trunk-Based Development vs GitFlow"
date: 2026-02-08
draft: false
description: "Choosing the right branching strategy for your team. Feature branches, protection rules, and merging."
summary: "Should you use GitFlow or Trunk-Based Development? We analyze the pros and cons of modern version control strategies."
tags: ["Git", "Collaboration", "DevOps", "Workflow"]
series: ["DevOps Zero to Hero"]
featuredImage: "https://images.unsplash.com/photo-1556075798-4825dfaaf498?q=80&w=2076&auto=format&fit=crop"
layout: "simple"
---

{{< lead >}}
Git is more than `commit` and `push`. It's how teams communicate. Your branching strategy determines your deployment velocity.
{{< /lead >}}

## 1. GitFlow (The Old Way)

GitFlow involves two long-running branches: `main` and `develop`.

-   **Pros**: strict control, clear release versions.
-   **Cons**: Merge conflicts hell, slow deployment cycle.

## 2. Trunk-Based Development (The Modern Way)

Everyone pushes to `main` (or short-lived feature branches that merge to main within hours).

1.  Developer creates branch `feat/login-page`.
2.  Writes code.
3.  Opens PR.
4.  CI/CD runs tests.
5.  Code merges to `main`.
6.  `main` automatically deploys to Staging.

{{< mermaid >}}
gitGraph
   commit
   branch feature-A
   checkout feature-A
   commit
   commit
   checkout main
   merge feature-A
   commit
   branch feature-B
   checkout feature-B
   commit
   checkout main
   merge feature-B
   commit
{{< /mermaid >}}

## 3. Advanced Scenarios

### The `Interactive Rebase`

Before merging your branch, clean up your history.

```bash
# Combine the last 3 commits into one
git rebase -i HEAD~3
```

Change `pick` to `squash` for the commits you want to combine.

### The `Cherry Pick`

Need a specific hotfix from another branch without merging everything?

```bash
git cherry-pick <commit-hash>
```

### The "Oh No, I Committed to Main" Protocol

```bash
# 1. Reset main to the previous commit (keeping changes)
git reset --soft HEAD~1

# 2. Create a new branch
git checkout -b my-feature-branch

# 3. Commit there
git commit -m "Saved my work"
```

## 4. Branch Protection Rules

If you use GitHub, enable these settings on `main`:

*   [x] Require pull request reviews before merging.
*   [x] Require status checks to pass before merging (CI/CD).
*   [x] Require linear history (no merge commits, only rebase/squash).

## Comparison

| Feature | GitFlow | Trunk-Based |
| :--- | :--- | :--- |
| **Release Speed** | Slow (Scheduled) | Fast (Continuous) |
| **Complexity** | High | Low |
| **Ideal For** | Legacy Software | SaaS / Web Apps |

{{< badge >}}
Verdict: Use Trunk-Based
{{< /badge >}}
