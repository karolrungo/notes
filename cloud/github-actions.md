---
title: GitHub Actions - Introduction
created: 2026-05-14
tags: [devops, ci-cd, github, github-actions, learning]
status: learning
source: intro video
---
# GitHub Actions — Introduction

## What it is

A **workflow automation service** built into GitHub.
It lets me automate things that happen *around* my repository — not only CI/CD, but also repo management tasks (auto-labeling issues, requesting reviewers, closing stale PRs, posting comments, etc.).

## Why it matters

- Lets me build a **CI/CD pipeline** without setting up a separate tool (no Jenkins server to maintain).
- Tightly integrated with GitHub events (push, PR, issue, release…).
- Free quota for public repos, generous quota for private ones.

## Core building blocks (vocabulary I need to know)

| Term         | What it means                                                                               | Example                                                 |
| ------------ | ------------------------------------------------------------------------------------------- | ------------------------------------------------------- |
| **Event**    | Something that happens in the repo and triggers a workflow                                  | `push`, `pull_request`, `schedule`, `workflow_dispatch` |
| **Workflow** | A YAML file in `.github/workflows/` describing the automation                               | `ci.yml`                                                |
| **Job**      | A unit of work that runs on one machine. By default, all jobs in a workflow run in parallel | "build", "test", "deploy"                               |
| **Step**     | A single command or action inside a job                                                     | `npm install`, `terraform plan`                         |
| **Action**   | A reusable, pre-built block I can plug into a step                                          | `actions/checkout@v4`                                   |
| **Runner**   | The machine that executes a job                                                             | GitHub-hosted Ubuntu, or my own self-hosted runner      |

## Mental model

```
Event (push, PR, …)
   │
   ▼
Workflow (.github/workflows/xyz.yml)
   │
   ├── Job 1 (runs on Runner A)
   │     ├── Step 1 → uses an Action
   │     ├── Step 2 → runs a shell command
   │     └── Step 3 → …
   │
   └── Job 2 (runs on Runner B, maybe in parallel)
         └── Steps…
```

## What it can automate (examples)

- **CI/CD:** build, test, lint, security scan, deploy.
- **Repo hygiene:** auto-label PRs, request reviewers, close stale issues.
- **Release management:** draft release notes, publish artifacts, push Docker images.
- **Scheduled tasks:** nightly builds, dependency updates (Dependabot-like flows).

## Open questions / next to learn

- [ ] How does YAML syntax look in practice?
- [ ] How do secrets work (`secrets.MY_TOKEN`)?
- [ ] Difference between **GitHub-hosted** and **self-hosted** runners.
- [ ] How to share logic between workflows (reusable workflows, composite actions).
- [ ] How matrix builds work.

## See also

- [[ci-cd]]
- [[YAML basics]]